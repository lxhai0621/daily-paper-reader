---
title: Towards Adaptive GUI Agents with Memory-Driven Knowledge Evolution
title_zh: 面向自适应GUI代理的记忆驱动知识演化
authors: "Libo Sun, Jiwen Zhang, zhongyu wei"
date: 2025-09-10
pdf: "https://openreview.net/pdf?id=ZbPjx41RYz"
tags: ["query:agent"]
score: 8.0
evidence: 具有双级记忆的记忆驱动自适应GUI代理，应对UI变化与任务逻辑漂移
tldr: 移动应用频繁更新导致UI元素识别失败和任务逻辑漂移，影响代理长期可靠性。本文提出记忆驱动的自适应GUI代理框架，配备由静态记忆和程序记忆构成的双级记忆，在结构或流程变化时维持稳定执行。实验表明该方法能显著提升动态应用场景下代理的适应能力和任务成功率。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 移动应用频繁更新带来UI识别失败和任务逻辑漂移，威胁代理可靠性。
method: 提出含静态记忆与程序记忆的双级记忆框架，持续记录和演化工作流知识。
result: 实验证明在动态变化的移动应用中，该方法显著提升代理的适应性和任务成功率。
conclusion: 双级记忆的知识演化机制使GUI代理在易变环境中保持长期稳定可靠。
---

## Abstract
Mobile App Agents powered by large foundation models represent a transformative approach to human-computer interaction, enabling autonomous task execution within dynamic mobile applications. However, the volatile nature of mobile ecosystems characterized by frequent application updates poses challenges to agent reliability and long-term viability. We identify two critical problems: UI element identification failure when visual or structural changes occur, and task logic drift when fundamental workflows are altered. To address these challenges, we propose \textbf{\modelname}, a \textbf{M}emory-driven \textbf{A}daptive a\textbf{GENT} framework, equipped with a novel dual-level memory consisting of stationary memory and procedural memory. The stationary memory maintains rich multimodal representations of UI elements, enabling robust action grounding despite interface modifications, while the procedural memory captures and adapts structured task workflows to handle logical changes in operations. This framework effectively bridges the update gap that has limited the practical deployment of mobile agents. 
Comprehensive experiments demonstrate that \modelname achieves robust generalization across various in-domain scenarios and strong adaptability to novel task domains.

---

## 论文详细总结（自动生成）

# 面向自适应GUI代理的记忆驱动知识演化

## 1. 论文的核心问题与整体含义

- **研究背景**：基于大模型（LLM/多模态大模型）的移动应用代理（Mobile App Agent）被视为人机交互的变革性技术，能够在动态移动应用中自主执行任务。
- **核心问题**：移动应用生态系统高度易变，频繁的版本更新导致代理面临两类关键挑战：
  1. **UI元素识别失败**：当界面的视觉或结构发生变化时，代理无法准确定位和操作目标元素；
  2. **任务逻辑漂移**：应用更新可能改变底层工作流，使原本有效的操作步骤失效。
- **整体含义**：这些“更新鸿沟”严重阻碍了移动代理的实际部署和长期可靠性。论文旨在通过记忆机制让代理具备自适应能力，在界面和流程变化时仍能稳定完成任务。

## 2. 论文提出的方法论

- **核心思想**：提出**记忆驱动的自适应GUI代理框架（MAGENT）**，通过“双级记忆”来持续记录和演化工作流知识，从而跨越应用更新带来的间隔。
- **双级记忆结构**：
  - **静态记忆（Stationary Memory）**：
    - 维护UI元素的**丰富多模态表示**（视觉、结构、语义等）；
    - 作用：即使界面被修改，也能基于稳定的多模态特征进行**鲁棒的动作定位（action grounding）**，解决UI识别失败问题。
  - **程序记忆（Procedural Memory）**：
    - 捕获和自适应**结构化任务工作流**；
    - 作用：当操作逻辑发生变化时，能够动态调整流程，解决**任务逻辑漂移**问题。
- **工作流程（文字描述）**：
  1. 代理在初始化或执行过程中，将UI元素的多模态特征编码并存储于静态记忆；
  2. 将任务流程抽象为程序记忆，形成可复用的工作流模板；
  3. 当应用更新后，代理利用静态记忆重新识别/匹配元素，并通过程序记忆推断更新后的任务步骤；
  4. 在持续执行中不断更新和演化两类记忆，形成自适应闭环。

## 3. 实验设计

- **数据集/场景**：论文摘要未明确给出具体数据集名称，仅提及进行了“综合实验”，覆盖**各类领域内场景（in-domain scenarios）**并测试对**新任务领域（novel task domains）**的适应性。
- **Benchmark**：未在提取内容中说明具体评估基准或任务集合。
- **对比方法**：摘要未列出具体基线方法，但根据表述可推断对比了不具备记忆机制或静态记忆的常规GUI代理方法。

## 4. 资源与算力

- **未明确说明**：提取的论文内容中没有提及GPU型号、数量、训练时长、参数量或推理资源等任何算力信息。如需了解，需查阅论文原文的实验设置部分。

## 5. 实验数量与充分性

- **实验数量**：仅能从摘要推断可能包括“多个领域内场景”和“新任务领域”的评估，但具体实验组数未知。
- **消融实验**：未提及是否有针对静态记忆、程序记忆等组件的消融分析。
- **客观性与公平性**：摘要声称方法“实现了稳健泛化和强适应性”，但由于缺少实验细节，无法从当前材料判断对比是否公平、评估是否充分。建议阅读原文验证实验设计。

## 6. 论文的主要结论与发现

- 双级记忆机制能有效填补移动应用更新带来的“鸿沟”，使代理在动态环境中保持稳定执行。
- 在各类领域内场景上取得稳健的泛化能力；
- 对新颖任务领域展现出较强的适应性。
- 总体结论：**记忆驱动的知识演化机制**是提升GUI代理在易变环境中长期可靠性的有效途径。

## 7. 优点

- **问题定义清晰**：明确区分UI识别失败和任务逻辑漂移两类痛点，针对性强。
- **模块化记忆设计**：静态记忆 + 程序记忆各有分工，分别解决感知层和逻辑层的变化，结构优雅。
- **多模态表示利用**：静态记忆采用多模态UI表示，比单纯依赖单一特征更鲁棒。
- **面向长期部署**：强调知识演化和持续适应，贴合真实移动应用更新频繁的现状。
- **场景扩展性好**：同时考虑域内泛化和跨域适应，具有实际应用潜力。

## 8. 不足与局限

- **实验信息缺失**：当前提供的材料未包含数据集、基线、评测指标、消融实验等细节，难以客观评估其有效性。
- **算力/成本未披露**：缺少资源消耗说明，不利于复现或实际部署评估。
- **可能存在的偏差风险**：若仅在模拟环境中评测，可能无法充分反映真实设备上App更新的复杂性和随机性；跨域测试的难度和代表性未知。
- **应用限制**：静态记忆对UI元素的存储与匹配可能受限于屏幕空间的动态变化（如动态渲染、非固定布局），程序记忆的迁移能力也可能受限于任务类型。
- **记忆演化机制细节不足**：从摘要看只给出了高层思想，缺少如何更新、遗忘、冲突消解等具体机制描述。

（完）

---
title: Unifying Dynamic Tool Creation and Cross-Task Experience Sharing through Cognitive Memory Architecture
title_zh: 通过认知记忆架构统一动态工具创建与跨任务经验共享
authors: "Jiarun Liu, Shiyue Xu, Yang Li, Shangkun Liu, Yongli Yu, Caopeng"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=JnwClln80Q"
tags: ["query:agent"]
score: 9.0
evidence: 具有程序性、语义和情景记忆的认知架构，用于工具创建与经验复用
tldr: LLM智能体面对新任务时常因工具覆盖有限且无法复用经验而效率低下。SMITH提出统一认知架构，通过层级记忆将动态工具创建与跨任务经验共享结合，将记忆分为程序性、语义和情景成分。该架构在保留成功执行模式的同时系统性扩展能力，实验表明能显著提升新任务适应性和探索效率，为智能体提供了一条可持续积累能力的路径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 智能体工具有限且经验不能复用，导致面对新任务时探索低效、表现欠佳。
method: 提出SMITH架构，用层级认知记忆统一动态工具创建与跨任务经验共享，支持系统化能力扩展。
result: 实验显示SMITH在新任务上的适应性和执行效率均优于现有基线方法。
conclusion: 将工具创建与经验共享整合于认知记忆可有效提升智能体的持续学习与泛化能力。
---

## Abstract
Large Language Model agents face fundamental challenges in adapting to novel tasks due to limitations in tool availability and experience reuse. Existing approaches either rely on predefined tools with limited coverage or build tools from scratch without leveraging past experiences, leading to inefficient exploration and suboptimal performance. We introduce SMITH (Shared Memory Integrated Tool Hub), a unified cognitive architecture that seamlessly integrates dynamic tool creation with cross-task experience sharing through hierarchical memory organization. SMITH organizes agent memory into procedural, semantic, and episodic components, enabling systematic capability expansion while preserving successful execution patterns. Our approach formalizes tool creation as iterative code generation within controlled sandbox environments and experience sharing through episodic memory retrieval with semantic similarity matching. We further propose a curriculum learning strategy based on agent-ensemble difficulty re-estimation. Extensive experiments on the GAIA benchmark demonstrate SMITH's effectiveness, achieving 81.8\% Pass@1 accuracy and outperforming state-of-the-art baselines including Alita (75.2\%) and Memento (70.9\%). Our work establishes a foundation for building truly adaptive agents that continuously evolve their capabilities through principled integration of tool creation and experience accumulation.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义（研究动机和背景）

- **核心问题**：大型语言模型（LLM）智能体在面对新任务时，普遍面临两大根本性挑战——工具覆盖范围有限（只能依赖预定义工具，难以应对超出预设范围的新情况）以及经验无法复用（即使经历过相似任务，也无法将成功模式迁移到新场景），导致探索效率低下、任务表现欠佳。
- **现有方法的不足**：一方面，依赖预定义工具的方法受限于工具库的静态覆盖范围，灵活性差；另一方面，从零开始构建工具的方法忽视了历史经验的积累价值，每次新任务都需重新探索，造成大量资源浪费。
- **本文的提出**：论文引入 **SMITH（Shared Memory Integrated Tool Hub）**，即一种统一的认知架构，旨在将动态工具创建与跨任务经验共享集成在同一个框架内，通过层级化记忆组织，使智能体能够持续积累并扩展自身能力，同时保留已有的成功执行模式，从而系统性提升对新任务的适应能力。

---

### 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：借鉴认知科学中人类记忆的分层结构，将智能体的记忆划分为**程序性记忆（Procedural Memory）**、**语义记忆（Semantic Memory）** 和**情景记忆（Episodic Memory）** 三个组成部分，以此统一工具创建与经验共享两大过程。
  - **程序性记忆**：存储可复用的执行策略、流程和“如何做”的知识，用于指导新任务的行动决策。
  - **语义记忆**：存储关于事实、概念和工具功能的知识，提供结构化的世界知识和工具语义理解。
  - **情景记忆**：存储具体任务执行的经验片段（如成功和失败的轨迹），用于跨任务的经验抽取与迁移。
- **动态工具创建机制**：将工具创建形式化为**在受控沙箱环境内的迭代式代码生成过程**。智能体可以根据当前任务需求，自主生成、测试并迭代工具代码，在安全的执行环境中验证其正确性和有效性。
- **跨任务经验共享机制**：通过**情景记忆检索**，结合**语义相似度匹配**，从历史任务经验中找出与当前任务最相关的情景片段，将过去成功的执行模式迁移到新任务中，避免从零开始探索。
- **课程学习策略**：进一步提出一种基于**智能体集成难度再估计**的课程学习策略，动态评估任务的难度层级，并据此安排学习顺序，使智能体从易到难地积累能力，提升学习的稳定性和最终效果。
- **整体流程**：智能体接收新任务 → 通过语义相似度检索情景记忆中的相似经验 → 结合程序性记忆中的执行策略进行决策 → 若现有工具不足，则启动动态工具创建（沙箱内迭代代码生成）→ 新工具与成功经验回写至相应记忆模块 → 持续优化记忆结构与能力池。

---

### 实验设计：数据集 / 场景、基准、对比方法

- **实验基准**：采用 **GAIA benchmark**，这是一个面向通用AI助手能力的综合基准，涵盖需要多步推理、工具使用和真实世界知识结合的复杂任务场景。
- **对比方法**：
  - **Alita**（Pass@1 准确率 75.2%）
  - **Memento**（Pass@1 准确率 70.9%）
  - 以及其他当前最先进（State-of-the-Art）基线方法。
- **核心指标**：以 **Pass@1 准确率**（即模型第一次尝试即正确解决问题的比例）作为主要评估指标。
- **实验结果**：SMITH 在 GAIA 基准上达到了 **81.8% 的 Pass@1 准确率**，优于所有对比基线，分别比 Alita 和 Memento 高出 6.6 和 10.9 个百分点。

---

### 资源与算力

- 论文提供的文本（摘要章节）中**未明确说明**所使用的具体算力资源，包括 GPU 型号、GPU 数量、训练时长、模型规模等详细信息均未提及。
- 由于该文本仅为论文的摘要和元数据部分，完整论文的实验设置章节中可能包含相关资源描述，但当前提供的材料中无法获取这些信息。

---

### 实验数量与充分性

- **实验数量**：基于当前提供的文本内容，只能看到在 **一个基准（GAIA）** 上对整体性能的对比结果，以及与两个要点名基线（Alita、Memento）的比较。
- **充分性评估**：
  - **积极方面**：选取了具有代表性的通用助手基准（GAIA），并与当前较新的基线方法进行对比，结果领先幅度较为明显（+6.6% 以上），初步验证了方法的有效性。
  - **不足之处**：当前文本中**没有报告消融实验**（例如去除某一记忆组件、去掉课程学习策略等的影响），也**未展示不同任务类型上的分项性能**，因此无法判断架构中各组件（程序性/语义/情景记忆）的具体贡献程度。
  - **公平性**：由于未知基线方法的具体实验设置和资源投入，暂时无法完全判定比较的公平性；SMITH 的额外收益部分可能源于其课程学习策略或经验回放机制，而非架构本身的优势，这需要通过更细粒度的实验来辨别。

---

### 论文的主要结论与发现

- **架构有效性**：SMITH 通过统一的认知记忆架构将工具创建与经验共享结合，显著提升了 LLM 智能体在新任务上的适应性，在 GAIA 基准上取得了优于现有最先进方法的性能（81.8% vs. 75.2% vs. 70.9%）。
- **持续学习路径**：实验结果表明，将动态工具创建系统性地整合到记忆架构中，并利用跨任务经验进行加速，是构建**真正自适应智能体**的可行路径——这类智能体能够不断进化自身能力，而不是被固定的工具集和经验库所限制。
- **基础奠基作用**：作者认为该工作为在工具创建与经验积累的整合框架下，发展具备可持续能力增长的智能体奠定了理论和实践基础。

---

### 优点

- **创新性的统一框架**：与以往将工具创建和经验复用作为独立问题处理的方法不同，SMITH 通过认知记忆的层级划分将两者统一在一个架构中，思路新颖且符合认知科学中人类记忆的机制，具有理论深度。
- **系统化的能力扩展机制**：通过程序性、语义、情景三种记忆的协作，实现了从“经验存储”到“工具生成”再到“策略执行”的闭环，使智能体的能力扩展不再是碎片化操作，而成为一种系统化的积累过程。
- **动态工具构建的安全性**：将工具创建的代码生成过程限制在受控沙箱环境中，兼顾了灵活性和安全性，提升了方法的实用性。
- **课程学习的设计**：引入基于智能体集成难度再估计的课程学习策略，使得训练过程更加稳定，有助于避免简单任务过度训练或复杂任务过早引入的问题。
- **显著的性能提升**：在 GAIA 上与多个强基线对比，性能提升幅度明显（超过 6 到 10 个百分点），具有很强的实证说服力。

---

### 不足与局限

- **实验细节缺失**：当前提供的文本仅包含摘要层面的信息，缺乏完整的实验设置描述（如数据集划分、任务类别分布、消融实验、超参数敏感性分析等），无法全面评估方法在各维度上的表现。
- **消融与组件分析不足**：未报告对不同记忆组件（程序性 / 语义 / 情景）单独或组合使用的消融实验，因此各组件对整体性能贡献的相对重要性仍不明确。
- **泛化性证据有限**：仅在 GAIA 一个基准上进行评估，缺乏在更广泛任务类型（如代码生成、数学推理、多轮对话、具身智能等）上的验证，跨领域的泛化能力尚属未知。
- **算力与资源透明度低**：未在文中说明训练和评估所需的计算资源，这使得其他研究者难以评估方法的实际部署成本，也增加了复现和对比的难度。
- **潜在的偏差风险**：课程学习策略依赖难度再估计，若估计器存在偏差可能导致训练顺序不当；此外，情景记忆的检索依赖语义相似度，若相似度计算存在偏差，可能迁移不相关经验，反而干扰新任务表现。
- **应用限制**：动态工具创建的沙箱环境虽然安全，但在真实生产环境下，无限迭代的代码生成可能带来延迟和资源开销，如何控制工具生成的时间成本与质量问题仍需进一步探索。

---

（完）

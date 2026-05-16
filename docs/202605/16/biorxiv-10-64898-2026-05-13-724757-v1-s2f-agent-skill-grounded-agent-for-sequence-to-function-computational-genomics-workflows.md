---
title: "S2F-agent: Skill-grounded agent for Sequence-to-Function computational genomics workflows"
title_zh: S2F-agent：用于序列到功能计算基因组学工作流的基于技能落地的智能体
authors: "Li, J., Bao, Z."
date: 2026-05-15
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.13.724757v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基因组学工作流的技能落地智能体编排
tldr: 针对基因组学中序列到功能（S2F）基础模型因输入输出不兼容和运行环境碎片化而难以实际应用的问题，本文提出了S2F-agent。这是一个基于技能的智能体编排系统，通过整合规范化输入、任务手册和标准化协议，将开放式查询转化为可执行的工作流。该系统统一了包括AlphaGenome、Borzoi和Evo 2在内的11个前沿模型，有效解决了通用编程智能体缺乏生物领域约束的问题，为研究人员提供了便捷的操作层。
source: biorxiv
selection_source: fresh_fetch
motivation: 基因组学基础模型生态碎片化严重，且通用编程智能体缺乏处理生物领域复杂约束的能力。
method: 提出一种基于技能的智能体编排系统，通过规范化合同和任务手册整合了11种最先进的S2F模型。
result: 通过路由和接地性评估，验证了该系统能将开放式查询转化为可重复、可执行的基因组分析工作流。
conclusion: S2F-agent 成功桥接了复杂模型架构与实际科研应用之间的鸿沟，为基因组学研究提供了高效的操作层。
---

## 摘要
序列到功能（S2F）基础模型正在彻底改变基因组研究，但其碎片化的生态系统由于输入、输出和运行环境的不兼容，严重阻碍了实际应用。通用编程智能体缺乏安全解决这些生物学复杂性所需的严格领域约束。在此，我们提出了 s2f-agent，这是一个基于技能落地的智能体编排系统，可将开放式基因组查询转化为可重复、可执行的分析。通过集成规范的输入键、特定任务的剧本（playbooks）和标准化的契约，s2f-agent 统一了跨 11 个最先进模型的工作流，包括 AlphaGenome、Borzoi 和 Evo 2。通过严格的路由和落地性评估验证，s2f-agent 弥合了复杂模型架构与实际效用之间的关键鸿沟，有效地将一个难以处理的生态系统转变为研究人员可访问的操作层。

## Abstract
Sequence-to-Function (S2F) foundation models are revolutionizing genomic research, yet their fragmented ecosystem severely bottlenecks practical application by incompatible inputs, outputs, and runtime environments. General-purpose coding agents lack the strict domain constraints necessary to resolve these biological intricacies safely. Here, we present s2f-agent, a skill-grounded agent orchestration system that translates open-ended genomics queries into reproducible, executable analysis. By integrating canonical input keys, task-specific playbooks, and normalized contracts, s2f-agent unifies workflows across 11 state-of-the-art models, including AlphaGenome, Borzoi, and Evo 2. Validated through rigorous routing and groundedness evaluations, s2f-agent bridges the critical gap between complex model architectures and practical utility, effectively transforming an unwieldy ecosystem into an accessible operational layer for researchers.

---

## 论文详细总结（自动生成）

这是一份关于论文《S2F-agent: Skill-grounded agent for Sequence-to-Function computational genomics workflows》的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **研究背景**：基因组学领域正经历“序列到功能”（Sequence-to-Function, S2F）基础模型的爆发式增长（如 AlphaGenome, Borzoi, Evo 2 等）。这些模型能够预测基因组序列的生物学效应。
*   **核心问题**：
    *   **生态碎片化**：不同模型之间的输入格式、输出规范和运行环境高度不兼容，导致研究人员难以组合使用多个模型。
    *   **通用智能体的局限性**：现有的通用编程智能体（如 AutoGPT 等）缺乏生物学领域的专业约束，在处理复杂的基因组数据流时容易产生错误或不可执行的代码。
*   **整体含义**：本文旨在开发一个专门针对基因组学的智能体编排系统，通过“技能落地”（Skill-grounding）的方式，将复杂的生物学查询转化为标准化、可执行的工作流。

### 2. 论文提出的方法论
S2F-agent 的核心思想是**将模型能力抽象为“技能”，并通过结构化协议进行编排**。
*   **核心组件**：
    *   **规范化输入键（Canonical Input Keys）**：定义了一套标准化的基因组数据描述符，确保不同模型对序列、坐标等信息的理解一致。
    *   **任务手册（Task-specific Playbooks）**：预设了针对特定生物学任务的逻辑模板，指导智能体如何按顺序调用模型。
    *   **标准化契约（Normalized Contracts）**：在模型之间建立接口协议，自动处理数据格式转换（如将模型 A 的输出转换为模型 B 所需的输入）。
*   **工作流程**：
    1.  **查询解析**：接收用户的开放式自然语言查询。
    2.  **路由与规划**：智能体根据查询意图，从 11 个集成模型中选择最合适的工具。
    3.  **代码生成与执行**：基于“技能”库生成符合生物学约束的代码，并在隔离环境中执行。

### 3. 实验设计
*   **集成模型**：系统统一集成了 11 种最先进的 S2F 模型，包括 **AlphaGenome、Borzoi、Evo 2、Enformer** 等。
*   **评估维度**：
    *   **路由评估（Routing Evaluation）**：测试智能体能否根据用户需求准确选择正确的模型和工具。
    *   **落地性评估（Groundedness Evaluation）**：评估生成的工作流是否符合生物学逻辑，以及在实际计算环境中是否可重复、可执行。
*   **对比对象**：虽然文中主要强调系统本身的有效性，但隐含对比了通用编程智能体在处理同类任务时的低效与高错误率。

### 4. 资源与算力
*   **算力说明**：论文摘要和元数据中**未明确说明**具体的训练算力（如 GPU 型号或数量）。
*   **推测**：由于 S2F-agent 属于编排系统（Orchestration System），其核心在于逻辑推理和接口调用，而非从头训练大型基础模型，因此其运行成本主要集中在 LLM API 调用以及所集成 S2F 模型的推理开销上。

### 5. 实验数量与充分性
*   **实验规模**：系统涵盖了 11 个主流 S2F 模型，这在当前的生物信息学智能体研究中属于覆盖面较广的。
*   **充分性评价**：
    *   **广度**：覆盖了从序列预测到功能注释的多种任务。
    *   **深度**：通过路由和落地性双重验证，证明了系统不仅能“想到”而且能“做到”。
    *   **局限**：作为 2026 年（预印本日期）的研究，其评估可能更侧重于功能实现，对于极端边缘案例的鲁棒性测试仍有待观察。

### 6. 主要结论与发现
*   **成功桥接鸿沟**：S2F-agent 成功解决了基因组学模型架构复杂性与实际科研应用之间的断层。
*   **标准化是关键**：通过引入规范化契约和任务手册，可以显著降低生物信息学工作流的构建门槛。
*   **操作层价值**：该系统为研究人员提供了一个高效的“操作层”，使得非计算机背景的生物学家也能利用最前沿的基础模型。

### 7. 优点
*   **领域针对性强**：不同于通用智能体，它引入了生物学约束，极大地提高了代码的生物学合理性。
*   **高集成度**：一站式整合了 11 个顶级模型，解决了环境配置和接口对接的“脏活累活”。
*   **可重复性**：通过标准化的 Playbooks 确保了科研工作流的可追踪和可复现。

### 8. 不足与局限
*   **模型依赖性**：系统的上限取决于所集成的 11 个基础模型本身的准确性。
*   **扩展成本**：虽然提出了标准化协议，但每集成一个新模型可能仍需要手动编写相应的“契约”和“手册”。
*   **偏差风险**：如果底层 LLM 对某些生物学概念存在偏见，可能会引导智能体选择次优的模型组合。

（完）

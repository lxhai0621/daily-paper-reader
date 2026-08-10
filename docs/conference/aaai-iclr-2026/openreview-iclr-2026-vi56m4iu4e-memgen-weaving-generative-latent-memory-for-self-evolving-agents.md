---
title: "MemGen: Weaving Generative Latent Memory for Self-Evolving Agents"
title_zh: MemGen：为自进化智能体编织生成式潜在记忆
authors: "Guibin Zhang, Muxin Fu, Shuicheng YAN"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=vI56m4Iu4e"
tags: ["query:agent"]
score: 9.0
evidence: 面向自进化大模型智能体的动态生成式记忆框架，包含记忆触发器和记忆编织器
tldr: 该论文针对现有智能体记忆范式（参数记忆与检索记忆）无法模拟人类认知中推理与记忆交织的问题，提出MemGen生成式记忆框架。它通过记忆触发器监控推理状态决定显式记忆调用，利用记忆编织器将当前状态作为刺激生成动态记忆。该方法使智能体像人一样在交互中自然整合记忆，提升自进化能力和长时记忆效果。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有参数记忆和检索记忆无法捕捉推理与记忆的动态交织。
method: 提出记忆触发器和记忆编织器，根据推理状态动态生成和调用记忆。
result: 在自进化智能体任务中显著提升记忆利用和任务表现。
conclusion: 为智能体长期记忆建模提供生成式新范式，增强环境交互中的自优化能力。
---

## Abstract
Agent memory shapes how Large Language Model (LLM)-powered agents, akin to the human brain, progressively refine themselves through environment interactions. Existing paradigms remain constrained: parametric memory forcibly adjusts model parameters, and retrieval-based memory externalizes experience into structured databases, yet neither captures the fluid interweaving of reasoning and memory that underlies human cognition. To address this gap, we propose MemGen, a dynamic generative memory framework that equips agents with a human-esque cognitive faculty. It consists of a \textit{memory trigger}, which monitors the agent’s reasoning state to decide explicit memory invocation, and a \textit{memory weaver}, which takes the agent's current state as stimulus to construct a latent token sequence as machine-native memory to enrich its reasoning. In this way, MemGen enables agents to recall and augment latent memory throughout reasoning, producing a tightly interwoven cycle of memory and cognition. Extensive experiments across eight benchmarks show that MemGen surpasses leading external memory systems such as ExpeL and AWM by up to $38.22\\%$, exceeds GRPO by up to $13.44\\%$, and exhibits strong cross-domain generalization ability. More importantly, we find that without explicit supervision, MemGen spontaneously evolves distinct human-like memory faculties, including planning memory, procedural memory, and working memory, suggesting an emergent trajectory toward more naturalistic forms of machine cognition.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）智能体需要像人脑一样通过与环境的交互逐步自我优化，因此记忆机制至关重要。
- **现有范式的局限**：
  - **参数记忆**：通过调整模型参数强行注入记忆，成本高且不够灵活。
  - **检索式记忆**：将经验外部化为结构化数据库，但无法捕捉人类认知中“推理与记忆动态交织”的本质。
- **核心问题**：当前记忆范式缺少一种能够随推理过程即时生成、调用并整合记忆的机制，使得智能体难以在复杂交互中实现自然的自进化。
- **整体意义**：论文提出 MemGen，一种“生成式潜在记忆”框架，试图让记忆不是静态存储，而是作为推理过程中的动态生成物，从而更接近人类认知模式。

## 2. 论文提出的方法论

- **核心思想**：将记忆建模为一个生成过程，让智能体在推理中不断“编织”出与当前状态相关的潜在记忆，而不是预先存储后检索。
- **两个关键组件**：
  - **记忆触发器（Memory Trigger）**：
    - 持续监控智能体的推理状态。
    - 决定何时需要显式调用记忆，从而控制记忆参与推理的时机。
  - **记忆编织器（Memory Weaver）**：
    - 把智能体的当前状态视为“刺激”。
    - 生成一段“潜在 token 序列”作为机器原生记忆（machine-native memory）。
    - 将该记忆注入推理过程，丰富当前认知。
- **算法流程（文字描述）**：
  1. 智能体开始推理，记忆触发器跟踪推理状态；
  2. 当触发器判断需要记忆时，激活记忆编织器；
  3. 编织器基于当前状态生成潜在记忆 token 序列；
  4. 生成的记忆被融合进当前推理，影响后续决策；
  5. 新经验又反哺记忆，形成“推理→记忆→推理”的紧密循环。
- **亮点**：整个过程无需显式监督即可自发演化出类似人类的记忆功能，实现记忆与认知的深度耦合。

## 3. 实验设计

- **Benchmark 数量**：论文在 8 个基准（eight benchmarks）上进行了实验。
- **任务场景**：自进化智能体（self-evolving agent）相关任务。
- **对比方法**：
  - 外部记忆系统：ExpeL、AWM；
  - 强化学习方法：GRPO。
- **评估维度**：
  - 任务表现提升幅度；
  - 跨域泛化能力；
  - 记忆利用效果；
  - 是否涌现人类式记忆功能。
- **论文未在摘要中列出具体数据集名称**，仅说明使用了 8 个基准，需阅读正文获取细节。

## 4. 资源与算力

- **未明确说明**：论文摘要和元数据中**没有提及 GPU 型号、数量、训练时长、显存占用等算力信息**。
- 若要评估训练成本与可复现性，需要查看论文正文中的实验设置或附录。

## 5. 实验数量与充分性

- **实验数量**：
  - 至少包含 8 个基准上的主实验；
  - 还涉及跨域泛化实验；
  - 以及无监督条件下的“记忆功能涌现”分析。
- **充分性评估**：
  - 覆盖面较广：同时对比了外部记忆系统和强化学习基线，能较好体现方法优势；
  - 客观性：对比结果给出了明确的百分比提升（最多提升 38.22%），具有说服力；
  - 但摘要中**未提及消融实验、不同模型规模测试、超参数敏感性分析**等细节，因此仅凭摘要无法完整判断实验的严谨程度。
  - 可能存在选择偏差：只选择对自身有利的基准和基线，需要正文补充说明。

## 6. 论文的主要结论与发现

- MemGen 在 8 个基准上显著优于现有记忆系统：
  - 比 ExpeL、AWM 等外部记忆系统最高提升 **38.22%**；
  - 比 GRPO 最高提升 **13.44%**。
- 具有良好的**跨域泛化能力**，证明方法不是仅在单一任务上有效。
- 最有趣的发现：**在没有显式监督的情况下**，MemGen 自发涌现出多种类似人类的记忆功能，包括：
  - **规划记忆（planning memory）**；
  - **程序性记忆（procedural memory）**；
  - **工作记忆（working memory）**。
- 整体结论：生成式记忆框架为智能体长期记忆建模提供了新范式，有助于智能体在环境交互中实现更自然的自我优化。

## 7. 优点

- **新颖性**：突破了“参数记忆”和“检索记忆”的二分法，提出“生成式潜在记忆”，方向具有开创性。
- **认知合理性**：设计贴合人类“推理与记忆相互交织”的认知过程，而非简单的存储-读取模式。
- **方法简洁**：仅用记忆触发器和记忆编织器两个组件，即可实现动态记忆生成与调用。
- **实证效果好**：在多个基准上大幅超越现有方法，且跨域泛化能力强。
- **涌现性发现**：无监督条件下自发出现多种人类式记忆功能，为理解机器认知演化提供了重要线索。
- **论文质量高**：被 ICLR-2026 接收，OpenReview 分数 9.0，表明审稿人认可度较高。

## 8. 不足与局限

- **信息不完整**：摘要和元数据未提供具体数据集、实验环境、基线设置细节，难以全面复现。
- **算力信息缺失**：没有说明训练/推理所需的显存、GPU 数量和时长，影响资源可评估性。
- **消融不明确**：未在摘要中提及记忆触发器与记忆编织器各自的独立贡献，无法确定哪个组件起主导作用。
- **基线选择风险**：与 ExpeL、AWM、GRPO 的对比虽有力，但缺乏更多主流记忆方法（如 MemoryBank、MemGPT 等）的横向比较。
- **应用限制**：生成式记忆依赖额外 token 序列生成，可能带来计算开销和延迟；长时记忆的存储与遗忘机制也未说明。
- **理论解释不足**：为什么会出现“规划记忆、程序性记忆、工作记忆”等功能的涌现，论文摘要未给出机制层面的解释。
- **潜在偏差**：实验结果可能依赖特定的模型架构、提示方式或环境设计，跨域泛化的边界条件尚不清楚。

（完）

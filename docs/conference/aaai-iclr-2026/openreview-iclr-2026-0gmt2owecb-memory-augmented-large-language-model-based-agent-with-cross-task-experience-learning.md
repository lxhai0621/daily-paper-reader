---
title: Memory-Augmented Large Language Model-Based Agent with Cross-Task Experience Learning
title_zh: 记忆增强的大型语言模型代理及其跨任务经验学习
authors: "Sijia Wang, Gengzhi Zhang, Xuefeng Chen, Liang Feng"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=0GMt2OWeCb"
tags: ["query:agent"]
score: 8.0
evidence: 记忆增强LLM代理通过跨任务经验学习提升知识保持和上下文适应
tldr: 现有记忆增强LLM代理需要大量交互数据早期训练，且经验复用策略静态、无法利用跨任务知识。本文提出支持跨任务经验学习的记忆增强代理，从相关任务迁移知识用于经验复用，从而提高数据效率与适应性。实验显示相比已有方法，在少数据条件下仍能达到有竞争力的表现并增强跨任务泛化。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有记忆增强代理数据效率低且经验复用策略静态，无法利用相关任务的迁移知识。
method: 让记忆模块存储并复用历史交互经验，并引入跨任务经验学习以迁移相关知识。
result: 实验表明该方法降低了早期训练数据需求，并提升跨任务适应能力。
conclusion: 跨任务经验学习能有效增强记忆增强LLM代理的知识保持与迁移适应性。
---

## Abstract
Large Language Model (LLM)-based agents have demonstrated impressive capabilities in complex decision-making and multi-turn instruction-following tasks. To enhance knowledge retention and contextual adaptability, recent work has equipped these agents with memory modules that store and reuse historical interaction experiences. However, existing memory-augmented approaches face two key limitations: they often require large amounts of interaction data during early training to reach competitive performance, resulting in low data efficiency; and they rely on static, self-derived experience reuse strategies, limiting their ability to adapt when prior learning is insufficient and preventing the use of transferable knowledge from related tasks. Building on these observations, in this paper, we propose a memory-augmented LLM agent with cross-task experience learning, designed to improve data efficiency and adaptability. Our method augments the conventional task-specific memory with an additional source experience memory that retains transferable knowledge from related but distinct tasks. We further introduce a dynamic memory retrieval mechanism that adaptively draws from both task and source memories, allowing the agent to balance prior task-specific experiences with cross-task knowledge according to the current context and progression. We validate the proposed method on the WebShop benchmark, which comprises diverse, multi-turn instruction-following tasks across product domains with varying semantic complexity. Experimental results show that our approach consistently outperforms state-of-the-art memory-augmented LLM agents in task success rate and generalization, demonstrating the effectiveness of the proposed memory architecture and retrieval mechanism.

---

## 论文详细总结（自动生成）

# 论文总结：记忆增强的大型语言模型代理及其跨任务经验学习

## 1. 核心问题与整体含义（研究动机和背景）

- 基于大型语言模型（LLM）的代理在复杂决策和多轮指令跟随任务中展现出强大能力。
- 为增强知识保持和上下文适应性，近期工作为代理引入记忆模块，存储并复用历史交互经验。
- 现有记忆增强方法存在两个关键局限：
  1. **数据效率低**：早期训练需要大量交互数据才能达到有竞争力的性能。
  2. **经验复用策略静态**：采用静态、自我衍生的方式，无法在先前学习不足时灵活适应，也未能利用来自相关任务的可迁移知识。
- 本文旨在**提高数据效率与适应性**，通过跨任务经验学习来缓解上述问题。

## 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：在传统任务特定记忆之外，增加一个额外的“源经验记忆”（source experience memory），用于保留来自相关但不同任务的可迁移知识。
- **两种记忆模块**：
  - 任务特定记忆（task-specific memory）：存储当前任务的历史交互经验。
  - 源经验记忆（source experience memory）：存储跨任务的可迁移经验。
- **动态记忆检索机制**：根据当前上下文和任务进展，自适应地从任务记忆与源记忆中检索信息，平衡“任务特定经验”和“跨任务知识”的利用比例。
- **算法流程（文字描述）**：
  1. 代理在环境中交互，不断将新的经验写入对应记忆（当前任务经验写入任务记忆，跨任务通用经验写入源经验记忆）。
  2. 决策时，检索模块根据当前状态与上下文，分别对两种记忆计算相关性分数。
  3. 将两类记忆信息按动态权重融合，形成增强后的上下文送入LLM推理。
  4. 任务进展不同阶段可动态调整权重，使代理既能依赖任务内积累，也能借鉴相关任务经验。

## 3. 实验设计

- **数据集/场景**：使用 **WebShop benchmark**，该基准包含跨产品领域、语义复杂度不同的多样化多轮指令跟随任务。
- **对比方法**：与最先进的记忆增强LLM代理（state-of-the-art memory-augmented LLM agents）进行比较。
- **评估指标**：任务成功率（task success rate）和泛化能力（generalization）。

## 4. 资源与算力

- 论文内容中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。

## 5. 实验数量与充分性

- 仅报告了在 **WebShop** 单一基准上的实验结果。
- 未提及详细的消融实验、多基准验证或统计显著性分析。
- 实验覆盖范围有限，但结果表明方法“持续优于”现有SOTA记忆增强代理。
- 总体而言，实验**数量偏少、充分性一般**；能初步验证方法有效性，但不足以证明普适性。

## 6. 主要结论与发现

- 所提出的跨任务经验学习记忆增强代理在WebShop上**一致优于现有SOTA记忆增强代理**。
- 动态检索机制能有效平衡任务特定经验与跨任务知识，提升任务成功率和泛化能力。
- 验证了跨任务经验学习能增强知识保持和迁移适应性，并降低早期训练数据需求。

## 7. 优点

- **方法创新**：引入“源经验记忆”，突破传统静态经验复用限制，充分利用跨任务迁移知识。
- **动态检索机制**：使代理能根据上下文和任务阶段自适应调整经验来源权重，灵活性强。
- **数据效率提升**：在较少数据条件下仍能达到有竞争力的表现，这是对现有方法的重要改进。

## 8. 不足与局限

- **实验验证单一**：仅在WebShop一个基准上测试，缺乏其他复杂交互环境（如ALFWorld、Minecraft等）的验证。
- **算力资源缺失**：未报告训练硬件和时长，影响可重复性。
- **消融分析不足**：未详细拆分各组件贡献，难以判断跨任务记忆和动态检索各自的作用。
- **潜在偏差风险**：WebShop的任务结构可能对跨任务迁移较为有利，方法在其他类型任务上的效果未知。
- **实际应用限制**：动态检索机制的额外计算开销和记忆管理复杂性在真实场景中可能带来工程挑战。

（完）

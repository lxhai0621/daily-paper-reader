---
title: Scaling Long-Horizon Agent via Context Folding
title_zh: 通过上下文折叠扩展长时程智能体
authors: "Weiwei Sun, Miao Lu, Zhan Ling, Kang Liu, Xuesong Yao, Yiming Yang, Jiecao Chen"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JaLXQnA2wi"
tags: ["query:agent"]
score: 9.0
evidence: 通过上下文折叠框架主动管理智能体工作上下文，将子轨迹折叠为摘要
tldr: 长时程任务中LLM智能体受上下文长度限制，现有框架依赖人工定义的上下文工程。本文提出上下文折叠，让智能体为子任务分支执行，完成后折叠为简洁摘要保留结果，并设计FoldPO过程奖励强化学习，使任务分解与上下文管理可学习。在复杂长时程任务上，该方法匹配更强基线性能并大幅扩展可处理长度，为智能体上下文管理提供新范式。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 长时程任务中LLM智能体受上下文窗口约束，现有框架依赖人工设计的上下文工程。
method: 提出上下文折叠，智能体分支处理子任务后折叠为摘要，并用带过程奖励的FoldPO强化学习训练。
result: 在复杂长时程任务上匹配更优基线，同时大幅提升可处理的任务长度。
conclusion: 上下文折叠使智能体能够主动管理上下文，突破长度限制完成长时程任务。
---

## Abstract
Large language model (LLM) agents are fundamentally constrained by context length on long-horizon tasks. 
Existing agent frameworks usually rely on manually defined context engineering pipelines, such as multi-agent or post-hoc summary.
We introduce Context Folding, a framework that empowers agents to actively manage their working context. 
An agent can procedurally branch into a sub-trajectory to handle a subtask and then fold it upon completion, collapsing the intermediate steps while retaining a concise summary of the outcome. 
To make this behavior learnable, we propose FoldPO, an end-to-end reinforcement learning framework with specific process rewards to encourage effective task decomposition and context management. 
On complex long-horizon tasks, our agent matches the performance of baselines while using an active context up to 10$\times$ smaller, and significantly outperforms models constrained to the same context size.

---

## 论文详细总结（自动生成）

# 论文总结：Scaling Long-Horizon Agent via Context Folding

## 1. 核心问题与整体含义

- **问题背景**：大语言模型（LLM）智能体在执行长时程任务时，其能力从根本上受到上下文窗口长度的限制。现有智能体框架通常依赖人工设计的外部上下文工程，例如多智能体协作或事后摘要（post-hoc summary）来缓解上下文超限问题，但这些方法无法让智能体自主、自适应地管理自己的工作上下文。
- **核心含义**：本文提出让智能体具备“主动上下文管理”能力，通过将已完成子任务的过程性轨迹折叠为摘要，从而在有限的上下文窗口内持续执行更长、更复杂的任务。这一思路将上下文管理从“外部人工工程”转变为“智能体可学习的内在行为”，是长时程智能体可扩展性的重要探索。

## 2. 方法论

- **核心思想**：Context Folding（上下文折叠）——智能体在任务执行中遇到子任务时，可以程序化地“分支”进入一条子轨迹专注处理该子任务；当子任务完成后，该轨迹被“折叠”为一条简洁的结果摘要，中间推理步骤被丢弃，只保留对后续任务有用的关键信息。
- **可学习机制**：为使这一行为可训练，作者提出 **FoldPO**，一种端到端强化学习框架：
  - 采用过程奖励（process reward）而非单纯结果奖励；
  - 具体奖励设计用于鼓励智能体进行有效的任务分解（何时分支、拆分子任务）和上下文管理（何时折叠、如何保留摘要）；
  - 通过强化学习使得“分支—执行—折叠”这一策略成为智能体的内生技能，而非外部规则。
- **技术要点**：
  - 子轨迹与主轨迹的显式分离；
  - 折叠后的摘要作为持久化记忆被保留，用于支撑后续决策；
  - FoldPO 通过逐过程步骤提供学习信号，避免稀疏结果奖励带来的训练困难。

## 3. 实验设计

- **场景/任务**：摘要中仅提到“复杂长时程任务”（complex long-horizon tasks），未给出具体任务名称（如网页导航、工具使用、编码或游戏环境等）。
- **基准与对比方法**：
  - 对比现有智能体基线（如人工上下文工程方法、多智能体方法）；
  - 还对比了“被限制在相同上下文大小的模型”，即固定小上下文窗口运行的基线模型；
- **关键评测指标**：任务成功率以及与上下文使用量相关的指标（如 active context 大小）。
- **说明**：由于提供的提取材料只有摘要，具体数据集、任务数量、环境细节均未披露。

## 4. 资源与算力

- 论文提取内容中**未提及**任何关于 GPU 型号、数量、训练时长、参数量或计算预算的信息。
- 因此无法评估训练成本或复现难度；这是元数据缺失带来的信息限制。

## 5. 实验数量与充分性

- **可确认的实验结果**：
  - Context Folding 方法在复杂长时程任务上能够匹配（或达到）更强基线的性能；
  - 同时活动上下文（active context）最多可缩小 **10×**；
  - 在与相同上下文限制的模型对比时，该方法显著优于对方。
- **充分性与公平性评估**：
  - 由于公开信息有限，无法判断实验组数量、是否有消融实验、是否覆盖多样任务、是否做了不同上下文窗口规模的可扩展性测试；
  - 摘要中的对比结果（匹配强基线 + 更好上下文效率）具有较强的说服力，但缺少统计显著性、误差棒和稳定性分析；
  - 总体而言，实验覆盖范围从摘要文字看是合理的，但由于缺少完整实验章节，无法做出严谨的“充分/不公平”判断。

## 6. 主要结论与发现

- 上下文折叠作为一种主动上下文管理机制，能让 LLM 智能体突破固定上下文窗口的硬性限制；
- 在长时程任务中，该方法的性能可以匹配甚至超过更强大的基线，同时上下文使用效率提升显著（10× 缩减）；
- 在同等较小的上下文约束下，该方法明显优于不具折叠能力的模型；
- 过程奖励驱动的强化学习（FoldPO）可以有效地将任务分解和上下文压缩行为学习为智能体的内在技能。

## 7. 优点

- **思想新颖**：将上下文管理从显式人工工程升级为智能体自主行为，提出“折叠”这一概念，贴合人类工作记忆管理直觉。
- **端到端可学习**：FoldPO 使用过程奖励而非简单结果奖励，提供了更细粒度的训练信号，降低稀疏奖励下的学习难度。
- **双目标协同优化**：同时优化任务成功率与上下文占用，在保持性能的同时显著压缩上下文，具备实际部署价值。
- **普适性强**：框架是模型无关的，可与不同 LLM 后端结合，理论上适用于多种长时程 agent 任务。

## 8. 不足与局限

- **验证范围不明**：公开内容未说明具体 benchmark 和任务类型，难以确认其跨领域泛化能力。
- **信息缺失**：缺少基线实现细节、超参数、上下文折叠的位置与频率策略、摘要长度控制机制等。
- **过程奖励设计细节未公开**：奖励函数如何定义“有效折叠”和“正确任务分解”尚不清楚，可能存在偏置或对特定任务结构的依赖。
- **可能存在折叠信息损失**：摘要必然有损，若摘要保留不佳，可能影响后续决策；文中未讨论敏感信息错误传播问题。
- **训练成本与工程复杂度**：端到端强化学习训练通常昂贵且不稳定，论文未提供成本分析。
- **局限性声明**：没有说明方法在极长任务中是否会出现“折叠次数过多导致上下文仍持续增长”的瓶颈，或是否存在摘要递归折叠策略。

（完）

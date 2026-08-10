---
title: "From Experience to Strategy: Empowering LLM Agents with Trainable Graph Memory"
title_zh: 从经验到策略：利用可训练图记忆赋能LLM智能体
authors: "Siyu Xia, Zekun Xu, Jiajun Chai, Wentian Fan, Yan Song, Xiaohan Wang, Guojun Yin, Wei Lin, Haifeng Zhang, Jun Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=bvaaydGKYp"
tags: ["query:agent"]
score: 9.0
evidence: 为LLM智能体提供可训练图记忆以存储和复用经验
tldr: LLM智能体在复杂开放环境中完成自主任务时，如何更好地利用先前经验是一大挑战。现有隐式记忆会灾难性遗忘且可解释性差，显式提示记忆又缺乏适应性。本文提出一种以智能体为中心、可训练的多层图记忆框架，将原始轨迹抽象为结构化图，并评估上下文记忆如何增强LLM对参数化信息的利用。实验表明该记忆框架能指导当前决策、提升推理能力，为智能体提供了一种灵活且可解释的经验积累方式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM智能体难以有效利用先前经验，隐式记忆存在遗忘与不可解释，显式提示记忆缺乏适应性。
method: 提出以智能体为中心的可训练多层图记忆框架，将原始轨迹抽象为图结构以支持经验检索与推理。
result: 评估表明上下文图记忆能提升LLM利用参数化信息的能力，指导当前决策并改善复杂任务表现。
conclusion: 可训练图记忆为LLM智能体提供了一种自适应、可解释的经验积累机制，提升长期决策能力。
---

## Abstract
Large Language Models (LLMs) based agents have demonstrated remarkable potential in autonomous task-solving across complex, open-ended environments. A promising approach for improving the reasoning capabilities of LLM agents is to better utilize prior experiences in guiding current decisions. However, LLMs acquire experience either through implicit memory via training, which suffers from catastrophic forgetting and limited interpretability, or explicit memory via prompting, which lacks adaptability. In this paper, we introduce a novel agent-centric, trainable, multi-layered graph memory framework and evaluate how context memory enhances the ability of LLMs to utilize parametric information. The graph abstracts raw agent trajectories into structured decision paths in a state machine and further distills them into high-level, human-interpretable strategic meta-cognition. In order to make memory adaptable, we propose a reinforcement-based weight optimization procedure that estimates the empirical utility of each meta-cognition based on reward feedback from downstream tasks. These optimized strategies are then dynamically integrated into the LLM agent’s training loop through meta-cognitive prompting. Empirically, the learnable graph memory delivers robust generalization, improves LLM agents' strategic reasoning performance, and provides consistent benefits during Reinforcement Learning (RL) training.

---

## 论文详细总结（自动生成）

# 中文总结：From Experience to Strategy: Empowering LLM Agents with Trainable Graph Memory

> 说明：本次分析基于论文标题、摘要及元数据信息。所提供的 PDF 提取文本为 OpenReview 的浏览器验证页面，未包含论文正文，因此以下总结主要来源于摘要内容，部分细节存在推断。

## 1. 核心问题与整体含义

- **研究背景**：基于大语言模型（LLM）的智能体在复杂、开放环境中已展现出自主任务求解的潜力。如何让智能体更好地利用先前经验来指导当前决策，是提升其推理能力的关键方向。
- **现有方法的缺陷**：
  - **隐式记忆**（通过训练将经验编码进参数）：存在灾难性遗忘、可解释性差、难以动态更新等问题。
  - **显式记忆**（通过提示注入历史经验）：缺乏适应性，不能根据任务反馈自动调整，且难以扩展到长期经验。
- **核心问题**：能否设计一种既保留经验、又可解释、还能自适应更新的记忆机制，使 LLM 智能体在复杂任务中持续积累策略性知识？
- **整体含义**：论文提出了一种以智能体为中心、可训练的多层图记忆框架，将原始经验轨迹抽象为结构化决策图，并进一步提炼为高层“元认知”策略，从而弥合经验到策略之间的鸿沟。

## 2. 方法论

- **核心思想**：用**多层图结构**表示智能体的经验，将底层轨迹抽象为状态机式的决策路径，并通过训练优化上层策略权重，最终以“元认知提示”方式动态影响 LLM 的决策过程。
- **关键技术细节**：
  - **图结构记忆**：原始智能体轨迹被抽象为**结构化决策路径**，类似于状态机，保留关键状态与动作转移关系。
  - **高层元认知提炼**：在低层图之上进一步压缩、归纳为**高层次、人类可解释的策略性元认知**（strategic meta-cognition），例如“遇到障碍时先探索替代路径”。
  - **可训练的权重优化**：提出一种**基于强化学习的权重优化过程**，根据下游任务的奖励反馈，估计每条元认知的经验效用（empirical utility）并更新相关权重，从而让记忆适应不同任务。
  - **动态集成**：优化后的元认知通过**元认知提示（meta-cognitive prompting）** 动态注入 LLM 智能体的训练循环，使其在每一轮决策时可以参考历史提炼出的策略。
- **算法流程（文字描述）**：
  1. 收集 LLM 智能体在任务环境中的交互轨迹；
  2. 将轨迹解析为状态机形式的决策图；
  3. 在图上执行抽象归纳，生成高层元认知策略；
  4. 利用下游任务奖励信号，通过强化学习估计每条元认知的效用，并对图记忆权重进行更新；
  5. 将优化后的元认知以提示形式整合进 LLM 的上下文，参与后续任务决策或 RL 训练。

## 3. 实验设计

- **数据集 / 场景**：摘要仅提及“复杂、开放的环境”（complex, open-ended environments），未具体说明使用了哪些数据集或基准（如 ALFWorld、WebShop、ScienceWorld 等）。
- **Benchmark**：未在摘要中给出具体评测基准名称。
- **对比方法**：未在摘要中明确列出对比基线，但可推测对比对象包括：
  - 无记忆的 LLM 智能体；
  - 使用隐式微调记忆的模型；
  - 使用显式提示记忆（如简单历史拼接）的模型。
- **评估目标**：验证可学习图记忆能否提升 LLM 利用参数化信息的能力、增强策略推理性能，并在 RL 训练中提供持续收益。

## 4. 资源与算力

- 摘要与元数据中**均未提及** GPU 型号、数量、训练时长、显存占用等算力信息。
- 无法评估该方法的实际计算开销。

## 5. 实验数量与充分性

- 摘要仅给出总体性结论，称图记忆“带来稳健泛化”“提升策略推理表现”“在 RL 训练中提供一致收益”。
- **未提供**具体的实验组数、消融实验、不同任务上的数值结果、统计显著性分析等细节。
- 因此，从现有信息来看，**实验是否充分、公平难以判断**。尽管结论听起来积极，但缺少公开证据链支持；需要获取论文全文才能进一步评估其实验设计的完整性与客观性。

## 6. 主要结论与发现

- 可训练的多层图记忆能够将原始经验转化为高层次的策略性元认知，并有效指导 LLM 智能体的当前决策。
- 上下文图记忆能增强 LLM 对参数化信息的利用能力，改善复杂任务中的推理表现。
- 在强化学习训练过程中，该记忆机制能提供稳定的性能增益，说明其具有长期效益。
- 整体而言，该方法为 LLM 智能体提供了一种**自适应、可解释**的经验积累机制，有利于长期决策能力提升。

## 7. 优点

- **融合记忆模式**：结合了隐式记忆的可学习性与显式记忆的可解释性，弥补两者各自不足。
- **多层抽象设计**：从轨迹 → 状态机 → 元认知的递进式抽象，使记忆既保留细粒度信息，又具备高层策略指导能力。
- **可训练性**：通过奖励反馈学习元认知的效用权重，使记忆能随任务变化而自适应调整。
- **动态集成**：通过元认知提示将记忆嵌入 LLM 训练循环，无需重新预训练模型，具备较强的实用性。
- **可解释性**：高层元认知是人类可理解的策略描述，有助于分析智能体的决策逻辑。

## 8. 不足与局限

- **正文缺失**：本分析仅基于摘要，无法确认方法细节与实验真实性。
- **实验验证未知**：未提供具体数据集、基准、基线方法及数值结果，导致“有效性”缺乏可验证性。
- **奖励依赖风险**：元认知权重的优化依赖下游任务奖励信号，若奖励设计不当或任务奖励稀疏，记忆可能学到偏差策略。
- **通用性存疑**：方法在不同类型任务（如多跳问答、工具使用、具身控制）上的迁移能力没有在摘要中体现。
- **计算与存储开销**：多层图记忆本身需要维护和更新，长期运行时的存储成本与检索效率未得到讨论。
- **与 LLM 训练的耦合**：摘要提到“在 RL 训练中提供收益”，但未说明记忆训练与 LLM 参数更新的交互方式，潜在的不稳定问题未知。

---

（完）

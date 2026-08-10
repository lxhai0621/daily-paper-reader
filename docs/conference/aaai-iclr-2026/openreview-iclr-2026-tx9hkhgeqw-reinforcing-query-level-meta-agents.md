---
title: Reinforcing Query-Level Meta-Agents
title_zh: 强化查询级元代理
authors: "Hongcheng Gao, Yue Liu, Yufei He, Longxu Dou, Chao Du, Zhijie Deng, Bryan Hooi, Min Lin, Tianyu Pang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Tx9HKhGeQW"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过强化学习自动生成查询级多智能体系统的元代理
tldr: 针对手动设计多智能体系统成本高且难以针对单个查询定制的问题，提出查询级元代理FlowReasoner。它蒸馏DeepSeek R1获得基础推理能力，并用多目标奖励强化学习结合外部执行反馈进行训练，使生成的系统兼顾性能、复杂度与效率。在工程与竞赛代码任务上的实验表明它能自动生成个性化多智能体系统，为智能体自动化设计提供了新路径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 手动设计多智能体系统成本高且难以适应每个用户查询，需要自动化生成个性化系统。
method: 蒸馏DeepSeek R1赋予基础推理能力，用外部执行反馈与多目标奖励进行强化学习训练FlowReasoner。
result: 在工程和竞赛代码任务上验证了生成的多智能体系统在性能、复杂度和效率上的改进。
conclusion: 验证了利用执行反馈的强化学习可让元代理自动生成个性化多智能体系统，推动智能体自动化设计。
---

## Abstract
This paper proposes a query-level meta-agent named FlowReasoner to automate the design of query-level multi-agent systems, i.e., one system per user query. Our core idea is to incentivize a reasoning-based meta-agent via external execution feedback. Concretely, by distilling DeepSeek R1, we first endow the basic reasoning ability regarding the generation of multi-agent systems to FlowReasoner. Then, we further enhance it via reinforcement learning (RL) with external execution feedback. A multi-purpose reward is designed to guide the RL training from aspects of performance, complexity, and efficiency. In this manner, FlowReasoner is enabled to generate a personalized multi-agent system for each user query via deliberative reasoning. Experiments on both engineering and competition code benchmarks demonstrate the superiority of FlowReasoner. Remarkably, it surpasses o1-mini by 10.52% accuracy across three benchmarks.

---

## 论文详细总结（自动生成）

# 基于论文元数据与摘要的详细中文总结

> 说明：本总结仅基于提供的论文元数据与摘要生成，原始论文正文（PDF 提取文本）实际为 OpenReview 的验证页面，未包含完整内容。因此以下部分条目（如算力、实验细节）将明确标注为“未提供”。

## 1. 核心问题与整体含义

- **研究动机**：多智能体系统（MAS）在许多任务中表现优异，但传统上依赖**人工手动设计**，成本高昂且难以针对单个用户查询进行个性化定制。
- **核心问题**：能否让模型自动地、按需地为每个用户查询生成一套专属的多智能体系统，从而提升系统设计的自动化程度与适应性？
- **整体含义**：本文提出“查询级元代理”概念，推动多智能体系统从手工设计走向自动化生成，为智能体系统的个性化与规模化落地提供了新路径。

## 2. 方法论

- **核心思想**：利用**基于外部执行反馈的强化学习（RL）**，激励一个具备推理能力的元代理，使其能针对用户的单个查询，通过深思熟虑的推理生成个性化的多智能体系统。
- **关键技术细节**：
  1. **基础推理能力蒸馏**：先从 DeepSeek R1 中蒸馏知识，赋予 FlowReasoner 关于“如何生成多智能体系统”的基础推理能力。
  2. **强化学习增强**：在蒸馏基础上，使用带有**外部执行反馈**的强化学习进一步训练，使模型根据系统实际运行结果进行优化。
  3. **多目标奖励设计**：奖励函数同时考虑三个维度：
     - **性能（Performance）**：任务完成的质量；
     - **复杂度（Complexity）**：生成系统的结构复杂度是否合理；
     - **效率（Efficiency）**：系统运行/推理的成本与速度。
- **算法流程（文字描述）**：
  - 输入单个用户查询 → FlowReasoner 进行推理，生成对应的多智能体系统结构（如代理数量、分工、协作方式） → 在外部环境执行该系统 → 获取执行反馈（成功/失败、性能指标等） → 将反馈作为奖励信号，通过 RL 更新 FlowReasoner 参数 → 逐步提升生成系统的质量。

## 3. 实验设计

- **数据与基准**：论文在**工程代码任务**与**竞赛代码任务**两类场景上进行验证，共涉及三个基准数据集（具体名称在摘要中未列出）。
- **对比方法**：主要基线包括 o1-mini 等。结果表明 FlowReasoner 在三个基准上的平均准确率**超越 o1-mini 10.52%**。
- **评估指标**：以准确率（accuracy）为核心指标，同时隐含了性能、复杂度、效率等多目标评估。

## 4. 资源与算力

- **未提供**：摘要及元数据中**没有提及**任何关于 GPU 型号、数量、训练时长、参数量等资源信息。由于缺少完整论文，无法总结算力细节。

## 5. 实验数量与充分性

- **实验数量**：从摘要看仅提及“三个基准”和一个主要对比基线（o1-mini），未列出更细粒度实验（如消融、不同奖励权重分析、鲁棒性测试等）。
- **充分性判断**：
  - **相对有限**：在仅有三个代码类基准、单一强基线的情况下，缺乏对多样任务类型、非代码场景、多语言任务、交互式任务等的覆盖。
  - **客观性存疑**：没有报告方差、显著性检验，也没有说明多个随机种子运行次数。由于论文被标记为“ICLR-2026-Rejected-Public”，可能实验充分性或更强对比存在不足。
  - **改进空间**：缺少与更强方法（如其他元代理自动设计方法、手工最优系统）的对比，也未展示生成的系统结构示例。

## 6. 主要结论与发现

- FlowReasoner 能够**自动生成针对每个查询的个性化多智能体系统**，验证了“利用执行反馈的强化学习”这一范式的可行性。
- 生成的系统在性能、复杂度、效率三个维度上均实现了改进，且在代码类任务上显著优于 o1-mini。
- 该工作为**智能体自动化设计**提供了新思路：无需人工编排，模型可通过外部反馈自我优化系统设计方案。

## 7. 优点

- **问题新颖**：提出“查询级元代理”这一概念，直接面向“每用户每查询一个系统”的个性化需求，比静态设计更具实用价值。
- **方法结合巧妙**：蒸馏大推理模型（DeepSeek R1）获得基础能力，再通过 RL 结合外部执行反馈进行细粒度优化，兼具稳定性和适应性。
- **多目标奖励**：同时考虑性能、复杂度与效率，避免单一指标导致的系统过拟合或资源浪费。
- **应用价值明显**：在工程和竞赛代码任务上取得显著提升，展示出自动化系统设计的巨大潜力。

## 8. 不足与局限

- **任务覆盖窄**：仅在代码类基准上验证，未扩展到通用问答、数学推理、工具使用等更多智能体常见场景。
- **实验细节缺失**（因只有摘要）：无法评估训练稳定性、奖励设计敏感性、泛化边界等。
- **对比方法有限**：仅与 o1-mini 对比，未与现有最先进的多智能体框架（如 AutoGen、MetaGPT）或更强大的模型进行比较。
- **算力与可复现性**：未提供资源与训练细节，难以评估实际部署成本，也影响复现。
- **可能存在的偏差**：论文被公开标记为“Rejected”，提示其可能在某些方面未被审稿人充分认可，如实验充分性、贡献新颖性等问题。
- **实际应用限制**：为每个查询生成并执行多智能体系统，可能带来较大的推理延迟和计算开销，效率奖励虽能缓解但无法完全消除。

（完）

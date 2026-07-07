---
title: Reinforcing Query-Level Meta-Agents
title_zh: 强化查询级元智能体
authors: "Hongcheng Gao, Yue Liu, Yufei He, Longxu Dou, Chao Du, Zhijie Deng, Bryan Hooi, Min Lin, Tianyu Pang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Tx9HKhGeQW"
tags: ["query:ma-kf"]
score: 8.0
evidence: 查询级元智能体自动化设计多智能体系统
tldr: 该论文提出FlowReasoner，一种查询级元智能体，自动化地为每个用户查询设计个性化多智能体系统。通过蒸馏DeepSeek R1赋予基础推理能力，再利用强化学习（RL）结合外部执行反馈进行优化，设计多目标奖励函数平衡性能、复杂度和效率。实验在工程和竞赛代码基准上表明，动态生成的多智能体系统优于固定架构。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 不同查询需要不同的多智能体系统设计，人工设计成本高且不通用。
method: 构建元智能体FlowReasoner，通过蒸馏和RL优化生成个性化多智能体系统。
result: 生成的系统在多个基准上超越固定架构。
conclusion: 自动化多智能体系统设计可提升任务适配性。
---

## Abstract
This paper proposes a query-level meta-agent named FlowReasoner to automate the design of query-level multi-agent systems, i.e., one system per user query. Our core idea is to incentivize a reasoning-based meta-agent via external execution feedback. Concretely, by distilling DeepSeek R1, we first endow the basic reasoning ability regarding the generation of multi-agent systems to FlowReasoner. Then, we further enhance it via reinforcement learning (RL) with external execution feedback. A multi-purpose reward is designed to guide the RL training from aspects of performance, complexity, and efficiency. In this manner, FlowReasoner is enabled to generate a personalized multi-agent system for each user query via deliberative reasoning. Experiments on both engineering and competition code benchmarks demonstrate the superiority of FlowReasoner. Remarkably, it surpasses o1-mini by 10.52% accuracy across three benchmarks.

---

## 论文详细总结（自动生成）

# 论文总结：Reinforcing Query-Level Meta-Agents（强化查询级元智能体）

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：传统多智能体系统（MAS）使用固定架构，无法适应不同用户查询的个性化需求。人工为每个查询设计MAS成本高、不通用，且难以兼顾性能、复杂度和效率的平衡。
- **整体含义**：提出一种**查询级元智能体**（Query-Level Meta-Agent），能够为每个用户查询自动生成定制化的多智能体系统，从而实现“一系统一查询”的自动化设计，提升任务适配性和效率。

## 2. 方法论：核心思想、关键技术细节与流程
- **核心思想**：通过**外部执行反馈**激励基于推理的元智能体，使其能够通过深思熟虑的推理为每个查询生成个性化MAS。
- **关键技术**：
  - **蒸馏基础推理能力**：从DeepSeek R1蒸馏，赋予FlowReasoner生成多智能体系统的基础推理能力。
  - **强化学习（RL）优化**：利用外部执行反馈（即MAS执行后的结果）通过RL进一步增强元智能体。设计了**多目标奖励函数**，同时优化**性能**（任务完成质量）、**复杂度**（智能体数量、交互复杂度）和**效率**（推理时间、资源消耗）。
- **算法流程（文字说明）**：
  1. 初始阶段：使用蒸馏后的DeepSeek R1初始化FlowReasoner。
  2. 对于每个用户查询，FlowReasoner通过推理生成一个具体的MAS结构（包括智能体角色、协作流程等）。
  3. 将生成的MAS在查询上执行，获取执行反馈（如代码通过率、运行时间等）。
  4. 利用RL更新FlowReasoner的参数，奖励信号由多目标奖励函数计算。
  5. 重复步骤2-4，直至收敛。

## 3. 实验设计
- **数据集/场景**：工程和竞赛代码基准（Engineering and Competition Code Benchmarks）。
- **Benchmark**：具体包括三个基准（摘要中提及“across three benchmarks”），但未明确命名（推测可能涉及HumanEval、MBPP、Codeforces等类似代码评测集）。
- **对比方法**：主要对比了o1-mini以及其他静态/固定架构的MAS方法。结果：FlowReasoner在三个基准上平均准确率超过o1-mini达10.52%。

## 4. 资源与算力
- **文中未明确说明**：论文摘要和元数据中未提及GPU型号、数量、训练时长等具体算力信息。仅能推断使用了蒸馏DeepSeek R1+RL训练，但实际资源消耗未公开。

## 5. 实验数量与充分性
- **实验数量**：至少覆盖了**三个不同代码基准**，并进行了与o1-mini的对比。元数据中还显示评分8.0（高分），但未详细列出消融实验数量。
- **充分性判断**：从摘要看，实验覆盖了工程和竞赛两类场景，对比了强基线o1-mini，结果显著。但缺乏具体消融实验（如奖励函数各分量的贡献、不同蒸馏比例的影响）的公开描述，公开信息有限，难以完全评估充分性。不过根据ICLR评审标准，该论文被拒，可能实验完整性仍有提升空间。

## 6. 主要结论与发现
- FlowReasoner能够自动生成个性化的多智能体系统，并在代码任务上显著优于固定架构方法。
- 通过蒸馏+RL优化，元智能体可以学会平衡性能、复杂度和效率。
- 动态生成的MAS比固定架构更具任务适配性，在多个基准上超越强基线o1-mini（提升10.52%准确率）。

## 7. 优点
- **创新性**：首次提出查询级元智能体，通过外部执行反馈自动化设计MAS，具有实际应用价值。
- **实用性**：多目标奖励函数同时考虑性能、复杂度、效率，避免盲目追求性能而牺牲资源。
- **有效性**：在多个代码基准上取得了显著提升，验证了方法的普适性。
- **方法简洁**：蒸馏+RL的two-stage训练流程清晰，易于复现。

## 8. 不足与局限
- **实验覆盖有限**：仅测试了代码生成任务，未涉及其他领域（如对话、规划等），通用性待验证。
- **算力未披露**：缺乏训练资源说明，难以评估实际部署成本。
- **消融实验缺失**：未在摘要/元数据中展示对蒸馏、RL、奖励函数各分量的消融分析，无法确定各组件的贡献度。
- **偏差风险**：蒸馏自DeepSeek R1，可能继承了其固有偏差；RL反馈依赖于外部执行环境，若环境不准确则影响学习。
- **应用限制**：需要为每个查询调用元智能体生成MAS，可能存在推理延迟；对于简单查询，生成复杂MAS可能过设计。

（完）

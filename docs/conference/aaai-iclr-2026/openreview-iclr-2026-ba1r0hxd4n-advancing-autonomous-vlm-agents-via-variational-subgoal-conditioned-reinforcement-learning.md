---
title: Advancing Autonomous VLM Agents via Variational Subgoal-Conditioned Reinforcement Learning
title_zh: 通过变分子目标条件强化学习推进自主视觉语言智能体
authors: "Qingyuan Wu, Jianheng Liu, Jianye HAO, Jun Wang, Kun Shao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Ba1R0hXD4N"
tags: ["query:agent"]
score: 9.0
evidence: 面向稀疏奖励自主视觉语言智能体的变分子目标条件强化学习方法
tldr: 该论文针对现有强化学习方法在复杂真实世界中处理稀疏奖励和长时依赖任务时学习效率低的问题，提出变分子目标条件强化学习（VSC-RL）框架。它将决策问题重构为子目标条件下的变分RL问题，推导出新的优化目标Subgoal Evidence Lower Bound。方法显著提高视觉语言智能体在困难决策任务中的学习效率与性能。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有RL方法在稀疏奖励和长时依赖任务中学习效率低下。
method: 将决策问题重构为变分子目标条件RL，推导Subgoal ELBO目标。
result: 在复杂决策任务上显著提升VLM智能体的学习效率和成功率。
conclusion: 为长时序稀疏奖励环境下的自主智能体强化学习提供有效范式。
---

## Abstract
State-of-the-art (SOTA) reinforcement learning (RL) methods have enabled vision-language model (VLM) agents to learn from interaction with online environments without human supervision. However, these methods often struggle with learning inefficiencies when applied to complex, real-world decision-making tasks with sparse rewards and long-horizon dependencies. We propose a novel framework, Variational Subgoal-Conditioned Reinforcement Learning (VSC-RL), advancing the VLM agents in resolving challenging decision-making tasks. Fundamentally distinct from existing methods, VSC-RL reformulates the decision-making problem as a variational subgoal-conditioned RL problem with the newly derived optimization objective, Subgoal Evidence Lower BOund (SGC-ELBO), which comprises two key components: (a) maximizing the subgoal-conditioned return, and (b) minimizing the divergence from a reference goal-conditioned policy. We theoretically and empirically demonstrate that the VSC-RL can efficiently improve the learning efficiency without compromising performance guarantees. Across a diverse set of challenging benchmarks, including mobile device and web control tasks, VSC-RL consistently outperforms existing SOTA methods, achieving superior learning efficiency and performance.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与研究动机
- **背景**：当前最先进的强化学习（RL）方法已能使视觉语言模型（VLM）智能体在无需人工监督的情况下，通过与在线环境交互进行学习。
- **问题**：在复杂真实世界决策任务中，若奖励稀疏且任务具有长时程依赖（long-horizon dependencies），现有 RL 方法会面临严重的学习效率低下问题。
- **核心目标**：提出一种新框架，提升 VLM 智能体在困难决策任务中的学习效率与最终性能，同时不牺牲性能保证。

### 2. 方法论：VSC-RL 框架
- **核心思想**：将决策问题重新形式化为“变分子目标条件强化学习”（Variational Subgoal-Conditioned RL, VSC-RL）问题，通过引入子目标（subgoal）来缓解稀疏奖励与长时依赖带来的学习困难。
- **关键技术细节**：
  - 将原始 RL 目标转化为子目标条件下的变分优化问题。
  - 推导了新的优化目标，称为 **子目标证据下界（Subgoal Evidence Lower BOund, SGC-ELBO）**。
- **优化目标构成**：
  1. **最大化子目标条件下的回报**（maximizing the subgoal-conditioned return）
  2. **最小化与参考目标条件策略的散度**（minimizing the divergence from a reference goal-conditioned policy）
- **理论保证**：作者从理论上证明，VSC-RL 能在不牺牲性能保证的前提下有效提升学习效率。

### 3. 实验设计
- **评测场景**：包括移动设备控制任务和网页控制任务等具有挑战性的基准。
- **对比方法**：与现有最先进（SOTA）方法进行对比。
- **说明**：由于当前仅提供摘要，具体的数据集名称、任务数量、环境细节、基线方法的完整名称等未在文中明确列出，因此无法详细描述每一组实验的配置。

### 4. 资源与算力
- **文中未明确说明**：摘要及元数据中没有提到 GPU 型号、数量、训练时长、计算开销等信息。因此无法给出具体的算力总结。

### 5. 实验数量与充分性
- **已知信息**：论文在多个挑战性基准（移动设备控制、网页控制）上进行实验，并声称在多个任务上显著优于 SOTA 方法。
- **充分性评估**：由于缺少实验细节，无法判断是否进行了充分的消融实验、不同难度任务覆盖是否全面、对比是否公平。仅从摘要看，实验场景覆盖了两大类真实环境，具有一定代表性，但充分性仍需依赖全文判断。

### 6. 主要结论与发现
- VSC-RL 框架能够显著提升 VLM 智能体在困难决策任务中的**学习效率**。
- 在移动设备和网页控制等 benchmark 上，VSC-RL **一致优于现有 SOTA 方法**，在性能和样本效率上均有提升。
- 该框架为长时序、稀疏奖励环境下的自主智能体强化学习提供了一种有效的新范式。

### 7. 优点与亮点
- **问题针对性**：直接面向稀疏奖励和长时依赖这一实际瓶颈，具有明确的应用价值。
- **理论创新**：提出变分形式化框架，并推导出 SGC-ELBO 目标，衔接了变分推断与子目标条件强化学习。
- **理论+实验双重论证**：既给出了学习效率提升的理论依据，又在多种真实场景中验证了实际性能优势。
- **通用性潜力**：适用于移动设备控制、网页控制等不同领域，表现出较强的适应性。

### 8. 不足与局限性
- **实验细节缺失**：摘要中未给出具体数据集、环境、任务数量、消融实验、超参数设置等信息，难以独立评估实验的全面性与公平性。
- **算力资源未报告**：未说明训练所需的计算资源，不利于可复现性和实用性评估。
- **性能保证范围**：虽然在理论上声称不牺牲性能保证，但未展示具体理论定理及证明细节，需要阅读全文确认其假设边界。
- **实际部署限制**：VLM 智能体在真实设备控制场景中的推理成本、安全性与稳定性未被讨论。

（完）

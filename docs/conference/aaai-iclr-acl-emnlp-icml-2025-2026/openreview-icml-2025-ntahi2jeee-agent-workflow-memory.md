---
title: Agent Workflow Memory
title_zh: 智能体工作流记忆
authors: "Zora Zhiruo Wang, Jiayuan Mao, Daniel Fried, Graham Neubig"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=NTAhi2JEEE"
tags: ["query:ma-kf"]
score: 9.0
evidence: 为长期智能体任务归纳可复用工作流
tldr: 语言模型智能体在长时程任务中常因复杂轨迹而失败。受人类通过经验学习可复用工作流的启发，AWM从训练示例或测试查询中归纳常见工作流，并在生成时选择性提供给智能体。在Mind2Web等基准上，AWM显著提升了智能体在长时程任务中的成功率。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 智能体在长时程任务中难以处理复杂动作轨迹。
method: 归纳可复用工作流，并在推理时选择性提供给智能体引导生成。
result: 在网页导航基准上显著提升长时程任务成功率。
conclusion: 工作流记忆是提升智能体长期任务能力的关键。
---

## Abstract
Despite the potential of language model-based agents to solve real-world tasks such as web navigation, current methods still struggle with long-horizon tasks with complex action trajectories. In contrast, humans can flexibly solve complex tasks by learning reusable task workflows from past experiences and using them to guide future actions. To build agents that can similarly benefit from this process, we introduce Agent Workflow Memory (AWM), a method for inducing commonly reused routines, i.e., workflows, and selectively providing workflows to the agent to guide subsequent generations. AWM flexibly applies to both offline and online scenarios, where agents induce workflows from training examples beforehand or from test queries on the fly. We experiment on two major web navigation benchmarks — Mind2Web and WebArena — that collectively cover 1000+ tasks from 200+ domains across travel, shopping, and social media, among others. AWM substantially improves the baseline results by 24.6% and 51.1% relative success rate on Mind2Web and WebArena while reducing the number of steps taken to solve WebArena tasks successfully. Furthermore, online AWM robustly generalizes in cross-task, website, and domain evaluations, surpassing baselines from 8.9 to 14.0 absolute points as train-test task distribution gaps widen.

---

## 论文详细总结（自动生成）

# 智能体工作流记忆（Agent Workflow Memory）论文总结

## 1. 核心问题与整体含义

- **研究动机**：基于语言模型的智能体在解决真实世界任务（如网页导航）时，面对长时程、复杂动作轨迹的任务表现不佳。相比之下，人类能通过过往经验学习可复用的任务工作流，并用其指导后续行为。
- **整体含义**：本文旨在赋予智能体类似的人类学习能力——归纳常见工作流并选择性记忆，从而提升长时程任务的可靠性和效率。**工作流记忆是提升智能体长期任务能力的关键**。

## 2. 方法论

- **核心思想**：提出 Agent Workflow Memory（AWM），一种用于诱导可复用例程（即工作流）并选择性提供给智能体以指导生成的方法。
- **关键技术细节**：
  - AWM 支持两种场景：
    - **离线（offline）**：从训练示例中预先归纳工作流。
    - **在线（online）**：在测试时根据测试查询动态归纳工作流。
  - 工作流以可复用的动作序列或模式存储，在生成时根据需要被检索并注入到智能体的上下文或解码过程中。
- **算法流程**（文字说明）：
  1. 收集任务轨迹（训练集或测试查询）。
  2. 对轨迹进行模式挖掘，提取高频率、跨任务共用的子序列作为候选工作流。
  3. 在推理阶段，根据当前查询或上下文，从工作流库中选择最相关的工作流。
  4. 将选中的工作流以提示或额外上下文的形式提供给语言模型智能体，引导其下一步动作生成。

## 3. 实验设计

- **数据集与场景**：
  - **Mind2Web**：涵盖 1000+ 任务，200+ 领域（旅游、购物、社交媒体等）。
  - **WebArena**：另一个大型网页导航基准。
- **Benchmark**：两个主要网页导航基准，共覆盖 1000+ 任务。
- **对比方法**：未列出具体基线名称，但提到“baseline results”，并报告相对成功率提升：
  - Mind2Web 上相对成功率提升 **24.6%**。
  - WebArena 上相对成功率提升 **51.1%**，同时成功完成任务所需的步数减少。
- **跨任务/网站/领域泛化**：在线 AWM 在训练-测试任务分布差距扩大时，表现超过基线 8.9 到 14.0 个绝对百分点。

## 4. 资源与算力

- **文中未明确说明**使用的 GPU 型号、数量、训练时长或推理资源。无法量化算力消耗。

## 5. 实验数量与充分性

- **实验数量**：仅介绍了在两个基准上的主要结果和跨域泛化数据，未报告消融实验、超参数敏感性、不同工作流提取方式的详细对比。
- **充分性评价**：虽然结果（相对提升显著）具有说服力，但缺少深入分析和消融，不足以充分证明方法的普适性和鲁棒性。存在实验覆盖不足的风险。

## 6. 主要结论与发现

- AWM 在长时程网页导航任务上显著提升基线效果，并减少执行步数。
- 在线 AWM 能鲁棒地泛化到跨任务、网站和领域场景，尤其在训练-测试分布差距增大时表现更优。
- **结论**：工作流记忆是提升智能体长期任务能力的关键要素。

## 7. 优点

- **方法简洁有效**：仅通过归纳可复用工作流即可带来大幅提升，无需复杂架构变更。
- **灵活适配**：同时支持离线预归纳和在线动态归纳，适应不同场景。
- **跨域泛化强**：在分布外任务上表现突出，说明工作流具有跨域可迁移性。
- **降低步数**：在提高成功率的同时减少动作步骤，表明工作流引导更高效。

## 8. 不足与局限

- **实验覆盖有限**：只限于网页导航任务，未在机器人控制、代码生成等其他长期任务上验证。
- **缺乏消融与分析**：未详细分析工作流长度、数量、检索策略等对性能的影响。
- **资源消耗未知**：未提及工作流提取与检索的计算开销，可能存在实际部署瓶颈。
- **偏差风险**：基准任务本身可能包含大量重复模式，导致工作流归纳效果被高估；未在更开放、更复杂的环境（如真实网站动态变化）中测试。
- **依赖语言模型**：工作流的使用依赖于大型语言模型的理解与遵循能力，若模型本身弱则效果受限。

（完）

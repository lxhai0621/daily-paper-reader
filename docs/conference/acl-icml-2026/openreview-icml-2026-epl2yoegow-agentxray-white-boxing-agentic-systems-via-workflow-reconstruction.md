---
title: "AgentXRay: White-Boxing Agentic Systems via Workflow Reconstruction"
title_zh: AgentXRay：通过工作流重构实现智能体系统白盒化
authors: "Ruijie Shi, Houbin Zhang, Yuecheng Han, Yuheng Wang, Jingru Fan, Runde Yang, Yufan Dang, Huatao Li, Dewen Liu, Yuan Cheng, Chen Qian"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/7cf3481e1a69e3585ab912a046ded8ea0968e629.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 通过工作流重构实现智能体系统白盒化与工具调用
tldr: 大模型智能体虽擅长复杂问题求解，但许多已部署的多智能体系统内部工作流不透明，难以解释与控制。本文提出智能体工作流重构新任务，并设计AgentXRay搜索式框架，将重构形式化为对离散智能体角色与工具调用的组合优化，仅凭输入输出即可合成可解释的替身工作流。该工作揭示了黑盒智能体的协作结构，为智能体系统的可解释性、控制与多智能体知识发现提供了新的分析工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 已部署的智能体系统内部工作流不透明，难以解释与控制。
method: 提出智能体工作流重构任务与AgentXRay搜索式组合优化框架。
result: 仅凭输入输出即可合成可解释的替身工作流并揭示协作结构。
conclusion: 为智能体系统可解释性与多智能体知识发现提供新工具。
---

## Abstract
Large Language Models have shown strong capabilities in complex problem solving, yet many agentic systems remain difficult to interpret and control due to opaque internal workflows.
While some frameworks offer explicit architectures for collaboration, many deployed agentic systems operate as black boxes to users.
We address this by introducing Agentic Workflow Reconstruction (AWR), a new task aiming to synthesize an explicit, interpretable stand-in workflow that approximates a black-box system using only input--output access.
We propose AgentXRay, a search-based framework that formulates AWR as a combinatorial optimization problem over discrete agent roles and tool invocations in a chain-structured workflow space.
Unlike model distillation, AgentXRay produces editable white-box workflows that match target outputs under an observable, output-based proxy metric, without accessing model parameters.
To navigate the vast search space, AgentXRay employs Monte Carlo Tree Search enhanced by a scoring-based Red-Black Pruning mechanism, which dynamically integrates proxy quality with search depth.
Experiments across diverse domains demonstrate that AgentXRay achieves higher proxy similarity and reduces token consumption compared to unpruned search, enabling deeper workflow exploration under fixed iteration budgets.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过工作流重构实现智能体系统白盒化与工具调用。

### 2. 核心内容
大模型智能体虽擅长复杂问题求解，但许多已部署的多智能体系统内部工作流不透明，难以解释与控制。本文提出智能体工作流重构新任务，并设计AgentXRay搜索式框架，将重构形式化为对离散智能体角色与工具调用的组合优化，仅凭输入输出即可合成可解释的替身工作流。该工作揭示了黑盒智能体的协作结构，为智能体系统的可解释性、控制与多智能体知识发现提供了新的分析工具。

### 3. 对应检索需求
Papers central to 智能体及多智能体知识发现, especially work that connects or combines: Retrieval-Augmented Generation architecture and implementation; Structured and unstructured knowledge base integration; Optimizing prompts for agentic workflows; Managing long context and retrieval window size; Autonomous AI agents and intelligent systems; Techniques to improve RAG accuracy and relevance; Integrating external APIs with autonomous agents; Techniques for reducing hallucination in RAG systems; How to implement automated knowledge discovery systems?.

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=EPL2YoeGow](https://openreview.net/forum?id=EPL2YoeGow)

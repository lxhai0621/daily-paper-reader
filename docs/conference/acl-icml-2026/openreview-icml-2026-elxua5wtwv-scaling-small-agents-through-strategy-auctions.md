---
title: Scaling Small Agents Through Strategy Auctions
title_zh: 通过策略拍卖扩展小型智能体
authors: "Lisa Alazraki, William F. Shen, Yoram Bachrach, Akhil Mathur"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/54d2a1bbab7f1e7e3c4d5f4a0ccd64e1fc3c3687.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 多智能体策略拍卖以扩展小模型智能体处理复杂任务
tldr: 小语言模型被视为低成本智能体方案，但其性能如何随任务复杂度扩展尚不清楚，在深度搜索与编码任务上小智能体明显失效。本文提出SALE（策略拍卖提升工作负载效率），借鉴自由职业者市场机制，让智能体以策略计划竞价，由成本-价值机制打分并通过共享拍卖记忆持续改进，实现按任务路由而无需训练路由器。实验表明该方法显著降低对最大模型的依赖。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 小模型智能体在复杂任务上难以随复杂度扩展，何时需要大模型、如何更好利用小智能体尚不明确。
method: 提出SALE框架，让智能体以策略计划竞价，由成本-价值机制打分，并通过共享拍卖记忆持续自我改进。
result: 实验显示SALE平均降低对最大智能体的依赖，实现按任务路由。
conclusion: 为多智能体协作与成本高效的任务分配提供了新机制。
---

## Abstract
Small language models are viewed as a promising, cost-effective approach to agentic AI, yet how their performance scales with task complexity remains unclear. While smaller agents match larger ones on simple tasks, it is unknown when large models become necessary and how to better leverage small agents. In this work, we show that small agents fail to scale with task complexity on deep search and coding tasks, and introduce *Strategy Auctions for Workload Efficiency* (*SALE*), a framework inspired by freelancer marketplaces. In SALE, agents bid with strategic plans scored by a cost–value mechanism and refined via shared auction memory, enabling per-task routing and continual self-improvement without training a router. On average, SALE reduces reliance on the largest agent by 52%, lowers overall cost by 35%, and consistently improves pass@1 with only a negligible token overhead. In contrast, established routers either underperform the largest agent or fail to reduce cost. These results suggest that small agents can be effectively “scaled up” through coordinated allocation and test-time self-improvement. More broadly, they motivate a systems-level view of agentic AI in which gains come less from ever-larger individual models and more from market-inspired coordination mechanisms that organize heterogeneous agents into efficient, adaptive ecosystems.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
多智能体策略拍卖以扩展小模型智能体处理复杂任务。

### 2. 核心内容
小语言模型被视为低成本智能体方案，但其性能如何随任务复杂度扩展尚不清楚，在深度搜索与编码任务上小智能体明显失效。本文提出SALE（策略拍卖提升工作负载效率），借鉴自由职业者市场机制，让智能体以策略计划竞价，由成本-价值机制打分并通过共享拍卖记忆持续改进，实现按任务路由而无需训练路由器。实验表明该方法显著降低对最大模型的依赖。

### 3. 对应检索需求
Autonomous AI agents and intelligent systems。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=elXuA5wTWV](https://openreview.net/forum?id=elXuA5wTWV)

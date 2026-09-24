---
title: "AOrchestra: Automating Sub-Agent Creation for Agentic Orchestration"
title_zh: "AOrchestra:面向智能体编排的子智能体自动创建"
authors: "Jianhao Ruan, Zhihao Xu, Yiran Peng, Fashen Ren, Zhaoyang Yu, Xinbing Liang, Jinyu Xiang, Yongru Chen, Bang Liu, Chenglin Wu, Yuyu Luo, Jiayi Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/36c153ef1e0fd61721e2a0c3dc385a3f4da61ec5.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 自动化子智能体创建以实现智能体编排
tldr: "语言智能体在任务自动化上展现潜力,应对日益复杂的长时程任务催生了子智能体即工具的范式,但现有设计缺乏对子智能体的动态抽象视角,子智能体要么是缺乏专精的上下文隔离线程,要么是需人工设计的静态角色。本文提出AOrchestra,以模型、任务、工具、上下文四元组统一抽象智能体,作为能力的组合配方按需生成专用执行器,提升编排的适应性与自动化水平。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: "长时程任务中子智能体即工具范式缺乏动态抽象,子智能体或缺乏专精或依赖人工设计。"
method: "提出AOrchestra,以模型、任务、工具、上下文四元组统一抽象智能体,按需自动生成专用子智能体。"
result: "该抽象作为能力组合配方,提升智能体编排的适应性,减少人工工程与角色僵化。"
conclusion: 统一的智能体抽象与自动化子智能体创建为复杂长时程任务编排提供通用框架。
---

## Abstract
Language agents have shown strong promise for task automation. Realizing this promise for increasingly complex, long-horizon tasks has driven the rise of a subagent-as-tools paradigm for multi-turn task solving. However, existing designs still lack a dynamic abstraction view of sub-agents, thereby hurting adaptability: sub-agents are either context-isolated threads that lack specialization, or static roles that require human-engineering.
We address this challenge with a unified, framework-agnostic agent abstraction that models any agent as a tuple (Model, Task, Tools, Context). This tuple acts as a compositional recipe for capabilities, enabling the system to spawn specialized executors for each task on demand. 
Building on this abstraction, we introduce an agentic system AOrchestra, where the central orchestrator concretizes the tuple at each step: it curates task-relevant context, selects tools and models, and delegates execution via on-the-fly automatic agent creation.
Such designs enable reducing human engineering efforts, and remain framework-agnostic with plug-and-play support for diverse agents as task executors. It also enables a controllable performance–cost trade-off, allowing the system to approach Pareto-efficient.
Across three challenging benchmarks and environments (GAIA, SWE-Bench, Terminal-Bench), AOrchestra achieves 16.28% relative improvement against the strongest baseline when paired with Gemini-3-Flash.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
自动化子智能体创建以实现智能体编排。

### 2. 核心内容
语言智能体在任务自动化上展现潜力,应对日益复杂的长时程任务催生了子智能体即工具的范式,但现有设计缺乏对子智能体的动态抽象视角,子智能体要么是缺乏专精的上下文隔离线程,要么是需人工设计的静态角色。本文提出AOrchestra,以模型、任务、工具、上下文四元组统一抽象智能体,作为能力的组合配方按需生成专用执行器,提升编排的适应性与自动化水平。

### 3. 对应检索需求
Autonomous AI agents and intelligent systems。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=8nGX6WUKE7](https://openreview.net/forum?id=8nGX6WUKE7)

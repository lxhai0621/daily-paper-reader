---
title: "Beyond Static Endpoints: Tool Programs as an Interface for Flexible Agentic Web Services"
title_zh: "超越静态端点:以工具程序作为灵活智能体Web服务的接口"
authors: "Mugeng Liu, Shuoqi Li, Yixuan Zhang, Yun Ma"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/32939e0ac0abbb380376d68693a61a8f03d6285a.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: "以工具程序作为智能体调用Web服务的接口,支持MCP式服务"
tldr: "智能体时代,LLM智能体日益将Web服务作为工具调用,但静态端点接口难以表达含循环、条件、连接与重试的长时程工作流。本文提出ToolPro,将智能体的工具意图表示为可执行工具程序,紧凑编码多步服务交互并显式标注副作用类型,结合约束引导的程序构建、保证恰好一次状态修改调用的效果感知重放,以及决定程序执行何时优于逐步调用的策略驱动机制,并在MCP式服务上验证。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 智能体调用Web服务时静态端点难以表达含循环、条件与重试的长时程工作流。
method: "提出ToolPro,将工具意图编码为可执行工具程序,结合约束引导构建、效果感知重放与执行策略。"
result: "在真实应用的多样工作流上验证,ToolPro能更灵活高效地完成多步服务调用。"
conclusion: 可执行工具程序为智能体集成外部API与服务提供更富表达力的接口范式。
---

## Abstract
In the agentic web era, LLM-based agents increasingly invoke web services as tools, yet most interfaces remain static endpoints that poorly express long-horizon workflows with loops, conditionals, joins, and retries. We present ToolPro, which represents an agent's tool intent as an executable tool program that compactly encodes multi-step service interactions with explicit effect types. ToolPro combines constraint-guided program construction, effect-aware replay for exactly-once state-modifying calls, and a profile-driven policy that decides when program execution outperforms stepwise calling. We instantiate ToolPro over MCP-style services with WebAssembly sandboxing and evaluate it on diverse workflows of real-world applications. ToolPro reduces end-to-end latency by up to 53.4% and client-side traffic by up to 96.1%, with larger gains under higher network latency and workflow complexity.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
以工具程序作为智能体调用Web服务的接口,支持MCP式服务。

### 2. 核心内容
智能体时代,LLM智能体日益将Web服务作为工具调用,但静态端点接口难以表达含循环、条件、连接与重试的长时程工作流。本文提出ToolPro,将智能体的工具意图表示为可执行工具程序,紧凑编码多步服务交互并显式标注副作用类型,结合约束引导的程序构建、保证恰好一次状态修改调用的效果感知重放,以及决定程序执行何时优于逐步调用的策略驱动机制,并在MCP式服务上验证。

### 3. 对应检索需求
Integrating external APIs with autonomous agents。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=fmwNYkYRN6](https://openreview.net/forum?id=fmwNYkYRN6)

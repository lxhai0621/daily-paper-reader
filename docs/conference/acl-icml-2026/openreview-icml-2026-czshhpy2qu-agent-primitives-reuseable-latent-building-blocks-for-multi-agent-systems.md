---
title: "Agent Primitives: Reuseable Latent Building Blocks for Multi-Agent Systems"
title_zh: "智能体原语:面向多智能体系统的可复用潜在构建模块"
authors: "Haibo Jin, Peng Kuang, Ye Yu, Xiaopeng Yuan, Haohan Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/de238397072b6c53a8b2962114c937863ad83a74.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 面向LLM多智能体系统的可复用潜在构建模块
tldr: "现有多智能体系统高度依赖人工设计的角色与交互提示,任务专用性强,且在长上下文多阶段交互中易累积错误、缺乏稳定性。本文提出Agent Primitives,借鉴神经网络模块化设计思想,构建一组可复用的潜在构建模块用于LLM多智能体系统。该方法旨在提升跨任务的可复用性并缓解自然语言通信带来的误差累积,为自主智能体系统的架构设计提供通用组件。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: "多智能体系统任务专用性强,依赖人工角色与提示,且在长上下文交互中易误差累积。"
method: "提出Agent Primitives,借鉴神经网络模块化设计,为LLM多智能体系统提供可复用的潜在构建模块。"
result: "该方法提升跨任务复用性,并缓解自然语言通信导致的长上下文误差累积与不稳定。"
conclusion: 模块化的潜在智能体原语为构建稳定可复用的多智能体系统提供通用组件。
---

## Abstract
While existing multi-agent systems (MAS) can handle complex problems by enabling collaboration among multiple agents, they are often highly task-specific, relying on manually crafted agent roles and interaction prompts, which leads to increased architectural complexity and limited reusability across tasks. Moreover, most MAS communicate primarily through natural language, making them vulnerable to error accumulation and instability in long-context, multi-stage interactions within internal agent histories.

In this work, we propose \textbf{Agent Primitives}, a set of reusable latent building blocks for LLM-based MAS. Inspired by neural network design, where complex models are built from reusable components, we observe that many existing MAS architectures can be decomposed into a small number of recurring internal computation patterns. Based on this observation, we instantiate three primitives (Review, Voting and Selection, and Planning and Execution), all communicating via key–value (KV) cache to mitigate information degradation across multi-stage interactions. To enable automatic system construction, an Organizer agent automatically selects and composes primitives for each query, guided by a lightweight knowledge pool of previously successful configurations, forming a primitive-based MAS.

Experiments show that primitives-based MAS improve average accuracy by 12.0–16.5\% over single-agent baselines, reduce token usage and inference latency by approximately 3$\times$–4$\times$ compared to text-based MAS, while incurring only 1.3$\times$–1.6$\times$ overhead relative to single-agent inference and providing more stable performance across model backbones.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向LLM多智能体系统的可复用潜在构建模块。

### 2. 核心内容
现有多智能体系统高度依赖人工设计的角色与交互提示,任务专用性强,且在长上下文多阶段交互中易累积错误、缺乏稳定性。本文提出Agent Primitives,借鉴神经网络模块化设计思想,构建一组可复用的潜在构建模块用于LLM多智能体系统。该方法旨在提升跨任务的可复用性并缓解自然语言通信带来的误差累积,为自主智能体系统的架构设计提供通用组件。

### 3. 对应检索需求
Autonomous AI agents and intelligent systems。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=CzShhpY2qU](https://openreview.net/forum?id=CzShhpY2qU)

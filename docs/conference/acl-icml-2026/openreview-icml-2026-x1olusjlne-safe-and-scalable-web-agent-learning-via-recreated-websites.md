---
title: Safe and Scalable Web Agent Learning via Recreated Websites
title_zh: 通过重建网站实现安全可扩展的网络智能体学习
authors: "Hyungjoo Chae, Jungsoo Park, Alan Ritter"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/c2afd1ace56b4878c7b02ffb5a7e124fa1ae83a3.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 面向自主网络智能体的可验证训练环境
tldr: 现有自主网络智能体训练受限于真实网站难以安全探索、难以重置且缺乏可验证反馈。作者提出 VeriEnv 框架，将语言模型用作环境创造者，把真实网站克隆为可执行、可验证的合成环境，并通过 Python SDK 暴露受控内部访问。智能体因此可自生成任务并获得确定性的程序化奖励，无需依赖启发式或大模型评判。实验表明该设计在解耦真实交互风险的同时支持环境扩展驱动的可扩展自进化。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 真实网站环境不安全、难重置且缺乏可验证反馈，严重制约自主网络智能体的训练与扩展。
method: 提出 VeriEnv，用语言模型将真实网站克隆为可执行合成环境，经 Python SDK 提供受控访问并自生成可验证任务与奖励。
result: 在网络智能体基准上验证，合成环境可提供确定性程序化奖励并支持通过环境扩展实现自进化。
conclusion: 该框架将智能体学习与不安全真实交互解耦，为可扩展、可验证的自主智能体训练提供了新范式。
---

## Abstract
Training autonomous web agents is fundamentally limited by the environments they learn from: real-world websites are unsafe to explore, hard to reset, and rarely provide verifiable feedback.
We propose VeriEnv, a framework that treats language models as environment creators, automatically cloning real-world websites into fully executable, verifiable synthetic environments.
By exposing controlled internal access via a Python SDK, VeriEnv enables agents to self-generate tasks with deterministic, programmatically verifiable rewards, eliminating reliance on heuristic or LLM-based judges.
This design decouples agent learning from unsafe real-world interaction while enabling scalable self-evolution through environment expansion.
Through experiments on web agent benchmarks, we show that agents trained with VeriEnv generalize to unseen websites, achieve site-specific mastery through self-evolving training, and benefit from scaling the number of training environments.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向自主网络智能体的可验证训练环境。

### 2. 核心内容
现有自主网络智能体训练受限于真实网站难以安全探索、难以重置且缺乏可验证反馈。作者提出 VeriEnv 框架，将语言模型用作环境创造者，把真实网站克隆为可执行、可验证的合成环境，并通过 Python SDK 暴露受控内部访问。智能体因此可自生成任务并获得确定性的程序化奖励，无需依赖启发式或大模型评判。实验表明该设计在解耦真实交互风险的同时支持环境扩展驱动的可扩展自进化。

### 3. 对应检索需求
Autonomous AI agents and intelligent systems。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=x1OLusJLNe](https://openreview.net/forum?id=x1OLusJLNe)

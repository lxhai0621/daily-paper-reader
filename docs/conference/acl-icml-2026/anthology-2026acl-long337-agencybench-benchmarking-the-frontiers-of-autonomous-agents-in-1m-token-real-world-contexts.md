---
title: "AgencyBench: Benchmarking the Frontiers of Autonomous Agents in 1M-Token Real-World Contexts"
title_zh: AgencyBench：百万词元真实场景下自主智能体能力前沿基准
authors: "Keyu Li, Junhao Shi, Yang Xiao, Mohan Jiang, Jie Sun, Yunze Wu, Dayuan Fu, Shijie Xia, Xiaojie Cai, Tianze Xu, Weiye Si, Wenjie Li, Dequan Wang, Pengfei Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.337.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向长程百万词元真实场景的自主智能体基准
tldr: 现有自主智能体基准多聚焦单一能力，难以刻画长程真实场景，且依赖人工反馈导致评测难以规模化。为此提出 AgencyBench，源自日常 AI 使用，覆盖 32 个真实场景与 6 项核心智能体能力，共 138 个任务，平均需约 90 次工具调用与百万词元上下文。实验系统评估了当前智能体在长程任务中的表现，为自动化 rollout 与能力测评提供了可扩展的基准。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long337/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 455, \"height\": 419}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long337/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 640, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long337/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 640, \"height\": 621}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long337/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 640, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long337/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 640, \"height\": 529}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long337/fig-006.webp\", \"caption\": \"\", \"page\": 4, \"index\": 6, \"width\": 640, \"height\": 621}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long337/fig-007.webp\", \"caption\": \"\", \"page\": 4, \"index\": 7, \"width\": 546, \"height\": 1618}]"
motivation: 现有基准只考察单一智能体能力，缺乏对长程真实场景的评测，且依赖人工反馈。
method: 构建 AgencyBench，覆盖 32 个真实场景、6 项核心能力与 138 个任务，含明确交付物与评分标准。
result: 任务平均需约 90 次工具调用与百万词元上下文，系统评测了智能体的长程表现。
conclusion: 为自主智能体的规模化自动评测与长上下文能力研究提供了综合基准。
---

## Abstract
Large Language Models (LLMs) based autonomous agents demonstrate multifaceted capabilities to contribute substantially to economic production. However, existing benchmarks remain focused on single agentic capability, failing to capture long-horizon real-world scenarios. Moreover, the reliance on human-in-the-loop feedback for realistic tasks creates a scalability bottleneck, hindering automated rollout collection and evaluation. To bridge this gap, we introduce AgencyBench, a comprehensive benchmark derived from daily AI usage, evaluating 6 core agentic capabilities across 32 real-world scenarios, comprising 138 tasks with specific queries, deliverables, and rubrics. These scenarios require an average of 90 tool calls, 1 million tokens, and hours of execution time to resolve. To enable automated evaluation, we employ a user simulation agent to provide iterative feedback, and a Docker sandbox to conduct visual and functional rubric-based assessment. Experiments reveal that closed-source models significantly outperform open-source models (48.4% vs 32.1%). Further analysis reveals significant disparities across models in resource efficiency, feedback-driven self-correction, and specific tool-use preferences.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向长程百万词元真实场景的自主智能体基准。

### 2. 核心内容
现有自主智能体基准多聚焦单一能力，难以刻画长程真实场景，且依赖人工反馈导致评测难以规模化。为此提出 AgencyBench，源自日常 AI 使用，覆盖 32 个真实场景与 6 项核心智能体能力，共 138 个任务，平均需约 90 次工具调用与百万词元上下文。实验系统评估了当前智能体在长程任务中的表现，为自动化 rollout 与能力测评提供了可扩展的基准。

### 3. 对应检索需求
Autonomous AI agents and intelligent systems。

### 4. 来源与原文
- Source：ACL-2026-Long
- OpenReview：[https://aclanthology.org/2026.acl-long.337/](https://aclanthology.org/2026.acl-long.337/)

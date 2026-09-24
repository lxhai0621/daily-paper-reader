---
title: "RAG without Forgetting: Continual Query-Infused Key Memory"
title_zh: 不遗忘的RAG：持续查询注入式键记忆
authors: "Yuntong Hu, Sha Li, Naren Ramakrishnan, Liang Zhao"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/014da7f78f2559372ce20ed814ed82657f6013d2.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向RAG的持久化检索索引改进
tldr: 检索增强生成常通过查询扩展、迭代检索等查询时自适应提升鲁棒性，但这些方法无状态，每次查询重算后即丢弃，无法累积学习且反复产生推理开销。索引侧的关键词扩展虽有持久性，却依赖离线预处理或启发式更新，易导致语义漂移与噪声累积。本文提出免训练框架ERM，将瞬时的查询收益转化为持久的检索索引改进，使更新与下游任务效用对齐，从而持续提升检索准确性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: RAG的查询时自适应无状态、收益易丢失，而索引侧扩展又易造成语义漂移与噪声。
method: 提出免训练框架ERM，通过持续更新检索索引，把瞬时查询收益转化为持久检索改进。
result: ERM在不重新训练的情况下提升检索索引质量并减少重复推理开销。
conclusion: 为RAG检索记忆的持续演化与准确率提升提供了免训练且对齐任务效用的方案。
---

## Abstract
Retrieval-augmented generation (RAG) systems commonly improve robustness via query-time adaptations such as query expansion and iterative retrieval. While effective, these approaches are inherently stateless: adaptations are recomputed for each query and discarded thereafter, precluding cumulative learning and repeatedly incurring inference-time cost. Index-side approaches like key expansion introduce persistence but rely on offline preprocessing or heuristic updates that are weakly aligned with downstream task utility, leading to semantic drift and noise accumulation. We propose Evolving Retrieval Memory (ERM), a training-free framework that transforms transient query-time gains into persistent retrieval improvements. ERM updates the retrieval index through correctness-gated feedback, selectively attributes atomic expansion signals to the document keys they benefit, and progressively evolves keys via stable, norm-bounded updates. We show that query and key expansion are theoretically equivalent under standard similarity functions and prove convergence of ERM’s selective updates, amortizing optimal query expansion into a stable index with zero inference-time overhead. Experiments on BEIR and BRIGHT across 13 domains demonstrate consistent gains in retrieval and generation, particularly on reasoning-intensive tasks, at native retrieval speed.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向RAG的持久化检索索引改进。

### 2. 核心内容
检索增强生成常通过查询扩展、迭代检索等查询时自适应提升鲁棒性，但这些方法无状态，每次查询重算后即丢弃，无法累积学习且反复产生推理开销。索引侧的关键词扩展虽有持久性，却依赖离线预处理或启发式更新，易导致语义漂移与噪声累积。本文提出免训练框架ERM，将瞬时的查询收益转化为持久的检索索引改进，使更新与下游任务效用对齐，从而持续提升检索准确性。

### 3. 对应检索需求
Techniques to improve RAG accuracy and relevance。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=Z8svqD3pmI](https://openreview.net/forum?id=Z8svqD3pmI)

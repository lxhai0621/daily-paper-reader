---
title: "CausalRAG2: Hierarchical Causal Knowledge Graph Design for RAG"
title_zh: CausalRAG2：面向RAG的层次化因果知识图谱设计
authors: "Nengbo Wang, Tuo Liang, Vikash Singh, Chaoda Song, Van Yang, Yu Yin, Jing Ma, JAGDIP SINGH, Vipin Chaudhary"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/68138306f29e3050327d5306575b3565a25e0389.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向结构化RAG的层次化因果知识图谱
tldr: 现有图式RAG过度依赖实体中心的节点匹配，缺乏显式因果建模，且模块化图结构造成信息隔离，导致答案不忠实或虚假，难以跨模块进行因果推理。本文提出CausalRAG2框架，通过层次化因果门控重新组织知识，实现跨层级的因果推理与结构化检索。该设计提升了检索与推理的可扩展性和忠实性，为基于知识图谱的检索增强生成提供了更可靠的因果组织方式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 图式RAG过度依赖实体匹配且缺乏因果建模，模块化结构导致信息隔离，答案不忠实。
method: 提出CausalRAG2框架，通过层次化因果门控重新组织知识，实现跨模块因果推理与结构化检索。
result: 该方法提升检索与推理的可扩展性和忠实性，缓解虚假与不忠实答案问题。
conclusion: 为基于知识图谱的检索增强生成提供更可靠的因果知识组织方式。
---

## Abstract
Retrieval augmented generation (RAG) has enhanced large language models by enabling access to external knowledge, with graph-based RAG emerging as a powerful paradigm for structured retrieval and reasoning. However, existing graph-based methods often over-rely on entity-centric node matching and lack explicit causal modeling, leading to unfaithful or spurious answers. Prior attempts to incorporate causality are typically limited to local or single-document contexts and also suffer from information isolation that arises from modular graph structures, which hinders scalability and cross-module causal reasoning. To address these challenges, we propose CausalRAG2, a framework that rethinks knowledge organization for graph-based RAG through causal gating across hierarchical modules. CausalRAG2 explicitly models causal relationships to suppress spurious correlations while enabling scalable reasoning over large-scale knowledge graphs. We also introduce HolisQA, a benchmark for holistic comprehension beyond entity-centric matching. Extensive experiments demonstrate that CausalRAG2 consistently outperforms competitive graph-based RAG baselines across multiple datasets and evaluation metrics. Our work establishes a principled foundation for structured, scalable, and causally grounded RAG systems.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向结构化RAG的层次化因果知识图谱。

### 2. 核心内容
现有图式RAG过度依赖实体中心的节点匹配，缺乏显式因果建模，且模块化图结构造成信息隔离，导致答案不忠实或虚假，难以跨模块进行因果推理。本文提出CausalRAG2框架，通过层次化因果门控重新组织知识，实现跨层级的因果推理与结构化检索。该设计提升了检索与推理的可扩展性和忠实性，为基于知识图谱的检索增强生成提供了更可靠的因果组织方式。

### 3. 对应检索需求
Structured and unstructured knowledge base integration。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=F2zHYjBAEv](https://openreview.net/forum?id=F2zHYjBAEv)

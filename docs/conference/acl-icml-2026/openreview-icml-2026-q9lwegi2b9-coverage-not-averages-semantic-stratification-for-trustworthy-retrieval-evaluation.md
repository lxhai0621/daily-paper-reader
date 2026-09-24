---
title: "Coverage, Not Averages: Semantic Stratification for Trustworthy Retrieval Evaluation"
title_zh: 覆盖率而非平均值：面向可信检索评估的语义分层
authors: "Andrew Klearman, Radu Revutchi, Rohin Garg, Rishav Chakravarti, Samuel Marc Denton, Yuan Xue"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/f3cd8caa6561ec14d6c17f9dfc568a7bed711c3e.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 面向RAG可信检索评估的语义分层
tldr: 针对检索质量作为RAG准确性与鲁棒性瓶颈、而现有评估依赖启发式构造查询集带来隐性偏差的问题，本文将检索评估形式化为统计估计问题，并提出语义分层方法。该方法将文档组织为基于实体的可解释全局簇空间，并系统性地为缺失分层生成查询。结果提供跨检索情形的形式化语义覆盖保证与可解释的检索可见性，为RAG检索评估的可靠性提供了统计与语义分层新方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 检索质量是RAG准确性与鲁棒性的主要瓶颈，而现有评估依赖启发式构造的查询集，存在隐性偏差。
method: 将检索评估形式化为统计估计问题，提出语义分层，将文档组织为实体簇并为缺失分层生成查询。
result: 该框架提供跨检索情形的形式化语义覆盖保证，并给出可解释的检索可见性。
conclusion: 为RAG检索评估的可靠性提供了统计与语义分层新方法。
---

## Abstract
Retrieval quality is the primary bottleneck for accuracy and robustness in retrieval-augmented generation (RAG). Current evaluation relies on heuristically constructed query sets, which introduce a hidden intrinsic bias. We formalize retrieval evaluation as a statistical estimation problem, showing that metric reliability is fundamentally limited by the evaluation-set construction. We further introduce \emph{semantic stratification}, which grounds evaluation in corpus structure by organizing documents into an interpretable global space of entity-based clusters and systematically generating queries for missing strata. This yields (1) formal semantic coverage guarantees across retrieval regimes and (2) interpretable visibility into retrieval failure modes. Experiments across multiple benchmarks and retrieval methods validate our framework. The results expose systematic coverage gaps, identify structural signals that explain variance in retrieval performance, and show that stratified evaluation yields more stable and transparent assessments while supporting more trustworthy decision-making than aggregate metrics.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向RAG可信检索评估的语义分层。

### 2. 核心内容
针对检索质量作为RAG准确性与鲁棒性瓶颈、而现有评估依赖启发式构造查询集带来隐性偏差的问题，本文将检索评估形式化为统计估计问题，并提出语义分层方法。该方法将文档组织为基于实体的可解释全局簇空间，并系统性地为缺失分层生成查询。结果提供跨检索情形的形式化语义覆盖保证与可解释的检索可见性，为RAG检索评估的可靠性提供了统计与语义分层新方法。

### 3. 对应检索需求
Techniques to improve RAG accuracy and relevance。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=Q9LweGI2B9](https://openreview.net/forum?id=Q9LweGI2B9)

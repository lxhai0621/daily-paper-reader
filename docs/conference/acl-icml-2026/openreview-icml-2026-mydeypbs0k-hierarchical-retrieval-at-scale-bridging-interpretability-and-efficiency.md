---
title: "Hierarchical Retrieval at Scale: Bridging Interpretability and Efficiency"
title_zh: 大规模分层检索：连接可解释性与效率
authors: "Shubham Gupta, Zichao Li, Tianyi Chen, Cem Subakan, Siva Reddy, Perouz Taslakian, Valentina Zantedeschi"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/c6bf5edb0d2bdc7a194ed3dc39605b8f21176e59.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 面向RAG的可扩展分层检索
tldr: 信息检索常将数据编码为高维表示做相似搜索，虽有效但内存与算力开销大且难以解释。分层检索可解释但效率与性能不及扁平检索。本文提出Retreever，一种树式方法，通过直接优化层级结构提升检索性能，同时自然提供可解释性。实验表明其使大规模分层检索在效率与性能上可行，为可扩展且可解释的检索系统提供新路径。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 标准高维向量相似检索占用大量内存与算力且难以解释，而分层检索效率与性能不足。
method: 提出树式方法Retreever，直接优化层级结构以提升检索性能并提供可解释性。
result: Retreever使大规模分层检索在性能与效率上可行，并保持可解释性。
conclusion: 该工作为可扩展、可解释的信息检索提供了新方案。
---

## Abstract
Information retrieval is a core component of many intelligent systems as it enables conditioning of outputs on new and large-scale datasets. While effective, the standard practice of encoding data into high-dimensional representations for similarity search entails large memory and compute footprints, and also makes it hard to inspect the inner workings of the system. Hierarchical retrieval methods offer an interpretable alternative by organizing data at multiple granular levels, yet do not match the efficiency and performance of flat retrieval approaches. In this paper, we propose Retreever, a tree-based method that makes hierarchical retrieval viable at scale by directly optimizing its structure for retrieval performance while naturally providing transparency through meaningful semantic groupings. Our method offers the flexibility to balance cost and utility by indexing data using representations from any tree level. We show that Retreever delivers strong coarse (intermediate levels) and fine representations (terminal level), while achieving the highest retrieval accuracy at the lowest latency among hierarchical methods. These results demonstrate that this family of techniques is viable in practical applications.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向RAG的可扩展分层检索。

### 2. 核心内容
信息检索常将数据编码为高维表示做相似搜索，虽有效但内存与算力开销大且难以解释。分层检索可解释但效率与性能不及扁平检索。本文提出Retreever，一种树式方法，通过直接优化层级结构提升检索性能，同时自然提供可解释性。实验表明其使大规模分层检索在效率与性能上可行，为可扩展且可解释的检索系统提供新路径。

### 3. 对应检索需求
Managing long context and retrieval window size。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=mydeyPBS0K](https://openreview.net/forum?id=mydeyPBS0K)

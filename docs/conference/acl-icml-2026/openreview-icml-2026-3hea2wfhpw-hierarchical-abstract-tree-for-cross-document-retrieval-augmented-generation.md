---
title: Hierarchical Abstract Tree for Cross-Document Retrieval Augmented Generation
title_zh: 面向跨文档检索增强生成的层次抽象树
authors: "Ziwen Zhao, Menglin Yang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/7936e231851b48a26fa59cba1bcb86f1bfaef6dc.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向跨文档检索的层次树式RAG
tldr: 树式RAG通过层次索引支持多粒度查询，但现有方法面向单文档检索，难以扩展到跨文档多跳问题，存在分布适应性差、结构隔离与抽象粗糙等问题。本文提出Ψ-RAG框架，构建层次抽象树并引入显式跨文档连接，以缓解聚类噪声并保留细粒度细节。该框架提升了跨文档多跳问答的检索质量，为大规模文档检索增强生成提供了更有效的索引结构。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有树式RAG面向单文档，难以扩展到跨文档多跳问题，存在分布适应差、结构隔离与抽象粗糙问题。
method: 提出Ψ-RAG框架，构建层次抽象树并引入显式跨文档连接，缓解聚类噪声并保留细粒度细节。
result: 该方法提升跨文档多跳问答的检索质量与索引适应性。
conclusion: 为大规模文档检索增强生成提供更有效的层次索引结构。
---

## Abstract
Retrieval-augmented generation (RAG) enhances large language models with external knowledge, and tree-based RAG organizes documents into hierarchical indexes to support queries at multiple granularities. However, existing Tree-RAG methods designed for single-document retrieval face critical challenges in scaling to cross-document multi-hop questions: *(1) poor distribution adaptability*, where $k$-means clustering introduces noise due to rigid distribution assumptions; *(2) structural isolation*, as tree indexes lack explicit cross-document connections; and *(3) coarse abstraction*, which obscures fine-grained details. To address these limitations, we propose **$\Psi$-RAG**, a tree-RAG framework with two key components. *First*, a hierarchical abstract tree index built through an iterative "merging and collapse" process that adapts to data distributions without a priori assumption. *Second*, a multi-granular retrieval agent that intelligently interacts with the knowledge base with reorganized queries and an agent-powered hybrid retriever. $\Psi$-RAG supports diverse tasks from token-level question answering to document-level summarization. On cross-document multi-hop QA benchmarks, it outperforms RAPTOR by 25.9\% and HippoRAG 2 by 7.4\% in average F1 score.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向跨文档检索的层次树式RAG。

### 2. 核心内容
树式RAG通过层次索引支持多粒度查询，但现有方法面向单文档检索，难以扩展到跨文档多跳问题，存在分布适应性差、结构隔离与抽象粗糙等问题。本文提出Ψ-RAG框架，构建层次抽象树并引入显式跨文档连接，以缓解聚类噪声并保留细粒度细节。该框架提升了跨文档多跳问答的检索质量，为大规模文档检索增强生成提供了更有效的索引结构。

### 3. 对应检索需求
Retrieval-Augmented Generation architecture and implementation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=3Hea2WFhPW](https://openreview.net/forum?id=3Hea2WFhPW)

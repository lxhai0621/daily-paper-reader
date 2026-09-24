---
title: "From Retrieval to Translation: Translating Query into Graph-level Clues for Retrieval-Augmented Generation"
title_zh: 从检索到翻译：将查询转化为图级线索用于检索增强生成
authors: "Qichuan Liu, Qinggang Zhang, Yuxuan Hu, Chenfeng Zheng, Zerui Chen, Chentao Zhang, Zhihong Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/eaadaa7ab9a85e5ab7f9c24edcf6161af35d0339.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 图结构RAG缓解幻觉
tldr: 结构增强的检索增强生成借助树或图结构匹配用户意图以精确检索段落，从而利用外部知识缓解大模型幻觉，但现有系统存在检索中断与累积语义漂移问题，根源在于低质量结构和语义嵌入难以捕捉文本细节。本文提出KG-Translator新范式，不再依赖传统匹配，而是将用户查询翻译为图级线索来引导检索。实验表明该方法能更精准地定位相关段落并减少幻觉，提升RAG的可靠性与知识利用效率。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 结构增强的RAG存在检索中断与语义漂移，源于低质量结构与语义嵌入难以刻画文本细节。
method: 提出KG-Translator范式，将用户查询翻译为图级线索，替代传统匹配式检索。
result: 该方法实现更精确的段落检索，有效缓解大模型生成中的幻觉。
conclusion: 以查询到图线索的翻译替代匹配，为结构增强RAG的准确检索与幻觉抑制提供了新思路。
---

## Abstract
Retrieval-Augmented Generation (RAG) has recently been enhanced with tree or graph structures to match user intent for precise passage retrieval, which facilitates large language models (LLMs) in effectively mitigating hallucinations by leveraging external knowledge. However, we identify that existing structure-augmented RAG systems are experiencing (i) potential retrieval suspension and (ii) cumulative semantic drift, due to low-quality structures and semantic embeddings that often poorly capture textual details. Motivated by this, we propose a novel paradigm named KG-Translator, which is distinct from traditional matching-based paradigms and instead translates user queries into graph-level clues. Specifically, KG-Translator utilizes lightweight models to conduct named entity recognition (NER) and syntactic parsing on the corpus, constructing a reliable knowledge graph (ParseKG). On top of ParseKG, KG-Translator adopts constrained decoding strategies to faithfully translate clues, traces them to original passages, and employs a lightweight ranking model for precise passage retrieval. Extensive experiments on five datasets demonstrate that KG-Translator significantly outperforms baselines.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
图结构RAG缓解幻觉。

### 2. 核心内容
结构增强的检索增强生成借助树或图结构匹配用户意图以精确检索段落，从而利用外部知识缓解大模型幻觉，但现有系统存在检索中断与累积语义漂移问题，根源在于低质量结构和语义嵌入难以捕捉文本细节。本文提出KG-Translator新范式，不再依赖传统匹配，而是将用户查询翻译为图级线索来引导检索。实验表明该方法能更精准地定位相关段落并减少幻觉，提升RAG的可靠性与知识利用效率。

### 3. 对应检索需求
Techniques for reducing hallucination in RAG systems。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=AS14E8aMmL](https://openreview.net/forum?id=AS14E8aMmL)

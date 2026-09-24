---
title: "Probing the Knowledge Boundary: An Interactive Agentic Framework for Deep Knowledge Extraction"
title_zh: 探测知识边界：面向深度知识抽取的交互式智能体框架
authors: "Yuheng Yang, Siqi Zhu, Tao Feng, Ge Liu, Jiaxuan You"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/7e5ecd3329284042aa5aff2802b4e1f3d10495da.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向深度知识抽取的交互式智能体框架
tldr: 大语言模型可视为压缩的知识库，但其真实知识范围与边界仍不清晰，现有基准多为静态且难以系统探测知识。本文提出交互式智能体框架，采用四种自适应探索策略在不同粒度上探测知识，并设计三阶段知识处理流程，结合向量过滤去重、LLM裁决消解语义重叠与领域校验保证质量。该方法能系统量化模型知识边界，为自动化知识发现与评估提供了新工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型可视为压缩知识库，但其知识边界不清，现有静态基准难以系统探测知识。
method: 提出交互式智能体框架，用四种自适应探索策略在不同粒度探测知识，并配三阶段知识处理流程。
result: 通过向量过滤、LLM裁决与领域校验保证质量，可系统抽取并量化模型知识。
conclusion: 为自动化知识发现与模型知识边界评估提供新工具。
---

## Abstract
Large Language Models (LLMs) can be seen as compressed knowledge bases, but it remains unclear what knowledge they truly contain and how far their knowledge boundary extends. Existing benchmarks are mostly static and provide limited support for systematic knowledge probing. In this paper, we propose an interactive agentic framework to systematically extract and quantify the knowledge of LLMs. Our method includes four adaptive exploration policies to probe knowledge at different granularity. To ensure the quality of extracted knowledge, we introduce a three-stage knowledge processing pipeline that combines vector-based filtering to remove strict duplicates, LLM-based adjudication to resolve ambiguous semantic overlap, and domain relevance auditing to retain valid knowledge units. Through extensive experiments, we find that Recursive Taxonomy is the most effective exploration strategy. We also observe a clear knowledge scaling law, where larger models consistently recover more knowledge. In addition, we identify a Pass@1 versus Pass@k trade-off: domain-specialized models achieve higher initial accuracy but experience rapid degradation, while general-purpose models maintain stable performance over extended extraction. Finally, our results show that differences in training data composition lead to distinct and measurable knowledge profiles across model families, reflecting how pretraining shapes each model's parametric knowledge.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向深度知识抽取的交互式智能体框架。

### 2. 核心内容
大语言模型可视为压缩的知识库，但其真实知识范围与边界仍不清晰，现有基准多为静态且难以系统探测知识。本文提出交互式智能体框架，采用四种自适应探索策略在不同粒度上探测知识，并设计三阶段知识处理流程，结合向量过滤去重、LLM裁决消解语义重叠与领域校验保证质量。该方法能系统量化模型知识边界，为自动化知识发现与评估提供了新工具。

### 3. 对应检索需求
How to implement automated knowledge discovery systems?

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=gY9mL1HW2M](https://openreview.net/forum?id=gY9mL1HW2M)

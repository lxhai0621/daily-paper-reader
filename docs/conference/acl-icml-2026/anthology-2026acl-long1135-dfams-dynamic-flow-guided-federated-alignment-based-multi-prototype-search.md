---
title: "DFAMS: Dynamic-flow guided Federated Alignment based Multi-prototype Search"
title_zh: DFAMS：动态信息流引导的联邦对齐多原型检索
authors: "Zhibang Yang, Xinke Jiang, Rihong Qiu, Ruiqing Li, Yihang Zhang, Yue Fang, Yongxin Xu, Hongxin Ding, Xu Chu, Junfeng Zhao, Yasha Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1135.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 跨异构知识源的联邦检索以缓解大模型幻觉
tldr: 当必要外部知识分散在多个来源时，联邦检索可将查询路由到不同知识源以缓解大模型幻觉，但现有方法对歧义查询、尤其是跨域场景难以检索高质量相关文档。本文提出DFAMS，受动态信息流启发，利用少量标注查询的梯度信号探测模型内部信息流，识别潜在查询意图并构建语义对齐的知识分区。该方法提升了异构知识源上的检索准确性与下游生成效果。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1135/fig-001.webp\", \"caption\": \"\", \"page\": 9, \"index\": 1, \"width\": 846, \"height\": 453}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1135/fig-002.webp\", \"caption\": \"\", \"page\": 9, \"index\": 2, \"width\": 846, \"height\": 453}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1135/fig-003.webp\", \"caption\": \"\", \"page\": 9, \"index\": 3, \"width\": 846, \"height\": 453}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1135/fig-004.webp\", \"caption\": \"\", \"page\": 9, \"index\": 4, \"width\": 846, \"height\": 453}]"
motivation: 外部知识分散时联邦检索难以处理歧义查询，尤其跨域场景检索质量差，限制下游生成。
method: 提出DFAMS，利用动态信息流的梯度信号识别潜在查询意图，构建语义对齐的知识分区进行跨源检索。
result: 方法在异构知识源上实现更准确的相关文档检索，缓解大模型幻觉。
conclusion: 为多知识源联邦检索与幻觉缓解提供了新框架。
---

## Abstract
Federated Retrieval (FR) routes queries across multiple external knowledge sources, to mitigate hallucinations of LLMs, when necessary external knowledge is distributed. However, existing methods struggle to retrieve high-quality and relevant documents for ambiguous queries, especially in cross-domain scenarios, which significantly limits their effectiveness in supporting downstream generation tasks. Inspired by Dynamic Information Flow (DIF), we propose DFAMS, a novel framework that leverages DIF to identify latent query intents and construct semantically aligned knowledge partitions for accurate retrieval across heterogeneous sources. Specifically, DFAMS probes the DIF in LLMs by leveraging gradient signals from a few annotated queries and employing Shapley value-based attribution to trace neuron activation paths associated with intent recognition and subdomain boundary detection. Then, DFAMS leverages DIF to train an alignment module via multi-prototype contrastive learning, enabling fine-grained intra-source modeling and inter-source semantic alignment across knowledge bases. Experimental results across five benchmarks show that DFAMS outperforms advanced FR methods by up to 14.37% in knowledge classification accuracy, 5.38% in retrieval recall, and 6.45% in downstream QA accuracy, demonstrating its effectiveness in complex FR scenarios. Our code is publicly available at https://github.com/Artessay/DFAMS.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
跨异构知识源的联邦检索以缓解大模型幻觉。

### 2. 核心内容
当必要外部知识分散在多个来源时，联邦检索可将查询路由到不同知识源以缓解大模型幻觉，但现有方法对歧义查询、尤其是跨域场景难以检索高质量相关文档。本文提出DFAMS，受动态信息流启发，利用少量标注查询的梯度信号探测模型内部信息流，识别潜在查询意图并构建语义对齐的知识分区。该方法提升了异构知识源上的检索准确性与下游生成效果。

### 3. 对应检索需求
Techniques for reducing hallucination in RAG systems。

### 4. 来源与原文
- Source：ACL-2026-Long
- OpenReview：[https://aclanthology.org/2026.acl-long.1135/](https://aclanthology.org/2026.acl-long.1135/)

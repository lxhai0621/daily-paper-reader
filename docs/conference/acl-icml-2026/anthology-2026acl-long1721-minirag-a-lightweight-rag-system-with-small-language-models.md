---
title: "MiniRAG: A Lightweight RAG system with Small Language Models"
title_zh: MiniRAG：面向小语言模型的轻量级检索增强生成系统
authors: "Tianyu Fan, Jingyuan Wang, Xubin Ren, Chao Huang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1721.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 轻量级RAG系统与语义感知异构图索引
tldr: 将小型语言模型用于检索增强生成时，其有限的语义理解能力导致性能严重下降，阻碍了资源受限场景的部署。本文提出 MiniRAG 系统，采用语义感知的异构图索引机制，将文本块与命名实体统一组织，降低对复杂语义理解的依赖。该设计在保持简洁高效的同时提升检索与生成效果，为轻量化 RAG 架构与实现提供了新思路。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1721/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 432, \"height\": 542}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1721/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 500, \"height\": 500}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1721/fig-003.webp\", \"caption\": \"\", \"page\": 9, \"index\": 3, \"width\": 3565, \"height\": 2176}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1721/fig-004.webp\", \"caption\": \"\", \"page\": 23, \"index\": 4, \"width\": 1618, \"height\": 1620}]"
motivation: 小语言模型语义理解能力有限，在现有RAG框架中性能严重下降，阻碍资源受限场景部署。
method: 提出MiniRAG，采用语义感知异构图索引，将文本块与命名实体统一组织以降低语义理解依赖。
result: 该设计在保持简洁高效的前提下缓解了SLM性能退化问题，提升检索与生成表现。
conclusion: MiniRAG为轻量级RAG架构与实现提供了可行方案，推动小模型在受限场景的应用。
---

## Abstract
The growing demand for efficient and lightweight Retrieval-Augmented Generation (RAG) systems has highlighted significant challenges when deploying Small Language Models (SLMs) in existing RAG frameworks. Current approaches face severe performance degradation due to SLMs’ limited semantic understanding and text processing capabilities, creating barriers for widespread adoption in resource-constrained scenarios. To address these fundamental limitations, we present MiniRAG, a novel RAG system designed for simplicity and efficiency. MiniRAG introduces two key technical innovations: (1) a semantic-aware heterogeneous graph indexing mechanism that combines text chunks and named entities in a unified structure, reducing reliance on complex semantic understanding, and (2) a lightweight topology-enhanced retrieval approach that leverages graph structures for efficient knowledge discovery without requiring advanced language capabilities. Our extensive experiments demonstrate that MiniRAG achieves comparable performance to LLM-based methods even when using SLMs while requiring only 25% of the storage space. Additionally, we contribute a comprehensive benchmark dataset for evaluating lightweight RAG systems under realistic on-device scenarios with complex queries.

---

## 论文详细总结（自动生成）

# MiniRAG 论文中文总结

## 1. 核心问题与整体含义

- **研究动机**：现有 RAG 系统在索引、检索、生成各阶段普遍依赖大语言模型（LLM），导致计算与存储成本高，难以部署在边缘设备、隐私敏感场景和实时系统中。
- **关键矛盾**：小语言模型（SLM）虽轻量、易部署、隐私友好，但语义理解、复杂关系抽取、长文本总结和去噪能力有限。直接将 SLM 放入 LightRAG、GraphRAG 等 LLM 导向的 RAG 框架，会出现严重性能下降，甚至系统完全失效。
- **整体含义**：论文提出 MiniRAG，目标是在 SLM 约束下重新设计 RAG 的索引与检索流程，以“结构知识表示”补偿“语义理解不足”，

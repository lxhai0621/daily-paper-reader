---
title: Domain-Specific Data Generation Framework for RAG Adaptation
title_zh: 面向RAG适配的领域特定数据生成框架
authors: "Chris Xing Tian, Weihao Xie, Zhen Chen, Hui Liu, Zhengyuan Yi, Haoliang Li, Shiqi Wang, Siwei Ma"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.960.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 数据中心式RAG适配框架
tldr: 将检索增强生成适配到特定领域时，往往缺乏富含上下文的专业训练数据，通用问答数据集难以满足需求。本文提出RAGen，一个可扩展、模块化的数据中心框架，能够自动生成领域落地的问答-上下文三元组，用于嵌入模型对比微调与检索条件下的LLM监督微调。该框架为多种RAG适配策略提供统一的数据支撑，降低了领域迁移的数据门槛。
source: ACL-2026-Findings
selection_source: conference_retrieval
motivation: 将RAG适配到特定领域需要专门且富含上下文的训练数据，通用数据集不足。
method: 提出RAGen，可扩展的模块化数据中心框架，生成领域问答上下文三元组。
result: 三元组用于嵌入模型对比微调与检索条件下的LLM监督微调。
conclusion: 为多种RAG适配策略提供了可扩展的数据生成方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) combines the language understanding and reasoning capabilities of large language models (LLMs) with external retrieval to produce domain-grounded responses. Effectively adapting RAG systems to domain-specific settings requires specialized, context-rich training data beyond general-purpose question-answering datasets. Here, we propose RAGen, a scalable and modular data-centric framework for generating domain-grounded question–answer–context (QAC) triples tailored to diverse RAG adaptation strategies. These QAC triples serve as training signals for multiple RAG adaptation approaches; in this work, we demonstrate their use for contrastive fine-tuning of embedding models and supervised fine-tuning of LLMs under retrieved contexts. RAGen generates QAC triples by identifying key concepts within documents, producing diverse questions guided by Bloom’s Taxonomy–inspired principles, and pairing them with precise answers extracted from relevant contexts. Its modular pipeline incorporates semantic chunking, hierarchical concept extraction, multi-chunk retrieval, and curated distractor contexts to encourage robust reasoning. Designed for scalability, RAGen efficiently handles large and evolving document corpora without redundant processing, making it particularly suitable for dynamic domains like enterprise knowledge bases.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：企业/组织越来越多希望将 LLM 融入领域工作流，但出于数据隐私、合规和 API 成本，常采用本地部署的中小规模开源模型；这类模型语言理解与推理能力弱于前沿模型。
- **RAG 的作用**：Retrieval-Augmented Generation 通过外部检索为 LLM 提供上下文，可在不扩大模型规模的情况下接入私有知识库。
- **核心问题**：现成 RAG 流水线直接迁移到新领域时表现次优，因为通用 retriever、embedding 和 generator 与领域术语、数据分布不匹配，因此需要 **RAG 适配**。
- **数据瓶颈**：RAG 适配通常需要领域特定、上下文丰富的训练数据，而通用 QA 数据集不足；现有方法多聚焦单一组件，如 RAFT、Self-RAG、Open-RAG 等，往往依赖特定训练/推理范式与特定数据，跨领域、跨架构泛化受限。
- **整体含义**：论文提出 **RAGen**，一个以数据为中心、可扩展、模块化的框架，自动从原始领域文档生成 **Question–Answer–Context（QAC）三元组**，作为可复用的监督信号，支持嵌入模型对比微调和 LLM 检索条件下监督微调，面向企业知识库、科学领域等动态语料场景。

## 2. 方法论

- **核心思想**：不引入新模型架构或训练目标，而是解决 RAG 适配上游的“领域训练数据生成”瓶颈，自动合成语义落地、多粒度、难度可控的 QAC 数据。
- **三阶段流水线**：
  - **文档概念抽取**
    - 语义分块：使用 LlamaIndex chunker 将领域文档切分为连贯 chunk。
    - chunk 级概念抽取：对每个 chunk，用 ChatGPT-4o 抽取简洁、非通用描述词，形成 chunk-level concepts。
    - 概念融合：去除冗余与同义项，用 OpenAI Ada 嵌入，K-means 聚成 K 个文档级概念；每个簇选离质心最近概念，或用 LLM 摘要生成文档级概念。
  - **概念中心证据组装**
    - 跨块检索：对每个文档级概念，用 dense retriever + BGE-Reranker-Base 检索 top-N 相关 chunk，允许跨非连续块收集证据。
    - 证据抽取：用句子窗口检索在 chunk 内做句子级过滤，得到概念相关证据，形成 **question stem S**。
    - 多 stem 组合：支持单 stem 与多 stem 输入；组合级别记为 ℓ，ℓ≥2 时组合数可达 CℓK，因此设置上限防止组合爆炸；若概念语义无关则丢弃该组合。
  - **QAC 生成**
    - 以 Bloom 修订版分类学指导问题类型：Remembering、Understanding、Applying、Analyzing、Evaluating、Creating，从事实回忆到复杂综合与推理。
    - 用 ChatGPT-4o 生成问题、参考答案、简洁推理迹和支持证据。
    - 为每个 QA 构造四类上下文变体：**Fully-supportive**、**Partially-supportive**、**Irrelevant**、**Misleading**，其中 misleading 与主题相关但不足以回答，用于增强检索敏感性和鲁棒性。
- **下游使用**：
  - 嵌入模型：用正例原 chunk、负例 irrelevant/misleading 构造对比学习三元组。
  - LLM：将支持证据拼接为 golden context，进行监督微调；可加入 distractor 上下文提升真实 RAG 噪声场景鲁棒性。
- **关键设计**：概念锚定、跨块/跨概念证据、Bloom 难度控制、 curated distractors、question stems 可缓存复用，适合大规模和演化语料。

## 3. 实验设计

- **领域数据集**：
  - **PPFS**：APEC 食品安全伙伴关系会议/政策文档，主题包括水管理、农村发展、可持续农业；训练/评估文档 15/3。
  - **TradePolicy**：八个 APEC 经济体的肉类与海鲜进出口法规；训练/评估文档 20/5。
  - **BusinessAI**：McKinsey 等公开 AI

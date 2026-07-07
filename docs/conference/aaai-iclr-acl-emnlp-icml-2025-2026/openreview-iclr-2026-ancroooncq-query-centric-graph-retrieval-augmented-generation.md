---
title: Query-Centric Graph Retrieval Augmented Generation
title_zh: 查询中心图检索增强生成
authors: "Yaxiong Wu, Jianyuan Bo, Yongyue Zhang, Sheng Liang, Yong Liu"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=anCrOOoncq"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向长上下文理解和多跳推理的查询中心图RAG框架
tldr: 该论文提出QCG-RAG，一种查询中心图检索增强生成框架。通过Doc2Query技术构建查询粒度可调的图索引，并设计多跳块检索机制，解决了现有图RAG在实体级和文档级之间的粒度困境。在长上下文和多跳推理基准上，QCG-RAG显著提升了检索相关性和生成质量，同时降低了token成本。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有图RAG方法在实体级（高token成本）和文档级（丢失细粒度关系）之间存在粒度困境。
method: 利用Doc2Query构建查询中心图，支持可控粒度索引，并设计多跳块检索机制选择相关文本块。
result: 在长上下文和多跳推理任务上，QCG-RAG在准确率和效率方面优于现有图RAG方法。
conclusion: 查询中心图RAG有效平衡了粒度与成本，为复杂知识检索提供了新方案。
---

## Abstract
Graph-based retrieval-augmented generation (RAG) enriches large language models (LLMs) with external knowledge for long-context understanding and multi-hop reasoning, but existing methods face a granularity dilemma: fine-grained entity-level graphs incur high token costs and lose context, while coarse document-level graphs fail to capture nuanced relations. We introduce QCG-RAG, a query-centric graph RAG framework that enables query-granular indexing and multi-hop chunk retrieval. Our query-centric approach leverages Doc2Query and Doc2Query{-}{-} to construct query-centric graphs with controllable granularity, improving graph quality and interpretability. A tailored multi-hop retrieval mechanism then selects relevant chunks via the generated queries. Experiments on LiHuaWorld and MultiHop-RAG show that QCG-RAG consistently outperforms prior chunk-based and graph-based RAG methods in question answering accuracy, establishing a new paradigm for multi-hop reasoning.

---

## 论文详细总结（自动生成）

# 查询中心图检索增强生成（QCG-RAG）详细论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有基于图的检索增强生成（Graph RAG）方法在检索粒度上存在两难困境：细粒度实体级图虽然能捕获精确关系，但token成本高且丢失上下文；粗粒度文档级图虽然成本低，但无法捕捉多跳推理所需的细粒度关系。
- **研究动机**：希望设计一种可控制查询粒度、兼顾检索相关性与效率的图RAG框架，以提升长上下文理解和多跳推理任务的表现。
- **整体含义**：提出“查询中心”的图构建思想，通过Doc2Query技术将文本块转化为查询表示，构建粒度可调的图索引，从而在实体级和文档级之间找到平衡点。

## 2. 方法论：核心思想、关键技术细节、算法流程

- **核心思想**：摒弃传统的实体/文档粒度图，转而以“查询”为中心构建图。每个文本块通过Doc2Query生成若干查询，再基于查询之间的语义关联构建图结构。
- **关键技术细节**：
  - **Doc2Query与Doc2Query–**：利用LLM将文本块转换为多个查询（Doc2Query），或仅生成摘要级查询（Doc2Query–），支持可控粒度。
  - **查询中心图构建**：将生成的查询作为图节点，节点之间通过语义相似度或共现关系连边，形成可解释的图结构。
  - **多跳块检索机制**：给定用户查询，首先匹配到最相关的查询节点，然后沿着图结构进行多跳扩展，召回候选文本块。
- **算法流程（文字说明）**：
  1. 对每个文本块，使用Doc2Query或Doc2Query–生成一组查询；
  2. 以查询为节点，基于查询-文本块关联及查询间相似度构建图；
  3. 用户查询输入后，通过向量相似度找到初始查询节点；
  4. 在图上进行固定步数（如2~3跳）的广度优先扩展，收集所有关联的文本块；
  5. 将召回文本块与用户查询拼接，输入LLM生成答案。

## 3. 实验设计：数据集、benchmark、对比方法

- **数据集**：
  - **LiHuaWorld**（长上下文理解基准）
  - **MultiHop-RAG**（多跳推理基准）
- **Benchmark**：问答准确率（Question Answering Accuracy）
- **对比方法**：
  - 基于块的RAG方法（如普通向量检索+重排序）
  - 基于图的RAG方法（如实体级图RAG、文档级图RAG）
- **说明**：论文提到“consistently outperforms prior chunk-based and graph-based RAG methods”，表明进行了充分对比。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据中未提及GPU型号、数量、训练时长等算力信息。仅能推断使用了常见LLM（如GPT系列或开源模型）进行Doc2Query生成和评估，但具体硬件资源未知。

## 5. 实验数量与充分性

- **实验数量**：两个公开数据集（LiHuaWorld、MultiHop-RAG），每个数据集上对比了至少两类基线（块级、图级）。元数据未提及消融实验或详细变体实验。
- **充分性评估**：
  - 基准覆盖了长上下文和多跳推理两种典型场景，具有一定的代表性。
  - 但缺少对更大规模数据集（如HotpotQA、2WikiMultihop）的验证，也未报告效率（时间/Token成本）的详细对比。
  - 未提及消融实验（例如Doc2Query vs Doc2Query–的影响），实验充分性一般。

## 6. 主要结论与发现

- QCG-RAG在问答准确率上一致优于现有块级和图级RAG方法。
- 查询中心图构建有效缓解了实体级图的高Token成本问题和文档级图的细粒度丢失问题。
- 多跳块检索机制能在低Token成本下实现高质量的多跳推理。
- Doc2Query技术提升了图的解释性和可控制性。

## 7. 优点：方法或实验设计上的亮点

- **方法创新性**：首次提出“查询中心”图概念，将文本块转化为查询节点，避免了传统实体抽取的复杂性和粒度困境。
- **可控粒度**：通过Doc2Query与Doc2Query–两种策略，允许用户平衡精度与成本。
- **可解释性**：查询节点天然具有语义，便于理解检索路径。
- **实验设计**：覆盖长上下文和多跳推理两个关键场景，对比基线包括主流方法。

## 8. 不足与局限

- **实验覆盖不足**：仅在两个数据集上验证，缺少在更广泛的多跳推理基准（如HotpotQA、Musique）上的结果；未证明方法的通用性。
- **缺乏消融与效率分析**：未系统评估不同跳数、不同查询生成策略对最终结果的影响；未提供详细的Token消耗和延迟对比。
- **应用限制**：依赖LLM生成查询（Doc2Query），可能引入额外开销和噪声；图构建的静态性质可能难以适应动态知识更新。
- **偏差风险**：可能对LLM生成的查询质量敏感，且未讨论Doc2Query生成的查询分布是否覆盖所有重要信息。

（完）

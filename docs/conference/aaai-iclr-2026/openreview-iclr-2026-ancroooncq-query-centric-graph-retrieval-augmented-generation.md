---
title: Query-Centric Graph Retrieval Augmented Generation
title_zh: 以查询为中心的图检索增强生成
authors: "Yaxiong Wu, Jianyuan Bo, Yongyue Zhang, Sheng Liang, Yong Liu"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=anCrOOoncq"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向RAG长上下文与多跳检索的查询中心图索引
tldr: 图RAG在长上下文与多跳推理中面临粒度困境：细粒度实体图成本高，粗粒度文档图丢失关系。本文提出QCG-RAG，以查询为中心构建可控制粒度的图索引，并配合多跳块检索。实验表明QCG-RAG在长上下文理解任务上优于现有图RAG方法，兼顾检索质量与可解释性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有图RAG存在粒度困境，难以平衡token成本与关系捕捉，从而限制长上下文理解。
method: 提出查询中心图RAG，利用Doc2Query等方式构建可控粒度的查询中心图并实现多跳块检索。
result: QCG-RAG在长上下文与多跳推理任务上取得更优检索与生成性能。
conclusion: 查询中心图索引为长上下文RAG提供了高质、可解释的检索框架。
---

## Abstract
Graph-based retrieval-augmented generation (RAG) enriches large language models (LLMs) with external knowledge for long-context understanding and multi-hop reasoning, but existing methods face a granularity dilemma: fine-grained entity-level graphs incur high token costs and lose context, while coarse document-level graphs fail to capture nuanced relations. We introduce QCG-RAG, a query-centric graph RAG framework that enables query-granular indexing and multi-hop chunk retrieval. Our query-centric approach leverages Doc2Query and Doc2Query{-}{-} to construct query-centric graphs with controllable granularity, improving graph quality and interpretability. A tailored multi-hop retrieval mechanism then selects relevant chunks via the generated queries. Experiments on LiHuaWorld and MultiHop-RAG show that QCG-RAG consistently outperforms prior chunk-based and graph-based RAG methods in question answering accuracy, establishing a new paradigm for multi-hop reasoning.

---

## 论文详细总结（自动生成）

## 论文总结：Query-Centric Graph Retrieval Augmented Generation（QCG-RAG）

### 1. 论文的核心问题与整体含义
- **背景**：基于图的检索增强生成（Graph RAG）旨在利用外部知识增强大语言模型（LLM）的长上下文理解与多跳推理能力。
- **核心问题**：现有图 RAG 方法存在“粒度困境”（granularity dilemma）：
  - 细粒度实体级图：token 成本高，且容易丢失上下文；
  - 粗粒度文档级图：无法捕捉实体间的细微关系。
- **整体含义**：论文提出一种以查询为中心（Query-Centric）的图索引与检索框架，试图在“粒度”和“关系捕捉”之间取得更好的平衡，从而提升多跳推理与长上下文任务的问答效果。

### 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：将“查询”作为图构建与检索的基本粒度，通过查询中心图（query-centric graph）实现可控粒度索引，并配合多跳块检索（multi-hop chunk retrieval）。
- **技术细节**：
  - 使用 **Doc2Query** 和 **Doc2Query--** 两种方法为文档生成查询；
  - 基于生成的查询构建以查询为中心的图，图粒度可控，从而改善图质量与可解释性；
  - 定制化的多跳检索机制：通过已生成的查询逐步选择相关文本块（chunks）。
  - 方法名：**QCG-RAG**（Query-Centric Graph RAG）。
- **算法流程（文字描述）**：
  1. 输入：文档集合；
  2. 利用 Doc2Query / Doc2Query-- 为文档生成若干查询；
  3. 以查询为节点（或连接查询与文档/块）构建查询中心图，并可控制图的粒度；
  4. 给定用户问题，使用定制的多跳检索机制在图上游走，选取最相关的块；
  5. 将检索到的块注入 LLM，生成最终答案。

### 3. 实验设计
- **数据集/场景**：
  - **LiHuaWorld**：长上下文理解与多跳推理场景；
  - **MultiHop-RAG**：多跳检索增强生成的标准基准。
- **评估指标**：问答准确率（question answering accuracy）。
- **对比方法**：
  - 基于块（chunk-based）的 RAG 方法；
  - 基于图（graph-based）的 RAG 方法。
- **结果**：QCG-RAG 在这两个数据集上均一致优于对比方法。

### 4. 资源与算力
- 论文提供的材料中**未明确说明**使用了多少 GPU 型号、数量、训练时长等算力信息；
- 因此无法从现有内容中总结具体的计算资源投入。

### 5. 实验数量与充分性
- 从摘要可知，至少进行了**两个数据集**上的主实验（LiHuaWorld 和 MultiHop-RAG）；
- 未在提供内容中提及**消融实验**、参数敏感性分析、不同粒度控制的影响等详细实验；
- 由于信息有限，无法充分判断实验的全面性与公平性；
- 注：根据元数据，该论文在 ICLR 2026 被拒（Rejected-Public），可能意味着实验设计或论证存在不足，但具体审稿意见未知。

### 6. 主要结论与发现
- QCG-RAG 在长上下文理解与多跳推理任务上的问答准确率**一致优于**现有的基于块和基于图的 RAG 方法；
- 查询中心图索引提供了一种**高质量、可解释**的检索框架；
- 论文声称该方法为多跳推理的检索增强生成**建立了新范式**。

### 7. 优点
- **粒度可控**：通过查询中心图，可以在细粒度与粗粒度之间灵活调节，缓解粒度困境；
- **可解释性**：以查询作为图的节点，使检索路径更贴合用户意图，便于理解；
- **多跳检索**：专门设计了多跳块检索机制，适合需要跨文档推理的场景；
- **实证优势**：在两个公开基准上均取得了 outperforms 结果。

### 8. 不足与局限
- **公开信息有限**：仅摘要难以全面评价方法论细节与实验的严谨性；
- **未知计算成本**：没有提及训练/推理所需的算力，无法评估实际落地成本；
- **实验覆盖有限**：仅两个数据集，且未见消融、误差分析或可扩展性讨论；
- **应用限制**：查询中心图的构建依赖 Doc2Query 的质量，对领域迁移和噪声文档的鲁棒性未知；
- **发表状态**：该论文在 ICLR 2026 被拒，实际贡献可能仍需更多验证。

（完）

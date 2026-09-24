---
title: Query-Aware Graph Attention for Precise Subgraph Retrieval in Knowledge-Augmented Reasoning
title_zh: 面向知识增强推理中精确子图检索的查询感知图注意力
authors: "Yuanye Xu, Linyi Guo, Yue Zhang, Fu Ning"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.398.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于知识图谱的RAG，用查询-关系图注意力实现精确子图检索
tldr: 现有基于知识图谱的检索增强生成系统未能充分建模查询语义与关系类型的交互，导致子图检索不精确、多跳推理不稳定。本文提出QSRAG，构建查询-关系图注意力网络QR-GAT，将查询语义与关系嵌入直接融入注意力机制，实现细粒度三元组打分与可扩展子图构建。实验表明该方法能更精准地检索多跳证据，提升知识增强推理的稳定性，为缓解大模型幻觉、提升RAG检索精度提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-001.webp\", \"caption\": \"\", \"page\": 17, \"index\": 1, \"width\": 5970, \"height\": 3564}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-002.webp\", \"caption\": \"\", \"page\": 17, \"index\": 2, \"width\": 5970, \"height\": 3564}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-003.webp\", \"caption\": \"\", \"page\": 17, \"index\": 3, \"width\": 5970, \"height\": 3564}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-004.webp\", \"caption\": \"\", \"page\": 17, \"index\": 4, \"width\": 5970, \"height\": 3564}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-005.webp\", \"caption\": \"\", \"page\": 18, \"index\": 5, \"width\": 1079, \"height\": 973}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-006.webp\", \"caption\": \"\", \"page\": 19, \"index\": 6, \"width\": 1079, \"height\": 642}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-007.webp\", \"caption\": \"\", \"page\": 19, \"index\": 7, \"width\": 1079, \"height\": 658}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-008.webp\", \"caption\": \"\", \"page\": 20, \"index\": 8, \"width\": 1079, \"height\": 1012}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-009.webp\", \"caption\": \"\", \"page\": 21, \"index\": 9, \"width\": 1079, \"height\": 648}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-010.webp\", \"caption\": \"\", \"page\": 21, \"index\": 10, \"width\": 1079, \"height\": 670}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl398/fig-011.webp\", \"caption\": \"\", \"page\": 22, \"index\": 11, \"width\": 1079, \"height\": 718}]"
motivation: 大模型依赖外部知识缓解幻觉，但基于知识图谱的RAG难以精准检索多跳证据。
method: 提出QSRAG框架，用查询-关系图注意力网络QR-GAT将查询语义与关系嵌入融入注意力，实现细粒度三元组打分与子图构建。
result: 实验显示该方法能更精准地检索多跳证据，提升知识增强推理的稳定性。
conclusion: 为缓解大模型幻觉、提升RAG检索精度提供了新思路。
---

## Abstract
Large language models (LLMs) increasingly rely on external knowledge to mitigate hallucinations, yet retrieving precise multi-hop evidence for knowledge-augmented reasoning remains difficult. Existing Knowledge Graph (KG)-based Retrieval-Augmented Generation (RAG) systems insufficiently model the interaction between query semantics and relation types, resulting in imprecise subgraph retrieval and unstable reasoning. We propose Query-aware Subgraph Retrieval Augmented Generation (QSRAG), a retrieval framework built upon a Query-Relational Graph Attention Network (QR-GAT) that integrates query semantics and relation embeddings directly into the attention mechanism, enabling fine-grained triple scoring and scalable subgraph construction. This query–relation conditioning improves relevance estimation and suppresses noisy edges, producing faithful reasoning subgraphs. Experiments on WebQSP and CWQ establish new state-of-the-art results in both Triple Recall and Answer Recall, and significantly enhance LLMs reasoning accuracy without fine-tuning. These findings underscore the effectiveness of modeling query–relation interactions for reliable knowledge-augmented reasoning.

---

## 论文详细总结（自动生成）

# 论文总结：Query-Aware Graph Attention for Precise Subgraph Retrieval in Knowledge-Augmented Reasoning

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：大语言模型（LLM）依赖外部知识缓解幻觉，检索增强生成（RAG）是重要手段；知识图谱（KG）因结构化、多跳关系信息，特别适合知识图谱问答（KGQA）等复杂推理任务。
- **核心问题**：现有基于 KG 的 RAG 系统难以精准检索多跳证据，主要表现为三个挑战：
  - **挑战 1**：真实 KGQA 查询常依赖细微关系区分，现有方法易受冗余邻居和虚假关系干扰，难以识别正确多跳推理证据。
  - **挑战 2**：查询语义与关系类型的交互建模不足。多数图检索或 GNN 方法独立编码图结构，注意力无法根据查询意图自适应，尤其难以区分“born”与“raised”等细粒度关系。
  - **挑战 3**：多次调用 LLM 进行规划、路径扩展或迭代推理导致高延迟，限制可扩展性。
- **典型例子**：问题“Where was Rihanna raised?”的正确答案是 Saint Michael Parish，但 SubgraphRAG 因 DDE+MLP 打分缺乏显式查询–关系交互，检索到 Barbados，说明需要同时感知查询语义与关系类型的多跳检索机制。
- **整体含义**：论文提出 QSRAG，目标是通过查询–关系条件化注意力实现精准子图检索，并仅需单次 LLM 推理、无需微调，从而提升知识增强推理的准确性与效率。

## 2. 论文提出的方法论

### 2.1 整体框架

- **QSRAG 两阶段框架**：
  1. **结构化证据检索**：从 KG 中抽取与问题最相关的子图 \(S \subseteq G\)。
  2. **证据条件上下文推理**：将检索到的三元组序列化为文本证据，交给 LLM 通过上下文学习（ICL）生成答案。
- **语义编码**：使用 Qwen3-Embedding-0.6B 编码实体、关系和问题，得到实体嵌入 \(e_i\)、关系嵌入 \(r_{ij}\)、问题嵌入 \(q\)。

### 2.2 QR-GAT：查询–关系图注意力网络

- **节点初始化**：
  \[
  h_i^{(0)} = \text{Dropout}([e_i \parallel q \parallel p_i])
  \]
  其中 \(p_i\) 是标记实体是否为主题实体的 one-hot 向量。该初始化将查询语义和结构信息注入节点表示。
- **线性投影**：
  \[
  z_i^{(l)} = W_s^{(l)} h_i^{(l-1)}, \quad z_j^{(l)} = W_t^{(l)} h_j^{(l-1)}
  \]
  分别对应源节点和目标节点角色。
- **注意力分数**由结构项和查询引导项组成：
  \[
  \alpha_{ij,\text{base}}^{(l)} = a^{(l)\top} \cdot \text{LeakyReLU}(z_i^{(l)} + z_j^{(l)} + W_e^{(l)} r_{ij})
  \]
  \[
  \alpha_{ij,\text{plus}}^{(l)} = (W_q^{(l)} q)^\top \cdot (W_r^{(l)} r_{ij})
  \]
  \[
  \alpha_{ij}^{(l)} = \text{softmax}_j(\alpha_{ij,\text{base}}^{(l)} + \alpha_{ij,\text{plus}}^{(l)})
  \]
  其中 \(W_e\) 注入关系语义，\(W_q\) 和 \(W_r\) 将查询与关系投影到共享

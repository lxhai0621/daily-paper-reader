---
title: "MS-RAG: Simple and Effective Multi-Semantic Retrieval-Augmented Generation"
title_zh: MS-RAG：简单有效的多语义检索增强生成
authors: "Xiaozhou You, Yahui Luo, Lihong Gu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1151.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 结合知识图谱和密集向量的多语义RAG，提高效率并减少幻觉
tldr: 图RAG存在索引效率低、信息丢失和依赖LLM推理慢的问题。本文提出MS-RAG，将知识图谱与密集向量结合构建多语义检索，避免复杂图索引并加快检索速度。实验表明MS-RAG在跨块摘要等任务上性能超越现有图RAG方法，且显著降低计算开销。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1151/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 272, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1151/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 287, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1151/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1285, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1151/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1362, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1151/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1316, \"height\": 684, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1151/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1548, \"height\": 1018, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1394, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1545, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1550, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1384, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 757, \"height\": 382, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 771, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 793, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1481, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 852, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 691, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 733, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 799, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1653, \"height\": 779, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1436, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1151/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1333, \"height\": 216, \"label\": \"Table\"}]"
motivation: 图RAG索引效率低、信息丢失且推理依赖LLM速度慢。
method: 结合知识图谱和密集向量构建多语义RAG，无需复杂图索引。
result: 在多个任务上取得更好性能，同时降低计算开销。
conclusion: 多语义RAG是一种简单高效的RAG增强方法。
---

## Abstract
To alleviate the hallucination problem of large language model (LLM), retrieval-augmented generation (RAG) has been proposed and widely adopted. Due to the limitations in cross-chunk summarization task of naive RAG, graph-based RAG has emerged as a promising solution. However, a close study reveals several flaws in these works. First, most graph-based RAGs suffer from less efficient indexing process, which leads to information loss and expensive costs. Second, they heavily rely on LLM for retrieval thus inference slowly, which hinders their application in industry. To build a more efficient and effective RAG, we propose the multi-semantic RAG (MS-RAG). In this work, we combine knowledge graphs with dense vector to build a multi-semantic RAG. To be specific, (i) at indexing stage, we create multiple semantic-level indexes, including chunk-level, relation-level, and entity-level, to leverage the merits of dense vector and knowledge graph. (ii) at retrieval stage, unlike the previous LLM-empowered entity extraction, we propose a novel mix recall algorithm. Finally, we employ a multi-semantic rerank module to purify the results. Extensive experiments show that MS-RAG achieves superior performance. In terms of retrieval effect, MS-RAG achieves state-of-the-art performance, which is about 10%-30% improvement than the existing methods. In terms of question-answering effect, MS-RAG still achieves promising results with faster inference speed. More analysis and experiments are provided in Appendix.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有图检索增强生成（Graph-based RAG）方法存在两大缺陷：（1）索引阶段效率低下，依赖LLM构建知识图谱时容易产生信息丢失（缺失节点/边占比高达10-30%），且成本高昂；（2）检索阶段过度依赖LLM进行实体提取，推理速度慢，难以在工业场景中大规模应用。
- **整体含义**：本文旨在构建一种更高效、更准确的RAG系统，通过融合知识图谱与密集向量检索的优势，克服上述缺陷，实现快速且精准的多语义检索与生成。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **MS-RAG（Multi-Semantic RAG）**：在索引阶段建立多语义索引（块级、关系级、实体级），在检索阶段采用混合召回算法与多语义重排序模块，将密集向量检索与知识图谱结构优势互补。

### 关键技术细节
- **离线索引（Indexing Stage）**：
  - 构建三个数据库：**实体数据库**（存储名词/人物及相邻实体/关系）、**关系数据库**（存储声明性句子及其向量）、**块数据库**（存储原始文本块）。
  - 所有数据库均使用密集向量模型（如BGE-M3、Contriever）编码。
  - 额外进行**实体/关系摘要**（为LLM提供丰富提示）和**实体消歧**（合并同名实体，如“Clarence Fred Gehrke”与“Fred Gehrke”）。
- **在线检索（Retrieval Stage）**：
  - **混合召回算法（Mix Recall）**：包含两个子步骤：
    - **图元素召回**：使用向量搜索（而非LLM）提取λ1=5个实体和λ2=10个关系；然后进行语义邻居搜索，召回λh=4跳内的相邻关系/实体。
    - **块召回**：直接向量搜索，取λ3=10个最相似块。
  - **多语义重排序模块（Multi-Semantic Rerank）**：
    - **投票**：对来自不同召回源（实体、关系、块）的候选段落进行加权投票，选取前λ4=5个段落。
    - **重排序**：使用轻量级LLM（Qwen-7B）对候选段落进行排序，仅输出排序序号以加速推理。
- **算法流程（文字说明）**：
  1. 输入查询q
  2. 对图索引进行向量搜索，得到候选关系和实体
  3. 对块索引进行向量搜索，得到候选块
  4. 对候选关系和实体进行近邻搜索，扩展图元素
  5. 对块、关系、实体结果进行投票，选出前K个段落
  6. 使用轻量LLM对段落进行重排序，输出最终结果

## 3. 实验设计

### 数据集
- **HotpotQA**：113k个多跳问答对，选取约9k篇文档，1,000个问题。
- **2WikiMultiHopQA**：约6k篇文档，1,000个问题。
- **MuSiQue（可回答子集）**：约12k篇文档，1,000个问题。
- 额外简单QA任务：NaturalQA（1k）、PopQA（1k）、TriviaQA（2k）。

### 基准方法
- **单步检索**：BM25、Contriever、GTR、ColBERTv2、BGE-M3、RAPTOR、Propositionizer、HippoRAG。
- **多步检索**：IRCoT+BM25、IRCoT+Contriever、IRCoT+ColBERTv2、IRCoT+HippoRAG。
- **问答性能**：GraphRAG、HippoRAG。
- **消融实验**：对多语义索引、重排序模块、混合召回各组件、索引LLM（GPT-3.5、Llama-3-8B/70B、REBEL）、实体消歧等进行消融。

### 评估指标
- **检索**：R@2、R@5（top2/top5召回率），附加F1、EM、MRR。
- **问答**：正确性、多样性、理解性、总体（由Qwen-32B评分）。

## 4. 资源与算力

- 文中**未明确说明**使用的GPU型号、数量及训练时长。
- 使用的模型：GPT-3.5-turbo-1106（温度0）作为LLM构建索引；Qwen-7B用于重排序；Qwen-32B用于问答评估；BGE-M3和Contriever作为检索器。
- 推理时间对比：MS-RAG平均0.76s，HippoRAG 0.88s，GraphRAG 4.12s（基于100个样本）。
- 存储成本：MS-RAG多语义索引约2.4G，HippoRAG约2.1G。

## 5. 实验数量与充分性

- **实验数量充分**：包括单步检索（3个数据集×2个指标）、多步检索（3个数据集×2个指标）、问答对比（2组配对）、多组消融实验（模块消融、LLM消融、召回组件消融、重排序消融、实体消歧消融、错误分析、简单QA扩展实验、存储成本与API调用对比）。
- **公平性**：与当前SOTA（HippoRAG、GraphRAG）在同一数据集、相同评价设置下比较；消融实验系统评估每个组件贡献；使用相同的检索器骨干（BGE-M3/Contriever）进行公平对比。
- **局限性**：仅测试三个多跳QA数据集及三个简单QA数据集，未覆盖更多领域（如医疗、金融）；实验规模为1,000个样本，属于中等规模。

## 6. 主要结论与发现

- MS-RAG在单步检索上平均R@2达68.9%（BGE-M3版本），比最佳基线HippoRAG（57.2%）提升约20.5%；R@5提升8.4%。
- 多步检索中，MS-RAG平均R@2达71.8%，R@5达81.9%，显著优于IRCoT+HippoRAG（66.2%/77.1%）。
- 问答性能：MS-RAG总体评分61.8%，远高于GraphRAG（38.2%）和HippoRAG（40.6%）；推理速度比GraphRAG快5倍以上，略快于HippoRAG。
- 消融实验证实每个组件（多语义索引、混合召回、重排序、实体消歧）均有显著贡献。
- 索引LLM的选择：GPT-3.5-turbo最佳，Llama-3-70B接近，REBEL最差。

## 7. 优点

- **方法新颖**：首次将块级、实体级、关系级多语义索引与混合召回、投票重排序有机结合，有效弥补LLM构建图时缺失节点/边的缺陷。
- **效率高**：检索阶段避免使用LLM提取实体，改用向量搜索，大幅降低推理延迟（0.76s）；索引阶段仅需一次LLM调用构建图，无需层次聚类等复杂步骤。
- **鲁棒性强**：在多个数据集上一致领先，且在简单QA任务上同样表现优秀；错误分析表明主要误差来自召回（52%），而非图构建（26%）或重排序（22%），为后续改进指明方向。
- **工业适用性**：推理速度、存储成本与性能平衡良好，适合大规模部署。

## 8. 不足与局限

- **未披露训练/推理算力细节**：未说明GPU型号、数量及训练时长，难以复现成本。
- **实验覆盖有限**：仅测试三个多跳QA数据集和三个简单QA数据集；未涉及长文档、对话、实时场景等。
- **索引依赖LLM质量**：即使有块缓解，图构建仍依赖LLM（10-30%缺失），弱模型（REBEL）性能下降明显；未探索更鲁棒的图构建方法（如基于规则的抽取）。
- **重排序模块依赖模型**：使用Qwen-7B，未测试更大模型或更轻模型；重排序本身也会带来误差（22%）。
- **缺乏与其他最新RAG方法（如LightRAG、StructRAG）的对比**：论文中未提及，可能因时间原因。
- **投票机制简单**：仅基于出现频率，未考虑权重或置信度，可能丢失低频率但关键信息。

（完）

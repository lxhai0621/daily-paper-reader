---
title: "RAG over Tables: Hierarchical Memory Index, Multi-Stage Retrieval, and Benchmarking"
title_zh: 面向表格的RAG：分层记忆索引、多阶段检索与基准评测
authors: "Jiaru Zou, Dongqi Fu, Sirui Chen, Xinrui He, Zihao Li, Yada Zhu, Jiawei Han, Jingrui He"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1902.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向表格的RAG与分层记忆索引整合结构化知识
tldr: 检索增强生成通常假设知识以纯文本存储，但现实中大量知识分布在多张表格中，跨表检索与整合仍不成熟。本文提出面向表格的RAG方法，包含分层记忆索引与多阶段检索，并构建相应评测基准，以有效理解表内与表间知识并筛选最相关表格。研究回答了复杂检索上下文如何组织供大模型推理的问题，显著提升了答案相关性与准确性，为结构化与非结构化知识库融合提供了可行路径。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 1395, \"height\": 1399}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 2325, \"height\": 1437}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 8950, \"height\": 3600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-004.webp\", \"caption\": \"\", \"page\": 5, \"index\": 4, \"width\": 2171, \"height\": 1102}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-005.webp\", \"caption\": \"\", \"page\": 15, \"index\": 5, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-006.webp\", \"caption\": \"\", \"page\": 15, \"index\": 6, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-007.webp\", \"caption\": \"\", \"page\": 15, \"index\": 7, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-008.webp\", \"caption\": \"\", \"page\": 15, \"index\": 8, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-009.webp\", \"caption\": \"\", \"page\": 15, \"index\": 9, \"width\": 561, \"height\": 575}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-010.webp\", \"caption\": \"\", \"page\": 15, \"index\": 10, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-011.webp\", \"caption\": \"\", \"page\": 15, \"index\": 11, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-012.webp\", \"caption\": \"\", \"page\": 15, \"index\": 12, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-013.webp\", \"caption\": \"\", \"page\": 15, \"index\": 13, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-014.webp\", \"caption\": \"\", \"page\": 15, \"index\": 14, \"width\": 713, \"height\": 742}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-015.webp\", \"caption\": \"\", \"page\": 15, \"index\": 15, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-016.webp\", \"caption\": \"\", \"page\": 15, \"index\": 16, \"width\": 522, \"height\": 239}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-017.webp\", \"caption\": \"\", \"page\": 15, \"index\": 17, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-018.webp\", \"caption\": \"\", \"page\": 15, \"index\": 18, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-019.webp\", \"caption\": \"\", \"page\": 15, \"index\": 19, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-020.webp\", \"caption\": \"\", \"page\": 18, \"index\": 20, \"width\": 5981, \"height\": 2152}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1902/fig-021.webp\", \"caption\": \"\", \"page\": 20, \"index\": 21, \"width\": 1183, \"height\": 1491}]"
motivation: 现实中大量知识存于表格，跨表检索与整合对RAG仍很困难。
method: 提出分层记忆索引与多阶段检索，并构建表格RAG评测基准。
result: 方法提升了对表内表间知识的理解与答案相关性和准确性。
conclusion: 为结构化与非结构化知识库融合提供了可行路径。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances Large Language Models (LLMs) by integrating them with an external knowledge base to improve the answer relevance and accuracy. In real-world scenarios, beyond pure text, a substantial amount of knowledge is stored in tables, and user questions often require retrieving answers that are distributed across multiple tables. Retrieving knowledge from a table corpora (i.e., various individual tables) for a question remains nascent, for (i) how to understand intra- and inter-table knowledge effectively, (ii) how to filter unnecessary tables and retrieve the most relevant tables efficiently, (iii) how to organize complex retrieved contexts for LLMs’ reasoning, and (iv) how to evaluate the corresponding performance in a realistic setting. Facing the above challenges, in this paper, we first propose a table-corpora-aware RAG framework, named T-RAG, which consists of the hierarchical memory index, multi-stage retrieval, and graph-aware context organization for effective and efficient table knowledge retrieval and inference. Then, we develop a multi-table question answering benchmark named MultiTableQA, which spans 3 different task types, 57,193 tables, and 23,758 questions in total, and the sources are all from real-world scenarios. Based on MultiTableQA, we perform a comprehensive comparison of table retrieval methods, RAG-based approaches, and table-to-graph representation learning methods. T-RAG consistently achieves state-of-the-art accuracy, recall, and runtime performance, with improvements of up to 9.4%. Moreover, T-RAG yields an average inference gain of 11.8% across different downstream backbone LLMs. Our code and data are available at https://github.com/jiaruzouu/T-RAG.

---

## 论文详细总结（自动生成）

# 论文总结：RAG over Tables: Hierarchical Memory Index, Multi-Stage Retrieval, and Benchmarking

## 1. 核心问题与整体含义
- 背景：RAG 通过外部知识库增强 LLM，提升答案相关性与准确性；但现有 RAG 主要面向纯文本知识。
- 现实问题：大量知识存储在表格中，且用户问题常需跨多张表检索与推理。跨表 RAG 仍不成熟。
- 四个核心挑战：
  - 如何有效理解表内与表间知识；
  - 如何高效过滤无关表并检索最相关表；
  - 如何组织复杂的结构化与文本混合上下文供 LLM 推理；
  - 如何构建贴近真实场景的评测基准。
- 整体含义：论文提出面向表格语料的 RAG 框架 **T-RAG**，并构建多表问答基准 **MultiTableQA**，推动 RAG 从纯文本走向结构化表格知识。

## 2. 方法论
### 2.1 总体框架
- T-RAG 包含三个协同组件：
  - 分层记忆索引：将大规模表格语料组织为异构超图；
  - 多阶段检索：粗粒度多路检索 + 细粒度子图检索；
  - 图感知上下文组织：将图结构与关系分数注入 LLM 提示，引导推理。

### 2.2 表到图构建
- 表格线性化：
  - 将表名、表标题、列头拼接为序列，例如用 `[Table]`、`[Caption]`、`[Header]` 等特殊标记保留结构。
  - 公式含义：`s = [Table] ⊕ ([Caption], A) ⊕ ⊕_{k=1}^M ([Header], h_k)`。
- 多路特征提取：
  - 语义特征 `x(sem)`：句编码器；
  - 结构特征 `x(struct)`：spaCy 提取 token 数、POS 频率、标点等；
  - 启发式特征 `x(heur)`：TF-IDF 词袋表示。
- 异构超图构建：
  - 每种特征类型分别做 KMeans 聚类，每个簇作为一个超边；
  - 超边连接同簇表格节点，不同类型超边形成异构性；
  - 超边集合为不同特征类型下所有簇的并集。

### 2.3 粗粒度多路检索
- 代表分数：本质为余弦相似度，用于衡量节点与节点、节点与查询在某一特征类型下的代表性。
- 典型节点选择：
  - 对每个簇，选择与簇质心代表分数最高的 top-k 节点，形成典型节点集 `V_typ`。
- 查询-簇分配：
  - 查询同样提取多路特征；
  - 对每种特征类型，选择查询与典型节点平均相似度最高的簇；
  - 最终最优簇为各特征类型最优簇的并集 `C*`。
- 目的：以较低计算成本快速缩小候选表范围，同时保留高召回。

### 2.4 细粒度子图检索
- 局部子图构建：
  - 在粗粒度最优簇上，根据表格间语义相似度是否超过阈值 `τ` 建立边；
  - 边权为代表分数。
- 个性化 PageRank 检索：
  - 构造候选节点相似度矩阵，行归一化得到转移矩阵 `P`；
  - 查询与候选节点的语义相似度归一化得到个性化向量 `h`；
  - 迭代更新：`v(σ+1) = (1-α)h + αPv(σ)`；
  - 收敛后按 PageRank 分数排序，取 top 节点作为最终检索表集合 `V_final`。

### 2.5 图感知上下文组织
- 图信息插入：
  - 将节点索引、节点间相似度分数等图关系嵌入提示词。
- 分层长链式思维：
  - 引导 LLM 先识别最相关表，再解释查询与表的关系，再逐行逐列检查；
  - 输出分为 `<reasoning>` 推理过程和 `<answer>` 最终答案。
- 多步提示：
  - 高亮图信息；
  - 给出表检索指令；
  - 给出长 CoT 输出格式要求。

## 3. 实验设计
- 基准：**MultiTableQA**
  - 三类任务：
    - Table-based Fact Verification，TFV；
    - Single-hop Table Question Answering，Single-hop TQA；
    - Multi-hop Table Question Answering，Multi-hop TQA。
  - 摘要称规模：57,193 张表、23,758 个问题；表 1 分项为 TFV 34,351 表/15,106 查询，Single-hop 17,229 表/6,106 查询，Multi-hop 5,523 表/2,573 查询。
  - 数据来源：HybridQA、SQA、Tabfact、WikiTables 等真实人工标注单表数据。
  - 构建方式：行列拆分原始表，查询组合与去语境化；避免 LLM 合成查询与答案带来的偏差。
- 对比方法：
  - 表检索：DTR、Table-Contriever、Table-E5、Table-LLaMA；
  - RAG：RALM、ColBERT；
  - 表到图表示：单特征（heur/struc/sem）、Lattice、TaBERT、TAPAS；
  - 表提示方法：TAP4LLM。
- 下游 LLM：
  - Phi-3.5-mini、LLaMA-3.2-3B、Qwen-2.5-7B、LLaMA-3.1-8B、LLaMA-3.1-70B；
  - Claude-3.5-Sonnet、GPT-4o-mini、GPT-4o。
- 指标：
  - 检索：Acc@k、Recall@k，k 取 10、20、50；
  - 下游推理：EM、F1；
  - 效率：端到端延迟、候选表数量下降。
- 泛化实验：
  - 在 Spider 数据集上验证单表检索场景下的泛化能力。

## 4. 资源与算力
- 论文未明确说明使用的 GPU 型号、数量、训练时长或总计算量。
- 仅提供推理相关设置：
  - temperature = 0.1；
  - max output tokens = 4096；
  - top-p = 0.95；
  - 明确列出使用的闭源与开源 LLM 版本。
- 因此，无法从文中评估训练成本、微调成本或硬件资源规模。

## 5. 实验数量与充分性
- 主要实验组：
  - 表 2：三个任务上的检索准确率

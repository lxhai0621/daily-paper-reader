---
title: "REaR : Retrieve, Expand and Refine for Effective Multitable Retrieval"
title_zh: REaR：面向高效多表检索的检索、扩展与精炼框架
authors: "Rishita Agarwal, Himanshu Singhal, Peter Baile Chen, Manan Roy Choudhury, Dan Roth, Vivek Gupta"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1826.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 区分语义相关与结构可连接的多表检索
tldr: 关系型数据上的自然语言查询常需检索并推理多张表，但多数检索器仅优化查询与表的相关性，忽略表与表之间的兼容性。本文提出REaR三阶段无LLM框架，先检索与查询对齐的表，再通过预计算列嵌入比较扩展结构可连接的表，最后剪枝噪声候选。该方法与检索器无关，在复杂表格问答数据集上持续提升稠密与稀疏检索器效果，兼顾语义相关与结构可连接性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1826/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 1635, \"height\": 2027}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1826/fig-002.webp\", \"caption\": \"\", \"page\": 8, \"index\": 2, \"width\": 1526, \"height\": 385}]"
motivation: 多表查询需检索并推理多张表，但现有检索器只优化查询-表相关性，忽略表间结构兼容性。
method: 提出REaR三阶段无LLM框架：检索查询对齐表、扩展结构可连接表、剪枝噪声候选。
result: 该方法与检索器无关，在复杂表格问答数据集上持续提升稠密与稀疏检索器表现。
conclusion: 兼顾语义相关与结构可连接性，为多表检索提供高效框架。
---

## Abstract
Answering natural language queries over relational data often requires retrieving and reasoning over multiple tables, yet most retrievers optimize only for query–table relevance and ignore table–table compatibility. We introduce REaR (Retrieve, Expand and Refine), a three-stage, LLM-free framework that separates semantic relevance from structural joinability for efficient, high-fidelity multi-table retrieval. REaR (i) retrieves query-aligned tables, (ii) expands these with structurally joinable tables via fast, precomputed column-embedding comparisons, and (iii) refines them by pruning noisy or weakly related candidates. Empirically, REaR is retriever-agnostic and consistently improves dense/ sparse retrievers on complex table QA datasets (BIRD, MMQA, and Spider) by improving both multi-table retrieval quality and downstream SQL execution. Despite being LLM-free, it delivers performance competitive with state-of-the-art LLM-augmented retrieval systems (e.g., ARM) while achieving much lower latency and cost. Ablations confirm complementary gains from expansion and refinement, underscoring REaR as a practical, scalable building block for table-based downstream tasks (e.g., Text-to-SQL).

---

## 论文详细总结（自动生成）

# 论文总结：REaR：Retrieve, Expand and Refine for Effective Multitable Retrieval

## 1. 核心问题与整体含义（研究动机和背景）

- 关系型数据库上的自然语言查询与 Text-to-SQL 任务，常需要检索并推理多张表。
- 现有检索器大多只优化“查询—表相关性”（query–table relevance），忽略“表—表兼容性/可连接性”（table–table compatibility / joinability）。
- 这种“只看相关性”的检索会返回主题相关但结构上无法连接的表，导致下游 SQL 生成器被迫猜测 JOIN、遗漏约束或幻觉连接，最终生成无效或不完整 SQL。
- 论文的核心主张是：多表检索应同时评分两类信号：  
  1. 主题相关性：表内容是否与查询相关；  
  2. 关系适配性：表之间是否可连接，能否组合证据回答查询。
- 为此，作者提出 REaR（Retrieve, Expand and Refine），一个三阶段、在线检索阶段不调用 LLM 的多表检索框架，目标是在低延迟、低成本下实现高保真多表检索，并提升下游 Text-to-SQL 执行准确率。

## 2. 方法论：核心思想、关键技术细节与流程

- 核心思想：将“查询—表语义相关性”与“表—表结构可连接性”解耦建模，通过离线预计算列嵌入和在线轻量排序完成高效多表检索。
- 整体流程为三阶段：
  1. **Retrieve（检索）**：用标准稠密、稀疏或混合检索器选出 top-k′ 个语义相关基础表 \(T_{base}\)。
     - 稀疏检索：TF-IDF / BM25 / SPLADE 等基于词项重叠。
     - 稠密检索：查询与表嵌入的余弦相似度。
     - 混合检索：\(s_{hybrid}=\alpha \cdot s_{sparse}+(1-\alpha)\cdot s_{dense}\)。
  2. **Expand（扩展）**：加入与基础表结构可连接的表，提升召回与可组合性。
     - 将列名和值序列化后编码为列嵌入。
     - 两表可连接定义为：两表列嵌入最大余弦相似度 \(\max sim(c_i,c_j)\ge \tau\)，实验中 \(\tau=0.7\)。
     - 使用 FAISS 近似最近邻搜索避免全列对比较，降低复杂度。
     - 对每个基础表枚举可连接表，形成候选集 \(T_c\)。
     - 用 cross-encoder 重排序器按查询—表相关性筛选 top-\(\Delta k'\)，得到 \(T_{join}\)，扩展集为 \(T_{expanded}=T_{base}\cup T_{join}\)。
  3. **Refine（精炼）**：联合查询相关性和表间可连接性剪枝、重排，恢复精度。
     - 对扩展集中每张表 \(T_i\) 计算综合分数：  
       \[
       S(T_i)=C2(q,T_i)\cdot A(T_i)
       \]
     - \(C2(q,T_i)\) 为 cross-encoder 计算的查询—表相关性。
     - \(A(T_i)\) 为表—表 joinability 注意力式得分：对邻域表对相似度做 softmax，取最大归一化分数并乘以对应相似度，以抑制弱相关表。
     - 表对相似度取两表所有列对的最大 cross-encoder 相似度。
     - 最终返回 top-k 表。
- 关键特点：
  - 在线检索阶段不调用 LLM。
  - 重计算离线完成，查询时复杂度约为 \(O(KT)\)，其中 \(K\in[5,8]\)。
  - 框架与基础检索器无关，可插拔式提升 dense / sparse / hybrid 检索器。
- 注意：论文声称“LLM-free”主要针对检索流程；离线生成表描述时仍使用了 Gemini-1.5-Flash。

## 3. 实验设计：数据集、Benchmark 与对比方法

- 数据集：
  - **BIRD**：75 张表，1534 条查询，平均每表约 52436 行、10.64 列。
  - **Spider**：139 张表，1034 条查询，平均每表约 6742 行、5.51 列。
  - **MMQA**：695 张表，3312 条查询，平均每表约 1732 行、5.77 列。
  - 为增加检索难度，作者将各数据集的数据库合并为单一表语料，避免“小库内检索所有表即高召回”的平凡情形。
- 任务与评价指标：
  - 检索性能：Precision、Recall、Full Recall（所有金标准表是否都被检索到）。
  - 端到端性能：SQL execution accuracy，即生成 SQL 与金标准 SQL 执行结果是否一致。
  - 也讨论了 reasoning fidelity，但主要指标为上述两类。
- 对比方法：
  - 标准检索器：
    - 稀疏：BM25、SPLADE。
    - 稠密：UAE-Large-V1、GTE-large、e5-mistral、BGE-large-en。
    - 混合：SPLADE Hybrid。
  - LLM 增强检索方法：ARM、JAR、ReAcT、MURRE 等。
  - SQL 生成模型：Gemini-2.0-Flash、Llama-3.2-3B、Gemma-3-4B。
  - 上界对照：Oracle Retrieval、Oracle Prune。
- 实现细节：
  - 表序列化包含

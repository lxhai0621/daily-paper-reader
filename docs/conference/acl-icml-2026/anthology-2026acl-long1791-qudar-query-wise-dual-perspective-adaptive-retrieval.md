---
title: "QuDAR: Query-Wise Dual-Perspective Adaptive Retrieval"
title_zh: QuDAR：查询级别的双视角自适应检索
authors: "Joeun Kim, Seunghyouk Yoon, Xuan-Bach Le, Youngeun Nam, Doyoung Kim, Hwanjun Song, Jae-Gil Lee"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1791.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向RAG的查询自适应稀疏与稠密检索加权
tldr: RAG 系统依赖检索模块提供依据，但混合稀疏与稠密检索多采用固定权重，忽视查询与语料差异，查询扩展与原始查询的融合也常是静态的并引入噪声。为此提出 QuDAR，从检索器类型与查询形式两个视角自适应调节，利用分数间隔得到的置信度与大模型盲评相关性，动态分配查询级权重。该方法提升了检索准确性与鲁棒性，为改进 RAG 效果提供了通用方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-002.webp\", \"caption\": \"\", \"page\": 5, \"index\": 2, \"width\": 2048, \"height\": 904}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-003.webp\", \"caption\": \"\", \"page\": 6, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-004.webp\", \"caption\": \"\", \"page\": 6, \"index\": 4, \"width\": 684, \"height\": 413}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-005.webp\", \"caption\": \"\", \"page\": 6, \"index\": 5, \"width\": 586, \"height\": 635}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-006.webp\", \"caption\": \"\", \"page\": 6, \"index\": 6, \"width\": 535, \"height\": 571}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-007.webp\", \"caption\": \"\", \"page\": 6, \"index\": 7, \"width\": 2048, \"height\": 1152}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-008.webp\", \"caption\": \"\", \"page\": 14, \"index\": 8, \"width\": 2048, \"height\": 904}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-009.webp\", \"caption\": \"\", \"page\": 14, \"index\": 9, \"width\": 2048, \"height\": 904}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1791/fig-010.webp\", \"caption\": \"\", \"page\": 14, \"index\": 10, \"width\": 2048, \"height\": 904}]"
motivation: 混合检索多采用固定权重，忽视查询与语料差异，查询扩展融合静态且易引入噪声。
method: 提出 QuDAR，从检索器类型与查询形式双视角，用分数间隔置信度与大模型相关性打分动态加权。
result: 实现查询级自适应检索融合，提升检索的准确性与鲁棒性。
conclusion: 为提升 RAG 检索质量提供了自适应加权框架。
---

## Abstract
Retrieval-augmented generation(RAG) systems depend on retrieval modules to supply grounding evidence for large language models. While hybrid approaches combining sparse and dense retrievers improve performance, most rely on fixed weights that ignore query-specific and corpus-specific variation. Similarly, query expansion has long been used to enrich recall, but its integration with original queries is usually static and can introduce noise. We present QuDAR, a dual-perspective adaptive retrieval framework that adapts along two perspectives: retriever type (sparse vs. dense) and query format (original vs.expanded). Leveraging margin-derived confidence (e.g., top-1–top-2 score gaps) and blind LLM-based relevance scoring, QuDAR dynamically assigns query-specific weights, fusing lexical specificity with semantic breadth while mitigating noise. QuDAR is lightweight, retriever-agnostic, and broadly applicable. Experiments show consistent gains over static baselines, improving overall retrieval quality and yielding more stable performance across queries.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：RAG 系统依赖检索模块为大语言模型提供外部依据，检索质量直接影响问答、摘要等下游任务。稀疏检索（如 BM25）擅长词汇精确匹配，稠密检索（如 Contriever）擅长语义相似，两者互补。
- **核心问题**：现有混合检索多采用**固定权重**融合稀疏与稠密信号，忽略查询级和语料级差异；查询扩展虽能提升召回，但与原始查询的融合通常也是静态的，可能引入噪声、造成查询漂移。
- **论文主张**：检索效果由两个视角共同决定——**检索器类型**（稀疏 vs. 稠密）与**查询形式**（原始 vs. 扩展）。这两个视角相互依赖，存在组合效应，静态启发式无法充分利用。
- **整体含义**：论文提出 QuDAR，将双视角检索融合转化为**查询级自适应加权**问题，目标是在不训练、不依赖特定检索器的前提下，动态分配四路检索信号的权重，从而提升检索鲁棒性和 RAG 生成质量。

## 2. 方法论

### 2.1 问题形式化

- 给定查询 \(q\) 与文档语料 \(D\)，应用双视角得到四个检索输出：
  - \(R_{OS}(q)\)：原始查询 + 稀疏检索；
  - \(R_{OD}(q)\)：原始查询 + 稠密检索；
  - \(R_{ES}(q)\)：扩展查询 + 稀疏检索；
  - \(R_{ED}(q)\)：扩展查询 + 稠密检索。
- 每个输出提供排序列表与文档分数。目标是学习查询级权重 \(w_{OS}, w_{OD}, w_{ES}, w_{ED} \in [0,1]\)，且 \(\sum_i w_i = 1\)。
- 混合检索函数为：\(R_{hybrid}(q) = \sum_{i \in \{OS,OD,ES,ED\}} w_i \cdot R_i(q)\)。
- 优化目标：寻找权重 \(w^* = \arg\max_w S(R_{hybrid}(q))\)，其中 \(S(\cdot)\) 为检索质量评分函数。

### 2.2 三种训练免费加权策略

- **QuDAR-simple**：
  - **RRF 融合**：用倒数排名融合四路结果，\(score_{RRF}(d)=\sum_i 1/(k+rank_i(d))\)，优先保留任一检索器高排名的文档，平滑噪声。
  - **等权融合**：对四路归一化分数取平均，\(score_{Equal}(d)=\frac{1}{4}\sum_i score_i(d)\)，利用分数分布信息。
- **QuDAR-confidence**：
  - 对每路检索信号计算置信度间隔：\(m_i = \max(score_{i,1} - score_{i,2}, 0)\)，即 top-1 与 top-2 的归一化分数差。
  - 间隔越大，说明该路排序越自信。通过带温度 \(\tau\) 和防零项 \(\epsilon\) 的 softmax 将间隔转为权重：\(w_i = \exp((m_i+\epsilon)/\tau) / \sum_j \exp((m_j+\epsilon)/\tau)\)。
  - 该方法无需额外 LLM 调用，属于轻量自适应。
- **QuDAR-llm**：
  - 将四路 top-1 段落与查询交给 LLM，要求按 0–5 分评估相关性；使用 gpt-4o-mini。
  - 为避免检索器类型或展示顺序偏差，段落随机打乱，评分后再映射回原始检索源。
  - 将 LLM 分数通过 softmax 转为权重：\(w_i = \exp((score^{LLM}_i+\epsilon)/\tau) / \sum_j \exp((score^{LLM}_j+\epsilon)/\tau)\)。
  - 该方法扩展了 DAT 的思想，从仅调检索器类型权重扩展到同时处理检索器类型与查询形式。

## 3. 实验设计

- **数据集 / Benchmark**：
  - 主要使用 BEIR 中的四个数据集：FiQA、SciDocs、HotpotQA、Climate-FEVER。
  - 领域覆盖金融问答、科学文献检索、多跳问答、气候变化事实核查。
  - 论文实验部分称“五个数据集”，但表 9 仅列出四个，正文主实验也主要围绕四个展开，存在表述不一致。
- **检索器与查询扩展**：
  - 稀疏检索器：BM25；稠密检索器：Contriever。
  - 扩展查询由 LLaMA 3.1-8B 生成，采用 self-contained passage / HyDE 风格重写。
  - 泛化实验还测试 SPLADE++、E5-base、BGE-M3，以及 PRF、HyDE 等扩展方式。
- **对比方法**：
  - **单路检索器**：Original-Sparse、Original-Dense、Expanded-Sparse、Expanded-Dense。
  - **单视角混合**：
    - 检索器类型混合：Static Avg、Grid-searched Static UB、DAT。
    - 查询形式混合：Static Avg、Grid-searched Static UB。
  - **双视角混合**：Static Avg、Grid-searched Static UB、QuDAR 三种变体。
- **评价指标**：Recall@10、nDCG@10、Precision@1；附录还报告 MAP@10、MRR@20。
- **生成实验**：
  - 在 FiQA 与 HotpotQA 上各采样 500 条查询。
  - 用 Qwen2.5-7B 生成答案并做 LLM-based 评估，比较检索改进是否传递到生成质量。
- **分析实验**：
  - 稀疏–稠密权重 \(\alpha\) 从 0 到 1 以 0.1 步长扫描。
  - 原始–扩展权重 \(\beta\) 从 0 到 1 扫描。
  - 查询级最优上界分析、双视角组合热图分析。
- **成本分析**：统计 QuDAR-llm 使用 gpt-4o-mini 的时延、token 与费用。

## 4. 资源与算力

- 论文方法为**训练免费**，没有报告训练 GPU 型号、数量或训练时长。
- 使用的模型包括：
  - LLaMA 3.1-8B

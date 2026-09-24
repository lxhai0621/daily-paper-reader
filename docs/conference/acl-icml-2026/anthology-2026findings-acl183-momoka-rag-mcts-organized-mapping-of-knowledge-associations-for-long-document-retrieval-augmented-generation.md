---
title: "Momoka-RAG: MCTS-Organized Mapping of Knowledge Associations for Long-Document Retrieval Augmented Generation"
title_zh: Momoka-RAG：面向长文档检索增强生成的MCTS知识关联映射
authors: "Wenyu Tao, Xiaofen Xing, Zeliang Li, Xiangmin Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.183.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 基于蒙特卡洛树搜索的知识关联组织用于长文档RAG
tldr: 现有检索增强生成框架在构建知识结构时较为被动机械，只能发现块之间的浅层关联，缺乏对深层语义关系的主动探索。本文提出Momoka-RAG，利用蒙特卡洛树搜索构建Momoka-Map主动挖掘块间联系并生成最优语义信息路径，再由Momoka-Trail检索器扩展与细化检索。该方法提升了长文档场景下的检索质量与生成相关性，为增强RAG准确性与语义组织提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 1376, \"height\": 768}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 2094, \"height\": 1305}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-003.webp\", \"caption\": \"\", \"page\": 16, \"index\": 3, \"width\": 1125, \"height\": 578}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-004.webp\", \"caption\": \"\", \"page\": 16, \"index\": 4, \"width\": 1126, \"height\": 382}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-005.webp\", \"caption\": \"\", \"page\": 16, \"index\": 5, \"width\": 1125, \"height\": 542}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-006.webp\", \"caption\": \"\", \"page\": 17, \"index\": 6, \"width\": 1376, \"height\": 1193}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-007.webp\", \"caption\": \"\", \"page\": 17, \"index\": 7, \"width\": 1931, \"height\": 3593}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-008.webp\", \"caption\": \"\", \"page\": 17, \"index\": 8, \"width\": 3266, \"height\": 2954}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-009.webp\", \"caption\": \"\", \"page\": 17, \"index\": 9, \"width\": 3506, \"height\": 2809}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-010.webp\", \"caption\": \"\", \"page\": 17, \"index\": 10, \"width\": 3506, \"height\": 2664}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl183/fig-011.webp\", \"caption\": \"\", \"page\": 18, \"index\": 11, \"width\": 1378, \"height\": 773}]"
motivation: 现有RAG被动构建知识结构，仅能发现块间浅层关联。
method: 用蒙特卡洛树搜索构建语义路径，并设计Trail检索器扩展检索。
result: 方法提升了长文档检索质量与生成相关性。
conclusion: 为增强RAG准确性与语义组织提供新思路。
---

## Abstract
Existing frameworks remain trapped in a passive and mechanical approach in constructing knowledge structure, which only allows them to uncover superficial associations between chunks while lacking proactive exploration of deeper semantic relationships among them. To address the aforementioned issues, we propose **Momoka-RAG** (MCTS-Organized Mapping of Knowledge Associations for Long-Document Retrieval Augmented Generation). It employs the **Momoka-Map** to utilize Monte Carlo Tree Search (MCTS) to proactively uncover connections among chunks and construct optimal semantic information paths with the objective of completing semantic relationships. On this basis, the **Momoka-Trail Retriever** further expands and filters the chunk candidate pool to retrieve the chunks most relevant to the query. Experiments on datasets including Dragonball, SQUAD, NFCORPUS, SCI-DOCS, HotpotQA, and TriviaQA demonstrate that for long-document retrieval tasks, our framework achieves higher precision while maintaining competitive recall compared to other RAG frameworks.

---

## 论文详细总结（自动生成）

# Momoka-RAG 论文总结

## 1. 核心问题与整体含义

- **研究动机**：现有 RAG 框架在构建知识结构时偏“被动”和“机械化”，主要依赖固定规则或统计特征，如 RAPTOR 的向量聚类、GraphRAG 的实体关系抽取，只能发现 chunk 之间的浅层关联，难以主动挖掘跨段落、深层语义或因果推理链。
- **核心问题**：长文档场景下，单纯改进分块方法无法兼顾“局部语义连贯”与“跨段落语义连接”；主流知识结构重组方法又缺乏以“语义补全”为目标的主动探索。
- **整体含义**：论文提出 **Momoka-RAG**，将蒙特卡洛树搜索（MCTS）从传统检索阶段前移到索引阶段，把每个 chunk 视为节点，主动构建语义信息路径，再用该路径增强检索。核心目标是在长文档 RAG 中同时提升检索精度与语义组织能力。

## 2. 方法论

### 2.1 核心思想

- 不再只问“哪些 chunk 在向量空间更接近”，而是问“为了完整理解当前 chunk，下一步应检索哪些 chunk”。
- 用 MCTS 在 chunk 图上主动探索语义补全路径，形成 **Momoka-Map**；再用 **Momoka-Trail Retriever** 基于预计算路径扩展候选池并重排序。

### 2.2 Momoka-Map：基于 MCTS 的语义路径构建

- **文档解析与分块**：先用 LLM 生成全局标题 \(T_D\)，再动态切分为语义连贯的 chunk 序列。每个 chunk 表示为：
  - 文本：\(T_D \oplus text_i\)
  - 段落号 \(p_i\)
  - 句子号 \(s_i\)
- **MCTS 四阶段**：
  - **Selection**：用 UCT 公式平衡探索与利用，从根节点递归选择子节点。
  - **Expansion**：随机选择一个未探索节点加入路径，避免形成循环路径。
  - **Simulation**：每一步 rollout 都计算奖励，而非只看最终节点。奖励由 LLM 语义裁判与结构先验组成：
    - LLM 判断新 chunk 是否对根 chunk 有语义补全关系；
    - 加入段落距离、句子距离的平滑奖励项；
    - 论文设置 \(\alpha=3,\ \beta=2,\ \gamma=\delta=1\)。
  - **Backpropagation**：将 rollout 平均奖励回传，更新路径上节点的累计奖励与访问次数。
- **路径输出**：从根 chunk 出发，每层选择访问次数最高的子节点，形成最优信息路径 \(P_i\)。所有路径集合 \(G\) 与 chunk 序列一起存入向量数据库。

### 2.3 Momoka-Trail Retriever：路径增强检索

- **流程**：Retrieval → Expansion → Reranking。
- 先通过向量检索取得初始 \(2K\) 个 chunk。
- 对每个初始 chunk 取其关联路径，执行 **Mixed-Granularity Expansion Strategy**，候选包括：
  - 原始 chunk；
  - 完整路径上下文；
  - 路径中的单个节点；
  - 原始 chunk 与路径节点的两两组合。
- 最后用 Cross-Encoder Reranker 对扩展候选池做细粒度打分，选出 Top-K，以平衡语义匹配精度与大候选池效率。

## 3. 实验设计

- **数据集**：Dragonball（仅 Finance 子集）、SQuAD、NFCORPUS、SCI-DOCS、HotpotQA、TriviaQA，均按文档长度筛选。
- **任务场景**：长文档检索与生成质量评估。
- **对比方法**：
  - Late-Chunking；
  - RAPTOR；
  - Meta-Chunking-PPL / Meta-Chunking-MSP；
  - Dense X Retrieval；
  - LightRAG；
  - 以及 Fixed-Length、LLM-Chunk 等分块输入方式。
- **Momoka-RAG 作为 plug-and-play 框架**：可接在 Fixed-Length、LLM-Chunk、Meta-Chunking-MSP/PPL 等分块序列之后。
- **指标**：
  - 检索：Recall、MRR、Precision、F1，主文汇总为 Metric@1 + Metric@3 + Metric@5；
  - 生成：ROUGE-L、BLEU、METEOR、Relevant、Irrelevant、Wrong；
  - 其他：时间延迟、Dragonball 人工评估。
- **模型配置**：
  - Embedding：BGE-M3；
  - Reranker：bge-reranker-large；
  - LLM：OpenAI API 调用 Qwen-max；
  - 生成评估：DeepSeek-R1；
  - Meta-Chunking：Qwen2.5-1.5B-Instruct；
  - Dense X Retrieval：propositionizer-wiki-flan-t5-large。
- **超参数**：MCTS 迭代次数 100，最大 rollout 长度 5，\(\alpha=3,\ \beta=2,\ \gamma=\delta=1\)。

## 4. 资源与算力

- 论文**未明确报告 GPU 型号、数量、训练时长或总计算资源**。
- 方法本身**不涉及额外训练**，主要依赖预训练 LLM、Embedding 模型和 Reranker，通过 OpenAI API 调用 Qwen-max、DeepSeek-R1 等。
- 文中报告了索引与检索延迟：
  - 平均每 chunk 索引构建时间：Dragonball 约 116.23 秒，NFCORPUS 约 93.55 秒，HotpotQA 约 95.74 秒，SCI-DOCS 约 97.11 秒，SQuAD 约 28.84 秒，TriviaQA 约 25.49 秒。
  - 使用 Momoka-RAG 后，每问题检索延迟约为 1–4 秒；部分 baseline 约为 0.07–0.8 秒。
- 因此，该方法的主要代价在**离线索引阶段**，而非在线检索阶段。

## 5. 实验数量与充分性

- **实验组数较多**：
  - 6 个数据集上的检索对比；
  - 生成质量对比；
  - Base / MM / Momoka 三阶段消融；
  - MCTS 超参数敏感性分析，7 种迭代与 rollout 组合；
  - MCTS 奖励机制对比；
  - MCTS 扩展机制对比，随机扩展 vs. 相似度启发扩展；
  - 索引与检索延迟分析；
  - Dragonball 人工评估。
- **充分性**：整体覆盖较广

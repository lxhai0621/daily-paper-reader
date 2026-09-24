---
title: "Beyond Chunking: Discourse-Aware Hierarchical Retrieval for Long Document Question Answering"
title_zh: 超越分块：面向长文档问答的篇章感知层次化检索
authors: "Huiyao Chen, Yi Yang, Yinghui Li, Meishan Zhang, Baotian Hu, Min Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.829.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向长文档问答的篇章感知层次化检索
tldr: 长文档问答系统通常把文本当作扁平序列或采用启发式切分，忽视了引导人类理解的篇章结构。为此提出篇章感知的层次化框架，基于修辞结构理论，将篇章树转换为句子级表示，并用大模型增强节点表示以桥接结构与语义。框架包含通用篇章解析、节点语义增强与结构引导的层次化检索三项创新，在多个长文档数据集上验证了效果，为长上下文检索与分块策略提供了新思路。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long829/fig-002.webp\", \"caption\": \"\", \"page\": 15, \"index\": 2, \"width\": 512, \"height\": 512}]"
motivation: 长文档问答多将文本视为扁平序列或启发式切分，忽视篇章结构信息。
method: 提出篇章感知层次化框架，基于修辞结构理论构建篇章树，并用大模型增强节点表示。
result: 通过结构引导的层次化检索，在多个长文档问答数据集上取得提升。
conclusion: 为长上下文检索与分块策略提供了结合篇章结构的新方法。
---

## Abstract
Existing long-document question answering systems typically process texts as flat sequences or use heuristic chunking, which overlook the discourse structures that naturally guide human comprehension. We present a discourse-aware hierarchical framework that leverages rhetorical structure theory (RST) for long document question answering. Our approach converts discourse trees into sentence-level representations and employs LLM-enhanced node representations to bridge structural and semantic information. The framework involves three key innovations: language-universal discourse parsing for lengthy documents, LLM-based enhancement of discourse relation nodes, and structure-guided hierarchical retrieval. Extensive experiments on four datasets demonstrate consistent improvements over existing approaches through the incorporation of discourse structure, across multiple genres and languages. Moreover, the proposed framework exhibits strong robustness across diverse document types and linguistic settings.

---

## 论文详细总结（自动生成）

# 论文总结：Beyond Chunking: Discourse-Aware Hierarchical Retrieval for Long Document Question Answering

## 1. 核心问题与整体含义
- **研究背景**：长文档问答（Long Document QA）是 NLP 中的重要挑战。LLM 在短文档如 SQuAD 上已接近人类水平，但在 QASPER 等长文档数据集上，SOTA 模型 F1 仍常低于 50%。
- **核心问题**：现有长文档 QA 多把文档当作扁平序列，或采用固定长度分块、语义聚类、二分切分等启发式方法。这些方法忽视了人类理解长文档时依赖的**篇章结构**，例如主题、对比、列举、总结、详述等修辞关系。
- **整体含义**：论文提出 **DISRetrieval**，首次系统性地将修辞结构理论（RST）引入长文档问答检索，用篇章树组织文档，并通过 LLM 增强节点语义，实现结构引导的层次化证据检索。目标是在多种体裁、语言、上下文长度和生成模型下，提升长文档 QA 的检索与回答效果。

## 2. 方法论
### 2.1 核心思想
- 将长文档建模为 **RST 篇章树**：叶节点对应句子级基本单元，内部节点表示对比、详述、列举、总结等修辞关系。
- 不只做“语义相似度分块”，而是利用篇章结构识别自然连贯的语义单元，再在多个粒度上检索证据。
- 通过 LLM 为内部节点生成文本表示，桥接“抽象修辞关系”和“可检索语义内容”之间的鸿沟。

### 2.2 关键技术细节
- **句子级 RST 适配**：
  - 粒度适配：将传统 EDU 级解析转为句子级，合并句内 EDU，并用最低公共祖先分析确定句间关系，提升长文档处理效率。
  - 语言适配：用 GPT-4o 将 RST-DT 语料翻译为中文，训练语言通用篇章解析器，支持跨语言。
- **两阶段篇章树构建**：
  - 段落级：对每个段落构造局部篇章树。
  - 文档级：将段落树根节点表示作为输入，再构造全局篇章树。
  - 内部节点增强：若子节点合并长度超过阈值 τ，则用 LLM 生成摘要；否则直接拼接。公式可概括为：  
    `v* = LLM(v_l, v_r) if |v_l|+|v_r| >= τ else merge(v)`。
  - 树集成：用段落级树替换文档级树中对应叶节点，得到统一多粒度篇章树 `T_D`。
- **节点表示**：
  - 对 `T_D` 中所有节点用预训练编码器生成稠密向量：`e_v = f_enc(v)`。
  - 保留层次结构与语义信息，支持结构感知检索。
- **结构引导证据检索**：
  - 计算查询与所有节点余弦相似度：`score(v)=cos(f_enc(q), e_v)`。
  - 按相似度排序后执行双重选择：
    - 叶节点高相关则直接选；
    - 内部节点则从其子树中选择 top-k 未使用叶节点；
    - 去重，直到达到证据上限 K。
  - 该策略兼顾句子级精确证据与篇章级连贯片段，减少冗余。

## 3. 实验设计
- **数据集 / 场景**：
  - **QASPER**：科研论文问答，平均 4170 词，最大 21,165 词。
  - **QuALITY**：长文阅读理解，平均 5022 词，主要来自小说和杂志文章。
  - **NarrativeQA**：叙事理解，平均 51,372 词，最大 346,902 词，包含书籍和电影剧本。
  - **MultiFieldQA-zh**：中文长

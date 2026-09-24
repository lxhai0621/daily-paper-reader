---
title: Subgraph-Guided Executable Logical Form Generation for Knowledge Base Question Answering
title_zh: 子图引导的可执行逻辑形式生成用于知识库问答
authors: "Yuhang Tian, Dandan Song, Zhijing Wu, Changzhi Zhou, Jun Yang, Huipeng Ma, Chenhao Li, Luan Zhang, Yading Li, Xudong Li, Shenxi Liu, Jing Jiang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.177.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 面向知识库问答的子图引导逻辑形式生成
tldr: 现有检索增强的KBQA方法仅按语义相似度孤立检索实体与关系，忽略知识库与问题的结构信息，导致逻辑形式生成质量受限。本文提出SELF-KBQA框架，引入结构感知子图检索阶段，将候选子图与问题结构对齐，使大模型在结构对齐且语义相关的子图上生成可执行逻辑形式。该方法提升了知识库问答的准确性与结构一致性，为语义解析与检索融合提供了新路径。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl177/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 870, \"height\": 522}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl177/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 561, \"height\": 352}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl177/fig-003.webp\", \"caption\": \"\", \"page\": 1, \"index\": 3, \"width\": 669, \"height\": 310}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl177/fig-004.webp\", \"caption\": \"\", \"page\": 1, \"index\": 4, \"width\": 860, \"height\": 493}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl177/fig-005.webp\", \"caption\": \"\", \"page\": 16, \"index\": 5, \"width\": 657, \"height\": 403}]"
motivation: 检索增强KBQA仅按语义相似度孤立检索实体与关系，忽略知识库与问题的结构信息。
method: 提出SELF-KBQA框架，引入结构感知子图检索，使大模型在结构对齐子图上生成可执行逻辑形式。
result: 方法提升知识库问答的准确性与结构一致性。
conclusion: 为语义解析与结构化检索融合提供新路径。
---

## Abstract
Large Language Models (LLMs) have shown great potential in Knowledge Base Question Answering (KBQA) via semantic parsing. However, existing retrieval-augmented approaches typically retrieve entities and relations in isolation based solely on semantic similarity, ignoring the structural information of the Knowledge Base (KB) and the question. To address this limitation, we propose SELF-KBQA ( S ubgraph-Guided E xecutable L ogical F orm Generation), a novel framework that empowers LLMs to generate logical forms conditioned on structurally aligned and semantically relevant subgraphs. Specifically, we introduce a structure-aware subgraph retrieval stage that ranks candidate subgraphs by aligning them with the question’s structure, along with semantic relevance. Subsequently, we employ a token-budgeted evidence condensation strategy to distill the top-ranked subgraphs into compact contexts for the generation stage. Extensive experiments on GrailQA, WebQSP, and GraphQuestions demonstrate that SELF-KBQA achieves state-of-the-art performance.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：知识库问答（KBQA）中，基于语义解析的方法让 LLM 生成可执行逻辑形式（如 SPARQL、S-Expression），再在 KB 上执行以获得答案。该路线精度高、可解释、便于定位错误。
- **核心问题**：现有检索增强方法通常按语义相似度**孤立检索实体和关系**，把 KB 当作“词袋”，忽略 KB 结构以及问题隐含的逻辑结构，导致检索到的证据无法支撑正确逻辑形式生成。
- **典型例子**：问题 “What character did Natalie Portman play in Star Wars?” 需要 `film.performance.film` 等关键关系，但孤立语义检索容易遗漏，最终生成错误逻辑形式。
- **整体含义**：论文提出 **SELF-KBQA**（Subgraph-Guided Executable Logical Form Generation），将 KBQA 形式化为“子图引导的可执行逻辑形式生成”，强调检索证据应同时满足**结构对齐**与**语义相关**，从而提升逻辑形式的可执行性与答案准确率。

## 2. 方法论

- **核心思想**：两阶段框架。
  - 第一阶段：**结构感知子图检索**，预测问题核心推理模式，枚举并排序候选子图。
  - 第二阶段：**子图条件逻辑形式生成**，压缩 top 子图为紧凑证据，指导 LLM 生成可执行逻辑形式。

- **核心推理模式 CRP 预测**：
  - CRP 表示连接主题实体与答案实体的关系结构，限定为最多两跳。
  - 包括单跳、两跳四种方向、答案中心三类，共九种预定义模式。
  - 用 **Flan-T5-base** 微调，输入问题，输出 CRP 模式。
  - 论文强调 CRP 是声明式、模块化、拓扑级定义，可扩展到更长跳数，并可跨 KB 迁移。

- **子图枚举**：
  - 从问题中的实体提及得到候选实体集合。
  - 按 CRP 模板在 KB 中扩展，枚举单跳、两跳子图。
  - 若问题含两个实体提及，还枚举同时包含两个实体的子图。
  - 相邻实体可用抽象占位节点表示类型，提高信息密度。

- **子图排序**：
  - 联合考虑**结构兼容性**与**语义相关性**。
  - 结构兼容性：
    - 跳数一致性：`1 / (1 + |Hg - H|)`。
    - 方向一致性：比较候选子图方向序列与 CRP 方向序列，按匹配比例计算。
    - 二者加权得到结构分。
  - 语义相关性：在节点级、关系文本级、子图级三个粒度计算余弦相似度，使用 `BAAI/bge-m3` 编码，再加权求和。
  - 总评分：`S(g|q) = λ * Sstruct + (1 - λ) * Ssem`，按总分排序选 top-k 子图。

- **Token 预算证据压缩与生成**：
  - top-k 子图存在重叠冗余，需在 token 预算 `B` 内选择子集 `H`。
  - 目标函数：最大化 `Σ s(g) + |U(H)|`，其中 `U(H)` 是唯一实体和关系类型集合，重复单元只计一次。
  - 用贪心策略按“每 token 边际收益”近似选择。
  - 将压缩后的证据序列化，与问题一起输入 LLM。
  - 用 **LoRA** 微调开源

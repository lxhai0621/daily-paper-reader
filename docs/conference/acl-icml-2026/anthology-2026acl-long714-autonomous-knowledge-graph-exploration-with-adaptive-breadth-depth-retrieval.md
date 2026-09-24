---
title: Autonomous Knowledge Graph Exploration with Adaptive Breadth-Depth Retrieval
title_zh: 基于自适应广度深度检索的自主知识图谱探索
authors: "Joaquin Polonuer, Lucas Vittor, Iñaki Arango, Ayush Noori, David A. Clifton, Luciano Del Corro, Marinka Žitnik"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.714.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 工具化知识图谱检索平衡广度与深度
tldr: 从知识图谱中为语言模型查询检索证据，需要在全图广泛搜索与沿关系链多跳遍历之间取得平衡；相似度检索覆盖广但浅，遍历法又依赖种子节点选择，面对多实体多关系查询易失效。作者提出 ARK，一种工具化知识图谱检索器，通过全局词法搜索与一跳邻域探索两个操作，让语言模型自主控制广度与深度的权衡。ARK 交替进行广度发现与深度扩展，实现面向结构化知识的自适应检索与自动证据发现。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-001.webp\", \"caption\": \"\", \"page\": 7, \"index\": 1, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-002.webp\", \"caption\": \"\", \"page\": 7, \"index\": 2, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-004.webp\", \"caption\": \"\", \"page\": 7, \"index\": 4, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-005.webp\", \"caption\": \"\", \"page\": 7, \"index\": 5, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-006.webp\", \"caption\": \"\", \"page\": 7, \"index\": 6, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-007.webp\", \"caption\": \"\", \"page\": 7, \"index\": 7, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-008.webp\", \"caption\": \"\", \"page\": 7, \"index\": 8, \"width\": 3249, \"height\": 1033}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long714/fig-009.webp\", \"caption\": \"\", \"page\": 7, \"index\": 9, \"width\": 3249, \"height\": 1033}]"
motivation: 知识图谱检索需平衡全图广度搜索与多跳深度遍历，但相似度检索过浅、遍历法依赖种子节点易失效。
method: 提出 ARK 工具化检索器，通过全局词法搜索与一跳邻域探索两个操作让语言模型控制广度深度权衡。
result: ARK 交替进行广度发现与深度扩展，在跨多实体多关系查询上实现更有效的证据检索。
conclusion: 该工作为结构化知识库上的自主检索与知识发现提供了自适应、可组合的工具化方案。
---

## Abstract
Retrieving evidence for language model queries from knowledge graphs requires balancing broad search across the graph with multi-hop traversal to follow relational links. Similarity-based retrievers provide coverage but remain shallow, whereas traversal-based methods rely on selecting seed nodes to start exploration, which can fail when queries span multiple entities and relations. We introduce ARK: Adaptive Retriever of Knowledge, a tool-using KG retriever that gives a language model control over this breadth-depth tradeoff using a two-operation toolset: global lexical search over node descriptors and one-hop neighborhood exploration that composes into multi-hop traversal. ARK alternates between breadth-oriented discovery and depth-oriented expansion without depending on a fragile seed selection, a pre-set hop depth, or requiring retrieval training. ARK adapts tool use to queries, using global search for language-heavy queries and neighborhood exploration for relation-heavy queries.On STaRK, ARK reaches 59.1% average Hit@1 and 67.4 average MRR, improving average Hit@1 by up to 31.4% and average MRR by up to 28.0% over retrieval-based and agent-based training-free methods.Finally, we distill ARK’s tool-use trajectories from a large teacher into an 8B model via label-free imitation, improving Hit@1 by +7.0, +26.6, and +13.5 absolute points over the base 8B model on AMAZON, MAG, and PRIME datasets, respectively, while retaining up to 98.5% of the teacher’s Hit@1 rate.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：大语言模型需要从外部知识中检索证据来支撑生成与推理。知识图谱以实体和类型化关系组织证据，支持跨查询复用与关系约束，是结构化知识检索的重要载体。
- **核心矛盾**：从知识图谱中检索证据需要在两种搜索模式之间平衡：
  - **广度搜索**：查询涉及多个实体或松散概念时，需要覆盖全图，找到正确区域。
  - **深度搜索**：证据只出现在特定多跳关系路径之后，需要沿关系链遍历。
- **现有方法不足**：
  - 相似度检索器覆盖广，但通常较浅，未充分利用关系结构。
  - 遍历式方法依赖种子实体选择；种子不完整或模糊时，探索会局限在局部，错过图中其他相关证据。
  - 已有工作多将广度与深度需求分开处理，且部分方法依赖任务或图特定训练，迁移性受限。
- **论文目标**：提出 **ARK（Adaptive Retriever of Knowledge）**，一种训练-free、工具使用的知识图谱检索器，让语言模型通过最小工具集自主控制广度—深度权衡，无需脆弱种子选择、预设跳数或检索训练。

## 2. 方法论

- **核心思想**：
  - 将知识图谱检索建模为交互过程：智能体 `A = <LLM, T>` 通过工具接口 `T` 查询图，产生轨迹 `τ = ((s1, A1, o1), ..., (sT, AT, oT))`。
  - 智能体维护有序检索列表 `R`，每步可选择工具返回节点加入 `R`，或调用 `FINISH` 终止。
  - 最终输出为按选择顺序排序的节点列表。
- **相关性函数**：
  - 使用 `rel(q, dV(v))` 对节点 `v` 按文本子查询 `q` 打分。
  - 实现为基于节点文本属性倒排索引的 **BM25**，适合探索过程中大量短小、动态变化的子查询。
- **两个核心工具**：
  - **Global Search（全局搜索）**：
    - 对全图节点按 `rel(q, dV(v))` 取 Top-k。
    - 用于定位与用户查询相关的实体，或处理纯文本匹配即可解决的查询。
  - **Neighborhood

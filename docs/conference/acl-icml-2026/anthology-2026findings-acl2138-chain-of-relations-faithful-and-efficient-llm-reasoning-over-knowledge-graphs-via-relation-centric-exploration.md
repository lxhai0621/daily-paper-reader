---
title: "Chain-of-Relations: Faithful and Efficient LLM Reasoning over Knowledge Graphs via Relation-Centric Exploration"
title_zh: 关系链：通过关系中心探索实现知识图谱上的忠实高效大模型推理
authors: "Chenhui Liu, Jianpeng Zhou, Jiahai Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.2138.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 基于智能体的知识图谱推理
tldr: 知识图谱问答是基于知识图谱增强大模型的重要基准，其中基于智能体的方法多采用实体中心探索，逐步选择并连接中间实体。但该范式存在两大局限：中间实体缺乏语义信息时难以评估相关性，导致有效路径被误弃；束搜索只保留高分实体，又会过早剪枝候选。本文提出关系中心的探索方法Chain-of-Relations，以关系为单位构建推理路径。实验表明其在KGQA上更忠实且高效，提升推理准确率与可解释性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2138/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2138/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2138/fig-003.webp\", \"caption\": \"\", \"page\": 8, \"index\": 3, \"width\": 2616, \"height\": 2614}]"
motivation: 基于智能体的KGQA多采用实体中心探索，易因实体语义缺失与过早剪枝丢失有效推理路径。
method: 提出关系中心的探索方法Chain-of-Relations，以关系为单位增量构建推理路径。
result: 该方法在知识图谱问答上实现更忠实且高效的推理，减少路径误弃。
conclusion: 以关系为中心替代实体中心探索，为知识图谱增强的大模型推理提供了改进范式。
---

## Abstract
Knowledge graph question answering (KGQA) serves as an essential benchmark for KG-enhanced large language models. Among various approaches, agent-based methods have emerged as an effective solution.Existing methods adopt entity-centric exploration that incrementally constructs reasoning paths by selecting and connecting intermediate entities. However, they face two critical limitations. (1) Entity incompleteness vulnerability arises when some intermediate entities lack semantic information beyond opaque IDs, preventing relevance evaluation and leading to discarding valid reasoning paths.(2) Premature entity pruning occurs because beam search retains only top-ranked entities at each step, eliminating candidates before their relevance can be verified.To address these challenges, this paper proposes Chain-of-Relations (CoR) with relation-centric exploration and global entity filtering, reducing dependence on entity completeness and ensuring complete candidate retrieval before constraint validation.Experiments on three benchmark datasets show that CoR consistently outperforms strong baselines in both F1 score and KG-grounded Rate.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：知识图谱问答（KGQA）是评估“知识图谱增强大语言模型”的关键基准。已有方法包括预训练注入、微调、子图检索和基于智能体的探索；其中基于智能体的方法允许 LLM 主动在 KG 上构建推理路径，较灵活。
- **核心问题**：现有基于智能体的方法普遍采用**

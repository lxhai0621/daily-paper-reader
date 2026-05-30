---
title: Interpreting Omics Data Analysis with Large Language Models for Disease Target and Drug Discovery
title_zh: 利用大语言模型解读组学数据分析以发现疾病靶点和药物
authors: "XU, Z., Chen, W., Ren, W., Xu, T., Amaechin, S., Khan, R., Chen, Y., Province, M., Payne, P., Li, F."
date: 2026-05-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.30.721768v2.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 基于LLM的框架整合结构化与非结构化知识用于靶点发现
tldr: 整合文献知识是解读组学数据的关键，但现有LLM输出缺乏定量证据。本文提出provenance-aware Text-to-Target框架，结合模式约束的LLM检索与数值组学分析，通过模态感知融合将候选分为锚点、隐藏节点和新颖节点，并基于拓扑生成分期假设。在胰腺癌和阿尔茨海默病中，分别生成75/34基因集和23/14策略组合，DepMap与CRISPRbrain支持显著，且保留完整可审计性。该框架为跨疾病靶点优先化提供可复现方法，支持持续文献机制一致性验证。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有LLM检索缺乏定量证据，需将组学数据与文献知识融合，以可靠优先化疾病靶点和药物。
method: 提出Text-to-Target框架，耦合模式约束的多模型LLM检索与组学分析，通过模态感知融合和拓扑传播生成分期假设。
result: 在PDAC和AD中，生成75/34基因集和23/14策略，DepMap及CRISPRbrain富集显著，且全程可审计。
conclusion: 框架构建了可转移的发现架构，组学证据约束生物学，LLM扩展搜索空间，网络融合保持可解释性。
---

## 摘要
在生物医学科学发现中，综合文献中的先验知识是解读数值组学数据分析以识别疾病靶点和发现药物的关键环节。大语言模型（LLMs）可快速从生物医学文本中检索疾病机制，但仅依靠文本输出缺乏针对特定队列的定量证据，对于靶点和药物优先排序而言过于笼统且不可靠。为此，我们提出了一种基于溯源感知的“文本到靶点”框架，该框架将模式约束的多模型LLM检索与数值组学数据分析相结合。核心设计是一个模态感知的融合步骤：候选物被划分为重叠支持的锚点、仅检索的隐藏枢纽以及网络涌现的新颖节点，然后在拓扑约束下传播到分阶段假设和策略生成中。我们在阿尔茨海默病（AD）和胰腺导管腺癌（PDAC）中评估了该模型。在PDAC中，该流程生成了一个平衡的75基因候选集和23项策略组合，在靶点和策略层面均获得了显著的DepMap支持。在AD中，更严格的候选物控制产生了紧凑的34基因候选集和14项策略；在扩展的CRISPRbrain注册库下，两个靶点层面的轴线均显著，且策略层面富集强烈。在两种疾病中，最终策略均保持了与候选池的完整溯源闭合性，实现了从检索伪影到验证输出的端到端可审计性。这些结果支持一种可迁移的发现架构，其中组学证据约束生物活性，LLM检索扩展机制搜索空间，而网络感知融合保持了可解释性。该框架为双疾病靶点优先排序提供了可重复的基础，并通过代理性证据更新循环激励持续的文献-机制一致性。

## Abstract
In biomedical scientific discovery, synthesizing prior knowledge from the literature is an essential component of interpreting numerical omics data analyses for disease target identification and drug discovery. Large language models (LLMs) alone can rapidly retrieve disease mechanisms from biomedical text, but text-only outputs are general and unreliable for target and drug prioritization without cohort-specific quantitative evidence. Herein, we propose a provenance-aware Text-to-Target framework that couples schema-constrained multi-model LLM retrieval with numeric omics data analysis. The key design is a modality-aware fusion step: candidates are partitioned into overlap-supported anchors, retrieval-only hidden hubs, and network-emergent novelty nodes, then propagated into staged hypothesis and strategy generation under topology constraints. We evaluate the model in Alzheimers disease (AD) and pancreatic ductal adenocarcinoma (PDAC). In PDAC, the workflow produced a balanced 75-gene candidate universe and a 23-strategy portfolio, with significant DepMap support at both target level and strategy level. In AD, stricter candidate controls yielded a compact 34-gene universe and 14 strategies; under an expanded CRISPRbrain registry, both target-level axes were significant, with strong strategy-level enrichment. Across both diseases, final strategies preserved full provenance closure to the candidate pool, enabling end-to-end auditability from retrieval artifacts to validation outputs. These results support a transferable discovery architecture in which omics evidence constrains biological activity, LLM retrieval expands mechanistic search space, and network-aware fusion preserves interpretability. The framework provides a reproducible basis for dual-disease target prioritization and motivates continuous literature-mechanism concordance with agentic evidence-refresh loops.
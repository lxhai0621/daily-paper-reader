---
title: "ChatSpatial: Schema-Enforced Agentic Orchestration for Reproducible and Cross-Platform Spatial Transcriptomics"
title_zh: ChatSpatial：基于模式强制代理编排的可重复与跨平台空间转录组学
authors: "Yang, C., Zhang, X., Chen, J."
date: 2026-06-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.02.26.708361v3.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 通过MCP协调生物信息学工具的LLM智能体
tldr: 空间转录组学分析需要跨Python/R生态的数十种方法，研究者常陷于工具兼容而非生物学探索。ChatSpatial平台让LLM从预验证的工具schema中选择，嵌入领域知识实现上下文感知参数推断，基于MCP协议统一60余种方法。复现卵巢癌和口腔癌两项已发表研究，并在7个LLM平台上验证，表明schema强制编排为多步空间分析带来工作流级的近确定性可重复性。该平台还支持跨独立分析框架的实践三角验证，提升了分析可靠性。
source: biorxiv
selection_source: fresh_fetch
motivation: 空间转录组学分析因工具生态碎片化，导致可重复性差且研究效率低下，研究者需耗费大量精力协调工具而非探索生物学问题。
method: ChatSpatial利用LLM结合MCP协议，通过预验证工具schema的上下文感知选择与编排，统一了15类60多种跨Python/R生态的分析方法。
result: 复现两项已发表研究的分析结果，在7种LLM平台上验证，实现了接近确定性的工作流级可重复性。
conclusion: schema强制编排显著提升了空间转录组学分析的可重复性和可迁移性，并促进了跨平台分析框架的三角验证。
---

## 摘要
空间转录组学彻底改变了我们以分子分辨率研究组织结构的能力，然而分析这些数据需要在不相容的Python和R生态系统中穿梭使用数十种计算方法——迫使研究人员将更多精力花在让工具运行上，而不是追求生物学问题。我们提出了ChatSpatial，这是一个平台，其中大语言模型（LLM）从预验证的工具模式中进行选择，而不是生成自由形式的代码，同时将领域专业知识嵌入到模式描述中，用于上下文感知的参数推断。基于模型上下文协议（MCP），ChatSpatial将跨越15个分析类别的60多种方法统一到一个涵盖Python和R生态系统的单一对话式工作流程中。两项已发表研究的复现——恢复卵巢癌中的亚克隆异质性和口腔鳞状细胞癌中的肿瘤微环境组织——以及在七个LLM平台上的验证表明，基于模式强制的工作流程编排在多步空间分析的工作流程层面产生了近乎确定性的可重复性。除了复现之外，探索性的交叉方法分析展示了跨独立分析框架的实用三角验证。

## Abstract
Spatial transcriptomics has transformed our ability to study tissue architecture at molecular resolution, yet analyzing these data demands navigating dozens of computational methods across incompatible Python and R ecosystems---forcing researchers to devote more effort to making tools function than to pursuing biological questions. We present ChatSpatial, a platform in which the LLM selects from pre-validated tool schemas rather than generating free-form code, with domain expertise embedded in schema descriptions for context-aware parameter inference. Built on the Model Context Protocol (MCP), ChatSpatial unifies 60+ methods across 15 analytical categories into a single conversational workflow spanning Python and R ecosystems. Replication of two published studies---recovering subclonal heterogeneity in ovarian cancer and tumor microenvironment organization in oral squamous cell carcinoma---and validation across seven LLM platforms demonstrate that schema-enforced orchestration yields near-deterministic reproducibility at the workflow level for multi-step spatial analyses. Beyond replication, exploratory cross-method analyses illustrate practical triangulation across independent analytical frameworks.
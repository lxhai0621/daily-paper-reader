---
title: "OmniCellAgent: An AI Scientist for Omic-Driven Scientific Discovery"
title_zh: "OmniCellAgent: 用于组学驱动科学发现的AI科学家"
authors: "Huang, D., Li, H., Li, W., Zhang, H., Xu, T., Lu, Y., Fang, K., Xu, Z., Chen, J., Dickson, P., Sardiello, M., Buchser, W., Cooper, J. D., Cruchaga, C., Eghtesady, P., Li, G., Goedegebuure, P., DeNardo, D., Ding, L., Fields, R. C., Zhan, M., Miller, J. P., Province, M., Chen, Y., Payne, P., Li, F."
date: 2026-06-02
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.31.667797v3.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 多智能体AI框架用于生物医学领域的自动化知识发现
tldr: 生物医学发现中，识别相关组学数据集并利用先验知识解释结果对生成新假设至关重要。现有AI智能体要求用户预定义疾病数据集，对非计算研究人员困难。OmniCellAgent是一种基于大规模单细胞RNA测序资源的多智能体框架，能自动检索、整合和分析疾病与对照数据集，并通过先验知识代理和领域专家代理进行目标注释与下游解释。在多种疾病评估中，该框架能识别相关数据集、优先排序生物学靶点并生成证据支持的假设，降低了组学驱动发现的门槛，加速了精准医学假设生成。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有AI智能体依赖用户预定义疾病数据集，过程耗时且对非计算研究人员不友好。
method: 构建多智能体框架，自动检索整合scRNA-seq数据，利用先验知识注释靶点，并通过专家代理进行下游解释。
result: 在多种疾病中验证，能自动识别数据集、优先排序有意义靶点并生成结构化分析报告与数据驱动假设。
conclusion: 多智能体AI系统可降低组学发现障碍，加速精准医学假设生成。
---

## 摘要
在生物医学科学发现中，识别相关组学数据集并利用数据库和文献中的先验知识解释分析结果，对于生成新颖假设至关重要。尽管近期的人工智能代理支持自动化组学分析和文献检索，但它们通常要求用户预先定义和整理疾病特定数据集，这一过程仍然具有挑战性且耗时，尤其对于非计算研究人员。本文提出OmniCellAgent，一个基于大规模单细胞RNA测序（scRNA-seq）资源的多智能体AI框架，能够自主检索、整合并分析跨组织和疾病状态中不同细胞类型的疾病与对照相关数据集。此外，OmniCellAgent整合了一个生物医学先验知识智能体，用于利用整理好的数据库和文献进行系统靶点注释，以及领域特定专家智能体用于高优先级靶点的下游解读。通过聚合各智能体的证据，该框架生成结构化的分析报告和数据驱动的假设。我们在多种疾病场景下评估了OmniCellAgent，展示了其识别相关数据集、优先考虑具有生物学意义的靶点以及生成全面、有证据支持的假设的能力。我们的结果表明，多智能体AI系统能够降低组学驱动发现的障碍，并加速精准医学中的假设生成。

## Abstract
In biomedical scientific discovery, identifying relevant omics datasets and interpreting analysis results using prior knowledge from databases and literature are essential for generating novel hypotheses. Although recent AI agents support automated omics analysis and literature retrieval, they typically require users to predefine and curate disease-specific datasets, which is a process that remains challenging and time-consuming, particularly for non-computational researchers. Herein we present OmniCellAgent, a multi-agent AI framework built on large-scale single-cell RNA sequencing (scRNA-seq) resources that autonomously retrieves, integrates and analyzes disease and control-related datasets of diverse cell types across tissues and conditions. Moreover, OmniCellAgent incorporates a biomedical prior knowledge agent for systematic target annotation using curated databases and literature, as well as domain-specific expert agents for downstream interpretation of high-priority targets. By aggregating evidence across agents, the framework generates structured analytical reports and data-driven hypotheses. We evaluate OmniCellAgent across multiple disease settings, demonstrating its ability to identify relevant datasets, prioritize biologically meaningful targets and produce comprehensive, evidence-supported hypotheses. Our results suggest that multi-agent AI systems can reduce barriers to omics-driven discovery and accelerate hypothesis generation in precision medicine.
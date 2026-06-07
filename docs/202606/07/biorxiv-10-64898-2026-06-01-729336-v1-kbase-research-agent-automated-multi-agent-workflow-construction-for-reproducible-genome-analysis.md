---
title: "KBase Research Agent: Automated Multi-Agent Workflow Construction for Reproducible Genome Analysis"
title_zh: KBase研究代理：用于可重复基因组分析的自动化多代理工作流构建
authors: "Gupta, P., Riehl, W. J., Cashman, M., Chivian, D., Neely, C. J., Canon, S. R., Cottingham, R., Henry, C., Arkin, A. P., Dehal, P. S."
date: 2026-06-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.01.729336v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 自动多智能体工作流构建用于基因组分析知识发现
tldr: 基因组分析工作流构建复杂且依赖专业知识，成为可扩展再现分析的瓶颈。KBase Research Agent是一个多智能体系统，通过整合KBase文档和知识图谱自动规划、选择、参数化、验证并执行工作流，生成可再现的Narrative。在参考工作流和100个新细菌基因组上，系统自主完成从质控到功能注释的全流程，输出注释基因组和草稿手稿，验证了生产平台端到端自动化的可行性。
source: biorxiv
selection_source: fresh_fetch
motivation: 构建多步骤基因组分析工作流需要生物与计算工具双重专业知识，限制可扩展性与再现性，亟需自动化方法。
method: 提出多智能体系统，基于KBase文档和知识图谱自动构建分析计划，并选择、参数化、验证和执行KBase应用。
result: 在100个新细菌基因组上自主完成读段质控、基因组组装、分类和功能注释，生成可再现Narrative及草稿手稿。
conclusion: 该方法在生物信息学平台上实现了端到端自动化工作流，显著提升分析可再现性和效率。
---

## 摘要
构建从读段质量控制到基因组组装再到功能注释的多步骤生物信息学工作流，需要生物学和计算工具选择方面的专业知识，这成为可扩展和可重复分析的瓶颈。我们提出了KBase研究代理，一个在DOE系统生物学知识库（KBase）内自动化此类工作流的多代理系统。给定一组测序读段和一个研究目标，该代理基于KBase文档和KBase应用目录的知识图谱构建分析计划，然后选择、参数化、验证并执行适当的KBase应用以完成工作流。生成的分析结果作为可重复的KBase叙事文档保存。我们根据来自同行评审的《微生物资源公告》的参考工作流构建的真实情况，评估了系统的规划和执行质量。此外，我们将该代理应用于JGI IMG/M数据库中100个之前未分析过的细菌分离基因组，它自主执行了读段质量控制、基因组组装、基于GTDB-Tk的分类学分类以及下游分析，生成了注释基因组、可重复叙事文档和草稿手稿，无需人工干预。通过这些实验，KBase研究代理证明了在生产生物信息学平台中实现基于领域知识的端到端科学工作流自动化的可行性。

## Abstract
Constructing multi-step bioinformatics workflows, from read quality control through genome assembly to functional annotation, requires expertise in both biology and computational tool selection, creating a bottleneck for scalable and reproducible analysis. We present the KBase Research Agent, a multi-agent system for automating such workflows within the DOE Systems Biology Knowledgebase (KBase). Given a set of sequencing reads and a research objective, the agent constructs an analysis plan grounded in KBase documentation and a Knowledge Graph (KG) of the KBase application catalog, then selects, parameterizes, validates and executes appropriate KBase applications to carry out the workflow. The resulting analysis is preserved as a reproducible KBase Narrative. We evaluate the system's planning and execution quality against ground truth constructed from reference workflows derived from peer-reviewed Microbiology Resource Announcements. We further apply the agent to 100 previously unanalyzed bacterial isolate genomes from the JGI IMG/M database, where it autonomously performed read quality control, genome assembly, taxonomic classification with GTDB-Tk, and downstream analysis producing annotated genomes, reproducible Narratives, and draft manuscripts without human intervention. Across these experiments, the KBase Research Agent demonstrates the feasibility of domain-grounded, end-to-end scientific workflow automation in a production bioinformatics platform.
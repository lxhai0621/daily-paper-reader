---
title: "CARIBOU: Computational AI Research Interface for Bioinformatics, Omics, and Unifying Agents"
title_zh: CARIBOU：面向生物信息学、组学和统一代理的计算AI研究接口
authors: "Riffle, D., Shirooni, N., Sureshkumar, P., Vijay, V., Rose, M. F."
date: 2026-05-28
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.25.727730v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 用于自主生物信息学分析的多代理框架
tldr: 单细胞与空间组学数据规模激增，专家手动分析能力不足。现有大语言模型生成代码时存在无状态执行、不可重现等局限。CARIBOU是一个多智能体AI框架，通过可编辑蓝图组织专业智能体，在HPC中实现迭代执行-观察-纠正的自主分析。在Allen Brain Atlas等数据集上，迭代执行性能显著优于一次生成，并能从失败中恢复，为安全合规的生物信息学研究提供了高效、可复现的工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 解决专家手工分析大规模单细胞组学数据的瓶颈，并克服现有AI工具无状态执行、不可重现且部署受限的问题。
method: 构建多智能体CARIBOU框架，通过可编辑蓝图指定分析角色与流程，在持久化HPC环境中实现迭代式自主分析。
result: 在单元任务、元数据重建及端到端分析中，迭代执行优于一次生成，且能自适应恢复执行失败，兼容安全约束HPC。
conclusion: CARIBOU为安全HPC环境下的自主生物信息学分析提供有效方案，提升了分析鲁棒性与可重复性。
---

## 摘要
单细胞和空间组学技术正在以前所未有的规模生成生物数据集，这些数据集日益超出专家人工分析的能力。虽然大语言模型（LLM）能够生成生物信息学代码，但现有系统仍受限于无状态执行、可重复性差、部署环境受限以及无法根据中间结果调整分析等问题。在此，我们提出CARIBOU（面向生物信息学、组学和统一代理的计算AI研究接口），这是一个专为机构高性能计算（HPC）环境中的自主生物信息学分析设计的多代理AI框架。CARIBOU通过研究者可编辑的蓝图组织专门的AI代理，这些蓝图编码了分析角色、工作流指导和领域特定推理，同时将所有分析建立在可与基于Singularity/Apptainer的HPC系统兼容的持久可执行计算环境中。与静态代码生成方法不同，CARIBOU在工作流阶段之间维护共享的演化分析状态，从而在质量控制、批次整合、聚类和细胞类型注释过程中实现迭代的执行-观察-纠正行为。我们使用Allen Brain Atlas海马体和Tabula Sapiens数据集，在单元任务基准测试、元数据重建挑战以及端到端单细胞RNA-seq分析中对CARIBOU进行了评估。在这些任务中，迭代执行始终优于一次性代码生成，而该框架展示了从执行失败中自适应恢复的能力以及与安全受限的研究计算基础设施的兼容性。

## Abstract
Single-cell and spatial omics technologies are generating biological datasets at a scale that increasingly exceeds the capacity of expert manual analysis. Although large language models (LLMs) can generate bioinformatics code, most existing systems remain limited by stateless execution, poor reproducibility, restricted deployment environments, and an inability to adapt analyses in response to intermediate results. Here, we present CARIBOU (Computational AI Research Interface for Bioinformatics, Omics, and Unifying Agents), a multi-agent AI framework designed for autonomous bioinformatics analysis within institutional high-performance computing (HPC) environments. CARIBOU organizes specialized AI agents through researcher-editable blueprints that encode analytical roles, workflow guidance, and domain-specific reasoning while grounding all analyses in persistent executable computational environments compatible with Singularity/Apptainer-based HPC systems. Unlike static code-generation approaches, CARIBOU maintains a shared evolving analytical state across workflow stages, enabling iterative execute-observe-correct behavior during quality control, batch integration, clustering, and cell-type annotation. We evaluate CARIBOU across unit-task benchmarks, metadata reconstruction challenges, and end-to-end single-cell RNA-seq analyses using Allen Brain Atlas hippocampus and Tabula Sapiens datasets. Across these tasks, iterative execution consistently outperformed one-shot code generation, while the framework demonstrated adaptive recovery from execution failures and compatibility with security-constrained research computing infrastructure.
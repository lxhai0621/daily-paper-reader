---
title: "OmicOS: A Comprehensive Omics Ecosystem Infrastructure and Agent System for the AI Era"
title_zh: OmicOS：面向AI时代的综合组学生态系统基础设施与智能体系统
authors: "Zeng, Z., Meng, X., Hu, L., Li, C., Liu, P., Shi, Y., Ma, X., Gao, L., Wang, X., Luo, Z., Zheng, Y., Xian, J., Lin, Z., Zhu, H., Jiang, Z., Mao, S., Lu, Y., Tang, W., Peng, Q., Ma, Y., Zhou, L., Xing, C., Zhang, X., Xiong, Y., Du, H."
date: 2026-06-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.11.731775v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 面向组学生态系统的智能体系统
tldr: "当前组学方法分散在Python、R、命令行等不兼容生态中，AI系统难以可靠执行分析。OmicOS将OmicVerse V2社区（含694种方法、R工作流Python重建）注册为状态感知能力合约，使代理可组合、可控地执行分析。在BiomniBench上达到81.2%排名第一，最小代理加入OmicVerse后任务完成度提升34.2个百分点，成功复现R工作流并发现阿尔茨海默病结肠上皮风险轴。该系统将社区方法转化为可靠、可扩展的代理操作平台。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有组学工具分散且不兼容，AI系统无法可靠选择、执行和验证分析流程。
method: OmicVerse V2统一11个组学域的694种方法为高级API，并重建R/Bioconductor工作流；OmicOS注册为状态感知能力合约，代理可组合执行。
result: "在BiomniBench上达81.2%排名第一，最小代理加入OmicVerse后任务完成度提升34.2%，复现R工作流并发现阿尔茨海默病风险轴。"
conclusion: 提供了可依赖、可扩展的组学代理系统，将社区方法转化为可靠的自动化发现工具。
---

## 摘要
生物学已积累了大量组学方法的生态系统，但其中大部分仍是为人类专家而非科学智能体构建的。方法分散于Python包、R/Bioconductor和CRAN工作流、命令行工具、不兼容的数据容器及隐式对象状态中，导致即使是常规分析，AI系统也难以可靠地选择、执行和验证。本文介绍OmicOS——一个综合的组学生态系统基础设施与智能体系统，它将开源组学社区OmicVerse V2转化为可执行的智能体生物学基础。OmicVerse V2提供社区基底：可扩展的AnnDataOOM兼容Rust后端、面向智能体的Python算法（用于单细胞、空间、批量及多组学分析）、单细胞基础模型接口，以及历史上以R为中心的Bioconductor/CRAN风格工作流的Python原生重构。OmicOS通过将分析函数注册为状态感知能力合约，使该基底可操作化，允许智能体检查实时数据对象、选择有效方法、执行受控工作流并记录溯源。结果并非固定流水线，而是一个可编程的组学环境，智能体从中基于经过验证的社区方法组合真实分析，而非发明工具。在外部和专门构建的基准测试中，OmicOS在评估系统中排名第一，在BiomniBench上达到81.2%。将OmicVerse加入最小智能体后，使用qwen-3.6-35b时任务完成度提升高达34.2个百分点，控制消融实验表明，收益来自基于注册的执行，而非更大的模型、文档检索或无限制的工具暴露。同一基础设施可扩展至图集级别的数据，在Python中重现以R为中心的工作流，并将外部病理软件转化为智能体可用技能。在一项从全身空间图谱和术语“阿尔茨海默病”开始的发现任务中，OmicOS组合了一个非规范工作流，整合了空间表达、遗传关联、eQTL和共定位证据，提名了一个以PICALM、CD2AP和CR1为中心的结肠上皮风险轴。总之，OmicVerse和OmicOS为AI时代的组学定义了开放基础，展示了如何将生物学方法社区转化为一个可靠、可扩展且智能体可操作的系统，用于科学发现。

亮点
L_OmicVerse 2.0将涵盖11个组学领域的694种方法整合为智能体可调用的高级API。
L_RebuildR自动将R/Bioconductor方法重构并演化为基于Python的原生实现，并受输出等价门控。
L_OmicOS建立了最先进的组学智能体框架，在通用组学基准测试中跨模型排名第一，并显著提升了本地开源模型的分析能力。
L生态系统模块的组合使用提名了一个与阿尔茨海默病风险相关的结肠上皮轴。
L支持自动迭代演进的外部算法包可集成到OmicOS生态系统中。

## Abstract
Biology has accumulated a vast ecosystem of omics methods, but much of this ecosystem remains built for expert humans rather than scientific agents. Methods are scattered across Python packages, R/Bioconductor and CRAN workflows, command-line tools, incompatible data containers and implicit object states, making even routine analyses difficult for an AI system to choose, execute and verify reliably. Here we introduce OmicOS, a comprehensive omics ecosystem infrastructure and agent system that turns OmicVerse V2, an open-source omics community, into an executable foundation for agentic biology. OmicVerse V2 provides the community substrate: scalable AnnDataOOM-compatible rust backends, agent-friendly Python algorithms for single-cell, spatial, bulk and multi-omics analysis, interfaces to single-cell foundation models, and Python-native reconstructions of historically R-centred Bioconductor/CRAN-style workflows. OmicOS makes this substrate actionable by registering analytical functions as state-aware capability contracts, allowing agents to inspect live data objects, select valid methods, execute controlled workflows and record provenance. The result is not a fixed pipeline, but a programmable omics environment in which agents compose real analyses from verified community methods rather than inventing tools. Across external and purpose-built benchmarks, OmicOS ranked first among the evaluated systems, reaching 81.2% on BiomniBench. Adding OmicVerse to a minimal agent improved task completion by up to 34.2 percentage points with qwen-3.6-35b, and controlled ablations showed that the gains came from registry-grounded execution rather than from larger models, documentation retrieval or unrestricted tool exposure. The same infrastructure scaled to atlas-sized data, reproduced R-centred workflows in Python and converted external pathology software into agent-usable skills. In a discovery task starting from a whole-body spatial map and the term "Alzheimers disease", OmicOS composed a non-canonical workflow that integrated spatial expression, genetic association, eQTL and colocalization evidence to nominate a colon epithelial risk axis centred on PICALM, CD2AP and CR1. Together, OmicVerse and OmicOS define an open foundation for AI-era omics, showing how a community of biological methods can be transformed into a reliable, extensible and agent-operable system for discovery.

HighlightO_LIOmicVerse 2.0 consolidates 694 methods spanning 11 omics domains into agent-callable high-level APIs.
C_LIO_LIRebuildR automatically reconstructs and evolves R/Bioconductor methods as Python-native implementations under output-equivalence gates.
C_LIO_LIOmicOS establishes a state-of-the-art omics agent harness, ranking first on general omics benchmarks across models and substantially improving the analytical capability of local open-source models.
C_LIO_LICompositional use of ecosystem modules nominates a colon epithelial axis associated with Alzheimers disease risk.
C_LIO_LIExternal algorithm packages supporting automatic iterative evolution can be integrated into the OmicOS ecosystem.
C_LI
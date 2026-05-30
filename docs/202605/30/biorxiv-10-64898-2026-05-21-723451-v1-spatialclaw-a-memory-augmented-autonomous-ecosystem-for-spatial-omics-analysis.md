---
title: "SpatialClaw: A Memory-Augmented Autonomous Ecosystem for Spatial Omics Analysis"
title_zh: SpatialClaw：一种用于空间组学分析的记忆增强自主生态系统
authors: "Du, G., Lan, O., Wei, X., Wu, Y., Meng, G., Wu, J., Li, Z., Li, X., Shang, X."
date: 2026-05-25
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.21.723451v1.full.pdf"
tags: ["query:agent"]
score: 7.0
evidence: 记忆增强的自主智能体用于科学分析
tldr: 空间组学分析因方法碎片化而难以复现。SpatialClaw集成30项专业技能，引入基于图的三层持久内存架构（Session、Episodic、Semantic）及Memory-Augmented Reasoning (MAR) Operator，实现自然语言驱动的统一分析。在记忆敏感场景中优于标准大语言模型和纯内存配置，在三阴性乳腺癌数据集中通过三轮对话完成端到端分析。最终将空间组学从碎片化计算转变为可追溯、可复现、自我改进的生态系统。
source: biorxiv
selection_source: fresh_fetch
motivation: 克服空间组学分析方法碎片化、工作流不可复现的问题，且通用对话代理缺乏领域精度。
method: 提出SpatialClaw，集成30个专业技能，采用三层图持久内存架构和Memory-Augmented Reasoning (MAR) Operator。
result: 在三个记忆敏感场景中性能优于标准LLM和纯内存配置；在三阴性乳腺癌数据集上通过三轮对话完成端到端分析。
conclusion: SpatialClaw将空间组学从碎片化计算转变为完全可追溯、可复现、自我改进的发现生态系统。
---

## 摘要
尽管空间组学的扩展彻底改变了我们剖析组织结构的能力，但不相容的计算方法的积累使端到端分析严重碎片化，导致复杂工作流不可重现。通用对话代理缺乏导航复杂生物管线所需的领域特异性精度。为了克服这一问题，我们提出了SpatialClaw，一种记忆增强的自主生态系统，将空间组学分析统一在单一自然语言交互下。SpatialClaw集成了30项专业技能，涵盖原始数据预处理、空间域识别、反卷积、空间可变基因检测、细胞间通讯分析、多样本和跨模态整合。与现有代理不同，SpatialClaw引入了一种基于图的持久记忆架构，将数据集元数据、分析谱系、生物学见解和用户偏好存储为带版本的节点和边，分布在三个层次（会话、情景和语义），由确定性提升策略管理。一个记忆增强推理（MAR）算子连接记忆存储库和主代理，将检索到的经验综合为每个查询的任务特定指导。在跨越10项空间组学技能的三个记忆敏感场景的严格基准测试中，SpatialClaw优于标准大型语言模型和仅记忆配置。此外，我们通过剖析一个包含15个切片的人类三阴性乳腺癌队列的复杂肿瘤微环境，展示了其强大的生物学实用性。仅需三个对话轮次且无需直接编写脚本，SpatialClaw即可执行完整的端到端工作流，生成标准化输出包。最终，通过将综合分析工具与结构化持久记忆协同，SpatialClaw将空间组学从脱节的计算拼接提升为完全可追溯、可重现且自我改进的发现生态系统。SpatialClaw可在https://github.com/ShangBioLab/SpatialClaw获取使用。

## Abstract
While the expansion of spatial omics has revolutionized our ability to dissect tissue architecture, the accumulation of incompatible computational methods has heavily fragmented end-to-end analysis, rendering complex workflows irreproducible. Generic conversational agents lack the domain-specific precision necessary to navigate the intricate biological pipelines. To overcome this, we present SpatialClaw, a memory-augmented autonomous ecosystem to unify spatial omics analysis under a single natural-language interaction. SpatialClaw integrates 30 specialized skills, spanning raw data preprocessing, spatial domain identification, deconvolution, spatially variable gene detection, cell-cell communication analysis, multi-sample and cross-modality integration. Distinct from existing agents, SpatialClaw introduces a graph-based persistent memory architecture that stores dataset metadata, analysis lineage, biological insights, and user preferences as versioned nodes and edges across three hierarchical layers (Session, Episodic, and Semantic), governed by a deterministic promotion policy. A Memory-Augmented Reasoning (MAR) Operator bridges the memory store and the main agent, synthesizing retrieved experiences into task-specific guidance for each query. In rigorous benchmarking spanning three memory-sensitive scenarios across 10 spatialomics skills, SpatialClaw outperforms both a standard large language model and the memory-only configuration. Furthermore, we demonstrate its robust biological utility by dissecting the complex tumor microenvironment of a 15-section human triple-negative breast cancer cohort. In merely three conversational turns and with zero direct scripting, SpatialClaw executes a comprehensive end-to-end workflow, yielding standardized output bundles. Ultimately, by synergizing comprehensive analytical tools with structured persistent memory, SpatialClaw elevates spatial omics from disjointed computational stitching to a fully traceable, reproducible, and self-improving discovery ecosystem. SpatialClaw is ready to use at https://github.com/ShangBioLab/SpatialClaw.
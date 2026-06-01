---
title: "SpatialClaw: A Memory-Augmented Autonomous Ecosystem for Spatial Omics Analysis"
title_zh: SpatialClaw：面向空间组学分析的记忆增强自主生态系统
authors: "Du, G., Lan, O., Wei, X., Wu, Y., Meng, G., Wu, J., Li, Z., Li, X., Shang, X."
date: 2026-05-25
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.21.723451v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 记忆增强的自主生态系统，整合30个专业技能进行空间组学分析
tldr: 空间组学分析工具碎片化导致工作流不可重复，通用大语言模型缺乏领域精度。SpatialClaw集成30个专业化技能，引入图结构持久记忆（会话、情节、语义三层）和记忆增强推理算子。在三个记忆敏感场景中优于标准LLM和纯记忆配置，在三阴性乳腺癌队列中通过三轮自然语言交互完成端到端分析。该工作将空间组学从碎片化计算提升为可追溯、可重复、自我改进的发现生态系统。
source: biorxiv
selection_source: fresh_fetch
motivation: 克服空间组学分析工具碎片化导致的不可重复性，以及通用大语言模型在复杂生物流程中缺乏领域精度的问题。
method: 构建记忆增强自主生态系统SpatialClaw，集成30个技能，采用图结构分层持久记忆和记忆增强推理算子，实现任务指导与经验复用。
result: 在三个记忆敏感场景的10个空间组学技能中性能优于标准LLM和仅记忆配置；在三阴性乳腺癌队列中零脚本完成标准化端到端分析。
conclusion: SpatialClaw通过结构化持久记忆与综合工具协同，将空间组学分析转化为完全可追溯、可重复、自改进的发现生态。
---

## 摘要
尽管空间组学的扩展彻底改变了我们解析组织结构的能力，但不相容的计算方法的积累严重碎片化了端到端分析，导致复杂工作流不可重复。通用对话代理缺乏导航复杂生物学管线所需的领域特定精度。为克服这一挑战，我们提出SpatialClaw，一个记忆增强的自主生态系统，在单一自然语言交互下统一空间组学分析。SpatialClaw集成了30个专业技能，涵盖原始数据预处理、空间域识别、反卷积、空间可变基因检测、细胞-细胞通讯分析、多样本和跨模态整合。与现有代理不同，SpatialClaw引入基于图的持久记忆架构，将数据集元数据、分析谱系、生物学见解和用户偏好存储为跨三个层次（会话层、情景层、语义层）的版本化节点和边，并由确定性提升策略管理。记忆增强推理（MAR）算子桥接记忆存储与主代理，将检索到的体验综合为每个查询的任务特定指导。在跨越10个空间组学技能的三个记忆敏感场景的严格基准测试中，SpatialClaw优于标准大语言模型和仅记忆配置。此外，通过解析包含15个切片的三人三阴性乳腺癌队列的复杂肿瘤微环境，我们展示了其强大的生物学实用性。仅通过三个对话轮次且无需直接脚本编写，SpatialClaw执行了完整的端到端工作流，生成了标准化输出包。最终，通过将综合分析工具与结构化持久记忆协同，SpatialClaw将空间组学从零散的计算拼接提升为一个完全可追溯、可重复且自我改进的发现生态系统。SpatialClaw可在 https://github.com/ShangBioLab/SpatialClaw 直接使用。

## Abstract
While the expansion of spatial omics has revolutionized our ability to dissect tissue architecture, the accumulation of incompatible computational methods has heavily fragmented end-to-end analysis, rendering complex workflows irreproducible. Generic conversational agents lack the domain-specific precision necessary to navigate the intricate biological pipelines. To overcome this, we present SpatialClaw, a memory-augmented autonomous ecosystem to unify spatial omics analysis under a single natural-language interaction. SpatialClaw integrates 30 specialized skills, spanning raw data preprocessing, spatial domain identification, deconvolution, spatially variable gene detection, cell-cell communication analysis, multi-sample and cross-modality integration. Distinct from existing agents, SpatialClaw introduces a graph-based persistent memory architecture that stores dataset metadata, analysis lineage, biological insights, and user preferences as versioned nodes and edges across three hierarchical layers (Session, Episodic, and Semantic), governed by a deterministic promotion policy. A Memory-Augmented Reasoning (MAR) Operator bridges the memory store and the main agent, synthesizing retrieved experiences into task-specific guidance for each query. In rigorous benchmarking spanning three memory-sensitive scenarios across 10 spatialomics skills, SpatialClaw outperforms both a standard large language model and the memory-only configuration. Furthermore, we demonstrate its robust biological utility by dissecting the complex tumor microenvironment of a 15-section human triple-negative breast cancer cohort. In merely three conversational turns and with zero direct scripting, SpatialClaw executes a comprehensive end-to-end workflow, yielding standardized output bundles. Ultimately, by synergizing comprehensive analytical tools with structured persistent memory, SpatialClaw elevates spatial omics from disjointed computational stitching to a fully traceable, reproducible, and self-improving discovery ecosystem. SpatialClaw is ready to use at https://github.com/ShangBioLab/SpatialClaw.
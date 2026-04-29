---
title: "MSAgent: An Evidence Grounded Agentic Framework for LLM-driven Scientific Exploration in Mass Spectrometry-based Metabolomics"
authors: "Li, Y., Zhong, Y., Liu, P., Yusheng, T., Zhan, H., Xia, J."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.22.720103v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于科学探索和分子发现的自主智能体框架
tldr: MSAgent是一个自主智能体框架，模拟专家逻辑以实现代谢组学中的分子鉴定。
source: biorxiv
selection_source: fresh_fetch
motivation: 用于科学探索和分子发现的自主智能体框架。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Mass spectrometry (MS) is a cornerstone high-throughput technology for molecular discovery, yet the reliable elucidation of chemical structures remains a formidable, expert-dependent bottleneck. Currently, achieving a reliable molecular identification from raw mass spectra necessitates a manual assembly--a labor-intensive ordeal of heuristic reasoning and the tedious integration of siloed computational tools, perpetuating a profound throughput gap between rapid data acquisition and the glacial pace of structural annotation. Here we present MSAgent, an autonomous agentic framework that bridges the gap between computational automation and expert intuition by emulating the cognitive logic of human specialists. By orchestrating a MSToolbox of over 50 domain-specific tools via Large Language Models (LLMs), MSAgent dynamically unifies the analytical pipeline into a scalable, evidence-grounded workflow, allowing for intent-aware planning, cross-resources outputs synthesis, and visual mechanistic interpretation within traceable reasoning chains and evidence-backed analytical reports. We evaluated MSAgent across multiple open benchmarks, including the established community challenges - Critical Assessment of Small Molecule Identification (CASMI) 2016/2022, CANOPUS, and LLM-oriented test cases. On CASMI, MSAgent consistently boosts retrieval performance by over 10% MRR across diverse benchmarks while ensuring high reliability--improving or preserving ranks in 95% of cases. For more challenging molecular de novo tasks on CANOPUS, MSAgent builds upon the outputs of baseline models with consistent refinement, yielding over a 40% average gain in Tanimoto similarity for ground-truth recovery. In addition, MSAgent demonstrates remarkable advantages in eliminating the hallucination phenomenon over LLMs without domain tool support, producing better-calibrated confidence (Pearson r = 0.438 vs -0.219 for gpt-4o). It improves exact-match rate by 38.8% over gpt-4o in candidate discrimination tasks, and achieved a 64% success rate in recommending high-quality candidate structures with Tanimoto similarity more than 0.7, where gpt-4o predominantly selected candidates with similarity below 0.3. Our work enables high-throughput mass spectrometry data to be analyzed in an intent-driven and automated manner, lowering the analysis barrier for no-expert to deliver molecular identification result with transparent analytical process, and accelerating discovery in metabolism and related fields by bridging the gap between experimental data acquisition and computational interpretation.

---

## 论文详细总结（自动生成）

这篇论文介绍了 **MSAgent**，一个基于大语言模型（LLM）驱动的自主智能体框架，旨在解决质谱（Mass Spectrometry, MS）代谢组学中分子结构鉴定这一高度依赖专家的瓶颈问题。

### 1. 论文的核心问题与整体含义
*   **研究动机**：质谱技术虽然实现了高通量数据采集，但从原始光谱推断分子结构（结构鉴定）仍需专家手动整合各种孤立的计算工具，过程耗时耗力且难以规模化。
*   **核心问题**：如何弥合计算自动化与专家直觉之间的鸿沟，实现高通量、可解释且准确的自动化分子鉴定。
*   **整体含义**：MSAgent 通过模拟人类专家的认知逻辑，利用 LLM 编排 50 多个领域特定工具，将复杂的分析流程转化为可扩展、有证据支撑的自动化工作流。

### 2. 论文提出的方法论
*   **核心思想**：构建一个以 LLM 为核心控制器的智能体，通过 **MSToolbox** 统一管理领域工具，并利用 **ReAct（Reasoning and Acting）** 框架进行动态规划和证据合成。
*   **关键技术细节**：
    *   **MSToolbox**：集成了 50 多个工具，涵盖光谱模拟（如 NEIMS, Iceberg）、数据库检索（如 MS2Query, DreaMS）、从头合成（De Novo）生成（如 MSNovelist）及化学信息学分析。
    *   **多智能体协作机制**：包括鉴定智能体（评估候选结构一致性）和机制解释智能体（阐明分子与疾病机制的联系）。
    *   **执行模式**：
        *   **对话模式（Chat Mode）**：深度优先，适用于单谱图的精细探索。
        *   **批处理模式（Batch Mode）**：广度优先，通过预设或自动生成的 Pipeline 进行大规模并行分析。
        *   **网络模式（Network Mode）**：构建分子网络进行比较分析。
    *   **知识增强**：构建了一个包含 5000 多种疾病和 54.5 万个代谢物的分子-疾病知识图谱。

### 3. 实验设计
*   **数据集/场景**：
    *   **CASMI 2016/2022**：小分子鉴定的行业标准挑战赛。
    *   **CANOPUS (NPLIB1)**：用于评估从头结构生成能力。
    *   **MSAgent-Bench**：作者自建的基准，包含从 MassBank RIKEN 抽取的 500 张高质量光谱，分为 Open（开放检索）、Pool（候选池筛选）、MultiTool（多工具协同）和 Knowledge（知识消融）四个子集。
*   **对比方法**：
    *   **领域特定工具**：Fiora, Graff-MS, Iceberg, MSNovelist 等。
    *   **LLM 基准**：直接使用 GPT-4o 等模型（无工具支持）。

### 4. 资源与算力
*   **算力说明**：文中提到为了降低调用延迟，将许多工具转化为“常驻服务”模式（如 GPU 驻留模型），使大多数工具的执行时间缩短至亚分钟级（中位延迟 4.4 秒）。
*   **具体细节**：未明确给出训练智能体或运行实验的总 GPU 小时数或具体显卡数量，但提到使用了 GPT-4o 作为核心推理引擎，并涉及 GPU 加速的深度学习模型推理。

### 5. 实验数量与充分性
*   **实验规模**：
    *   在 CASMI 任务中测试了 425 个案例。
    *   在 CANOPUS 任务中测试了 819 个样本。
    *   自建基准 MSAgent-Bench 包含 500 组实验。
*   **充分性与公平性**：实验覆盖了检索、从头生成、候选者判别等多个维度，并进行了详细的消融实验（如知识来源的贡献分析）。通过对比“纯 LLM”和“单工具”表现，客观地展示了智能体框架的增益。

### 6. 主要结论与发现
*   **性能提升**：在 CASMI 检索任务中，MRR 提升超过 10%；在 CANOPUS 从头生成任务中，Tanimoto 相似度平均提升 40%。
*   **消除幻觉**：相比 GPT-4o，MSAgent 显著减少了化学幻觉。其置信度与准确度的相关性（Pearson r = 0.438）远优于 GPT-4o（r = -0.219）。
*   **结构判别**：在候选者筛选任务中，MSAgent 的准确率比 GPT-4o 高出 38.8%，且在 64% 的情况下能推荐高相似度（>0.7）的候选结构。
*   **公式推导**：MSAgent 的分子式推导准确率达到 93.3%，而纯 LLM 在此任务上几乎完全失败。

### 7. 优点
*   **工具集成度高**：MSToolbox 统一了 50 多种异构工具的输入输出协议，极大地扩展了 LLM 的能力边界。
*   **可解释性强**：提供可追踪的推理链和证据支撑的分析报告，而非“黑箱”预测。
*   **灵活性**：支持自然语言驱动的 Pipeline 构建，降低了非专家使用先进计算工具的门槛。

### 8. 不足与局限
*   **成本与延迟**：依赖 SOTA 商用模型（如 GPT-4o），API 调用成本较高，且多步推理导致整体分析时间长于传统算法。
*   **模型依赖性**：框架性能高度依赖底层 LLM 的推理能力，使用较弱的开源模型可能会导致性能显著下降。
*   **“暗物质”挑战**：对于完全未知的、不符合已知碎片化规则的分子（化学暗物质），智能体的表现可能受限于现有工具和知识库的覆盖范围。

（完）

---
title: "Claw4Science: A Dataset and Platform for the OpenClaw Scientific Agent Ecosystem"
title_zh: Claw4Science：面向 OpenClaw 科学智能体生态系统的数据集与平台
authors: "Xu, M., Chen, J., Zhang, Z."
date: 2026-04-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.30.715118v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 科学智能体生态系统与基于技能的工作流设计
tldr: 针对科学AI智能体生态中OpenClaw项目存在的碎片化、质量参差不齐及缺乏统一发现机制等问题，本文推出了Claw4Science。该工作包含首个涵盖91个项目、2230项技能的精选数据集，并构建了一个统一的公共平台。研究分析了科学智能体的发展模式，揭示了从孤立系统向模块化、可共享计算模型转变的趋势，为未来科学AI智能体的基准测试和基础设施建设奠定了基础。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-30-715118-v1/fig-001.webp\", \"caption\": \"Figure 5 | Example of a BioClaw-enabled analysis within the OpenClaw ecosystem. Given an input protein sequence, the system integrates distributed skills for sequence analysis, structural prediction, and functional annotation. The predicted structure corresponds to human 𝐿-tubulin (TUBG1), with the backbone colored by AlphaFold confidence (pLDDT) and the experimentally annotated GTP-binding region (residues 142–148) highlighted in magenta. This example illustrates how ecosystem-level composition of reusable skills enables end-to-end scientific workflows.\", \"page\": 21, \"index\": 1, \"width\": 832, \"height\": 678}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-30-715118-v1/fig-002.webp\", \"caption\": \"Figure 1 | Overview of the OpenClaw scientific ecosystem. The figure organizes projects into major branches, including core platform variants, team and orchestration systems, biomedicine-related agents, and general research agents. It also highlights the shift from pre-OpenClaw systems to a broader post-OpenClaw ecosystem.\", \"page\": 2, \"index\": 2, \"width\": 815, \"height\": 409}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-30-715118-v1/fig-003.webp\", \"caption\": \"Figure 6 | BioClaw-enabled RNA-seq di!erential expression analysis on a publicly available dataset (GSE150316). The system retrieves the dataset, performs di!erential expression analysis with FDR correction, and generates a publication-quality volcano plot. Significantly upregulated genes are shown in red and downregulated genes in blue (| log2 FC| > 1, FDR < 0.05). Representative genes are labeled. This example demonstrates how BioClaw integrates data retrieval, statistical analysis, visualization, and biological interpretation within the OpenClaw ecosystem.\", \"page\": 22, \"index\": 3, \"width\": 832, \"height\": 583}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-30-715118-v1/fig-004.webp\", \"caption\": \"Figure 4 | The Claw4Science platform. (a) Project directory view, which organizes OpenClaw-related projects into functional categories. (b) Skill hub interface, which aggregates o\\\"cial registries and community-maintained skill libraries into a unified navigation layer. (c) Blog and content view, which provides tutorials, updates, and ecosystem insights. (d) Watching list, which tracks emerging projects and recent activity across the ecosystem.\", \"page\": 10, \"index\": 4, \"width\": 806, \"height\": 433}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-30-715118-v1/fig-005.webp\", \"caption\": \"Figure 3 | Distribution of 2,230 skills across 34 scientific categories. Area represents the number of skills in each category. Due to space constraints, several minor categories are abbreviated as (A) research review and peer review, (B) physics, materials, and earth sciences, (C) general and developer tools, and (D) finance and economics.\", \"page\": 8, \"index\": 5, \"width\": 832, \"height\": 504}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-30-715118-v1/fig-006.webp\", \"caption\": \"Table 1 | Curated list of projects included in the post-OpenClaw ecosystem analysis.\", \"page\": 19, \"index\": 6, \"width\": 832, \"height\": 1123}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-30-715118-v1/fig-007.webp\", \"caption\": \"Figure 2 | Structural map of the post-OpenClaw ecosystem. The figure distinguishes direct OpenClawderived branches from adjacent independent systems, and organizes projects into major layers such as core platform variants, orchestration systems, research systems, domain applications, and skill libraries. Unlike Figure 1, this map is intended to provide a more systematic view of ecosystem structure rather than a purely conceptual overview.\", \"page\": 5, \"index\": 7, \"width\": 832, \"height\": 617}]"
motivation: 解决OpenClaw科学智能体生态中项目分散、技能质量不一及缺乏统一检索与比较工具的碎片化现状。
method: 构建并发布了首个包含91个项目和2230项技能的精选数据集，并开发了Claw4Science公共平台进行统一管理与展示。
result: 揭示了科学计算正从孤立系统转向模块化、可共享的模式，并识别出在评估、可复现性和治理方面的挑战。
conclusion: 该数据集和平台为科学AI智能体的标准化基础设施和未来基准测试提供了重要基础。
---

## 摘要
大语言模型催生了一类新型科学软件，即能够执行生物信息学、药物研发及相关领域研究工作流的 AI 智能体。在这些系统中，OpenClaw 引入了一种基于技能的设计，将工作流表示为结构化的 Markdown 文件，从而降低了贡献门槛并促进了生态系统的快速增长。然而，这种增长也导致了碎片化问题：项目分布在独立的仓库中，技能质量参差不齐，命名不一致，且缺乏统一的工具发现或比较机制。在这项工作中，我们推出了首个经过策划的 OpenClaw 科学生态系统数据集，涵盖了 34 个科学类别的 91 个项目和 2,230 项技能。基于该数据集，我们分析了科学智能体开发的结构、分布和新兴模式。我们进一步介绍了 Claw4Science (https://claw4science.org)，这是一个将项目进行组织并将分布式技能仓库聚合到统一科学工作流界面的公共平台。我们的研究结果揭示了科学计算正从孤立系统向更模块化、可共享的模型转变，同时强调了在评估、可复现性和治理方面面临的挑战。我们认为，该数据集为未来科学 AI 智能体的基准测试和标准化基础设施奠定了基础。

## Abstract
Large language models have enabled a new class of scientific software in the form of AI agents that can execute research workflows across bioinformatics, drug discovery, and related domains. Among these systems, OpenClaw introduced a skill-based design that represents workflows as structured Markdown files, lowering the barrier to contribution and enabling rapid ecosystem growth. However, this growth has led to fragmentation: projects are distributed across independent repositories, skill quality varies widely, naming is inconsistent, and there is no unified way to discover or compare tools. In this work, we present the first curated dataset of the OpenClaw scientific ecosystem, covering 91 projects and 2,230 skills across 34 scientific categories. Based on this dataset, we analyze the structure, distribution, and emerging patterns of scientific agent development. We further introduce Claw4Science (https://claw4science.org), a public platform that organizes projects and aggregates distributed skill repositories into a unified interface for scientific workflows. Our results reveal a shift from isolated systems toward a more modular and shareable model of scientific computation, while highlighting open challenges in evaluation, reproducibility, and governance. We argue that this dataset provides a foundation for future benchmarks and standardized infrastructure for scientific AI agents.

---

## 论文详细总结（自动生成）

### 论文总结：Claw4Science —— 面向 OpenClaw 科学智能体生态系统的数据集与平台

#### 1. 核心问题与整体含义（研究动机和背景）
随着大语言模型（LLM）的发展，科学 AI 智能体（如用于生物信息学、药物研发的智能体）大量涌现。**OpenClaw** 框架通过将研究工作流定义为结构化的 Markdown “技能”（Skills），极大地降低了开发门槛。然而，这种快速增长带来了严重的**碎片化问题**：
*   **项目分散**：大量项目分布在独立仓库，难以发现和比较。
*   **命名混乱**：存在严重的命名冲突（如多个项目均叫 "ScienceClaw"）。
*   **质量参差不齐**：缺乏统一的评估标准和质量控制。
*   **孤立开发**：早期系统多为封闭式，难以跨系统共享和复用工作流。
**Claw4Science** 的提出旨在通过构建首个精选数据集和统一平台，为科学智能体生态提供导航、规范和评估基础。

#### 2. 方法论：核心思想与技术细节
论文的核心思想是**“以技能为中心的生态整合”**。
*   **数据集构建**：通过 GitHub API 自动化扫描与人工审查相结合，收集了 91 个核心项目和 2,230 项科学技能。
*   **分类逻辑**：
    *   **功能分类**：将项目分为核心运行时（Runtimes）、编排系统（Orchestration）、领域特定智能体（Domain-specific Agents）和技能库。
    *   **结构分类**：区分 OpenClaw 的直接衍生分支与独立的兼容系统。
*   **技能（Skill）定义**：技能被定义为包含自然语言指令和可选代码块（Python, R, Bash 等）的 Markdown 文件。这种设计实现了“跨运行时”的移植性。
*   **Claw4Science 平台**：构建了一个公共门户（claw4science.org），提供项目目录、技能聚合中心（Skill Hub）和命名去重机制。

#### 3. 实验设计：数据集、场景与对比
由于本文属于**数据集与平台类论文**，其“实验”侧重于生态系统分析和功能验证：
*   **分析对象**：涵盖 34 个科学类别（如基因组学、临床医疗、药物研发等）的 2,230 项技能。
*   **基准对比**：将 OpenClaw 生态与早期的“封闭式”系统（如 AutoBA, CellVoyager, ChemCrow 等）进行对比，强调模块化与可重用性的提升。
*   **案例研究（Case Study）**：
    *   **BioClaw 验证**：在生物信息学场景下，演示了智能体如何动态调用技能完成蛋白质序列分析（TUBG1 鉴定）和 RNA-seq 差异表达分析（数据集 GSE150316）。
    *   **评估指标**：侧重于技能的分类准确率（96%）和工作流的端到端执行能力。

#### 4. 资源与算力
*   **算力说明**：论文中**未明确提及**具体的 GPU 型号、数量或训练时长。
*   **原因分析**：该研究主要关注生态系统的元数据收集、分类分析和平台构建，而非从头训练大型基础模型。其核心贡献在于数据治理和系统集成。

#### 5. 实验数量与充分性
*   **实验规模**：分析了 91 个项目和超过 2,200 个技能，样本量在同类生态研究中具有代表性。
*   **充分性评价**：
    *   **宏观层面**：对生态系统的层级结构（运行时、编排层、应用层）进行了深入的统计分析，较为充分。
    *   **微观层面**：通过 BioClaw 案例展示了实际应用闭环。
    *   **局限性**：缺乏对 2,230 项技能的大规模自动化性能评测（Benchmark），目前的验证仍偏向定性展示。

#### 6. 主要结论与发现
*   **模式转变**：科学计算正从“孤立的单体系统”转向“模块化、可共享的智能体生态”。
*   **技能驱动增长**：低门槛的 Markdown 技能设计是生态爆发的核心动力。
*   **分布不均**：关注度高度集中在少数核心平台，而科学应用类项目多处于“长尾”状态；基因组学是目前技能最丰富的领域。
*   **治理危机**：命名冲突（23 起案例）和技能质量波动是阻碍生态成熟的主要障碍。

#### 7. 优点：亮点与创新
*   **首创性**：填补了科学 AI 智能体领域缺乏统一索引和数据集的空白。
*   **实用性**：Claw4Science 平台为研究人员提供了实际的工具发现入口，解决了命名歧义。
*   **前瞻性**：提出了将“技能”作为科学贡献基本单位的观点，并倡导建立专门的科学技能评审机制（如 Claw4S 会议）。

#### 8. 不足与局限
*   **评估基准缺失**：尚未建立起针对科学技能准确性和可靠性的标准化自动评分系统。
*   **外部依赖风险**：许多技能依赖外部 API 或特定模型版本，存在“模型漂移”导致的可复现性问题。
*   **治理机制尚轻**：目前主要依靠人工策划和 Claw4Science 平台的维护，缺乏去中心化的自动治理协议。
*   **偏差风险**：数据集主要来源于 GitHub，可能忽略了非开源或非英语社区的贡献。

（完）

---
title: "OmniCellAgent: An AI Scientist for Omic-Driven Scientific Discovery"
title_zh: OmniCellAgent：面向组学驱动科学发现的AI科学家
authors: "Huang, D., Li, H., Li, W., Zhang, H., Xu, T., Lu, Y., Fang, K., Xu, Z., Chen, J., Dickson, P., Sardiello, M., Buchser, W., Cooper, J. D., Cruchaga, C., Eghtesady, P., Li, G., Goedegebuure, P., DeNardo, D., Ding, L., Fields, R. C., Zhan, M., Miller, J. P., Province, M., Chen, Y., Payne, P., Li, F."
date: 2026-05-20
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.31.667797v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于生物医学组学自动化知识发现的多智能体AI框架
tldr: 生物医学发现中，选择相关组学数据集并利用数据库和文献进行结果解读是假设生成的关键，但现有AI代理需要用户预定义疾病数据集，对非计算研究者困难。OmniCellAgent是一个基于大规模单细胞RNA测序资源的多智能体AI框架，可自动检索、整合和分析跨组织与条件的疾病及对照数据集。它通过生物医学先验知识智能体进行系统靶点注释，并由领域专家智能体进行下游解读，聚合证据生成结构化分析报告和数据驱动假设。在多种疾病设置下，该框架能识别相关数据集、优先排序生物学意义靶点并产生全面证据支持的假设，降低了组学驱动发现的障碍。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有AI代理需要用户预定义疾病数据集，过程繁琐耗时，尤其对非计算研究人员，阻碍了组学驱动的科学发现。
method: 构建多智能体AI框架OmniCellAgent，自动检索整合大规模scRNA-seq数据，结合先验知识智能体和领域专家智能体进行靶点注释与下游解读。
result: 在多种疾病设置中，框架能自动识别相关数据集、优先排序生物学意义靶点，并生成结构化的、证据支持的假设。
conclusion: 多智能体AI系统可降低组学驱动发现的壁垒，加速精准医学中的假设生成。
---

## 摘要
在生物医学科学发现中，利用数据库和文献中的先验知识识别相关组学数据集并解释分析结果，对于生成新颖假设至关重要。尽管最近的AI智能体支持自动化的组学分析和文献检索，但它们通常需要用户预先定义和整理疾病特定数据集，这一过程仍然具有挑战性且耗时，尤其对于非计算研究人员而言。在此，我们提出OmniCellAgent，这是一个基于大规模单细胞RNA测序（scRNA-seq）资源构建的多智能体AI框架，能够自主检索、整合和分析跨组织与条件下不同细胞类型的疾病及对照相关数据集。此外，OmniCellAgent整合了一个生物医学先验知识智能体，用于利用整理好的数据库和文献进行系统性靶标注释，以及领域特定专家智能体用于对高优先级靶标进行下游解释。通过聚合各智能体的证据，该框架生成结构化的分析报告和数据驱动的假设。我们在多种疾病场景下评估了OmniCellAgent，展示了其识别相关数据集、优先考虑生物学意义靶标以及生成全面、证据支持的假设的能力。我们的结果表明，多智能体AI系统可以降低组学驱动发现的障碍，并加速精准医学中的假设生成。源代码公开获取于：https://github.com/FuhaiLiAiLab/OmniCellAgent。

## Abstract
In biomedical scientific discovery, identifying relevant omics datasets and interpreting analysis results using prior knowledge from databases and literature are essential for generating novel hypotheses. Although recent AI agents support automated omics analysis and literature retrieval, they typically require users to predefine and curate disease-specific datasets, which is a process that remains challenging and time-consuming, particularly for non-computational researchers. Herein we present OmniCellAgent, a multi-agent AI framework built on large-scale single-cell RNA sequencing (scRNA-seq) resources that autonomously retrieves, integrates and analyzes disease and control-related datasets of diverse cell types across tissues and conditions. Moreover, OmniCellAgent incorporates a biomedical prior knowledge agent for systematic target annotation using curated databases and literature, as well as domain-specific expert agents for downstream interpretation of high-priority targets. By aggregating evidence across agents, the framework generates structured analytical reports and data-driven hypotheses. We evaluate OmniCellAgent across multiple disease settings, demonstrating its ability to identify relevant datasets, prioritize biologically meaningful targets and produce comprehensive, evidence-supported hypotheses. Our results suggest that multi-agent AI systems can reduce barriers to omics-driven discovery and accelerate hypothesis generation in precision medicine. The source code is publicly available at: https://github.com/FuhaiLiAiLab/OmniCellAgent.

---

## 论文详细总结（自动生成）

# OmniCellAgent 论文详细总结

## 1. 论文的核心问题与整体含义

- **背景与动机**：生物医学科学发现中，识别相关的组学数据集并利用数据库和文献中的先验知识进行结果解读，是生成新颖假设的关键步骤。尽管已有 AI 智能体支持自动化的组学分析和文献检索，但它们通常要求用户预先定义和整理疾病特异数据集，这一过程对非计算研究人员而言仍然繁琐且耗时，严重阻碍了组学驱动的科学发现。
- **核心问题**：如何构建一个能够自主完成“数据集检索→整合分析→靶标注释→假设生成”全流程的 AI 框架，降低组学发现的门槛，加速精准医学中的假设提出。
- **整体含义**：提出 OmniCellAgent，一个基于大规模单细胞 RNA 测序（scRNA‑seq）资源的多智能体 AI 框架，旨在自动完成从数据检索到假设生成的端到端流程，从而降低非计算研究人员参与组学发现的门槛，推动数据驱动假设的生成。

## 2. 论文提出的方法论

- **核心思想**：构建多智能体协同框架，将大规模 scRNA‑seq 数据检索整合、生物医学先验知识注释、领域专家解读等步骤分解为不同专业智能体，最后聚合证据输出结构化报告和数据驱动假设。
- **关键技术细节**：
  - **框架组成**：
    1. **数据检索与整合智能体**：自动检索、整合跨组织和条件（疾病与对照）的 scRNA‑seq 数据集。
    2. **生物医学先验知识智能体**：利用整理好的数据库和文献，对识别到的靶标进行系统性注释。
    3. **领域特定专家智能体**：针对高优先级的靶标进行下游生物学解释（如通路、功能、疾病关联等）。
  - **工作流程（文字描述）**：
    - 用户输入疾病或生物学问题（无需提供预定义数据集）→ 数据检索智能体自动从大规模 scRNA‑seq 资源中匹配相关疾病/对照数据集 → 整合并进行差异分析等 → 产生候选靶标 → 先验知识智能体对候选靶标进行数据库和文献注释 → 领域专家智能体对高优先级靶标进行深入解读 → 所有智能体的证据聚合 → 输出结构化分析报告 + 数据驱动的假设。
- **算法流程**：无显式公式，本质为多智能体协同的管道式流程，各智能体可能采用 LLM 或专门模型调用数据库/文献 API。

## 3. 实验设计

- **使用的数据集/场景**：基于大规模单细胞 RNA 测序（scRNA‑seq）资源，在“多种疾病设置”下评估。摘要未列出具体疾病名称，推测涵盖常见疾病（如癌症、神经退行性疾病等）。
- **Benchmark**：文中未提及与现有方法的定量对比（如传统分析方法或其它 AI 智能体）。评估侧重于框架自身的功能展示（能否识别相关数据集、能否优先排序有意义的靶标、能否生成证据支持的假设）。
- **对比方法**：论文未明确说明对比了哪些方法。可能仅通过案例分析/用户演示验证有效性，缺乏标准基准上的公平对比。
- **实验充分性**：由于缺少详细实验设计（具体疾病数量、统计指标、消融实验等），无法判断充分性。从摘要看，仅进行了“多种疾病场景”的定性评估，实验严谨性有待补充。

## 4. 资源与算力

- **论文中未明确说明**：未提及使用的 GPU 型号、数量、训练时长或推理阶段所需算力。也未说明大规模 scRNA‑seq 资源的存储规模。因此，无法判断其计算开销。

## 5. 实验数量与充分性

- **实验数量**：仅提到在“多种疾病设置”下评估，但具体数量未知。没有消融实验、不同组件对比实验或统计显著性检验。
- **充分性与客观性**：目前描述较为初步，缺乏定量指标（如召回率、准确率、假设新颖性评分等）。评估主要依赖定性展示，公平性难以保证。作为预印本（biorxiv），可能在后续版本中补充更多实验。

## 6. 论文的主要结论与发现

- OmniCellAgent 能够自动识别与疾病相关的 scRNA‑seq 数据集，无需用户预定义数据。
- 能优先排序具有生物学意义的靶标（通过先验知识注释）。
- 能生成全面、证据支持的假设，输出结构化报告。
- 表明多智能体 AI 系统可以有效降低组学驱动发现的壁垒，加速精准医学中的假设生成。

## 7. 优点

- **全流程自动化**：从数据检索到假设生成完全自主，极大降低使用者（特别是非计算研究人员）的技术门槛。
- **多智能体协作架构**：将先验知识注释、领域专家解读解耦，提高系统性 and 可靠性。
- **基于大规模 scRNA‑seq 资源**：覆盖面广，可支持跨组织、跨条件的多种疾病分析。
- **开源代码**：提供 GitHub 仓库，利于社区复现和扩展。

## 8. 不足与局限

- **实验验证不充分**：缺少定量指标和标准基准（Benchmark），仅通过案例展示，结论说服力有限。
- **未与现有方法对比**：无法判断其相较于传统分析或其它 AI 智能体的优势，公平性存疑。
- **依赖资源质量**：框架性能高度依赖底层 scRNA‑seq 资源的覆盖度和质量控制，对于罕见疾病或数据稀缺领域可能表现不佳。
- **算力与可扩展性未讨论**：未说明处理大规模数据所需的计算资源，可能限制实际部署。
- **偏差风险**：先验知识智能体依赖于已有数据库和文献，可能引入流行偏差（对热门基因/通路偏好），限制新颖假设的发现。
- **缺乏假阳性控制**：自动生成假设的可靠性如何验证？没有提及验证试验或人为监督机制。

（完）

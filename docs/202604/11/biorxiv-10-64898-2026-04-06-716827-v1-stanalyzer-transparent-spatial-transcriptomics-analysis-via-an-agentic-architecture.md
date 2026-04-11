---
title: "STAnalyzer: Transparent Spatial Transcriptomics Analysis via an Agentic Architecture"
title_zh: STAnalyzer：通过智能体架构实现透明的空间转录组学分析
authors: "Luo, H. H., Liu, L., Xing, Z., Li, X., Zhang, X., Du, W., Liu, B., Wang, J., Yu, G."
date: 2026-04-09
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.06.716827v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自动化知识发现和生物假设生成的智能体框架
tldr: 针对空间转录组学分析中工具链碎片化、参数复杂及解释困难等挑战，本文提出了STAnalyzer，一个基于多智能体架构的自动化分析框架。该框架通过意图驱动编排、多模态自我修正及基于证据的交叉验证，实现了从原始数据处理到生物学假设生成的全流程自动化。STAnalyzer不仅降低了分析门槛，还通过结合视觉模式、统计指标和文献数据库，确保了分析结果的鲁棒性与科学透明度，加速了生物学发现。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-001.webp\", \"caption\": \"Figure 2: Architecture of the Service Planner Agent. The framework is organized into three logical layers: (Top) The Tool Matching Layer leverages Service-File-Type Constraints and a semantic Tool Matching Engine to select appropriate tools (e.g., CellPhoneDB) based on standardized descriptions. (Middle) The Execution Workflow Layer illustrates the closedloop process from tool matching and parameter configuration to execution, incorporating a feedback mechanism for error recovery. (Bottom) The Infrastructure Layer supports the workflow via a Unified API Call interface and a Containerized Runtime Environment, providing Fine-Grained Diagnostic Feedback to resolve execution failures.\", \"page\": 6, \"index\": 1, \"width\": 943, \"height\": 623}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-002.webp\", \"caption\": \"Figure 6: Extended experiments on the 10x Xenium human lung cancer dataset. a Bar chart of the number of cells and genes before and after quality control. b Spatial domain identification results by STAnalyzer. c Heatmap of the top 3 GO terms enriched in each spatial domain. d Bar plot of cell type composition. The chart displays the number of spatial spots assigned. e The inferred functional results of the main spatial domain and the explainable supporting evidence. f STAnalyzer automatically formulates new biological hypotheses based on the available direct evidence. g Subcellular dynamics of the Treg-mediated immunosuppressive interface. The physical boundary between Tregs and T cells acts as an active signaling hub. Contact-driven spatial reorganization of co-inhibitory molecules and TNT-mediated mitochondrial transfer synergistically activate the cGAS-STING pathway in T cells. This triggers non-apoptotic immune silencing (anergy), redefining the static barrier as a dynamic target for precision immunomodulation.\", \"page\": 15, \"index\": 2, \"width\": 881, \"height\": 1088}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-003.webp\", \"caption\": \"Figure 1: System architecture and end-to-end workflow of STAnalyzer. The framework comprises: (1) a natural language User Interface; (2) the Orchestrator Agent for intent parsing and multi-agent coordination; (3) the Service Execution layer including the Service Planner Agent, specialized analytical services, and the Data Interpretation Agent; (4) the Knowledge Integration Agent linking external resources (PubMed, KEGG); (5) the Data Management module for file provenance and traceability; and (6) an end-to-end workflow from automated analysis through knowledge integration to result generation.\", \"page\": 2, \"index\": 3, \"width\": 943, \"height\": 693}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-004.webp\", \"caption\": \"Figure 3: Workflow of the Data Interpretation Agent. (A) Single File Query: The agent processes individual files (CSV, H5AD, Images, Reports, etc.) based on specific user queries. It utilizes tools like code interpreters and multimodal models to extract gene signatures, statistical metrics, and visual cluster patterns. (B) File Tree Query: For complex synthesis tasks, the agent inputs the entire execution record. It employs a “Reorder Plan” to prioritize data access (e.g., getting parameters before evidence), performs synthesis and deduction, and outputs a final validation result (Pass/Fail) regarding the analysis quality.\", \"page\": 8, \"index\": 4, \"width\": 892, \"height\": 396}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-005.webp\", \"caption\": \"Figure 5: Automated analysis on the human DLPFC dataset. a (Left) Statistical analysis of various metrics of the original ST data. (Right) Bar chart of the number of cells and genes before and after quality control. b Spatial domain identification results and the automatic assessment feedback provided by STAnalyzer. c Heatmap of the top-6 TFs with high spatial TF activity scores. d Heatmap visualizing the spatial distribution of major enriched metabolic pathway activities across the ST data. e Bar plot of cell type composition. The chart displays the number of spatial spots assigned to each identified major cell type across the tissue section. f Top 20 enriched GO terms for each of the eight spatial domains. g STAnalyzer conducts evidence cross-validation at four levels to automatically analyze the functional characteristics of each spatial domain. h Traceable and interpretable functional characterization of four spatial domains, highly consistent with established biological knowledge.12\", \"page\": 12, \"index\": 5, \"width\": 888, \"height\": 1161}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-006.webp\", \"caption\": \"Figure 4: The architecture of Knowledge Integration Agent. The workflow proceeds from left to right, starting with the Query Alignment which standardizes ambiguous user inputs. The process then bifurcates into two complementary pipelines: (Top) The Literature Pipeline employs a RAG-based funnel to process massive unstructured text, using coarse ranking and a targeted reading plan to distill the top 50 candidates down to highly relevant evidence; (Bottom) The Database Pipeline directly retrieves structured molecular facts via unified APIs. Finally, information from both sources is synthesized into Traceable Insights, grounded with explicit citations (DOIs, URLs) to support downstream verification and reasoning.\", \"page\": 9, \"index\": 6, \"width\": 939, \"height\": 396}]"
motivation: 空间转录组分析受限于碎片化的工具链、复杂的参数设置以及缺乏多模态反馈和生物学知识的深度整合。
method: 构建了一个多智能体协作框架，利用意图驱动编排、多模态闭环自我修正及基于权威数据库的证据交叉验证来自动化分析流程。
result: 实现了从原始数据处理到生物学假设生成的全生命周期自动化，并确保了分析过程的透明度与结果的科学可靠性。
conclusion: STAnalyzer为空间组学研究提供了一个稳健且可扩展的自动化分析平台，显著降低了技术门槛并加速了数据向生物学见解的转化。
---

## 摘要
空间转录组学能够在空间背景下实现基因表达的高分辨率分析，但其潜力往往受限于碎片化的工具链、复杂的参数以及解释高维数据时的认知瓶颈。尽管近期的大语言模型（LLM）智能体已尝试自动化这一过程，但它们仍受限于僵化的执行逻辑，缺乏用于自我修正的多模态反馈，且在认知上与已有的生物学知识相隔离。在此，我们提出了 STAnalyzer，这是一个智能多智能体框架，旨在自动化从原始数据处理到生物学假设生成的端到端分析生命周期。超越传统流程，STAnalyzer 采用协作智能架构来实现三项核心能力：(1) 意图驱动的编排（Intent Driven Orchestration），将自然语言查询动态转化为严谨的生物信息学工作流；(2) 多模态自我优化（Multi Modal Self Refinement），通过视觉模式和统计指标证据的闭环综合，自主确保分析的稳健性；(3) 基于证据的交叉验证（Evidence based Cross Validation），通过将研究发现锚定在金标准文献和结构化数据库中，弥合数据驱动的相关性与生物学因果关系之间的鸿沟。通过消除人工分析瓶颈并确保严谨的证据可追溯性和透明度，STAnalyzer 提升了高分辨率空间组学在更广泛研究群体中的可及性。它为跨平台自动化分析和加速生物学发现提供了一个稳健且可扩展的框架，将海量空间数据集转化为可验证的生物学见解。

## Abstract
Spatial transcriptomics enables high resolution profiling of gene expression within spatial contexts, yet its potential is often hindered by fragmented toolchains, intricate parameters, and cognitive bottlenecks of interpreting high dimensional data. While recent Large Language Model agents have attempted to automate this process, they remain constrained by rigid execution logic, lack multimodal feedback for self correction, and operate in epistemic isolation from established biological knowledge. Here, we present STAnalyzer, an intelligent multiagent framework designed to automate the end to end analytical lifecycle from raw data processing to biological hypothesis generation. Transcending traditional pipelines, STAnalyzer employs a collaborative intelligence architecture to achieve three core capabilities: (1) Intent Driven Orchestration, which dynamically translates natural language queries into rigorous bioinformatics workflows; (2) Multi Modal Self Refinement, which autonomously ensures analytical robustness through closed loop synthesis of evidence from visual patterns and statistical metrics; and (3) Evidence based Cross Validation, which bridges the gap between data driven correlations and biological causation by anchoring findings in ground truth literature and structured databases. By eliminating manual analytical bottlenecks and ensuring rigorous evidentiary traceability and transparency, STAnalyzer makes high resolution spatial omics more accessible to a broader research community. It provides a robust and scalable framework for cross platform automated analysis and accelerated biological discovery, translating massive spatial datasets into verifiable biological insights.

---

## 论文详细总结（自动生成）

### 论文总结：STAnalyzer —— 基于智能体架构的透明空间转录组分析框架

#### 1. 核心问题与整体含义（研究动机和背景）
空间转录组学（Spatial Transcriptomics, ST）通过结合基因表达与空间位置信息，为理解组织架构和疾病微环境提供了前所未有的视角。然而，该领域面临三大挑战：
*   **技术门槛高**：分析工具链碎片化，参数配置复杂，对非计算背景的生物学家极不友好。
*   **解释困难**：高维数据的生物学解读依赖深厚的领域知识，存在认知瓶颈。
*   **现有智能体缺陷**：现有的生物信息学 LLM 智能体通常执行逻辑僵化（缺乏依赖感知）、多模态盲区（无法理解图表结果）以及认知孤立（无法有效整合外部最新文献和数据库）。
**STAnalyzer** 旨在通过多智能体协作架构，实现从原始数据到生物学假设生成的全流程自动化、透明化和知识增强。

#### 2. 方法论：核心思想与关键技术
STAnalyzer 采用 **人机协同（Human-in-the-Loop）的多智能体架构**，包含四个专门化智能体：
*   **编排智能体 (Orchestrator Agent, OA)**：作为用户接口，将自然语言意图解析为任务序列，管理全局上下文，并根据反馈动态调整计划。
*   **服务规划智能体 (Service Planner Agent, SPA)**：
    *   **约束匹配**：基于输入文件类型和任务意图，从工具库中筛选最优工具。
    *   **鲁棒执行**：利用 Docker 容器化微服务解决环境依赖问题，并捕获细粒度错误日志进行自我修复。
*   **数据解释智能体 (Data Interpretation Agent, DIA)**：
    *   **多模态理解**：结合代码解释器（处理 CSV/H5AD 数据）和多模态大模型（理解 UMAP 图、空间分布图等可视化结果）。
    *   **有序阅读计划**：通过逻辑排序避免上下文溢出，综合统计指标与视觉证据。
*   **知识整合智能体 (Knowledge Integration Agent, KIA)**：
    *   **双管齐下**：文献流水线（基于 RAG 检索 PubMed）与数据库流水线（调用 KEGG、CellMarker 等 API）。
    *   **可追溯性**：所有结论均附带 DOI 或 URL，确保证据链闭环。

#### 3. 实验设计
论文在两个具有代表性的空间转录组数据集上验证了系统的有效性：
*   **10x Visium 人类背外侧前额叶皮层 (DLPFC) 数据集**：
    *   **规模**：3,673 个斑点（spots），33,538 个基因。
    *   **目标**：验证自动化分析与已知皮层架构的生物学一致性。
*   **10x Xenium 人类肺癌数据集**：
    *   **规模**：超过 161,000 个细胞（亚细胞分辨率），480 个基因。
    *   **目标**：展示系统在处理大规模、高分辨率数据时的扩展性及发现新生物学假设的能力。
*   **对比基准**：主要通过与已发表的权威生物学结论进行对标，验证系统生成的空间域划分、细胞类型标注及功能富集分析的准确性。

#### 4. 资源与算力
*   **模型集成**：系统集成了 **Qwen（通义千问）** 系列模型用于自然语言理解和决策。
*   **后端架构**：使用 FastAPI、Docker 容器化技术、MongoDB 存储元数据。
*   **算力说明**：论文**未明确说明**具体的 GPU 型号、数量或训练时长。由于该框架主要基于现有的预训练大模型进行推理和 Agent 编排，其核心算力消耗在于推理侧及生物信息学工具的运行。

#### 5. 实验数量与充分性
*   **实验规模**：论文详细展示了两组大规模的端到端案例研究。
*   **充分性评价**：实验涵盖了从低分辨率（spot-level）到高分辨率（subcellular-level）的跨平台数据，验证了从预处理、聚类、功能注释到高级假设生成的全生命周期。
*   **客观性**：通过展示“思维链（CoT）”和可追溯的文献引用，增强了结果的可信度。虽然缺乏与同类 Agent 框架（如 CellAgent）的直接量化 Benchmark 对比，但其在复杂空间拓扑结构（如免疫抑制屏障）的解读上表现出了深度。

#### 6. 主要结论与发现
*   **自动化能力**：STAnalyzer 能在几分钟内完成原本需要数天的人工分析，准确重建组织空间架构。
*   **生物学发现**：在肺癌数据中，系统自主识别出由 Treg 细胞构成的免疫抑制物理界面，并提出了关于“线粒体转移介导的免疫沉默”的深度生物学假设，这与最新的实验研究高度吻合。
*   **透明度**：通过 HITL 界面，用户可以实时干预和回滚，解决了“黑盒”自动化带来的不可控风险。

#### 7. 优点
*   **多模态闭环**：不仅读数据，还能“看”分析图表，实现了统计学与视觉证据的统一。
*   **知识增强**：通过 RAG 技术将分析结果与 PubMed 文献实时挂钩，显著降低了科研人员的文献调研负担。
*   **高扩展性**：容器化架构使其能够轻松集成新的生物信息学工具。
*   **可追溯性**：提供完整的证据链和 DOI 引用，符合学术严谨性要求。

#### 8. 不足与局限
*   **维度限制**：目前主要侧重于 2D 空间转录组任务，尚未充分扩展到空间多组学（Spatial Multi-omics）或 3D 组织重建。
*   **知识时效性**：虽然有 RAG 机制，但仍受限于外部数据库的更新频率和文献检索的覆盖面。
*   **用户门槛**：尽管降低了编程门槛，但对于完全没有生物学背景的用户，理解系统生成的复杂功能报告仍有挑战。
*   **算力成本**：大规模调用多模态 LLM 可能会产生较高的 API 使用成本。

（完）

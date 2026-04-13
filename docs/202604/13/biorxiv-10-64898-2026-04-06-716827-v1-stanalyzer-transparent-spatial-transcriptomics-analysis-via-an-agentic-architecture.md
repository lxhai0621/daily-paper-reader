---
title: "STAnalyzer: Transparent Spatial Transcriptomics Analysis via an Agentic Architecture"
title_zh: STAnalyzer：基于智能体架构的透明空间转录组学分析
authors: "Luo, H. H., Liu, L., Xing, Z., Li, X., Zhang, X., Du, W., Liu, B., Wang, J., Yu, G."
date: 2026-04-09
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.06.716827v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自动化分析生命周期的智能多智能体框架
tldr: 针对空间转录组学分析中工具链碎片化和解读门槛高的难题，本文推出了STAnalyzer。这是一个基于多智能体架构的自动化框架，能够将自然语言查询转化为严谨的分析流。它通过多模态自我修正和生物学知识库交叉验证，实现了从原始数据处理到假设生成的全生命周期管理，显著提升了分析的透明度与可重复性，助力科研人员更高效地从复杂空间组学数据中提取生物学洞见。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-001.webp\", \"caption\": \"Figure 2: Architecture of the Service Planner Agent. The framework is organized into three logical layers: (Top) The Tool Matching Layer leverages Service-File-Type Constraints and a semantic Tool Matching Engine to select appropriate tools (e.g., CellPhoneDB) based on standardized descriptions. (Middle) The Execution Workflow Layer illustrates the closedloop process from tool matching and parameter configuration to execution, incorporating a feedback mechanism for error recovery. (Bottom) The Infrastructure Layer supports the workflow via a Unified API Call interface and a Containerized Runtime Environment, providing Fine-Grained Diagnostic Feedback to resolve execution failures.\", \"page\": 6, \"index\": 1, \"width\": 943, \"height\": 623}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-002.webp\", \"caption\": \"Figure 6: Extended experiments on the 10x Xenium human lung cancer dataset. a Bar chart of the number of cells and genes before and after quality control. b Spatial domain identification results by STAnalyzer. c Heatmap of the top 3 GO terms enriched in each spatial domain. d Bar plot of cell type composition. The chart displays the number of spatial spots assigned. e The inferred functional results of the main spatial domain and the explainable supporting evidence. f STAnalyzer automatically formulates new biological hypotheses based on the available direct evidence. g Subcellular dynamics of the Treg-mediated immunosuppressive interface. The physical boundary between Tregs and T cells acts as an active signaling hub. Contact-driven spatial reorganization of co-inhibitory molecules and TNT-mediated mitochondrial transfer synergistically activate the cGAS-STING pathway in T cells. This triggers non-apoptotic immune silencing (anergy), redefining the static barrier as a dynamic target for precision immunomodulation.\", \"page\": 15, \"index\": 2, \"width\": 881, \"height\": 1088}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-003.webp\", \"caption\": \"Figure 1: System architecture and end-to-end workflow of STAnalyzer. The framework comprises: (1) a natural language User Interface; (2) the Orchestrator Agent for intent parsing and multi-agent coordination; (3) the Service Execution layer including the Service Planner Agent, specialized analytical services, and the Data Interpretation Agent; (4) the Knowledge Integration Agent linking external resources (PubMed, KEGG); (5) the Data Management module for file provenance and traceability; and (6) an end-to-end workflow from automated analysis through knowledge integration to result generation.\", \"page\": 2, \"index\": 3, \"width\": 943, \"height\": 693}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-004.webp\", \"caption\": \"Figure 3: Workflow of the Data Interpretation Agent. (A) Single File Query: The agent processes individual files (CSV, H5AD, Images, Reports, etc.) based on specific user queries. It utilizes tools like code interpreters and multimodal models to extract gene signatures, statistical metrics, and visual cluster patterns. (B) File Tree Query: For complex synthesis tasks, the agent inputs the entire execution record. It employs a “Reorder Plan” to prioritize data access (e.g., getting parameters before evidence), performs synthesis and deduction, and outputs a final validation result (Pass/Fail) regarding the analysis quality.\", \"page\": 8, \"index\": 4, \"width\": 892, \"height\": 396}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-005.webp\", \"caption\": \"Figure 5: Automated analysis on the human DLPFC dataset. a (Left) Statistical analysis of various metrics of the original ST data. (Right) Bar chart of the number of cells and genes before and after quality control. b Spatial domain identification results and the automatic assessment feedback provided by STAnalyzer. c Heatmap of the top-6 TFs with high spatial TF activity scores. d Heatmap visualizing the spatial distribution of major enriched metabolic pathway activities across the ST data. e Bar plot of cell type composition. The chart displays the number of spatial spots assigned to each identified major cell type across the tissue section. f Top 20 enriched GO terms for each of the eight spatial domains. g STAnalyzer conducts evidence cross-validation at four levels to automatically analyze the functional characteristics of each spatial domain. h Traceable and interpretable functional characterization of four spatial domains, highly consistent with established biological knowledge.12\", \"page\": 12, \"index\": 5, \"width\": 888, \"height\": 1161}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-006.webp\", \"caption\": \"Figure 4: The architecture of Knowledge Integration Agent. The workflow proceeds from left to right, starting with the Query Alignment which standardizes ambiguous user inputs. The process then bifurcates into two complementary pipelines: (Top) The Literature Pipeline employs a RAG-based funnel to process massive unstructured text, using coarse ranking and a targeted reading plan to distill the top 50 candidates down to highly relevant evidence; (Bottom) The Database Pipeline directly retrieves structured molecular facts via unified APIs. Finally, information from both sources is synthesized into Traceable Insights, grounded with explicit citations (DOIs, URLs) to support downstream verification and reasoning.\", \"page\": 9, \"index\": 6, \"width\": 939, \"height\": 396}]"
motivation: 空间转录组学分析受限于复杂的工具链、繁琐的参数设置以及缺乏多模态反馈和生物学知识验证的现有AI方案。
method: 提出一种多智能体协作框架，集成意图驱动编排、多模态自我修正及基于文献数据库的证据交叉验证技术。
result: 实现了从原始数据到生物学假设生成的端到端自动化，通过闭环反馈确保了分析的鲁棒性，并提供了可追溯的证据链。
conclusion: STAnalyzer降低了空间组学研究的技术门槛，为跨平台自动化分析和加速生物学发现提供了一个透明且可扩展的解决方案。
---

## 摘要
空间转录组学能够在空间背景下实现基因表达的高分辨率分析，但其潜力往往受限于碎片化的工具链、复杂的参数以及解释高维数据时的认知瓶颈。尽管近期的语言大模型智能体尝试自动化这一过程，但它们仍受限于僵化的执行逻辑，缺乏用于自我修正的多模态反馈，且在认知上与已有的生物学知识相隔离。在此，我们提出了 STAnalyzer，这是一个智能多智能体框架，旨在自动化从原始数据处理到生物学假设生成的端到端分析生命周期。超越传统的流水线，STAnalyzer 采用协同智能架构，实现了三项核心能力：(1) 意图驱动的编排，将自然语言查询动态转化为严谨的生物信息学工作流；(2) 多模态自我优化，通过对视觉模式和统计指标证据的闭环综合，自主确保分析的稳健性；(3) 基于证据的交叉验证，通过将研究发现锚定在真实文献和结构化数据库中，弥合了数据驱动的相关性与生物学因果关系之间的鸿沟。通过消除人工分析瓶颈并确保严谨的证据可追溯性和透明度，STAnalyzer 使高分辨率空间组学对更广泛的研究群体更具可及性。它为跨平台自动化分析和加速生物学发现提供了一个稳健且可扩展的框架，将海量空间数据集转化为可验证的生物学见解。

## Abstract
Spatial transcriptomics enables high-resolution profiling of gene expression within spatial contexts, yet its potential is often hindered by fragmented toolchains, intricate parameters, and cognitive bottlenecks of interpreting high-dimensional data. While recent Large Language Model agents have attempted to automate this process, they remain constrained by rigid execution logic, lack multimodal feedback for self-correction, and operate in epistemic isolation from established biological knowledge. Here, we present STAnalyzer, an intelligent multi-agent framework designed to automate the end-to-end analytical lifecycle--from raw data processing to biological hypothesis generation. Transcending traditional pipelines, STAnalyzer employs a collaborative intelligence architecture to achieve three core capabilities: (1) Intent-Driven Orchestration, which dynamically translates natural language queries into rigorous bioinformatics workflows; (2) Multi-Modal Self-Refinement, which autonomously ensures analytical robustness through closed-loop synthesis of evidence from visual patterns and statistical metrics; and (3) Evidence-based Cross-Validation, which bridges the gap between data-driven correlations and biological causation by anchoring findings in ground-truth literature and structured databases. By eliminating manual analytical bottlenecks and ensuring rigorous evidentiary traceability and transparency, STAnalyzer makes high-resolution spatial omics more accessible to a broader research community. It provides a robust and scalable framework for cross-platform automated analysis and accelerated biological discovery, translating massive spatial datasets into verifiable biological insights.

---

## 论文详细总结（自动生成）

### STAnalyzer：基于智能体架构的透明空间转录组学分析总结

#### 1. 核心问题与整体含义（研究动机和背景）
空间转录组学（Spatial Transcriptomics, ST）是现代生物医学的突破性技术，能够同时获取基因表达谱及其空间位置信息。然而，该领域面临两大瓶颈：
*   **技术瓶颈：** 分析工具链碎片化，环境配置复杂，参数调整依赖专家经验，对非计算背景的生物学家门槛极高。
*   **认知瓶颈：** 高维数据的解读需要深厚的领域知识，现有的自动化工具往往是“黑盒”操作，缺乏透明度，且容易产生大语言模型（LLM）常见的“幻觉”问题，无法将计算结果与已证实的生物学知识有效关联。
**研究动机：** 开发一个能够理解自然语言指令、自主规划工作流、具备多模态感知能力并能通过外部知识库验证结果的智能分析框架。

#### 2. 方法论：核心思想与关键技术
STAnalyzer 提出了一个**人机协同的多智能体（Multi-Agent）架构**，包含四个核心智能体：
*   **编排智能体 (Orchestrator Agent, OA)：** 作为用户接口，将模糊的自然语言意图解析为具体的生物信息学任务，并管理全局上下文。
*   **服务规划智能体 (Service Planner Agent, SPA)：** 
    *   **核心思想：** 解决工具执行的鲁棒性。
    *   **技术细节：** 采用基于约束的工具匹配（Service-File-Type Constraints），通过 Docker 容器化微服务执行代码，并建立细粒度的错误反馈循环，在代码报错时能自主修复参数或重试。
*   **数据解释智能体 (Data Interpretation Agent, DIA)：** 
    *   **核心思想：** 实现多模态理解。
    *   **技术细节：** 能够同时处理 CSV/H5AD 数值数据和 UMAP/空间分布图像。通过“重排序计划（Reorder Plan）”逻辑化地访问文件树，确保在解释结果前先获取参数和统计背景。
*   **知识集成智能体 (Knowledge Integration Agent, KIA)：** 
    *   **核心思想：** 消除认知孤岛。
    *   **技术细节：** 采用双管道模式——文献管道（基于 RAG 技术检索 PubMed）和数据库管道（通过 API 查询 KEGG、CellMarker 等）。所有结论均附带 DOI 或 URL，确保可追溯性。

#### 3. 实验设计
论文通过两个代表性场景验证了系统的有效性：
*   **数据集 1：10x Visium 人类背外侧前额叶皮层 (DLPFC)**
    *   **场景：** 点位级（Spot-level）分辨率，包含 3,673 个点位。
    *   **目的：** 验证系统能否自动重建已知的皮层分层结构及功能特征。
*   **数据集 2：10x Xenium 人类肺癌数据**
    *   **场景：** 亚细胞级（Subcellular）分辨率，包含超过 16.1 万个细胞。
    *   **目的：** 验证系统在大规模数据下的扩展性，以及在复杂肿瘤微环境中的科学发现能力。
*   **对比基准：** 实验结果主要与已发表的权威文献结论（Ground Truth）进行对比，验证智能体推断的准确性。

#### 4. 资源与算力
*   **软件架构：** 后端使用 FastAPI 和 Uvicorn，智能体逻辑基于 LangChain 和 LangGraph 构建。
*   **底层模型：** 集成了 Qwen（通义千问）系列大模型进行自然语言理解和决策。
*   **算力说明：** 文中**未明确说明**具体的 GPU 型号、数量或训练/推理的总时长。但提到系统采用异步任务处理机制，能在数十分钟内完成传统需要数天的人工分析工作。

#### 5. 实验数量与充分性
*   **实验规模：** 论文针对两个跨平台（Visium 和 Xenium）、跨分辨率（点位级和亚细胞级）的数据集进行了全流程测试。
*   **实验内容：** 涵盖了预处理、空间域识别、细胞类型注释、功能富集分析及高级假设生成。
*   **充分性评价：** 实验设计较为充分，展示了从基础分析到深度科学发现的端到端能力。通过与已知生物学事实的对齐，证明了结果的客观性。但由于该领域智能体尚处于起步阶段，论文缺乏与其他同类生物信息智能体（如 CellAgent）的量化横向对比。

#### 6. 主要结论与发现
*   **自动化效率：** STAnalyzer 能够自主完成从原始数据到最终报告的转化，显著降低了人工干预需求。
*   **生物学一致性：** 在 DLPFC 实验中，准确识别出与髓质白质和皮层神经元相关的空间域。
*   **科学发现：** 在肺癌实验中，系统自主发现了 Treg 细胞构成的免疫抑制物理屏障，并提出了关于线粒体转移介导免疫沉默的深度生物学假设，这些假设与最新的实验研究高度吻合。

#### 7. 优点
*   **透明与可追溯：** 解决了 LLM 的幻觉问题，所有生物学解释均有据可查（DOI 引用）。
*   **多模态融合：** 能够“看懂”分析图表并结合数值结果进行综合逻辑推理。
*   **人机协同（HITL）：** 允许用户在关键节点干预，平衡了自动化效率与专家经验。
*   **鲁棒性：** 容器化技术解决了生物信息学工具版本冲突和环境配置的顽疾。

#### 8. 不足与局限
*   **维度限制：** 目前主要针对 2D 空间转录组数据，尚未扩展到 3D 空间组学或多组学（如空间蛋白组）数据。
*   **知识滞后：** 依赖的外部数据库和文献库存在更新延迟，可能无法实时捕捉最前沿的未发表进展。
*   **交互门槛：** 尽管使用自然语言，但对于完全不熟悉空间组学基本概念的用户，如何提出高质量的 Prompt 仍是一个挑战。
*   **计算开销：** 大规模调用 LLM API 和 RAG 检索可能产生较高的 Token 成本。

（完）

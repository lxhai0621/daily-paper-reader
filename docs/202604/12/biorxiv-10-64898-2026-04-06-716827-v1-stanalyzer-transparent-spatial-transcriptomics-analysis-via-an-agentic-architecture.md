---
title: "STAnalyzer: Transparent Spatial Transcriptomics Analysis via an Agentic Architecture"
title_zh: STAnalyzer：通过智能体架构实现透明的空间转录组学分析
authors: "Luo, H. H., Liu, L., Xing, Z., Li, X., Zhang, X., Du, W., Liu, B., Wang, J., Yu, G."
date: 2026-04-09
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.06.716827v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自动化生物知识发现的多智能体框架
tldr: STAnalyzer是一个基于多智能体架构的空间转录组学分析框架，旨在解决现有工具链碎片化、参数复杂及缺乏生物学背景验证等问题。该框架通过意图驱动编排、多模态自我修正和基于证据的交叉验证，实现了从原始数据处理到生物学假设生成的全流程自动化。它不仅降低了空间组学分析的门槛，还通过结合视觉模式、统计指标和文献数据库，确保了分析结果的严谨性与可解释性，为加速生物学发现提供了有力工具。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-001.webp\", \"caption\": \"Figure 2: Architecture of the Service Planner Agent. The framework is organized into three logical layers: (Top) The Tool Matching Layer leverages Service-File-Type Constraints and a semantic Tool Matching Engine to select appropriate tools (e.g., CellPhoneDB) based on standardized descriptions. (Middle) The Execution Workflow Layer illustrates the closedloop process from tool matching and parameter configuration to execution, incorporating a feedback mechanism for error recovery. (Bottom) The Infrastructure Layer supports the workflow via a Unified API Call interface and a Containerized Runtime Environment, providing Fine-Grained Diagnostic Feedback to resolve execution failures.\", \"page\": 6, \"index\": 1, \"width\": 943, \"height\": 623}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-002.webp\", \"caption\": \"Figure 6: Extended experiments on the 10x Xenium human lung cancer dataset. a Bar chart of the number of cells and genes before and after quality control. b Spatial domain identification results by STAnalyzer. c Heatmap of the top 3 GO terms enriched in each spatial domain. d Bar plot of cell type composition. The chart displays the number of spatial spots assigned. e The inferred functional results of the main spatial domain and the explainable supporting evidence. f STAnalyzer automatically formulates new biological hypotheses based on the available direct evidence. g Subcellular dynamics of the Treg-mediated immunosuppressive interface. The physical boundary between Tregs and T cells acts as an active signaling hub. Contact-driven spatial reorganization of co-inhibitory molecules and TNT-mediated mitochondrial transfer synergistically activate the cGAS-STING pathway in T cells. This triggers non-apoptotic immune silencing (anergy), redefining the static barrier as a dynamic target for precision immunomodulation.\", \"page\": 15, \"index\": 2, \"width\": 881, \"height\": 1088}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-003.webp\", \"caption\": \"Figure 1: System architecture and end-to-end workflow of STAnalyzer. The framework comprises: (1) a natural language User Interface; (2) the Orchestrator Agent for intent parsing and multi-agent coordination; (3) the Service Execution layer including the Service Planner Agent, specialized analytical services, and the Data Interpretation Agent; (4) the Knowledge Integration Agent linking external resources (PubMed, KEGG); (5) the Data Management module for file provenance and traceability; and (6) an end-to-end workflow from automated analysis through knowledge integration to result generation.\", \"page\": 2, \"index\": 3, \"width\": 943, \"height\": 693}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-004.webp\", \"caption\": \"Figure 3: Workflow of the Data Interpretation Agent. (A) Single File Query: The agent processes individual files (CSV, H5AD, Images, Reports, etc.) based on specific user queries. It utilizes tools like code interpreters and multimodal models to extract gene signatures, statistical metrics, and visual cluster patterns. (B) File Tree Query: For complex synthesis tasks, the agent inputs the entire execution record. It employs a “Reorder Plan” to prioritize data access (e.g., getting parameters before evidence), performs synthesis and deduction, and outputs a final validation result (Pass/Fail) regarding the analysis quality.\", \"page\": 8, \"index\": 4, \"width\": 892, \"height\": 396}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-005.webp\", \"caption\": \"Figure 5: Automated analysis on the human DLPFC dataset. a (Left) Statistical analysis of various metrics of the original ST data. (Right) Bar chart of the number of cells and genes before and after quality control. b Spatial domain identification results and the automatic assessment feedback provided by STAnalyzer. c Heatmap of the top-6 TFs with high spatial TF activity scores. d Heatmap visualizing the spatial distribution of major enriched metabolic pathway activities across the ST data. e Bar plot of cell type composition. The chart displays the number of spatial spots assigned to each identified major cell type across the tissue section. f Top 20 enriched GO terms for each of the eight spatial domains. g STAnalyzer conducts evidence cross-validation at four levels to automatically analyze the functional characteristics of each spatial domain. h Traceable and interpretable functional characterization of four spatial domains, highly consistent with established biological knowledge.12\", \"page\": 12, \"index\": 5, \"width\": 888, \"height\": 1161}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716827-v1/fig-006.webp\", \"caption\": \"Figure 4: The architecture of Knowledge Integration Agent. The workflow proceeds from left to right, starting with the Query Alignment which standardizes ambiguous user inputs. The process then bifurcates into two complementary pipelines: (Top) The Literature Pipeline employs a RAG-based funnel to process massive unstructured text, using coarse ranking and a targeted reading plan to distill the top 50 candidates down to highly relevant evidence; (Bottom) The Database Pipeline directly retrieves structured molecular facts via unified APIs. Finally, information from both sources is synthesized into Traceable Insights, grounded with explicit citations (DOIs, URLs) to support downstream verification and reasoning.\", \"page\": 9, \"index\": 6, \"width\": 939, \"height\": 396}]"
motivation: 空间转录组分析受限于工具链碎片化、参数复杂以及现有自动化工具缺乏多模态反馈和生物学知识验证。
method: 开发了一种多智能体协作架构，包含意图驱动编排、多模态自我修正以及基于文献和数据库的证据交叉验证机制。
result: 实现了端到端的自动化分析流程，能够自主确保分析鲁棒性，并将数据关联与已知的生物学因果关系进行锚定。
conclusion: STAnalyzer为跨平台空间组学自动化分析提供了透明且可扩展的框架，显著降低了研究门槛并加速了生物学见解的生成。
---

## 摘要
空间转录组学能够在空间背景下实现基因表达的高分辨率分析，但其潜力往往受限于碎片化的工具链、复杂的参数以及解释高维数据时的认知瓶颈。尽管近期的大语言模型（LLM）智能体已尝试自动化这一过程，但它们仍受限于僵化的执行逻辑，缺乏用于自我修正的多模态反馈，且在认知上与已有的生物学知识相隔离。在此，我们提出了 STAnalyzer，这是一个智能多智能体框架，旨在自动化从原始数据处理到生物学假设生成的端到端分析生命周期。超越传统流程，STAnalyzer 采用协作智能架构来实现三项核心能力：(1) 意图驱动的编排（Intent Driven Orchestration），将自然语言查询动态转化为严谨的生物信息学工作流；(2) 多模态自我优化（Multi Modal Self Refinement），通过视觉模式和统计指标证据的闭环综合，自主确保分析的稳健性；(3) 基于证据的交叉验证（Evidence based Cross Validation），通过将研究发现锚定在金标准文献和结构化数据库中，弥合数据驱动的相关性与生物学因果关系之间的鸿沟。通过消除人工分析瓶颈并确保严谨的证据可追溯性和透明度，STAnalyzer 提升了高分辨率空间组学在更广泛研究群体中的可及性。它为跨平台自动化分析和加速生物学发现提供了一个稳健且可扩展的框架，将海量空间数据集转化为可验证的生物学见解。

## Abstract
Spatial transcriptomics enables high resolution profiling of gene expression within spatial contexts, yet its potential is often hindered by fragmented toolchains, intricate parameters, and cognitive bottlenecks of interpreting high dimensional data. While recent Large Language Model agents have attempted to automate this process, they remain constrained by rigid execution logic, lack multimodal feedback for self correction, and operate in epistemic isolation from established biological knowledge. Here, we present STAnalyzer, an intelligent multiagent framework designed to automate the end to end analytical lifecycle from raw data processing to biological hypothesis generation. Transcending traditional pipelines, STAnalyzer employs a collaborative intelligence architecture to achieve three core capabilities: (1) Intent Driven Orchestration, which dynamically translates natural language queries into rigorous bioinformatics workflows; (2) Multi Modal Self Refinement, which autonomously ensures analytical robustness through closed loop synthesis of evidence from visual patterns and statistical metrics; and (3) Evidence based Cross Validation, which bridges the gap between data driven correlations and biological causation by anchoring findings in ground truth literature and structured databases. By eliminating manual analytical bottlenecks and ensuring rigorous evidentiary traceability and transparency, STAnalyzer makes high resolution spatial omics more accessible to a broader research community. It provides a robust and scalable framework for cross platform automated analysis and accelerated biological discovery, translating massive spatial datasets into verifiable biological insights.

---

## 论文详细总结（自动生成）

这是一份关于论文《STAnalyzer: Transparent Spatial Transcriptomics Analysis via an Agentic Architecture》的结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：空间转录组学（ST）虽然能提供高分辨率的基因表达空间信息，但其分析过程面临三大挑战：
    1.  **工具链碎片化**：分析工具繁多且缺乏统一接口。
    2.  **参数复杂性**：非专家难以调整复杂的算法参数。
    3.  **解释瓶颈**：高维数据的生物学解释依赖专家经验，且现有的自动化工具（如简单的大模型智能体）缺乏多模态反馈和深度的生物学知识验证，容易产生“幻觉”或逻辑断层。
*   **整体含义**：STAnalyzer 旨在通过一种**多智能体（Multi-Agent）协作架构**，实现从原始数据到生物学假设生成的全流程自动化、透明化和可验证化。

### 2. 方法论：核心思想与技术细节
STAnalyzer 采用协作智能架构，包含以下核心组件和能力：
*   **意图驱动编排（Intent-Driven Orchestration）**：
    *   **Orchestrator Agent**：负责解析用户的自然语言指令，将其拆解为具体的生物信息学任务。
    *   **Service Planner Agent**：利用语义匹配引擎将任务对接至具体的工具（如 CellPhoneDB、Scanpy 等），并在容器化环境中执行，具备细粒度的错误诊断与自动恢复能力。
*   **多模态自我修正（Multi-Modal Self-Refinement）**：
    *   **Data Interpretation Agent**：不仅分析统计指标（如 CSV/H5AD 数据），还通过多模态模型观察视觉模式（如聚类图、空间分布图）。它会根据预设的质量标准（如聚类是否清晰、QC 指标是否达标）给出“通过/失败”反馈，驱动流程自主优化。
*   **基于证据的交叉验证（Evidence-Based Cross-Validation）**：
    *   **Knowledge Integration Agent**：结合了 RAG（检索增强生成）技术。它从 PubMed 等文献库中提取非结构化知识，并从 KEGG 等数据库中检索结构化事实，将数据分析结果与已知的生物学因果关系进行锚定，确保结论的可追溯性。

### 3. 实验设计
*   **数据集与场景**：
    1.  **人类 DLPFC（背外侧前额叶皮层）数据集**：用于验证框架在标准空间域识别、细胞类型鉴定及功能表征方面的准确性。
    2.  **10x Xenium 人类肺癌数据集**：用于展示在高分辨率亚细胞数据下的复杂分析能力，包括免疫微环境分析和新生物学假设的生成。
*   **对比与验证**：
    *   实验重点展示了 STAnalyzer 自动生成的分析路径与已知生物学知识（如脑层结构、代谢通路分布）的高度一致性。
    *   通过与传统手动分析流程对比，强调了其在效率和降低门槛方面的优势。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**具体的 GPU 型号、数量或训练时长。由于该框架主要基于大语言模型（LLM）的 API 调用和容器化生物信息学工具执行，其核心算力消耗在于 LLM 的推理以及后端生物信息学算法的运行。

### 5. 实验数量与充分性
*   **实验规模**：论文展示了两个主要的大型案例研究（DLPFC 和 Xenium 肺癌），涵盖了从质量控制、空间聚类、差异表达分析到功能富集和知识整合的完整生命周期。
*   **充分性评价**：实验设计较为充分，不仅验证了基础的分析功能，还深入到了“新假设生成”阶段（如 Treg 介导的免疫抑制界面动态）。然而，相比于纯算法类论文，其在不同 LLM 底座（如 GPT-4 vs Claude 3.5）之间的性能对比实验较少。

### 6. 主要结论与发现
*   **自动化能力**：STAnalyzer 能够自主完成复杂的空间组学分析流，显著降低了生物学家的技术门槛。
*   **鲁棒性与透明度**：通过多模态反馈机制，系统能识别并修正分析中的异常；所有结论均附带文献来源（DOI/URL），实现了分析过程的透明和可追溯。
*   **科学发现**：在肺癌数据中，STAnalyzer 自动识别了 Treg 细胞与 T 细胞接触界面的动态信号中心，并提出了涉及 cGAS-STING 通路激活的免疫沉默新假设。

### 7. 优点
*   **闭环反馈**：引入视觉模式识别进行自我修正，比单纯依赖代码执行结果的智能体更具鲁棒性。
*   **知识锚定**：通过 RAG 技术将分析结果与权威文献交叉验证，有效缓解了大模型的“幻觉”问题。
*   **端到端透明**：提供了从意图解析到证据溯源的完整链路，符合学术研究对严谨性的要求。

### 8. 不足与局限
*   **计算成本**：频繁调用高性能 LLM API 和多模态模型可能产生较高的经济成本。
*   **依赖外部数据库**：其知识验证的质量高度依赖于所连接的文献库和数据库的实时性与覆盖范围。
*   **复杂场景适应性**：对于极度非标或前沿的实验技术（如尚未有成熟工具链的新型组学），智能体的工具匹配能力可能受限。

（完）

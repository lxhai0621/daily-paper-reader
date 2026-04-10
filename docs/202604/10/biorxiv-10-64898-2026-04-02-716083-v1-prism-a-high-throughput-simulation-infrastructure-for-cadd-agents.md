---
title: "PRISM: A High-Throughput Simulation Infrastructure for CADD Agents"
title_zh: PRISM：面向 CADD 智能体的高通量模拟基础设施
authors: "Shi, Z., Gao, X., Xu, M., Zhu, X., Wang, P., Yang, Y., Yang, Z., Zhou, R."
date: 2026-04-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.02.716083v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 专家工作流驱动的药物筛选AI智能体
tldr: PRISM是一个基于GROMACS的Python平台，旨在解决计算机辅助药物设计（CADD）中模拟工具碎片化导致的效率瓶颈。它集成了配体参数化、系统构建、增强采样及自由能估算等功能，并通过MCP协议为AI智能体提供计算基础设施。该研究展示了其在核黄素合酶上的自动化应用，成功识别了潜在的变构抑制位点，显著提升了药物筛选的通量与自动化水平。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-02-716083-v1/fig-001.webp\", \"caption\": \"Figure 1. Architecture of PRISM. The platform integrates five sequential stages: input validation, protein pre-processing (PDBFixer repair, PROPKA protonation), multi-pathway ligand parameterization (GAFF/GAFF2 via AmberTools, OpenFF via Interchange, with optional Gaussian RESP charges), standardized output generation (GRO, ITP, force field and position restraint files), and trajectory post-analysis. The right panel shows the MCP interface enabling agent-driven simulation setup.\", \"page\": 6, \"index\": 1, \"width\": 837, \"height\": 573}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-02-716083-v1/fig-002.webp\", \"caption\": \"Figure 3. Algorithm of PRISM-FEbuilder. Schematic illustration of distance-based atom mapping and charge handling strategies for FEP system construction. (Left) The mapping algorithm identifies the shared core between reference and transformed ligands using distance criteria (0.6 Å cutoff) and element type matching, classifying atoms as common (shared scaffold), transformed (state-specific), or surrounding (position-matched but parameter-divergent). (Right) Charge assignment handles electrostatic differences across the perturbation through three strategies: reference-state preservation, mutant-state preservation, or arithmetic averaging for common atoms with minor charge differences. The single-topology GROMACS format encodes state-specific parameters via typeB/chargeB columns, enabling alchemical transformations without the parameter merging overhead required in dual-topology approaches.\", \"page\": 10, \"index\": 2, \"width\": 798, \"height\": 656}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-02-716083-v1/fig-003.webp\", \"caption\": \"Figure 5. Hierarchical screening of Riboflavin Synthase inhibitors. (A) Multi-tier screening funnel: ChEMBL candidate search → chemical space selection → docking→\", \"page\": 14, \"index\": 3, \"width\": 821, \"height\": 513}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-02-716083-v1/fig-004.webp\", \"caption\": \"Figure 6. Benchmark of PRISM-FEbuilder. Relative binding free energy calculations for (A) HIF-2α, (B) T4-lysozyme L99A, and (C) p38α kinase. Left: protein structures; center: alchemical perturbation networks with cycle-closure constraints; right: calculated vs. experimental ΔΔ𝐺 scatter plots (yellow line: equation 𝑥 = 𝑦; pink band: ±1 std). RMSE values are 0.90, 0.72, and 0.77 kcal/mol with R²of 0.45, 0.54, and 0.70, respectively.\", \"page\": 18, \"index\": 4, \"width\": 832, \"height\": 702}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-02-716083-v1/fig-005.webp\", \"caption\": \"Figure 2. Automated PMF setup procedure. The pulling direction is optimized by minimizing a steric hindrance objective on the unit sphere S2 via Metropolis-Hastings sampling with simulated annealing (upper panels; initial direction in yellow, optimized in red). The complex is then rotated to align the optimal vector with the z-axis, the box is elongated, and steered MD generates a continuous unbinding trajectory from which umbrella sampling windows are extracted at uniform spacing (lower panels). WHAM reconstructs the free\", \"page\": 8, \"index\": 5, \"width\": 829, \"height\": 546}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-02-716083-v1/fig-006.webp\", \"caption\": \"Figure 4. Workflow of the CADD-Agent. A user's natural-language research intent is interpreted by an LLM guided by a predefined expert workflow (six-stage pipeline prompt encoding domain constraints and quality gates). Computational tools--ChEMBLfind, MolScope, AutoDock Vina MCP, and PRISM--are exposed as independent MCP servers, enabling the LLM to chain tool calls with human-in-the-loop confirmation at each stage.\", \"page\": 12, \"index\": 6, \"width\": 881, \"height\": 533}]"
motivation: 现有的蛋白质-配体模拟工具链碎片化严重，限制了AI智能体在药物设计中进行大规模候选药物评估的效率。
method: 开发了集成多种力场、自动化系统构建和多级结合自由能估算的PRISM平台，并利用MCP协议将其与CADD-Agent对接。
result: 在核黄素合酶的试点应用中，实现了从候选库组装到结合位点表征的全流程自动化，并发现了一个潜在的变构抑制位点。
conclusion: PRISM为AI驱动的药物设计提供了高效、统一的高通量模拟基础设施，显著增强了智能体执行复杂药物筛选管线的能力。
---

## 摘要
尽管用于计算机辅助药物设计 (CADD) 的 AI 智能体取得了快速进展，但蛋白质-配体模拟工作流在不同工具之间仍然处于碎片化状态，这为可扩展的候选药物评估造成了主要瓶颈。在此，我们介绍了 PRISM（Protein-Receptor Interaction Simulation Modeler），这是一个基于 GROMACS 的 Python 平台，它在单一工作流中集成了跨多个力场的配体参数化、自动化系统构建、增强采样、多层级结合自由能估算以及轨迹分析。通过模型上下文协议 (MCP)，PRISM 进一步作为 CADD-Agent 的计算基础设施，CADD-Agent 是一种由专家工作流驱动的 AI 智能体，旨在编排层级化药物筛选流水线。作为试点应用，我们将 PRISM 应用于核黄素合成酶，并展示了从候选库组装到结合口袋表征的端到端自动化，识别出寡聚化界面上的一个潜在变构抑制位点。总之，这些结果确立了 PRISM 作为智能体赋能 CADD 的高通量模拟基础设施。

## Abstract
Despite rapid progress in AI agents for computer-aided drug design (CADD), protein-ligand simulation workflows remain fragmented across disparate tools, creating a major bottleneck for scalable candidate evaluation. Here, we present PRISM (Protein-Receptor Interaction Simulation Modeler), a Python platform built on GROMACS that unifies ligand parameterization across multiple force fields, automated system construction, enhanced sampling, multi-tier binding free energy estimation, and trajectory analysis within a single workflow. Through the Model Context Protocol (MCP), PRISM further serves as the computational infrastructure for CADD-Agent, an expert-workflow-driven AI agent designed to orchestrate hierarchical drug screening pipelines. As a pilot application, we applied PRISM to riboflavin synthase and demonstrated end-to-end automation from candidate library assembly to binding pocket characterization, identifying a potential allosteric inhibition site at the oligomerization interface. Together, these results establish PRISM as a high-throughput simulation infrastructure for agent-enabled CADD.

---

## 论文详细总结（自动生成）

以下是对论文《PRISM: A High-Throughput Simulation Infrastructure for CADD Agents》的结构化总结：

### 1. 核心问题与整体含义
*   **研究动机**：在计算机辅助药物设计（CADD）中，尽管AI智能体（Agents）发展迅速，但底层的蛋白质-配体模拟工具链（如动力学模拟、自由能计算）高度碎片化。不同工具间格式不兼容、参数化过程繁琐、手动干预多，成为限制AI智能体进行大规模、自动化候选药物评估的主要瓶颈。
*   **核心目标**：开发一个名为 **PRISM** 的统一模拟基础设施，旨在为AI智能体提供一个高通量、端到端的计算平台，实现从配体处理到复杂自由能估算的全面自动化。

### 2. 方法论
*   **核心思想**：基于 Python 构建 GROMACS 的高级封装库，通过模块化设计集成多种力场和采样算法，并利用 **MCP（Model Context Protocol）** 协议将这些能力暴露给大语言模型（LLM）驱动的智能体。
*   **关键技术细节**：
    *   **多路径参数化**：支持 GAFF/GAFF2（通过 AmberTools）、OpenFF（通过 Interchange）以及基于 Gaussian 的 RESP 电荷计算。
    *   **PRISM-PMF（自动化增强采样）**：开发了一种路径优化算法，利用 Metropolis-Hastings 采样和模拟退火技术，在单位球面上寻找位阻最小的解离路径，自动构建伞状采样（Umbrella Sampling）系统。
    *   **PRISM-FEbuilder（自由能构建器）**：采用基于距离（0.6 Å 截断值）和元素匹配的原子映射算法，支持单拓扑（Single-topology）格式，自动处理 FEP（自由能扰动）中的电荷平衡和状态转换。
    *   **CADD-Agent 集成**：通过 MCP 接口，将 PRISM 的功能（如系统构建、模拟运行、分析）转化为智能体可调用的“技能”，配合专家工作流提示词实现自动化筛选。

### 3. 实验设计
*   **基准测试（Benchmark）**：
    *   **FEP 准确性验证**：在 HIF-2α、T4-溶菌酶 L99A 和 p38α 激酶三个标准数据集上进行相对结合自由能（RBFE）计算。
    *   **对比指标**：计算值与实验值的均方根误差（RMSE）和相关系数（$R^2$）。
*   **应用场景**：
    *   **核黄素合酶（RS）抑制剂筛选**：从 ChEMBL 数据库搜索候选物，经历“分子对接 -> 分子动力学（MD）平衡 -> PMF 粗筛 -> FEP 精筛”的层级化管线。
    *   **变构位点探索**：利用 PRISM 自动表征 RS 寡聚化界面上的潜在结合口袋。

### 4. 资源与算力
*   **算力说明**：论文提到使用了 GROMACS 进行模拟，PMF 窗口通常运行 10ns，FEP 窗口运行 5ns。
*   **具体细节**：文中未明确列出总 GPU 小时数或具体的硬件集群型号（如 A100 数量），但强调了其设计目标是支持在高性能计算（HPC）环境下的高通量并发运行。

### 5. 实验数量与充分性
*   **实验规模**：
    *   完成了 3 个标准蛋白系统的 FEP 基准测试，结果显示 RMSE 均在 1.0 kcal/mol 以下（分别为 0.90, 0.72, 0.77），证明了自动化流程的可靠性。
    *   在 RS 案例中，展示了从数千个候选分子到最终识别变构位点的完整闭环。
*   **充分性评价**：实验设计较为客观，涵盖了从算法精度验证到实际药物设计管线的全流程演示。基准测试选择了领域内公认的挑战性系统，具有较强的说服力。

### 6. 主要结论与发现
*   **自动化能力**：PRISM 成功消除了 CADD 模拟中的手动操作障碍，使 AI 智能体能够独立执行复杂的物理化学计算任务。
*   **科学发现**：在核黄素合酶（RS）的研究中，PRISM 辅助识别出了一个位于蛋白质寡聚化界面的潜在变构抑制位点（Site 2），为开发新型抗生素提供了理论依据。
*   **性能表现**：PRISM 构建的 FEP 系统在预测精度上达到了专家级手动设置的水平。

### 7. 优点
*   **高度集成化**：将碎片化的工具（PDBFixer, PROPKA, AmberTools, GROMACS 等）统一在单一 Python 框架下。
*   **智能体友好**：率先引入 MCP 协议，解决了 LLM 与底层科学计算工具之间的“对话”难题。
*   **算法创新**：自动化的解离路径搜索（PMF 路径优化）显著降低了增强采样模拟的门槛。

### 8. 不足与局限
*   **力场局限**：目前主要集中在 GROMACS 兼容的力场体系，对于某些特殊金属酶或非标准氨基酸的支持可能仍需扩展。
*   **实验验证缺失**：RS 案例中的变构位点发现主要基于计算模拟，文中未提及是否进行了湿实验（如表面等离子体共振或 X 射线晶体学）的最终验证。
*   **计算成本**：虽然流程自动化了，但高精度的 FEP 计算本身依然极其耗费算力，大规模筛选时的成本控制仍是实际应用中的挑战。

（完）

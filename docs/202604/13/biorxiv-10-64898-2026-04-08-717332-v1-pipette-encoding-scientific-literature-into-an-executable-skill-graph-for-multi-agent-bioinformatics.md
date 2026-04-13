---
title: "Pipette: Encoding scientific literature into an executable Skill Graph for multi-agent bioinformatics"
title_zh: Pipette：将科学文献编码为用于多智能体生物信息学的可执行技能图谱
authors: "Gupta, C., Sharma, A."
date: 2026-04-12
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.08.717332v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 由文献衍生的技能图谱引导的多智能体框架
tldr: Pipette是一个多智能体AI框架，旨在降低生物信息学分析的专业门槛。它通过从2万多篇论文中提取知识构建“技能图谱”，引导大模型生成符合生物学逻辑的端到端工作流。该框架支持自然语言交互，在单细胞测序、药物设计等任务中表现优异，显著提升了分析的逻辑性与可重复性。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-001.webp\", \"caption\": \"Figure 8. ACMG Secondary Findings v3.2 variant filtering and classification in HG002. A) Variant filtering pipeline showing progressive reduction from 9,924 PASS variants in ACMG gene regions (chr1-22) to 101 HIGH/MODERATE impact and splice region candidates, 9 variants remaining after common variant filtering (BA1: allele frequency > 5%), and 0 confirmed Pathogenic or Likely Pathogenic variants. B) ACMG/AMP classification of the 101 candidate variants: 92 (91%) classified as Benign/Likely Benign and 9 (9%) as Variants of Uncertain Significance (VUS). C) Classification breakdown by ACMG disease category, showing Cardiovascular genes contribute the most variants (Benign and VUS), followed by Cancer and Miscellaneous categories. D) Seven known pathogenic variants spanning six ACMG SF\", \"page\": 21, \"index\": 1, \"width\": 979, \"height\": 974}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-002.webp\", \"caption\": \"Figure 2. Skill Graph: automated construction of a bioinformatics workflow knowledge graph from scientific literature. A) Overview of the Skill Graph construction pipeline. Starting from ~20,000 open-access PMC papers and 800 structured notes across 9 domains, Named Entity Recognition (NER) and Relation Extraction (RE) models were trained on PubMedBERT with IOB2 tags and cross-entropy loss, respectively. Dictionary-based tool detection using EDAM ontology and bio.tools API identified 215 tool regex patterns. Tool mentions and positions were aggregated into skill-skill edges weighted by paper count, yielding 628 raw pipeline edges. Data type validation retained edges where source outputs matched target inputs, producing 258 literature-backed edges. An additional 225 edges were inferred from type compatibility alone. B) Model performance on held-out test set. Grouped bar chart showing Precision (blue), Recall (teal), and F1 (red) for NER (overall entity recognition), RE (USES relation type), and RE (FOLLOWED_BY relation type). C) Pipeline extraction accuracy expressed as percentage\", \"page\": 7, \"index\": 2, \"width\": 979, \"height\": 966}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-003.webp\", \"caption\": \"Figure 5: Evaluation of Pipette’s differential expression analysis workflows. A) Diverging bar charts comparing DEG counts (up = positive, down = negative) at matched FDR < 0.01 between Robertson et al. 2025 (left) and the AI agent recalculated at the same threshold (right). The agent consistently over-estimates DEG counts by ~11–24%, attributable to the absence of LFC shrinkage. Colours: red = up-regulated, blue = down-regulated. B) Four-panel scatter plot showing gene-level log₂FC concordance between the AI agent's DESeq2 output and Robertson et al. 2025 (Table S2) across all four contrasts. Only paper-significant genes (FDR < 0.01, |LFC| ≥ 1) are shown. Points coloured red (up-regulated in paper) or blue (down-regulated). Dashed line = identity (y = x). Pearson r ≥ 0.976 for all contrasts, confirming near-identical fold-change estimates.\", \"page\": 14, \"index\": 3, \"width\": 979, \"height\": 475}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-004.webp\", \"caption\": \"Figure 7. De novo cyclic peptide design targeting the p53-MDM2 interaction. (A) Docking scores for 10 cyclic peptides (6-8 residues) designed to mimic the p53 Phe19-Trp23-Leu26 hotspot triad, docked into the MDM2 hydrophobic cleft (PDB 1YCR). Bars are coloured by\", \"page\": 18, \"index\": 4, \"width\": 979, \"height\": 948}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-005.webp\", \"caption\": \"Figure 4: Evaluation of Pipette to execute scRNA-seq workflows using the PBMC 68K dataset. A)\", \"page\": 13, \"index\": 5, \"width\": 971, \"height\": 498}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-006.webp\", \"caption\": \"Figure 1. Architecture of Pipette.bio, a multi-agent AI framework for autonomous bioinformatics analysis. The system comprises three layers. (Top) A conversational interface where the Copilot Agent classifies user intent – responding directly to conceptual questions or dispatching analysis requests to the pipeline with domain-aware queue routing. (Middle) A six-stage orchestrated analysis pipeline coordinated by a deterministic orchestrator. Stage 1 initializes an ephemeral workspace and restores outputs from prior conversation turns for multi-turn continuity. Stage 2 houses the Executor Agent, which operates in an iterative tool-use loop (Plan, Write Code, Execute, Observe) across bash, Python, and R, with access to a library of 91+ injectable domain knowledge modules (skills) covering RNA-seq alignment,\", \"page\": 4, \"index\": 6, \"width\": 979, \"height\": 552}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-007.webp\", \"caption\": \"Figure 3. Pipette behavioural metrics and system validation across production deployments. A) Distribution of autonomous pipeline queries across four computational domains during a two-month deployment period. Percentages reflect proportion of total query volume. B) Skill usage distribution showing the 20 most frequently invoked skills (of 48 active), coloured by analytical domain. Differential\", \"page\": 9, \"index\": 7, \"width\": 775, \"height\": 1202}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-717332-v1/fig-008.webp\", \"caption\": \"Figure 6. Molecular docking validation of imatinib into ABL1 kinase (PDB: 2HYY). A) Binding affinity rankings for the top 10 docking modes at pH 7.4 protonation state. The best-scoring pose achieved -11.8 kcal/mol (red), within the expected range from published crystal structure data. The dashed green line indicates the expected threshold (-8 kcal/mol) and the orange line marks the strong binder cutoff (-12\", \"page\": 16, \"index\": 8, \"width\": 979, \"height\": 1033}]"
motivation: 生物信息学分析对计算专业知识要求极高，且现有大模型在生成复杂多步工作流时常因缺乏领域约束而产生不连贯或无效的结果。
method: 开发了基于文献驱动技能图谱的多智能体框架，利用从两万多篇同行评审论文中提取的逻辑约束来指导AI生成生物学有效的工作流。
result: 在单细胞测序、差异表达分析及药物设计等多个领域的测试中，Pipette的表现均优于无约束的大模型，并成功执行了符合临床标准的基因变异分类。
conclusion: Pipette通过将科学文献转化为可执行的技能图谱，有效降低了复杂基因组分析的门槛，为非计算背景的实验科学家提供了可靠的研究工具。
---

## 摘要
基因组测序成本已下降了几个数量级，但数据分析仍然是一个瓶颈，主要集中在具有专业计算背景的研究人员手中。虽然大语言模型（LLM）可以生成生物信息学代码，但由于缺乏特定领域的分析约束，它们经常产生不连贯的多步工作流。在此，我们提出了 Pipette，这是一个多智能体 AI 框架，它通过自然语言交互，在源自文献的技能图谱（Skill Graph）指导下，编排端到端的生物信息学工作流。该有向边加权知识图谱是从 20,000 多篇经同行评审的出版物中提取的，它将工作流的生成约束在生物学有效的分析转换内，从而防止产生不完整或不连贯的工作流。我们利用已发表的数据集在四个生物学领域对 Pipette 进行了基准测试：外周血单核细胞和人类胰腺图谱的单细胞 RNA-seq 分析、环境压力下水稻的大体（bulk）RNA-seq 差异表达分析，以及两个基于结构的计算药物设计工作流。在与两个没有技能图谱约束的 LLM 进行的消融实验中，Pipette 在所有定量指标上都达到或超过了两个基准模型，同时能够独特地完成多步跨领域转换。我们进一步在临床基因组学任务上评估了 Pipette，它在参考人类基因组上执行了符合 ACMG/AMP 标准的变异分类。在所有案例中，Pipette 都在重现已确立的生物学和临床发现的同时，生成了完全可重复且机器可读的出处记录。通过降低执行标准基因组分析所需的计算专业知识门槛，Pipette 为实验科学家降低了从测序数据到生物学见解之间的障碍。Pipette 可在 https://pipette.bio 获取。

## Abstract
The cost of genomic sequencing has fallen by several orders of magnitude, yet data analysis remains a bottleneck concentrated among researchers with specialized computational expertise. While Large Language Models can generate bioinformatics code, they frequently produce incoherent multi-step workflows due to the absence of domain-specific analytical constraints. Here, we present Pipette, a multi-agent AI framework that orchestrates end-to-end bioinformatics workflows through natural language interaction, guided by a literature-derived Skill Graph. This directed, edge-weighted knowledge graph, extracted from over 20,000 peer-reviewed publications, constrains workflow generation to biologically valid analytical transitions, preventing incomplete or incoherent workflows. We benchmarked Pipette across four biological domains using published datasets: single-cell RNA-seq analysis of peripheral blood mononuclear cells and a human pancreas atlas, bulk RNA-seq differential expression in rice under environmental stress, and two structure-based computational drug design workflows. In ablation against two LLMs operating without Skill Graph constraints, Pipette matched or exceeded both baselines across all quantitative metrics while uniquely completing multi-step cross-domain transitions. We further evaluated Pipette on a clinical genomics task, where it executed an ACMG/AMP-compliant variant classification on a reference human genome. In all cases, Pipette recapitulated established biological and clinical findings while generating a fully reproducible, machine-readable provenance record. By reducing the computational expertise required to execute standard genomic analyses, Pipette lowers the barrier between sequencing data and biological insight for bench scientists. Pipette is available at https://pipette.bio.

---

## 论文详细总结（自动生成）

### 论文总结：Pipette —— 基于文献驱动技能图谱的生物信息学多智能体框架

#### 1. 核心问题与整体含义（研究动机和背景）
随着测序技术的发展，生物数据的生成速度远超研究人员的分析能力。传统的生物信息学分析要求研究者具备命令行操作、统计学知识及复杂工具链的编排能力，这为实验生物学家（Bench Scientists）构成了极高的门槛。虽然大语言模型（LLM）具备生成代码的能力，但在处理多步骤生物信息学任务时，常因缺乏领域特定的逻辑约束而产生“幻觉”，导致生成的工作流不连贯、数据类型不匹配或不符合科学规范。

#### 2. 论文提出的方法论
Pipette 的核心思想是**通过从海量科学文献中提取知识，构建一个“可执行的技能图谱（Skill Graph）”来约束 AI 智能体的行为**。
*   **技能图谱构建**：
    *   **数据源**：从 PubMed Central 提取了 20,000 多篇全文论文和 800 份专家笔记。
    *   **双轨提取**：利用微调后的 PubMedBERT 模型进行命名实体识别（NER）和关系提取（RE），识别工具、操作和数据类型；同时利用正则表达式和本体（EDAM）扫描方法论部分，提取工具的使用顺序。
    *   **逻辑约束**：通过“数据类型验证”过滤无效连接。只有当前一技能的输出类型与后一技能的输入类型匹配时，边才被保留。
*   **多智能体架构**：
    *   **Copilot Agent**：负责自然语言交互和意图分类。
    *   **Executor Agent**：根据技能图谱规划路径，编写并执行 Python/R/Bash 代码。
    *   **Reviewer Agent**：独立审计代码和结果，针对统计严谨性、QC 阈值等进行“同行评审”，不合格则触发重试循环。
    *   **Provenance Tracking**：自动记录软件版本、随机种子和数据流向，生成机器可读的溯源记录。

#### 3. 实验设计
论文在四个关键生物学领域进行了验证，并与未受技能图谱约束的基准模型（Claude 4.5 和 GPT 5.4）进行了对比：
*   **单细胞 RNA-seq**：使用 PBMC 68K 数据集和人类胰腺图谱，验证细胞聚类、注释和标记基因识别的准确性。
*   **Bulk RNA-seq**：分析水稻在环境压力下的差异表达（GSE295637），验证其处理复杂实验设计（多因素 GLM 模型）的能力。
*   **药物设计**：执行伊马替尼与 ABL1 激酶的分子对接，以及针对 p53-MDM2 相互作用的从头环肽设计。
*   **临床变异分析**：在 GIAB HG002 参考基因组上执行符合 ACMG/AMP 标准的变异分类。
*   **Benchmark**：以已发表的论文结果为金标准，对比指标包括 Pearson 相关系数、调整兰德指数（ARI）、灵敏度和特异性。

#### 4. 资源与算力
*   **模型微调**：使用了 PubMedBERT 进行 NER 和 RE 任务的微调，但未详细说明具体的 GPU 型号和训练时长。
*   **推理环境**：Pipette 运行在可扩展的云基础设施上，提供不同等级的计算队列：
    *   标准型：4 vCPU, 16 GB 内存。
    *   高内存型：32 vCPU, 128 GB 内存, 500 GB 磁盘（用于 Bulk RNA-seq 比对等高负载任务）。
*   **底层 LLM**：主要使用 Claude 4.5，备用模型为 GPT 5.4。

#### 5. 实验数量与充分性
论文进行了多维度的实验：
*   **覆盖面广**：涵盖了转录组学、结构生物学和临床基因组学。
*   **消融实验**：通过移除技能图谱，对比了纯 LLM 与 Pipette 的表现，证明了图谱在减少错误和提高相关性方面的必要性。
*   **真实性**：使用了生产环境中的 125 份真实报告进行错误分类统计。
*   **充分性评价**：实验设计较为客观，不仅展示了成功案例，还详细记录了 Reviewer Agent 捕获的错误类型（如 QC 阈值不足、统计校正缺失等），体现了系统的鲁棒性。

#### 6. 主要结论与发现
*   **性能优异**：Pipette 在所有任务中均能重现已发表的生物学发现，其生成的差异表达倍数（LFC）与原论文的相关性高达 0.97-0.99。
*   **逻辑严密**：技能图谱显著提升了跨领域任务的成功率，避免了纯 LLM 常见的工具链断裂问题。
*   **自我修复**：通过 Reviewer-Executor 循环，系统能自动识别并修复如“pH 值未校准”、“染色体缺失”或“非规范转录本注释”等专业错误。
*   **临床潜力**：在变异分类任务中实现了 100% 的敏感性和特异性（针对注入的致病变异）。

#### 7. 优点
*   **知识驱动**：将非结构化的文献转化为结构化的技能图谱，解决了 LLM 在专业领域“懂代码但不精通流程”的问题。
*   **自动化审计**：引入 Reviewer Agent 模拟同行评审，极大地提高了分析结果的可靠性。
*   **高可重复性**：自动生成的溯源 DAG 记录了所有计算细节，符合开放科学的要求。
*   **降低门槛**：使非计算专业的生物学家能够通过自然语言完成复杂的端到端分析。

#### 8. 不足与局限
*   **图谱时效性**：技能图谱基于静态语料库，对于最新发表的算法或工具可能存在滞后。
*   **依赖商业模型**：系统核心依赖于闭源的商业 LLM，存在供应商锁定风险及相关的成本/隐私问题。
*   **临床风险**：尽管表现优异，但 AI 生成的临床报告仍需专业医师审核，不能直接用于医疗决策。
*   **文献检索偏差**：在某些案例中，系统倾向于检索近期文献而忽略了奠基性的经典文献。

（完）

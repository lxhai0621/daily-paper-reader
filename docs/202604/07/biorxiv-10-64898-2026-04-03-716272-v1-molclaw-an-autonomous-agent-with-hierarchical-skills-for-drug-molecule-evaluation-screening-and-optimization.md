---
title: "MolClaw: An Autonomous Agent with Hierarchical Skills for Drug Molecule Evaluation, Screening, and Optimization"
title_zh: MolClaw：一种具备分层技能的自主智能体，用于药物分子评估、筛选与优化
authors: "Zhang, L., Wang, L., Sun, X., Tang, W., Su, H., Qian, Y., Yang, Q., Li, Q., Tang, Z., Sun, H., Han, Y., Jiang, Y., Lou, W., Zhou, B., Wang, X., Bai, L., Xie, Z."
date: 2026-04-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.03.716272v1.full.pdf"
tags: ["query:ma-kf"]
score: 10.0
evidence: 具有分层技能的药物发现自主智能体
tldr: MolClaw是一个专为药物分子评估、筛选和优化设计的自主智能体。它通过三层分级技能架构（包含工具级、工作流级和学科级共70项技能）整合了30多个专业领域资源，解决了AI在复杂药物研发流程中编排能力不足的问题。此外，研究者还推出了MolBench基准测试。实验表明，MolClaw在多项任务中达到SOTA水平，尤其在处理长序列、高复杂度的结构化工作流时表现卓越。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-001.webp\", \"caption\": \"Figure 5: Ablation studies and in-depth statistical analyses reveal the mechanistic basis of MolClaw’s superiority. (A–C) Ablation on Claude Code and OpenClaw platforms: accuracy metrics (A), docking hit count (B), optimization delta (C). Largest skill-driven gain: binding affinity +29.7 pp (P = 0.013, h = 0.64). (D) Rank trajectory across four tasks for top six methods. (E) Average rank (Friedman χ2 = 35.35, P = 2.17 × 10−4); MolClaw-CC best at 1.5. (F–I) Cohen’s h effect sizes for MolClaw-CC vs. each baseline. Dashed lines: small/medium/large thresholds. (J–M) Pairwise Fisher’s exact test matrices for all 13 methods. ∗P < 0.05; ∗∗P < 0.01; ∗∗∗P < 0.001.\", \"page\": 11, \"index\": 1, \"width\": 822, \"height\": 1162}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-002.webp\", \"caption\": \"Figure 7: QED-driven iterative optimization of a triazolo-benzodiazepine scaffold by the AI agent. (A) Multi-dimensional property trajectory across five optimization rounds: QED score (target ≥ 0.70), MW, ALogP, Tanimoto similarity (constraint ≥ 0.40), TPSA and rotatable bonds. (B) QED desirability decomposition by component and round (R0–R5). (C) QED–Tanimoto trade-off for all 182 molecules; red stars, selected best per round; green quadrant, feasible region. (D) ADMET profile evolution (top: risk endpoints; bottom: benefit endpoints). (E) Generation efficiency: molecules requested, generated and qualifying per round (left); yield and qualification rates (right). (F) QED component contribution waterfall (R0 → R4). (G) Radar chart comparing R0 and R4 desirability profiles. (H) Cumulative QED gain (left) and marginal gain per round (right). QED and Tanimoto computed via RDKit (Morgan fingerprint, radius = 2, 2,048 bits); ADMET by ADMET-AI; n = 182 molecules (54 + 28 + 44 + 23 + 33).\", \"page\": 15, \"index\": 2, \"width\": 832, \"height\": 1175}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-003.webp\", \"caption\": \"Figure 4: Statistical validation confirms the significance and reliability of MolClaw’s performance advantages. (A) Normalized performance heatmap across seven metrics for 13 methods. MolClaw variants highlighted by red borders. (B–E) Wilson score 95% CI forest plots for binding affinity accuracy (B), molecule editing accuracy (C), optimization success rate (D), and property filtering accuracy (E). (F–I) Category-level box-and-strip plots comparing LLMs (n = 8), vanilla agents (n = 2), and MolClaw (n = 2). ∗P < 0.05, Mann–Whitney U . (J) Waterfall chart of MolClaw-CC improvement over best non-MolClaw baseline per metric.\", \"page\": 10, \"index\": 3, \"width\": 798, \"height\": 1162}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-004.webp\", \"caption\": \"Figure 8: Comprehensive evaluation of AI-agent-driven iterative lead optimization of Erlotinib targeting the EGFR kinase domain. (A) Optimization trajectory showing best QuickVina docking score per round; blue dashed line: Erlotinib baseline (−6.9 kcal/mol); red dashed line: −8.9 kcal/mol target. (B) Docking score distributions across Rounds 1–6 (box-and-strip plot, n = 54). (C) Tanimoto similarity heatmap between round-best molecules. (D) Druglikeness radar plot comparing Erlotinib with two target-met derivatives. (E) Agent performance audit against sevencriterion rubric (100/100). (F) Molecule generation sources per round (left) and convergence curve (right). (G) Atompair contact counts (< 4.0 Å) across 15 binding-site residues. (H) Contact frequency by interaction type across round-best poses. (I) Interaction evolution for six key residues across rounds. (J) Protein–ligand interaction fingerprint heatmap for all seven round-best poses.\", \"page\": 18, \"index\": 4, \"width\": 760, \"height\": 1163}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-005.webp\", \"caption\": \"Figure 6: Coarse-grained conformational sampling of the EGFR kinase domain by OpenAWSEM and GoCa. (A) Superposition of 10 PULCHRA-reconstructed all-atom conformations from the OpenAWSEM ensemble, aligned to the 1M17 crystal structure. (B) Corresponding superposition for the GoCa ensemble. (C) Cα-RMSD to native structure: GoCa 4.54 ± 0.93 Å versus AWSEM 7.78 ± 1.53 Å (P = 7.69 × 10−4). (D) Radius of gyration: GoCa Rg = 23.77 ± 0.65 Å, AWSEM Rg = 19.66 ± 1.18 Å, native Rg = 22.2 Å (dashed line; P = 1.83 × 10−4). (E) Pairwise Cα-RMSD within each ensemble (n = 45 pairs): GoCa 4.28 ± 0.88 Å versus AWSEM 5.67 ± 1.60 Å (P = 2.44 × 10−5). (F) Per-residue RMSF profiles across 312 residues (Pearson r = 0.685); shaded regions denote the N-lobe β-sheet, αC-helix, and C-lobe. Violin plots show individual data points with box-and-whisker summaries; P -values from two-sided Mann–Whitney U tests; ∗∗∗P < 0.001; n = 10 conformations per method.\", \"page\": 13, \"index\": 5, \"width\": 832, \"height\": 1177}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-006.webp\", \"caption\": \"Figure 2: Agent execution traces for the three MolBench-E2E tasks. (A) E2E-Q1: coarse-grained conformational sampling. Five tool-level failures (red) were resolved via skill-governed recovery actions (orange), yielding 20 verified all-atom structures. (B) E2E-Q2: QED-driven iterative optimization. One tool fallback (F1), two constraintdriven rejections (F2–F3), and five strategy adaptations (D1–D5) were autonomously managed across five rounds, with all 19 reported values verified against source files. (C) E2E-Q3: structure-guided lead optimization of Erlotinib. Three failure categories—baseline docking crashes, persistent ProLIF errors, and generative-model collapse—were resolved via pipeline rewriting, score-only SAR, and manual analog design. Inset: optimization trajectory reaching the −8.9 kcal/mol target. Blue dashed boxes: agent decisions; purple badges: governing skill layer; green diamonds: verification checkpoints.\", \"page\": 8, \"index\": 6, \"width\": 740, \"height\": 1109}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-007.webp\", \"caption\": \"Figure 9: Schrödinger-style 2D protein–ligand interaction diagrams and 3D pose overlay. (A) Erlotinib baseline (−6.9 kcal/mol): two H-bonds (Thr766, Asp831) and eight hydrophobic contacts. (B) R1 best (−7.4): methoxy shortening + meta-Br; new Met769 H-bond (2.99 Å). (C) R2 best (−8.0): Br→F substitution; Met769 maintained. (D) R3 best (−8.3): F + OH + CH3 on aniline. (E) R4 best (−8.9, target met): 2,6-diF-4-OH aniline; four simultaneous H-bonds (Met769, Thr766, Thr830, Asp831). (F) R5 best (−8.4): three H-bonds. (G) R6 best (−8.9, target met): distinct three-H-bond network (Lys721, Thr766, Met769). (H) 3D rendering of representative poses within the EGFR ATP-binding pocket (electrostatic potential surface).\", \"page\": 19, \"index\": 7, \"width\": 822, \"height\": 1165}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-008.webp\", \"caption\": \"Table 3: Complete hierarchical skill inventory of the MolClaw agent, including skill level, name, and description.\", \"page\": 32, \"index\": 8, \"width\": 952, \"height\": 669}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-009.webp\", \"caption\": \"Figure 3: MolClaw achieves state-of-the-art performance across all MolBench evaluation dimensions. (A) Binding affinity comparison accuracy. MolClaw-CC achieves 81.1%. (B) Docking screening hit count. MolClaw-CC attains 0.80. (C) Molecule editing accuracy. MolClaw-CC reaches 100.0%. (D) Optimization success rate. (E) Property filtering accuracy. (F) Property filtering F1 score. (G) Agent systems grouped comparison across three MS sub-tasks. (H) Standalone LLMs grouped comparison. (I) Radar chart of normalized multi-dimensional performance for seven representative methods. Bars color-coded: LLMs (light blue-grey), Biomni (coral), vanilla agents (dark blue), MolClaw (red). “fail”: no valid output.\", \"page\": 9, \"index\": 9, \"width\": 810, \"height\": 1165}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-010.webp\", \"caption\": \"Figure 10: Statistical validation, source attribution, and interaction conservation analysis. (A) Docking scores of all 54 molecules by source: REINVENT4 (blue, n = 20) and agent-designed (red, n = 34). (B) Per-round mean scores ± s.e.m. tested against baseline (Wilcoxon); R1 n.s., R2–R3 ∗∗, R4–R6 ∗∗∗. (C) Early (R1–R3) vs. late (R4–R6) violin plot (p = 1.24× 10−4). (D) Agent vs. REINVENT violin plot (p = 0.104, n.s.). (E) H-bond residue count across rounds (Kruskal–Wallis p = 0.89, n.s.). (F) H-bond frequency for five key residues per round. (G) Met769 H-bond present vs. absent (p = 0.0036). (H) Forest plot of per-residue H-bond impact; only Met769 significant (p = 0.007). (I) Score vs. Tanimoto (Spearman ρ = +0.650, p < 10−7). (J) Tanimoto across rounds (ρ = −0.691, p = 7.4 × 10−9). (K) 3D rendering of R6 target-met compound in EGFR binding pocket with three-point H-bond network. n = 54 molecules; ∗∗P < 0.01; ∗∗∗P < 0.001.\", \"page\": 20, \"index\": 10, \"width\": 686, \"height\": 1163}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-03-716272-v1/fig-011.webp\", \"caption\": \"Figure 1: Technical architecture of MolClaw. The left side illustrates the construction of hierarchical skills, while the right side depicts the agent execution process and example interactions.\", \"page\": 5, \"index\": 11, \"width\": 922, \"height\": 410}]"
motivation: 针对现有AI智能体在处理涉及数十个专业工具的复杂药物研发工作流时，难以维持鲁棒性能且缺乏科学原则指导的问题。
method: 开发了具有三层分级技能架构的MolClaw智能体，通过工具标准化、工作流验证及学科原理指导来实现复杂的分子筛选与优化。
result: MolClaw在包含8至50步以上工具调用的MolBench基准测试中取得了最先进的性能，显著优于现有的AI智能体。
conclusion: 研究证明工作流编排能力是AI药物研发的关键瓶颈，而MolClaw的分级技能架构为解决这一高复杂度场景提供了有效方案。
---

## 摘要
计算药物发现，特别是药物分子筛选和优化的复杂工作流，需要在多步流程中编排数十个专业工具。然而，目前的AI智能体在这些高复杂度场景中难以保持稳健性能，且表现持续欠佳。本文提出了MolClaw，一种用于药物分子评估、筛选和优化的自主智能体。它通过三层分层技能架构（共70项技能）统一了30多个专业领域资源，旨在促进智能体在运行时的长期交互：工具级技能标准化了原子操作；工作流级技能将原子操作组合成包含质量检查与反思的验证流水线；学科级技能则提供了指导该领域所有场景下规划与验证的科学原理。此外，我们引入了MolBench基准测试，涵盖了分子筛选、优化及端到端发现挑战，涉及8到50多个连续工具调用。MolClaw在所有指标上均达到了最先进的性能。消融研究证实，性能提升主要集中在需要结构化工作流的任务中，而在可通过临时脚本解决的任务中则不明显。这表明工作流编排能力是AI驱动药物发现的主要能力瓶颈。

## Abstract
Computational drug discovery, particularly the complex workflows of drug molecule screening and optimization, requires orchestrating dozens of specialized tools in multi-step workflows, yet current AI agents struggle to maintain robust performance and consistently underperform in these high-complexity scenarios. Here we present MolClaw, an autonomous agent that leads drug molecule evaluation, screening, and optimization. It unifies over 30 specialized domain resources through a three-tier hierarchical skill architecture (70 skills in total) that facilitates agent long-term interaction at runtime: tool-level skills standardize atomic operations, workflow-level skills compose them into validated pipelines with quality check and reflection, and a discipline-level skill supplies scientific principles governing planning and verification across all scenarios in the field. Additionally, we introduce MolBench, a benchmark comprising molecular screening, optimization, and end-to-end discovery challenges spanning 8 to 50+ sequential tool calls. MolClaw achieves state-of-the-art performance across all metrics, and ablation studies confirm that gains concentrate on tasks that demand structured workflows while vanishing on those solvable with ad hoc scripting, establishing workflow orchestration competence as the primary capability bottleneck for AI-driven drug discovery.

---

## 论文详细总结（自动生成）

### MolClaw：用于药物分子评估、筛选与优化的分层技能自主智能体论文总结

#### 1. 论文的核心问题与整体含义
*   **研究动机**：早期药物研发是一个极其复杂且耗时的过程，涉及蛋白质结构预测、虚拟筛选、分子动力学模拟等多个环节。每个环节都依赖于输入输出格式各异、参数空间复杂的专业软件工具。
*   **核心问题**：现有的AI智能体（如ChemCrow、Biomni等）在处理简单的单步工具调用时表现尚可，但在面对需要编排数十个工具、跨越多个阶段的长程（Long-horizon）药物研发工作流时，往往表现出鲁棒性不足、缺乏科学严谨性以及容易产生幻觉等问题。
*   **整体含义**：本文提出了MolClaw智能体，旨在通过一种“分层技能架构”来解决AI在复杂科学工作流中的编排瓶颈，实现端到端的自主药物发现。

#### 2. 论文提出的方法论
*   **核心思想**：将药物研发的专业知识解构为三个层次的技能，将LLM从不稳定的“规划者”转变为遵循专家验证协议的“执行者”。
*   **关键技术细节（三层分层技能架构，共70项技能）**：
    *   **L1 工具级技能（58项）**：标准化原子操作（如RDKit计算、Vina对接）。规定了严格的输入输出模式和参数默认值。
    *   **L2 工作流级技能（11项）**：将L1模块组合成验证过的流水线（如虚拟筛选、迭代优化）。包含质量门控（Quality Gates）和失败恢复机制。
    *   **L3 学科级技能（1项，含25条原则）**：提供顶层科学治理。例如“报告前计数”原则（防止幻觉）、“残基编号对齐”原则（解决结构生物学中的编号混乱）。
*   **科学上下文协议（SCP）**：一种兼容MCP的工具集成基础设施，支持GPU集群调度、并发任务管理和标准化的工具访问。
*   **执行流程**：遵循“评估（Assess）→ 诊断（Diagnose）→ 设计（Design）→ 验证（Verify）”的闭环逻辑。

#### 3. 实验设计
*   **数据集与场景（MolBench 基准测试）**：
    *   **MolBench-MS（分子筛选）**：属性过滤、结合亲和力比较、分子对接筛选。
    *   **MolBench-MO（分子优化）**：分子编辑、理化性质优化。
    *   **MolBench-E2E（端到端发现）**：包含3个极具挑战性的任务（如EGFR激酶域的构象采样、QED驱动的迭代优化、厄洛替尼的结构导向先导化合物优化），涉及8到50步以上的工具调用。
*   **对比方法**：
    *   **前沿LLM**：GPT-4o/5.2, Claude 3.5 Sonnet, Gemini 1.5 Pro, DeepSeek v3, Qwen 2.5等。
    *   **领域智能体**：Biomni（通用生物医学智能体）。
    *   **基准框架**：未加载MolClaw技能的Claude Code和OpenClaw。

#### 4. 资源与算力
*   **算力说明**：论文提到工具部署在“GPU加速的计算集群”上，通过SCP服务器进行调度。
*   **具体细节**：文中**未明确说明**具体的GPU型号（如A100或H100）数量以及实验的总耗时。由于MolClaw主要基于现有的预训练模型和计算工具，其核心贡献在于编排逻辑而非模型训练，因此算力消耗主要集中在推理和工具运行（如分子动力学模拟）上。

#### 5. 实验数量与充分性
*   **实验规模**：
    *   分子属性过滤：50个查询。
    *   亲和力比较：37对分子。
    *   对接筛选：25个靶点。
    *   分子编辑：39个任务。
    *   端到端任务：3组深度案例研究。
*   **充分性与公平性**：实验设计较为全面，涵盖了从简单脚本任务到复杂科学决策的梯度。通过在两个不同的智能体平台（Claude Code和OpenClaw）上进行消融实验，证明了MolClaw的性能提升源于“技能架构”而非特定的底层模型，具有较强的客观性和说服力。

#### 6. 论文的主要结论与发现
*   **性能卓越**：MolClaw在MolBench的所有维度上均达到SOTA，尤其在结合亲和力准确率和分子对接命中数上显著优于基准。
*   **瓶颈识别**：消融研究发现，对于简单的脚本任务（如属性过滤），技能架构提升有限；但对于需要结构化编排的任务，技能架构是性能跨越的关键。这证实了**工作流编排能力**是AI驱动药物发现的主要瓶颈。
*   **鲁棒性**：MolClaw能够自主处理工具运行中的错误（如残基编号不匹配、工具崩溃），通过L2/L3层的规则实现自我修复。

#### 7. 优点
*   **架构创新**：首次提出三层分层技能体系，将模糊的科学原则转化为可执行的约束。
*   **解决幻觉**：通过“报告前计数”和“三级自审计”机制，从制度上杜绝了智能体伪造实验数据的可能。
*   **模型无关性**：设计具有通用性，可以适配不同的底层大模型和运行环境。
*   **基准贡献**：MolBench填补了药物发现智能体缺乏长程、多步骤评估基准的空白。

#### 8. 不足与局限
*   **静态技能限制**：目前的技能层是静态的，智能体无法从过去的失败中自动学习并进化出新技能。
*   **注意力偏差**：在E2E实验中发现，智能体有时会过度关注初始有问题的指标，而忽视了在优化过程中逐渐恶化的其他指标（如AMES致突变性）。
*   **收敛标准**：目前的迭代停止准则主要基于启发式规则，缺乏更深层的理论保证（如贝叶斯优化的收敛性）。
*   **样本量**：端到端（E2E）任务虽然深入，但样本量（3个）相对较小，未来需扩展到更多靶点类型。

（完）

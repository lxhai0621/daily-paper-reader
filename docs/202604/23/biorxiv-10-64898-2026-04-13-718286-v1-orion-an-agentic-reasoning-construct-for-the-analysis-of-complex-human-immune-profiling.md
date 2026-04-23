---
title: "ORION: An agentic reasoning construct for the analysis of complex human immune profiling"
title_zh: ORION：一种用于复杂人类免疫图谱分析的智能体推理架构
authors: "Dayao, M. T., Kim, K., Khor, B., Jaech, A., van Opheusden, B., Bodansky, A., DeRisi, J."
date: 2026-04-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.13.718286v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自动化文献综述和知识发现的多智能体框架
tldr: ORION是一个基于大语言模型的多智能体框架，旨在解决高维免疫分析数据（如PhIP-seq）解读效率低下的问题。它集成了统计分析、机器学习和自动文献综述，能将原本需要数月的分析缩短至数小时。通过在APS-1和唐氏综合征数据集上的验证，证明了其在自动发现生物标志物和生成科学假设方面的卓越能力。
source: biorxiv
selection_source: fresh_fetch
motivation: 高维生物数据集的生成速度远超人工解读能力，导致从海量数据到生物学机制的转化成为研究瓶颈。
method: 开发了名为ORION的多智能体框架，利用具备推理能力的大模型整合统计分析、机器学习和自动化文献检索，实现端到端的数据分析。
result: ORION在两小时内复现了APS-1的经典自身抗体特征，并在唐氏综合征数据中准确识别了疾病样本并提出了新的生物学假设。
conclusion: 智能体AI系统能显著压缩复杂免疫数据的分析周期，使科学家能够从繁琐的数据处理中解脱，专注于基础生物学研究。
---

## 摘要
生成高维生物数据集的能力已经超过了对其进行解释的能力。诸如噬菌体免疫沉淀测序（PhIP-seq）等技术能够实现蛋白质组规模的抗体库图谱绘制，但将数千个富集肽段解释为机制性假设仍然是一个劳动密集型瓶颈，需要专家综合统计学、文献和领域知识。在此，我们描述了 ORION（组学推理与解释编排器），这是一个多智能体框架，利用具备推理能力的大语言模型对复杂的免疫图谱数据进行端到端分析。ORION 将统计分析、机器学习和自动化文献综述整合到一个单一的结构化工作流中，产生的结果具有可重复性和完全可追溯性。应用于已发表的 1 型自身免疫性多内分泌腺病综合征（APS-1）PhIP-seq 数据集时，ORION 在约两小时内恢复了经典的自身抗体特征，高度重现了最初需要一到两个月人工努力完成的分析。为了测试在未知数据上的假设生成能力，我们将 ORION 应用于来自唐氏综合征患者的新型 PhIP-seq 数据集，该领域目前尚不存在全蛋白质组范围的自身抗体参考。ORION 以高准确度区分了疾病样本与对照样本，确定了候选自身抗体靶点的优先级，并将其组织成涵盖免疫、肠道和神经程序的生物学连贯组，为后续实验生成了可验证的假设。这些结果表明，智能体 AI 系统可以将复杂免疫图谱数据的分析时间从数周压缩至数小时，使科学家能够将时间重新投入到基础生物学研究中。

## Abstract
The capacity to generate high-dimensional biological datasets has outpaced the ability to interpret them. Technologies such as phage immunoprecipitation and sequencing (PhIP-seq) enable proteome-scale profiling of antibody repertoires, but interpreting thousands of enriched peptides into mechanistic hypotheses remains a labor-intensive bottleneck requiring expert synthesis of statistics, literature, and domain knowledge. Here we describe ORION (Omics Reasoning & Interpretation Orchestrator), a multi-agent framework that uses reasoning-capable large language models to perform end-to-end analysis of complex immune profiling data. ORION integrates statistical analysis, machine learning, and automated literature review into a single structured workflow, producing results that are reproducible and fully traceable. Applied to a published PhIP-seq dataset from autoimmune polyendocrine syndrome type 1 (APS-1), ORION recovered the canonical autoantibody signature in approximately two hours, closely recapitulating an analysis that originally required one to two months of manual effort. To test hypothesis-generation capacity on previously unseen data, we applied ORION to a novel PhIP-seq dataset from individuals with Down syndrome, for which no proteome-wide autoantibody reference exists. ORION distinguished disease from control samples with high accuracy, prioritized candidate autoantibody targets, and organized them into biologically coherent groups spanning immune, gut, and neuronal programs, generating testable hypotheses for experimental follow-up. These results demonstrate that agentic AI systems can compress the analysis of complex immune profiling data from weeks to hours, allowing scientists to redirect their time toward the fundamental biology.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **ORION**（Omics Reasoning & Interpretation Orchestrator）的多智能体推理框架，旨在利用大语言模型（LLM）的推理能力自动化分析复杂的高维免疫组学数据。

以下是对该论文的结构化总结：

### 1. 核心问题与研究动机
*   **核心问题**：生物组学数据（如 PhIP-seq 噬菌体展示免疫沉淀测序）的生成速度远超人类专家的解读能力。
*   **研究背景**：PhIP-seq 可以检测全蛋白质组规模的抗体-抗原相互作用，但其数据具有高度个体差异性、稀疏性且非直接反映分子丰度。
*   **瓶颈**：从数千个富集的肽段信号转化为具有生物学意义的机制假设，通常需要领域专家花费数周甚至数月时间查阅文献、进行统计建模和综合分析。

### 2. 方法论：ORION 框架
ORION 是一个多智能体（Multi-agent）协作框架，其核心思想是通过“计划→执行→验证”的闭环逻辑实现端到端分析。
*   **核心智能体角色**：
    *   **主分析智能体 (Main Analysis Agent)**：负责制定分析计划、编写并运行 Python 代码进行统计处理和机器学习建模。
    *   **文献智能体 (Literature Agent)**：负责检索和总结蛋白质功能、亚细胞定位、组织表达及疾病关联等生物学背景。
    *   **监督智能体 (Supervisor Agent)**：根据预设的 9 项清单（如数据完整性、归一化合理性、结论可追溯性等）对分析结果进行审计，不合格则触发重试。
*   **关键技术细节**：
    *   **沙盒环境**：所有计算步骤在隔离的 Python 环境中执行。
    *   **数据管理**：使用 SQLite 存储中间产物和执行日志，确保分析过程可追溯、可审计。
    *   **算法流程**：包括数据清洗、基于逻辑回归（L2 正则化）和随机森林的特征筛选、蛋白质水平的聚合评分，以及最终的生物学机制建模。

### 3. 实验设计
论文通过两个主要场景验证了 ORION 的性能：
*   **基准测试 (Benchmark)**：使用已发表的 **APS-1（1 型自身免疫性多内分泌腺病综合征）** 数据集。该病有明确的自身抗体特征，以此验证 ORION 能否复现已知结论。
*   **新发现测试**：使用全新的、未公开的 **唐氏综合征 (DS)** 自身抗体数据集（105 名患者 vs 103 名健康对照）。该领域尚无全蛋白质组参考标准，用于测试 ORION 的假设生成能力。
*   **对比对象**：主要对比对象是**人类专家分析**所需的时间和结论准确度。

### 4. 资源与算力
*   **模型**：文中提到了使用 **GPT-5.2** 和 **GPT-5.2 pro**（注：这可能是论文撰写时的内部版本或特定代号）。
*   **算力说明**：文中**未明确说明**具体的 GPU 型号和数量。
*   **耗时**：APS-1 分析耗时 **2 小时 16 分钟**（人工需 1-2 个月）；唐氏综合征分析耗时 **1 小时 41 分钟**。

### 5. 实验数量与充分性
*   **实验规模**：涵盖了两个大型队列（APS-1 和 DS），涉及数十万个肽段和近两万个蛋白质。
*   **充分性**：
    *   采用了 **5 折分层交叉验证 (Stratified K-Fold)** 来评估分类器的鲁棒性。
    *   对比了“有无归一化”对结果的影响，证明了框架在处理实验伪影（如非特异性结合）方面的客观性。
    *   实验设计较为公平，特别是针对从未见过的唐氏综合征数据，展示了其泛化能力。

### 6. 主要结论与发现
*   **效率提升**：将原本需要数月的分析周期压缩至 **2 小时以内**。
*   **生物学发现**：
    *   在 APS-1 中准确找回了所有经典的自身抗体靶点（如 IL-17F, IFN-α 等）。
    *   在唐氏综合征中，ORION 识别出了一组分布式的信号，分类 AUC 达到 **0.911**，并提出了涉及免疫调节（IL17F）、肠道屏障（MGAM）和神经粘附（NTM）的三个生物学程序。
*   **可验证性**：ORION 不仅给出结论，还生成了具体的、可用于后续实验验证的假设。

### 7. 优点与亮点
*   **端到端集成**：首次将代码执行、统计分析与实时文献综述整合在智能体工作流中。
*   **高可追溯性**：通过 SQLite 记录每一步推理和计算，克服了传统 AI 分析“黑箱”的问题。
*   **伪影感知**：能够自动识别并处理 PhIP-seq 中的非特异性背景噪声（AG-bead 归一化）。

### 8. 不足与局限
*   **幻觉风险**：尽管有监督智能体，但 LLM 仍可能生成看似合理但错误的解释，结论必须经过实验验证。
*   **成本问题**：大规模队列的迭代推理和长上下文处理可能带来较高的计算成本。
*   **应用限制**：目前主要针对 PhIP-seq 优化，虽然设计上是模态无关的，但扩展到单细胞测序或转录组学仍需调整输入模式和提示词工程。
*   **依赖性**：分析质量高度依赖于底层 LLM 的推理能力和外部数据库的完备性。

（完）

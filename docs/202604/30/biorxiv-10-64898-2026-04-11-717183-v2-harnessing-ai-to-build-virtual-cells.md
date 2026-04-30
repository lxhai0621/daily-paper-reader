---
title: Harnessing AI to Build Virtual Cells
title_zh: 利用人工智能构建虚拟细胞
authors: "Cheng, X., Li, P., Guo, H., Liang, Y., Gong, J., de Vazelhes, W., Gou, C., Xie, P., Song, L., Xing, E. P."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.11.717183v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 结合AI编码智能体与多模态模型自动构建模型的自主AI系统
tldr: 本研究针对虚拟细胞模型构建中专家依赖性强、开发周期长的问题，提出了VCHarness自主AI系统。该系统通过结合AI编码代理与多模态生物基础模型，能够自动探索大规模架构空间并迭代优化扰动响应模型。实验表明，VCHarness不仅将模型开发时间从数月缩短至数天，且性能优于传统专家设计的方案，并揭示了非直观的架构规律，为构建大规模虚拟细胞世界模型提供了高效、数据驱动的新范式。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统的虚拟细胞模型构建高度依赖专家手动设计与调试，导致研发效率低下且难以规模化。
method: 开发了VCHarness自主系统，利用AI编码代理与生物基础模型自动进行模型架构搜索、训练及迭代优化。
result: 该系统在多项扰动响应基准测试中超越了专家设计的模型，并将开发周期从数月缩短至数天。
conclusion: 研究结果表明，自主AI系统可以取代手动工程来构建虚拟细胞组件，实现对细胞系统的高效、自动化探索。
---

## 摘要
虚拟细胞是细胞的世界模型：一种跨模态、跨尺度预测、模拟和编程细胞过程的计算系统。实现这一目标的一个重要途径是模拟遗传和化学扰动如何产生转录响应，这是疾病理解和药物发现的核心能力。然而，目前的方法仍然属于专家密集型，依赖于长达数月的迭代式人工模型设计、训练和调试。在此，我们提出了 VCHarness，这是一个通过将 AI 编码智能体与多模态生物基础模型相结合来构建扰动-响应模型的自主 AI 系统。该系统在极少人工干预的情况下探索庞大的架构和训练流水线空间，迭代地生成、评估和优化候选模型。在多个扰动-响应基准测试中，VCHarness 识别出的架构优于专家设计的方案，同时将开发时间从数月缩短至数天。它还发现了与性能提升相关的非直观架构模式，表明自动化搜索可以超越传统的设计策略。这些结果表明，构建虚拟细胞世界模型组件的方式正在从人工工程模型转向自主系统，从而实现对细胞系统的可扩展且数据驱动的探索。

## Abstract
A virtual cell is a world model of a cell: a computational system that predicts, simulates and programs cellular processes across modalities and scales. An important path toward this goal is to model how genetic and chemical perturbations give rise to transcriptional responses, a core capability for disease understanding and drug discovery. However, current approaches remain expert-intensive, relying on iterative manual model design, training and debugging over months. Here we present VCHarness, an autonomous AI system that constructs perturbation-response models by combining an AI coding agent with multimodal biological foundation models. The system explores large spaces of architectures and training pipelines with minimal human intervention, iteratively generating, evaluating and refining candidate models. Across multiple perturbation-response benchmarks, VCHarness identifies architectures that outperform expert-designed approaches while reducing development time from months to days. It further uncovers non-obvious architectural patterns associated with improved performance, indicating that automated search can extend beyond conventional design strategies. These results suggest a shift from manually engineered models toward autonomous systems for constructing components of virtual cell world models, enabling scalable and data-driven exploration of cellular systems.

---

## 论文详细总结（自动生成）

这是一份关于论文《Harnessing AI to Build Virtual Cells》（利用人工智能构建虚拟细胞）的结构化深度分析报告：

### 1. 论文的核心问题与整体含义
*   **研究动机**：构建“虚拟细胞”（细胞的世界模型）是生物医学领域的重大目标，旨在跨模态、跨尺度模拟细胞过程。目前，预测细胞在遗传或化学扰动下的转录响应是其核心任务。
*   **核心问题**：传统的模型开发模式高度依赖人类专家，涉及数月的手动架构设计、超参数微调和反复调试。这种“专家密集型”模式限制了模型探索的广度和开发速度，难以应对生物数据的复杂性和异构性。
*   **整体含义**：论文提出了 **VCHarness** 系统，旨在将模型构建从“人工工程”转变为“自主搜索”，通过 AI 智能体自动完成从代码编写到模型优化的全闭环流程。

### 2. 方法论：核心思想与技术细节
VCHarness 是一个端到端的自主 AI 系统，其核心思想是将模型构建视为在可执行程序空间中的搜索问题。
*   **核心组件**：
    1.  **AI 编码智能体（Coding Agent）**：基于 Claude 4.6 Sonnet，负责编写、修改和调试机器学习流水线代码。它拥有约 100 种内置技能（如集成基础模型、数据预处理、分布式训练启动等）。
    2.  **生物基础模型库（AIDO Library）**：提供预训练的生物表征能力，包括 AIDO.DNA、AIDO.Protein、AIDO.Cell 以及开源的 scGPT、Geneformer 等。
    3.  **蒙特卡洛树搜索（MCTS）**：用于在庞大的程序空间中平衡“探索”与“利用”。通过 UCB 公式 $UCB(i) = \bar{J}_i + c \sqrt{\frac{\log N}{n_i}}$ 选择最有潜力的节点进行扩展。
    4.  **结构化反馈存储**：系统会将每次运行的性能、失败日志和评估结果总结为自然语言反馈，存入共享内存，指导后续的程序生成。
*   **算法流程**：
    *   **生成与调试**：智能体根据任务描述生成代码，若运行失败则自动捕获错误并修复。
    *   **执行与评估**：在分布式 GPU 集群上训练模型，计算验证集指标。
    *   **反馈与更新**：将结果回传至 MCTS 树，更新节点统计信息，并生成经验总结以供下一轮迭代参考。

### 3. 实验设计
*   **数据集与场景**：使用了 **Essential 数据集**，聚焦于 CRISPR 敲除（Knockdown）后的差异表达基因（DEG）分类任务。
*   **实验对象**：涵盖了四种不同的细胞系：**HepG2、Jurkat、K562 和 hTERT-RPE1**。
*   **基准测试（Benchmark）**：
    *   **专家设计模型**：如 GNN Simple、TranscriptFormer。
    *   **基础模型直接微调**：包括单细胞模型（scGPT, Geneformer, scFoundation）、蛋白质模型（ESM2）、DNA 模型（AIDO.DNA）。
    *   **先验知识模型**：基于 STRING 数据库的各种图神经网络（GNN）变体。
*   **对比维度**：预测性能（Macro-F1 分数）、开发周期、架构复杂性。

### 4. 资源与算力
*   **硬件支持**：实验在分布式环境下运行，模型训练主要使用 **NVIDIA H100 GPU**。
*   **时间消耗**：
    *   单节点平均运行时间约为 **59 分钟**（其中模型训练占 35 分钟，代码生成与调试约 17 分钟）。
    *   整个开发周期从传统的**数月缩短至数天**。
*   **成本结构**：论文详细列出了单节点预算分配，包括 GPU 训练成本（约占 24%）和 LLM API 调用成本（生成、调试、反馈合计约占 68%）。

### 5. 实验数量与充分性
*   **实验规模**：系统共进行了 **1344 次** 节点尝试（即 1344 组独立的模型训练与评估实验）。
*   **充分性**：
    *   **多细胞系验证**：在四个异构数据集上均取得了一致的性能提升，证明了系统的泛化能力。
    *   **消融实验**：通过对搜索出的架构进行 motif（模体）分析，验证了不同组件（如 STRING GNN、LoRA 微调、融合策略）对最终性能的贡献。
    *   **客观性**：验证集与测试集得分呈现高度线性相关（$r$ 值较高），表明搜索过程未出现严重的过拟合，结果具有客观性。

### 6 主要结论与发现
*   **性能超越专家**：VCHarness 自动发现的模型在所有细胞系上的 Macro-F1 分数均显著优于人类专家设计的基准模型。
*   **发现非直观架构**：系统发现了一些人类难以预见的模式，例如：在 hTERT-RPE1 任务中，**部分微调（Partial Fine-tuning）** 优于全量微调；在 HepG2 中，**ESM2 蛋白质特征与 STRING GNN 的门控融合** 效果最佳。
*   **搜索效率**：MCTS 引导的搜索轨迹显示出明显的“初期快速提升、后期稳步精炼”的特征，证明了搜索算法的有效性。

### 7. 优点与亮点
*   **全流程自动化**：不仅搜索超参数，还搜索数据处理逻辑、模型拓扑结构和损失函数，实现了真正的“代码级”搜索。
*   **生物先验与数据驱动结合**：成功将大规模生物基础模型作为“积木”，通过 AI 智能体进行逻辑组装。
*   **闭环纠错**：具备自动调试（Self-debugging）能力，极大地降低了自动化流水线的中断率。

### 8. 不足与局限
*   **任务范围有限**：目前主要集中在静态的 DEG 分类任务，尚未扩展到时间序列预测、多模态响应或细胞间相互作用等更复杂的虚拟细胞场景。
*   **计算成本**：虽然缩短了人力时间，但大规模搜索对 GPU 资源和高级 LLM API 的消耗依然较高。
*   **经验复用不足**：目前的系统在不同任务间（如从一个细胞系到另一个细胞系）的知识迁移主要依赖简单的总结，缺乏更深层次的跨任务学习机制。
*   **可解释性挑战**：自动生成的复杂架构（如多层嵌套的融合机制）虽然性能高，但其背后的生物学意义有时难以直观解释。

（完）

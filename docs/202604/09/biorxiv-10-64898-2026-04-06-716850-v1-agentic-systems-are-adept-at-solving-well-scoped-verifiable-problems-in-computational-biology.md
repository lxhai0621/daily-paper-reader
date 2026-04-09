---
title: "Agentic systems are adept at solving well-scoped, verifiable problems in computational biology"
title_zh: 智能体系统擅长解决计算生物学中定义明确、可验证的问题
authors: "Nair, S., Gunsalus, L., Orcutt-Jahns, B., Rossen, J., Lal, A., Donno, C. D., Celik, M. H., Fletez-Brant, K., Xie, X., Bravo, H. C., Eraslan, G."
date: 2026-04-09
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.06.716850v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 评估具有工具使用和外部资源交互能力的智能体系统
tldr: 本研究针对计算生物学数据噪声大、解释性强的特点，推出了包含100个多样化任务的基准测试CompBioBench。该基准通过合成数据和元数据脱敏技术，构建了具有唯一标准答案的挑战性问题，涵盖基因组学、单细胞分析等多个领域。评估显示，领先的智能体系统如GPT 5.4和Opus 4.6在解决复杂生物计算任务中表现出色，为衡量和指导生物领域智能体的发展提供了重要工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的计算生物学评估缺乏像数学和编程那样具有系统验证性和唯一标准答案的基准测试。
method: 提出一种基于合成数据增强和元数据混淆的新型基准构建策略，确保任务需要多步推理和工具调用且结果可客观验证。
result: "领先的智能体系统在CompBioBench上表现强劲，其中GPT 5.4和Opus 4.6的整体准确率分别达到了83%和81%。"
conclusion: 智能体系统已具备解决定义明确且可验证的计算生物学问题的能力，CompBioBench为该领域的未来研究提供了实用的测试平台。
---

## 摘要
我们介绍了 CompBioBench，这是一个包含 100 个多样化任务的基准测试，用于评估计算生物学中的智能体系统。与更容易进行系统验证的数学和编程不同，生物数据本质上具有噪声且存在多种解释。为了在不将任务简化为规定性清单的情况下实现客观评估，我们提出了一种新的基准构建策略，该策略基于合成/增强数据以及对真实数据集进行元数据扰乱/清洗，从而创建具有单一标准答案的挑战性问题，这些问题需要多步推理、工具使用、定制代码以及与现实世界外部资源的交互。该基准涵盖了基因组学、转录组学、表观基因组学、单细胞分析、人类遗传学和机器学习工作流。问题由领域专家策划，涵盖了不同难度的广泛技能。我们从最基础的环境开始评估领先的通用智能体系统，要求它们根据需要获取数据和工具来解决每个问题。我们发现了强大的端到端性能，Codex CLI (GPT 5.4) 达到了 83% 的准确率，Claude Code (Opus 4.6) 达到了 81%。在最难的问题上，Codex CLI (GPT 5.4) 达到 59%，而 Claude Code (Opus 4.6) 达到 69%。CompBioBench 为衡量计算生物学中智能体系统的进展以及指导未来的基准设计提供了一个实用的测试平台。

## Abstract
We introduce CompBioBench, a benchmark of 100 diverse tasks for evaluating agentic systems in computational biology. Unlike mathematics and programming, which more readily admit systematic verification, biological data are inherently noisy and open to interpretation. To enable objective evaluation without reducing tasks to prescriptive checklists, we propose a new benchmark construction strategy based on synthetic/augmented data and metadata scrambling/scrubbing of real datasets to create challenging problems with a single ground-truth answer that require multi-step reasoning, tool use, bespoke code, and interaction with real-world external resources. The benchmark spans genomics, transcriptomics, epigenomics, single-cell analysis, human genetics, and machine learning workflows. Questions are curated by domain experts to cover a broad range of skills with varying difficulty. We evaluate leading general-purpose agentic systems starting from a bare-minimum environment, requiring them to fetch data and tools as needed to solve each problem. We find strong end-to-end performance, with Codex CLI (GPT 5.4) reaching 83% accuracy and Claude Code (Opus 4.6) reaching 81%. On the hardest questions, Codex CLI (GPT 5.4) reaches 59%, while Claude Code (Opus 4.6) reaches 69%. CompBioBench provides a practical testbed for measuring the progress of agentic systems in computational biology and for guiding future benchmark design.

---

## 论文详细总结（自动生成）

以下是对论文《Agentic systems are adept at solving well-scoped, verifiable problems in computational biology》的结构化总结：

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：现有的计算生物学 AI 评估缺乏像数学或编程领域那样具有“系统验证性”和“唯一标准答案”的基准测试。
*   **研究背景**：生物数据本质上具有高噪声和多重解释性，导致很难客观评估 AI 智能体（Agents）在处理复杂生物信息学任务时的真实能力。
*   **整体含义**：本文旨在填补这一空白，通过构建一个高质量、难泄露、可客观验证的基准测试 **CompBioBench**，评估领先的 AI 智能体在解决实际计算生物学问题时的端到端表现。

### 2. 论文提出的方法论
*   **核心思想**：采用“合成数据增强”与“元数据混淆”策略，确保任务既具有挑战性，又拥有唯一的客观标准答案（Ground-truth），从而避免评估过程中的主观性。
*   **关键技术细节**：
    *   **数据脱敏与混淆**：对真实数据集的元数据（如样本名称、基因 ID 等）进行扰乱或清洗，防止模型通过记忆训练数据直接“背出”答案。
    *   **合成数据生成**：利用算法生成具有特定生物学特征的合成序列或矩阵，确保答案的确定性。
    *   **任务设计**：涵盖基因组学、转录组学、表观基因组学、单细胞分析、人类遗传学和机器学习工作流。
    *   **自主环境**：智能体从一个极简的计算环境开始，必须自主决定需要哪些外部资源（如 NCBI、Ensembl）、安装哪些生物信息学工具并编写定制代码。

### 3. 实验设计
*   **基准测试（Benchmark）**：**CompBioBench**，包含 100 个由领域专家策划的多样化任务。
*   **评估场景**：要求智能体执行多步推理、调用外部工具、处理真实/合成数据并返回最终数值或分类结果。
*   **对比方法**：主要评估了当前最领先的通用智能体系统，包括：
    *   **Codex CLI (基于 GPT 5.4)**
    *   **Claude Code (基于 Opus 4.6)**
*   **难度分级**：任务根据所需技能和推理步骤分为不同难度等级。

### 4. 资源与算力
*   **算力说明**：论文主要侧重于对现有大模型（LLM）驱动的智能体进行**推理评估**，而非从头训练模型。
*   **具体细节**：文中未明确提及训练这些底层模型（如 GPT 5.4 或 Opus 4.6）所消耗的具体 GPU 型号、数量或时长，因为这些属于模型开发商（OpenAI, Anthropic）的内部信息。实验主要记录了智能体在解决 100 个任务时的成功率和调用成本。

### 5. 实验数量与充分性
*   **实验规模**：共 100 个独立任务，每个任务都经过专家审核以确保科学准确性和可验证性。
*   **充分性与公平性**：
    *   实验覆盖了计算生物学的六大主流子领域，具有较好的代表性。
    *   通过元数据混淆有效降低了“数据泄露”风险，确保了评估的客观性。
    *   对比了当前最顶尖的两大模型家族，实验结果具有较高的时效性和参考价值。

### 6. 论文的主要结论与发现
*   **智能体表现强劲**：领先的智能体系统在解决定义明确的计算生物学问题上表现出色。GPT 5.4 (Codex CLI) 总体准确率达到 **83%**，Claude 4.6 (Claude Code) 达到 **81%**。
*   **高难度任务仍具挑战**：在最困难的任务中，GPT 5.4 的准确率下降至 **59%**，而 Claude 4.6 表现稍好，达到 **69%**。
*   **自主性验证**：实验证明，当前的智能体已经具备了自主配置生物信息学环境、检索数据库和编写复杂分析脚本的能力。

### 7. 优点
*   **客观验证性**：通过合成数据和混淆技术解决了生物学任务答案模糊的痛点。
*   **端到端评估**：不只是评估代码编写，而是评估从获取数据、安装工具到得出结论的全流程能力。
*   **领域覆盖广**：任务设计紧贴科研实战，涵盖了从基础序列分析到复杂单细胞 ML 工作流的广泛领域。

### 8. 不足与局限
*   **任务规模限制**：100 个任务虽然精炼，但对于全面覆盖极其庞大的生物信息学领域来说，样本量仍有提升空间。
*   **定义明确的局限性**：该基准专注于“定义明确、可验证”的问题，而现实中的科学发现往往涉及模糊的目标和探索性研究，这部分能力尚未被此基准完全覆盖。
*   **偏差风险**：虽然进行了元数据混淆，但模型可能仍对某些标准生物信息学流程（如特定的 R 包或 Python 库用法）存在先验偏见。

（完）

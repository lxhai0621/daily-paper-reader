---
title: "Agentic systems are adept at solving well-scoped, verifiable problems in computational biology"
title_zh: 智能体系统擅长解决计算生物学中范围明确、可验证的问题
authors: "Nair, S., Gunsalus, L., Orcutt-Jahns, B., Rossen, J., Lal, A., Donno, C. D., Celik, M. H., Fletez-Brant, K., Xie, X., Bravo, H. C., Eraslan, G."
date: 2026-05-03
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.06.716850v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 评估智能体系统和工具使用的基准
tldr: "本研究针对计算生物学数据噪声大、难以客观验证的挑战，提出了CompBioBench基准测试。该基准包含100个涵盖基因组学、转录组学等领域的任务，通过合成数据和元数据脱敏技术确保了答案的唯一性和可验证性。评估显示，领先的智能体系统（如GPT-5.4、Gemini-3.1 Pro和Claude-4.6）在处理复杂生物信息学工作流、工具调用及多步推理方面表现出色，最高准确率达83%，证明了智能体在解决定义明确的生物学问题上的巨大潜力。"
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在解决计算生物学领域因数据噪声和解释开放性而缺乏客观、可验证的智能体评估基准的问题。
method: 提出一种基于合成增强数据和元数据混淆的基准构建策略，创建具有唯一标准答案且需多步推理和工具使用的复杂任务。
result: "领先的智能体系统在CompBioBench上表现强劲，其中Codex CLI (GPT 5.4) 达到了83%的端到端准确率。"
conclusion: 智能体系统已具备解决计算生物学中定义明确、可验证问题的能力，CompBioBench为衡量该领域进展提供了实用工具。
---

## 摘要
我们介绍了 CompBioBench，这是一个包含 100 个多样化任务的基准测试，用于评估计算生物学中的智能体系统。与更容易进行系统验证的数学和编程不同，生物数据本质上具有噪声且存在多种解释。为了在不将任务简化为指令性清单的情况下实现客观评估，我们提出了一种新的基准构建策略，该策略基于合成/增强数据以及对真实数据集的元数据扰乱/清洗，从而创建具有唯一标准答案且需要多步推理、工具使用、定制代码以及与现实世界外部资源交互的挑战性问题。该基准涵盖了基因组学、转录组学、表观基因组学、单细胞分析、人类遗传学和机器学习工作流。问题由领域专家策划，涵盖了不同难度的广泛技能。我们从最基础的环境开始评估领先的通用智能体系统，要求它们根据需要获取数据和工具来解决每个问题。我们发现了强大的端到端性能，其中 Codex CLI (GPT 5.4) 达到 83% 的准确率，Gemini CLI (3.1 Pro) 达到 82%，Claude Code (Opus 4.6) 达到 81%，Claude Code (Opus 4.7) 达到 78%。在最难的问题上，Claude Code (Opus 4.6) 达到 69%，Codex CLI (GPT 5.4) 达到 59%，Gemini CLI (3.1 Pro) 达到 49%。CompBioBench 为衡量计算生物学中智能体系统的进展以及指导未来的基准设计提供了一个实用的测试平台。数据和公共排行榜可在 https://huggingface.co/collections/Genentech/compbiobench-v1 获取。

## Abstract
We introduce CompBioBench, a benchmark of 100 diverse tasks for evaluating agentic systems in computational biology. Unlike mathematics and programming, which more readily admit systematic verification, biological data are inherently noisy and open to interpretation. To enable objective evaluation without reducing tasks to prescriptive checklists, we propose a new benchmark construction strategy based on synthetic/augmented data and metadata scrambling/scrubbing of real datasets to create challenging problems that have a single ground-truth answer and require multi-step reasoning, tool use, bespoke code, and interaction with real-world external resources. The benchmark spans genomics, transcriptomics, epigenomics, single-cell analysis, human genetics, and machine learning workflows. Questions are curated by domain experts to cover a broad range of skills with varying difficulty. We evaluate leading general-purpose agentic systems starting from a bare-minimum environment, requiring them to fetch data and tools as needed to solve each problem. We find strong end-to-end performance, with Codex CLI (GPT 5.4) reaching 83% accuracy, Gemini CLI (3.1 Pro) reaching 82%, Claude Code (Opus 4.6) reaching 81%, and Claude Code (Opus 4.7) reaching 78%. On the hardest questions, Claude Code (Opus 4.6) reaches 69%, Codex CLI (GPT 5.4) reaches 59%, and Gemini CLI (3.1 Pro) reaches 49%. CompBioBench provides a practical testbed for measuring the progress of agentic systems in computational biology and for guiding future benchmark design. Data and a public leaderboard are available at https://huggingface.co/collections/Genentech/compbiobench-v1.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **CompBioBench** 的基准测试，旨在评估通用智能体（Agentic Systems）在计算生物学领域的实际解决问题能力。以下是对该论文的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心挑战**：计算生物学具有高度跨学科性，涉及复杂的工具链、异构的数据格式和海量的外部数据库。与数学或纯编程不同，生物数据具有天然的**噪声**和**解释开放性**，导致很难建立一个既具有挑战性又能客观验证（即有唯一标准答案）的评估基准。
*   **研究动机**：现有的生物信息学基准测试通常过于狭窄、问题描述过于具体（降低了对自主策略的需求），或者缺乏明确的真值。作者希望创建一个涵盖多领域、需要多步推理、能模拟真实科研工作流（如安装工具、查阅文档、处理原始数据）的基准。

### 2. 论文提出的方法论
*   **核心思想**：通过**合成/增强数据**和**元数据扰乱/清洗**来构建具有唯一真值的任务。
*   **关键技术策略**：
    *   **合成/增强数据**：例如，将不同物种的 RNA-seq 读取片段按特定比例混合，要求智能体识别污染物种。
    *   **元数据恢复**：例如，故意交换真实数据集中的样本标签，要求智能体通过分析数据（如 ATAC-seq 计数矩阵）检测并指出被交换的样本。
    *   **工具化与环境构建**：提供一个“极简”的计算环境，强制智能体自主执行 `conda` 安装、从 GitHub 克隆代码、处理复杂的依赖冲突（如配置 NVIDIA 库）。
    *   **外部资源交互**：鼓励智能体访问互联网、使用 REST API（如 ENCODE API）或从公共数据库（如 Zenodo、FTP）下载 TB 级数据中的特定部分。
*   **评估方式**：采用二元评估（Binary Evaluation），即智能体的最终输出必须与标准答案字符串完全匹配（允许极小的数值舍入误差）。

### 3. 实验设计
*   **数据集/场景**：包含 100 个任务，涵盖基因组学、转录组学、表观基因组学、单细胞分析、人类遗传学和机器学习工作流。
*   **对比的方法（智能体系统）**：
    *   **OpenAI**: Codex CLI (基于 GPT 5.4)。
    *   **Google**: Gemini CLI (基于 3.1 Pro)。
    *   **Anthropic**: Claude Code (包括 Haiku 4.5, Sonnet 4.6, Opus 4.6, Opus 4.7)。
*   **基准线（Baseline）**：使用非智能体模式的单次 LLM 调用（ChatGPT 5.2 和 Claude Opus 4.6），在不提供输入文件的情况下测试其纯知识储备。

### 4. 资源与算力
*   **硬件环境**：实验在 NVIDIA DGX A100 节点上运行，配置包括：
    *   8 × NVIDIA A100 (80 GB) GPU。
    *   2 × AMD EPYC 7742 64核 CPU。
    *   2 TB RAM。
*   **运行参数**：每个任务设置了 120 至 240 分钟的硬性超时限制。

### 5. 实验数量与充分性
*   **实验规模**：对 100 个任务中的每一个，领先的智能体（GPT 5.4, Gemini 3.1 Pro, Claude 4.6/4.7）均进行了 **3 次独立重复实验**，以评估性能的稳定性。
*   **充分性与公平性**：
    *   实验涵盖了从 Level 1 到 Level 5 的不同难度梯度。
    *   所有智能体均从相同的极简 Conda 环境开始，确保了评估的起点公平。
    *   通过记录 Token 消耗和运行时间，提供了成本效益分析。

### 6. 论文的主要结论与发现
*   **强劲的端到端能力**：领先智能体表现出色，Codex CLI (GPT 5.4) 准确率最高（83.3%），Gemini 3.1 Pro (82.0%) 和 Claude Opus 4.6 (81.0%) 紧随其后。
*   **难度敏感性**：随着任务难度增加，性能明显下降。在最难的任务（Level 4-5）中，Claude Opus 4.6 表现最佳（69%），显著高于其他模型。
*   **模型规模效应**：较小的模型（如 Haiku 4.5）准确率仅为 34%，证明复杂生物信息学任务需要极强的推理能力。
*   **脆弱性（Brittleness）**：失败通常不是因为能力不足，而是因为智能体在发现一个“看似合理”的初步答案后过早停止，或在复杂的长程推理中被次优策略误导。
*   **成本与效率**：Gemini 3.1 Pro 在保持高准确率的同时，平均每个任务的成本最低（0.9 美元）。

### 7. 优点
*   **任务设计巧妙**：通过元数据扰乱等手段解决了生物学评价主观性的难题，确保了评估的客观性。
*   **真实感强**：不提供预装工具，真实模拟了生物信息学家在处理“长尾”专业工具和过时代码库时的困境。
*   **多维评估**：不仅关注准确率，还深入分析了时间、成本、技能分布和推理路径。

### 8. 不足与局限
*   **领域覆盖偏差**：任务主要受限于贡献者的专业知识，未能覆盖计算生物学的所有子领域。
*   **缺乏人类对比**：由于任务耗时极长（部分任务专家需数小时），未收集系统的人类表现数据作为对照。
*   **外部依赖风险**：部分任务依赖外部 FTP 或 Web 资源，若这些资源失效，基准测试的某些题目将无法运行。
*   **评估单一**：仅采用字符串精确匹配，不记录中间步骤的“部分学分”，可能低估了智能体在复杂探索中的价值。

（完）

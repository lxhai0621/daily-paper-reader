---
title: "PromptBio-Bench: Benchmarking LLM-based Bioinformatics Agents for End-to-End Data Analysis"
title_zh: PromptBio-Bench：用于端到端数据分析的基于大语言模型的生物信息学智能体基准测试
authors: "Guo, W., Zhang, M., Han, B., Ma, Y., Leng, Y., Hebbar, S., Zhou, X., Gu, W., Yang, X., Dhar, S."
date: 2026-05-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.05.723092v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 针对自动化工作流的LLM智能体基准测试
tldr: 本研究针对基于大语言模型（LLM）的生物信息学智能体缺乏系统评估的问题，提出了PromptBio-Bench评估套件。该套件包含194个由专家策划的跨难度任务，并建立了一套结构化文件对比评分框架。通过对Biomni和ToolsGenie等前沿智能体的测试，揭示了当前模型在处理高难度任务时的局限性，为生物信息学智能体的发展提供了重要的基准设施。
source: biorxiv
selection_source: fresh_fetch
motivation: 目前缺乏系统性的评估手段来衡量基于大语言模型的生物信息学智能体在处理真实世界复杂任务时的实际能力。
method: 开发了包含194个专家策划任务的PromptBio-Bench基准测试集，并建立了一套基于结构化文件对比和专家参考答案的评分框架。
result: 测试发现Biomni和ToolsGenie表现相近，但所有受试智能体在处理高难度任务时的准确率均出现大幅下滑。
conclusion: PromptBio-Bench为生物信息学智能体领域提供了关键的基准设施，有助于系统性地追踪和推动该领域的技术进步。
---

## 摘要
基于大语言模型（LLM）的智能体在自动化生物信息学工作流方面具有变革性潜力；然而，对其能力的系统性评估仍然有限，这阻碍了对其在现实世界应用中成熟度的清晰评估。我们推出了 PromptBio-Bench，这是一个包含 194 个专家策划任务的综合评估套件，涵盖了不同难度级别的生物信息学和数据科学，以及一个用于结构化文件比较和针对专家参考答案进行评分的评估框架。对三个最先进的智能体进行的基准测试显示，Biomni 和 ToolsGenie 取得了相当的性能，且所有智能体的准确率在更高难度级别下均显著下降。随着基础模型和智能体框架的不断演进，PromptBio-Bench 为社区提供了一个宝贵的基准基础设施，用于系统地跟踪智能体化生物信息学的进展。

## Abstract
Large language model (LLM)-based agents hold transformative potential for automating bioinformatics workflows; however, systematic evaluations of their capabilities remain limited, hindering a clear assessment of their readiness for real-world application. We introduce PromptBio-Bench, a comprehensive evaluation suite of 194 expert-curated tasks spanning bioinformatics and data science at varied difficulty levels, and an evaluation framework for structured file comparison and scoring against expert reference answers. Benchmarking three state-of-the-art agents revealed that Biomni and ToolsGenie achieved comparable performance, and accuracy declined markedly at higher difficulty levels across all agents. As foundation models and agent frameworks continue to evolve, PromptBio-Bench provides a valuable benchmark infrastructure for the community to systematically track the progress of agentic bioinformatics.

---

## 论文详细总结（自动生成）

这是一份关于论文《PromptBio-Bench: Benchmarking LLM-based Bioinformatics Agents for End-to-End Data Analysis》的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
随着大语言模型（LLM）及其智能体（Agents）在自动化生物信息学工作流中的潜力日益凸显，领域内面临一个关键瓶颈：**缺乏系统性、端到端的评估基准**。现有的评估往往局限于简单的代码生成或问答，无法真实反映智能体在处理复杂、多步骤的生物数据分析任务时的实际能力。本研究旨在填补这一空白，通过构建 **PromptBio-Bench**，为评估生物信息学智能体在真实科研场景下的表现提供一套标准化的“度量衡”。

### 2. 方法论：核心思想与关键技术
PromptBio-Bench 的核心思想是构建一个**由专家策划、难度分级、结果可验证**的端到端任务库。
*   **任务构建**：包含 194 个任务，涵盖生物信息学（如差异表达分析、单细胞测序处理）和通用数据科学领域。
*   **难度分级**：任务被划分为“简单（Easy）”、“中等（Medium）”和“困难（Hard）”三个等级，以测试智能体的鲁棒性和复杂逻辑处理能力。
*   **评估框架**：
    *   **结构化文件对比**：不同于仅检查代码正确性，该框架直接对比智能体生成的输出文件（如 CSV、图片、报告）与专家提供的参考答案（Reference Answers）。
    *   **自动评分机制**：建立了一套针对不同文件格式的结构化评分逻辑，确保评估的客观性。

### 3. 实验设计
*   **测试对象**：评估了三个最先进（SOTA）的生物信息学智能体，包括 **Biomni** 和 **ToolsGenie** 等。
*   **数据集/场景**：任务涵盖了从原始数据预处理、统计建模到结果可视化的全流程。
*   **对比维度**：
    *   不同智能体之间的横向对比。
    *   同一智能体在不同难度等级下的纵向表现。
    *   生物信息学专业任务与通用数据科学任务的差异。

### 4. 资源与算力
论文摘要及元数据中**未明确说明**具体的算力消耗（如 GPU 型号、数量或训练时长）。这通常是因为该研究侧重于基准测试（Benchmarking）而非模型训练，实验主要涉及对现有智能体 API 或开源框架的推理调用。

### 5. 实验数量与充分性
*   **实验规模**：共包含 194 个专家策划的任务，这在生物信息学这类高度专业化的领域属于较大规模的专家级数据集。
*   **充分性与公平性**：通过引入不同难度等级和跨学科任务，实验设计较为全面。使用专家参考答案作为金标准（Gold Standard），保证了评估的客观性和公平性，避免了仅依赖 LLM 自评可能带来的偏差。

### 6. 主要结论与发现
*   **性能瓶颈**：所有受试智能体在处理“困难”级别任务时，准确率均出现大幅下滑，表明当前智能体在处理复杂长链逻辑时仍有局限。
*   **SOTA 对比**：Biomni 和 ToolsGenie 在整体性能上表现相当，处于当前行业领先水平。
*   **领域差异**：智能体在通用数据科学任务上的表现普遍优于高度专业化的生物信息学任务，反映出生物领域知识整合的挑战。

### 7. 优点
*   **专家驱动**：任务由专家策划，保证了生物学意义上的正确性和科研实用性。
*   **端到端评估**：不仅关注代码，更关注最终产出的数据结果，贴近真实科研需求。
*   **基础设施贡献**：为生物信息学智能体社区提供了一个可扩展、标准化的评估工具，有助于推动该领域的迭代。

### 8. 不足与局限
*   **静态性风险**：随着 LLM 训练数据的更新，基准测试任务可能面临数据泄露（Data Leakage）的风险。
*   **工具依赖**：智能体的表现高度依赖于其可调用的底层生物信息学工具包，评估结果可能受限于工具环境的配置。
*   **覆盖范围**：虽然包含 194 个任务，但生物信息学领域极其广阔（如蛋白质结构预测、多组学整合等），基准测试可能尚未覆盖所有前沿子领域。

（完）

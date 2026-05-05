---
title: Skill-Augmented Frontier Agents Nearly Saturate BixBench-Verified-50
title_zh: 技能增强的前沿智能体几乎使 BixBench-Verified-50 基准测试达到饱和
authors: "Zhang, X."
date: 2026-05-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721523v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 评估用于生物数据分析的前沿大模型智能体
tldr: "本研究评估了具备科学技能增强的前沿大模型在生物信息学基准测试 BixBench-Verified-50 上的表现。通过对 GPT-5.4、Claude Opus 4.7 和 GPT-5.5 进行测试，发现配备 bioSkills 和联网能力的 GPT-5.5 达到了 98% 的极高准确率。研究表明，在消除歧义并提供高质量专业技能支持后，当前顶尖 AI 智能体已基本能够胜任常规生物信息学分析任务，同时也指出了资源获取和问题表述对评估结果的关键影响。"
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在重新评估前沿大模型在经过人工校对的生物信息学基准测试中的真实能力，以解决此前测试中因题目歧义导致的低分问题。
method: 在 BixBench-Verified-50 基准上，对比测试了集成科学技能插件及联网功能的 GPT 和 Claude 系列模型在不同配置下的表现。
result: "具备 bioSkills 和联网能力的 GPT-5.5 达到了 98% 的准确率，而其他未联网配置的模型准确率也均超过 84%。"
conclusion: 拥有高质量专业技能增强的前沿模型已接近饱和解决生物信息学基准测试，但外部资源获取和精确的题目定义仍是确保可靠性的关键。
---

## 摘要
大语言模型 (LLM) 智能体越来越多地用于生物数据分析，但之前的基准测试结果对于它们是否已准备好进行常规生物信息学工作给出了褒贬不一的评价。最初的 BixBench 研究报告称，前沿智能体在开放式生物信息学问题上的准确率仅为 ~17-21%。随后对 BixBench-Verified-50 的整理移除或修订了歧义项，揭示了现代智能体具有更高的性能。在这里，我们使用相同的本地基准、提示结构、回答格式和评分流水线，在 50 个经过验证的问题上评估了三种前沿模型配置：不具备网络访问权限且配备 Claude Scientific Skills 的 GPT-5.4，不具备网络访问权限且配备 Claude Scientific Skills 的 Claude Opus 4.7，以及具备网络访问权限且配备 Claude Scientific Skills 和 bioSkills 的 GPT-5.5。这三种配置的准确率分别为 88.0% (44/50)、84.0% (42/50) 和 98.0% (49/50)。剩下的 GPT-5.5 错误并非明显的分析失败：该智能体正确计算了分发的 CRISPRGeneEffect.csv 数值上的 Spearman 相关性并选择了 CCND1，而只有在将更强的必需性解释为原始基因效应评分的相反符号后，才能得出参考答案。离线错误主要发生在智能体缺乏通路、生物体注释、BUSCO 或 PhyKIT 相关资源时。这些结果表明，配备高质量科学技能的前沿智能体几乎可以使经过整理的生物信息学基准测试达到饱和，同时也强调了问题措辞、评分符号约定以及对当前外部资源的访问对于可靠评估仍然至关重要。

## Abstract
Large language model (LLM) agents are increasingly used for biological data analysis, but prior benchmark results have given a mixed picture of whether they are ready for routine bioinformatics work. The original BixBench study reported only ~17-21% accuracy for frontier agents on open-answer bioinformatics questions. Subsequent curation of BixBench-Verified-50 removed or revised ambiguous items, revealing much higher performance for modern agents. Here we evaluate three frontier-model configurations on the 50 verified questions using the same local benchmark, prompt structure, answer format, and grading pipeline: GPT-5.4 with Claude Scientific Skills and no web access, Claude Opus 4.7 with Claude Scientific Skills and no web access, and GPT-5.5 with Claude Scientific Skills, bioSkills, and web access. The three configurations achieve 88.0% (44/50), 84.0% (42/50), and 98.0% (49/50) accuracy, respectively. The remaining GPT-5.5 error is not a clear analytical failure: the agent correctly computed Spearman correlations on the distributed CRISPRGeneEffect.csv values and selected CCND1, whereas the reference answer is recovered only after interpreting stronger essentiality as the opposite sign of the raw gene-effect score. Offline errors mainly occurred when agents lacked pathway, organism-annotation, BUSCO, or PhyKIT-related resources. These results show that frontier agents equipped with high-quality scientific skills can nearly saturate a curated bioinformatics benchmark, while also emphasizing that question wording, score sign conventions, and access to current external resources remain decisive for reliable evaluation.

---

## 论文详细总结（自动生成）

这是一份关于论文《Skill-Augmented Frontier Agents Nearly Saturate BixBench-Verified-50》的结构化分析报告：

### 1. 论文的核心问题与整体含义
*   **研究背景**：尽管大语言模型（LLM）在通用领域表现出色，但在生物信息学等专业科学领域的评估结果却存在矛盾。早期的 BixBench 测试显示前沿智能体的准确率仅为 17-21%，这引发了关于 AI 是否能胜任常规生物信息学工作的质疑。
*   **核心问题**：之前的低分究竟是因为模型推理能力不足，还是由于测试题目存在歧义以及模型缺乏必要的专业工具支持？
*   **整体含义**：本研究通过使用经过人工校对的基准测试集（BixBench-Verified-50）并引入“技能增强”（Skill Augmentation）机制，重新评估了顶尖 AI 智能体的极限能力，证明了在消除歧义和工具补强后，AI 已基本能够“通关”现有的生物信息学常规任务。

### 2. 论文提出的方法论
*   **核心思想**：**技能增强型智能体架构**。研究认为，单纯依靠模型参数无法解决复杂的生物信息学问题，必须为模型配备专门的科学工具集和实时信息获取能力。
*   **关键技术细节**：
    *   **技能插件集成**：引入了 `Claude Scientific Skills`（通用科学处理能力）和 `bioSkills`（专门针对生物信息学的工具库，如处理特定文件格式、调用生物数据库 API 等）。
    *   **联网能力（Web Access）**：允许智能体实时检索最新的生物学数据库、注释信息和文献。
    *   **标准化流水线**：采用统一的提示词结构（Prompt Structure）、固定的回答格式要求以及自动化的评分流水线，以减少评估过程中的随机性。

### 3. 实验设计
*   **数据集/基准（Benchmark）**：**BixBench-Verified-50**。这是对原始 BixBench 的精简与校对版，移除了有歧义的题目，保留了 50 个经过人工验证的高质量生物信息学问题。
*   **对比方法（模型配置）**：
    1.  **GPT-5.4**：配备 Claude Scientific Skills，**无**联网权限。
    2.  **Claude Opus 4.7**：配备 Claude Scientific Skills，**无**联网权限。
    3.  **GPT-5.5**：配备 Claude Scientific Skills + bioSkills，且**具备**联网权限。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**具体的训练算力（如 GPU 型号、数量或时长）。由于该研究侧重于对现成前沿模型（Frontier Models）的推理评估和插件集成，而非从头训练模型，因此算力消耗主要集中在 API 调用和推理测试上。

### 5. 实验数量与充分性
*   **实验规模**：针对 3 种不同的模型配置，在 50 个核心验证问题上进行了完整的端到端测试。
*   **充分性与客观性**：
    *   **充分性**：虽然 50 个样本在数量上看似不多，但由于这些题目经过了深度的人工校对（Verified），其评估效度远高于包含大量噪声的自动化题库。
    *   **公平性**：研究采用了相同的本地基准、提示结构和评分标准，确保了不同模型之间的横向对比是公平的。同时，通过对比“联网”与“离线”状态，清晰地展示了资源获取对结果的影响。

### 6. 主要结论与发现
*   **性能近乎饱和**：具备 bioSkills 和联网能力的 GPT-5.5 达到了 **98% (49/50)** 的惊人准确率，基本解决了该基准测试。
*   **离线性能亦有大幅提升**：即使不联网，GPT-5.4 和 Claude Opus 4.7 的准确率也分别达到了 88% 和 84%，远超早期研究报告的 ~20%。
*   **错误根源分析**：
    *   **非分析性失败**：GPT-5.5 唯一的错误并非计算错误，而是由于对数据符号（正负号）约定的理解与参考答案不一致（关于 CRISPR 基因效应评分的解释）。
    *   **资源限制**：离线模型的错误主要集中在需要特定生物体注释、通路数据或特定工具（如 BUSCO, PhyKIT）支持的任务上。

### 7. 优点
*   **纠偏贡献**：有力地反驳了“AI 无法处理生物信息学任务”的早期观点，指出了基准测试质量（歧义性）对评估结果的巨大影响。
*   **模块化增强**：展示了通过“技能插件”增强模型专业能力的有效路径，为未来科学 AI 智能体的开发提供了参考。
*   **深度分析**：不仅给出了分数，还对每一个错误进行了定性分析，区分了“逻辑失败”与“资源缺失”。

### 8. 不足与局限
*   **样本覆盖面**：50 个问题虽然高质量，但可能无法完全覆盖生物信息学的所有子领域（如复杂的蛋白质折叠模拟或超大规模基因组组装）。
*   **闭源模型依赖**：测试对象均为闭源商业模型（GPT/Claude 系列），其内部更新可能导致实验结果难以在未来完全复现。
*   **提示词敏感性**：尽管使用了统一提示词，但模型对微小措辞变化的敏感性仍可能影响在更广泛场景下的鲁棒性。

（完）

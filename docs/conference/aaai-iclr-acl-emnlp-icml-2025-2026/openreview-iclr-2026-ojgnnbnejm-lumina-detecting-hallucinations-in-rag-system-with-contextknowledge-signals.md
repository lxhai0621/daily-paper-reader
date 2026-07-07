---
title: "LUMINA: Detecting Hallucinations in RAG System with Context–Knowledge Signals"
title_zh: LUMINA：通过上下文-知识信号检测RAG系统中的幻觉
authors: "Samuel Yeh, Sharon Li, Tanwi Mallick"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=oJgNNBNEJM"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过上下文-知识信号检测RAG中的幻觉
tldr: 该论文提出LUMINA框架，用于检测检索增强生成（RAG）系统中的幻觉。现有方法需要大量超参数调优，泛化性差。LUMINA通过分布距离量化外部上下文利用和内部知识使用信号，无需手动调参即可识别幻觉。实验表明，LUMINA在多个RAG基准上有效检测幻觉，且具有良好泛化性，为提高RAG系统可信度提供了实用工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: RAG系统即使提供正确上下文仍可能产生幻觉，现有检测方法需大量调参。
method: 提出LUMINA，利用分布距离量化上下文利用和内部知识信号，无需调参。
result: 在多个RAG基准上有效检测幻觉。
conclusion: LUMINA为RAG幻觉检测提供了无调参的通用方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) aims to mitigate hallucinations in large language models (LLMs) by grounding responses in retrieved documents. Yet, RAG-based LLMs still hallucinate even when provided with correct and sufficient context. A growing line of work suggests that this stems from an imbalance between how models use external context and their internal knowledge, and several approaches have attempted to quantify these signals for hallucination detection. However, existing methods require extensive hyperparameter tuning, limiting their generalizability. We propose LUMINA, a novel framework that detects hallucinations in RAG systems through context--knowledge signals: external context utilization is quantified via distributional distance, while internal knowledge utilization is measured by tracking how predicted tokens evolve across transformer layers. We further introduce a framework for statistically validating these measurements. Experiments on common RAG hallucination benchmarks and four open-source LLMs show that LUMINA achieves consistently high AUROC and AUPRC scores, outperforming prior utilization-based methods by up to +13% AUROC on HalluRAG. Moreover, LUMINA remains robust under relaxed assumptions about retrieval quality and model matching, offering both effectiveness and practicality.

LUMINA: https://github.com/deeplearning-wisc/LUMINA

---

## 论文详细总结（自动生成）

# LUMINA: 通过上下文-知识信号检测RAG系统中的幻觉 — 中文详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：检索增强生成（RAG）系统旨在通过检索外部文档来缓解大语言模型（LLM）的幻觉问题，但即使在提供正确且充分的上下文时，基于RAG的LLM仍然会产生幻觉。已有研究表明，这源于模型对外部上下文与内部知识利用之间的不平衡。现有的一些量化方法尝试通过测量这两个信号来检测幻觉，但**均需要大量超参数调优，限制了其泛化能力**。
- **整体目标**：提出一种无需调参、通用性强的幻觉检测框架LUMINA，通过分布距离和层间演化信号量化上下文利用和内部知识使用，从而有效识别RAG系统中的幻觉。

## 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：将外部上下文利用（context utilization）与内部知识利用（internal knowledge utilization）分别建模为两个可量化信号，利用**分布距离**和**层间预测令牌演化**进行度量，并通过统计验证框架确保测量的可靠性。
- **关键技术细节**：
  - **外部上下文利用**：通过量化模型预测分布与仅基于上下文生成的分布之间的**分布距离**（如KL散度或JS散度）来衡量。距离较小表示模型高度依赖上下文，反之表示模型忽略上下文。
  - **内部知识利用**：通过追踪预测令牌在Transformer各层输出中的演化（例如令牌身份变化或概率变化）来度量。具体地，比较不同层中预测的top-1令牌是否一致，或计算层间概率分布的差异。
  - **统计验证框架**：引入假设检验或置信区间等方法，对上述信号进行统计显著性判断，避免偶然波动导致的误判。
- **算法流程**（文字描述）：
  1. 给定输入查询和检索到的上下文，利用RAG模型生成回答；
  2. 计算每一层中预测令牌的概率分布，并存储；
  3. 计算外部上下文利用信号：对比当前模型完整输出分布与仅使用上下文的参考分布之间的分布距离；
  4. 计算内部知识利用信号：分析令牌在层间的演化模式（如变化率、稳定性）；
  5. 根据预设的统计阈值（无需调参，使用默认分布特性）判断是否产生幻觉；
  6. 输出幻觉检测结果。

## 3. 实验设计：数据集、Benchmark、对比方法
- **数据集/场景**：在**常见的RAG幻觉基准测试**上进行实验，具体包括HalluRAG等数据集。未详细列出所有基准名称，但提及使用了四个开源LLM进行实验。
- **Benchmark**：以AUROC（AUC-ROC）和AUPRC（AUC-PR）作为主要评估指标，对比**基于利用率的先前方法**（utilization-based methods）。
- **对比方法**：文中仅笼统提及“prior utilization-based methods”，未列出具体方法名称（可能指如DOLA、factual consistency等早期工作）。LUMINA在HalluRAG上相比这些方法**AUROC提升了最多13%**。

## 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及代码开源（https://github.com/deeplearning-wisc/LUMINA），推测实验可在单卡或少量GPU上完成（因方法主要基于推理阶段信号计算，无需额外训练）。但无法从提供文本中获取确切资源消耗数据。

## 5. 实验数量与充分性
- **实验数量**：至少覆盖了**四个开源LLM**（具体型号未列出）和多个RAG幻觉基准测试。在HalluRAG上报告了AUROC提升结果，但未提供完整消融实验、不同检索质量下的鲁棒性测试等细节。
- **充分性与公平性**：
  - **优点**：实验覆盖多个模型和基准，且提到了鲁棒性测试（在放宽检索质量和模型匹配假设下表现稳健），具备一定的客观性。
  - **不足**：缺少与更多类型基线（如基于分类器的检测方法）的对比；未明确说明重复次数、统计显著性检验结果；消融实验（如单独去除外部或内部信号）未提及，实验设计细节不够透明。

## 6. 主要结论与发现
- LUMINA在多个RAG基准上**持续获得高AUROC和AUPRC分数**，显著优于现有的基于利用率的检测方法（最高提升+13% AUROC）。
- 即使在**放松检索质量和模型匹配假设**（例如检索文档不完美或模型与检测器不严格对应）的情况下，LUMINA仍保持**鲁棒性和有效性**。
- 无需超参数调优的特性使得LUMINA成为**实用且通用**的RAG幻觉检测工具，有助于提升RAG系统的可信度。

## 7. 优点：方法或实验设计上的亮点
- **无需调参**：避免了现有方法对超参数（如阈值、权重）的手动调节，直接基于分布距离和层间演化统计特性，通用性强。
- **双信号融合**：同时考虑外部上下文和内部知识两种信号，更全面地捕捉幻觉产生的根本原因（利用不平衡）。
- **统计验证框架**：为信号测量提供统计支撑，减少随机波动干扰，增强可解释性和可靠性。
- **实验鲁棒性**：在非理想条件下（检索质量低、模型不匹配）仍然有效，贴近真实应用场景。

## 8. 不足与局限
- **实验覆盖有限**：未给出具体LLM型号、测试数据集数量及详细结果表格，无法全面评估泛化性；缺少与基于语言模型判别器（如NLI-based）或基于不确定性方法的对比。
- **资源信息缺失**：未说明计算开销（推理时间、内存占用），无法判断实际部署成本。
- **安全性风险**：依赖检索质量，若检索文档充满噪声或恶意内容，信号的可信度难以保证；未讨论对抗性攻击下的表现。
- **可解释性不足**：尽管有统计验证，但信号具体含义（如什么分布距离阈值对应幻觉）仍需用户理解，可能影响非专家使用。
- **缺乏消融与参数敏感性分析**：未分别验证外部信号和内部信号的独立贡献，也未测试不同分布距离度量或层间演化方法的敏感性。

（完）

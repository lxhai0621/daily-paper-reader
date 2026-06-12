---
title: "SciCore-Omics: a tri-modal foundation model unifying histology, spatial transcriptomics and language for spatial biology"
title_zh: SciCore-Omics：一个统一组织学、空间转录组学和语言的三模态基础模型，用于空间生物学
authors: "Xiao, X., Li, Y., Zeng, Z., Yan, Y., Liu, Z., Xiang, Y., Ye, Z., Ying, J., Xie, L., He, F."
date: 2026-06-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.30.728937v2.full.pdf"
tags: ["query:mmkqa"]
score: 6.0
evidence: 用于知识推理的三模态基础模型
tldr: "现有基础模型通常只能成对连接组织学、组学或语言，难以联合推断分子状态和解码空间组织。SciCore-Omics是首个三模态基础模型，统一组织学图像、空间转录组学和生物语言。在151,182个空间点上三阶段渐进训练，在基因表达预测和空间域识别任务上相对最强基线提升23.6-80.9%。零样本病理分类平均准确率超越GPT-5达6.16个百分点，专家评估确认其仅H&E的分子推理能力。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有模型只能成对连接组织学、组学和语言，限制了联合推断分子状态和解释空间组织的能力。
method: "构建包含151,182个空间点的图像-基因-文本配对数据集，对SciCore-Omics进行三阶段渐进训练。"
result: "在基因表达预测和空间域识别上相对最强基线提升23.6-80.9%；零样本病理分类平均准确率超越GPT-5达6.16个百分点。"
conclusion: 三模态框架有效地桥接了组织形态与分子状态，为计算病理和组学分析提供了更通用、可解释的基础模型。
---

## 摘要
组织形态学和空间转录组学捕捉了组织生物学的互补方面，但它们之间的关系在大规模上仍然难以提取、对齐和解读。现有的基础模型通常仅成对连接组织学、组学或语言，这限制了它们共同推断分子状态、解码空间组织结构和生成基于生物学的解释的能力。在此，我们展示了SciCore-Omics，这是首个连接组织学图像、空间转录组学和生物学语言的三模态基础模型。我们构建了一个空间配对的图像-基因-文本数据集，包含跨多个组织的151,182个点，并在该数据集上对SciCore-Omics进行了三阶段渐进式训练。在基因表达预测和空间域识别方面，SciCore-Omics在任务特定指标上比最强的外部基线实现了23.6-80.9%的相对增益。它还在组织病理学分类中展示了强大的零样本泛化能力，在四个基准测试中的平均准确率上比GPT-5高出6.16个百分点。在10例乳腺癌病例中的专家评估证实了其仅基于H&E的病例级分子推理能力。总之，我们的方法表明，三模态框架可以有效弥合组织形态学和分子状态，为计算病理学和组学分析提供更通用且可解释的基础模型。

## Abstract
Histomorphology and spatial transcriptomics capture complementary aspects of tissue biology, but their relationships remain difficult to extract, align, and interpret at scale. Existing foundation models typically connect histology, omics, or language only pairwise, which limits their capacity to jointly infer molecular states, decode spatial tissue organization, and generate biologically grounded explanations. Here, we show SciCore-Omics, the first tri-modal foundation model linking histology images, spatial transcriptomics, and biological language. We constructed a spatially paired image-gene-text dataset comprising 151,182 spots across multiple tissues and performed a three-stage progressive training of SciCore-Omics on this dataset. Across gene expression prediction and spatial domain recognition, SciCore-Omics achieved 23.6-80.9% relative gains in task-specific metrics over the strongest external baselines. It further showed robust zero-shot generalization in histopathology classification, outperforming GPT-5 by 6.16 percentage points in mean accuracy across four benchmarks. Expert evaluation in 10 breast cancer cases confirmed its H&E-only case-level molecular reasoning capability. Together, our method demonstrates that a tri-modal framework can effectively bridge histomorphology and molecular state, providing a more general and interpretable foundation model for computational pathology and omics analysis.
---
title: "SciCore-Omics: a tri-modal foundation model unifying histology, spatial transcriptomics and language for spatial biology"
title_zh: SciCore-Omics：一个统一组织学、空间转录组学和语言的三模态基础模型用于空间生物学
authors: "Xiao, X., Li, Y., Zeng, Z., Yan, Y., Liu, Z., Xiang, Y., Ye, Z., Ying, J., Xie, L., He, F."
date: 2026-06-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.30.728937v2.full.pdf"
tags: ["query:mmkqa"]
score: 6.0
evidence: 三模态基础模型对齐组织学图像、空间转录组学和语言
tldr: "组织学形态与空间转录组学的关系难以提取和对齐，现有基础模型仅成对连接。本文提出首个三模态基础模型SciCore-Omics，通过构建空间配对图像-基因-文本数据集和三阶段训练，实现了组织学、分子状态与语言的联合建模。在基因表达预测和空间域识别上，相对基线提升23.6-80.9%；零样本病理分类超越GPT-5平均准确率6.16个百分点；乳腺癌案例中验证了其H&E分子推理能力。该三模态框架为计算病理学和组学分析提供了更通用可解释的基础模型。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有模型仅成对连接组织学、组学或语言，无法联合推断分子状态与组织结构。
method: "构建含151,182个空间配对点的图像-基因-文本数据集，通过三阶段渐进训练SciCore-Omics。"
result: "基因表达预测和空间域识别相对提升23.6-80.9%，零样本病理分类超越GPT-5。"
conclusion: 三模态框架有效桥接组织形态与分子状态，为计算病理学提供更通用可解释的基础模型。
---

## 摘要
组织形态学和空间转录组学捕捉了组织生物学的互补方面，但它们之间的关系在大规模上仍然难以提取、对齐和解释。现有的基础模型通常仅成对连接组织学、组学或语言，这限制了它们共同推断分子状态、解码空间组织结构和生成生物学合理解释的能力。在此，我们展示了SciCore-Omics，这是第一个连接组织学图像、空间转录组学和生物学语言的三模态基础模型。我们构建了一个包含跨多个组织151,182个点的空间配对图像-基因-文本数据集，并在该数据集上对SciCore-Omics进行了三阶段渐进训练。在基因表达预测和空间域识别方面，SciCore-Omics在任务特定指标上相比最强外部基线取得了23.6-80.9%的相对提升。它还在组织病理学分类中展现了强大的零样本泛化能力，在四个基准测试中的平均准确率上超过GPT-5 6.16个百分点。在10例乳腺癌病例中的专家评估证实了其仅依赖H&E切片的病例级分子推理能力。综上所述，我们的方法证明了三模态框架可以有效桥接组织形态学和分子状态，为计算病理学和组学分析提供了更通用和可解释的基础模型。

## Abstract
Histomorphology and spatial transcriptomics capture complementary aspects of tissue biology, but their relationships remain difficult to extract, align, and interpret at scale. Existing foundation models typically connect histology, omics, or language only pairwise, which limits their capacity to jointly infer molecular states, decode spatial tissue organization, and generate biologically grounded explanations. Here, we show SciCore-Omics, the first tri-modal foundation model linking histology images, spatial transcriptomics, and biological language. We constructed a spatially paired image-gene-text dataset comprising 151,182 spots across multiple tissues and performed a three-stage progressive training of SciCore-Omics on this dataset. Across gene expression prediction and spatial domain recognition, SciCore-Omics achieved 23.6-80.9% relative gains in task-specific metrics over the strongest external baselines. It further showed robust zero-shot generalization in histopathology classification, outperforming GPT-5 by 6.16 percentage points in mean accuracy across four benchmarks. Expert evaluation in 10 breast cancer cases confirmed its H&E-only case-level molecular reasoning capability. Together, our method demonstrates that a tri-modal framework can effectively bridge histomorphology and molecular state, providing a more general and interpretable foundation model for computational pathology and omics analysis.
---
title: "SpatialDataAgent: Autonomous Spatial Omics Data Curation at Decade Scale"
title_zh: SpatialDataAgent：十年尺度的自主空间组学数据整理
authors: "Ji, J.-H., Zou, Q., Cheng, J., She, Z., Hao, Y., Liu, W., Zhang, D., Wang, Z., Yu, J.-T., Yuan, Z."
date: 2026-05-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.27.727615v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 用于空间组学数据知识发现的自主智能体
tldr: "空间组学档案中的元数据碎片化导致大量多模态分子-组织学数据成为“暗数据”。为此提出SpatialDataAgent，一种结合模式约束证据评估与自优化标准化智能体的自主数据整理工作流。应用于十年GEO记录，识别出769对H&E-空间转录组数据集，是现有手动整理基线的6.4倍扩展；在基准窗口内高置信度配对数据集增加141%，并自动过滤组装成含2920万个点/细胞的HESRT数据湖。该方法为多模态生物医学档案的自主整理建立了蓝图。"
source: biorxiv
selection_source: fresh_fetch
motivation: 空间组学元数据碎片化导致大量可用数据成为“暗数据”，缺乏有效整理。
method: 提出SpatialDataAgent，结合模式约束证据评估与自我优化标准化智能体的自主工作流。
result: "识别769对H&E-ST数据集，是手动基线的6.4倍；高置信度配对增加141%，构建含2920万点/细胞的HESRT数据湖。"
conclusion: 为证据驱动的多模态生物医学档案自主整理建立蓝图。
---

## 摘要
空间组学档案中的碎片化元数据导致大量多模态分子-组织学数据作为“暗数据”无法访问。在此，我们提出SpatialDataAgent，一种用于自主空间组学数据整理的智能体工作流，结合了模式约束的证据评估与自我优化的标准化代理。应用于十年的GEO记录，SpatialDataAgent识别出769个配对H&E-空间转录组（ST）数据集，相较于现有手动整理的基线实现了6.4倍的规模扩展。在基准测试窗口内，该框架实现了高置信度（A类）配对数据集的141%增长，这些数据集被自动过滤并组装为HESRT（包含2920万个点/细胞的数据湖），为基于证据的多模态生物医学档案自主整理建立了蓝图。

## Abstract
Fragmented metadata in spatial omics archives has rendered large volumes of multimodal molecular-histological data inaccessible as 'dark data'. Here, we introduce SpatialDataAgent, an agentic workflow for autonomous spatial omics data curation, combining schema-constrained evidence evaluation with a self-refining standardization agent. Applied to a decade of GEO records, SpatialDataAgent identified 769 paired H&E-spatial transcriptomics (ST) datasets, representing a 6.4-fold scale expansion over existing manually curated baselines. Within the benchmarking window, the framework achieved a 141% increase in high-confidence (Class A) paired datasets, which were automatically filtered and assembled to establish HESRT (a datalake containing 29.2 million spots/cells), establishing a blueprint for evidence-grounded autonomous curation of multimodal biomedical archives.
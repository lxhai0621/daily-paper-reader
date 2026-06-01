---
title: "SpatialDataAgent: Autonomous Spatial Omics Data Curation at Decade Scale"
title_zh: SpatialDataAgent：十年尺度空间组学数据自主整理
authors: "Ji, J.-H., Zou, Q., Cheng, J., She, Z., Hao, Y., Liu, W., Zhang, D., Wang, Z., Yu, J.-T., Yuan, Z."
date: 2026-05-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.27.727615v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 自主空间组学知识发现智能体
tldr: "空间组学档案中元数据碎片化导致大量多模态分子-组织学数据成为“暗数据”。为此，提出SpatialDataAgent，一种结合模式约束证据评估与自优化标准化代理的自主数据整理工作流。应用于十年GEO数据，识别出769个配对H&E-ST数据集，是现有手动基线的6.4倍；高置信度配对数据集增加141%，并自动构建含2920万个点/细胞的HESRT数据湖，为多模态生物医学档案的自主整理奠定基础。"
source: biorxiv
selection_source: fresh_fetch
motivation: 空间组学数据元数据碎片化导致大量多模态数据难以访问，需自主整理方法。
method: 提出SpatialDataAgent，结合模式约束证据评估与自优化标准化代理的自主工作流。
result: "识别769个配对H&E-ST数据集（6.4倍提升），高置信度增加141%，构建HESRT数据湖。"
conclusion: 实现十年尺度空间组学数据自主整理，为多模态档案整理提供蓝图。
---

## 摘要
空间组学档案中的碎片化元数据使得大量多模态分子-组织学数据成为无法访问的“暗数据”。在此，我们介绍SpatialDataAgent，一种用于自主整理空间组学数据的工作流，它结合了模式约束的证据评估与自我优化的标准化代理。应用于十年间的GEO记录，SpatialDataAgent识别出769个配对H&E-空间转录组（ST）数据集，相较现有手动整理基线实现了6.4倍的规模扩展。在基准测试窗口内，该框架使高置信度（A类）配对数据集增加了141%，这些数据集经过自动过滤和组装，形成了HESRT（一个包含2920万个点/细胞的数据湖），为基于证据的多模态生物医学档案自主整理建立了蓝图。

## Abstract
Fragmented metadata in spatial omics archives has rendered large volumes of multimodal molecular-histological data inaccessible as 'dark data'. Here, we introduce SpatialDataAgent, an agentic workflow for autonomous spatial omics data curation, combining schema-constrained evidence evaluation with a self-refining standardization agent. Applied to a decade of GEO records, SpatialDataAgent identified 769 paired H&E-spatial transcriptomics (ST) datasets, representing a 6.4-fold scale expansion over existing manually curated baselines. Within the benchmarking window, the framework achieved a 141% increase in high-confidence (Class A) paired datasets, which were automatically filtered and assembled to establish HESRT (a datalake containing 29.2 million spots/cells), establishing a blueprint for evidence-grounded autonomous curation of multimodal biomedical archives.
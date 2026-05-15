---
title: "Lense: Optimizing data preprocessing in single-cell omics using LLMs"
title_zh: Lense：利用大语言模型（LLMs）优化单细胞组学数据预处理
authors: "Liu, J., Ji, Z."
date: 2026-05-11
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.07.723465v1.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 基于语言模型引导的自动化数据预处理方法
tldr: 本研究针对单细胞组学分析中默认预处理流程对多样化数据集（如空间转录组）适应性差的问题，开发了 Lense。Lense 是一种基于大语言模型（LLM）的引导方法，通过自动对比不同预处理变体生成的低维可视化图表，智能选择最优处理方案。该工具与 Seurat 深度集成，不仅简化了分析流程，还显著增强了预处理的鲁棒性，消除了繁琐的手动调优过程，为单细胞研究提供了高效的自动化支持。
source: biorxiv
selection_source: fresh_fetch
motivation: 单细胞组学分析中默认的预处理流程在处理多样化数据集时表现不佳，且手动调优过程复杂耗时。
method: 提出 Lense 方法，利用大语言模型通过比较不同预处理变体的低维可视化图表来自动选择最优流程。
result: Lense 成功集成于 Seurat 框架，实现了预处理的自动化并显著提升了在不同平台数据集上的鲁棒性。
conclusion: Lense 为单细胞组学提供了一种无需人工干预的高效预处理优化方案，极大地简化了数据分析流程。
---

## 摘要
数据预处理对于单细胞组学分析至关重要，但默认流程在多样化数据集（尤其是来自空间转录组学等新兴平台的数据）上往往表现不佳。我们介绍了 Lense，这是一种由语言模型引导的方法，通过比较可视化不同流程变体中低维表示的图表，自动选择最佳预处理方案。Lense 与 Seurat 集成，简化了分析流程并提高了预处理的鲁棒性，且无需手动调优。作者简介：刘静云是杜克大学生物统计与生物信息学系的硕士研究生。纪志成博士是杜克大学生物统计与生物信息学系的终身轨助理教授。他的研究重点是单细胞基因组学、空间基因组学和生物医学成像的人工智能与统计建模。

## Abstract
Data preprocessing is critical for single-cell omics analyses, but default pipelines often underperform on diverse datasets, especially from emerging platforms like spatial transcriptomics. We introduce Lense, a language-model-guided method that automatically selects optimal preprocessing by comparing plots that visualize low-dimensional representations across pipeline variants. Integrated with Seurat, Lense streamlines analysis and improves preprocessing robustness without requiring manual tuning.

Biographical NoteJingyun Liu is a Masters student in the Department of Biostatistics and Bioinformatics at Duke University. Dr. Zhicheng Ji is a tenure-track Assistant Professor in the Department of Biostatistics and Bioinformatics at Duke University. His research focuses on artificial intelligence and statistical modeling for single-cell genomics, spatial genomics, and biomedical imaging.
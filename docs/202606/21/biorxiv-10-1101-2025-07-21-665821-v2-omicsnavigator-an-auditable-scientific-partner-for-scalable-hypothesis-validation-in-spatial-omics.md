---
title: "OmicsNavigator: An auditable scientific partner for scalable hypothesis validation in spatial omics"
title_zh: OmicsNavigator：面向空间组学可扩展假设验证的审计式科学伙伴
authors: "Li, Y., Vakharia, N., Liang, W., Mayer, A. T., Luo, R., Trevino, A. E., Wu, Z."
date: 2026-06-14
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.21.665821v2.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 自主LLM驱动系统用于数据探索和零样本语义检索
tldr: 空间组学数据分析面临高维分子数据难以转化为可测试生物学发现的瓶颈。本文提出OmicsNavigator，一个由大语言模型驱动的自主系统，能直接推理多模态空间组学数据（视觉与分子特征），进行知识引导的空间结构注释。通过将高维数据转化为文本解释，实现零样本组织生物标志物检索和患者级疾病谱重建，并拥有基于预注册、人工审计蓝图的客观假设验证引擎。在糖尿病肾病、肾移植排斥和COVID-19肺病理数据集上的验证表明，该系统能生成基于证据、人类可读的洞察，有望加速空间生物学发现。
source: biorxiv
selection_source: fresh_fetch
motivation: 高维空间组学数据难以直接转化为可测试的生物学发现，需要自动化系统进行可审计的假设验证。
method: OmicsNavigator基于大语言模型，融合视觉与分子特征进行知识引导注释，通过文本化实现零样本检索与疾病谱重建，并采用预注册蓝图的验证引擎。
result: 在糖尿病肾病、肾移植排斥和COVID-19肺病理数据中，OmicsNavigator成功生成证据充分、人类可读的生物学洞察。
conclusion: 该系统为空间组学数据提供可扩展、可审计的假设验证方案，加速空间生物学发现进程。
---

## 摘要
将高维、空间解析的分子数据集转化为可检验的生物学发现仍然是研究中的主要瓶颈。本文提出了OmicsNavigator，一个基于自主大语言模型的系统，用于空间组学数据的端到端数据探索和假设验证。OmicsNavigator直接对空间组学数据的多模态输入（包括视觉和分子特征）进行推理，执行知识引导的空间结构注释。我们表明，通过将高维数据转化为文本解释，OmicsNavigator能够实现组织生物标志物的零样本语义检索，以及从原始组学观测中重建患者级别的疾病概况。此外，OmicsNavigator配备了一个由预先注册、人工审计蓝图控制的目标假设验证引擎。通过跨越多种病理条件（包括糖尿病肾病、肾移植排斥和COVID-19肺部病理）的数据集验证该系统，我们证明OmicsNavigator能够从空间组学数据中生成基于证据、人类可读的洞见，具有加速空间生物学发现的潜力。

## Abstract
Translating high-dimensional, spatially resolved molecular datasets into testable biological findings remains a major research bottleneck. Here, we present Omic-sNavigator, an autonomous large language model-powered system for end-to-end data exploration and hypothesis validation on spatial omics data. OmicsNaviga-tor reasons directly over the multi-modal inputs of spatial omics data, including visual and molecular signatures, to perform knowledge-guided annotation of spatial structures. We show that by transforming high-dimensional data into textual interpretations, OmicsNavigator enables zero-shot semantic retrieval of tissue biomarkers and the reconstruction of patient-level disease profiles from raw omics observations. Furthermore, OmicsNavigator features an objective hypothesis validation engine governed by pre-registered, human-audited blueprints. By validating the system across datasets spanning diverse pathological conditions including diabetic kidney disease, kidney transplant rejection, and COVID-19 pulmonary pathology, we demonstrate that OmicsNavigator generates evidence-based, human-readable insights from spatial omics data, with potential to accelerate spatial biology discoveries.
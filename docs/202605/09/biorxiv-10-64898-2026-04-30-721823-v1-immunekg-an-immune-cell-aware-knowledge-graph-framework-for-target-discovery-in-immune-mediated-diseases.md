---
title: "immuneKG: An Immune-Cell-Aware Knowledge Graph Framework for Target Discovery in Immune-Mediated Diseases"
title_zh: immuneKG：一种用于免疫介导疾病靶点发现的免疫细胞感知知识图谱框架
authors: "Ye, Y., PB-IDD Department, Pharmablock Sciences Inc.,"
date: 2026-05-05
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.30.721823v1.full.pdf"
tags: ["query:mmkqa"]
score: 8.5
evidence: 用于目标发现的多模态知识图谱
tldr: 本研究提出immuneKG，一个专注于自身免疫性疾病的多模态知识图谱框架。通过引入免疫细胞实体和四种新关系类型，并整合自身抗体、细胞因子和HLA基因型等免疫特征，该框架实现了对免疫疾病的深度机制建模。结合HeteroPNA-Attn图神经网络，immuneKG在炎症性肠病靶点预测中表现优异，为药物研发提供了可解释的决策支持。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的生物医学知识图谱在免疫介导疾病的靶点识别方面缺乏深度机制建模和转化影响力。
method: 构建包含免疫细胞实体和多模态免疫特征（如抗体、细胞因子）的知识图谱，并利用HeteroPNA-Attn图神经网络进行建模。
result: "在炎症性肠病靶点预测中，该模型在临床管线验证下达到了0.99的Hits@100评分，并成功识别出高潜力的“暗靶点”。"
conclusion: immuneKG将候选空间筛选转向开发导向的决策支持范式，为免疫疾病的药物发现提供了高效且具生物学意义的工具。
---

## 摘要
生物医学知识图谱已成为人工智能驱动药物研发的基础设施，但其在免疫介导疾病新靶点识别方面的转化影响仍然有限。在此，我们提出了 immuneKG，这是一个以自身免疫性疾病为中心的多模态知识图谱，通过对疾病节点进行具有生物学意义的特征重编程构建而成，旨在实现对免疫相关疾病的深度机制建模。immuneKG 引入了一个新的实体类别 immune_cell 以及四种原始的有向关系类型，共增加了 9,105 个现有生物医学知识图谱模式中缺失的新三元组。疾病节点被赋予了三组量化免疫稳态失衡的新模态特征集：自身抗体谱、细胞因子特征和 HLA 基因型，并辅以全身受累评分和遗传特征。该图谱包含分布在 7,287 个实体和 32 种关系类型中的超过 407,000 个训练三元组。应用于炎症性肠病（IBD）时，immuneKG 结合 HeteroPNA-Attn 图神经网络，在针对 Clarivate II 期及以上临床管线的测试中实现了 0.99 的 Hits@100，同时一种新颖性惩罚评分函数挖掘出了具有高潜力的暗靶点。该框架从传统的候选空间筛选转向以开发为导向的决策支持范式，为下游药物研发提供可操作且可解释的指导。immuneKG 项目现已在 GitHub 上公开：https://github.com/YaowenYe/immuneKG。

## Abstract
Biomedical knowledge graphs have emerged as foundational infrastructure for AI-driven drug discovery, yet their translational impact on novel target identification in immune-mediated diseases remains limited. Here we present immuneKG, a multimodal knowledge graph centred on autoimmune diseases, constructed through biologically meaningful feature reprogramming of disease nodes to enable deep mechanistic modelling of immune-related disorders. immuneKG introduces a new entity class immune_cell, and four original directed relation types, together adding 9,105 novel triples absent from all existing biomedical KG schemas. Disease nodes are endowed with three novel modal feature sets quantifying immune homeostatic imbalance: autoantibody profiles, cytokine signatures, and HLA genotypes, complemented by systemic involvement scores and genetic features. The graph encompasses over 407,000 training triples across 7,287 entities and 32 relation types. Applied to inflammatory bowel disease (IBD), immuneKG combined with a HeteroPNA-Attn graph neural network achieves a Hits@100 of 0.99 against a Clarivate Phase II+ clinical pipeline, while a novelty-penalised scoring function surfaces high-potential dark targets. The framework shifts from conventional candidate-space screening to a development-oriented decision-support paradigm, providing actionable and interpretable guidance for downstream drug discovery. The immuneKG project is publicly available now on GitHub at https://github.com/YaowenYe/immuneKG.
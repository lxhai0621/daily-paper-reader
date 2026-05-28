---
title: "IID-KG: An ontology-aligned literature-derived knowledge graph for infectious and immune-mediated diseases"
title_zh: IID-KG：面向感染性和免疫介导疾病的本体对齐文献知识图谱
authors: "PAN, F., Zhang, Y., Wang, J., Liu, M.-C., Sui, X., Yue, H., Zhang, J."
date: 2026-05-26
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.21.727015v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 基于文献构建知识图谱，集成结构化与非结构化知识
tldr: 感染和免疫介导疾病（IID）领域文献快速膨胀，亟需可扩展的知识整合方法。本研究构建了IID专用知识图谱，通过嵌套命名实体识别、本体对齐及全文关系抽取，从PubMed和PMC文章提取实体与关系。最终图谱包含约183万实体和1629万关系，并公开发布，支持疾病机制分析与药物重定位假设生成。
source: biorxiv
selection_source: fresh_fetch
motivation: 解决IID领域文献爆炸与知识整合不足的问题，实现可扩展、本体对齐的文献挖掘。
method: 集成嵌套实体识别、统一本体构建、全文关系抽取及关系消歧策略。
result: "构建的知识图谱含1,837,513个实体和16,295,390条关系，覆盖8种关系类型。"
conclusion: 该资源为IID研究提供本体对齐的文献挖掘与药物重定位支持。
---

## 摘要
感染性和免疫介导疾病（IIDs）代表了一个广泛且快速扩张的生物医学文献领域，其中可扩展的证据提取、疾病本体细化和可解释的知识整合对于生物医学发现至关重要。我们通过整合嵌套命名实体识别、本体引导的标识符分配、全文关系提取和关系解析策略，从PubMed摘要和PMC全文文章中构建了一个IID特异性生物医学知识图谱（IID KG）。一个由500篇PubMed摘要和8篇PMC全文文章组成的黄金标准语料库被手动注释，涵盖六种实体类型的嵌套生物医学实体。所得模型应用于30,128,068篇PubMed摘要和1,385,500篇IID相关PMC全文文章。从411,341个疾病术语出发，使用层次文本分类、基于大语言模型的细化、本体交叉引用和专家评审，开发了一个统一的IID本体，产生了179,657个确认的MeSH映射。最终的IID知识图谱包含约1,837,513个独特实体和16,295,390个独特关系，涵盖八种关系类型。该资源与重利用工作流一起公开发布，支持面向本体对齐的文献挖掘、疾病机制分析和针对IID研究的药物重利用假设生成。

## Abstract
Infectious and immune-mediated diseases (IIDs) represent a broad and rapidly expanding biomedical literature domain in which scalable evidence extraction, disease ontology refinement, and interpretable knowledge integration are essential for biomedical discovery. We constructed an IID-specific biomedical knowledge graph (IID KG) from PubMed abstracts and PMC full-text articles by integrating nested named entity recognition, ontology-guided identifier assignment, full-text relation extraction, and relation-resolution strategies. A gold-standard corpus of 500 PubMed abstracts and 8 PMC full-text articles was manually annotated for nested biomedical entities across six entity types. The resulting models were applied to 30,128,068 PubMed abstracts and 1,385,500 IID-related PMC full-text articles. A unified IID ontology was developed from 411,341 disease terms using hierarchical text classification, large language model-based refinement, ontology cross-referencing, and expert review, yielding 179,657 confirmed MeSH mappings. The final IID KG contains approximately 1,837,513 unique entities and 16,295,390 unique relations across eight relation types. The resource was released publicly together with repurposing workflows, supporting ontology-aligned literature mining, disease mechanism analysis, and drug-repurposing hypothesis generation for IID research.
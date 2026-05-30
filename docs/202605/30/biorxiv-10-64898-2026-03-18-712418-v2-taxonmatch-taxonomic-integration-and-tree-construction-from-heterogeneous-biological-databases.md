---
title: "TaxonMatch: taxonomic integration and tree construction from heterogeneous biological databases"
title_zh: TaxonMatch：来自异质生物数据库的分类学整合与树构建
authors: "Leone, M., Rech De Laval, V., Drage, H. B., Waterhouse, R. M., Robinson-Rechavi, M."
date: 2026-05-28
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.18.712418v2.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 异构数据库整合与分类学调和
tldr: 异构生物数据库间分类学数据整合面临命名不规范、同义词注释不完整和层级不一致等挑战。TaxonMatch框架结合TF-IDF向量化候选生成、监督机器学习匹配分类与谱系感知同义词解析，实现跨数据库分类单元对齐。在GBIF、NCBI和iNaturalist数据上验证，能解决传统方法无法处理的模糊案例。该框架支持构建统一、可互操作的生物多样性数据集，适用于生态、进化与保护生物学等下游分析。
source: biorxiv
selection_source: fresh_fetch
motivation: 解决异构生物数据库间因命名不规范、同义词不完整和层级不一致导致的分类数据整合困难。
method: 结合TF-IDF候选生成、监督机器学习匹配分类与谱系感知同义词解析，对齐并合并多源分类单元。
result: 成功整合GBIF、NCBI和iNaturalist数据，解决传统方法无法处理的模糊案例，并在三个用例中验证有效性。
conclusion: TaxonMatch提供了可扩展、可复现的分类数据整合方案，促进生态、进化与保护领域的数据互操作。
---

## 摘要
整合来自异质生物数据库的分类学数据仍然是生物多样性研究中的一个主要挑战，原因是命名法不标准化、同义词注释不完整以及分类层级不一致。这些问题限制了关键资源之间的互操作性，例如全球生物多样性信息设施（GBIF）、美国国家生物技术信息中心（NCBI）以及公民科学平台如iNaturalist。

在此，我们提出TaxonMatch，一个可扩展且可重现的分类学协调和跨数据库整合框架。该工作流结合了基于TF-IDF向量化的字符串候选生成、用于匹配分类的监督机器学习以及谱系感知的同义词解析，以对齐来自多个来源的分类实体。通过整合显式和隐式的等价关系，TaxonMatch解决了分类学数据中的排版变异、同义词和结构不一致问题。

该框架产生一个统一的分类结构，其中等价实体得到协调，同时保留来源特定的标识符、溯源信息和层级关系。我们评估了其在多个分类器上的稳健性，并展示了其在解决传统匹配方法无法处理的模糊分类案例中的有效性。

我们通过三个用例说明了TaxonMatch的适用性：构建整合GBIF、NCBI和iNaturalist数据的统一节肢动物分类学；识别具有分子信息的化石分类群的最接近现存亲属；以及将基因组资源与IUCN红色名录的保护数据进行整合。这些应用突显了该工作流支持生态学、基因组学和古生物学数据集整合的能力。

TaxonMatch为分类学数据整合提供了一个灵活且可泛化的解决方案，能够为生态学、进化和保护生物学中的下游分析构建连贯且可互操作的生物多样性数据集。

## Abstract
Integrating taxonomic data across heterogeneous biological databases remains a major challenge in biodiversity research due to non-standardized nomenclature, incomplete synonym annotation, and inconsistencies in taxonomic hierarchies. These issues limit interoperability between key resources such as the Global Biodiversity Information Facility (GBIF), the National Center for Biotechnology Information (NCBI), and citizen science platforms such as iNaturalist.

Here, we present TaxonMatch, a scalable and reproducible framework for taxonomic reconciliation and cross-database integration. The workflow combines string-based candidate generation using TF-IDF vectorization, supervised machine learning for match classification, and lineage-aware synonym resolution to align taxonomic entities across multiple sources. By integrating both declared and implicit equivalences, TaxonMatch resolves typographical variation, synonymy, and structural inconsistencies in taxonomic data.

The framework produces a unified taxonomic structure in which equivalent entities are reconciled while preserving source-specific identifiers, provenance information, and hierarchical relationships. We evaluate its robustness across multiple classifiers and demonstrate its effectiveness in resolving ambiguous taxonomic cases that are not handled by traditional matching approaches.

We illustrate the applicability of TaxonMatch through three use cases: the construction of a unified arthropod taxonomy integrating GBIF, NCBI, and iNaturalist data; the identification of closest extant relatives of fossil taxa with molecular information; and the integration of genomic resources with conservation data from the IUCN Red List. These applications highlight the ability of the workflow to support the integration of ecological, genomic, and paleontological datasets.

TaxonMatch provides a flexible and generalizable solution for taxonomic data integration, enabling the construction of coherent and interoperable biodiversity datasets for downstream analyses in ecology, evolution, and conservation biology.
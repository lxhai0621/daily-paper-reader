---
title: "The GA4GH Categorical Variation Representation Specification: A Unified Computational Framework for Reasoning over Genomic Variant Categories"
title_zh: GA4GH 类别变异表示规范：一个用于基因组变异类别推理的统一计算框架
authors: "Puthawala, D., Reardon, B., Babb, L., Kuzma, K., Stevenson, J. S., Goar, W. A., Dolin, R. H., Freimuth, R. R., Procknow, C., Pitel, B., Kundu, P., Rampersad, A., Van Allen, E. M., Wagner, A. H."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.02.10.705161v2.full.pdf"
tags: ["query:ma-kf"]
score: 6.5
evidence: 基因组知识库推理的统一计算框架
tldr: 针对生物医学领域分类变异表示不一致且不可计算的问题，本研究开发了GA4GH分类变异表示规范（Cat-VRS）。该框架通过统一的计算模型定义变异类别，支持分子和系统层面的约束。Cat-VRS实现了知识库协调、可计算搜索及变异自动匹配，为基因组知识的标准化交换和推理奠定了基础。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的分类变异描述缺乏统一标准和可计算性，严重阻碍了临床基因组数据的互操作性和解释。
method: 开发了基于约束的Cat-VRS框架，为精确和广泛的基因组变异类别提供统一的计算表示模型。
result: 成功实现了基因组知识库的协调、基于类别的搜索以及检测变异与分类实体之间的自动化匹配。
conclusion: Cat-VRS为基因组变异类别的可计算推理提供了原则性模型，是实现基因组知识标准化交换的重要基石。
---

## 摘要
类别变异（Categorical variants），即受共同属性约束的一组基因组变异，在生物医学生态系统的临床、监管和研究领域中无处不在，但其不一致且不可计算的表示方式阻碍了数据的互操作性和临床解释。我们调查了涵盖监管审批和生物医学文献的基因组知识库，发现类别变异构成了临床基因组学知识的很大一部分，但主要使用不兼容的定制模型进行描述。为解决这一问题，我们开发了 GA4GH 类别变异表示规范（Cat-VRS），这是一个基于约束的框架，为分子和系统变异领域中精确以及有意宽泛的类别提供了统一的可计算表示。Cat-VRS 实现了基因组知识库的协调、基于类别的可计算搜索，以及临床和研究背景下检测到的变异与类别实体之间的自动匹配。通过为类别变异提供一个有原则、可扩展的模型，Cat-VRS 实现了对基因组变异类别的可计算推理，并为基因组知识的标准化表示和交换奠定了基础。

## Abstract
Categorical variants, or sets of genomic alterations constrained by shared properties, are pervasive across clinical, regulatory, and research domains in the biomedical ecosystem, yet their inconsistent and non-computable representation hinders data interoperability and clinical interpretation. We surveyed genomic knowledgebases spanning regulatory approvals and the biomedical literature and found that categorical variants underpin a substantial proportion of clinical genomics knowledge, but are largely described using incompatible bespoke models. To address this, we developed the GA4GH Categorical Variation Representation Specification (Cat-VRS), a constraint-based framework that provides a unified computable representation for both precise and intentionally broad categories across molecular and systemic variant domains. Cat-VRS enables harmonization of genomic knowledgebases, computable category-based search, and automated matching between assayed variants and categorical entities in clinical and research contexts. By providing a principled, extensible model for categorical variation, Cat-VRS enables computable reasoning over genomic variant categories and establishes a foundation for the standardized representation and exchange of genomic knowledge.
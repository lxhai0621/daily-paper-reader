---
title: "OTRec: Deep learning recommender for prospective druggable disease-target associations"
title_zh: OTRec：用于前瞻性可成药疾病-靶点关联的深度学习推荐系统
authors: "Ofer, D., Linial, M."
date: 2026-05-10
pdf: "https://www.biorxiv.org/content/10.64898/2025.12.21.695803v2.full.pdf"
tags: ["query:ma-kf"]
score: 6.5
evidence: 整合文本描述、本体特征和生物注释进行推荐
tldr: 本研究开发了名为OTRec的深度学习推荐系统，旨在解决药物靶点与疾病关联识别的难题。该系统采用双塔架构，整合了文本描述、本体特征及生物学注释等异构数据，对66万余个疾病-靶点对进行建模。通过2022年至2025年的时间跨度验证，OTRec在预测临床试验成功率方面显著优于现有的Open Targets评分，并为约1.9万种疾病提供了候选关联排名，为药物研发和老药新用提供了有力支持。
source: biorxiv
selection_source: fresh_fetch
motivation: 识别具有成药潜力的疾病-靶点关联是转化医学的核心挑战，限制了新药发现和老药新用的效率。
method: 提出一种基于双塔架构的深度学习推荐系统，融合文本、本体和生物学通路等异构信息来学习疾病与靶点的潜在表示。
result: 在时间验证集上，OTRec的ROC-AUC达到0.872，显著超过了Open Targets原有的证据评分（0.559）。
conclusion: OTRec通过大规模预测成药基因组关联，为包括罕见病在内的数千种疾病提供了高置信度的候选靶点，具有重要的临床应用价值。
---

## 摘要
识别可成药的疾病-靶点关联仍然是转化医学中的核心挑战，限制了治疗方法的发现和老药新用。在这里，我们提出了 OTRec，这是一种基于深度学习的推荐系统，能够大规模对这些关联进行排序，并在时间留出（temporal hold-out）设置下对其进行评估。与依赖人工策划或聚合证据评分的方法不同，OTRec 采用双塔架构，从 663,351 个疾病-靶点对中学习潜在表示。该模型整合了异构输入，包括文本描述、本体衍生特征以及生物学注释，如可成药性（tractability）、基因本体（GO）术语和通路信息。我们通过在 2022 年 Open Targets (OT) 发布版本上进行训练，并在 2025 年的临床试验数据上进行评估，执行了时间验证。OTRec 改进了回顾性 OT 关联评分（ROC-AUC：0.872 ± 0.005 对比 0.559；PR-AUC：0.288 ± 0.009 对比 0.08）。在 5x5 靶点不相交交叉验证中，OTRec 的 ROC-AUC 达到 0.950，PR-AUC 达到 0.844，优于 OT 证据评分（ROC-AUC 0.91；PR-AUC 0.45）。我们对约 19,000 种 OT 平台（OTP）疾病的可成药基因组进行了排序，并通过交互式预测平台发布了约 282,500 个评分阈值在 0.65 以上的候选关联（分布内交叉验证精确度为 0.92），涵盖了 4,346 种疾病，其中包括 2,322 种罕见病。

## Abstract
Identifying druggable disease--target associations remains a central challenge in translational medicine, limiting therapeutic discovery and repurposing. Here, we present OTRec, a deep learning--based recommender system that ranks such associations at scale and evaluates them in a temporal hold-out setting. Unlike approaches that rely on manually curated or aggregated evidence scores, OTRec employs a two-tower architecture to learn latent representations from 663,351 disease--target pairs. The model integrates heterogeneous inputs, including textual descriptions, ontology-derived features, and biological annotations such as tractability, Gene Ontology (GO) terms, and pathway information. We perform temporal validation by training on the 2022 Open Targets (OT) release and evaluating on clinical trial data from 2025. OTRec improves on the retrospective OT association score (ROC-AUC: 0.872 {+/-} 0.005 vs 0.559; PR-AUC: 0.288 {+/-} 0.009 vs. 0.08). In 5x5 target-disjoint cross-validation, OTRec reaches ROC-AUC 0.950 and PR-AUC 0.844) improving on the OT evidence score (ROC-AUC 0.91; PR-AUC 0.45). We rank the druggable genome across ~19,000 OT platform (OTP) diseases and release ~282,500 candidate associations above a 0.65 score threshold (in-distribution CV precision 0.92), covering 4,346 diseases including 2,322 orphan diseases, through an interactive prediction platform.
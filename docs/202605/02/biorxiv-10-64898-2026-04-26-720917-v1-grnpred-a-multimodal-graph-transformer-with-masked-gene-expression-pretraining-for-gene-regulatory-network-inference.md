---
title: "GRNPred: A Multimodal Graph Transformer with Masked Gene Expression Pretraining for Gene Regulatory Network Inference"
title_zh: GRNPred：一种基于掩码基因表达预训练的多模态图 Transformer，用于基因调控网络推理
authors: "Nguyen, T. M., Hegde, A., Cheng, J."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.26.720917v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.5
evidence: 整合多模态数据用于基因调节网络推理和知识发现
tldr: 基因调控网络（GRN）推断在系统生物学中至关重要，但面临标注数据有限和复杂非线性关系的挑战。本文提出GRNPred，一种多模态图Transformer框架，融合了基因表达、功能注释、语义描述及基序先验等多源信息。通过掩码基因表达重建的自监督预训练和有监督微调两阶段策略，该模型能有效捕捉长程调控关系。在七个基准数据集上，GRNPred表现优于现有方法，显著提升了推断准确性。
source: biorxiv
selection_source: fresh_fetch
motivation: 针对基因调控网络推断中存在的标注数据稀缺、类别不平衡及复杂非线性调控关系等难题。
method: 提出一种多模态图Transformer框架，结合自监督掩码预训练与有监督微调，整合基因表达、语义及拓扑等多源数据。
result: 在七个基准数据集上，该模型取得了高达0.94的AUROC和0.93的AUPRC，性能显著超越现有最先进方法。
conclusion: GRNPred通过多模态融合与预训练策略，为复杂生物背景下的基因调控网络推断提供了一种高效且鲁棒的解决方案。
---

## 摘要
基因调控网络（GRN）推理是系统生物学中的一个关键问题，旨在从高维基因表达数据中识别转录因子（TF）与靶基因之间的相互作用，但由于标注数据有限、类别不平衡以及复杂的非线性调控关系，这仍然具有挑战性。为了解决这一问题，我们提出了 GRNPred，这是一个多模态图 Transformer 框架，整合了基因表达、功能注释、语义基因描述、调控基序先验和共表达网络拓扑。GRNPred 采用两阶段训练策略：首先是自监督预训练阶段，图 Transformer 通过在以 TF 为中心的子图上进行掩码基因表达重建来学习转录上下文；其次是监督微调阶段，利用已知的调控注释进行 TF-靶标边预测。通过利用基于 Transformer 的注意力机制，该模型捕捉到了传统方法难以建模的远程和上下文相关的相互作用。在七个基准数据集和三种调控网络构建上的广泛评估表明，GRNPred 优于现有最先进的方法，实现了高达 0.94 的 AUROC 和 0.93 的 AUPRC，同时在多种生物学背景下保持了强大的鲁棒性。

## Abstract
Gene regulatory network (GRN) inference is a key problem in systems biology that aims to identify transcription factor (TF)-target gene interactions from high-dimensional gene expression data, but it remains challenging due to limited labeled data, class imbalance, and complex nonlinear regulatory relationships. To address this, we propose GRNPred, a multimodal graph transformer framework that integrates gene expression, functional annotations, semantic gene descriptions, regulatory motif priors, and co-expression network topology. GRNPred uses a two-stage training strategy: first, a self-supervised pretraining phase where a graph transformer learns transcriptional context through masked gene-expression reconstruction on TF-centered subgraphs, and second, a supervised fine-tuning phase for TF-target edge prediction using known regulatory annotations. By leveraging transformer-based attention, the model captures long-range and context-dependent interactions that traditional methods struggle to model. Extensive evaluation across seven benchmark datasets and three regulatory network constructions shows that GRNPred outperforms state-of-the-art approaches, achieving up to 0.94 AUROC and 0.93 AUPRC while maintaining strong robustness across diverse biological settings.
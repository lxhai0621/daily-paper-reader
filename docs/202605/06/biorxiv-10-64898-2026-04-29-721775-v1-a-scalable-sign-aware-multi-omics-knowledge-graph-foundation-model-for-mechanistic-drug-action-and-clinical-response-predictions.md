---
title: A Scalable Sign-Aware Multi-Omics Knowledge Graph Foundation Model for Mechanistic Drug Action and Clinical Response Predictions
title_zh: 一种用于机制性药物作用和临床反应预测的可扩展符号感知多组学知识图谱基础模型
authors: "Mottaqi, M., Zhang, S., Adoremos, I., Zhang, P., Xie, L."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.29.721775v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.5
evidence: 用于药物作用机制预测的大规模有向多组学知识图谱
tldr: 针对现有生物医学知识图谱缺乏正负调控逻辑的问题，本文提出了SIGMA-KG大规模有符号多组学知识图谱及FLASH轻量化有符号异构图神经网络。该模型作为基础模型，通过自监督预训练学习生物通路中的激活与抑制效应，在药物作用机制预测、临床反应建模及药物重利用等任务中表现优异，显著提升了预测准确性与计算效率，为精准医疗提供了新工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有生物医学知识图谱多为无符号关联，忽略了分子间激活或抑制的调控逻辑，限制了药物机制预测的准确性与可解释性。
method: 构建了整合多组学数据的有符号图谱SIGMA-KG，并提出基于结构平衡原理的FLASH基础模型进行大规模自监督预训练。
result: "FLASH在药物机制预测和临床反应建模等任务中优于9种主流模型，并在药物重利用验证中取得69.6%的临床成功率。"
conclusion: 该研究提供了一个可扩展且感知符号的机制推理框架，有效提升了药物发现、多药联用设计及临床安全评估的预测精度。
---

## 摘要
从机制上预测药物作用的后果需要区分分子相互作用是激活性的还是抑制性的，然而大多数生物医学知识图谱和图神经网络将生物学过程表示为无符号的关联。这种局限性模糊了调节逻辑，限制了机制的可解释性，并降低了下游治疗预测的准确性。现有方法还受到化学覆盖范围有限以及跨生物尺度的分子和临床数据整合不足的进一步限制。在此，我们提出了 SIGMA-KG（有符号多组学图谱知识图谱），一个大规模的有符号多组学知识图谱，以及 FLASH（用于有符号异构图神经网络的快速轻量级架构），一种用于在生物医学知识图谱上进行基础模型预训练的快速轻量级有符号异构图神经网络。SIGMA-KG 将超出已批准药物范围的化学基因组扰动与转录组学、蛋白质组学和临床数据整合在一起，明确编码了生物和表型效应的方向和极性。FLASH 能够在此有符号图谱上进行大规模的高效自监督预训练，学习可迁移的表示，通过结构平衡原理保留激活和抑制效应如何在多跳生物通路中组合。在包括靶点特异性作用模式预测、药物诱导的临床反应建模和药物相互作用预测在内的多个下游任务中（无需特定任务的微调），预训练的 FLASH 基础模型始终优于或匹配九种最先进的无符号、关系和有符号图基准模型，同时显著提高了计算效率。我们通过可解释的归纳式药物重定向进一步证明了 FLASH 的转化效用，为四种复杂疾病确定了新的治疗候选药物，外部临床验证成功率达 69.6%。SIGMA-KG 和 FLASH 共同提供了一个可扩展的、符号感知的机制潜空间推理框架，提升了药物研发、多药联合设计和临床安全性评估的预测准确性。

## Abstract
Mechanistically predicting the consequences of drug action requires distinguishing whether molecular interactions are activating or inhibitory, yet most biomedical knowledge graphs and graph neural networks represent biology as unsigned associations. This limitation obscures regulatory logic, restricts mechanistic interpretability, and reduces the accuracy of downstream therapeutic predictions. Existing approaches are further constrained by limited chemical coverage and insufficient integration of molecular and clinical data across biological scales. Here we present SIGMA-KG (SIGned Multi-omics Atlas Knowledge Graph), a large-scale signed multi-omics knowledge atlas, and FLASH (Fast Lightweight Architecture for Signed Heterogeneous GNN), a fast and lightweight signed heterogeneous graph neural network for foundation-model pretraining on biomedical knowledge graphs. SIGMA-KG integrates chemogenomic perturbations beyond approved drugs with transcriptomic, proteomic, and clinical data, explicitly encoding the direction and polarity of biological and phenotypic effects. FLASH enables efficient self-supervised pretraining on this signed atlas at scale, learning transferable representations that preserve how activating and inhibitory effects compose across multi-hop biological pathways through structural balance principles. Across multiple downstream tasks (without task-specific fine-tuning), including target-specific mode-of-action prediction, drug-induced clinical response modeling, and drug-drug interaction prediction, the pretrained FLASH foundation model consistently outperforms or matches nine state-of-the-art unsigned, relational, and signed graph baselines while substantially improving computational efficiency. We further demonstrate the translational utility of FLASH through explainable inductive drug repurposing, identifying novel therapeutic candidates for four complex diseases with a 69.6% external clinical validation success rate. Together, SIGMA-KG and FLASH provide a scalable, sign-aware framework for mechanistic latent-space reasoning, advancing the predictive accuracy of drug discovery, polypharmacy design, and clinical safety assessment.
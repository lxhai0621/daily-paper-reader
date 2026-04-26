---
title: An autonomous LLM agent platform for computational binder design and conjugation-aware prioritization of antibody drug conjugates
authors: "Liu, G., He, M., Sun, L., Cheng, F., Zhang, Y."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.719907v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于计算生物学工作流的自主LLM智能体平台
tldr: Open Intelligence Hub是一个自主智能体平台，可规划并执行复杂的蛋白质设计工作流。
source: biorxiv
selection_source: fresh_fetch
motivation: 用于计算生物学工作流的自主LLM智能体平台。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Large language model (LLM) agents have automated tool use in chemistry, but orchestrating multi step computational biology workflows spanning structure prediction, protein design, and covalent conjugation remains manually intensive. Here we present Open Intelligence Hub (OIH), an autonomous LLM agent platform that dynamically plans and executes 32 containerised tools for protein binder design and antibody drug conjugate (ADC) prioritization. OIH introduces tier based decision routing, ipSAE guided interface filtering, and failure to knowledge distillation from 265 curated cases. Across five oncology targets, the agent correctly classified all five evaluated targets and required human correction for hotspot selection in only one case, producing binders ranked by ipSAE (Nectin4 ipTM = 0.87, HER2 ipTM = 0.85). A controlled ablation suggests that the agent's PPI-informed routing yields improved downstream ipTM and ipSAE scores than epitope guided alternatives. The LLM agnostic architecture enables deployment with local or commercial models without pipeline changes. All results are computational predictions awaiting experimental validation.
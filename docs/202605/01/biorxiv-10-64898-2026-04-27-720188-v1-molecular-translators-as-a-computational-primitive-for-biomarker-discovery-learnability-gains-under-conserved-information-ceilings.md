---
title: "Molecular Translators as a Computational Primitive for Biomarker Discovery: Learnability Gains Under Conserved Information Ceilings"
title_zh: 分子转换器作为生物标志物发现的计算原语：守恒信息上限下的可学习性增益
authors: "Saisan, P. A., Patel, S. P."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.720188v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.5
evidence: 病理学中的自动化知识发现
tldr: "本研究探讨了将H&E图像转换为分子表征的翻译器在生物标志物发现中的作用。针对H&E预测分子标志物的性能瓶颈，研究提出了形式化框架，区分了方法局限与形态学固有信息上限。研究发现，确定性翻译虽不增加新信息，但能通过提高有限样本的可学习性来提升性能。作者还发布了开源工具包，用于诊断学习状态、估计信息上限及压力测试，为克服计算病理学中的性能平台提供了理论指导和实用工具。"
source: biorxiv
selection_source: fresh_fetch
motivation: "旨在探究H&E图像预测分子标志物的性能瓶颈究竟源于算法局限还是形态学本身的信息上限。"
method: 开发了一个形式化框架来刻画确定性翻译器的特性，并提出“守恒信息上限下的可学习性增益”理论及配套开源工具包。
result: 证明了翻译器虽不改变信息总量，但能显著改善有限样本下的学习效率，并提供了区分不同性能受限机制的诊断方法。
conclusion: 该研究为理解和突破计算病理学中的性能平台提供了理论基础，其开源工具包有助于优化分子标志物的发现流程。
---

## 摘要
诸如 MISO 和 GigaTIME 之类的虚拟分子映射系统为计算病理学引入了一种具有潜在变革性的原语：将 H&E 全视野数字化切片图像转换为具有生物结构的分子表征，这些表征在配对队列上学习并作为推理时映射进行部署。尽管机器学习取得了持续进展，但从 H&E 到分子生物标志物（如基因突变）的预测在领域层面仍持续表现出反复的性能瓶颈，其驱动因素尚不明确。目前尚不清楚持续的优化是针对可消除的方法学局限，还是在触碰形态学施加的内在上限。我们开发了一个正式框架，用于刻画确定性转换器能够改变和不能改变的内容。基于组织学的生物标志物建模受两个约束条件的支配：方法受限的差距（有限标签、弱监督、结构化干扰）和模态受限的上限（形态学中固有的切片特异性信息）。由于确定性转换在推理时不引入新的切片级测量，因此 H&E 信息上限是守恒的；然而，转换仍能提高有限样本的可学习性，从而产生一种表观上的“信息-性能悖论”，我们将其正式定义为守恒信息上限下的可学习性增益。我们推导出了区分这些机制的可证伪特征，并在以 MISO 和 GigaTIME 等代表性系统为基础的受控分析实验中对其进行了表征。我们推出了一套开源工具包，包含学习机制诊断、信息上限估计、相位分析、保真度扰动测试以及捷径混淆压力测试，作为识别和克服转换器辅助的分子生物标志物发现及计算病理学中可消除性能瓶颈的操作准则。

## Abstract
Virtual molecular mapping systems such as MISO and GigaTIME introduce a potentially transformative primitive in computational pathology: translation of H\&E whole-slide images into biologically structured molecular representations, learned on paired cohorts and deployed as an inference-time map. Despite sustained progress in machine learning, H\&E-to-molecular-biomarker (e.g., gene mutation) prediction continues to exhibit recurrent field-level performance plateaus whose drivers remain poorly resolved. It remains unclear whether continued optimization targets a removable methodological limitation or instead presses against an intrinsic ceiling imposed by morphology. We develop a formal framework characterizing what deterministic translators can and cannot change. Histology-based biomarker modeling is governed by two constraints: method-limited gaps (finite labels, weak supervision, structured nuisance) and modality-limited ceilings (intrinsic slide-specific information in morphology). Because deterministic translation introduces no new slide-level measurements at inference, H\&E information ceilings are conserved; however, translation can still improve finite-sample learnability, yielding an apparent information--performance paradox that we formalize as learnability gains under conserved information ceilings. We derive falsifiable signatures distinguishing these regimes and characterize them in controlled analytical experiments anchored to representative systems, including MISO and GigaTIME. We introduce an open-source toolkit comprising learning regime diagnosis, information-ceiling estimations, phase analyses, fidelity perturbation tests, and shortcut-confounding stress tests as an operational rubric for identifying and overcoming removable performance plateaus in translator-assisted molecular biomarker discovery and computational pathology.
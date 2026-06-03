---
title: "CodeCytos: AI-assisted spatial molecular imaging analysis via code-augmented agent action space"
title_zh: CodeCytos：通过代码增强的智能体动作空间实现AI辅助空间分子成像分析
authors: "Vo, H. Q., Ly, S. T., Wan, Z., Nguyen, A.-V., Zhao, H., Sheng, J., Wong, S. T. C., Nguyen, H. V."
date: 2026-06-03
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.30.728935v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 用于空间分子成像分析的编码推理智能体
tldr: 传统空间分子成像分析工具依赖手动操作和固定预设特征，缺乏自动化与灵活性。为此提出CodeCytos，一个基于代码驱动的推理智能体框架，通过动态可编程交互支持自定义空间细胞特征探索。在额叶皮层等四个数据集上，使用领域外少样本编码示例即显著提升性能，无需专家标注，整体优于基线方法。该工作证明了代码驱动智能体在加速生物标志物发现方面的潜力。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统工具手动干预多、仅支持固定特征，无法灵活满足多样化的空间分析需求，限制了效率与可扩展性。
method: 基于大语言模型的代码推理智能体框架，通过代码增强动作空间实现动态交互，并利用领域无关的少样本示例引导编码。
result: 在四个组织数据集上，CodeCytos在最小提示设置下优于基线，且领域外少样本示例显著提升了性能。
conclusion: 代码驱动的推理智能体能有效支持自定义空间特征探索，加速组织微环境中的生物标志物发现。
---

## 摘要
传统的组织图像分析软件为细胞分析提供了基础功能，包括分割、形态特征提取和空间组织分析；然而，这些工具通常需要人工干预，且缺乏与代码驱动自动化的无缝集成，限制了复杂空间组织研究的效率和可扩展性，同时仅支持一组固定的预定义空间细胞特征，对定制分析的灵活性有限。为了解决这些局限，我们提出了CodeCytos，一个基于编码的推理智能体框架，能够实现与空间分子成像数据的动态、可编程交互，并简化针对不同研究需求的定制空间细胞特征的探索。我们通过四个专家精选的数据集案例研究展示了其实用性，这些数据集涵盖不同的组织类型，包括额叶皮层、非小细胞肺癌、胰腺和扁桃体，并在一个现实的极简提示设置下进行评估，其中生物科学家提出简单问题，无需任务特定指令或先验背景知识，同时以多个具有强大编码能力的大型语言模型骨干作为基准。我们进一步证明，纳入从空间分析领域外随机采样的领域无关的小样本上下文编码推理示例，能够显著提升性能，而无需昂贵的专家制作领域内演示；总体而言，CodeCytos优于基线方法，突显了代码驱动推理智能体在支持空间分子成像中定制特征探索和加速生物标志物发现方面的潜力。

## Abstract
Conventional tissue image analysis software provides foundational capabilities for cellular analysis, including segmentation, morphological feature extraction, and spatial organization analysis; however, these tools often require manual intervention and lack seamless integration with code-driven automation, limiting efficiency and scalability for complex spatial tissue studies, while also offering limited flexibility for custom analyses by supporting only a fixed set of predefined spatial cellular features. To address these limitations, we propose CodeCytos, a coding-based reasoning agent framework that enables dynamic, programmable interaction with spatial molecular imaging data and streamlines the exploration of custom spatial cellular features across diverse research needs. We demonstrate its utility through case studies on four expert-curated datasets spanning distinct tissue types, including frontal cortex, non-small-cell lung cancer, pancreas, and tonsil, and evaluate it under a realistic minimal prompt setting in which bioscientists pose simple questions without task-specific instructions or prior contextual knowledge, benchmarking multiple large language model backbones with strong coding capabilities. We further show that incorporating domain-agnostic few-shot in-context coding-reasoning examples, randomly sampled from outside the spatial analysis domain, substantially improves performance without requiring costly expert-crafted in-domain demonstrations; overall, CodeCytos outperforms baseline approaches, highlighting the potential of code-driven reasoning agents to support custom feature exploration in spatial molecular imaging and accelerate biomarker discovery.
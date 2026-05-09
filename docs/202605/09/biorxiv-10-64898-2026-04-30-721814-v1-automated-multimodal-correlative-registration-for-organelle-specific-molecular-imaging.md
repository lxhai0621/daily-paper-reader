---
title: Automated Multimodal Correlative Registration for Organelle-Specific Molecular Imaging
title_zh: 自动化多模态关联配准用于细胞器特异性分子成像
authors: "Lu, C., ZHAO, K., Cui, D., Chen, G., Yang, Q., Yang, H., Zhao, M., Song, K., Nikan, M., Li, Z., Zhao, S., Cen, J., Qiu, X., Young, S., Bennett, C. F., Seth, P., Chen, K., Qi, X., Jiang, H."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.30.721814v1.full.pdf"
tags: ["query:cmv"]
score: 7.5
evidence: 关联化学与超微结构图像进行跨尺度对齐
tldr: 亚细胞药物分布研究对理解药效至关重要，但NanoSIMS与电镜图像的人工关联极其耗时。本研究推出一种AI驱动的自动化配准流程，通过双向光流和置信度引导变换，实现跨尺度图像的精准对齐。该平台在多种生物样本中验证了其追踪治疗性分子的能力，为细胞器水平的分子成像和亚细胞药理学研究提供了高效、通用的自动化解决方案。
source: biorxiv
selection_source: fresh_fetch
motivation: 针对NanoSIMS化学成像与电子显微镜超微结构关联过程中人工操作繁琐且效率低下的挑战。
method: 提出一种集成双向光流、置信度引导仿射变换和自动模板匹配的AI驱动自动化配准流程。
result: 在多种细胞和组织中成功实现了寡核苷酸和抗体药物的跨尺度、细胞器级精准定位。
conclusion: 该研究建立了一个通用的自动化多模态配准平台，显著提升了亚细胞药理学研究的效率和精度。
---

## 摘要
绘制亚细胞药物分布图对于理解转运和脱靶效应至关重要。纳米二次离子质谱（NanoSIMS）能够对标记的治疗药物进行化学成像，但信号解释需要与电子显微镜进行超微结构关联，这是一个手动且费力的过程。我们提出了一种自动化的AI驱动流水线，用于关联化学和超微结构图像，从而实现细胞和组织中分子的多尺度、细胞器精确成像。该方法集成了双向光流、置信度引导的仿射变换以及用于跨尺度电镜（EM）对齐的自动模板匹配。形态丰富的离子通道（如32S）估计变换，并将其传播到稀疏的治疗信号（如79Br、15N），从而克服了低信噪比的挑战。我们在多种细胞和组织类型中验证了该框架，在体外和体内追踪寡核苷酸和抗体药物，揭示了细胞类型和细胞器特异性的分布模式。这项工作为自动化多模态配准和细胞器分辨率的亚细胞药理学建立了一个通用的平台。

## Abstract
Mapping subcellular drug distribution is essential for understanding trafficking and off-target effects. NanoSIMS enables chemical imaging of labeled therapeutics, but signal interpretation requires ultrastructural correlation with electron microscopy, a manual and laborious process. We present an automated AI-driven pipeline for correlating chemical and ultrastructural images, enabling multiscale, organelle-precise imaging of molecules in cells and tissues. The method integrates bidirectional optical flow, confidence-guided affine transformation, and automated template matching for cross-scale EM alignment. Morphology-rich ion channels (e.g., 32S) estimate transformations that propagate to sparse therapeutic signals (e.g., 79Br, 15N), overcoming low signal-to-noise challenges. We validate this framework across diverse cell and tissue types, tracking oligonucleotide and antibody therapeutics in vitro and in vivo to reveal cell-type- and organelle-specific distribution patterns. This work establishes a generalizable platform for automated multimodal registration and organelle-resolved subcellular pharmacology.
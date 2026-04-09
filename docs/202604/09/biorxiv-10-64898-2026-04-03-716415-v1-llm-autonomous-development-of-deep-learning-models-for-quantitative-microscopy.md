---
title: LLM-autonomous development of deep learning models for quantitative microscopy
authors: "Zhou, X., Wang, S."
date: 2026-04-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.03.716415v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于显微镜深度学习模型自主开发的LLM智能体
tldr: 本研究开发了一个基于大语言模型（LLM）的自主框架，旨在解决显微成像研究人员缺乏深度学习专业知识的难题。研究人员只需通过简短对话描述需求，该智能体即可自主完成物理模拟数据设计、神经网络实现、训练、故障诊断及迭代优化。在核分割、全息显微成像和组织病理学分类等多个任务中，该框架均达到了接近人类专家的性能水平，显著降低了深度学习在显微分析中的应用门槛。
source: biorxiv
selection_source: fresh_fetch
motivation: 深度学习在显微图像定量分析中表现卓越，但其开发过程对非机器学习专业的成像科学家而言具有极高的技术门槛。
method: 提出一种LLM智能体框架，通过与研究人员的简短对话获取需求，随后自主进行数据生成、模型构建、训练诊断及多轮迭代优化。
result: "在多个基准测试中，该智能体自主开发的模型在核分割任务中达到0.97的Dice系数，在病理分类任务中达到96.3%的AUC，性能接近已发表的基准水平。"
conclusion: 该框架证明了LLM能够自主处理复杂的深度学习开发全流程，使显微成像研究人员无需机器学习背景即可利用先进的图像分析技术。
---

## Abstract
Deep learning can extract quantitative measurements from microscopy images that are inaccessible to classical analysis, but developing these models requires machine learning expertise that most imaging scientists do not have. Here we present a framework in which a researcher describes their microscopy problem to a large language model (LLM) agent in under ten minutes of conversation---specifying what they image, what they want to measure, and what success looks like---and the agent autonomously handles the rest: designing physics-based training data, implementing a neural network, training, diagnosing failures, and iterating without human intervention. A researcher can start the agent before leaving the lab; overnight, it tests tens to a hundred model variations, each one an experiment that would otherwise demand active attention. We validate the framework across six microscopy modalities and four problem types. On the BBBC039 nuclear segmentation benchmark, the agent autonomously trains a U-Net with 3-class semantic segmentation and morphological post-processing, achieving pixel-level Dice of 0.97 and object-level F1 of 0.84---within 7% of the published baseline---while diagnosing a data pipeline bug that no amount of hyperparameter tuning could resolve. On single-protein holographic microscopy, the agent reads a published paper, designs a simulator, and develops an optimized model in a single session. On PatchCamelyon histopathology classification, the agent autonomously evolves through four optimization phases---from scratch training through transfer learning and regularization to inference-time ensembling---completing 97 iterations on 262,144 images to reach 89.3% test accuracy and 96.3% AUC, nearly matching the published rotation-equivariant baseline. This framework enables microscopy researchers to use deep learning-based image analysis without machine learning domain knowledge.
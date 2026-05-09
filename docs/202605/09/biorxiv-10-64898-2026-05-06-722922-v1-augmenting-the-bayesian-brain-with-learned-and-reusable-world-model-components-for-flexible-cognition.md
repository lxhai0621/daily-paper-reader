---
title: Augmenting the Bayesian Brain with learned and reusable world-model components for flexible cognition
title_zh: 利用学习且可重用的世界模型组件增强贝叶斯大脑，以实现灵活认知
authors: "Findling, C., Lee, J. K., Bakermans, J. J. W., Pouget, A., Wyart, V."
date: 2026-05-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.06.722922v1.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 模块化神经状态空间模型作为贝叶斯大脑的可扩展实现
tldr: 贝叶斯大脑假说认为认知依赖于内部生成模型，但现有模型受限于预设的任务特定结构和高计算开销。本研究提出了模块化神经状态空间模型，通过可学习的世界模型组件和摊销神经更新取代固定结构。该框架支持组件在不同任务间无缝重组，实现了零样本泛化。实验证实人类行为符合该模型的预测，揭示了可重用组件是实现灵活认知的关键计算原理。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的贝叶斯大脑模型通常依赖于预先设定的、特定于任务的生成结构，缺乏灵活性且计算成本高。
method: 提出了一种模块化神经状态空间模型，利用可学习的世界模型组件和摊销神经更新来实现灵活的推理。
result: 该模型支持在具有相似潜在动力学的任务间进行组件重组和零样本泛化，且其预测在人类行为实验中得到了验证。
conclusion: 可学习且可重用的世界模型组件是实现灵活认知的一种重要计算原理。
---

## 摘要
贝叶斯大脑假说认为认知依赖于世界的内部生成模型，但现有的实现仍受限于预先指定的、特定于任务的生成结构以及计算繁重的迭代推理方案。在这里，我们引入了模块化神经状态空间模型作为贝叶斯大脑的一种可扩展实现，用学习到的世界模型组件和摊销神经更新取代了固定的生成结构和预先指定的推理规则。该框架保留了通过隐藏原因解释观测结果的核心承诺，同时使推理变得可学习且可重用，而非预先指定且特定于任务。我们对这些模型的模块化实现使得学习到的组件能够在共享相似潜在动力学的、表面上不同的任务之间无缝重组和堆叠。这种计算重用支持零样本泛化，并预测了任务之间推理参数的选择性相关性。我们在人类行为中证实了这些关键预测，将学习且可重用的世界模型组件确定为灵活认知的一种候选计算原理。

## Abstract
The Bayesian Brain hypothesis assumes that cognition relies on internal generative models of the world, yet existing implementations remain constrained by pre-specified, task-specific generative structures and computationally heavy iterative inference schemes. Here, we introduce modular neural state-space models as a scalable realization of the Bayesian Brain, replacing fixed generative structures and pre-specified inference rules with learned world-model components and amortized neural updates. This framework preserves the core commitment to explaining observations through hidden causes while making inference learned and reusable rather than pre-specified and task-specific. Our modular implementation of these models affords learned components to be seamlessly recombined and stacked across superficially different tasks that share similar latent dynamics. Such computational reuse supports zero-shot generalization and predicts selective correlations of inference parameters between tasks. We confirm these key predictions in human behavior, identifying learned and reusable world-model components as a candidate computational principle for flexible cognition.
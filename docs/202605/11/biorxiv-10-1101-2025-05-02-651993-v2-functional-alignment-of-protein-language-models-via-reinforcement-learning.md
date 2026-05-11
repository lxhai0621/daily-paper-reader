---
title: Functional alignment of protein language models via reinforcement learning
title_zh: 通过强化学习实现蛋白质语言模型的功能对齐
authors: "Blalock, N., Seshadri, S., Nakamura, K., Babbar, A., Fahlberg, S. A., Kulkarni, A., Romero, P. A."
date: 2026-05-08
pdf: "https://www.biorxiv.org/content/10.1101/2025.05.02.651993v2.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 通过强化学习使蛋白质语言模型与功能目标对齐
tldr: 针对蛋白质语言模型在蛋白质工程中缺乏功能对齐、难以超越自然属性的问题，本研究提出了RLXF框架。该方法借鉴大语言模型的强化学习对齐技术，利用实验反馈数据引导模型优化特定生化目标。在五个蛋白质家族的实验中，RLXF显著提升了高功能序列的生成成功率，并成功设计出目前荧光强度最高的CreiLOV变体，证明了其在超越自然进化限制、实现功能驱动设计方面的巨大潜力。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的蛋白质语言模型缺乏对功能的显式理解，导致其设计的序列往往难以突破自然界已有的性能瓶颈。
method: 提出RLXF框架，通过借鉴大语言模型的强化学习对齐方法，利用实验测量数据对预训练模型进行功能化微调。
result: 在五个蛋白质家族中均提升了高功能变体的生成效率，并发现了迄今为止荧光性能最强的CreiLOV蛋白质变体。
conclusion: RLXF有效地将进化知识与实验反馈相结合，为超越自然进化限制的功能驱动型蛋白质设计提供了一种可扩展的方案。
---

## 摘要
蛋白质语言模型（pLMs）能够生成式地设计新型蛋白质序列，但在根本上仍与蛋白质工程目标不一致，因为它们缺乏对功能的显式理解，且往往无法将属性提升至超越自然界现有水平。我们引入了实验反馈强化学习（RLXF），这是一个受 ChatGPT 等大语言模型对齐方法启发而设计的通用框架，旨在将蛋白质语言模型与实验测量的功能目标相对齐。通过在五个不同的蛋白质家族中应用，RLXF 提升了高功能变体的生成效果，超越了预训练基准模型。我们在不依赖氧气的荧光蛋白 CreiLOV 上演示了这一点，RLXF 对齐的模型生成的序列具有显著增强的荧光强度，其中包括迄今为止报道的最强荧光 CreiLOV 变体。我们的结果表明，RLXF 对齐的模型有效地将预训练 pLMs 中编码的进化知识与实验观测相结合，提高了生成序列的成功率，并能够发现通过零样本或进化方法难以识别的协同突变组合。RLXF 提供了一种可扩展且易于实现的方法，引导生成模型趋向所需的生化属性，从而实现超越自然进化限制的功能驱动型蛋白质设计。

## Abstract
Protein language models (pLMs) enable generative design of novel protein sequences but remain fundamentally misaligned with protein engineering goals, as they lack explicit understanding of function and often fail to improve properties beyond those found in nature. We introduce Reinforcement Learning from eXperimental Feedback (RLXF), a general framework that aligns protein language models with experimentally measured functional objectives, drawing inspiration from the methods used to align large language models like ChatGPT. Applied across five diverse protein families, RLXF improves generation of high-functioning variants beyond pre-trained baselines. We demonstrate this with CreiLOV, an oxygen-independent fluorescent protein, where RLXF-aligned models generate sequences with significantly enhanced fluorescence, including the most fluorescent CreiLOV variants reported to date. Our results indicate that RLXF-aligned models effectively integrate the evolutionary knowledge encoded in pre-trained pLMs with experimental observations, improving the success rate of generated sequences and enabling the discovery of synergistic mutation combinations that are difficult to identify through zero-shot or evolutionary approaches. RLXF provides a scalable and accessible approach to steer generative models toward desired biochemical properties, enabling function-driven protein design beyond the limits of natural evolution.
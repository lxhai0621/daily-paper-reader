---
title: Self-Organized Neural Integrators in Noisy Spiking Networks
title_zh: 噪声脉冲网络中的自组织神经积分器
authors: "Feng, B., Gao, R., Li, N., Shouval, H."
date: 2026-05-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.04.722735v1.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 脉冲网络中用于工作记忆和证据积累的神经积分器
tldr: 本研究探讨了神经积分器在噪声脉冲网络中的自组织实现。传统模型通常依赖精细调节的循环连接，而本文通过平均场理论证明，随机连接的噪声网络在特定参数空间内可近似积分功能，且线性积分高度依赖噪声。研究进一步提出了一种受奖励调节的局部可塑性规则，使网络能自发达到该积分状态。该模型成功模拟了触觉决策任务中的皮层动力学，并为工作记忆、眼动持久性和证据积累提供了统一的生物物理机制。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在探索如何在无需精细调节连接的情况下，使生物神经系统实现工作记忆和证据积累所需的积分功能。
method: 结合平均场理论分析噪声对脉冲网络动力学的影响，并采用受奖励调节的双迹线可塑性规则进行自组织学习。
result: 证明了噪声是实现线性积分的关键，且模型能准确复现实验中观察到的皮层斜坡到阈值的动力学特征。
conclusion: 研究揭示了噪声脉冲网络通过自组织实现积分的生物学路径，为理解大脑处理时间相关任务提供了新视角。
---

## 摘要
神经积分器将短暂的输入转换为持久的放电，是工作记忆、证据积累和注视保持等功能的基础。经典的积分器模型通常依赖于精细调节的循环连接。在本文中，我们确定了一种生物学上合理的路径，通过该路径，随机连接的噪声脉冲网络可以在有限的参数空间区域内近似实现积分。平均场理论（MFT）揭示了此类网络中出人意料的简单动力学，这些动力学由平均循环权重和平均前馈权重决定，并表明线性积分关键取决于噪声。我们进一步证明，这一机制可以通过一种局部的、受奖励调制的双迹可塑性规则来实现。通过将该模型与来自延迟切换触觉决策任务的新实验结果进行比较，我们发现它再现了计时相关学习过程中自适应斜坡至阈值（ramp-to-threshold）皮层动力学的关键特征。同一框架还进一步联系了动眼神经持久性和证据积累，为单边界漂移扩散动力学提供了一种机械论实现。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWNeural integrators convert brief inputs into persistent firing and underlie functions such as working memory, evidence accumulation, and gaze holding. Classical integrator models typically rely on finely tuned recurrent connectivity. Here we identify a biologically plausible route by which randomly connected noisy spiking networks can approximate integration over a finite region of parameter space. Mean-field theory (MFT) reveals surprisingly simple dynamics in such networks, governed by the mean recurrent weight and mean feedforward weight, and shows that linear integration critically depends on noise. We further show that this regime can be reached through a local, reward-modulated two-trace plasticity rule. Comparing the model with new experimental results from a delay-switching tactile decision-making task, we find that it reproduces key features of adaptive ramp-to-threshold cortical dynamics during timing-related learning. The same framework further connects to oculomotor persistence and evidence accumulation, providing a mechanistic realization of single-boundary drift-diffusion dynamics.
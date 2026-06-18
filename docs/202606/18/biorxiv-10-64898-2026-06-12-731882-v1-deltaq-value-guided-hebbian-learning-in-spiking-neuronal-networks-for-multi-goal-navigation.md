---
title: "DeltaQ: Value-Guided Hebbian Learning in Spiking Neuronal Networks for Multi-Goal Navigation"
title_zh: "DeltaQ: 脉冲神经网络中基于价值的赫布学习用于多目标导航"
authors: "Earl, C., Unal, G., Hazan, H., Neymotin, S. A."
date: 2026-06-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.12.731882v1.full.pdf"
tags: ["query:agent"]
score: 6.0
evidence: 脉冲神经网络中的强化学习用于导航
tldr: 动物在稀疏或延迟奖励环境中导航需依赖内部空间表征和记忆。现有模型主要复现神经动态，未展示如何支持导航学习。本文提出DeltaQ脉冲神经网络模型，结合网格细胞空间编码、DeltaQ调制的Hebbian可塑性及上下文细胞调制，在两种迷宫环境中实现多目标导航。模型能生成不同空间表征、学习高效策略并支持共享环境下的多种导航目标，为连接神经回路与功能强化学习提供桥梁。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有计算模型多聚焦于复现神经动态，而非展示空间表征如何支持导航任务学习。
method: 提出DeltaQ SNN，含网格细胞、关联细胞和上下文细胞，通过DeltaQ调制的Hebbian可塑性实现局部突触学习。
result: 在稀疏延迟奖励下成功学习高效导航策略，上下文调制使共享网络支持多个导航目标。
conclusion: 生物启发空间表征、价值引导可塑性和上下文调制可联合支持脉冲神经网络中的灵活导航。
---

## 摘要
动物通常需要导航至目标，而关于目标进展的反馈稀疏或延迟，这要求其具有内部空间表征和先前经验记忆。海马-内嗅系统被认为通过分布式空间表征支持这一能力，从而引导目标导向行为。然而，许多关于这些回路的计算模型主要侧重于再现神经动态，而非演示此类表征如何支持导航任务中的学习。我们提出了一种生物启发的脉冲神经网络（SNN）模型，该模型结合了网格细胞衍生的空间表征、ΔQ调制的赫布可塑性以及上下文依赖调制，以支持稀疏奖励条件下的导航。网格细胞群体生成分布式空间编码，由关联细胞群体转化为更具空间选择性的内部表征。学习由从目标条件Q表计算的Q值变化（ΔQ）驱动，使得局部突触可塑性能够纳入关于长期导航结果的信息。对于包含多个导航目标的环境，上下文细胞群体提供任务依赖调制，使得共享网络架构能够支持不同的导航策略。在两种互补的迷宫环境中，该模型展示了三个核心能力：生成不同的空间表征、在稀疏和延迟奖励下学习高效的导航策略，以及在共享环境中支持多个导航目标。结果进一步表明，上下文调制在基本共享的群体表征中引入了微妙的、依赖于任务的变异，使得相同的空间位置能够支持不同的导航行为。这些发现表明，生物启发的空间表征、价值引导的可塑性和上下文调制可以共同支持脉冲神经网络中的灵活导航，从而在机械性神经回路模型与功能性强化学习之间架起桥梁。

## Abstract
Animals must often navigate environments where feedback about progress toward a goal is sparse or delayed, requiring internal representations of space and memory of prior experience. The hippocampal-entorhinal system is believed to support this capability through distributed spatial representations that guide goal-directed behavior. However, many computational models of these circuits focus primarily on reproducing neural dynamics rather than demonstrating how such representations support learning on navigation tasks. We present a biologically inspired spiking neuronal network (SNN) model that combines grid-cell-derived spatial representations, {Delta}Q-modulated Hebbian plasticity, and context-dependent modulation to support navigation under sparse reward conditions. Grid Cell populations generate distributed spatial codes that are transformed by an Association Cell population into more spatially selective internal representations. Learning is driven by changes in Q-values ({Delta}Q) computed from a goal-conditioned Q-table, allowing local synaptic plasticity to incorporate information about long-term navigation outcomes. For environments containing multiple navigation objectives, a Context Cell population provides task-dependent modulation that enables a shared network architecture to support distinct navigation policies. Across two complementary maze environments, the model demonstrates three core capabilities: generation of distinct spatial representations, learning of efficient navigation policies under sparse and delayed reward, and support for multiple navigation objectives within a shared environment. The results further show that contextual modulation introduces subtle task-dependent variations into a largely shared population representation, allowing identical spatial locations to support different navigation behaviors. These findings demonstrate that biologically inspired spatial representations, value-guided plasticity, and contextual modulation can jointly support flexible navigation in spiking neuronal networks, providing a bridge between mechanistic neural circuit models and functional reinforcement learning.
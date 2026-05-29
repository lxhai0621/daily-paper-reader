---
title: "Semantic map learning and externalization in an embodied neural agent: A comparison to human behavioral and neural data"
title_zh: 具身神经智能体中的语义地图学习与外部化：与人类行为和神经数据的比较
authors: "Simone, K., Steffen, L., Dumont, N. S.-Y., Yu, S., Ly, H., Damberger, G., Eliasmith, C."
date: 2026-05-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.19.726370v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 具身神经智能体用于空间学习和记忆
tldr: "人类空间记忆如何构建认知地图并外化知识仍待探索。本研究将脉冲语义SLAM算法适配于虚拟现实'寻宝'任务，构建具身神经代理，整合双足运动、视觉、记忆与手臂控制网络，实现第一人称学习位置-物体关联并通过指向与置信度表达外化知识。与人类数据对比，模型复现了准确性随置信度单调递增的行为效应，以及回忆依赖左海马局部场电位功率的神经特征。工作为具身导航、记忆与交流的机制提供了统一框架。"
source: biorxiv
selection_source: fresh_fetch
motivation: 人类空间记忆中的认知地图构建与外化回忆机制尚未明确，尤其是SLAM（同步定位与建图）在人类中的神经关联。
method: 将脉冲语义SLAM算法用于虚拟现实寻宝任务，构建具身代理，集成运动、视觉、记忆网络，学习位置-物体关联并通过指向和置信度外化。
result: 模型复现了人类行为中准确性随置信度单调递增，以及回忆依赖左海马局部场电位功率的神经效应。
conclusion: 该工作为具身导航、记忆与交流提供了统一的机制框架，连接了算法与人类认知。
---

## 摘要
所有哺乳动物都能从感官输入中构建内部认知地图，支持空间学习和规划。虽然啮齿类动物研究表明哺乳动物导航系统解决了SLAM（同时定位与地图构建）问题，但其在人类空间记忆和显式回忆中的作用仍知之甚少。为此，我们改进了一个脉冲语义SLAM算法，用于“寻宝”任务——人类参与者在虚拟现实中导航一个3D海滩，随后指向记忆中的物体位置。我们的智能体整合了双足运动、视觉、记忆和手臂控制网络，以实现第一人称的场所-物体关联学习，并通过指向和表达置信度来外部化该知识。将模型可观测数据与人类数据比较，我们重现了关键的行为和神经效应：准确度随置信度单调递增，以及回忆依赖于在左侧海马体中观察到的局部场电位功率。这项工作提供了一个将人类空间认知中的具身导航、记忆和交流联系起来的机制框架。

## Abstract
All mammals can build internal cognitive maps from sensory input, supporting spatial learning and planning. While rodent studies have shown the mammalian navigation system solves the SLAM (Simultaneous Localization and Mapping) problem, its role in human spatial memory and overt recall are less understood. To investigate this, we adapted a spiking semantic SLAM algorithm for a "Treasure Hunt" task, where human participants navigate a 3D beach in virtual reality and later point to remembered object locations. Our agent integrates networks for bipedal locomotion, vision, memory, and arm control to enable first-person learning of place-object associations, and externalizing that knowledge by pointing and expressing confidence. Comparing model observables to human data, we replicate key behavioral and neural effects: monotonic scaling of accuracy with confidence, and recall-dependence on local field potential power observed in the left hippocampus. This work offers a mechanistic framework linking embodied navigation, memory, and communication in human spatial cognition.
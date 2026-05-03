---
title: "Fast learning, memorization and generalization: A computational characterization of sparse to dense hippocampal-cortical codes"
title_zh: 快速学习、记忆与泛化：从稀疏到稠密的海马-皮层编码的计算表征
authors: "Sasan, A., Mok, R. M."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.721238v1.full.pdf"
tags: ["query:agent"]
score: 7.5
evidence: 神经网络中用于记忆的海马-皮层编码
tldr: "本研究探讨了海马体稀疏编码对快速学习和泛化的影响。通过在深度神经网络中系统调节稀疏水平和层深度，研究发现5%的平衡稀疏度（与生物观测一致）能最大化学习性能。研究揭示了稀疏编码在不同层级的作用：早期层稀疏促进快速记忆但泛化差，而后期层稀疏则显著提升泛化能力，为海马体-皮层回路的计算机制提供了统一解释。"
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在阐明海马体中的稀疏编码如何平衡复杂任务中的快速学习、记忆化与泛化能力。
method: 利用深度神经网络，通过改变稀疏比例和所处层级，分析其对表征正交化及学习表现的影响。
result: "实验表明5%的稀疏度表现最优，且稀疏层的位置决定了系统是倾向于单纯记忆还是有效泛化。"
conclusion: 该研究证明了海马体-皮层回路通过灵活配置稀疏编码，能够同时支持快速记忆与通用知识的获取。
---

## 摘要
神经心理学和动物研究的经典发现已确定海马体是快速学习和情景记忆的关键基质，其中齿状回表现出极端的稀疏编码。长期以来，人们假设稀疏编码通过模式分离实现快速学习，从而能够快速区分高度相似的输入。然而，先前的计算工作主要集中在情景记忆或简化的线性任务上，关于海马稀疏性如何影响复杂任务中的学习速度和泛化能力仍不清楚。在本文中，我们对深度神经网络中的稀疏编码进行了系统研究，改变了稀疏水平和位置（层深度），并评估了其对学习和泛化的功能性影响。我们发现，当稀疏水平平衡在5%时，学习性能达到最大化，这与海马稀疏编码的经验估计相吻合。维度和表征相似性分析表明，稀疏层促进了输入表征的正交化，镜像了支持快速学习的海马模式分离。此外，早期层的稀疏性仅在训练集上导致快速学习，而在留出测试集上泛化表现较差，反映了记忆化；而后期层的稀疏性则持续有助于泛化，这为海马-皮层学习理论提供了启示。我们的研究结果展示了海马稀疏编码的力量和权衡，并表明海马-皮层回路如何根据稀疏性实施的位置，具备支持快速学习和泛化的计算能力。我们为海马体作为一个快速、稀疏的记忆系统，以及海马-皮层通路作为一种可泛化学习的机制，提供了一个统一的视角。

## Abstract
Classic findings from neuropsychology and animal studies established the hippocampus as a key substrate for rapid learning and episodic memory, with the dentate gyrus exhibiting extreme sparse coding. Sparse coding has long been hypothesized to enable fast learning through pattern separation, enabling rapid separation of highly similar inputs. However, prior computational work has largely focused on episodic memory or simplified linear tasks, leaving open how hippocampal sparsity affects learning speed and generalization in complex tasks. Here, we present a systematic investigation of sparse coding in deep neural networks varying the sparsity level and location (layer depth) and evaluated the functional consequences for learning and generalization. We found that learning performance is maximized at a balanced sparsity level of 5%, matching empirical estimates of the hippocampal sparse code. Dimensionality and representational similarity analyses revealed that sparse layers promoted orthogonalization of input representations, mirroring hippocampal pattern separation that enables fast learning. Furthermore, sparsity in early layers led to fast learning only on the training set and poor generalization to a held out test set, reflecting memorization, while sparsity in later layers consistently aided generalization, providing implications for theories of hippocampal-cortical learning. Our findings demonstrate the power and tradeoffs of the hippocampal sparse code, and show how hippocampal-cortical circuits possess the computational capacity to support both fast learning and generalization, depending on where sparsity is implemented. We offer a unifying perspective on how the hippocampus works as a fast, sparse memory system and the hippocampal-cortical pathway as a mechanism for generalizable learning.
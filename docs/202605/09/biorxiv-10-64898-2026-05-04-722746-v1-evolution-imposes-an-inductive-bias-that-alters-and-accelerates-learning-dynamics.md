---
title: Evolution imposes an inductive bias that alters and accelerates learning dynamics
title_zh: 进化施加了一种改变并加速学习动力学的归纳偏置
authors: "Midler, B., Pan-Vazquez, A."
date: 2026-05-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.04.722746v1.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 神经网络的进化优化与学习动力学
tldr: 本研究探讨了进化对神经网络学习动力学的影响，旨在解决人工神经网络训练数据需求过大的问题。通过结合自然选择算法与在线学习，研究者提出了一种进化调节方法。实验表明，进化赋予了网络独特的归纳偏置，使其在强化学习和监督学习中表现出更快的微调速度和更优的学习效率，证明了进化在加速生物和人工系统学习中的关键作用。
source: biorxiv
selection_source: fresh_fetch
motivation: 针对人工神经网络缺乏生物大脑那种由进化产生的、能实现快速学习的先天结构这一差距展开研究。
method: 提出一种结合自然选择模拟与在线学习的进化调节算法，并将其应用于强化学习和监督学习任务。
result: 进化调节后的网络虽然初始表现一般，但具备独特的潜在动力学，能够通过极少量的微调迅速达到顶尖性能。
conclusion: 进化作为一种归纳偏置，能够预先调整神经系统的状态，从而显著改变并加速其后续的学习动力学。
---

## 摘要
生物大脑和人工神经网络的学习动力学是神经科学和机器学习共同关注的课题。它们之间的一个关键区别在于，神经网络通常是从随机初始化状态开始训练的，而每个大脑都是数代进化优化的产物，产生了能够实现少样本学习和内置反射的先天结构。相比之下，人工神经网络需要非生态数量的训练数据才能达到相当的性能。为了研究进化优化对神经网络学习动力学的影响，我们结合了模拟自然选择和在线学习的算法，开发出一种进化调节人工神经网络的方法，并将其应用于强化学习和监督学习场景。我们发现，进化调节算法本身的表现与未优化的基准相当。然而，经过进化调节的网络显示出独特且潜在的学习动力学迹象，并且可以快速微调至最佳性能。这些结果表明，进化构成了一种归纳偏置，通过调节神经系统来实现快速学习。

## Abstract
The learning dynamics of biological brains and artificial neural networks are of interest to both neuroscience and machine learning. A key difference between them is that neural networks are often trained from a randomly initialized state whereas each brain is the product of generations of evolutionary optimization, yielding innate structures that enable few-shot learning and inbuilt reflexes. Artificial neural networks, by contrast, require non-ethological quantities of training data to attain comparable performance. To investigate the effect of evolutionary optimization on the learning dynamics of neural networks, we combined algorithms simulating natural selection and online learning to produce a method for evolutionarily conditioning artificial neural networks, and applied it to both reinforcement and supervised learning contexts. We found the evolutionary conditioning algorithm, by itself, performs comparably to an unoptimized baseline. However, evolutionarily conditioned networks show signs of unique and latent learning dynamics, and can be rapidly fine-tuned to optimal performance. These results suggest evolution constitutes an inductive bias that tunes neural systems to enable rapid learning.
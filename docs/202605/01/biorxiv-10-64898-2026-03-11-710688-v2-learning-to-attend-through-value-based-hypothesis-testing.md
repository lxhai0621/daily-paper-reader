---
title: Learning to Attend Through Value-Based Hypothesis Testing
authors: "Maher, C., Saez, I., Radulescu, A."
date: 2026-04-28
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.11.710688v2.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 用于决策智能体的基于特征的强化学习
tldr: "本研究探讨了人类在复杂环境中如何确定关键特征。研究者通过训练循环神经网络（RNN）来模拟特征强化学习（FRL）和序列假设检验（SHT）两种竞争性心理学理论。结果发现，结合了价值学习与假设检验的混合模型能以超过80%的准确率解码人类的潜在注意力。这一发现揭示了人类注意力并非单一机制，而是由学习到的特征价值引导规则生成与评估的动态交互过程。"
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在区分人类注意力分配是源于渐进的特征价值学习还是选择性的规则假设检验。
method: 采用RNN在FRL和SHT模型生成的合成数据上进行训练，从而推断并解码人类在决策过程中的潜在注意力动态。
result: "混合模型在解码人类注意力方面的表现优于单一模型，准确率达到了80%以上。"
conclusion: 研究证明人类注意力反映了基于价值的学习与假设检验之间的相互作用，特征价值引导了假设的生成。
---

## Abstract
In complex environments, humans must determine which features are relevant for learning and decision-making. Psychological theories offer competing accounts of this process: associative models suggest that attention emerges gradually through learned changes in feature values, whereas hypothesis-driven accounts propose that learners selectively attend to actively tested rules. Because attentional states are covert, similar behavior can arise from different underlying strategies, making these accounts difficult to distinguish using choice data alone. We inferred latent attention dynamics during learning and decision-making by training recurrent neural networks on synthetic data generated from feature-based reinforcement learning (FRL) and serial hypothesis testing (SHT) models. A network trained on hybrid (FRL+SHT) data outperformed single-model networks, decoding latent human attention with more than 80% accuracy. These results suggest that human attention reflects an interaction between value-based learning and hypothesis testing, in which learned feature value guides the generation and evaluation of candidate rules.
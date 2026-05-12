---
title: Task-space dimensions guide human exploration in complex environments
title_zh: 任务空间维度引导复杂环境中的人类探索
authors: "An, J., Hu, J., Wu, Y. E., Ning, S., Liu, C., Pan, Y., Zhu, F., Wang, R., Ji, N."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.29.720265v1.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 人类探索策略与强化学习智能体的对比
tldr: 本研究探讨了人类在复杂高维环境中如何通过识别任务相关维度来优化决策。研究者设计了一种新型多维学习任务，受试者需在未知任务维度的情况下通过探索识别奖励相关维度。研究发现了两种典型的“维度引导”探索与利用策略，证明了这种策略能显著提升奖励学习效率，为改进人工智能的探索效率提供了新思路。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在揭示人类在复杂高维环境中优于标准强化学习算法的认知策略，特别是如何识别任务相关信息。
method: 开发了一种受试者事先不知道任务维度、需通过探索识别奖励相关维度的多维学习实验任务。
result: 识别出两种典型的“维度引导”选择模式，并发现这种探索方式能有效促进基于奖励的学习效率。
conclusion: 人类利用任务空间维度来引导探索，这一发现为提升AI智能体的探索效率提供了重要启发。
---

## 摘要
人类经常在复杂的、高维的环境中做出决策，在这些环境中，识别与任务相关的信息对于快速优化行为至关重要。在应对此类复杂性方面，人类的表现优于标准的强化学习智能体，但人类的认知策略仍不清楚。为了解决这一问题，我们开发了一种新型的多维学习任务，其中只有一部分维度与奖励相关。关键在于，与之前的研究不同，受试者并不知道真实的任务维度，必须通过探索来识别它们。这种设计紧密模拟了现实世界任务中的模糊性。我们的结果识别出了两种典型的选择模式，揭示了探索和利用中的“维度引导”策略。跨受试者分析表明，维度引导的探索可能会提高基于奖励的学习效率。这些发现表明，人类利用任务维度来引导探索，并为提高人工智能智能体的探索效率提供了灵感。

## Abstract
Humans frequently make decisions in complex, high-dimensional environments, where identifying task-relevant information is critical for rapid behavior optimization. Humans outperform standard reinforcement learning agents in navigating such complexity, yet the cognitive strategies of humans remain unclear. To address this, we developed a novel multi-dimensional learning task in which only a subset of dimensions is reward-related. Crucially, unlike prior studies, subjects are uninformed of the true task dimensionality and have to identify them through exploration. This design closely mimics the ambiguity in real-world tasks. Our results have identified two stereotyped choice patterns that reveal "dimension-guided" strategies in exploration and exploitation. Cross-subject analyses suggest that dimension-guided exploration may promote the efficiency of reward-based learning. These findings indicate that humans leverage task dimensionality to guide exploration, and provide inspiration for improving exploration efficiency in AI agents.
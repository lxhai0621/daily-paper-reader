---
title: Designing biochemical circuits with tree search
title_zh: 利用树搜索设计生化电路
authors: "Bhamidipati, P. S., Thomson, M."
date: 2026-05-03
pdf: "https://www.biorxiv.org/content/10.1101/2025.01.27.635147v2.full.pdf"
tags: ["query:agent"]
score: 6.5
evidence: 使用蒙特卡洛树搜索强化学习算法优化电路设计
tldr: 本研究针对生化电路设计中搜索空间随组件增加而呈指数级增长的难题，提出了基于蒙特卡洛树搜索（MCTS）的强化学习框架 CircuiTree。该方法将电路设计视为序列决策过程，成功实现了从三组件到五组件电路的高效设计。研究不仅发现了具有高度容错性的“基序多路复用”新策略，还证明了该框架在处理复杂生物网络拓扑优化方面的卓越扩展性和鲁棒性。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统的穷举法在处理超过四个组件的生化电路设计时，因搜索空间的组合爆炸而变得难以实现。
method: 开发了名为 CircuiTree 的强化学习框架，利用并行蒙特卡洛树搜索优化电路拓扑以匹配目标表型。
result: 该框架成功设计出能抵御基因缺失的五组件电路，并揭示了通过重叠多个功能基序来增强鲁棒性的“基序多路复用”机制。
conclusion: CircuiTree 是首个可扩展的生化电路设计计算平台，为发现复杂且具有鲁棒性的生物网络提供了有力工具。
---

## 摘要
发现表现出预期行为的生化电路是生物工程中的一个突出问题。由于搜索空间的组合规模增长，枚举每种可能的电路拓扑结构的传统方法对于具有四个以上组件的电路变得难以处理。在这里，我们使用蒙特卡洛树搜索（MCTS），一种强化学习（RL）算法，通过将电路设计视为一系列组装决策，来针对目标表型优化电路拓扑。我们的基于强化学习的设计框架（我们称之为 CircuiTree）通过优先考虑稀疏性，高效且全面地找到了三组件振荡器的鲁棒设计。CircuiTree 还可以从其搜索结果中推断出候选网络基序，产生与枚举法相似的结果。利用并行 MCTS，我们将该工作流程扩展到五个组件，并发现高度容错的设计使用了一种新颖的策略，我们称之为基序多路复用（motif multiplexing）。多路复用电路包含许多重叠的网络基序，每个基序在不同的突变场景下激活，在一种情况下，为五分之四的单基因缺失提供了鲁棒性。总的来说，CircuiTree 为设计生化电路提供了第一个可扩展的计算平台。

## Abstract
Discovering biochemical circuits that exhibit a desired behavior is an outstanding problem in biological engineering. The traditional approach of enumerating every possible circuit topology becomes intractable for circuits with more than four components due to combinatorial scaling of the search space. Here, we use Monte Carlo Tree Search (MCTS), a reinforcement learning (RL) algorithm, to optimize circuit topology for a target phenotype by approaching circuit design as a sequence of assembly decisions. Our RL-based design framework, which we call CircuiTree, efficiently and comprehensively finds robust designs for three-component oscillators by prioritizing sparsity. CircuiTree can also infer candidate network motifs from its search results, producing similar results to enumeration. Using parallel MCTS, we scale this workflow up to five components and find that highly fault-tolerant designs use a novel strategy, which we call motif multiplexing. Multiplexed circuits contain many overlapping network motifs that each activate in different mutational scenarios, in one case lending robustness to four out of five single-gene deletions. Overall, CircuiTree provides the first scalable computational platform for designing biochemical circuits.
---
title: Nonlinear influence of reward volatility on arbitration between multiple learning strategies reflects cost-benefit optimization
title_zh: 奖励波动性对多种学习策略之间仲裁的非线性影响反映了成本效益优化
authors: "Yamada, T., Samejima, K."
date: 2026-06-19
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.15.732293v1.full.pdf"
tags: ["query:agent"]
score: 6.0
evidence: 强化学习策略仲裁
tldr: 环境变化需要灵活行为，但奖励波动性如何调节学习策略尚不清楚。研究采用两步决策任务系统操纵波动性和时间压力，结合模型无关分析和层次贝叶斯拟合。发现奖励波动性对模型自由与模型基础策略的仲裁呈倒U形非线性影响：中等波动性时模型基础策略最强，时间压力则促使转向模型自由策略。这表明人类在不确定环境下并非总是采用模型基础策略，支持成本-收益优化。
source: biorxiv
selection_source: fresh_fetch
motivation: 探究奖励波动性如何系统调节模型自由与模型基础强化学习策略之间的仲裁。
method: 使用修改的两步决策任务，系统操纵奖励波动性和时间压力，结合模型无关分析、模拟和层次贝叶斯建模。
result: 奖励波动性对策略仲裁呈倒U形非线性影响，中等波动性增强模型基础策略；时间压力促使转向模型自由策略。
conclusion: 人类在不确定和动态环境中并非始终使用模型基础策略，即使了解任务结构，也体现成本-收益优化。
---

## 摘要
动作选择涉及两个系统：依赖动作-结果对经验的无模型强化学习策略，以及通过使用不变环境结构的模型进行推理从而实现更灵活行为的基于模型的强化学习策略。尽管环境变化需要更灵活的行为，但波动性（一种捕捉环境变化速度或频率的高阶统计量）系统性地调节这些策略的能力仍不清楚。我们使用两种修改后的两步决策任务，研究了奖励波动性对无模型和基于模型的强化学习策略之间仲裁的影响。在实验1中，参与者在不同水平的奖励波动性和时间压力下执行任务。在实验2中，我们在更广范围内系统地操纵奖励波动性，以评估波动性与学习策略之间的关系。行为数据通过模型无关的单试次和多试次回溯分析、强化学习模拟以及分层贝叶斯模型拟合进行分析。跨实验结果表明，奖励波动性对无模型和基于模型的强化学习策略之间的仲裁产生逆U型非线性效应，因为基于模型的学习策略在中等奖励波动性水平下被强烈驱动。这些调节效应仅在已学习任务中转换结构的个体中观察到，而未学习转换结构的个体无论奖励波动性如何都依赖无模型学习策略。强化学习模拟揭示，基于模型的学习策略相对于无模型学习策略的优势在中等奖励波动性水平达到峰值。此外，增加时间压力使行为转向无模型学习策略。这些结果表明，人类在不确定和动态环境中并不总是使用基于模型的强化学习策略，即使他们了解任务结构，这支持了成本效益优化。

## Abstract
Action selection involves two systems: a model-free reinforcement learning strategy, which relies on experience with action-outcome pairs, and a model-based reinforcement learning strategy, which enables more flexible behavior via inference using a model of the invariant environmental structure. Although environmental change requires more flexible behavior, the ability of volatility, a higher-order statistic that captures how rapidly or frequently the environment changes, to systematically modulate these strategies remains unclear. We examined the effects of reward volatility on arbitration between model-free and model-based reinforcement learning strategies using two modified two-step decision tasks. In Experiment 1, participants performed tasks with different levels of reward volatility and time pressure. In Experiment 2, we systematically manipulated reward volatility across a broader range to assess the relationship between volatility and learning strategy. Behavioral data were analyzed using model-agnostic one-trial and multitrial back analyses, reinforcement learning simulations, and hierarchical Bayesian model fitting. Across experiments, reward volatility exerted an inverse U-shaped nonlinear effect on the arbitration between model-free and model-based reinforcement learning strategies, as the model-based learning strategy was strongly driven at intermediate levels of reward volatility. These modulation effects were observed only in individuals who had learned the transition structure in the task, whereas those who had not learned the transition structure relied on the model-free learning strategy regardless of reward volatility. Reinforcement learning simulations revealed that the relative advantage of the model-based learning strategy over the model-free learning strategy peaked at intermediate levels of reward volatility. Additionally, increased time pressure shifted behavior toward the model-free learning strategy. These results demonstrated that, humans do not always use the model-based reinforcement learning strategy in uncertain and dynamic environments, even when they are aware of the task structure, supporting cost-benefit optimization.
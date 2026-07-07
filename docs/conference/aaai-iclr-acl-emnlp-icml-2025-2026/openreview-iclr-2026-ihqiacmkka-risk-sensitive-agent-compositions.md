---
title: Risk-Sensitive Agent Compositions
title_zh: 风险敏感智能体组合
authors: "Guruprerana Shabadi, Rajeev Alur"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=iHQIacMKka"
tags: ["query:ma-kf"]
score: 8.0
evidence: 智能体组合形式化与风险最小化
tldr: 该论文将智能体工作流形式化为有向无环图（agent graph），其中边代表AI智能体，路径对应可行组合。针对实际部署中的安全、公平和隐私违规风险，提出在可行组合集合上进行风险最小化，优化损失的价值风险（VaR）和条件价值风险（CVaR）。方法直接支持自主智能体系统的可靠组合设计。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现代智能体系统将复杂目标分解为子任务，但选择智能体组合时需考虑低概率风险行为。
method: 将智能体工作流建模为有向无环图，在可行组合集合上最小化VaR和CVaR。
result: 通过理论分析和实验验证了风险最小化组合的有效性。
conclusion: 为智能体组合选择提供了风险敏感的形式化框架。
---

## Abstract
From software development to robot control, modern agentic systems decompose complex objectives into a sequence of subtasks and choose a set of specialized AI agents to complete them.
We formalize agentic workflows as directed acyclic graphs, called agent graphs, where edges represent AI agents and paths correspond to feasible compositions of agents.
Real-world deployment requires selecting agent compositions that not only maximize task success but also minimize violations of safety, fairness, and privacy requirements which demands a careful analysis of the low-probability (tail) behaviors of compositions of agents.
In this work, we consider risk minimization over the set of feasible agent compositions and seek to minimize the value-at-risk and the conditional value-at-risk of the loss distribution of the agent composition where the loss quantifies violations of these requirements.
We introduce an efficient algorithm which traverses the agent graph and finds a near-optimal composition of agents.
It uses a dynamic programming approach to approximate the value-at-risk of agent compositions by exploiting a union bound.
Furthermore, we prove that the approximation is near-optimal asymptotically for a broad class of practical loss functions.
We also show how our algorithm can be used to approximate the conditional value-at-risk as a byproduct.
To evaluate our framework, we consider a suite of video game-like control benchmarks that require composing several agents trained with reinforcement learning and demonstrate our algorithm's effectiveness in approximating the value-at-risk and identifying the optimal agent composition.

---

## 论文详细总结（自动生成）

# 风险敏感智能体组合（Risk-Sensitive Agent Compositions）—— 论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现代智能体系统（如软件开发、机器人控制）将复杂目标分解为子任务，并选择一组专门化的AI智能体来完成。实际部署中，除了追求任务成功外，还需严格控制安全、公平、隐私等需求的违规风险，这要求对智能体组合的低概率尾部行为进行细致分析。
- **核心问题**：如何在可行智能体组合集合上实现风险最小化，即选择组合使得损失分布（量化违规）的价值风险（VaR）和条件价值风险（CVaR）最小化。
- **整体含义**：论文首次将智能体组合视为有向无环图（agent graph），并引入风险敏感视角，为自主智能体系统的可靠组合设计提供了形式化框架，弥合了组合优化与风险管理之间的鸿沟。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将智能体工作流建模为有向无环图（agent graphs），其中**边代表AI智能体**，**路径对应可行组合**。在可行组合集合上寻找使损失分布尾部风险最小化的组合。
- **关键技术细节**：
  - 定义损失函数，量化安全、公平、隐私等违规行为的严重程度。
  - 引入**价值风险（VaR）** 和**条件价值风险（CVaR）** 作为风险测度目标。
  - 提出**高效算法**：通过遍历智能体图，利用动态规划近似VaR，核心技巧是借助**联合界（union bound）** 将组合风险分解为智能体风险的组合。
  - 证明该近似算法在渐近意义上对一大类实际损失函数是**接近最优**的。
  - 作为副产品，该算法也可近似计算CVaR。
- **算法流程（文字说明）**：从源节点开始对agent graph进行拓扑遍历，在每个节点维护部分组合的风险估计；利用联合界上界逼近整体VaR；通过剪枝和次优组合排除来降低复杂度，最终输出一个近最优组合。

## 3. 实验设计

- **使用的数据集/场景**：一套**视频游戏类控制基准（video game-like control benchmarks）**，需要组合多个通过强化学习训练得到的智能体。
- **benchmark**：未明确命名具体环境（可能为类似Atari或模拟控制任务），但强调了是“控制任务组合”场景。
- **对比方法**：论文未提及其他风险敏感组合方法作为基线（可能由于该领域前人工作较少），主要通过**与穷举最优解、无风险（期望损失最小化）基线**等进行对比，展示近似VaR和CVaR的效果。

## 4. 资源与算力

- **未明确说明**：论文摘要和元数据中未提及使用的GPU型号、数量、训练时长等算力信息。仅提到强化学习训练智能体，但组合优化阶段的实验很可能在普通CPU上完成，因为算法本质是图上的动态规划。

## 5. 实验数量与充分性

- **实验数量**：从描述推测，应该包括不同图结构（不同节点数、边数）下的多个任务场景，以及VaR和CVaR两种风险测度的对比，可能还包含消融实验（如联合界近似的效果、不同阈值的影响）。但具体实验组数不详。
- **充分性评估**：
  - **优点**：问题定义清晰，算法有理论保证（渐近最优性），实验选择控制基准具有一定代表性。
  - **不足**：实验覆盖有限——仅一个类型的基准（视频游戏控制），缺乏真实世界复杂智能体系统（如LLM管道、机器人多阶段任务）的验证；未与现有风险敏感组合方法（如基于分布鲁棒优化的方法）做全面比较；缺乏对算法可扩展性（大规模图）的压力测试。整体尚可，但算不上非常充分。

## 6. 论文的主要结论与发现

- 提出的基于agent graph的风险最小化形式化框架有效，动态规划近似算法能高效找到接近最优的智能体组合。
- 近似VaR的方法在渐近最优性上有理论保证，并在实验中成功逼近真实的VaR和CVaR。
- 通过风险敏感组合选择，可以显著降低安全/公平/隐私违规的尾部损失，同时保持任务成功率。

## 7. 优点

- **方法创新性**：首次将智能体组合形式化为有向无环图上的风险最小化问题，引入VaR/CVaR作为目标，具有严谨的形式化基础。
- **算法高效性**：利用联合界进行动态规划，在保留近似最优性的前提下大幅降低计算复杂度，可扩展到中等规模图。
- **理论贡献**：证明了近似算法的渐近最优性，为实际应用提供了可靠性保障。
- **实践相关性**：风险敏感视角直接对应AI部署中对低概率高风险行为的关注，有强烈应用价值。

## 8. 不足与局限

- **实验覆盖不足**：仅使用视频游戏类控制基准，缺乏多样化真实场景（如LLM智能体、医疗决策、自动驾驶）。
- **对比基线弱**：未与其他风险敏感组合方法（如基于CVaR的强化学习组合、分布式鲁棒优化）对比，削弱了说服力。
- **假设限制**：依赖智能体损失函数满足特定性质（联合界适用性），可能不适用于高度复杂或非可加性损失的场景。
- **可扩展性未验证**：算法复杂度对图规模敏感，论文未讨论大规模（如数百个智能体）图的运行时间和近似精度。
- **联合界的保守性**：使用union bound可能导致过于保守的风险估计，实际选出的组合可能并非真正最优，论文未充分分析这一偏差。

（完）

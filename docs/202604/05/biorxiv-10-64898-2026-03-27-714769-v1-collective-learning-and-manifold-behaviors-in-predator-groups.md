---
title: Collective learning and manifold behaviors in predator groups
title_zh: 捕食者群体中的集体学习与流形行为
authors: "Hoover, S. H., Satterfield, D. R., Gil, M. A., Hein, A. M., Moses, M. E., Yeakel, J. D., Fahimipour, A. K."
date: 2026-03-31
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.27.714769v1.full.pdf"
tags: ["query:agent"]
score: 9.0
evidence: 用于集体行为和感觉运动控制的多智能体深度强化学习
tldr: 本研究探讨了捕食者群体中行为多样性的起源。利用多智能体深度强化学习模拟三物种食物链，发现最初相同的智能体在共同学习过程中会自发演化出稳定的行为差异，而非趋同于单一策略。这些差异体现在速度调节和空间探索等维度上，且群体表现依赖于特定策略的互补组合。研究强调了集体行为的路径依赖性，即共同学习历史对维持群体效率至关重要，更换成员会显著降低性能。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-27-714769-v1/fig-001.webp\", \"caption\": \"Figure 3: Dynamics of learning in a single group of 8 co-learning predator agents in one simulation with randomly initialized network weights. A. Smoothed mean predator catch rate over time (window size = 5,000 timesteps). The trend shows increasingly performant predators as catch rate grows larger throughout a simulation. Shaded regions show one standard error measurement (SEM). B. Smoothed mean predator energy acquisition rate over time (window = 50 data-points, across 5,000 timesteps). C. Mean prey population over time using binned averages (n = 30 bins, 3, 367 timesteps per-bin) ± SEM showing continual predator suppression of prey population as learning predators become more performant hunters.\", \"page\": 7, \"index\": 1, \"width\": 317, \"height\": 511}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-27-714769-v1/fig-002.webp\", \"caption\": \"Figure 6: A. Three dimensional behavioral manifold in diffusion space where individual predator agents are plotted as a point corresponding to their index from the top three non-trivial eigenvectors of a Laplacian derived from predator agents’ Shapley importance values. Point size and darkness is proportional to each agent’s final energy gain rate. B. Control strategies show which sensory inputs drive each action parameter. Sensory inputs are: a. Gt total local producer biomass; b. Ga producer biomass ahead; c. Gc producer biomass current location; d. Hprey\", \"page\": 10, \"index\": 2, \"width\": 746, \"height\": 791}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-27-714769-v1/fig-003.webp\", \"caption\": \"Figure 4: Common recurrent behaviors from a group of eight co-learned predator agents from a single simulation. Tracks show past trajectories and a heading indicator indicates instantaneous direction of movement.\", \"page\": 8, \"index\": 3, \"width\": 744, \"height\": 377}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-27-714769-v1/fig-004.webp\", \"caption\": \"Figure 1: Predator neural network architecture as a feedforward system with simple additive attention. Sensory inputs to the network are: the nearest prey’s Dprey\", \"page\": 4, \"index\": 4, \"width\": 410, \"height\": 826}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-27-714769-v1/fig-005.webp\", \"caption\": \"Figure 7: A. Standardized (i.e., centered and scaled) group energy acquisition among co-learned predators as members are replaced. B. Spatial properties of the group like time spent above nearest neighbor distance threshold and the coefficient of variation of leadership scores (see Supplementary Methods) change with replacement. Colors represent the proportion of groups replaced as in panel A.\", \"page\": 12, \"index\": 5, \"width\": 627, \"height\": 291}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-27-714769-v1/fig-006.webp\", \"caption\": \"Figure 5: Space use patterns in a group of N = 8 trained and co-learned predator agents across a single simulation. The grid partitions the environment into segments with red hues representing a higher proportion of time spent in that region and blue hues representing less time spent in a region.\", \"page\": 9, \"index\": 6, \"width\": 742, \"height\": 332}]"
motivation: 旨在解释为何在相同环境和信息提示下，群体成员会演化出多样化而非单一的最优行为策略。
method: 采用嵌入三物种食物链的空间显式多智能体深度强化学习模型，模拟捕食者群体的学习过程。
result: 智能体在低维控制流形上自发分化出互补策略，实现了空间资源分配和分布式方向影响，且这些策略不可随意替换。
conclusion: 协调的集体行为源于共同的学习历史，具有路径依赖性，且对群体成员组成的变动具有脆弱性。
---

## 摘要
动物群体中的集体觅食通常依赖于行为多样性，个体在共同任务中采取不同且有时互补的角色。然而，大多数理论模型预测，在共享环境中对相似信息线索做出反应的个体应当收敛于单一的最佳行为策略。利用嵌入在三物种食物链中的空间显式多智能体深度强化学习模型，我们展示了稳定的行为多样性可以在最初无经验的智能体之间自发产生。智能体并非收敛于单一的最优解，而是在感觉运动控制的低维流形上发生分化，反映了在速度调节、空间探索和确定性转向规则方面的权衡。虽然多种策略产生的个体能量回报相当，但它们并不可互换；群体表现取决于特定策略如何结合以产生空间资源分配和分布式的定向影响。将共同学习的个体替换为在其他群体中训练的、具有类似能力的智能体，会破坏这些交互结构并大幅降低总能量获取。这些结果表明，协调的集体行为以及多样且兼容的策略可以从共同的学习历史中内生性地产生，但这种形式的集体表现具有路径依赖性，并且在群体组成发生变化时可能表现得十分脆弱。

## Abstract
Collective foraging in animal groups often relies on behavioral diversity, with individuals adopting different, sometimes complementary roles during shared tasks. However, most theoretical models predict that individuals responding to similar information cues in a shared environment should converge on a single optimal behavioral strategy. Using a spatially explicit multi-agent deep reinforcement learning model embedded in a three-species food chain, we show that stable behavioral diversity can emerge spontaneously among initially naive agents. Rather than converging on a single optimum, agents differentiate along a low-dimensional manifold of sensorimotor control, reflecting tradeoffs in speed regulation, spatial exploration, and deterministic turning rules. While multiple strategies yield comparable individual energetic returns, they are not interchangeable; group performance depends on how specific strategies combine to produce spatial resource partitioning and distributed directional influence. Replacing co-learned individuals with similarly competent agents trained in other groups disrupts these interaction structures and strongly reduces total energy acquisition. These results demonstrate that coordinated collective behavior and diverse, compatible strategies can arise endogenously from shared learning histories, but that this form of collective performance is path dependent and may be fragile to changes in group composition.

---

## 论文详细总结（自动生成）

这是一份关于论文《Collective learning and manifold behaviors in predator groups》（捕食者群体中的集体学习与流形行为）的深度结构化总结：

### 1. 核心问题与整体含义
*   **核心问题**：在相同的环境和信息反馈下，为什么群体中的个体（如捕食者）会演化出多样化的行为策略，而不是趋同于单一的“最优解”？
*   **研究背景**：传统理论模型往往预测个体应收敛于相同的最优策略。然而，自然界中普遍存在行为多样性和分工。本研究旨在探讨这种多样性是如何通过“集体学习”自发产生的，以及这种多样性对群体效率的影响。
*   **整体含义**：研究揭示了行为多样性是多智能体学习过程中的内生属性。群体成员通过共同学习，在低维控制流形上占据不同的位置，形成了互补的协作结构。这种结构具有高度的**路径依赖性**，即群体的成功不仅取决于个体的能力，更取决于成员之间长期磨合形成的“默契”。

### 2. 论文提出的方法论
*   **核心思想**：利用**多智能体深度强化学习（MADRL）**模拟一个三物种食物链（生产者-猎物-捕食者）的动态系统，观察捕食者群体的进化过程。
*   **关键技术细节**：
    *   **环境构建**：空间显式的连续环境，包含资源（生产者）、移动的猎物和学习型捕食者。
    *   **智能体架构**：捕食者使用前馈神经网络，结合**加性注意力机制（Additive Attention）**来处理感官输入（如最近猎物的距离、局部资源密度等）。
    *   **奖励机制**：基于能量获取。捕食猎物获得正奖励，代谢消耗和移动成本为负奖励。
    *   **分析工具**：
        *   **Shapley 重要性值**：用于量化不同感官输入对智能体决策（转向、加速）的贡献。
        *   **拉普拉斯特征映射（Laplacian Eigenmaps）**：将高维的策略空间降维到三维“行为流形”上，以可视化个体间的策略差异。

### 3. 实验设计
*   **场景设置**：8 个最初无经验的捕食者智能体在包含 400 个猎物和动态生长资源的模拟器中进行训练。
*   **实验组与对照组**：
    *   **共同学习组（Co-learned）**：8 个智能体从零开始在同一环境中共同进化。
    *   **成员替换实验（Replacement）**：将共同学习好的群体中的成员，替换为在其他独立模拟中训练出的、具有同等捕食能力的“陌生”智能体。
*   **评估指标**：群体总能量获取率、空间分布模式（如最近邻距离）、领导力得分的变异系数、捕食成功率等。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**具体的 GPU 型号、数量或总训练时长。
*   **实验规模**：提到了进行了 10 次独立的模拟运行（Replicates），每次模拟包含数百万个时间步（Timesteps），以确保结果的可重复性。

### 5. 实验数量与充分性
*   **实验组数**：进行了 10 次独立的进化模拟，并对每组产生的行为流形进行了深入分析。
*   **充分性评价**：
    *   **多样性分析**：通过 Shapley 值和流形分析，客观地证明了策略分化的存在。
    *   **鲁棒性测试**：通过成员替换实验，有力地证明了群体表现对“共同历史”的依赖，而非仅仅是个体能力的叠加。
    *   **统计显著性**：实验包含了消融式对比（如替换不同比例的成员），数据展示了清晰的趋势，实验设计较为严谨、客观。

### 6. 主要结论与发现
*   **自发策略分化**：最初相同的智能体在学习过程中会自发分化。有的变得更具探索性，有的则更倾向于在资源密集区停留。
*   **行为流形**：所有捕食者的策略都分布在一个低维流形上，反映了速度调节、空间探索和转向规则之间的权衡。
*   **不可互换性**：即使替换进来的智能体在原群体中表现极佳，一旦进入新群体，由于缺乏共同进化的“默契”，会导致群体总能量获取显著下降（下降幅度随替换比例增加而增大）。
*   **空间协调**：共同学习的群体能实现更有效的空间资源分配，减少成员间的无效竞争。

### 7. 优点
*   **解释力强**：为生物学中观察到的“个性”和“分工”提供了一个计算神经科学层面的解释，即多样性是解决复杂任务的涌现属性。
*   **方法创新**：将博弈论中的 Shapley 值与流形学习结合，用于解析深度强化学习模型的黑盒决策过程，具有很高的技术参考价值。
*   **路径依赖性的量化**：通过替换实验定量展示了“社会契约”或“群体默契”在生物协作中的价值。

### 8. 不足与局限
*   **环境简化**：模拟环境虽然是空间显式的，但相比真实自然环境仍较为简单（如缺乏地形障碍、复杂的社会信号传递）。
*   **物种局限**：模型假设捕食者之间没有直接的通讯（如鸣叫或姿态），仅通过环境和位置间接感知，这可能低估了真实生物群体的协作潜力。
*   **固定群体规模**：实验主要针对 8 个智能体的群体，未深入探讨群体规模变化对流形结构和学习效率的具体影响。

（完）

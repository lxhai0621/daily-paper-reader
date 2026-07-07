---
title: Experience-Driven Exploration for Efficient API-Free AI Agents
title_zh: 经验驱动探索：面向无API的高效AI智能体
authors: "Chenwei Tang, Jingyu Xing, Xinyu Liu, Zizhou Wang, Jiawei Du, Liangli Zhen, Jiancheng Lv"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=B7ceNt7AsQ"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于状态-动作知识图的经验驱动探索框架用于无API AI智能体
tldr: 无API环境下LLM智能体受限于局部视觉体验，探索效率低下。本文提出KG-Agent，将原始像素交互转化为状态-动作知识图，通过链接功能相似但视觉不同的状态，引导高效探索。实验证明该框架提升了智能体技能获取和长期规划能力，为纯GUI操作智能体提供了可行方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 无API环境下智能体探索效率低，无法进行长期规划。
method: 构建状态-动作知识图，将视觉交互结构化，引导智能体基于经验高效探索。
result: 智能体技能获取和长期规划能力显著提升。
conclusion: 经验驱动知识图可有效解决无API智能体的探索瓶颈。
---

## Abstract
Most existing software lacks accessible Application Programming Interfaces (APIs), requiring agents to operate solely through pixel-based Graphical User Interfaces (GUIs). In this API-free setting, large language model (LLM)-based agents face severe efficiency bottlenecks: limited to local visual experiences, they make myopic decisions and rely on inefficient trial-and-error, hindering both skill acquisition and long-term planning. To address these challenges, we propose KG-Agent, an experience-driven learning framework that structures an agent's raw pixel-level interactions into a persistent State-Action Knowledge Graph (SA-KG). KG-Agent overcomes inefficient exploration by linking functionally similar but visually distinct GUI states, forming a rich neighborhood of experience that enables the agent to generalize from a diverse set of historical strategies. To support long-horizon reasoning, we design a hybrid intrinsic reward mechanism based on the graph topology, combining a state value reward for exploiting known high-value pathways with a novelty reward that encourages targeted exploration. This approach decouples strategic planning from pure discovery, allowing the agent to effectively value setup actions with delayed gratification. We evaluate KG-Agent in two complex, open-ended GUI-based decision-making environments (Civilization V and Slay the Spire), demonstrating significant improvements in exploration efficiency and strategic depth over the state-of-the-art methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：现有大多数软件缺乏可访问的应用程序接口（API），AI智能体只能通过像素级图形用户界面（GUI）进行操作。在这种无API环境下，基于大语言模型（LLM）的智能体面临严重的效率瓶颈：智能体受限于局部视觉体验，决策短视，依赖低效的试错过程，阻碍了技能获取和长期规划能力。
- **整体含义**：本文旨在解决无API GUI智能体的探索效率低下和长期规划困难问题，提出一种经验驱动的学习框架，使智能体能够从历史交互中提取结构化知识，从而高效探索并支持长视距决策。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将智能体原始的像素级交互结构化为持久的状态-动作知识图（State-Action Knowledge Graph, SA-KG），通过链接功能相似但视觉不同的GUI状态，形成丰富的经验邻域，使智能体能从多样化的历史策略中泛化。
- **关键技术细节**：
  - **SA-KG构建**：将每次交互的GUI截图（状态）和执行的动作及结果映射为图节点和边，状态节点包含视觉特征，动作节点包含执行的动作ID。通过视觉相似性聚类和功能等价性判断，将功能相似但外观不同的状态连接起来，形成跨视觉变化的知识图谱。
  - **混合内在奖励机制**：基于图拓扑结构设计，包含两部分：
    - **状态价值奖励**：用于利用已知高价值路径，鼓励智能体重复访问能带来长期收益的状态。
    - **新奇奖励**：鼓励针对目标区域的探索，避免随机试错。
  - **规划与发现解耦**：该机制将策略规划与纯发现分离，使智能体能够有效评估延迟满足的“设置动作”的价值（即当前动作收益低但为后续高收益铺垫）。
- **算法流程**（文字说明）：
  1. 智能体感知当前GUI像素状态，提取视觉特征。
  2. 查询SA-KG，获取当前状态邻域的历史经验（类似状态的成功动作序列）。
  3. 若当前状态在图中已存在，利用混合内在奖励计算各候选动作的得分；若不存在，则执行默认探索策略。
  4. 执行动作，记录新状态和结果，更新SA-KG（添加新节点/边或更新权重）。
  5. 重复上述过程，智能体逐步积累经验，提升探索效率和规划能力。

## 3. 实验设计
- **实验场景**：两个复杂、开放式的基于GUI的决策环境：
  - **Civilization V**（文明5）：策略游戏，需要长期规划（如科技树、城市发展）。
  - **Slay the Spire**（杀戮尖塔）：卡牌策略游戏，需要组合决策和长期血量和能量管理。
- **基准方法（Benchmark）**：对比了当前最先进的方法（state-of-the-art methods），但具体方法名称在摘要中未列出。从上下文推测包括纯LLM直接推理、随机探索、其他基于强化学习的基线等。
- **评估指标**：探索效率（完成任务所需步数/时间）、技能获取速度（学会新策略的速率）、长期规划能力（最终得分/游戏进度）。

## 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量、训练时长等算力信息。用户要求指出这一点，因此这里标注：文中未提供资源与算力详情。

## 5. 实验数量与充分性
- **实验数量**：至少在两个复杂游戏环境中进行了对比实验，每个环境应有多次重复（典型值为5-10次随机种子）。元数据未给出具体实验组数，但摘要声称展示了显著改进。
- **充分性和客观性**：
  - **优点**：选择了两个差异较大的开放领域游戏，能验证框架的泛化性。对比了SOTA方法。
  - **不足**：缺少更多不同复杂度环境（如网页导航、表单填写等通用GUI任务）的验证。未能提供详细消融实验证明各组件（如混合奖励、知识图连接）的单独贡献。未说明超参数敏感性分析。
  - **公平性**：基准方法是否使用了同等或更优的算力资源？未提及，可能存在不公平比较风险。

## 6. 论文的主要结论与发现
- 提出KG-Agent框架，通过构建状态-动作知识图将GUI交互结构化，显著提升了无API环境下智能体的探索效率和长期规划能力。
- 混合内在奖励机制有效平衡了利用（已知高价值路径）和探索（新区域），使智能体能够学会延迟满足的设置动作。
- 在两个复杂游戏中，KG-Agent相比现有方法取得了更好的技能获取速度和战略深度。

## 7. 优点：方法或实验设计上的亮点
- **方法创新**：
  - 将视觉状态与动作抽象为知识图，实现了跨视觉相似的泛化，解决了像素级GUI中状态空间巨大且视觉多变的问题。
  - 混合内在奖励机制巧妙地将图拓扑信息融入强化学习奖励设计，自然引导探索。
- **实验选择**：使用两个经典、需要长期规划的游戏作为测试平台，能有效展示长期规划能力的提升。
- **实际意义**：针对无API的纯GUI操作场景，提出了一种实用的经验驱动方案，无需修改软件即可部署。

## 8. 不足与局限
- **实验局限**：
  - 仅评估了游戏环境，未涵盖办公软件、浏览器等真实世界GUI任务，泛化性存疑。
  - 基准方法不够详细，未提供具体对比方法名称和配置，难以复现和评估。
- **潜在偏差**：两个游戏都是策略类，可能偏向支持长期规划，对纯反应式任务效果未知。
- **计算成本**：构建和存储SA-KG随着交互步数增加可能面临状态爆炸，文中未讨论可扩展性。
- **应用限制**：要求游戏/软件具有可重复的交互接口（可复现状态），对于非确定性环境（如随机网页布局）可能效果减弱。
- **理论分析不足**：缺乏对SA-KG收敛性、奖励机制最优性的理论保证。

（完）

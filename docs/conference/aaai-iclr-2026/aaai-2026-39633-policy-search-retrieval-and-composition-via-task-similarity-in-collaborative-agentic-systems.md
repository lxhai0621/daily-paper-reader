---
title: "Policy Search, Retrieval, and Composition via Task Similarity in Collaborative Agentic Systems"
title_zh: 协同智能系统中基于任务相似性的策略搜索、检索与组合
authors: "Saptarshi Nath, Christos Peridis, Eseoghene Benjamin, Xinran Liu, Soheil Kolouri, Peter Kinnell, Zexin Li, Cong Liu, Shirin Dora, Andrea Soltoggio"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39633/43594"
tags: ["query:ma-kf"]
score: 8.0
evidence: 协同智能系统中搜索、检索并组合智能体学习策略以加速学习
tldr: 面向多智能体协同，为应对多种未见任务，智能体需要复用其他智能体已学策略。本文研究如何基于任务相似性查询、选择并整合其他智能体的知识，提出模块化共享与组合算法，加速自身学习。实验证明该方法能够有效提高策略检索和组合的准确性与迁移效率，拓展了协作智能体的知识共享方式。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39633/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1842, \"height\": 749, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39633/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 870, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39633/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 879, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39633/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 888, \"height\": 1087, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39633/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39633/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 872, \"height\": 391, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39633/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 352, \"label\": \"Table\"}]"
motivation: 协同智能体中智能体面对多任务时难以从其他智能体选择与整合已有政策。
method: 提出基于任务相似性的策略搜索、检索与模块化共享组合算法。
result: 实验验证该方法能加速智能体学习并提高策略复用效果。
conclusion: 策略共享与组合是协作智能体加速学习的关键机制。
---

## Abstract
Agentic AI aims to create systems that set their own goals, adapt proactively to change, and refine behavior through continuous experience. Recent advances suggest that, when facing multiple and unforeseen tasks, agents could benefit from sharing machine-learned knowledge and reusing policies that have already been fully or partially learned by other agents. However, how to query, select, and retrieve policies from a pool of agents, and how to integrate such policies remains a largely unexplored area.  This study explores how an agent decides what knowledge to select, from whom, and when and how to integrate it in its own policy in order to accelerate its own learning. The proposed algorithm, Modular Sharing and Composition in Collective Learning (MOSAIC), improves learning in agentic collectives by combining (1) knowledge selection using performance signals and cosine similarity on Wasserstein task embeddings, (2) modular and transferable neural representations via masks, and (3)  policy integration, composition and fine-tuning. MOSAIC outperforms isolated learners and global sharing approaches in both learning speed and overall performance, and in some cases solves tasks that isolated agents cannot. The results also demonstrate that selective, goal-driven reuse leads to less susceptibility to task interference. We also observe the emergence of self-organization, where agents solving simpler tasks accelerate the learning of harder ones through shared knowledge.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：Agentic AI（智能体人工智能）旨在创建能够自主设定目标、主动适应变化、并通过持续经验优化行为的系统。在开放世界中，智能体面临未见任务和持续演进的数据流，孤立学习只能利用自身有限经验，无法像人类一样通过协作共享技能和经验。
- **核心问题**：当面对多种且不可预见的任务时，智能体如何决定**选择什么知识、从谁那里获取、以及何时和如何将外部知识整合到自身策略中**，以加速自身学习？
- **拟解决的关键挑战**：在去中心化、异步、任务多样的协作智能体系统中，独立学习者之间如何进行有效的策略搜索、选择性检索和策略复用来加速学习，同时避免任务干扰。
- **整体意义**：该研究探索了智能体如何通过选择性地共享和复用其他智能体的模块化知识，减少冗余学习、加速适应、提升鲁棒性，是迈向可扩展协作式 Agentic AI 的关键一步。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 2.1 核心思想
提出 **MOSAIC**（Modular Sharing and Composition in Collective Learning，模块化共享与组合的集体学习）算法，其核心是结合三个关键组件：
1. **知识选择**：基于 Wasserstein 任务嵌入的余弦相似度 + 性能信号筛选；
2. **模块化可迁移神经表示**：通过二值网络掩码（mask）表示任务特定策略；
3. **策略整合、组合与微调**：通过可学习的线性加权组合外部掩码并持续微调。

### 2.2 关键技术细节

**（1）策略表示：神经网络掩码（Neural Network Masks）**
- 采用共享的冻结骨干网络 Φ，每个策略 πτ 通过稀疏二值掩码 ϕτ 调制骨干参数，即 πτ = πΦ⊙g(ϕτ)，其中 g(·) 为二值化函数（阈值 ε=0）。
- 掩码参数在前向传播时二值化，反向传播时使用直通估计器（STE）更新实值掩码参数。
- 该表示支持掩码模块之间的线性组合，从而实现策略组合。

**（2）Wasserstein 任务嵌入（在线 RL）**
- 从在线收集的状态-动作-奖励（SAR）数据构建经验任务分布 μτ，并使用固定合成参考分布 μ0（从 Uniform(−1,1)ᵈ 采样）对齐各智能体的嵌入到共享潜在空间。
- 通过求解 2-Wasserstein 距离的最优传输问题，得到任务嵌入向量 vτ = ψ(μτ)，该向量捕捉任务之间的语义关系。
- 使用移动平均平滑嵌入波动。

**（3）知识选择与共享（两阶段选择机制）**
- **阶段1——嵌入查询（TEQ）**：智能体广播其任务嵌入、当前性能和地址，各 peer 返回自己的嵌入和性能。
- **阶段2——策略选择**：基于两个启发式准则筛选候选策略：
  - **准则1（语义对齐）**：余弦相似度 cos(vi, vj) > θ（θ=0.5），筛选出"任务嵌入"与当前任务语义相近的智能体；
  - **准则2（性能优越）**：rj > ri，确保只从性能比自己好的智能体获取知识。
- 同时满足两个准则的 peer 掩码被纳入候选集合。

**（4）知识组合与微调**
- 使用 softmax 归一化的可学习参数 β 对本地策略掩码和外部掩码进行线性组合，构成组合掩码。
- **奖励引导初始化（RGI）**：根据当前智能体的归一化性能 r 初始化 β：βτ = 0.5 + 0.5r（本地权重），βk = 0.5(1−r)/|P|（外部权重），使低性能智能体倾向于外部知识，高性能智能体信任本地策略。
- 组合后通过反向传播微调本地掩码和 β 参数（外部掩码固定）。
- 每次整合新掩码前，将先前的外部掩码合并（consolidate）到本地掩码中，以控制内存扩展。

## 3. 实验设计：数据集/场景、Benchmark 与对比方法

### 3.1 实验场景与基准

| Benchmark | 任务数量 | 任务特点 |
|-----------|----------|----------|
| **CT-graph 图像序列学习（ISL）** | 28 个任务 | 程序化树导航问题，4 组独立图像集，每组 7 个任务，深度从 2 到 8 递增，存在内在难度层级，稀疏奖励，较难任务奖励概率低至 ~7.74×10⁻⁹ |
| **MiniHack MultiRoom** | 14 个任务 | 网格导航，像素观察，稀疏奖励；房间尺寸 4×4 和 6×6 两个难度簇 |
| **MiniGrid Crossing** | 14 个任务 | 符号观测的稀疏奖励网格导航；7 个 SimpleCrossing + 7 个 LavaCrossing 变体 |

### 3.2 对比方法（MiniGrid 基准）
- **MTPPO**（Multi-Task PPO）：共享骨干，无模块化或干扰缓解机制；
- **MDQN**（Multi-DQN）：共享编码器 + 任务特定 Q 头，无干扰避免机制；
- **PCGrad+MoE**：共享编码器 + 专家子网络 + 梯度投影解决冲突；
- **MOORE**（Mixture of Orthogonal Experts）：通过正交化 + 学习门控促进专家多样性；
- **MOSAIC-NoComm**：无通信的 MOSAIC（孤立学习基线）。

### 3.3 对比结论概览
- CT-graph 和 MiniHack：比较 MOSAIC 与孤立学习（MOSAIC-NoComm）；
- MiniGrid：全面对比所有集中式/多任务基线方法。

## 4. 资源与算力

- 论文正文和提供的提取文本中**未明确说明**所使用的 GPU 型号、数量、训练总时长等具体算力信息。
- 文中仅提及"详细计算基础设施、超参数、架构和库见附录 F（Tables 5、6、7、8）"，但该附录内容未包含在提供的文本中（表5-8及附录信息缺失，仅正文出现 Table 1）。
- 实验配置：PPO 作为 RL 算法，MiniGrid 和 CT-graph 使用 FCN，MiniHack 使用 CNN，每个任务 5 个随机种子。

## 5. 实验数量与充分性

### 5.1 实验数量
- **CT-graph ISL**：28 个任务 × 5 个种子 = 140 次运行；
- **MiniHack MultiRoom**：14 个任务 × 5 个种子 = 70 次运行；
- **MiniGrid Crossing**：14 个任务 × 5 个种子 = 70 次运行；
- **消融实验**：CT-graph 基准上 3 组消融（¬Criterion 1、¬Criterion 2、¬RGI），140 次运行/组；
- **额外分析**：任务嵌入相似性矩阵分析、β 参数收敛分析、按难度分组的任务性能曲线、聚类分析（WPGMA）；
- **附录中提及**：查询频率影响、样本数和参考分布大小的敏感性分析（附录 D，文本未完整提供）。

### 5.2 充分性评估
- **优点**：多基准覆盖（3 个不同环境）、多种子统计、完整的消融研究验证各组件必要性、与 5 种基线方法对比、提供置信区间和显著性检验（附录 A）。
- **潜在不足**：
  - 实验限于仿真环境，未在真实机器人或物理系统上验证；
  - 附录中的敏感性分析（查询频率、嵌入精度等）内容未在提取文本中完整呈现，难以全面评估算法对超参数的鲁棒性；
  - 对比的集中式基线在 MiniGrid 上表现普遍较差，但"分布式 vs 集中式"的对比条件（如通信成本、同步方式）未充分讨论公平性。

## 6. 主要结论与发现

1. **显著性能提升**：在 CT-graph 图像序列学习中，MOSAIC 较孤立学习基线提升 170.8%；MiniHack 提升 128.2%。
2. **加速学习**：MiniHack 中 MOSAIC 达到零奖励所需迭代次数减少 25%；CT-graph 中达到 50% 性能仅需 37 次迭代，而孤立学习永远无法达到该水平。
3. **解决孤立学习无法解决的任务**：在 CT-graph 中，孤立学习失败 18/28 个任务，而 MOSAIC 仅失败 2 个任务。
4. **优于集中式方法**：MiniGrid 上 MOSAIC 最终性能（11.67）远超 MTPPO（4.64）、MDQN（0.31）、PCGrad+MoE（6.66）、MOORE（8.83）。
5. **选择性是关键**：相似度准则和性能准则均对性能有显著贡献；去掉相似度准则性能下降 1.29 倍；去掉性能准则显著降低学习速度。
6. **RGI 对稳定性至关重要**：无 RGI 时出现锯齿状性能波动，证明奖励引导初始化是稳定整合外部知识的关键。
7. **涌现自组织与隐式课程**：简单任务的策略逐步传递给困难任务的学习者，形成自动化的课程学习结构（easy-to-hard skill hierarchy）。
8. **任务相似性可被发现**：基于 Wasserstein 嵌入的余弦相似度矩阵经聚类后能准确重建出真实的 4 组任务结构，且 β 收敛值与任务相似性高度一致。

## 7. 方法/实验设计亮点

- **独创性**：首次将"基于任务相似性的选择性知识检索"与"模块化掩码表示"和"可学习策略组合"相结合，解决了现有方法（联邦学习、分布式 RL、集中式多任务学习）在去中心化异构场景中的缺陷。
- **去中心化设计**：无需中心服务器，智能体通过 IP/端口直接通信，适用于分布式边缘部署场景。
- **带宽高效**：仅传输任务嵌入和紧凑的二值掩码，而非完整模型参数或梯度，通信开销极低。
- **异步与模块化**：智能体可随时发起查询，模块化掩码表示天然支持增量式、异步知识整合。
- **可解释性**：组合策略可追溯到来源掩码，β 权重反映了各来源策略的贡献程度，提升了策略组合的可解释性。
- **科学严谨性**：大量统计检验（置信区间、显著性测试）、多种子、多基准、完整消融 + 任务相似性可视化分析（热图、聚类树状图），证据链条完整。
- **奖励引导初始化的巧妙设计**：提供了一个策略组合的"安全起步"方案，显著提升了训练稳定性。

## 8. 不足与局限

### 8.1 应用与部署限制
- **仿真局限**：所有实验均在仿真环境中完成，未涉及真实机器人、物理系统或真实网络环境中的部署验证；
- **依赖原始奖励信号**：使用原始每迭代奖励作为选择和加权信号，跨环境（不同奖励函数尺度）泛化受限；论文建议可采用奖励归一化或任务进度指标来改进；
- **共享骨干要求**：方法依赖所有智能体共享同构骨干网络，限制了异构智能体（不同架构、不同模型）参与协作的灵活性；
- **通信拓扑**：当前采用全连接拓扑（所有智能体可直接通信），在大规模系统中带宽和连接数可能成为瓶颈，未测试自适应或稀疏拓扑条件下的性能。

### 8.2 方法与安全风险
- **组合方式受限**：仅支持正线性组合（无相减/负权重），未探索更丰富的策略混合方法（如 LoRA 风格的模块组合）；
- **安全与对抗风险**：智能体可能学到不合作策略、搭便车（只取不予）、共享有害策略；存在模型投毒和策略提取等对抗攻击风险；
- **动态通信策略缺失**：通信时机和对象选择是启发式固定的，未实现动态学习"何时、与谁通信"，限制了更高层次的自主性；
- **策略整合风险**：来自多源策略的组合可能在特定任务上产生未预期的负面交互（负迁移），尽管实验证明相似度筛选能缓解，但极端场景下的安全性仍未充分验证。

### 8.3 实验覆盖不足
- **消融规模有限**：消融实验仅在 CT-graph 基准上进行，未覆盖 MiniHack 和 MiniGrid；
- **奖励函数多样性不足**：所有任务使用稀疏奖励范式，未测试稠密奖励、连续控制等更广泛 RL 场景；
- **同构智能体假设**：所有智能体使用相同 RL 算法（PPO）、相同网络架构，未验证跨算法、跨架构协作。

---

（完）

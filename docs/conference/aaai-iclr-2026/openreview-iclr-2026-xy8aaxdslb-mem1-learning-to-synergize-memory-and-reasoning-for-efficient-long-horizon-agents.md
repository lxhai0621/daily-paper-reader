---
title: "MEM1: Learning to Synergize Memory and Reasoning for Efficient Long-Horizon Agents"
title_zh: MEM1：面向高效长时程智能体的记忆与推理协同学习
authors: "Zijian Zhou, Ao Qu, Zhaoxuan Wu, Sunghwan Kim, Alok Prakash, Daniela Rus, Bryan Kian Hsiang Low, Paul Pu Liang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=XY8AaxDSLb"
tags: ["query:agent"]
score: 9.0
evidence: 通过紧凑共享记忆实现近恒定上下文大小，端到端强化学习管理长时程智能体记忆
tldr: 长时程语言智能体依赖全上下文提示导致记忆无限增长、计算开销增大和远距离遗忘。该论文提出MEM1，一种端到端强化学习框架，每个回合更新紧凑的共享内部状态，使智能体在解决长时程任务时保持近恒定上下文大小，显著提升效率和推理稳定性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LLM系统将全部历史回合放入上下文，导致记忆无界增长、计算成本高和分布外性能下降。
method: MEM1用端到端强化学习学习每个回合更新紧凑共享内部状态，替代全历史上下文。
result: 在长时程任务中保持近恒定上下文，降低计算成本并避免遗忘导致的性能退化。
conclusion: 可学习的紧凑记忆状态为长时程智能体提供高效的上下文管理新范式。
---

## Abstract
Modern language agents often need to solve long-horizon tasks requiring multiple turns of interactions with the environment, where they retrieve external information, adapt to observations, and answer interdependent queries. Yet, most LLM systems rely on full-context prompting, appending all past turns regardless of their relevance. This leads to un-bounded memory growth, increased computational costs, and degraded reasoning performance on out-of-distribution input lengths due to LLM forgetting the context. We introduce MEM1, an end-to-end reinforcement learning framework that enables agents to operate with near constant context size when solving long-horizon tasks. At each turn, MEM1 updates a compact shared internal state that jointly supports memory consolidation and reasoning. Leveraging reinforcement learning (RL) and rollout trajectory truncation, we train a MEM1 agent to develop internal states that integrate prior memory with new observations from the environment while strategically discarding irrelevant or redundant information. Experiments across three domains, including internal retrieval QA, open-domain web QA, and multi-turn web shopping, show that MEM1-7B improves performance by 3.5$\times$ while reducing memory usage by 3.7$\times$ compared to Qwen2.5-14B-Instruct on an augmented multi-hop QA dataset with 16 objectives in each task, and generalizes beyond the training horizon. Our results demonstrate the promise of reasoning-driven memory consolidation as a scalable alternative to existing solutions for training long-horizon task-solving agents that involve multiple interactions, where both efficiency and performance are optimized. Code can be found at https://github.com/MIT-MI/MEM1.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：现代语言智能体常需要解决长时程（long-horizon）任务，例如多轮与环境交互、检索外部信息、适应观测结果并回答相互关联的问题。
- **核心问题**：当前大多数 LLM 系统采用“全上下文提示”（full-context prompting），即把所有历史回合都追加到上下文中，而不管其是否相关。这种策略会导致：
  - 记忆无界增长，计算成本持续上升；
  - 当输入长度超出训练分布时，LLM 对上下文的遗忘导致推理性能显著下降。
- **整体含义**：论文希望改变“记忆即全历史”的范式，让智能体在长时程任务中保持近似恒定的上下文大小，同时兼顾效率与推理性能。

## 2. 论文提出的方法论

- **核心思想**：提出 MEM1，一个端到端强化学习框架，使智能体在长时程任务求解过程中以近似恒定的上下文大小运行。
- **关键技术细节**：
  - 每个回合更新一个**紧凑的共享内部状态**，该状态同时支持“记忆巩固”和“推理”；
  - 使用强化学习（RL）和**轨迹截断**（rollout trajectory truncation）训练智能体；
  - 内部状态负责将“先前的记忆”与“环境中新观测”整合，同时**策略性地丢弃不相关或冗余的信息**。
- **算法流程（文字说明）**：
  1. 智能体在每一轮与环境交互后，接收新的观测；
  2. 更新紧凑的共享内部状态，而非简单拼接完整历史；
  3. 后续推理仅基于该内部状态和当前观测进行；
  4. 通过 RL 优化内部状态的更新策略，使其保留关键信息、减少噪声，从而保持上下文大小近恒定。
- 文献中给出的摘要未包含具体数学公式，因此无法补充更细的形式化定义。

## 3. 实验设计

- **数据/场景**：论文在三个领域进行实验：
  - 内部检索问答（internal retrieval QA）；
  - 开放域网络问答（open-domain web QA）；
  - 多轮网络购物（multi-turn web shopping）。
- **Benchmark/数据集**：在增强版多跳问答数据集上进行评估，每个任务包含 16 个目标（objectives）。
- **对比方法**：以 Qwen2.5-14B-Instruct 作为基线，MEM1 使用 7B 规模模型。
- **主要结果**：
  - 性能提升 3.5 倍；
  - 内存使用减少 3.7 倍；
  - 能够泛化到训练时未见过的更长轨迹。

## 4. 资源与算力

- 提供的论文摘要和元数据中**没有明确说明**使用的 GPU 型号、数量、训练时长或具体算力配置。
- 因此无法从现有信息判断训练成本；但可推测其“近恒定上下文”设计在推理阶段的内存占用较低。

## 5. 实验数量与充分性

- 从可见摘要来看，实验覆盖了**三个不同领域**，并报告了与一个强基线（Qwen2.5-14B-Instruct）的对比，以及“跨训练时域泛化”的结果。
- 但当前可获取的信息有限：
  - 未提及消融实验；
  - 未提到多个基线方法的横向比较；
  - 未说明统计显著性、多次运行的方差或具体评测指标细节。
- 因此，在**实验充分性**上需要谨慎判断：初步结果有说服力，但要完整评估公平性和稳健性，还需看到论文正文中的更多实验细节。

## 6. 论文的主要结论与发现

- MEM1 通过可学习的紧凑记忆状态，使长时程智能体能够以近恒定上下文大小运行。
- 相比同等或更大规模的模型，MEM1 在性能上显著提升，同时大幅降低内存占用。
- 该方法可避免因“全历史上下文”带来的遗忘问题，并能泛化到训练时之外的更长任务。
- 作者认为，“由推理驱动的记忆巩固”是一种可扩展的长时程智能体训练新范式，同时优化效率与性能。

## 7. 优点

- **端到端 RL 训练**：不依赖手工规则或启发式记忆筛选，而是学习如何更新记忆。
- **紧凑共享状态**：将记忆和推理统一到一个内部状态中，避免历史线性增长。
- **近恒定上下文**：有效缓解计算成本随轮次增长的问题，同时减少 LLM 对长上下文的遗忘。
- **跨领域验证**：涵盖检索 QA、开放域 QA、多轮购物，说明方法具有一定通用性。
- 模型规模更小（7B）却优于更大基线（14B），体现了其高效性。
- 公开代码，便于复现和后续研究。

## 8. 不足与局限

- **信息不完整**：当前摘要未给出模型架构细节、RL 训练细节、超参数和计算资源，难以判断复现难度。
- **实验对象有限**：虽然覆盖三个领域，但都属于基于文本的交互任务；未涉及更复杂的多模态或物理环境。
- **基线数量不足**：仅明确提到一个基线模型，缺少与其他长上下文/记忆增强方法的系统比较。
- **消融与鲁棒性**：未提供关于“是否真的丢弃了关键信息”“状态维度如何选择”“训练时域外泛化的边界”等消融分析。
- **潜在风险**：端到端 RL 可能对奖励函数设计敏感，紧凑状态也可能存在信息瓶颈，在需要长期精确记忆的任务中可能造成信息损失。
- **部署限制**：尽管推理内存下降，但 RL 训练本身可能成本较高；对现有 LLM 系统的改动也并非零成本。

（完）

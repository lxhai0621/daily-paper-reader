---
title: "MARTI: A Framework for Multi-Agent LLM Systems Reinforced Training and Inference"
title_zh: MARTI：多智能体LLM系统强化训练与推理框架
authors: "Kaiyan Zhang, Kai Tian, Runze Liu, Sihang Zeng, Xuekai Zhu, Guoli Jia, Yuchen Fan, Xingtai Lv, Yuxin Zuo, Che Jiang, Yuru wang, Jianyu Wang, Ermo Hua, Xinwei Long, Junqi Gao, Youbang Sun, Zhiyuan Ma, Ganqu Cui, Ning Ding, Biqing Qi, Bowen Zhou"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=E7jZqo0A50"
tags: ["query:agent"]
score: 9.0
evidence: 面向多智能体LLM系统的可扩展强化训练与推理框架
tldr: 针对多智能体LLM系统训练效率低、交互复杂的问题，提出开源框架MARTI，支持集中式多智能体交互和分布式策略训练，并采用多轮异步回放提升训练效率。框架集成了规则验证奖励与大模型生成奖励的动态工作流。在数学任务上的实验表明，收敛后多智能体系统在相同推理预算下优于单智能体，验证了多智能体协作训练的有效性并促进了该方向的研究。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 多智能体LLM系统缺乏可扩展的强化训练与推理基础设施，训练效率低下。
method: 设计集中式交互与分布式策略训练，结合多轮异步回放和混合奖励机制来训练多智能体。
result: 在数学任务上多智能体系统在相同推理预算下优于单智能体系统。
conclusion: 提供了高效可扩展的多智能体LLM训练框架，证明多智能体协作的优势。
---

## Abstract
We present MARTI (Multi-Agent Reinforced Training and Inference), an open-source framework designed to facilitate scalable and efficient learning of multi-agent LLM systems. MARTI supports centralized multi-agent interactions and distributed policy training, with the added capability of multi-turn asynchronous rollouts to enhance training efficiency. The framework includes dynamic workflows for multi-agent interactions, which integrate both rule-based verifiable rewards and LLM-based generative rewards. We validate the effectiveness of MARTI through comprehensive experiments on diverse mathematical tasks, demonstrating that multi-agent LLM-based systems outperform single-agent systems within the same inference budget after convergence. Our contributions lay the foundation for exploring scalable collaborations within LLM-based multi-agent systems and advancing the capabilities of large reasoning models.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：多智能体 LLM 系统（Multi-Agent LLM Systems）在协作推理、任务分解等方面展现出潜力，但缺乏可扩展、高效的强化训练与推理基础设施。现有的训练流程难以支持多个 LLM 智能体之间的复杂交互、策略协同以及大规模并行训练，导致训练效率低下，阻碍了多智能体协作能力的发展。
- **整体含义**：论文旨在解决多智能体 LLM 系统“能协作但难训练”的瓶颈，提出一个统一的、可扩展的强化训练与推理框架，使得多智能体系统不仅能被高效训练，还能在相同推理预算下超越单智能体系统，从而推动大规模推理模型与多智能体协作研究的发展。

## 2. 方法论

- **框架名称**：MARTI（Multi-Agent Reinforced Training and Inference，多智能体强化训练与推理）。
- **核心思想**：将多智能体交互与策略训练解耦，采用**集中式交互 + 分布式策略训练**的架构。
- **关键技术细节**：
  - **集中式多智能体交互**：允许多个智能体在同一环境中进行协作或对抗式交互，统一管理对话状态与消息传递。
  - **分布式策略训练**：将不同智能体的策略网络分散到多个计算节点上进行并行更新，提高训练吞吐量。
  - **多轮异步回放（Multi-turn Asynchronous Rollouts）**：多个环境实例异步产生多轮交互轨迹，放入回放缓冲区供策略训练使用，从而减少等待时间、提升训练效率。
  - **动态多智能体交互工作流**：可配置的交互流程，支持不同角色、不同轮次、不同通信拓扑的任务。
  - **混合奖励机制**：
    - **规则可验证奖励（Rule-based Verifiable Rewards）**：用于数学等有确定答案的任务，直接判断结果正确性。
    - **LLM 生成奖励（LLM-based Generative Rewards）**：当规则无法覆盖时，由大模型对智能体输出进行质量评估。
  - 两种奖励可动态组合，形成灵活的训练信号。
- **公式/算法流程**（文字说明）：
  1. 初始化多个 LLM 智能体策略。
  2. 在多个环境中并行启动多智能体交互，每个环境按动态工作流执行多轮对话。
  3. 异步收集交互轨迹，并存入回放缓冲区。
  4. 对每条轨迹，计算规则验证奖励和/或 LLM 生成奖励，形成强化学习信号。
  5. 从缓冲区采样批次数据，分布式更新各智能体策略。
  6. 重复上述过程直至收敛。

## 3. 实验设计

- **数据集/场景**：论文使用了**多种数学任务**（diverse mathematical tasks）进行验证。具体数据集名称在摘要中未列出，但可以推断包括需要精确答案的数学推理基准（如 GSM8K、MATH 等常见数学 benchmark 的可能性较高，但原文未明确）。
- **Benchmark**：未明确说明具体 benchmark 名称，仅指出是“多种数学任务”。
- **对比方法**：
  - 主要对比对象为**单智能体 LLM 系统**。
  - 对比条件为**相同推理预算**（same inference budget），即保证总计算量或 token 数一致的情况下比较性能。

## 4. 资源与算力

- 原文摘要未提及 GPU 型号、数量、训练时长、显存占用等具体算力信息。
- 元数据中也未给出实验硬件细节。
- 需要指出：论文在可用文本中**未明确报告算力配置**，这是信息完整度上的一个缺口。

## 5. 实验数量与充分性

- 从摘要看，实验覆盖了**多个数学任务**，说明至少包含多组任务上的对比实验。
- 但可获取文本中**未列出具体实验数量**，也未明确介绍消融实验、奖励机制对比、扩展性分析等。
- 因此，基于现有文本，实验充分性**无法全面评估**。仅从结论“多智能体优于单智能体”来看，实验方向合理，但缺乏公开细节来评判其公平性与统计显著性。
- 需要强调：由于论文 PDF 内容仅有摘要，无法获得完整的实验设置、超参数、基线实现、多次运行方差等关键信息，因此关于充分性的判断需要谨慎，建议查阅完整论文。

## 6. 主要结论与发现

- MARTI 框架能够高效支持多智能体 LLM 系统的强化训练与推理。
- 在多种数学任务上，经过训练收敛后的多智能体 LLM 系统，在与单智能体系统相同的推理预算下，取得了**更好的性能**。
- 该结果验证了多智能体协作训练的有效性，也为大规模推理模型的能力提升提供了新方向。

## 7. 优点

- **架构创新**：集中式交互与分布式训练解耦，兼顾多智能体交互的复杂性与训练的可扩展性。
- **效率提升**：多轮异步回放机制有效降低训练等待时间，提高硬件利用率。
- **奖励设计灵活**：结合规则验证奖励与 LLM 生成奖励，既能利用硬性正确性信号，又能适应开放性任务。
- **开源贡献**：框架开源，便于社区复现和进一步研究。
- **结论直接**：在相同推理预算下对比单智能体，公平性导向明确（至少在预算控制上有意识）。

## 8. 不足与局限

- **实验覆盖有限**：仅涉及数学任务，未展示在开放域对话、决策、编程等更广泛场景下的效果。
- **具体细节缺失**：摘要中未提供数据集名称、基线实现细节、训练超参数、计算资源、消融实验等，无法全面评估方法的普适性和效率。
- **奖励模型偏差风险**：LLM 生成奖励本身可能存在偏好偏差或评分不一致问题，文中未讨论如何处理这类偏差。
- **单智能体对比可能不够充分**：虽然控制了推理预算，但多智能体系统可能使用更多的模型参数（多个模型实例），需要更详细的成本计量（如总参数量、总内存占用）才能得出绝对优势。
- **框架复杂度**：集中式交互与多智能体策略分布式训练的实现复杂度较高，实际部署和维护成本可能较大，论文未讨论易用性。

（完）

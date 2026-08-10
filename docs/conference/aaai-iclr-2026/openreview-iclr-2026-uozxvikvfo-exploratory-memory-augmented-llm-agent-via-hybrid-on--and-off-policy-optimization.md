---
title: Exploratory Memory-Augmented LLM Agent via Hybrid On- and Off-Policy Optimization
title_zh: 基于混合在线与离线策略优化的探索性记忆增强LLM智能体
authors: "Zeyuan Liu, Jeonghye Kim, Xufang Luo, Dongsheng Li, Yuqing Yang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=UOzxviKVFO"
tags: ["query:agent"]
score: 9.0
evidence: 混合在线/离线强化学习结合记忆增强，提升LLM智能体的探索和适应能力
tldr: "探索瓶颈限制了大语言模型智能体的强化学习训练。该论文提出EMPO²，一种混合在线/离线策略优化框架，利用记忆增强探索，并兼顾有无记忆时的鲁棒性。在ScienceWorld和WebShop上分别比GRPO提升128.6%和11.3%，并能在少量尝试内适应新任务。"
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: LLM智能体强化学习中探索不足，尤其在需要发现新状态的环境中，现有方法依赖预训练知识而失败。
method: 提出混合在线-离线策略优化框架，结合记忆增强的探索更新和鲁棒性训练，使智能体有效记忆并泛化。
result: 在ScienceWorld和WebShop上性能大幅提升，且具有很强的分布外适应能力。
conclusion: 记忆增强与混合策略优化结合，为LLM智能体的探索与持续学习提供有效方案。
---

## Abstract
Exploration remains the key bottleneck for large language model agents trained with reinforcement learning. While prior methods exploit pretrained knowledge, they fail in environments requiring the discovery of novel states. We propose EMPO$^2$, a hybrid RL framework that leverages memory for exploration and combines on- and off-policy updates to make LLMs perform well with memory while also ensuring robustness without it. On ScienceWorld and WebShop, EMPO$^2$ achieves 128.6% and 11.3% improvements over GRPO, respectively. Moreover, in out-of-distribution tests, EMPO$^2$ demonstrates superior adaptability to new tasks, requiring only a few trials with memory and no parameter updates. These results highlight EMPO$^2$ as a promising framework for building more exploratory and generalizable LLM-based agents.

---

## 论文详细总结（自动生成）

# 论文总结：探索性记忆增强LLM智能体——基于混合在线与离线策略优化

## 1. 核心问题与整体含义

- **研究动机**：大语言模型（LLM）智能体在使用强化学习（RL）训练时，**探索（Exploration）不足**是其性能提升的关键瓶颈。现有方法虽然能较好地利用预训练知识，但在需要**主动发现新状态（novel states）** 的环境中往往表现不佳。
- **核心问题**：如何让LLM智能体具备更强的探索能力，并能在没有记忆辅助的情况下依然保持鲁棒性，而不是完全依赖预训练知识或外部记忆。
- **整体含义**：探索能力是LLM智能体走向通用性和持续学习的关键。若不能有效探索新状态，智能体就难以应对分布外（out-of-distribution）的真实任务。

## 2. 方法论：EMPO² 框架

- **基本思路**：提出一种**混合在线/离线策略优化**框架（EMPO²），将记忆（Memory）作为探索的辅助工具，同时兼顾有无记忆两种情况下的鲁棒性。
- **核心创新点**：在在线策略更新和离线策略更新之间进行**协同优化**，使智能体既能在训练中借助记忆高效探索，又能在不依赖记忆的情况下保持稳定的决策能力。
- **技术细节**：
  - **记忆增强探索**：智能体通过与环境的交互将新状态存入外部记忆，并在后续决策中检索利用，从而实现对未知状态的系统化探索。
  - **混合策略优化**：在线策略更新负责利用当前交互数据进行探索性学习，离线策略更新则基于历史记忆数据进行鲁棒性训练。
  - **鲁棒性训练**：在训练中同时模拟“有记忆”和“无记忆”两种情境，确保智能体即使在没有记忆辅助时也不会性能崩溃。

## 3. 实验设计

- **数据集/环境**：
  - **ScienceWorld**：需要复杂科学推理和多步探索的文本环境。
  - **WebShop**：需要在线购物决策的交互式文本环境。
- **基准方法**：主要对比了 **GRPO**（一种广泛使用的LLM智能体策略优化方法）。
- **评估维度**：
  - 在标准benchmark上比较平均性能提升。
  - 设计**分布外测试（out-of-distribution tests）**，评估智能体在新任务上的适应能力。
- **核心实验结果**：在ScienceWorld上比GRPO提升 **128.6%**，在WebShop上提升 **11.3%**。

## 4. 资源与算力

- 论文提供的信息中**未明确说明**所使用的GPU型号、数量、训练时长等具体算力配置。
- 也未提及训练成本、参数量级等细节。
- 提示：若需要复现或评估资源开销，需查阅论文附录或作者补充材料。

## 5. 实验数量与充分性

- **实验组数**：从现有摘要与元数据看，主要在 **两个基准环境**（ScienceWorld和WebShop）上进行了性能对比，并补充了**分布外适应能力测试**。
- **消融实验**：摘要中未明确提及是否有系统的消融实验（如有无记忆模块、在线/离线策略分别的效果等）。
- **充分性评价**：
  - **优点**：跨两个不同领域的任务环境进行验证，且包含分布外测试，具有一定说服力。
  - **不足**：环境数量偏少（仅两个），未展示在更广泛任务（如代码生成、工具调用等）上的泛化能力；缺乏对方法各组件贡献的详细量化分析。

## 6. 主要结论与发现

- EMPO² 在需要探索的环境（ScienceWorld）上表现出**显著性能提升**，验证了记忆增强探索的有效性。
- 在分布外新任务上，EMPO² 仅需**少量尝试**即可适应，且**无需更新参数**，说明其具有较强的泛化和快速适应能力。
- 记忆增强与混合在线/离线策略优化的结合，是提升LLM智能体探索能力与鲁棒性的有效方案。

## 7. 优点

- **方法设计新颖**：将记忆机制与混合在线/离线强化学习统一在一个框架下，而非单纯堆叠记忆模块。
- **兼顾探索与鲁棒性**：同时优化有记忆和无记忆情境，避免了对记忆的过度依赖。
- **探索瓶颈针对性明确**：直接解决LLM智能体在RL训练中探索不足的核心痛点。
- **泛化能力突出**：分布外任务上的少样本适应能力是实际部署中的重要优势。

## 8. 不足与局限

- **实验覆盖有限**：仅验证了ScienceWorld和WebShop两个环境，缺乏更多样化的任务类型（如多轮对话、代码执行等）。
- **消融与分析不足**：摘要层面未涉及关键组件的消融实验，无法判断记忆机制和混合策略各自贡献了多少。
- **算力与复现细节缺失**：未报告训练资源、超参数设置、记忆容量等实现细节，影响复现性。
- **可解释性欠缺**：未讨论智能体探索到的记忆内容是否存在偏差或冗余，以及记忆策略是否可解释。
- **基准数量少**：仅对比GRPO一个基线方法，缺少与其他记忆增强LLM智能体方法（如Reflexion、ExpAgent等）的直接比较。

（完）

---
title: Scaling LLM Multi-turn RL with End-to-end Summarization-based Context Management
title_zh: 基于端到端摘要上下文管理的可扩展LLM多轮强化学习
authors: "Miao Lu, Weiwei Sun, Weihua Du, Zhan Ling, Xuesong Yao, Kang Liu, Jiecao Chen"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=778Yl5j1TE"
tags: ["query:agent"]
score: 9.0
evidence: 面向长时程RL智能体的上下文管理以解决记忆溢出
tldr: 长时程多轮工具使用场景下，LLM智能体强化学习面临上下文长度瓶颈，导致指令遵循下降与高额开销。本文将基于摘要的上下文管理引入训练流程：周期性利用LLM生成摘要压缩工具使用历史，保留任务相关信息并控制上下文规模。基于此推导出可无缝支持标准策略梯度的表示，使智能体能够超越固定上下文窗口进行训练。实验表明该方法在长时程任务中显著提升学习效率和最终性能，为解决RL智能体的长序列训练问题提供了新范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 长时程多轮工具使用中，LLM智能体RL训练受上下文窗口限制，指令遵循差且成本高。
method: 把基于摘要的上下文管理集成到RL训练，周期性压缩历史并推导策略梯度表示。
result: 该办法突破上下文窗口限制，提升长时程RL训练的效率与智能体性能。
conclusion: 端到端摘要式上下文管理为LLM智能体长时程强化学习提供可行的扩展方案。
---

## Abstract
We study reinforcement learning (RL) fine-tuning of large language model (LLM) agents for long-horizon multi-turn tool use, where context length quickly becomes a fundamental bottleneck. Existing RL pipelines can suffer from degraded instruction following, excessive rollout costs, and most importantly, strict context limits. To address the challenge, we introduce \emph{summarization-based context management} to training. In specific, it periodically compresses the tool using history by LLM-generated summaries that retain task-relevant information to keep a compact context while enabling the agent to scale beyond the fixed context window. Building on this formulation, we derive a policy gradient representation that seamlessly enables standard LLM RL infrastructures to optimize both tool-use behaviors as well as summarization strategies in an end-to-end fashion. We instantiate this framework with \underline{SU}mmarization augmented \underline{P}olicy \underline{O}ptimization (\texttt{SUPO}), an LLM RL algorithm that enables long-horizon training beyond a fixed context limit. Experiments on interactive function calling and searching tasks demonstrate that \texttt{SUPO} significantly improves the success rate while maintaining the same or even lower working context length compared to baselines. We also demonstrate that for complex searching tasks \texttt{SUPO} can further improve the evaluation performance when scaling test-time maximum round of summarization beyond that of training time. Our results establish summarization-based context management as a principled and scalable approach for training RL agents beyond fixed context length limits.

---

## 论文详细总结（自动生成）

# 论文总结：Scaling LLM Multi-turn RL with End-to-end Summarization-based Context Management

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：大语言模型（LLM）智能体在长时程（long-horizon）多轮工具使用场景中进行强化学习（RL）微调时，上下文长度会迅速增长，成为根本性瓶颈。
- **核心问题**：
  - 现有 RL 管线在长上下文下出现指令遵循能力下降；
  - rollout 成本过高；
  - 受固定上下文窗口限制，无法训练超出该窗口的智能体。
- **整体含义**：论文旨在突破固定上下文长度对 LLM 智能体强化学习训练的限制，提出一种可扩展的上下文管理范式，使智能体能够在更长时程任务中有效学习和推理。

## 2. 方法论

- **核心思想**：将 **基于摘要的上下文管理（summarization-based context management）** 引入 LLM 智能体的 RL 训练流程。
- **关键技术细节**：
  - 在训练过程中周期性使用 LLM 生成摘要，压缩工具使用历史；
  - 摘要保留与任务相关的关键信息，同时控制上下文规模；  
  - 通过这种方式，智能体能够超越固定上下文窗口进行训练。
- **公式 / 算法流程**（文字说明）：
  - 论文基于摘要式上下文管理推导出一种 **策略梯度表示**（policy gradient representation）；
  - 该表示可以无缝兼容标准 LLM RL 基础设施，使得工具使用行为与摘要生成策略能够**端到端联合优化**；
  - 具体算法命名为 **SUPO（SUmmarization augmented Policy Optimization）**，一种支持超越固定上下文限制的长时程训练的 LLM RL 算法。

## 3. 实验设计

- **任务场景**：
  - 交互式函数调用（interactive function calling）；
  - 搜索任务（searching tasks）。
- **Benchmark**：文中未明确给出具体基准数据集名称（如 ToolBench、WebShop 等），仅描述了任务类型。
- **对比方法**：摘要未列出具体基线名称，但提及与基线相比，SUPO 在成功率上显著提升，同时保持相同或更短的工作上下文长度。

## 4. 资源与算力

- 论文原文（提取到的内容）**未明确说明** GPU 型号、数量、训练时长、显存占用等算力资源信息。
- 因此，无法从现有文本中总结具体的算力消耗；需要查阅论文全文或附录才能获知。

## 5. 实验数量与充分性

- **从摘要看**，实验覆盖了两类任务（函数调用与搜索任务）的主要结果；
- **未明确提及消融实验**，例如：
  - 不同摘要频率的影响；
  - 不同摘要模型/提示的影响；
  - 与截断、丢弃历史等其他上下文管理方法的对比；
  - 策略梯度推导的有效性验证。
- **客观性评估**：由于缺乏实验细节（数据规模、基线的具体实现、重复次数、方差等），无法全面判断实验的公平性与充分性。但摘要中提到了超越训练时摘要轮数的测试时扩展实验，说明作者至少考虑了泛化能力，这部分增加了实验的可信度。

## 6. 主要结论与发现

- SUPO 能够显著提升长时程多轮工具使用任务中的成功率；
- 相比基线，SUPO 在保持相同或更低工作上下文长度的前提下获得更好性能；
- 在复杂搜索任务中，**测试时增加最大摘要轮数**可以进一步提升评估性能，说明该方法具有很好的扩展性；
- 总体结论：基于摘要的上下文管理是一种**有原则且可扩展**的训练 RL 智能体的方法，能够突破固定上下文长度限制。

## 7. 优点

- **创新性**：首次将摘要式上下文管理引入 RL 训练阶段，而非仅用于推理阶段，解决训练时上下文限制问题；
- **端到端优化**：推导的策略梯度表示可以统一优化工具使用与摘要策略，兼容现有 LLM RL 基础设施，实用性强；
- **效率提升**：在提升任务成功率的同时降低或维持上下文长度，兼顾性能与成本；
- **可扩展性**：支持超越训练时长度限制，测试时可进一步增加摘要轮数以提升效果，具备良好的外推能力。

## 8. 不足与局限

- **实验透明度不足**：摘要未提供数据集名称、任务规模、基线细节、超参数等关键信息，难以独立复现或验证；
- **缺乏消融研究**：未看到对摘要频率、摘要质量、上下文压缩率等因素的系统性分析；
- **算力消耗未报告**：无法评估训练成本的可接受性；
- **摘要带来的信息损失风险**：压缩历史可能丢失细粒度信息，尤其在需要精确记忆的工具调用场景下，论文未讨论该风险；
- **通用性有待验证**：仅覆盖函数调用与搜索两类任务，尚未验证在其他长时程交互场景（如多智能体协作、复杂规划）中的适用性；
- **测试时扩展的机制不明确**：摘要轮数的增加如何影响最终决策、是否可能引入累积误差，均在摘要中未展开。

（完）

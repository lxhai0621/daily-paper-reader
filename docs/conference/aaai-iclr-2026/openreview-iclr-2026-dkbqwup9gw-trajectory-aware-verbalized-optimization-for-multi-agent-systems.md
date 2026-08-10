---
title: Trajectory-Aware Verbalized Optimization for Multi-Agent Systems
title_zh: 多智能体系统的轨迹感知语言化优化
authors: "Bin Wu, Haoran Xu, Xiang Zhuang, Emine Yilmaz, Qiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=dkbQwUp9gW"
tags: ["query:ma-kf"]
score: 9.0
evidence: 利用轨迹级信用分配对多智能体系统进行自动提示词优化
tldr: LLM多智能体系统的效果依赖人工提示词，手动调优耗时费力，而现有自动优化方法多依赖粗粒度的任务结果，忽略轨迹级推理与协调信息。本文提出轨迹感知的语言化优化框架TAVO，受强化学习启发，通过信用分配机制将交互轨迹分解为子轨迹，把具体推理和协调步骤与最终结果关联。实验表明，TAVO能自动生成更优的智能体提示词，显著减少人工调优成本，提升多智能体协作效果。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 多智能体系统高度依赖人工提示词，而现有自动优化方法忽略了轨迹级信息。
method: 提出TAVO框架，将交互轨迹分解为子轨迹并进行信用分配，用语言化方式优化提示词。
result: 自动生成高质量提示词，提升多智能体推理与协调效果，降低人工调优开销。
conclusion: 利用轨迹级信用分配可以更精细化地优化多智能体提示词，提升系统整体表现。
---

## Abstract
Large language model (LLM)-based multi-agent systems have shown significant potential, but their effectiveness often depends on manually engineered prompts, which are refined through labor-intensive trial and error. While automatic optimization methods exist, they often rely on coarse, task-level outcomes, neglecting the rich trajectory-level information that captures how agents reason, coordinate, and fail. To address this gap, we propose a Trajectory-Aware Verbalized Optimization (TAVO) framework for prompt refinement in multi-agent systems. Inspired by reinforcement learning, TAVO introduces a credit assignment mechanism that decomposes interaction trajectories into sub-trajectories, linking specific reasoning and coordination steps to the final outcome. This generates fine-grained, process-level feedback. By modeling prompts as verbalized policies, TAVO translates this trajectory feedback into concrete editing instructions, which are aggregated across tasks for systematic refinement. Experiments on both collaborative and competitive multi-agent benchmarks demonstrate that our framework enhances system performance while reducing coordination costs, underscoring the value of leveraging trajectory-level signals to construct more adaptive and efficient LLM-based multi-agent systems.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **背景**：基于大语言模型（LLM）的多智能体系统虽潜力巨大，但其性能高度依赖人工精心设计的提示词（prompts），而人工调优通常需要大量试错，成本高昂。
- **现有方法的不足**：已有的自动优化方法大多依赖粗粒度的任务级结果（如最终得分），忽略了交互轨迹中蕴含的丰富信息——智能体如何推理、如何协调、在何处失败。
- **核心问题**：如何利用轨迹级信息，自动、精细化地优化多智能体系统的提示词，从而提升系统整体性能并降低协调成本。
- **整体含义**：论文提出的思路是从“只看结果”转向“分析过程”，将强化学习中的信用分配思想引入提示词优化，为构建更自适应、更高效的LLM多智能体系统提供了新路径。

## 2. 论文提出的方法论

- **方法名称**：轨迹感知语言化优化（Trajectory-Aware Verbalized Optimization, TAVO）。
- **核心思想**：
  - 受强化学习启发，引入**信用分配机制**，将完整的交互轨迹分解为若干子轨迹。
  - 将具体的推理步骤、协调动作与最终结果关联起来，从而定位哪些步骤导致成功或失败。
  - 这种分解生成了**细粒度的过程级反馈**，而不仅仅是任务结束后的单一得分。
- **关键技术细节**：
  - 将提示词视为一种“语言化策略”（verbalized policy）。
  - 将轨迹反馈转化为**具体的编辑指令**（如修改某段指令、补充约束、调整角色描述等）。
  - 在多个任务上聚合这些编辑指令，进行系统性、迭代式的提示词优化。
- **公式或算法流程**：论文摘要中未给出具体公式或逐步伪代码，仅以文字描述了“轨迹分解 → 信用分配 → 反馈生成 → 提示词编辑 → 跨任务聚合”的逻辑流程。

## 3. 实验设计

- **使用的数据集/场景**：论文使用了**协作式**和**竞争式**两类多智能体基准（collaborative and competitive multi-agent benchmarks），但摘要中未列出具体数据集名称（如具体游戏、对话任务或推理评测集）。
- **对比方法**：摘要中未明确提及对比了哪些基线方法（如人工提示词、任务级自动优化方法等），也未给出相对提升的量化数值。
- **评估指标**：提到了“系统性能”（system performance）和“协调成本”（coordination costs），但具体指标定义未展示。

## 4. 资源与算力

- **论文中未提及**任何关于GPU型号、数量、训练时长或推理算力的信息。
- 由于该框架依赖LLM进行轨迹理解和指令生成，实际运行可能需要较大算力，但原文未给出具体数据，因此无法总结。

## 5. 实验数量与充分性

- **实验数量**：摘要中只概括了“在多个基准上”进行了验证，未给出具体实验组数（如多少个任务、几组消融、几次重复）。
- **是否充分**：从现有信息看，**无法判断实验的充分程度**。
  - 缺少消融实验描述（例如，是否验证了信用分配模块单独的作用？）。
  - 缺少与不同优化策略的对比细节。
  - 缺少统计显著性检验或误差范围。
- **客观与公平性**：由于缺乏实验细节、基线设置和数据集信息，难以评估实验是否客观公平。只能说论文声称在两类基准上均能提升性能、降低成本，但具体证据未被摘要充分呈现。

## 6. 论文的主要结论与发现

- TAVO能够**自动生成更优的智能体提示词**，显著减少人工调优开销。
- 通过利用轨迹级信号，框架在**协作与竞争**两种模式下都能增强系统性能，并降低智能体之间的协调成本。
- 验证了轨迹级信用分配对于构造自适应、高效LLM多智能体系统的价值。

## 7. 优点

- **方法角度**：
  - 将强化学习中的信用分配思想引入提示词优化，视角新颖。
  - 利用轨迹级细粒度反馈，比传统任务级反馈信息量更大、更可解释。
  - 提示词作为可编辑的“语言化策略”，与LLM的文本接口天然契合。
- **实验角度**：
  - 覆盖了协作与竞争两类典型多智能体场景，具有一定普适性。
  - 同时关注性能提升和协调成本，评估维度较全面（不过都是定性描述）。
- **应用价值**：可自动化提示词优化流程，降低人工调优的人力成本，对实际部署LLM多智能体系统有实用意义。

## 8. 不足与局限

- **实验信息不完整**：论文摘要中未给出具体数据集、基线、超参数、实验次数等，导致结论的可复现性和说服力不足。
- **算力信息缺失**：未报告计算资源，无法评估方法在实际应用中的成本门槛。
- **可能存在的偏差风险**：
  - 若基准任务或场景选择有偏向（例如轨迹可清晰分解的任务），则结果可能不适用于轨迹混乱或奖励稀疏的复杂场景。
  - 信用分配依赖轨迹分解的质量，若分解错误，反馈可能无效甚至有害。
  - 语言化反馈的生成受限于LLM的理解和编辑能力，可能与更底层的梯度式优化精度不同。
- **应用限制**：该方法要求交互轨迹可记录、可分解，对于无法获取完整轨迹或需要实时优化的系统可能不适用。

（完）

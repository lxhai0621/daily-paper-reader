---
title: "Don’t Lose the Thread: Empowering Long-Horizon LLM Agents with Cognitive Resource Self-Allocation"
title_zh: 不要迷失主线：通过认知资源自分配增强长时程LLM智能体
authors: "Zheng Zhu, Xiaozhuan Liang, Bei Yu, Xi Chen, Jiaya Jia"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=NBGlItueYE"
tags: ["query:agent"]
score: 9.0
evidence: 智能体上下文与工作记忆的自管理
tldr: 长时程任务中LLM智能体的工作记忆易被无关信息挤占，导致认知过载和规划能力下降。本文提出认知资源自分配范式CORAL，将其实现为智能体可调用的工作记忆管理工具集。它允许智能体在工作记忆中维护关键进度检查点，并自适应地初始化与清理上下文，从而优化注意力分配。在长时程推理与规划任务中，CORAL有效提升了智能体的任务完成质量与稳定性，为长程智能体提供了一种轻量级上下文管理方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM智能体在长时程任务中因工作记忆膨胀与信息冗余而认知过载，损害规划与推理。
method: 提出CORAL范式，以智能体可调用的工作记忆管理工具集维护关键检查点并自适应管理上下文。
result: CORAL在长时程任务上提升了智能体推理与规划质量，减少了无关信息干扰。
conclusion: 上下文自分配是增强长时程LLM智能体鲁棒性的有效手段。
---

## Abstract
Agents powered by large language models (LLMs) have demonstrated remarkable progress in solving complex reasoning tasks. However, LLM agents often falter on long-horizon tasks due to cognitive overload, as their working memory becomes cluttered with expanding and irrelevant information, which dilutes their attention and hinders effective planning and reasoning. To mitigate this challenge, we introduce **CO**gnitive **R**esource Self-**AL**location (**CORAL**), a novel reasoning paradigm that empowers agents to proactively optimize their context. Implemented as an agent-callable working memory management toolset, CORAL allows an agent to maintain crucial checkpoints of its progress within its working memory and adaptively initiate a new problem-solving episode by purging cluttered working memory and resuming its reasoning from the most recent checkpoint, effectively reallocating agentic cognitive resources by implicitly sharpening their attention on the checkpoints. We further enhance the agent's checkpoint capabilities using a Multi-episode Agentic Reinforced Policy Optimization algorithm. On several long-horizon task benchmarks, CORAL significantly outperforms standard LLM agent methods. Notably, analysis of the LLMs' attention distribution reveals that CORAL substantially optimizes agentic RL dynamics, which in turn ensures agents maintain a focused cognitive resource allocation, thereby continuously amplifying performance gains.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：基于大语言模型（LLM）的智能体在复杂推理任务上已取得显著进展，但在**长时程（long-horizon）任务**中表现不佳。
- **核心问题**：LLM 智能体在长时程任务中面临**认知过载（cognitive overload）**。随着任务推进，其工作记忆（working memory）被不断膨胀的、与当前目标无关的信息所充斥，导致：
  - 注意力被稀释（diluted attention）
  - 规划与推理能力被削弱（hinders effective planning and reasoning）
- **整体含义**：本文旨在解决LLM智能体在长时程任务中“迷失主线”的问题，通过赋予智能体主动管理自身上下文（即认知资源）的能力，来缓解认知过载，提升任务完成质量与稳定性。

## 2. 方法论：核心思想、关键技术细节

### 2.1 核心思想

- 提出 **CORAL（Cognitive Resource Self-ALLocation，认知资源自分配）** 范式：让智能体**主动优化、管理自己的上下文**，而不是被动地让上下文无限增长。
- 核心洞察：通过**隐式地强化对检查点（checkpoints）的注意力**，实现智能体认知资源的再分配。

### 2.2 技术实现

- **工具集形式**：CORAL 被实现为一套**智能体可调用的工作记忆管理工具集（agent-callable working memory management toolset）**，智能体可以在推理过程中自主决定何时调用这些工具。
- **关键功能**：
  1. **维护关键进度检查点**：在工作记忆中保存重要的任务进度信息（checkpoints of progress）。
  2. **自适应初始化新会话**：当工作记忆变得杂乱时，智能体可以主动清空（purge）被污染的工作记忆。
  3. **从最近检查点恢复推理**：清空记忆后，从最新的检查点继续推理，而不是从头开始或继续在混乱的上下文中推理。
- **工作流程（文字描述）**：
  1. 智能体开始解决长时程任务，持续在上下文中累积信息。
  2. 当智能体检测到工作记忆过于杂乱、注意力被稀释时，调用 CORAL 工具。
  3. 智能体将当前关键进度保存为检查点。
  4. 清空工作记忆中的冗余信息。
  5. 从最近检查点重新开始一段新的问题解决片段（episode），在新上下文中继续推理。
- **增强算法**：进一步提出 **Multi-episode Agentic Reinforced Policy Optimization（MARPO）** 算法，用于增强智能体的检查点能力，即通过多片段智能体强化学习优化智能体何时、如何保存和利用检查点的策略。

## 3. 实验设计

- **基准（Benchmark）**：使用了**多个长时程任务基准**（several long-horizon task benchmarks），但摘要中**未具体列出数据集名称**。
- **对比方法**：与**标准LLM智能体方法（standard LLM agent methods）**进行对比。
- **额外分析**：对LLM的**注意力分布（attention distribution）**进行了分析，以验证CORAL对注意力优化的有效性。
- **注意**：由于论文摘要未提供更详细的信息，具体的数据集列表、任务类型、评估指标细节无法确认。

## 4. 资源与算力

- **原文未明确说明**：提供的摘要和元数据中**没有提及任何算力信息**，包括：
  - GPU 型号与数量
  - 训练时长
  - 总计算量
- 因此，无法从现有信息中评估该方法的计算成本。

## 5. 实验数量与充分性

- **实验概况**：摘要中提到的实验包括：
  1. 在多个长时程任务基准上与标准方法的对比实验。
  2. 对LLM注意力分布的分析实验（机制分析）。
- **充分性评估**：
  - **正面**：跨多个基准的验证以及注意力分布分析，表明作者在验证方法有效性方面做出了努力。
  - **不足**：由于摘要信息有限，无法确知：
    - 是否进行了**消融实验**（如去掉MARPO只保留CORAL工具集的效果）。
    - 每个基准上实验的重复次数、方差是否报告。
    - 基线方法的数量和强弱程度。
  - **总体评价**：从现有信息看，实验设计合理，但**验证的完整性尚无法全面评估**，需要阅读全文以确认消融和统计显著性检验。

## 6. 主要结论与发现

- **CORAL 显著优于标准 LLM 智能体方法**：在多个长时程任务基准上取得了明显性能提升。
- **注意力分布优化**：对LLM注意力分布的分析显示，CORAL **实质性地优化了智能体强化学习的动态过程（agentic RL dynamics）**。
- **保障专注的认知资源分配**：CORAL确保持久地保持**专注的认知资源分配（focused cognitive resource allocation）**，从而**持续放大性能增益（continuously amplifying performance gains）**。
- **核心结论**：上下文自分配（context self-allocation）是提升长时程LLM智能体鲁棒性与任务质量的有效手段。

## 7. 优点

- **问题定位精准**：直击LLM智能体在长时程任务中的核心痛点——工作记忆膨胀与注意力稀释，具有明确的现实意义。
- **方法论创新性**：将上下文管理从“被动的系统设计问题”转变为“智能体主动决策问题”，提出了认知资源自分配的崭新视角。
- **轻量级方案**：以工具集形式实现，无需改变底层LLM架构，具备较强的即插即用性和通用性。
- **理论分析深入**：不仅报告了性能提升，还通过注意力分布分析揭示了方法生效的内在机制，增强了结果的可信度与解释力。
- **强化学习结合的亮点**：将MARPO算法与工具使用结合，使得检查点策略可以端到端优化，而非依赖人工规则。

## 8. 不足与局限

- **实验细节缺失**：摘要中未列出具体使用的基准数据集、任务类别与评估指标，无法独立判断方法适用范围。
- **计算成本未披露**：未说明训练和推理所需的算力资源，实际部署的可行性难以评估。
- **消融验证不明确**：未在摘要中展示消融实验，CORAL工具集与MARPO各自的独立贡献大小不清楚。
- **潜在偏差风险**：
  - 若仅与标准智能体方法对比，而未与更先进的显式记忆管理方案对比，可能高估方法的相对优势。
  - 注意力分布分析可能只展示了有利案例，存在选择性展示的风险。
- **应用限制**：
  - “清空工作记忆并恢复检查点”这一策略依赖智能体对“何时该清理”的正确判断，判断失误可能导致关键信息丢失。
  - 检查点的质量直接决定恢复后推理的上限，若在错误时机保存了不完整的进度，反而可能损害性能。
  - 方法在极其长程、动态变化剧烈的任务中是否依然鲁棒，尚待验证。

（完）

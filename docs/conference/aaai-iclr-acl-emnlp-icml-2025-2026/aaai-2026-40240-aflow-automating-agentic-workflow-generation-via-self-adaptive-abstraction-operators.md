---
title: "A²Flow: Automating Agentic Workflow Generation via Self-Adaptive Abstraction Operators"
title_zh: A²Flow：通过自适应抽象算子自动化智能体工作流生成
authors: "Mingming Zhao, Xiaokang Wei, Yuanqi Shao, Kaiwen Zhou, Lin Yang, Siwei Rao, Junhui Zhan, Zhitang Chen"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40240/44201"
tags: ["query:ma-kf"]
score: 9.0
evidence: 自动化智能体工作流生成
tldr: A2Flow针对现有自动化智能体工作流设计依赖手动预定义算子的问题，提出基于自适应抽象算子的全自动框架。通过案例算子生成、聚类抽象和深度提取三阶段，自动生成可泛化的工作流算子，适用于多种任务。实验验证了其有效性和通用性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 手动预定义算子限制了智能体工作流设计的自动化和泛化。
method: 三阶段算子提取：案例生成、聚类抽象、深度提取抽象执行算子。
result: 在多个任务上自动生成的工作流性能优于或媲美人工设计。
conclusion: 自适应算子实现了智能体工作流的全自动生成。
---

## Abstract
Large language models (LLMs) have shown strong potential in automating the design of agentic workflows. However, existing methods still rely heavily on manually predefined operators, limiting generalization and scalability. To address this issue, we propose A²Flow, a fully automated framework for agentic workflow generation based on self-adaptive abstraction operators. A²Flow employs a three-stage operator extraction process: 1) Case-based Initial Operator Generation: leveraging expert demonstrations and LLM reasoning to generate case-specific operators; 2) Operator Clustering and Preliminary Abstraction: grouping similar operators across tasks to form preliminary abstractions; and 3) Deep Extraction for Abstract Execution Operators: applying long chain-of-thought prompting and multi-path reasoning to derive compact and generalizable execution operators. These operators serve as reusable building blocks for workflow construction without manual predefinition. Furthermore, we enhance node-level workflow search with an operator memory mechanism, which retains historical outputs to enrich context and improve decision-making. Experiments on general and embodied benchmarks show that A²Flow achieves a 2.4% and 19.3% average performance improvement and reduces resource usage by 37% over state-of-the-art baselines.

---

## 论文详细总结（自动生成）

# A²Flow：通过自适应抽象算子自动化智能体工作流生成——详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **背景**：大语言模型（LLM）在自动化智能体工作流设计方面展现出潜力，但现有方法（如 AFLOW、DebFlow、MermaidFlow）严重依赖**手动预定义的算子**（如 Ensemble、Review、Revise），导致：
  - 泛化能力差：预定义算子针对特定任务设计，难以迁移到开放世界或具身任务。
  - 可扩展性受限：每次面对新任务都需要人工重新设计算子，阻碍了全自动工作流生成。
- **核心目标**：提出 A²Flow，一个**全自动**的智能体工作流生成框架，能够自动从专家数据中提取**自适应抽象算子**，无需人工预定义，从而提高泛化性和效率。

## 2. 方法论：核心思想、关键技术细节
### 2.1 整体框架
- 使用 LLM 作为优化器，基于**蒙特卡洛树搜索（MCTS）的变体**搜索最佳工作流结构。
- 核心创新：**Self-Adaptive Abstraction Operators**（自适应抽象算子） + **Operators Memory Mechanism**（算子记忆机制）。

### 2.2 自适应抽象算子生成（三阶段）
1. **Case-based Initial Operator Generation**：
   - 从专家数据（20% 验证集）中，利用 LLM 推理生成**针对每个案例的初始算子**（如 `ObserveEnvironment()`、`ExecuteAction()`）。
   - 算子定义为代码块，具有单一输入/输出，无分支。
2. **Operator Clustering and Preliminary Abstraction**：
   - 通过 LLM 对相似功能的算子进行**聚类和约简**，得到初步抽象算子（如 `Planner()`、`Executor()`）。
3. **Deep Extraction for Abstract Execution Operators**：
   - 使用**长链式思维（Long CoT）** 和多路径并行生成（m=6 条独立路径），通过三次迭代精炼，最终利用自一致性聚合得到**任务感知的抽象算子**（如 `Planner()`, `Executor()`, `Validator()`）。
   - 引入**反射机制**：LLM 输出的 Python 代码需通过语法和执行验证，否则自纠正。

### 2.3 算子记忆机制
- 在每个节点，算子不仅接收前一个算子的输出，还访问**全局记忆空间**（存储所有历史中间结果）。
- 公式：\( o_k = f_k(input_k, P_k, M_{k-1}) \)，\( M_k = M_{k-1} \cup \{o_k\} \)。
- 增强上下文感知能力，减少交互步骤，提升决策质量。

### 2.4 工作流优化（基于 AFLOW 框架增强）
- 工作流表示为代码（节点、边、算子），通过 MCTS 进行初始化、选择、扩展、评估、反向传播。
- 搜索空间包含节点参数、边结构，以及我们自动生成的算子集合 \(\{O^{(t)}\}\) 和记忆机制 \(M\)。
- 最终最优工作流：\( W^* = S(W_0, \{O^{(t)}\}, G, D_V, M) \)。

## 3. 实验设计
### 3.1 数据集与场景
- **5 个领域，8 个公开基准**：
  - **代码生成**：HumanEval、MBPP（pass@1）
  - **数学推理**：GSM8K、MATH Level 5（Solve Rate）
  - **阅读理解**：HotpotQA、DROP（F1 Score）
  - **具身任务**：ALFWorld（成功/失败）
  - **游戏**：TextCraft（成功/失败）
- 数据集划分：验证集 20%、测试集 80%，固定随机种子 42。

### 3.2 对比基线
- **手动工程工作流**：IO、CoT、Self-Consistency（5-shot）、MedPrompt、MultiPersona、Self-Refine
- **自动工作流优化器**：ADAS、AFLOW
- **执行模型**：GPT-4o-mini、GPT-4o、DeepSeek-v3
- **优化器模型**：Claude-3.5-sonnet

### 3.3 评估指标
- 各基准专用指标：pass@1、F1、Solve Rate、二元成功/失败。
- 成本分析：记录 token 用量，绘制 Pareto 前沿对比效率和性能。

## 4. 资源与算力
- **文中未明确说明**使用的 GPU 型号、数量或训练时长。
- 仅提到采用不同 LLM 作为执行器和优化器（如 Claude-3.5-sonnet、GPT-4o-mini、DeepSeek-v3），但未涉及分布式训练或硬件具体配置。
- **结论**：论文缺乏算力细节，读者无法复现完整资源消耗。

## 5. 实验数量与充分性
- **主实验**：在 5 个领域/8 个数据集上对比 8 个基线，全面覆盖。
- **附加实验**：
  - **消融实验**（表 3）：在 MATH 上对 4 个组件（初始算子、聚类、深度提取、记忆机制）进行逐项消融。
  - **成本分析**（图 3）：在 DROP 上绘制 Pareto 前沿。
  - **案例研究**（图 4）：以 ALFWorld 为例展示算子生成和工作流演化。
- **充分性评价**：实验设计较完整，对比基线选择合理（包括手动和自动方法）。但存在以下潜在偏差：
  - 消融实验仅在一个数据集（MATH）上进行，未在其他领域重复。
  - HumanEval 上由于预定义算子（含 Python 解释器）建立的强基线，A²Flow 表现不如某些基线，作者解释了原因，但仍需更多分析。
  - 具身任务（ALFWorld、TextCraft）只对比了 ReAct 和 AFLOW，基线数量较少。
- **公平性**：所有实验使用相同执行模型、固定随机种子，多次重复取均值，具有客观性。

## 6. 主要结论与发现
1. **性能提升**：
   - 在阅读、代码、数学任务的 6 个基准上，A²Flow 平均超越最优基线 **2.4%**（如 DROP 上 +4.5%，MATH 上 +4.1%）。
   - 在具身/游戏任务上平均提升 **19.3%**（ALFWorld +7.9%，TextCraft +6.0%）。
2. **成本降低**：在 DROP 上比 AFLOW 节省约 **37%** 资源使用，同时达到更优 Pareto 前沿。
3. **组件贡献**：消融实验显示：
   - 移除记忆机制 → 性能下降 4.1%。
   - 移除整个自适应算子模块 → 性能下降 >10%。
4. **泛化能力**：自动生成的算子可应用于开放世界任务（如 ALFWorld），无需重新设计。

## 7. 方法或实验设计上的亮点
- **全自动化**：首次提出不依赖人工预定义算子的工作流生成方法，实现端到端自动化。
- **三阶段算子提取**：从案例级→聚类级→深度抽象级，结合 CoT、多路径、反射机制，逻辑清晰且可解释。
- **算子记忆机制**：简单有效，通过保留历史输出增强节点决策，减少无效交互。
- **成本-性能平衡**：通过 Pareto 前沿分析证明经济效益，实用性强。
- **代码开源**（GitHub），便于复现和扩展。

## 8. 不足与局限
- **实验覆盖不均衡**：
  - 消融实验仅基于 MATH 数据集，未在代码生成或阅读理解上验证各组件贡献。
  - 具身/游戏任务基线过少（仅 ReAct 和 AFLOW），未与更多专门方法（如 Voyager、SayCan）对比。
- **某些任务表现受限**：在 HumanEval 上由于预定义算子包含 Python 解释器，抽象算子难以超越；GSM8K 上基线已高，A²Flow 增益微弱。
- **依赖 LLM 作为优化器**：三阶段算子生成需要多次调用 LLM（尤其是长 CoT 和多路径），可能引入额外开销和随机性。
- **安全性与偏差风险未讨论**：未涉及算子生成可能引入的偏见、错误指令或安全性问题。
- **算力细节缺失**：无法评估方法的实际训练/推理成本。
- **应用限制**：自适应算子依赖于专家数据，若专家数据质量低或领域极特殊，可能生成低效算子。

（完）

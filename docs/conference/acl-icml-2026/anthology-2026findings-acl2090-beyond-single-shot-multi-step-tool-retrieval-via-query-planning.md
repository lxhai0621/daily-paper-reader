---
title: "Beyond Single-Shot: Multi-step Tool Retrieval via Query Planning"
title_zh: 超越单次检索：基于查询规划的多步工具检索
authors: "Wei Fang, James Glass"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.2090.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向LLM智能体的多步工具检索与查询规划
tldr: 大模型智能体在庞大且动态的工具库上依赖检索，但单次稠密检索难以应对复杂请求，根源在于抽象用户目标与技术文档之间存在语义鸿沟，固定嵌入也难以刻画工具组合。为此提出 ToolQP，把检索建模为迭代式查询规划，先将指令分解为子任务，再动态生成查询与检索器交互。方法以合成查询数据训练，有效弥合语义差距，提升了组合式工具检索与外部接口调用的准确性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2090/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 3836, \"height\": 1764}]"
motivation: 面向大规模动态工具库时，单次稠密检索难以处理复杂请求，抽象目标与文档存在语义鸿沟。
method: 提出 ToolQP，将检索建模为迭代查询规划，把指令分解为子任务并动态生成检索查询。
result: 通过合成查询训练，弥合语义差距，提升了组合式工具检索的效果。
conclusion: 为智能体调用外部工具与接口提供了多步检索新方法。
---

## Abstract
LLM agents operating over massive, dynamic tool libraries rely on effective retrieval, yet standard single-shot dense retrievers struggle with complex requests. These failures primarily stem from the disconnect between abstract user goals and technical documentation, and the limited capacity of fixed-size embeddings to model combinatorial tool compositions. To address these challenges, we propose ToolQP, a lightweight framework that models retrieval as iterative query planning. Instead of single-shot matching, ToolQP decomposes instructions into sub-tasks and dynamically generates queries to interact with the retriever, effectively bridging the semantic gap by targeting the specific sub-tasks required for composition. We train ToolQP using synthetic query trajectories followed by optimization with Reinforcement Learning with Verifiable Rewards (RLVR). Experiments demonstrate that ToolQP achieves state-of-the-art performance, exhibiting superior zero-shot generalization, robustness across diverse retrievers, and significant improvements in downstream agentic execution.

---

## 论文详细总结（自动生成）

# 论文总结：Beyond Single-Shot: Multi-step Tool Retrieval via Query Planning

## 1. 核心问题与整体含义

- **研究背景**：LLM 智能体需要调用大量外部工具（API、数据库、软件函数等），工具库规模从几十个扩展到数万乃至 52k+，无法全部放入上下文窗口，因此“工具检索”成为关键前置步骤。
- **核心问题**：传统单次稠密检索（single-shot dense retrieval）在复杂、组合式工具使用请求上表现不佳，主要存在三类挑战：
  - **语义错位**：用户抽象目标（如“让录音高质量”）与工具技术文档（如 `lfilter`、参数 `b/a`）之间存在鸿沟。
  - **组合瓶颈**：固定维度嵌入难以编码多个异构工具的组合需求。
  - **缺乏交互式工具集感知**：单次检索把工具库当静态数据库，无法处理工具间依赖、内部约束或工具集动态变化。
- **整体含义**：论文提出 **ToolQP**，把工具检索从静态相似度匹配重构为**迭代式查询规划过程**，先分解用户指令为子任务，再动态生成查询与检索器交互，从而弥合语义鸿沟、处理组合工具需求，并提升下游智能体执行成功率。

## 2. 方法论

### 2.1 核心思想

- 将检索器 `E` 视为可交互的动态环境，而非静态索引。
- ToolQP 是一个轻量、模块化、可插拔的规划层，可叠加在任意现有稠密检索器和下游 LLM 之上，无需修改底层索引或微调检索器。
- 整体流程分三阶段：**规划（Planning）→ 交互式查询生成（Interactive Query Generation）→ 检索聚合（Retrieval Aggregation）**。

### 2.2 三阶段流程

- **规划：任务分解**
  - 输入用户查询 `q`，生成自然语言计划 `P`，并分解为逻辑子任务序列 `{s_n}`。
  - 目标是把高层用户意图映射到低层工具功能，缓解语义错位。
- **交互式查询生成**
  - 针对每个子任务，逐步生成搜索查询 `{q_t}`。
  - 每一步观察检索反馈 `O_t = E(q_t; D)`，再决定下一步查询 `q_{t+1}`。
  - 若初始查询发现某工具需要特定参数或前置工具，可继续查询该前置依赖。
  - 过程持续到模型认为子任务已被充分覆盖，形成查询-检索轨迹 `{(q_t, O_t)}`。
- **检索聚合**
  - 不采用 RRF 或复杂 rank fusion，而采用 **peak-rank aggregation**：对每个唯一工具，以其在任意单次检索中取得的最好排名作为最终排名。
  - 这样可以避免子任务查询次数不同导致的频率偏差，平衡各子任务结果。

### 2.3 数据生成与 SFT

- 标准工具检索数据只有用户查询 `q` 和真值工具集 `T*`，缺少查询轨迹。
- 论文设计合成数据流水线（Alg. 1）：
  - **Plan Alignment**：让教师模型把高层计划 `P` 解析为子任务，并把真值工具分配给各子任务。
  - **Query Generation**：只根据子任务描述生成候选查询，避免直接使用目标工具名；若初始候选查询无法召回目标工具，则逐步加入更多目标信息，采用课程学习式重提示。
  - **Query Verification and Trajectory Construction**：用检索器评估候选查询，选择召回和排名最好的查询；保留一定比例失败尝试后成功的轨迹，以训练自我纠错。
- 合成轨迹用于标准监督微调（SFT），采用最大似然和 teacher forcing。

### 2.4 RLVR / GRPO 训练

- 在 SFT 后，进一步使用 **Reinforcement Learning with Verifiable Rewards (RLVR)**，具体采用 **GRPO**，无需价值网络。
- 总体奖励：
  - `R = β1 R_retrieval + β2 R_format + β3 R_plan`
- 关键奖励：
  - `R_retrieval`：最终聚合工具列表相对真值的 nDCG@K 和 Recall@K 序列级奖励，鼓励全局覆盖。
  - `R_format`：格式有效性，包括正确格式比例和是否以 `<stop_retrieval>` 结束。
  - `R_plan`：生成计划与参考计划的语义相似度，作为正则项，防止偏离用户意图。
- 奖励权重：`β1,n=5.0, β1,r=2.5, β2,f=1.5, β2,s=0.6, β3=1.0`。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- **主检索 benchmark：ToolRet**
  - 包含 35 个工具调用数据集，工具库约 44k 工具。
  - 分 Web、Code、Custom 三个域。
  - 训练数据来自 ToolBench、ToolACE、APIGen 的 ToolRet 训练子集，共抽样 10k。
  - Web 训练来源对应的测试集视为 in-domain，其余为 zero-shot transfer。
  - 指标：nDCG@10、Completeness@10（`1[R@K=1]`），K=10，按类别宏平均。
- **端到端工具调用 benchmark**
  - **API-Bank**：73 个工具，测试 Level-1 和 Level-2，Level-1 被改造为强制工具检索。
  - **StableToolBench（STB）**：I2-Category（13k 工具）和 I3-Instruction（1.6k 工具），更复杂、组合式、多步推理。
  - 使用 Qwen3-30B + ReAct 推理管线，报告准确率或 solvable pass rate。
- **检索器迁移实验**
  - 在多个检索器上测试 ToolQP 的 out-of-the-box 迁移能力。
  - 包括 bge-large-en-v1.5、e5-base-v2、e5-mistral-7b-instruct、ToolRet-bge-large-en-v1.5、ToolRet-e5-base-v2，以及 BM25 等。

### 3.2 对比方法

- **Prompting 方法**：Q2E、Q2D、HyDE、D2Q、Re-Invoke，使用 Qwen3-30B-A3B-Instruct。
- **Re-ranking 方法**：bge-reranker-v2-m3、bge-reranker-v2-gemma。
- **Fine-tuning 方法**：Q2P/SFT、gte

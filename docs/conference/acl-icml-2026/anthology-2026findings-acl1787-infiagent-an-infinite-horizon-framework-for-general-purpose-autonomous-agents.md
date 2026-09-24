---
title: "InfiAgent: An Infinite-Horizon Framework for General-Purpose Autonomous Agents"
title_zh: InfiAgent：面向通用自主智能体的无限时程框架
authors: "Chenglin Yu, Yuchen Wang, Songmiao Wang, Hongxia Yang, Li Ming"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1787.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 保持推理上下文严格有界的无限时程智能体框架
tldr: 大模型智能体虽能推理和使用工具，但在长时程任务中因上下文无限增长与误差累积而失效，常见的压缩或检索增强提示又带来信息保真与推理稳定性的权衡。本文提出 InfiAgent，将持久状态外化为以文件为中心的状态抽象，使推理上下文始终有界。智能体每步从工作区快照加固定窗口的近期动作重建上下文。实验表明其在深度研究与文献综述任务上无需微调即可稳定运行。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1787/fig-001.webp\", \"caption\": \"\", \"page\": 5, \"index\": 1, \"width\": 2816, \"height\": 1536}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1787/fig-002.webp\", \"caption\": \"\", \"page\": 6, \"index\": 2, \"width\": 4152, \"height\": 2056}]"
motivation: 大模型智能体在长时程任务中因上下文无限增长与误差累积而失效，现有缓解手段存在权衡。
method: 提出InfiAgent，将持久状态外化为文件中心抽象，每步从状态快照与固定窗口重建有界上下文。
result: 在深度研究与八十篇文献综述任务上，无需任务微调即可保持稳定的长时程推理。
conclusion: 该框架通过有界上下文管理解决了长时程智能体的记忆溢出问题，提升了推理稳定性。
---

## Abstract
LLM agents can reason and use tools, but they often break down on long-horizon tasks due to unbounded context growth and accumulated errors. Common remedies such as context compression or retrieval-augmented prompting introduce trade-offs between information fidelity and reasoning stability. We present InfiAgent, a general-purpose framework that keeps the agent’s reasoning context strictly bounded regardless of task duration by externalizing persistent state into a file-centric state abstraction. At each step, the agent reconstructs context from a workspace state snapshot plus a fixed window of recent actions. Experiments on DeepResearch and an 80-paper literature review task show that, without task-specific fine-tuning, InfiAgent with a 20B open-source model is competitive with larger proprietary systems and maintains substantially higher long-horizon coverage than context-centric baselines. These results support explicit state externalization as a practical foundation for stable long-horizon agents.

---

## 论文详细总结（自动生成）

# InfiAgent 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：当前基于大语言模型（LLM）的自主智能体虽具备推理与工具调用能力，但在**长时程任务（long-horizon tasks）**中普遍表现脆弱，主要源于两大问题：
  - **上下文无限增长**：多数框架将对话历史、工具轨迹、中间计划与部分结果直接累积在提示词（prompt）中，随任务时长增加，上下文长度无界增长。
  - **误差累积**：为适配有限上下文窗口而采用的截断、摘要或启发式检索，会引入信息丢失、无关 token 干扰以及对早期错误的敏感放大，导致长时程行为不稳定。
- **现有缓解手段的局限**：
  - **上下文压缩 / RAG / 长上下文模型**：只是部分缓解，仍将长期任务状态与即时推理上下文纠缠，随着执行推进增加 LLM 的认知负荷。
  - **MAKER 等极端任务分解**：仅适用于高度结构化、子任务边界预定义的逻辑任务，难以推广到科研等开放式领域。
- **整体含义**：论文主张实现长时程稳定性需要**显式分离持久任务状态与有界推理上下文**，并提出 InfiAgent 框架，将长期状态外化为**以文件为中心（file-centric）的状态抽象**，使推理上下文严格有界，不随任务时长增长。

## 2. 方法论

- **核心思想**：将任务状态从提示词中解耦，外化为文件系统中的持久状态；每一步仅从**工作区状态快照 + 固定窗口的近期动作**重建推理上下文。
- **形式化定义**：
  - 传统上下文中心表示为 `c_t = ⟨o_1, a_1, …, o_{t-1}, a_{t-1}, o_t⟩`，随 t 增长无界。
  - 持久状态外化：`S_t = F_t`，其中 `F_t` 为工作区文件与结构化工件集合，是任务进度的权威记录。
  - 状态转移：`F_{t+1} = T(F_t, a_t)`，T 表示文件创建、修改或删除，F_t 不受上下文窗口限制。
  - 有界推理上下文：`c^bounded_t = g(F_t, a_{t-k:t-1})`，k 为固定的小常数，保证 |c^bounded_t| = O(1)。
- **关键技术细节**：
  - **固定模式（fixed-schema）上下文构建**：g(·) 不是自由形式的目录转储，而是固定模式构建器。一个专门的“思考模型”周期性根据工作区与最近动作窗口重写持久思考记录 M_t。
  - **思考记录四部分**：① 任务级待办清单；② 相关文件描述；③ 需跨窗口保留的固定状态（工作区结构、规则、失败记录等）；④ 下一个窗口的 k 步工具级计划。
  - **动作窗口重置**：每次思考更新后，可见动作窗口被清空，长轨迹由更新后的 M_t 替代，而非在提示词中累积。
  - **检查点恢复**：各 agent 的动作轨迹与最新思考记录分别持久化，中断后可从最近保存的检查点恢复，无需重放完整对话。
- **多层级 agent 架构（树状 DAG）**：
  - **Level 3（Alpha Agent）**：编排者，负责高层规划与任务分解，为决策树根节点。
  - **Level 2（Domain Agents）**：领域专家，如数据收集、数据分析、编码、材料转文档等。
  - **Level 1（Atomic Agents）**：单一用途执行器，如从论文回答、从 arXiv 获取数据、网络搜索等。
  - 高层 agent 将低层 agent 作为可调用工具（Agent-as-a-Tool），避免扁平多 agent 系统中的“工具调用混乱”。
- **外部注意力管线（External Attention Pipeline）**：
  - 当需要文档信息时，agent 不将文档载入上下文，而是调用专用文档阅读 agent，后者启动隔离的 LLM 进程查询文档，仅返回抽取答案。
  - 公式：`C_main ← C_main ∪ Tool(Query, Document)`。
  - 相当于应用层的注意力头，仅选择相关信息注入主状态，降低主 agent 认知负荷。

## 3. 实验设计

- **数据集 / 场景**：
  1. **DeepResearch Bench**：标准化评估，衡量多步研究质量，从四个维度打分——全面性（Comprehensiveness）、洞察力（Insight）、指令遵循（Instruction Following）、可读性（Readability）。
  2. **长时程文献综述任务**：提供 80 篇本地 PDF + 评分标准，要求 agent 逐篇阅读、生成简短摘要并分配相关性评分，考验数百步的持续工具使用与状态跟踪。
- **Benchmark 与对比方法**：
  - DeepResearch Bench 上对比了约 30 个系统，包括 tavily-research (GPT-5)、thinkdepthai-deepresearch (GPT-5)、cellcog (GPT-4o)、salesforce-air-deep-research、gemini-2.5-pro-deepresearch、openai-deepresearch、claude-research、kimi-researcher、doubao-deepresearch、perplexity-Research、grok-deeper-search、sonar 系列、gpt-4o / gpt-4.1 系列等。
  - 文献综述任务中对比 Claude Code（Claude-4.5-Sonnet）与 Cursor（Claude-4.5-Sonnet、Gemini-3-Flash）。
- **评估指标**：
  - DeepResearch Bench：四维度归一化得分及总体分。
  - 文献综述：**覆盖率（coverage）**，基于日志审计，只有轨迹中包含实际 PDF 正文读取或抽取，且最终输出包含非空的、有内容依据的笔记（不仅是标题/元数据），该论文才计为已覆盖。报告最大值、最小值与平均值。
- **消融设置**：移除 file-centric state，改用压缩长上下文提示，对比 GPT-OSS-20B、Gemini-3-Flash、Claude-4.5-Sonnet。

## 4. 资源与算力

- **论文未明确说明使用的算力资源**，包括：
  - 未提及 GPU 型号、数量。
  - 未提及训练时长（事实上方法为**无需任务特定微调**的免训练架构）。
  - 仅说明使用 **20B 参数的开源模型 gpt-oss-20b** 作为骨干，并在文献综述任务中另外使用 Gemini-3-Flash 与 Claude-4.5-Sonnet 作为对比/更强骨干。
- 参数规模方面，表中估计了各对比系统的参数量（如 GPT-5 约 1000B、GPT-4o 约 200B 等），但这属于公开报告估计，非本文实际消耗。

## 5. 实验数量与充分性

- **实验组数概览**：
  - DeepResearch Bench：1 组主实验，含约 30 个系统的横向对比 + 四维度分解（Figure 2）。
  - 长时程文献综述：主结果（3 个 InfiAgent 配置 + 3 个基线配置）+ 消融实验（3 个模型 × 去除 file-centric state）。
  - 消融实验：核心消融仅 1 类（去掉文件状态、改用压缩长上下文）。
- **充分性评估**：
  - **优点**：横向对比系统数量多，覆盖多种专有与开源研究 agent；消融实验直接支撑核心主张。
  - **不足**：
    - 消融维度较单一，仅验证了“文件状态 vs 压缩长上下文”，未系统拆分各组件（如分层架构、外部注意力管线、思考记录模式）的独立贡献。
    - 未进行跨模型规模的系统内缩放实验（作者也明确说明只在单一模型尺寸上评估）。
    - 长时程任务仅一个（80 篇文献综述），任务类型较窄。
    - 与商业系统对比存在不确定性，商业 agent 可能有未公开的优化或终止启发式。
- **客观性与公平性**：
  - 使用相同骨干模型与可比提示预算，多次运行取平均以减少方差。
  - 覆盖率采用日志审计，标准相对客观。
  - 作者主动声明不主张绝对优于专有系统，态度较审慎。

## 6. 主要结论与发现

- **DeepResearch Bench**：InfiAgent 搭配 20B 开源模型取得 **41.45 总体分**，接近多个远大于其规模的专有研究 agent；在**指令遵循与可读性**上表现尤其突出，归因于文件中心状态与结构化执行管线。
- **长时程文献综述**：
  - 有文件状态时：GPT-OSS-20B 平均覆盖 **67.1**，Gemini-3-Flash 与 Claude-4.5-Sonnet 均达 **80.0**。
  - 基线：Claude Code 平均 29.1，Cursor 分别为 1.0（Claude-4.5-Sonnet）和 0.1（Gemini-3-Flash）。
  - 消融（去掉文件状态、用压缩长上下文）：覆盖率降至 3.2（GPT-OSS-20B）、21.1（Gemini-3-Flash）、27.7（Claude-4.5-Sonnet）。
- **核心发现**：
  - 显式持久状态外化是长时程稳定性的关键贡献因素，**长上下文无法替代持久状态**。
  - 免训练架构即可让 20B 开源模型保持竞争力，并显著提升长时程覆盖率。
  - 基线失败模式常表现为：提前终止、跳过条目、摘要仅复述标题而非正文内容。

## 7. 优点

- **问题定位清晰**：明确区分“持久任务状态”与“有界推理上下文”，并给出形式化定义，理论动机充分。
- **架构设计优雅**：
  - 文件中心状态作为一等公民，上下文构建为固定模式、确定性、有预算，保证 |c^bounded| = O(1)。
  - 分层 DAG 架构 + Agent-as-a-Tool 有效抑制错误传播与工具调用混乱。
  - 外部注意力管线将“阅读”成本卸载到工具层，主 agent 认知负荷低。
  - 支持检查点恢复，工程实用性强。
- **免训练通用性**：无需任务特定微调，20B 开源模型即可对标更大专有系统，降低了部署门槛。
- **实验态度审慎**：多次运行取平均、日志审计覆盖率、明确声明对比局限与不主张绝对优越。
- **消融设计直击核心主张**：直接对比“文件状态 vs 压缩长上下文”，结论有力。

## 8. 不足与局限

- **方法层面的固有限制**：
  - **不提升底层模型推理能力**：若骨干模型产生错误中间结论，错误仍会写入持久状态并向下游传播。
  - **延迟开销**：文件操作、周期状态巩固、串行 agent 执行增加延迟，不适合实时交互应用。
  - **幻觉累积风险**：小模型在超长任务中若错误信息未被验证机制捕获，下游 agent 可能继续传播。
  - **不支持并行**：严格串行执行以保证状态一致性，限制了天然可并行任务（如同时文献综述与实验编码）的效率。
- **实验覆盖限制**：
  - 评估集中于研究型任务（文档处理与多步信息综合），未覆盖反应式对话、具身交互、外部状态快速变化等场景。
  - 长时程任务仅一个，任务多样性不足。
  - 仅在单一模型尺寸上评估 InfiAgent，缺乏系统内缩放分析。
  - 消融维度单一，未逐一拆分各组件贡献。
- **偏差与公平性风险**：
  - 与商业系统对比存在未公开优化或终止启发式的影响，作者也承认不主张绝对优越。
  - DeepResearch Bench 分数直接取自基准评估，但不同系统的参数规模估计来自公开报告，可能不精确。
- **资源信息缺失**：未报告 GPU 型号、数量、训练/推理时长等算力细节，影响可复现性与成本评估。
- **应用限制**：更适合长时程、知识密集型工作流，而非实时交互场景。

（完）

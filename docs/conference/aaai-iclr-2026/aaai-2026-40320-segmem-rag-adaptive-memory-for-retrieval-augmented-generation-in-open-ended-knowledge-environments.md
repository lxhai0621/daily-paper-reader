---
title: "SegMem-RAG: Adaptive Memory for Retrieval-Augmented Generation in Open-Ended Knowledge Environments"
title_zh: SegMem-RAG：面向开放知识环境的自适应记忆检索增强生成
authors: "Xuanbo Fan, Tianqi Zhao, Yi Cheng, Chi Xiu, Jiaxin Guo, Boci Peng, Bingjing Xu, Jessica Zhang, Feng Sun, Yan Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40320/44281"
tags: ["query:ma-kf"]
score: 8.0
evidence: 通过经验学习和自反思更新结构化记忆，自适应路由查询以提升开放环境下RAG准确性
tldr: 真实世界语料异质且无标注，固定检索逻辑难以应对。SegMem-RAG提出经验驱动的记忆增强检索框架：它根据历史经验习得跨多个未标注语料的查询路由，并通过自反思增量更新结构化记忆，无需监督即可自适应调整检索行为。实验表明该方法能有效提升开放知识环境下的检索与生成准确性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40320/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40320/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1468, \"height\": 979, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40320/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 845, \"height\": 862, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40320/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1826, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40320/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 316, \"label\": \"Table\"}]"
motivation: 真实语料异质无标签，固定检索逻辑不适应开放变化的知识环境。
method: 构建可增量更新的结构化记忆，基于经验学习查询路由，并用自反思在无监督下引导检索。
result: 实验证实该方法在多个未标注语料上检索与生成准确性优于固定检索方法的基线。
conclusion: 自适应记忆与自我反思能显著提升RAG在开放知识环境中的鲁棒性与准确性。
---

## Abstract
Retrieval-Augmented Generation (RAG) improves the factual accuracy of large language models by grounding responses in external content. However, most RAG systems assume access to static and well-organized corpora with fixed retrieval logic. In practice, real-world sources are heterogeneous and unlabeled, including user-uploaded documents, manuals, and datasets. Effective access in such settings requires adaptive and self-directed retrieval behavior.
We present SegMem‑RAG, a memory-augmented RAG framework that learns to route queries across multiple unlabeled corpora based on experience. It incrementally updates a structured memory and uses self-reflection to guide retrieval over time without supervision. Experimental results demonstrate that SegMem‑RAG significantly outperforms recent baselines in generation quality on multi-corpus QA tasks.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- 现有 RAG 系统的核心前提是**静态、有组织、有标签的语料库**，并搭配固定检索逻辑；但现实世界中的知识环境通常是**动态、异构、无标签**的（如用户上传文档、手册、日志、数据集等）。
- 在开放环境中，用户通过统一接口提问，不指定知识源，系统需要**自主决定从哪里检索、检索什么以及如何组织答案**。
- 知识源会随时间**新增或废弃**，结构、粒度、风格差异大；人工标注和查询日志很快过时，无法依赖静态监督。
- 已有方法存在明显不足：
  - 检索规划方法（如 ResLLM、Omni-RAG）在知识变化时需要重新训练；
  - 会话内 agent（如 ReAct、Reflexion）缺乏跨会话/跨语料的长期学习机制；
  - 基于接口/工具描述的方法（如 EasyTool、DRAFT）无法泛化到无结构化 schema 的开放文本语料。
- 论文因此提出一个**自指导（self-guided）RAG 范式**，要求系统具备三种认知能力：
  1. **局部化规划**：将检索决策从干扰性上下文中隔离出来；
  2. **检索感知**：反思检索内容是否真正满足信息需求；
  3. **自适应学习**：通过积累反馈持续修正检索偏好。

## 2. 方法论：核心思想与关键技术细节

### 总体框架
SegMem-RAG 由三个紧密耦合组件构成，在不依赖外部监督和重训练的前提下实现自适应检索：

**（1）Segment Planner（分段规划器）**
- 受认知科学中**事件分割理论（Event Segmentation Theory）**启发，将推理过程分解为局部化、语义连贯的决策段（segment）。
- 通过**段图编译（Segment Graph Compilation）**将动作 schema 编译为有向图（节点=状态，边=合法转移），形成有限的推理状态空间，支持符号化规划。
- 推理时采用**分段推理**：在状态 s，综合微指令 Is、长期记忆 Es = M.recall(s)、短期上下文 Cs = S.relevant(s)，由基础模型输出决策：o= M.infer(Is, Es, Cs)。执行检索后更新状态直至终止。

**（2）Feedback Evaluator（反馈评估器）**
- 每个检索段执行后，评估器对比检索内容与当前子查询意图，生成两类信号：
  - **二元成功标签** yi ∈ {0,1}；
  - **描述性反思**（自然语言反馈，说明内容与期望是否对齐）。
- 维护各语料的失败计数器 fc，当某个语料检索失败时累加；这些统计作为**符号先验**影响后续源选择——惩罚持续低效的语料，促进更可靠替代源的探索，实现无监督的**偏好自适应**。

**（3）Memory Controller（记忆控制器）**
- 维护三层符号化、结构化记忆：
  - **程序性记忆（Mproc）**：记录查询模式与偏好语料的关联启发式规则；
  - **语义记忆（Msem）**：维护每个语料的能力描述与可靠性统计（如失败次数）；
  - **情景性记忆（Mepis）**：记录单个检索片段的具体先例（查询、所选语料、结果摘要）。
- 使用**符号相似度**对外部子查询与存储条目统一检索，避免依赖稠密嵌入，支持中英文等多语言。
- 记忆更新以**异步批量**方式完成，避免在实时交互中引入延迟。

**（4）Coldstart Explorer（冷启动探索器）**
- 当某语料交互次数低于阈值时，主动触发探测段：从程序性和情景性记忆中采样有代表性的子查询，对该语料发起检索，评估结果并写入记忆，快速建立对新语料的基础经验，提升低利用率语料的覆盖率。

## 3. 实验设计：数据集、Benchmark 与对比方法

### 知识环境设置
- 构建了包含 19 个独立、无标签、异构语料库的统一检索环境，涵盖论证、生物医学、金融、知识库、法律、科学、网页、维基等8个领域，文件类型包括段落片段、文档、摘要、文章、教科书、报告、知识三元组等（如表1）。
- 语料规模不归一化，保留真实世界的不均衡性；每个语料用 multilingual-e5-large 独立索引。
- 各方法只获得语料的数字 ID 和 GPT-4o 自动生成的简短自然语言描述，不包含任何下游任务信息。

### 任务与指标
- **开放域 QA**：NQ、TriviaQA、PopQA、HotpotQA、2WikiMultiHopQA（单跳+多跳），使用 token-level F1。
- **金融 QA**：OmniEval 的四个子任务（抽取式、长形式、多跳、构造型），使用 fact-level F1（LLM 判官）。
- **生物医学 QA**：BioASQ，使用 fact-level F1。

### 对比基线（按能力分组）
- **检索控制**：Prompting（固定提示）、BlindRAG（随机选语料）。
- **Agentic 推理**：ResLLM（描述式语料路由）、ReAct（推理+检索交替）。
- **记忆与反思**：Reflexion（步骤级语言自我反馈）、DRAFT（利用交互历史优化指引）。
- **Oracle 上限**：EnumRAG（穷举所有语料检索）、GoldRAG（仅检索最优单语料）。

### 实现细节
- 推理模型：Qwen2.5-7B-Instruct；判官模型：Qwen2.5-32B-Instruct。
- 每个查询最多 32 个推理段；记忆检索和知识检索各取 top-5；每数据集随机抽样 500 个 QA 对测试。

## 4. 资源与算力

- 论文**未明确报告 GPU 型号、数量、训练时长等算力信息**。
- 可推断：框架是 **训练-free** 的（无需重训练或参数更新），推理阶段使用 Qwen2.5-7B-Instruct，评估阶段使用 Qwen2.5-32B-Instruct 作为 LLM 判官；具体硬件配置和推理成本未在文中说明。

## 5. 实验数量与充分性

- **主实验**：表2 覆盖 3 大领域（开放域、金融、生物医学）、10 个 QA 任务，对 8 类方法进行系统比较，规模较充分。
- **消融实验**：在 NQ 和 PopQA 上分别移除四个核心组件（Segment Planner、Feedback Evaluator、Memory Controller、Coldstart Explorer），共 8 组对照，覆盖所有关键模块。
- **优势**：与强基线（ReAct、Reflexion、DRAFT）及 oracle 方法（EnumRAG、GoldRAG）对比，且所有方法共享相同的语料描述与控制条件，公平性良好。
- **不足**：实验仅覆盖 QA 类任务，未涉及对话、摘要等开放式知识环境；单个数据集的测试规模为 500 条，统计显著性未报告；不同语料间规模差异极大，对检索公平性存在潜在影响。

## 6. 主要结论与发现

1. **SegMem-RAG 在整体平均性能上优于全部基线，甚至超过 oracle 方法（EnumRAG、GoldRAG）**——特别是在多跳任务（HotpotQA、2WikiMultiHopQA）上优势明显。
2. **准确的语料选择在多源环境中至关重要**：EnumRAG 远优于 Prompting，而随机选源的 BlindRAG 表现最差，证明盲目选择会带来有害噪声。
3. **仅依赖静态语料描述的检索不足**：ResLLM、BlindRAG 表现差，ReAct 提升有限——静态摘要和浅层交互不足以应对复杂多源环境。
4. **反馈驱动的目标检索优于穷举枚举和单一最优语料约束**：说明分段反馈+符号记忆能实现比暴力枚举更高效的证据定位。
5. **消融结果**（表3）：移除 Memory Controller 带来的下降最大（NQ −33.7%，PopQA −40.4%），其次为 Segment Planner（PopQA −30.6%）和 Feedback Evaluator；Coldstart Explorer 的移除也造成 9%–10% 的性能损失。

## 7. 方法或实验设计的优点

- **训练-free 的自适应机制**：通过符号记忆和反馈实现持续改进，无需重训练或人工标注，适合动态环境快速部署。
- **模块化设计**：分段规划、反馈评估、记忆控制三组件解耦，易于扩展（新语料/新工具只需更新 action schema）。
- **认知科学启发**：事件分割理论和三层记忆模型（程序性/语义性/情景性）提供了坚实的理论基础，设计逻辑自洽。
- **符号化记忆**支持解释性与多语言适用，不依赖稠密嵌入，计算开销低。
- **异步记忆更新**规避了实时推理延迟问题。
- **冷启动机制**解决了新语料/长尾语料无历史经验的问题，设计上有前瞻性。
- **实验对比全面**：既包含强基线，又包含两种 oracle 上限方法，验证了自指导检索的上限价值。

## 8. 不足与局限

- **算力与效率信息缺失**：未报告 GPU 型号/数量、推理耗时、记忆更新开销等，无法评估工程落地成本。
- **领域覆盖有限**：虽然语料多，但任务类型仅限于 QA，未验证在对话生成、摘要、结构化知识更新等更广泛场景下的表现。
- **评估指标风险**：事实级 F1 依赖 LLM 判官，可能存在判断偏差；token-level F1 难以完全反映语义质量。
- **实验规模有限**：每数据集仅 500 条，缺少多次运行的标准差和显著性检验，结论的稳健性有待证明。
- **冷启动依赖记忆种子**：如果没有初始的程序性/情景性记忆，探测质量可能不足。
- **动态性验证不足**：论文强调语料“动态变化”，但实验中语料库是固定的；对语料新增/废弃场景的适应性没有专门实验。
- **没有与更新的长上下文 RAG 或多智能体框架比较**，如长上下文模型直接处理全语料的方法。

（完）

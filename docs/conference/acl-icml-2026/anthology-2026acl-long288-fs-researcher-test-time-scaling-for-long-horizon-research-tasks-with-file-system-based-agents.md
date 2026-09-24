---
title: "FS-Researcher: Test-Time Scaling for Long-Horizon Research Tasks with File-System-Based Agents"
title_zh: "FS-Researcher:基于文件系统智能体的长时程研究任务测试时扩展"
authors: "Chiwei Zhu, Benfeng Xu, Mingxuan Du, Shaohan Wang, Xiaorui Wang, Zhendong Mao, Yongdong Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.288.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: "基于文件系统的双智能体工作区,突破上下文窗口限制"
tldr: "深度研究等长时程任务轨迹常超出模型上下文窗口,压缩证据收集与报告撰写预算,阻碍测试时扩展。本文提出FS-Researcher,基于文件系统的双智能体框架,通过持久工作区突破上下文限制:上下文构建智能体像图书管理员一样浏览网络、撰写结构化笔记并将原始资料归档为可无限增长的分层知识库,报告撰写智能体再逐节生成报告。该设计实现长时程研究的高效扩展与知识发现。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long288/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 3164, \"height\": 3630}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long288/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 4346, \"height\": 3155}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long288/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 2671, \"height\": 1772}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long288/fig-004.webp\", \"caption\": \"\", \"page\": 7, \"index\": 4, \"width\": 2671, \"height\": 1654}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long288/fig-005.webp\", \"caption\": \"\", \"page\": 18, \"index\": 5, \"width\": 3022, \"height\": 1023}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long288/fig-006.webp\", \"caption\": \"\", \"page\": 18, \"index\": 6, \"width\": 3022, \"height\": 1023}]"
motivation: "长时程深度研究轨迹超出模型上下文窗口,压缩证据与撰写预算,阻碍测试时扩展。"
method: "提出基于文件系统的双智能体框架FS-Researcher,以持久工作区分层知识库存储笔记与资料,并逐节撰写报告。"
result: "该框架使研究规模突破上下文长度限制,支持证据收集与报告生成的持续扩展。"
conclusion: 文件系统式持久工作区为长时程智能体研究任务提供可扩展的记忆与知识组织方案。
---

## Abstract
Deep research is emerging as a representative long-horizon task for large language model (LLM) agents. However, long trajectories in deep research often exceed model context limits, compressing token budgets for both evidence collection and report writing, and preventing effective test-time scaling. We introduce FS-Researcher, a file-system-based, dual-agent framework that scales deep research beyond the context window via a persistent workspace. Specifically, a Context Builder agent acts as a librarian which browses the internet, writes structured notes, and archives raw sources into a hierarchical knowledge base that can grow far beyond context length. A Report Writer agent then composes the final report section by section, treating the knowledge base as the source of facts. In this framework, the file system serves as a durable external memory and a shared coordination medium across agents and sessions, enabling iterative refinement beyond the context window. Experiments on two open-ended benchmarks (DeepResearch Bench and DeepConsult) show that FS-Researcher achieves state-of-the-art report quality across different backbone models. Further analyses demonstrate a positive correlation between final report quality and the computation allocated to the Context Builder, validating effective test-time scaling under the file-system paradigm. The code and data are open-sourced at https://github.com/Ignoramus0817/FS-Researcher.

---

## 论文详细总结（自动生成）

# FS-Researcher 论文中文总结

## 1. 核心问题与整体含义

- **研究背景**：Deep Research（深度研究）正在成为 LLM 智能体最具代表性的长时程（long-horizon）任务，要求智能体以博士级专业水平，系统地从互联网搜集证据并综合成一份超过 10K token 的长篇报告，往往需要浏览数百个网页。
- **核心矛盾**：模型上下文窗口有限，而长时程研究轨迹极易超出该限制。一旦超限，用于**证据收集**与**报告撰写**的 token 预算被严重压缩，智能体被迫中止，无法进行有效的**测试时扩展（test-time scaling）**。
- **现有方案的局限**：主流做法是把网页浏览卸载给子智能体、或对工具观测做摘要压缩，仅在主智能体上下文中保留精炼事实。这类方法只是"权宜之计"：
  - 仍受制于模型上下文的**硬上限**；
  - 是有损瓶颈，细粒度证据与出处（provenance）可能丢失，摘要误差会逐级累积；
  - 思考、工具观测等中间状态是**一次性消耗品**，会话结束后即被丢弃，无法支撑迭代式精炼。
- **整体含义**：受编程智能体与 AI IDE 中"文件系统工作区"范式的启发，论文提出 **FS-Researcher**——一个基于文件系统的双智能体框架，把研究状态与证据外化（externalize）到可持久、可无限增长的工作区中，从而突破上下文窗口，实现长时程研究任务的有效测试时扩展。

## 2. 方法论

### 2.1 核心思想
- 将深度研究拆分为**两个阶段、两个智能体**：
  1. **Context Builder（上下文构建者）**：像图书管理员一样浏览互联网、阅读文档、撰写结构化笔记，并归档原始网页，构建分层知识库（KB），其规模可远超上下文长度。
  2. **Report Writer（报告撰写者）**：以知识库为**唯一事实来源**，按需加载信息，逐节（section by section）撰写最终报告。
- **文件系统的三重作用**：（1）复刻人类处理复杂长时程任务的天然环境；（2）存储远超上下文窗口的信息，支持按需访问而不溢出；（3）使计划、错误日志等中间产物**持久化、可回溯**，支持跨会话迭代精炼。
- 文件 I/O 引入的延迟可忽略（占总墙钟时间 <0.03%）。

### 2.2 通用架构
- **工具**（见表 1）：
  - 文件系统工具：`ls`、`grep`（简化版 UNIX grep，支持正则）、`read_file`（支持分页）、`insert/delete/replace`（按行修改文件）。
  - 网页浏览工具：`search_web`（Google SERP API，返回 URL 与摘要）、`read_webpage`（Jina AI API，支持分页）。
- **工作流**：每个智能体采用标准 ReAct 架构，可形式化为：

  - `Tᵢ, Aᵢ = Mθ(T_{j<i}, A_{j<i}, O_{j<i}, P)`
  - `Oᵢ = Execute(Aᵢ)`

  其中 `Tᵢ / Aᵢ / Oᵢ` 分别为第 i 步的思考、动作与观测，`Mθ` 为参数为 θ 的模型，`P` 为提示（系统提示 + 用户查询），`Execute(·)` 为工具执行函数。
- **工作区**：所有文件均为 Markdown 格式，分为两类：
  - **交付物（deliverables）**：最终输出文件，随任务类型而异。
  - **控制文件（control files）**：
    - **Todos**：待办列表，状态为 `[PENDING]` / `[IN-PROGRESS]` / `[COMPLETE]`；
    - **Checklist**：验收标准（文件格式规则、质量检查等）；
    - **Logs**：执行轨迹日志。
  - 原生支持**多会话（multi-session）**工作流：每次会话开始时检查工作区、制定计划；执行中动态更新 todo；会话结束时对照 checklist 评估，把不合规项重新标记为 `[IN-PROGRESS]`，并判断整体任务是否完成。Todos 由智能体自主生成，Checklist 由人工静态策划。

### 2.3 Context Builder 阶段
- 交付物：一个 `index.md` 文件 + 两个目录 `knowledge_base/` 与 `sources/`。
  - `index.md`：知识库的"目录"，包含（1）研究主题的拆解，（2）KB 的分层结构；Todos 随其更新。
  - `knowledge_base/`：树状结构的笔记，文件夹/文件名具描述性，反映语义关系。
  - `sources/`：归档的原始网页；笔记中每条陈述都带**引用**指向 `sources/` 中的文件，保证可追溯。
- **非线性流程**：`index.md` 与 `knowledge_base/` 随浏览过程**动态更新**，而非先定结构再填充。
- 每次会话结束进行 checklist 自查，发现问题则标记为 `[IN-PROGRESS]` 并记入日志；迭代精炼直到达到会话预算上限或自查无问题为止。

### 2.4 Report Writer 阶段
- **移除网页浏览工具**，知识库为唯一事实来源，交付物为 `report.md`。
- **多会话分段撰写**（关键设计）：若一次性生成整篇报告，容易沦为事实罗列，缺乏解释与深度分析。因此：
  - 首个写作会话生成大纲（`report_outline.md`），该大纲同时充当 todo 文件，每节带状态标记；
  - 后续每次会话**只撰写一节**；
  - 每节完成后按**节级 checklist** 自查，通过才标为 `[COMPLETE]`；
  - 全部完成后按**报告级 checklist** 做整体审查，发现问题则把对应节重新标为 `[IN-PROGRESS]`；
  - 此阶段**无预算上限**，直到报告完成并通过全部审查。

## 3. 实验设计

### 3.1 数据集 / Benchmark
- **DeepResearch Bench**：100 个博士级研究任务，覆盖 22 个领域；双轴评估——报告质量用 **RACE**（基于参考的自适应准则驱动评估 + 动态权重，含 Comprehensiveness、Insight/Depth、Instruction-Following、Readability 四维），引用可靠性用 **FACT**（含 Effective Citations 与 Citation Accuracy）。使用 Gemini-2.5-Pro 作 RACE 评判、Gemini-2.5-Flash 作 FACT 评判，以 Gemini-2.5-Pro Deep Research 报告为参考。
- **DeepConsult**：103 个（论文评估中提及 102 个查询）商业/咨询类查询，LLM-as-a-judge 成对比较，4 个维度：Instruction Following、Comprehensiveness、Completeness、Writing Quality；多次评判（6 次独立试验）聚合以减少位置偏差。
- **BrowseComp**：1,266 个复杂但**答案可验证**的 agentic search 问题，随机抽样 100 条测试，作为 LLM-as-judge 之外的客观指标补充。
- 所有分数为 **3 次测试的平均**。

### 3.2 对比方法
- **专有深度研究产品**：Claude-DeepResearch、OpenAI-DeepResearch、Gemini-2.5-Pro-DeepResearch。
- **开源系统与近期论文**：LangChain-Open-Deep-Research、WebWeaver、RhinoInsight、EnterpriseDeepResearch。
- **主干模型**：Gemini-2.5-Pro、GPT-5、Claude-Sonnet-4.5（另加 GPT-5-mini 做可及性实验）。
- 额外的对照：Gemini-2.5-Pro 在"仅带搜索工具"与"官方 harness"两种配置下的表现（附录 I）。

## 4. 资源与算力

- **论文未报告任何 GPU 型号、数量或训练时长**。该工作本质是**推理时（test-time）框架**，不涉及模型训练，因此未提供训练算力信息。
- 文中给出的**经济与时间开销**数据：
  - LLM API 成本（10 条采样 DeepResearch Bench 查询平均，每查询）：3 轮 GPT-5 **$6.10**、5 轮 **$8.16**、10 轮 **$12.54**；3 轮 Claude **$9.31**；GPT-5-mini 10 轮 **$2.51**。
  - 上下文压缩（用 GPT-5-mini 摘要网页）可降低 Context Builder 成本 **47%**（$3.77 → $2.00），性能几乎无损（51.18 → 51.14 RACE）。
  - **墙钟时间分解**：Context Building 阶段 LLM 调用 236.72s + 网页工具 219.96s + 文件 I/O 0.055s；Report Writing 阶段 LLM 调用 376.65s + 网页工具 0s + 文件 I/O 0.186s。文件 I/O 占比 <0.03%。

## 5. 实验数量与充分性

### 实验规模概览
- **主实验**：3 个 benchmark（DeepResearch Bench、DeepConsult、BrowseComp），3 个主干模型 × 多组基线对比。
- **测试时扩展分析**：在 DeepResearch Bench 上随机采样 **10 条查询**，以 GPT-5 为骨干，比较 3/5/10 轮 Context Builder 预算对 KB 规模与报告质量的影响。
- **模块消融（3 组）**：
  1. 去掉持久工作区（移除控制文件、把结构化工作区退化为扁平笔记）；
  2. 合并双智能体为单智能体（同一会话内浏览 + 写作，跑 3 轮）；
  3. 取消逐节写作（一次性生成整篇报告）。
- **补充实验**：
  - Agent harness 贡献拆解（仅搜索工具 vs 官方 harness vs FS-Researcher）；
  - 小模型可及性（GPT-5-mini 10 轮 vs OpenAI-DeepResearch vs GPT-5 3 轮）；
  - 可读性恢复（10 轮 + 后处理改写）；
  - 上下文压缩成本实验；
  - 墙钟延迟剖析；
  - 工具使用频率–位置热力图分析（两个阶段前三次迭代）；
  - 案例分析（3/5/10 轮 KB 与报告演化）。

### 充分性与客观性评估
- **优点**：覆盖"开放式报告生成"（LLM-as-judge）与"答案可验证"（BrowseComp）两类评估，避免单一评判范式偏差；消融设计针对性强，能定位各模块贡献；分数取 3 次平均，降低随机性。
- **需注意的局限**：
  - 扩展性分析与消融实验仅在 **10 条采样查询**上完成，统计代表性有限；
  - DeepConsult 上 Claude-Sonnet-4.5 的结果**仅基于采样的 20 条查询**（预算限制），与其他方法并非完全同条件对比；
  - 评判依赖 LLM-as-a-judge（Gemini 系列），存在评判者偏好风险（如 Claude 报告因术语密集、引用密集而在 Writing Quality 上得分偏低）；
  - 基线各自使用不同骨干模型，跨类别比较时存在骨干强度混淆，论文通过"同骨干对比"（GPT-5 vs LangChain、Gemini vs RhinoInsight）部分缓解。

## 6. 主要结论与发现

- **SOTA 报告质量**：
  - DeepResearch Bench：FS-Researcher（Claude-Sonnet-4.5）达 **53.94 RACE**，比最强基线 RhinoInsight 高 **+3.02**；Comprehensiveness 与 Insight 提升显著（+3.74 / +4.4）。
  - DeepConsult：最高 **80.00% 胜率**、最佳平均分 **8.33**，失败率降至 9.58%。
  - BrowseComp（100 条抽样）：Claude 骨干 **55.0% vs 官方 harness 43.9%**；GPT-5 骨干 **68.0% vs 54.9%**。
- **增益并非仅来自骨干模型**：同 GPT-5 骨干下比 LangChain Open Deep Research 高 +2.16 RACE；同 Gemini-2.5-Pro 骨干下比 RhinoInsight 高 +1.59 RACE。Gemini-2.5-Pro 仅带搜索工具为 31.90 RACE，官方 harness 为 49.71，FS-Researcher 进一步到 52.51（Insight +5.58），说明 **agent harness 本身贡献巨大**。
- **测试时扩展成立**：报告质量与分配给 Context Builder 的计算量呈**正相关**；3→5 轮增益明显，5→10 轮出现**边际递减**（KB 趋于完整）。
- **可读性与信息密度的权衡**：Readability 在 5 轮达峰（51.93），10 轮略降至 51.66，原因是 KB 增大后报告风格更技术化、术语与内联引用更密集；这是**呈现层问题**，通过针对性后处理改写可恢复（51.66 → 51.92）而不损其他维度，说明二者并非本质冲突。
- **模块重要性排序**（以 RACE 降幅衡量）：双智能体合并（-10.35）> 逐节写作取消（-5.13）> 持久工作区移除（-4.07）；其中 Insight 维度受损最严重，说明这些设计主要贡献**深度推理与覆盖度**而非表层格式合规。
- **成本与可及性**：GPT-5-mini 在 10 轮设置下达到 46.63 RACE，接近 OpenAI-DeepResearch（46.45），成本仅 $2.51/查询；框架与上下文压缩方法正交，可进一步降本。

## 7. 优点

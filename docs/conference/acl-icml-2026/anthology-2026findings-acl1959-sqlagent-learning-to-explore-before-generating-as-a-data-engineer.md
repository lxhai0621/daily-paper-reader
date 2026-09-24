---
title: "SQLAgent: Learning to Explore Before Generating as a Data Engineer"
title_zh: SQLAgent：像数据工程师一样先探索再生成
authors: "Wenjia Jiang, Yiwei Wang, Boyan Han, Joey Tianyi Zhou, Chi Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1959.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 查询生成前自主构建数据库知识库
tldr: 大模型在自然语言转 SQL 任务中表现亮眼，但面对真实复杂场景时，因 SQL 推理高度依赖特定模式、语义含糊且连接路径复杂而难以泛化。作者提出 SQLAgent 两阶段框架，将知识获取与查询生成解耦：在探索阶段，系统以类似蒙特卡洛树搜索的策略自主导航数据库模式，构建数据库专属知识库并生成结构化三元组。该自主知识发现机制显著提升了复杂数据库问答的泛化能力。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-006.webp\", \"caption\": \"\", \"page\": 4, \"index\": 6, \"width\": 429, \"height\": 491}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-007.webp\", \"caption\": \"\", \"page\": 6, \"index\": 7, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-008.webp\", \"caption\": \"\", \"page\": 6, \"index\": 8, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-009.webp\", \"caption\": \"\", \"page\": 6, \"index\": 9, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-010.webp\", \"caption\": \"\", \"page\": 6, \"index\": 10, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-011.webp\", \"caption\": \"\", \"page\": 6, \"index\": 11, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-012.webp\", \"caption\": \"\", \"page\": 6, \"index\": 12, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-013.webp\", \"caption\": \"\", \"page\": 6, \"index\": 13, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-014.webp\", \"caption\": \"\", \"page\": 6, \"index\": 14, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-015.webp\", \"caption\": \"\", \"page\": 6, \"index\": 15, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-016.webp\", \"caption\": \"\", \"page\": 6, \"index\": 16, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-017.webp\", \"caption\": \"\", \"page\": 6, \"index\": 17, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-018.webp\", \"caption\": \"\", \"page\": 6, \"index\": 18, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1959/fig-019.webp\", \"caption\": \"\", \"page\": 6, \"index\": 19, \"width\": 512, \"height\": 512}]"
motivation: 现有文本转 SQL 方法因依赖特定模式、语义含糊与复杂连接路径，难以在真实复杂数据库场景中泛化。
method: 提出两阶段框架，将知识获取与查询生成解耦，用类似蒙特卡洛树搜索的策略自主构建数据库专属知识库。
result: 该探索式知识构建方法提升了复杂数据库自然语言接口的泛化能力。
conclusion: 研究展示了自主知识发现对结构化数据问答的价值，为智能体式数据库交互提供新思路。
---

## Abstract
Large Language Models have recently shown impressive capabilities in reasoning and code generation, making them promising tools for natural language interfaces to relational databases. However, existing approaches often fail to generalize in complex, real-world settings due to the highly database-specific nature of SQL reasoning, which requires deep familiarity with unique schemas, ambiguous semantics, and intricate join paths. To address this challenge, we introduce a novel two-stage LLM-based framework that decouples knowledge acquisition from query generation. In the Exploration Stage, the system autonomously constructs a database-specific knowledge base by navigating the schema with a Monte Carlo Tree Search–inspired strategy, generating triplets of schema fragments, executable queries, and natural language descriptions as usage examples. In the Deployment Stage, a dual-agent system leverages the collected knowledge as in-context examples to iteratively retrieve relevant information and generate accurate SQL queries in response to user questions. This design enables the agent to proactively familiarize itself with unseen databases and handle complex, multi-step reasoning. Extensive experiments on large-scale benchmarks demonstrate that our approach significantly improves accuracy over strong baselines, highlighting its effectiveness and generalizability.

---

## 论文详细总结（自动生成）

# SQLAgent 论文深度总结

## 一、核心问题与整体含义（研究动机与背景）

- **领域背景**：Text-to-SQL 旨在将自然语言问题翻译为可执行 SQL，以降低结构化数据的访问门槛。LLM 在推理与代码生成上的进展使其成为该任务的理想候选。
- **核心痛点**：现有方法在真实企业级数据库上泛化能力差，性能显著下降。根本原因在于 **SQL 推理是"数据库专属"的而非可移植的**：
  - 有效查询严格依赖独特的模式结构；
  - 列名语义含糊、需要依赖具体命名消歧；
  - 推理必须与特定数据库的 join 路径精确对齐。
- **关键洞察**：人类数据工程师之所以能胜任，是因为他们**先建立对数据库模式与关系的深度熟悉**，再动手写查询。论文据此提出：在最终翻译任务之前，先设置一个"前置知识构建"过程。
- **整体含义**：将知识获取与查询生成解耦，让 Agent 在用户查询到来之前就主动"熟悉"未知数据库，从而把 SQL 生成从"零样本猜测"变为"基于已验证经验的合成"。

## 二、方法论

### 2.1 核心思想
两阶段 LLM 框架：
1. **Exploration Stage（探索阶段）**：自主构建数据库专属知识库；
2. **Deployment Stage（部署阶段）**：双 Agent 利用该知识库进行上下文学习，迭代生成 SQL。

### 2.2 数据库模式表示：Shared Field Group
- 企业库常因时间分片产生大量结构完全相同的表（如日表、小时快照）。逐表建模会为 N 张分片表 × M 个共享字段产生 **O(N×M)** 条边，模式图过大无法遍历。
- 方案：把模式表示为可遍历的树状图，节点类型包括 Database / Schema / Table / Field / **Shared Field Group**。
- **形式化定义**：对表 Ti 的模式签名 Si = {(fi,j, τi,j)}，共享字段组 Gk = { Ti ∈ T | Hash(sort(Si)) = Hash(sort(Sk)) }，其中 sort(·) 消除列序影响，Hash(·) 生成 128 位唯一标识。
- **效果**：每张表只连到对应组节点，边复杂度从 O(N×M) 降为 **O(N+M)**，提升可遍历性与可解释性。

### 2.3 探索阶段：LLM 引导的树搜索
- **目标**：为模式关键组件生成三元组 **(S, Q, U)** ——模式子结构、可执行 SQL、自然语言描述。
- **搜索策略**：受 MCTS 启发，但**替换 UCT 策略**为 **LLM-as-Policy-and-Evaluator**。原因是 SQL 有效性是二值的、语义质量是连续且依赖上下文的，标量奖励不适用；LLM 可用自然语言反馈区分"语法无效路径"与"语义无产出路径"。
- **四阶段流程**：
  1. **LLM 引导的选择与扩展**：给定当前查询状态（动作序列）与可达表的简化 JSON 上下文，LLM 从离散动作空间（Select Column、Add Constraint、Apply Aggregation、Introduce Join、Add Group By、Add Ordering、Add Having 等）中选择下一步，生成子节点。
  2. **SQL 模拟**：从节点生成完整 SQL，**两阶段验证**——先用 SQL parser 检查语法，再对实库执行验证运行时有效性。成功条件：语法有效 + 无运行时错误 + 返回非空非平凡结果集。成功后由 LLM 生成自然语言描述 U，补全三元组。
  3. **反向传播**：成功路径在贡献的实体节点上记录正反馈；失败路径记录负反馈，降低该路径选择优先级。反馈被注入后续选择 prompt，形成自精炼过程。
  4. **终止条件**：达到目标三元组数量或最大迭代预算。

### 2.4 部署阶段：双 Agent SQL 合成
- **InfoAgent（模式接地与上下文管理）**：
  - *Schema Grounding*：将每列序列化为 `"[Name]: name; [Type]: type; [Desc]: comment"`，用句嵌入模型预计算列向量索引；查询时抽取语义关键词，做 top-k 相似度检索。
  - *Context Expansion*：LLM 扮演数据库专家，推理已检索组件之间的关系，**推断并补充必要的 join key**（如从 users.user_name 与 orders.order_amount 推出 user_id / customer_id）。
- **GenAgent（知识驱动合成）**：
  - 将用户问题与 InfoAgent 提供的模式上下文**联合编码**（代码嵌入模型），避免仅编码问题导致检索到结构不匹配的示例；
  - 对知识库中每个三元组的 SQL 分量 Q 的预计算嵌入做相似度搜索，取 top-k 三元组作为**数据库专属 few-shot 示例**；
  - 组合"用户查询 + 精炼模式上下文 + 检索示例"生成最终 SQL。
- **协作精炼循环**：执行失败时 InfoAgent 并行做两件事——(1) **上下文剪枝**，移除存在于上下文但未出现在生成查询中的组件；(2) **重新分析用户查询**，召回初次接地遗漏的次级关键词与候选表列。执行成功则进行 **Semantic Fidelity Check**（语义保真检查），确认结果符合用户原始意图。循环至成功或达到迭代上限。

## 三、实验设计

### 3.1 数据集 / 场景
- **Spider 2.0-Snow**：企业级基准，547 个示例、150+ 数据库、每库约 800 列；按 token 数分三档：Easy（<80）、Medium（80–159）、Hard（≥160）。
- **BIRD**（dev set）：覆盖更多样的真实数据库，模式复杂度更温和、自然语言变化更丰富，用于检验跨基准泛化性。

### 3.2 评测指标
- **Execution Accuracy (EX)**：比较预测与真值 SQL 在数据库实例上的执行结果，可容纳一题多解。
- **PASS@K**：K 次运行内是否产出正确结果（应对输出随机性）。
- **效率**：平均每查询的 LLM 调用次数与数据库（DB）执行次数。

### 3.3 对比方法
| 类别 | 方法 |
|---|---|
| 多 Agent 任务分解 | Spider-Agent |
| 检索 + 迭代自精炼 | Re-FoRCE |
| 强化学习 | AlphaSQL、MARS-SQL |
| 免训练 CoT | CHASE-SQL |
| 内部消融基线 | 文本模式索引 + 检索 DDL + 执行反馈迭代精炼 |

## 四、资源与算力

- **明确提及的部分**：
  - 主干 LLM：**GPT-4o**（除非特别说明），所有 LLM 温度设为 0.7；
  - 本地模型推理使用**两块 NVIDIA RTX 4090 GPU**；
  - 多 Agent 框架基于 **LangGraph** 构建；
  - 向量嵌入使用 OpenAI **text-embedding-3-small**，向量化由 **Faiss** 处理；
  - 图建模基于 **Neo4j**，遍历使用 **Cypher**。
- **未明确说明的部分**：
  - **未报告 GPU 总训练/推理时长**（该方法为免训练的 prompt-based 框架，不涉及模型训练）；
  - 未披露探索阶段的总 API 调用量或总花费（仅给出单库 token 成本）；
  - 未说明 RTX 4090 的具体用途与运行规模。

## 五、实验数量与充分性

### 实验规模概览
- **主实验**：Spider 2.0-Snow 上按 Easy/Medium/Hard 分档对比 5 类基线 + 内部基线；
- **消融实验**：分步消融（Baseline → w/ Exp. Stage → Full Method）+ **组件退化消融**（7 种配置 × 5 轮迭代）；
- **成本摊销分析**：Direct Input / Chunked Retrieval / SQLAgent 三种策略的 token 成本对比（@10、@100 查询规模）；
- **动态探索 vs. 静态语义视图**对比（同 GPT-4o 主干）；
- **迭代过程性能曲线**（有/无知识库，1–8 轮）；
- **超参数分析**：top-k（1/3/5/7）与 temperature（0/0.3/0.5/0.7/1.0）；
- **BIRD 泛化实验**；
- **LLM 主干分析**：4 个主干（Qwen2.5-7B、GPT-4o、GPT-5、Claude-Sonnet-4.0）× Baseline/Full；
- **Shared Field Group 可扩展性分析**：单库（BLS_QCEW）+ 全基准（151 库）；
- **知识检索策略分析**：结构化三元组 vs. 原始轨迹向量化；
- **案例研究与错误分析**：100 个 Hard 失败样本人工分析。

### 充分性与公平性评估
- **充分**：覆盖主实验、多维度消融、成本、超参、跨基准、跨主干、可扩展性、检索策略，实验矩阵相当完整。
- **客观公平**：基线设置一致（k=3、最大精炼 5 次），消融控制了主干变量，静态语义视图用相同 GPT-4o 隔离执行反馈的贡献。
- **潜在偏差**：**所有结果仅来自单次评估运行**（作者以"SQL 执行在固定数据集上确定性"为由辩护，但 LLM 生成存在随机性，PASS@K 部分缓解了这一问题）；未报告方差或置信区间。

## 六、主要结论与发现

- **Spider 2.0-Snow 主结果**：SQLAgent 总体 EX **25.78%**，超过 ReFoRCE（20.84%）与 Spider-Agent（12.98%）；RL 方法（AlphaSQL 7.28%、MARS-SQL 5.30%）与 CHASE-SQL（1.28%）均被大幅超越。
- **Hard 子集优势最显著**：**12.21%**，而多数竞争方法近乎失效（基线 0%），说明知识库直接提供了使复杂多步 join 查询可解的已验证模式。
- **效率更优**：平均 5.2 次 LLM 调用、3.6 次 DB 调用，DB 交互次数少于 ReFoRCE（3.9）却精度更高。
- **消融结论**：Baseline 14.26% → +探索阶段 20.10% → 完整方法 25.78%，两阶段各有独立贡献。
- **成本摊销**：单次探索 467k token，仅 **8 次查询即回本**；之后每查询 16.4k token，比分块检索便宜 **4.6×**；100 次查询节省超 5.5M token 并同时提升 EX 14.48 个百分点。
- **动态探索显著优于静态语义视图**：8.22% → 25.78%（+17.56%），静态方法在 Hard 上完全为 0；说明许多约束（如 VARIANT 嵌套字段所需的 UNNEST）无法从 DDL 推断，只能通过运行时执行发现。
- **迭代稳定性**：有知识库时 EX 从 5.5% 单调升至第 4 轮峰值 25.8%；无知识库时在第 5 轮后急剧退化（14.1% 平台期后下降）。
- **跨主干稳健**：强模型上约 **+10% 绝对提升**；Qwen2.5-7B 上 EX@8 从 7.12% 翻倍到 14.99%。
- **BIRD 泛化**：**70.53% EX**，超过 ReFoRCE（57.0%）、MARS-SQL（66.8%）、AlphaSQL（69.7%）。
- **Shared Field Group 效果**：全基准节点数从

- **Shared Field Group 效果**：全基准（151 库）的图节点数由逐表建模的 76,219 压缩至 6,053（约 **12.6×** 缩减），单库（BLS_QCEW）亦从数万条边降至千级，使模式图在 150+ 库规模下仍可完整遍历并保持可解释性。
- **知识检索策略分析**：以**结构化三元组 (S, Q, U)** 作为检索单元，优于把原始探索轨迹整体向量化；说明显式、短小、语义对齐的"SQL–描述"配对比长文本轨迹更利于跨查询复用。
- **错误分析（100 个 Hard 失败样本）**：失败主要集中于需要**多跳嵌套聚合与复杂窗口语义**、**外部知识/业务口径**（如财年定义、单位换算）、以及**自然语言歧义无法由模式消解**的情形；纯粹的 join 路径错误已因知识库而大幅减少，印证了该框架"解决的是可发现的知识问题，而非全部推理问题"。

---

## 七、局限性与未来工作

- **对基础模型能力的天花板依赖**：探索阶段的有效性与部署阶段的合成质量均受主干 LLM 能力约束；在 Qwen2.5-7B 上虽翻倍提升（7.12%→14.99% EX@8），但绝对水平仍远低于 GPT-4o，说明方法**放大而非替代**模型能力。
- **探索成本的前置性**：单库探索约 467k token 属**一次性摊销投入**，在低查询量或一次性查询场景下不划算（需约 8 次查询才回本）；且探索产出会随模式变更（如新增分片表、字段改名）而**需要增量重建**，论文未给出增量维护方案。
- **知识库的可移植性边界**：三元组是**数据库专属**的，无法跨库迁移；每接入一个新库都要付出一次探索代价，规模上虽由 Shared Field Group 缓解了图结构爆炸，但 token 成本仍随库数线性增长。
- **评估统计严谨性**：所有主结果来自**单次运行**，未报告多次运行的方差或置信区间；尽管以 SQL 执行的确定性为由辩护、并以 PASS@K 部分补偿，但 LLM 生成与检索的随机性仍使复现存在波动风险。
- **失败类型未被方法覆盖**：涉及外部世界知识、业务口径约定与真实歧义的查询，仍需人工介入或额外知识源，框架本身未提供解决路径。
- **潜在方向**：探索阶段的增量/在线更新、跨库共性知识的迁移与共享、把语义保真检查从二值判定扩展为可解释的偏差定位，以及降低对昂贵商业模型的依赖。

---

## 八、整体评价与启示

- **定位准确**：论文抓住了 Text-to-SQL 在企业场景失效的**根因**——SQL 推理依赖"数据库专属知识"而非通用语言能力——并据此设计了两阶段解耦架构，问题—方法—实验三者高度自洽。
- **贡献层次清晰**：
  1. **概念层**：把"先熟悉库、再写查询"的工程师工作流显式工程化；
  2. **结构层**：Shared Field Group 用哈希签名把模式图从 O(N×M) 降到 O(N+M)，是工程可扩展性的关键；
  3. **算法层**：以 LLM-as-Policy-and-Evaluator 替代 UCT，匹配 SQL 有效性的二值性 + 语义质量的连续性；
  4. **系统层**：InfoAgent/GenAgent 分工 + 执行失败驱动的上下文剪枝与关键词重召回，形成闭环自精炼。
- **最有力的证据**：**动态探索 8.22% vs 静态语义视图 25.78%（+17.56%）** 且静态方法在 Hard 上为 0——这直接证明了许多约束（如 VARIANT 嵌套字段的 UNNEST）**无法从 DDL 推断，只能靠运行时执行发现**，为"必须探索"提供了强反证。
- **成本论证有说服力**：把探索视为可摊销的资本支出（8 次查询回本、之后每查询 16.4k token、比分块检索便宜 4.6×），使其在真实生产（同一库被反复查询）中具备可行性，而不仅是 benchmark 刷分。
- **可复现性**：主干模型、温度、嵌入模型、图数据库与 Agent 框架均有明确披露，实验矩阵完整（主实验 / 分步与组件消融 / 成本 / 超参 / 跨基准 / 跨主干 / 可扩展性 / 检索策略 / 错误分析），在同类工作中属较高水平。
- **保留意见**：单次运行、缺少方差报告，以及探索成本随库数线性增长的规模性问题，是接受该结论时最需留意的两点；此外 Hard 子集 12.21% 的绝对精度说明**真实企业级 Text-to-SQL 仍远未解决**，本文的价值更在于指出了正确的攻坚方向而非给出终局方案。

---

## 九、一句话总结

SQLAgent 通过"**先自主探索构建数据库专属知识库、再以双 Agent 检索式合成 SQL**"的两阶段设计，把企业级 Text-to-SQL 从零样本猜测转变为基于已验证经验的知识驱动推理，在 Spider 2.0-Snow（25.78% EX，Hard 12.21%）与 BIRD（70.53% EX）上取得领先，并以 8 次查询回本的摊销成本证明了其工程可行性。

（完）

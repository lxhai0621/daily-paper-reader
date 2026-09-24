---
title: "MAGMA: A Multi-Graph based Agentic Memory Architecture for AI Agents"
title_zh: "MAGMA:面向AI智能体的多图智能体记忆架构"
authors: "Dongming Jiang, Yi Li, Guanpeng Li, Bingzhe Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1709.pdf"
tags: ["query:agent"]
score: 9.0
evidence: "多图智能体记忆架构,采用策略引导的检索遍历"
tldr: "记忆增强生成借助外部记忆支持长上下文推理,但现有方法多依赖单一记忆库上的语义相似度,混淆时间、因果与实体信息,限制可解释性与检索对齐。本文提出MAGMA多图智能体记忆架构,将每条记忆在语义、时间、因果与实体四个正交图上表示,并把检索建模为关系视图上的策略引导遍历,实现查询自适应的结构化上下文构建,提升智能体长期记忆的检索与推理精度。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1709/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 1536, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1709/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 413, \"height\": 352}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1709/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1709/fig-004.webp\", \"caption\": \"\", \"page\": 5, \"index\": 4, \"width\": 512, \"height\": 512}]"
motivation: "现有记忆增强生成依赖单一记忆库的语义相似度,混淆时间因果实体信息,限制可解释性与检索对齐。"
method: "提出多图记忆架构MAGMA,在语义、时间、因果、实体四类图上表示记忆,并将检索建模为策略引导遍历。"
result: "该架构实现查询自适应的记忆选择与结构化上下文构建,提升长期记忆推理准确性。"
conclusion: 多图解耦的记忆表示为智能体长期记忆存储与检索提供更具可解释性的方案。
---

## Abstract
Memory-Augmented Generation (MAG) extends large language models with external memory to support long-context reasoning, but existing approaches largely rely on semantic similarity over monolithic memory stores, entangling temporal, causal, and entity information. This design limits interpretability and alignment between query intent and retrieved evidence, leading to suboptimal reasoning accuracy. In this paper, we propose MAGMA, a multi-graph agentic memory architecture that represents each memory item across orthogonal semantic, temporal, causal, and entity graphs. MAGMA formulates retrieval as policy-guided traversal over these relational views, enabling query-adaptive selection and structured context construction. By decoupling memory representation from retrieval logic, MAGMA provides transparent reasoning paths and fine-grained control over retrieval. Experiments on LoCoMo and LongMemEval demonstrate that MAGMA consistently outperforms state-of-the-art agentic memory systems in long-horizon reasoning task.

---

## 论文详细总结（自动生成）

# MAGMA 论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：大语言模型（LLM）受限于固定注意力窗口，无法稳定持久地维护和推理长期上下文；即使在同一长序列中，也存在“lost-in-the-middle”和上下文衰减问题。
- **现有方案**：记忆增强生成（Memory-Augmented Generation, MAG）通过外部记忆模块记录交互历史，使智能体能够跨会话积累知识、保持一致性。
- **核心问题**：现有 MAG 系统大多依赖单一、扁平化记忆库上的语义相似度检索，将时间、因果、实体等信息纠缠在一起，导致：
  - 可解释性差；
  - 查询意图与检索证据之间对齐不足；
  - 能检索“发生了什么”，但难以推理“为什么发生”；
  - 在长程推理任务中准确率受限。
- **整体含义**：论文提出 MAGMA，将记忆显式表示为语义、时间、因果、实体四个正交关系图，并把检索建模为策略引导的图遍历，从而解耦记忆表示与检索逻辑，提升长期推理能力、可解释性和检索可控性。

## 2. 方法论

### 2.1 核心思想

- 将每条记忆项表示为多图结构中的节点，并在四类正交关系图上建立边：
  - **语义图**：基于嵌入余弦相似度连接概念相似事件；
  - **时间图**：按时间戳形成严格有序的不可变链；
  - **因果图**：由异步整合模块推断的逻辑蕴含边，支持“Why”查询；
  - **实体图**：连接事件与抽象实体节点，解决跨时间线的对象永久性问题。
- 检索不再是静态向量查找，而是**策略引导的图遍历**：根据查询意图选择相关关系视图，独立遍历并融合子图，构建类型对齐的紧凑上下文。

### 2.2 系统架构

- **查询过程（Query Process）**：
  - 意图感知路由器；
  - 自适应拓扑检索；
  - 上下文合成器。
- **数据结构层（Data Structure Layer）**：
  - 向量数据库 + 四个关系图；
  - 统一节点表示为事件内容、时间戳、稠密向量和结构化属性。
- **写入/更新过程（Write/Update Process）**：
  - **快路径（Synaptic Ingestion）**：处理延迟敏感操作，如事件分割、向量索引、更新时间骨干；
  - **慢路径（Asynchronous Consolidation）**：异步调用 LLM 推断因果和实体连接，稠密化图结构。

### 2.3 查询流程关键步骤

1. **查询分析与分解**：
   - 意图分类：`WHY`、`WHEN`、`ENTITY`；
   - 时间解析：将“上周五”等相对表达解析为绝对时间窗口；
   - 表示提取：稠密嵌入 + 稀疏关键词。
2. **多信号锚点识别**：
   - 使用 Reciprocal Rank Fusion（RRF）融合向量检索、关键词匹配和时间过滤，选出锚点节点。
3. **自适应遍历策略**：
   - 从锚点出发，使用启发式束搜索；
   - 动态转移分数融合结构对齐与语义相关性：
     - `S(nj | ni, q) = exp(λ1 · φ(type(eij), Tq) + λ2 · sim(nj, q))`
   - 其中 `φ` 根据查询意图对边类型加权，例如“Why”查询提高因果边权重。
4. **图线性化与叙事合成**：
   - 拓扑排序：时间查询按时间戳排序，因果查询按因果边拓扑排序；
   - 上下文脚手架：每个节点序列化为包含时间戳、内容和引用 ID 的结构块；
   - 基于显著性的 token 预算：高相关节点保留完整细节，低相关节点压缩为摘要。

### 2.4 记忆演化

- **快路径**：非阻塞地完成事件分割、向量索引和时间边添加，保证智能体响应性。
- **慢路径**：后台异步分析局部邻域，调用 LLM 推断潜在因果与实体关系，新增高价值边。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- **LoCoMo**：
  - 超长对话基准，平均长度约 9K tokens；
  - 评估长程时间与因果检索；
  - 包含 1,986 个样本，覆盖 Single-Hop、Adversarial、Temporal、Multi-Hop、Open-Domain 五类查询。
- **LongMemEval**：
  - 大规模压力测试基准，平均上下文超过 100K tokens；
  - 评估超长交互历史下的可扩展性和记忆保持稳定性。

### 3.2 对比方法

- **Full Context**：将完整对话历史直接输入 LLM；
- **A-MEM**：自演化、类 Zettelkasten 的记忆系统；
- **Nemori**：基于图的记忆，采用“预测-校准”机制进行情节分割；
- **MemoryOS**：语义聚焦的分层记忆操作系统。

### 3.3 评估指标

- 主要指标：LLM-as-a-Judge 语义评分；
- 辅助指标：token-level F1、BLEU-1；
- 所有系统统一使用 `gpt-4o-mini` 作为骨干模型，统一评估框架。

## 4. 资源与算力

- 论文**未明确说明**所使用的 GPU 型号、数量、训练时长或总计算资源。
- 文中仅提及：
  - 推理骨干模型为 `gpt-4o-mini`；
  - 嵌入模型默认使用 `all-MiniLM-L6-v2`，可选 `text-embedding-3-small`；
  - 系统效率对比中报告了内存构建时间、每查询 token 消耗和查询延迟，但未披露硬件配置。
- 因此，无法从论文中判断其训练或推理的完整算力开销。

## 5. 实验数量与充分性

- **主要实验**：
  - LoCoMo 整体性能对比；
  - LongMemEval 泛化与超长上下文评估；
  - 系统效率分析：构建时间、每查询 token 数、查询延迟；
  - 消融实验：
    - 移除自适应策略；
    - 移除因果链接；
    - 移除时间骨干；
    - 移除实体链接；
    - 单图消融：仅因果、仅时间、仅实体；
  - 案例研究：事实检索、逻辑推断、时间解析；
  - 指标验证分析：7 个受控案例比较 F1/BLEU 与 LLM-Judge。
- **充分性评价**：
  - 实验覆盖了多个数据集、多个基线、多类查询和多种消融，整体较充分；
  - 统一使用相同骨干模型和评估框架，公平性较好；
  - 但所有实验主要基于 `gpt-4o-mini`，未验证其他规模或类型 LLM 的泛化性；
  - 基准集中在对话式长上下文任务，尚未覆盖多模态或异构观测流场景。

## 6. 主要结论与发现

- MAGMA 在 LoCoMo 上取得最高 LLM-as-a-Judge 总分 **0.700**，显著优于 Full Context（0.481）、A-MEM（0.580）、MemoryOS（0.553）和 Nemori（0.590）。
- 在 LongMemEval 上平均准确率 **61.2%**，优于 Full-context（55.0%）和 Nemori（56.2%）。
- 效率方面：
  - MAGMA 查询延迟最低，为 **1.47 秒**，比次优检索基线快约 40%；
  - 每查询 token 消耗约 **3.37K**，远低于 Full Context 的 8.53K；
  - 在 LongMemEval 上，MAGMA 仅使用 0.7K–4.2K tokens/query，即可达到接近 Full-context 的准确率，token 减少超过 95%。
- 消融表明：
  - 自适应遍历策略贡献最大；
  - 因果链接和时间骨干互补且不可替代；
  - 实体链接有助于实体永久性和减少幻觉；
  - 单一关系图均无法恢复完整性能，多图组合最优。

## 7. 优点

- **表示解耦**：将语义、时间、因果、实体关系显式分离，避免单一语义相似度带来的信息混淆。
- **检索可控且可解释**：策略引导遍历提供透明推理路径，便于分析检索依据。
- **查询自适应**：意图感知路由和动态边权使检索更贴合问题类型。
- **双流记忆演化**：快慢路径分离，兼顾响应速度与结构深化。
- **效率优势**：在保持或提升准确率的同时，显著降低延迟和 token 消耗。
- **实验较系统**：包含主实验、泛化实验、效率分析、消融、案例研究和指标验证。
- **开源代码**：提供开源实现，便于复现和后续研究。

## 8. 不足与局限

- **依赖 LLM 推理质量**：因果和实体边由异步 LLM 推断，可能引入提取错误或幻觉，并传播到下游检索。
- **存储与工程复杂度**：多图结构和双流处理比扁平向量库更复杂，带来额外存储和实现开销，可能不适合资源极度受限环境。
- **评估覆盖有限**：主要在 LoCoMo 和 LongMemEval 上评估，尚未覆盖多模态智能体、异构观测流等更广泛场景。
- **骨干模型单一**：实验主要基于 `gpt-4o-mini`，未充分验证不同 LLM 下的泛化性。
- **算力信息缺失**：未报告 GPU 型号、数量、训练时长等，难以评估实际部署成本。
- **潜在偏差风险**：LLM-as-a-Judge 虽优于词法指标，但仍可能受 judge 模型偏好影响；基线系统使用默认超参数，虽公平但未必最优。

（完）

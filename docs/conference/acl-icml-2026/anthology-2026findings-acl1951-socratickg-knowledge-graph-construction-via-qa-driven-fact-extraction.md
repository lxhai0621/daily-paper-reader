---
title: "SocraticKG: Knowledge Graph Construction via QA-Driven Fact Extraction"
title_zh: SocraticKG：基于问答驱动事实抽取的知识图谱构建
authors: "Sanghyeok Choi, Woosang Jeon, Kyuseok Yang, Taehyeong Kim"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1951.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 通过问答驱动的事实抽取从非结构化文本自动构建知识图谱
tldr: 从非结构化文本构建知识图谱时，基于大模型的方法常面临事实覆盖与关系碎片化之间的两难，过早合并又会丢失信息。为此提出 SocraticKG，以问答对作为结构化中间表示，先系统展开文档级语义，再进行三元组抽取。方法采用 5W1H 引导的问答扩展，捕捉直接抽取流程中易丢失的上下文依赖与隐式关系链接，并在源文本中提供显式依据。该框架为自动化知识发现与结构化知识库构建提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1951/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 4290, \"height\": 1433}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1951/fig-002.webp\", \"caption\": \"\", \"page\": 5, \"index\": 2, \"width\": 7484, \"height\": 4497}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1951/fig-003.webp\", \"caption\": \"\", \"page\": 9, \"index\": 3, \"width\": 2371, \"height\": 694}]"
motivation: 现有基于大模型的知识图谱构建难以兼顾事实覆盖与关系连贯，直接抽取易丢失隐式关系。
method: 提出 SocraticKG，用 5W1H 引导的问答对作为中间表示，先展开文档语义再抽取三元组。
result: 通过问答扩展捕捉上下文依赖与隐式关系链接，并在源文本中提供显式依据。
conclusion: 为从非结构化文本自动构建结构化知识图谱提供了可解释的新范式。
---

## Abstract
Constructing Knowledge Graphs (KGs) from unstructured text provides a structured framework for knowledge representation and reasoning, yet current LLM-based approaches struggle with a fundamental trade-off: factual coverage often leads to relational fragmentation, while premature consolidation causes information loss. To address this, we propose SocraticKG, an automated KG construction method that introduces question-answer pairs as a structured intermediate representation to systematically unfold document-level semantics prior to triple extraction. By employing 5W1H-guided QA expansion, SocraticKG captures contextual dependencies and implicit relational links typically lost in direct KG extraction pipelines, providing explicit grounding in the source document that helps mitigate implicit reasoning errors. Evaluation on the MINE benchmark demonstrates that our approach effectively addresses the coverage-connectivity trade-off, achieving superior factual retention while maintaining high structural cohesion even as extracted knowledge volume substantially expands. These results highlight that QA-mediated semantic scaffolding plays a critical role in structuring semantics prior to KG extraction, enabling more coherent and reliable graph construction in subsequent stages.

---

## 论文详细总结（自动生成）

# SocraticKG 论文详细总结

## 1. 核心问题与整体含义

- **研究背景**：大语言模型（LLM）在知识密集型应用中广泛使用，但事实可靠性、可解释性与可溯源性受到关注。检索增强生成（RAG）虽能锚定外部来源，却常面临上下文碎片化与复杂事实整合浅层化的问题。知识图谱（KG）因此重新受到重视，作为结构化、可验证的知识表示与推理骨干。
- **核心问题**：基于 LLM 的自动 KG 构建面临一个根本性两难——
  - **事实覆盖优先** → 关系碎片化（图中有大量事实但语义连通性弱）；
  - **过早合并优先** → 信息丢失（图结构良好但遗漏不符合预定义结构的上下文细节）。
- **现有方法局限**：
  - **直接三元组抽取**：仅捕捉表层显式提及，忽略潜在逻辑联系，产出碎片化子图；
  - **合并中心策略**（如 GraphRAG、KGGen、CLARE）：实体集早期固定，形成表示瓶颈，排除不符合初始实体结构的关系与上下文依赖；
  - **先转换后抽取**（如 CoDe-KG）：主要在句子级做局部句法规范化，无法系统捕捉跨句依赖与文档级全局语义；
  - **QA 用于知识抽取**（如 StoryNet、ChatIE）：将 QA 对视为瞬时产物，单次生成即消费，未将其形式化为中间表示。
- **整体含义**：论文受人类“提问式理解”启发，提出将 QA 对作为结构化中间表示，在三元组抽取之前系统展开文档级语义，以同时兼顾事实覆盖与结构连贯。

## 2. 方法论

- **核心思想**：SocraticKG（SoKG）不直接从原始文本抽取三元组，而是先将文档分解为显式、自包含的 QA 对，再映射为原子三元组，最后经规范化统一为知识图谱。
- **三阶段流程**：

  **阶段一：5W1H 引导的 QA 生成**
  - 利用 5W1H 框架（Who、What、When、Where、Why、How）引导系统性提问，覆盖表层实体及因果（why）、程序性（how）依赖；
  - 强制**上下文独立性**：要求回答中替换代词为显式实体名，使每个 QA 对可独立理解，避免后续逐对处理时的信息丢失。

  **阶段二：从 QA 抽取三元组**
  - 以每个 QA 对为独立抽取单元，三条约束：
    - **原子分解**：将每个 QA 对拆为最小事实三元组，兼顾问题与回答中的信息；
    - **实体清晰性**：实体为具体名词短语，含歧义代词的 triple 被丢弃；
    - **关系简化**：谓词精简为简短动词短语，关系模糊则跳过。

  **阶段三：从三元组构建图**
  - 采用 Mo et al. (2025) 的规范化流程，对实体与关系分别执行“聚类-精炼”：
    - 用文本嵌入模型（all-MiniLM-L6-v2）生成语义嵌入；
    - 经 K-means 聚类（每簇最多 128 个元素）缩小搜索空间；
    - 在簇内以稠密语义相似度 + BM25 稀疏词法重叠选出 top-k（k=16）候选；
    - 由 LLM 将同义词、缩写映射到单一代表形式，合并碎片化三元组。

## 3. 实验设计

- **数据集 / 场景**：
  - **MINE benchmark**（Mo et al., 2025）：100 篇多样文章，每篇 15 条已验证原子事实，共 1,500 个独立事实实例；用于衡量源信息保留（事实可恢复性）与图结构特征。
  - **HotpotQA**（Yang et al., 2018）：800 个“Hard” Bridge 样本，需识别连接分散证据的中间实体，适合评估图基多跳推理。
- **评估指标**：
  - 事实保留分数（LLM-judge 对 top-8 相似节点及 2 跳邻居子图进行验证）；
  - 平均度（Deg）、三元组数（#Tri）、归一化碎片化指数（NFI = (C-1)/(N-1)）；
  - HotpotQA 多跳推理准确率（2-hop、3-hop）。
- **对比方法**：
  - **Direct Extraction**（单遍直接抽取 + 相同规范化）；
  - **GraphRAG**（微软官方实现，分层社区检测与聚合）；
  - **KGGen**（实体中心抽取与结构合并的 SOTA）；
  - **SoKG (w/o 5W1H)**（消融变体，保留 QA 中间表示但替换为通用 QA）；
  - **SoKG (Ours)**（完整方法）。
  - HotpotQA 另加 **Naive RAG** 基线（嵌入相似度检索扁平文本块，块大小与图检索上下文匹配）。
- **评估的 LLM**：GPT-4o、GPT-4o-mini、Gemini-2.5-Flash-Lite、Qwen2.5-7B-Instruct、Claude-4-Sonnet。
- **实现细节**：解码温度设为 0（GraphRAG 除外，沿用官方随机配置）；事实验证用 GPT-4o 作 LLM-judge；下游 QA 回答模型为 GPT-4.1。

## 4. 资源与算力

- **论文未明确说明使用的 GPU 型号、数量或训练时长**。
- 该工作为基于提示（prompting）的推理框架，**不涉及模型训练**，故未报告训练算力。
- 附录 D 提供了**计算成本分析**（表 7）：统计了各方法在 triple extraction 阶段前的总 token 消耗。
  - SoKG 在 Qwen-2.5 上消耗约 333,917 tokens、Claude-4 上约 553,530 tokens，约为 Direct Extraction 的 2–3 倍；
  - 但 SoKG 产出的规范化三元组数分别为 3,958 与 14,849，是 Direct Extraction 的约 2.0 倍与 3.4 倍；
  - GraphRAG 与 KGGen 在某些 backbone 上 token 消耗与 SoKG 相当甚至更高，但产出三元组显著更少。

## 5. 实验数量与充分性

- **主要实验组数概览**：
  1. **MINE 事实保留**（表 1）：5 个 LLM × 5 种方法 = 25 组配置；
  2. **拓扑特征**（表 2）：节点数、边数、平均度，同上 25 组；
  3. **碎片化与信息量**（表 3）：NFI 与 #Tri，同上 25 组；
  4. **HotpotQA 下游多跳推理**（表 4）：2 个 backbone（Qwen-2.5、Claude-4）× 2 个检索深度（2-hop、3-hop）× 5 种方法 + Naive RAG；
  5. **提示原型消融**（表 5，附录 A.1）：3 种提示模板（RO / PS / ID）× 5 个 LLM × 有无 5W1H = 30 组；
  6. **实体优先约束消融**（表 6，附录 A.2）：KGGen / SoKG-EF / SoKG 在 5 个 LLM 上对比；
  7. **三元组质量分析**（表 8，附录 E）：US、GS 及人工评估 FP（5 位标注者、3 篇随机文档）；
  8. **计算成本分析**（表 7，附录 D）；
  9. **失败案例分析**（附录 F）。
- **充分性与公平性评价**：
  - **充分**：覆盖两个数据集、五个不同架构与规模的 LLM、多组消融、下游任务、质量与成本分析，实验维度较完整；
  - **客观公平**：对比方法均为无需预定义 schema、无人工干预的自主开放域方法，且对 Direct Extraction 应用了相同规范化流程，Naive RAG 的块大小与图检索上下文匹配，控制变量较严谨；
  - **可复现**：温度设为 0，代码已公开（https://github.com/LABA-SNU/SocraticKG）；
  - 潜在局限：事实验证依赖 LLM-judge（GPT-4o），可能引入评判偏差；FP 人工评估仅抽样 3 篇文档，样本量有限。

## 6. 主要结论与发现

- **事实保留最优**：SoKG 在所有对比方法与 LLM 上均取得最高事实保留分数，Claude-4 上峰值达 **96.3%**；即使 w/o 5W1H 变体也全面优于 Direct Extraction，证明 QA 中间表示本身有效。
- **图规模与连通性同步提升**：SoKG 显著扩大图规模（节点、边、三元组数）同时保持或提高平均度，说明结构优势源自 QA 介导的中间表示，而非简单冗余扩张。
- **碎片化降低**：SoKG 在抽取更多三元组的同时保持更低 NFI，有效化解“覆盖-连通”两难；5W1H 引导不仅增加事实，还增强其整合入图结构。
- **下游多跳推理增益**：HotpotQA 上 SoKG 在所有 backbone 与检索深度均优于 Naive RAG 及其他图方法；Claude-4 在 3-hop 下达 56.38%，超出 Naive RAG 8.5 个百分点、超出 Direct Extraction 16.5 个百分点。
- **图结构检索并非天然有利**：只有当图足够连通、事实足够完整时（如 SoKG），图检索才优于 Naive RAG；KGGen、Direct Extraction 在部分设定下反而低于 Naive RAG。
- **三元组质量未因规模扩大而下降**：SoKG 的 Uniqueness Score（91.75%）最高，Granularity Score（82.59%）显著高于 Direct Extraction 与 GraphRAG，人工评估 Factual Precision 达 84.21%，与 Direct Extraction 相当。

## 7. 优点

- **方法创新性强**：首次将 QA 对形式化为 KG 构建的结构化中间表示，而非瞬时抽取产物，从认知层面模拟人类提问式理解；
- **5W1H 框架系统化**：提供可复用的提问脚手架，能主动外化隐式因果与程序性依赖；
- **上下文独立性约束**：强制代词消解，使每个 QA 对自包含，有效防止逐对处理时的信息丢失；
- **实验设计严谨**：
  - 跨 5 个 LLM 验证鲁棒性；
  - 对基线应用相同规范化流程，控制变量；
  - Naive RAG 块大小与图检索上下文匹配；
  - 同时报告覆盖度（事实保留）与结构质量（NFI、平均度），避免单一指标误导；
- **消融充分**：分别隔离 QA 脚手架（w/o 5W1H）与抽取策略（SoKG-EF）的贡献，并验证 5W1H 跨 3 种提示模板的普适增益；
- **质量验证全面**：引入 GenRES 框架的 US/GS 指标与人工 Factual Precision，证明扩张非冗余或幻觉；
- **透明度高**：提供成本分析、失败案例分析与伦理考量，附录详尽（提示词全文公开）。

## 8. 不足与局限

- **计算开销大**：多阶段 QA 流水线 token 消耗约为 Direct Extraction 的 2–3 倍，成本-知识比虽更优但绝对开销显著；
- **性能依赖底层 LLM 推理深度**：在需要高度专业化提问逻辑的领域，图质量可能下降；
- **主要瓶颈在 QA 中介阶段**：失败案例集中于“一维 What 查询”缺乏特异性，表现为：
  - **特异性不足**：问题指向宽泛话题，回答仅罗列实体而未阐明功能角色；
  - **精巧的非回答**：回答复述文档框架而非基于具体证据；
  - **上下文丢失**：回答事实正确但遗漏产生有区分度三元组的关键细节；
- **二元三元组表示局限**：可能简化多维限定符（如时间、空间数据），n 元关系或更紧凑；
- **评估覆盖有限**：
  - 仅聚焦事实可恢复性与多跳推理，未涵盖 schema 对齐、关系类型保真度等维度；
  - 人工 FP 评估仅抽样 3 篇文档、5 位标注者，统计效力有限；
  - 事实验证依赖 LLM-judge，可能带入评判模型自身偏差；
- **未报告算力细节**：无 GPU 型号、数量或时长信息，虽因无需训练可理解，但对完整复现与成本估算有所欠缺；
- **伦理风险**：自动抽取存在幻觉事实风险，基准与底层 LLM 可能带固有偏差，敏感或高风险领域需人工验证。

（完）

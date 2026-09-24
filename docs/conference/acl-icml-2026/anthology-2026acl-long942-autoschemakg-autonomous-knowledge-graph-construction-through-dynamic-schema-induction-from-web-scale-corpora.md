---
title: "AutoSchemaKG: Autonomous Knowledge Graph Construction through Dynamic Schema Induction from Web-Scale Corpora"
title_zh: AutoSchemaKG：通过动态模式归纳从网页级语料实现自主知识图谱构建
authors: "Jiaxin Bai, Wei Fan, Qi Hu, Qing Zong, Chunyang Li, Hong Ting Tsang, Hongyu Luo, Yauwai Yim, Haoyu Huang, Xiao Zhou, Feng Qin, Tianshi Zheng, Xi Peng, Xin Yao, Huiwen Yang, Leijie Wu, JI Yi, Gong Zhang, Renhai Chen, Yangqiu Song"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.942.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 从网页级语料自动构建知识图谱并归纳模式
tldr: 现有知识图谱构建依赖预定义模式，难以适配开放网页语料。本文提出 AutoSchemaKG 框架，利用大语言模型同时抽取知识三元组并自动归纳模式，将实体与事件概念化组织为语义类别。系统处理逾五千万文档，构建含九亿节点、五十九亿边的 ATLAS 图谱，在多跳问答上超越基线并提升事实性。该工作为自动化知识发现提供了可扩展的无模式方案。
source: ACL-2026-Long
selection_source: conference_retrieval
motivation: 传统知识图谱构建依赖人工预定义模式，难以应对开放、动态的大规模网页语料，自动化知识发现需求迫切。
method: 提出 AutoSchemaKG 框架，用大语言模型同时抽取知识三元组并归纳模式，对实体与事件进行概念化分类。
result: 处理五千万文档构建 ATLAS 图谱，含九亿节点与五十九亿边，多跳问答超越基线并提升事实性。
conclusion: 该框架证明无需预定义模式即可自主构建大规模知识图谱，为自动化知识发现提供可扩展范式。
---

## Abstract
We present AutoSchemaKG, a framework for fully autonomous knowledge graph construction that eliminates the need for predefined schemas. Our system leverages large language models to simultaneously extract knowledge triples and induce comprehensive schemas directly from text, modeling both entities and events while employing conceptualization to organize instances into semantic categories. Processing over 50 million documents, we construct ATLAS (Automated Triple Linking And Schema induction), a family of knowledge graphs with 900+ million nodes and 5.9 billion edges. This approach outperforms state-of-the-art baselines on multi-hop QA tasks and enhances LLM factuality. Notably, our schema induction achieves 92% semantic alignment with human-crafted schemas with zero manual intervention, demonstrating that billion-scale knowledge graphs with dynamically induced schemas can effectively complement parametric knowledge in large language models.

---

## 论文详细总结（自动生成）

# AutoSchemaKG 论文总结

## 一、核心问题与研究动机

- **核心矛盾（KG 构建的悖论）**：知识图谱是搜索、问答、推荐与复杂推理的语义骨架，但现有构建流程依赖**领域专家预定义的模式（schema）**，从根本上限制了可扩展性与领域覆盖范围。
- **研究目标**：实现**完全自主、无需预定义模式**的知识图谱构建，消除人工瓶颈，使 KG 能直接从网页级非结构化语料中自动生长。
- **关键洞察**：
  - 传统方法（OpenIE 类）只抽取实体-实体三元组，忽略事件与概念层，导致三元组不完整、歧义、子图连通性差。
  - 本文将**事件视为一等语义单元**，捕获时序、因果与过程性知识；实验显示事件信息可保留原文 90% 以上的内容，而纯实体信息仅约 70%。
  - 引入**概念化（conceptualization）**，把具体实体/事件/关系泛化为抽象类别，形成跨域语义桥梁与层次化组织，支撑零样本跨域推理。
- **规模诉求**：作者认为 KG 必须达到**十亿级事实**才能真正补充当代 LLM 的参数化知识，因此选择在 Dolma 1.7 预训练语料上做网页级处理。

## 二、方法论

### 2.1 总体框架（四阶段流水线）

1. **输入处理**：过滤英文文档；按 `Cmax = Lmax − Linst` 切分超长文档并打上唯一标识与元数据；再按批大小 B 分组。
2. **三元组抽取**：用 LLM 分三阶段抽取实体-实体、实体-事件、事件-事件关系。
3. **模式归纳**：对节点与关系做概念化，生成抽象短语，构成概念集合 C。
4. **图谱构建**：建立实体节点、事件节点、概念节点与关系边，完成概念链接，得到最终图 G。

### 2.2 形式化定义

- 带概念模式的知识图定义为 **G = (V, E, C, ϕ, ψ)**：
  - `V = VE ∪ VN`，`VE` 为事件节点集，`VN` 为实体节点集，且 `VE ∩ VN = ∅`；
  - `E ⊆ V × V × R`，边可连接实体-实体、实体-事件、事件-事件；
  - `C` 为概念类别集合；
  - `ϕ: V → P(C)` 为每个节点分配概念子集；`ψ: R → P(C)` 为每种关系分配概念子集；
  - 约束：`∀v ∈ V, ϕ(v) ≠ ∅`；`∀r ∈ R, ψ(r) ≠ ∅`。

### 2.3 三阶段三元组抽取

- **Stage 1（实体-实体）**：使用系统提示 `P_EE`，要求 LLM 识别重要实体及其相互关系，实体尽量具体、排除代词；输出 JSON 三元组 `(e1, r, e2)`。
- **Stage 2（实体-事件）**：使用提示 `P_EV`，要求事件为单句、不得使用省略号，输出 `(e, r, v)` 或 `(v, r, e)` 形式，双向捕获实体与事件的参与关系。
- **Stage 3（事件-事件）**：使用提示 `P_VV`，只允许 before / after / at the same time / because / as a result 五类时序或因果关系，输出 `(v1, r, v2)`；生成上限扩展为 `Lext = α · Lmax`（α > 1）。
- **工程细节**：定位答案起始 token、修复畸形 JSON、解析失败则返回空列表保证流水线不中断；三元组连同原文与元数据序列化为 JSON；支持多种 LLM（DeepSeek / LLaMA / Qwen 等）、bfloat16/float16 精度、GPU 加速与模型专属 chat template。

### 2.4 模式归纳（概念化）

- 对**事件、实体、关系**三类元素分批（批大小 `Bs`）处理，LLM 为每个元素生成**至少 3 个 1–2 词短语**，要求：能代表该元素类型或相关概念、抽象层次不同、不重复、不含原输入、严格输出格式。
- **实体概念化的上下文增强**：采样至多 `Nctx` 个邻居节点（前驱/后继）及其关系，拼接为上下文字符串（如 "neighbor1 relation1, relation2 neighbor2"），使抽象类型扎根于图中角色。例如 "Black Mountain College" + 上下文 "started by John Andrew Rice" → college, school, liberal arts college。
- **事件与关系**仅依赖自身文本描述，不引入图上下文。
- 结果写入 CSV，形成 `ϕ(v)`、`ϕ(e)`、`ψ(r)` 映射；支持切片分布式计算（`Stotal` 个切片中的第 `Sslice` 片）与随机子采样加速实验。

### 2.5 图谱构建

- 创建实体节点（VN）、事件节点（VE）、概念节点（C）；
- 依据抽取关系 R 建立边，并将节点/关系链接到对应概念节点；
- 完成图 `G = (V, E, C, ϕ, ψ)`。

## 三、实验设计

### 3.1 数据与构建规模

| 语料 | 来源 | 文本块 | 节点 | 边 |
|---|---|---|---|---|
| ATLAS-Wiki | Dolma 全量 Wikipedia & Wikibooks | 9.599M | 243.9M | 1.492B |
| ATLAS-Pes2o | Semantic Scholar 摘要 | 7.918M | 174.4M | 1.150B |
| ATLAS-CC | cc-head/middle/tail 各 3% | 35.040M | 937.3M | 5.958B |

- 合计处理 **5000 万+ 文档**，构建 900M+ 节点、5.9B 边的 ATLAS 家族图谱。

### 3.2 五类评测任务与对比方法

1. **三元组抽取准确性**：以 DeepSeek-V3 为裁判（给出原文与 LLaMA-3.1-8B 抽取结果，判定假阳性/假阴性）；对比 **OpenIE6**、**Stanford OIE**；另做跨 LLM 模块对比（DeepSeek-V3、LLaMA-3.2-1B/3B、LLaMA-3.1-8B、LLaMA-3.3-70B、Qwen-2.5-7B/72B）。
2. **信息保留度（MCQ）**：每篇 passage 由 LLaMA-3.3-70B 生成 5 道多选题，每数据集采样 200 篇 passage、1000 道 MCQ；设置下界（无上下文）、上界（完整原文）、Entity、Event、Event+Entity 五种条件；对比 OpenIE6、Stanford OIE。
3. **模式质量**：实体类型（FB15kET、YAGO43kET）、事件类型（wikiHow）、关系类型（FB15kET 关系域段）；对比 **Txt2onto**；指标为语义级 **BS-R**（Recall）与 **BS-C**（Coverage），基于 RoBERTa 嵌入的 BERTScore。
4. **多跳问答**：MuSiQue、HotpotQA、2WikiMultihopQA，各随机取 1000 题；指标 EM 与 F1；对比：
   - 无检索 / Contriever / BM25；
   - LLM 嵌入检索（GTE-Qwen2-7B、GritLM-7B、NV-Embed-v2）；
   - 图 RAG：RAPTOR、GraphRAG、LightRAG、MiniRAG、HippoRAG、HippoRAG2；
   - 传统 OpenIE + HippoRAG / HippoRAG2；
   - AutoSchemaKG 分别接入 Think-on-Graph（ToG）、HippoRAG、HippoRAG2。
5. **LLM 事实性与通用知识**：
   - **FELM**（847 样本、4,425 细粒度片段、5 领域），指标为 Balanced Accuracy 与 F1，对比 Random / BM25 / Dense Retrieval（MiniLM）/ Freebase-ToG / HippoRAG2；
   - **MMLU**：按学科分组（History、Law、Religion、Philosophy/Ethics、Medicine/Health、Global Facts、Social Sciences、Logic 等），

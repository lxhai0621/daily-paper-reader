---
title: "AWARE: Agentic Knowledge Warehousing for Contextual Intelligence"
title_zh: AWARE：面向情境智能的智能体式知识仓库
authors: "Hongjin Qian, Siqi Bao, Zhao Cao, Zheng Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.120.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向情境智能的智能体式知识仓库
tldr: 信息检索旨在弥合查询与答案间的知识鸿沟，但大模型受预训练限制，在专业或时效性查询上表现下降；现有做法要么将证据注入上下文，受限于分层依赖探索，要么交错检索与推理，受上下文长度约束，面对复杂依赖与大文本量时均显不足。本文提出AWARE（智能体知识仓库）框架，将异构知识转化为可复用的仓库，突破上下文与效率瓶颈。该工作为大规模复杂知识发现提供了新路径。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl120/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl120/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl120/fig-003.webp\", \"caption\": \"\", \"page\": 2, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl120/fig-004.webp\", \"caption\": \"\", \"page\": 2, \"index\": 4, \"width\": 512, \"height\": 512}]"
motivation: 大模型在专业与时新查询上表现受限，证据注入与交错检索两种方案在复杂依赖和大文本量下均不足。
method: 提出AWARE智能体式知识仓库框架，将异构知识转化为可复用仓库，支持智能体式信息检索。
result: 框架缓解了上下文长度与效率瓶颈，支持复杂依赖任务的信息检索。
conclusion: 为自动化知识发现与情境智能提供了新框架。
---

## Abstract
Information seeking bridges the knowledge gap between a query and its answer. Although LLMs perform well broadly, their ability to close this gap is limited by pretraining and degrades on specialized or up-to-date queries. A common remedy augments LLMs with external knowledge, either by injecting retrieved evidence into context or interleaving retrieval with reasoning. The former limits exploration of layered dependencies, while the latter is bounded by context length, constraining efficiency and scalability. For complex tasks with intricate dependencies and large text volumes, both approaches become inadequate.To tackle this bottleneck, we present AWARE (Agentic Knowledge Warehouse), an agentic knowledge warehousing framework that transforms heterogeneous, unstructured data into minimal, task-conditioned knowledge representations consumable by LLMs. Rather than exposing raw text, AWARE constructs knowledge through intent planning, online multi-threaded exploration, and map-reduce evidence integration, producing compact, LLM-ready context under finite budgets. Specifically, it applies offline document structuring to generate document headers that support controlled access, performs exploration with targeted refinement to recover layered information dependencies, and integrates distributed evidence into task-aware representations for downstream answer generation. Experiments on GAIA, WebWalker, and BrowseComp-Plus show improvements over all baselines

---

## 论文详细总结（自动生成）

# AWARE 论文中文总结

## 1. 核心问题与整体含义

- **研究动机**：LLM 的知识固定在预训练语料中，面对专业化、长尾或时效性强的查询时，知识覆盖与及时性不足，性能会下降。
- **现有方案瓶颈**：
  - **RAG**：预先检索并将证据注入上下文，但对复杂任务缺乏多步、分层依赖的探索深度。
  - **工具集成推理（TIR）**：将检索与推理交错进行，可迭代优化查询，但受上下文长度限制，效率与可扩展性差。
- **更根本挑战——Data Chaos**：真实外部数据（网页、PDF、TXT 等）长文本、异构、噪声、冗余，且**知识密度低**，答案相关信息稀疏嵌入大量文本中，导致 LLM 上下文预算被低密度内容迅速占满。
- **论文整体含义**：AWARE 将“检索”重新定义为**智能体式知识构建/知识仓库化**过程，不直接暴露原始文本，而是把异构非结构化数据转化为**最小、任务条件化、LLM-ready 的知识表示**，以在有限上下文预算下弥合复杂查询与答案之间的知识鸿沟。

## 2. 方法论

### 2.1 核心思想

- 复杂信息寻求任务的所需知识不是一次性检索得到，而是逐步构建的**序列知识链**：
  - \(K = (K_1 \rightarrow K_2 \rightarrow \cdots \rightarrow K_t)\)，其中 \(K_i\) 是第 \(i\) 步推理所需知识。
  - 每个 \(K_i\) 又由多个**原子知识空间**组合而成，体现“深度”上的顺序依赖与“广度”上的多源证据约束。
- 论文用信息论视角说明：复杂任务需要逐步降低条件熵 \(H(Y|X)\)，直到知识链足以确定答案。
- **Data Chaos 形式化**：定义知识密度 \(\delta(C)=I(Y;C|X)/|C|\)。当有限上下文预算 \(B\) 下 \(B\cdot\delta^*(R)<H(Y|X)\)，即原始证据虽总量丰富，但无法压缩成任务充分且预算可行的上下文，则发生 Data Chaos。
- AWARE 目标：构造高密度、紧凑、任务充分的上下文 \(C\)，使 \(\delta(C)\gg\delta(R)\)。

### 2.2 关键技术流程

- **离线文档结构化**：
  - 为每个文档或网页生成紧凑的**文档头（document header）** \(H_D\)，编码高层语义范围与结构组织。
  - 将语料交互分为两层：
    - 结构化控制：基于 \(\{H_D\}\) 估计相关性、冗余和优先级，产生文档级控制状态 \(C\)。
    - 内容访问：仅当必要时访问原始全文 \(D\)，进行细粒度证据抽取。
  - 文档头作为**访问控制原语**，决定何时检查、延迟或终止探索，避免无差别暴露低密度原始文本。

- **层级知识构建**：
  - 给定任务 \(X\)，形成初始信息意图 \(I_1\)，分解为多个子查询 \(\{q_{1,1},...,q_{1,n_1}\}\)。
  - 每个子查询触发一次信息访问，得到原子知识空间 \(S_{1,j}\)，整合为子空间 \(K_1\)。
  - 当 \(K_1\) 足够解决 \(I_1\)，推进到下一意图 \(I_2\)，重复直至意图序列完成。
  - 最终预测可写为：\(Y=\Theta(X\mid \{(I_i,K_i)\}_{i=1}^t)\)，即把推理算子条件化在“意图—证据链”上。

- **三个核心机制**：
  - **在线多线程探索**：
    - 初始子查询后形成暂定证据状态。
    - 不立即处理全文，而是先检查新候选文档的文档头，评估主题覆盖、冗余和缺失方面。
    - 若存在显著缺口，生成额外子查询，进行多线程扩展，覆盖未探索的意图侧面。
  - **Map–Reduce 证据集成**：
    - 先用文档头做轻量筛选，过滤明显不相关候选。
    - 通过筛选的文档并行抽取细粒度证据单元。
    - 最后由 reducer 聚合为子空间 \(K_i\)。
    - 形式化：\(K_i=R(\{E(D)\mid D\in F(D_i,I_i,\{H_D\})\})\)，其中 \(F\) 为头级过滤，\(E\) 为并行证据抽取，\(R\) 为归并。
  - **任务感知上下文化**：
    - 将意图序列与对应子空间组织为有序上下文：\(C=(X,(I_1,K_1),...,(I_t,K_t))\)。
    - 该表示保留意图推进、跨意图依赖和证据支撑，同时紧凑、预算可行，直接供下游 LLM 生成答案。

## 3. 实验设计

- **数据集 / Benchmark**：
  - **GAIA**：450+ 真实世界查询，涵盖多步推理、多模态与工具使用；论文使用其中 103 个纯文本验证问题。
  - **WebWalkerQA**：680 个查询，要求智能体遍历子页面并整合分散证据，属于长程推理挑战。
  - **BrowseComp-Plus**：830 个复杂问题，答案短且可验证，但通常需要大规模网络搜索与多文档阅读。
- **评价指标**：
  - GAIA：Exact Match。
  - WebWalkerQA：LLM Equivalence Accuracy。
  - BrowseComp-Plus：Accuracy 与 Search Calls。
- **对比方法**：
  - **直接推理无检索**：Qwen2.5-32B、Qwen3-32B、QwQ-32B、GPT-4o、Gemini-2.5-Flash、DeepSeek-R1-671B。
  - **RAG 类**：Vanilla RAG、Query Planning、Iterative RAG，分别搭配 Qwen2.5-32B / QwQ-32B。
  - **工具集成推理**：ReAct、Search-o1-32B、WebThinker-32B。
  - **BrowseComp-Plus 对比**：Gemini 2.5 Flash/Pro、Sonnet 4、GPT-4.1、GPT-5、Qwen3-32B、Search-R1-32B、AWARE。
- **实现细节**：
  - AWARE 中央推理模型：QwQ-32B；辅助处理器：Qwen2.5-7B，用于并行数据合成。
  - 索引：BGE-M3 稠密向量 + BM25，ElasticSearch 实现检索。
  - 在线检索：Google Custom Search JSON API；网页内容抽取：Jina AI Web Reader。
  - 多线程探索最大深度默认 5。
  - 初始化时每个查询收集 top-20 网页，5 次完整运行约得到 100K 网页，再生成文档头并建立本地索引。

## 4. 资源与算力

- **实际实验算力**：论文明确说明所有实验在**一个节点、8 张 NVIDIA A100-40G GPU** 上完成。
- **训练时长 / 训练算力**：AWARE 本身不涉及任务特定训练或端到端微调，因此论文未报告训练时长。
- **未执行的 RL 优化**：论文在 Limitations 中指出，若对 32B 模型做强化学习，合理估计至少需要 **32 张 H100 80G GPU**，但该资源超出作者条件，因此未进行。
- **API 与数据成本**

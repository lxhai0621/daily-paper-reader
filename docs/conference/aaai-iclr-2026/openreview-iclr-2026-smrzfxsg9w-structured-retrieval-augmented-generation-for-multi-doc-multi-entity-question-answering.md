---
title: Structured Retrieval-Augmented Generation for Multi-Doc Multi-Entity Question Answering
title_zh: 面向多文档多实体问答的结构化检索增强生成
authors: "Teng Lin, Yizhang Zhu, Zhengxuan Zhang, Yuyu Luo, Nan Tang"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=sMRzFxSg9W"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向多文档多实体问答的结构化RAG架构
tldr: 现有RAG在多文档多实体问答中常因粗粒度向量检索而遗漏关键事实。本文提出结构化RAG方法，通过构建跨文档证据链和实体关系图来弥补这一缺陷。实验表明该方法能更有效地整合碎片化信息并推断实体关系，提升复杂问答的准确性和可解释性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 针对现有RAG在多文档多实体问答中检索粒度过粗、难以构建跨文档证据链的问题，提出结构化检索增强生成方法。
method: 设计结构化RAG框架，显式建模实体间关系和跨文档证据链，融合向量检索与图结构信息进行增强生成。
result: 在MDMEQA任务上，所提方法相比基线RAG方法显著提升了答案准确率与证据构建能力。
conclusion: 结构化RAG能够有效整合碎片化信息，为多文档多实体复杂问答提供更可靠且可解释的检索增强范式。
---

## Abstract
Multi-document Multi-entity Question Answering (MDMEQA) fundamentally requires models to track and connect the implicit logic between multiple entities across documents, a task that reveals critical limitations of Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG) frameworks: they struggle to construct effective cross-document evidence chains and deduce entity relationships when faced with fragmented information. Although RAG improves answering capabilities through context injection, its coarse-grained retrieval strategy that relies on vector similarity often leads to the omission of critical facts. Meanwhile, graph-based RAG fails to efficiently integrate scattered complex relationship networks in multi-document scenarios, resulting in low efficiency in retrieving and reasoning MDMEQA. We propose Structured Retrieval-Augmented Generation (SRAG): a two-stage framework that first transforms unstructured text into semantically coherent relational tables via a SQL-driven Extraction-Retrieval module, then guides LLMs toward schema-aware relational reasoning over structured representations. This architectural breakthrough offers three key advantages: (1) SQL-powered indexing enables precise fact localization; (2) relational tables naturally support multi-hop entity join operations; (3) the structuring process mitigates the attention diffusion effect of LLMs. To verify the effectiveness of our proposed method, we evaluate SRAG on two multi-document QA benchmarks, MEBench and Loong. The results show that SRAG significantly outperforms the current state-of-the-art long-context LLMs and RAG systems, achieving 27.2% and 27% improvements in accuracy respectively. These results highlight the importance of structured data representation in enhancing complex reasoning and answer precision in multi-document multi-entity  question answering. The source code and data have been made available at https://anonymous.4open.science/r/SRAG-07A7.

---

## 论文详细总结（自动生成）

# 面向多文档多实体问答的结构化检索增强生成：论文总结

## 1. 论文核心问题与整体含义（研究动机与背景）

- **任务定义**：多文档多实体问答（MDMEQA）要求模型跨文档追踪多个实体之间的隐含逻辑关系并构建证据链，是一项极具挑战性的复杂推理任务。
- **现存痛点**：
  - **LLM 与 RAG 的局限**：面对碎片化信息时，难以构建有效的跨文档证据链，也难以推断实体间关系。
  - **向量检索粒度太粗**：传统 RAG 依靠向量相似度进行粗粒度检索，容易遗漏关键事实。
  - **图 RAG 效率不足**：图结构 RAG 在多文档场景下难以高效整合分散的复杂关系网络，检索与推理效率低下。
- **核心主张**：将非结构化文本转换为结构化关系表示，是解决 MDMEQA 中多实体关联与证据链构建困境的关键突破口。

## 2. 论文方法论：结构化检索增强生成（SRAG）

- **总体框架**：两阶段架构，核心思想是“先结构化、再推理”。
- **阶段一：SQL 驱动的抽取-检索模块（Extraction-Retrieval）**
  - 将非结构化文本转换为语义连贯的关系表（relational tables）。
  - 利用 SQL 建立精确索引，实现事实级精准定位（precise fact localization），替代传统向量相似度的粗粒度检索。
- **阶段二：模式感知的关系推理（Schema-aware Relational Reasoning）**
  - 引导 LLM 在结构化表示之上进行具备模式感知的关系推理。
  - 关系表天然支持多跳实体连接操作（multi-hop entity join），使跨文档实体关系推断成为可能。
- **三大关键技术优势**：
  1. SQL 索引实现精确事实定位；
  2. 关系表天然适配多跳实体连接；
  3. 结构化过程缓解了 LLM 的注意力扩散效应（attention diffusion effect）。
- **公式/算法流程**：原文未提供明确的数学公式，流程可概括为：`非结构化文本 → SQL驱动的抽取 → 关系表构建 → 模式感知推理 → 答案生成`。

## 3. 实验设计

- **Benchmark 数据集**（共两个）：
  - **MEBench**：多文档多实体问答专用基准。
  - **Loong**：长上下文问答基准。
- **对比方法**：
  - 当前 SOTA 的长上下文 LLM；
  - 现有 RAG 系统。
- **核心结果**：
  - 在 MEBench 上准确率提升 **27.2%**；
  - 在 Loong 上准确率提升 **27%**。
- **实验规模说明**：摘要仅报告了两个基准上的总体准确率对比，未包含逐类别的细粒度结果。

## 4. 资源与算力

- **论文中未明确说明**具体使用的 GPU 型号、数量、训练或推理时长、参数量级别等算力信息。
- 从摘要判断，SRAG 属于推理阶段的方法框架（基于现有 LLM），可能以推理开销为主而非大规模训练，但此推断缺乏原文数据支撑，需以论文全文为准。

## 5. 实验数量与充分性评估

- **实验组数**：从摘要来看，至少包含两个 benchmark 上的主实验，外加与多类基线（SOTA 长上下文 LLM + RAG 系统）的对比。
- **充分性评价**：
  - **积极方面**：跨越两个不同侧重的基准（多实体问答 + 长上下文），有一定覆盖度；相对于“当前 SOTA 长上下文 LLM 和 RAG 系统”均有较大幅度的提升，效果显著。
  - **不足方面**：摘要未提及消融实验（如去掉 SQL 索引、去掉结构化表示等）、不同 LLM 骨干的泛化测试、检索效率/延迟对比以及失败案例分析；实验是否对所有基线进行了公平的提示词调优等细节也未说明。

## 6. 论文主要结论与发现

- 结构化 RAG（SRAG）显著优于当前 SOTA 长上下文 LLM 与既有 RAG 系统，在 MEBench 与 Loong 两个基准上均实现约 27% 的准确率提升。
- 验证了核心假设：**结构化数据表示**（关系表 + SQL 索引）在增强多文档多实体复杂推理与答案精度方面具有重要价值。
- 为多文档复杂问答提供了一种更可靠且可解释的检索增强范式（结构化表示路径）。

## 7. 论文优点

- **问题选取得当**：精准识别了 MDMEQA 中“检索粒度粗”与“跨文档证据链难以构建”这两个关键缺陷。
- **方法设计巧妙**：
  - 用 SQL 索引替代纯向量检索，将“检索”转化为“查询”，兼顾精度与可解释性；
  - 关系表天然支持实体连接（join）操作，与多跳推理的需求高度契合；
  - 结构化处理缓解 LLM 注意力分散问题，具有一定理论启发性。
- **结果显著**：在两个基准上均取得大幅提升，且提升幅度接近，说明方法具有跨场景稳健性。
- **开源**：代码与数据已公开，为领域后续研究提供可复现基础。

## 8. 不足与局限

- **实验覆盖面有限**：仅两个 benchmark（MEBench、Loong），缺少更广泛的多文档 QA 基准（如 MultiHop-RAG、HotpotQA 等）上的验证；仅报告准确率，缺少推理效率、延迟、检索召回率等指标。
- **消融缺失**：摘要未提及消融实验，无法判定 SQL 索引与关系表各自对最终效果的贡献权重。
- **对图 RAG 的对比不够充分**：摘要提及图 RAG 效率不足，但未展示与图 RAG 的具体对比数据。
- **可迁移性存疑**：SQL 依赖的抽取-检索模块要求先将文本转换为关系表，这一转换对文本类型（如非结构化叙事文本、多语言文本）的适应性尚待检验。
- **算力与复现细节缺失**：未提供任何计算资源配置，影响复现与成本评估。
- **评估偏差风险**：摘要未说明答案匹配评估的具体方式（如精确匹配、LLM 评判），存在一定的评估口径不确定性。

（完）

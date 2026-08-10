---
title: "FineKB: Domain-Adaptive Issue Summarization and Cluster-Aware Retrieval for Support Knowledge Bases"
title_zh: FineKB：面向支持知识库的领域自适应问题摘要与聚类感知检索
authors: "Murat Kalender, Jeannie M Fitzgerald, Samaksh Gulati, Aashutosh Nema, Ian Roche"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=NWXUpwHPP7"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向支持知识库的领域自适应摘要与聚类感知检索
tldr: 企业支持场景中，用户描述冗长噪声大，与简洁KB文章语义不匹配。FineKB集成三部分：finetuned LLM生成伪摘要来规范化问题叙事；每篇KB多质心聚类建模不同子问题；置信度自适应混合推理，高置信向量检索辅以内容查找和LLM推理。实验表明该方法能显著提升领域内KB检索的相关性与鲁棒性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 企业支持场景中问题描述与KB表述存在语义鸿沟，检索困难。
method: FineKB结合LLM摘要规范化、多质心聚类和置信度自适应混合检索。
result: 在支持KB检索任务上显著优于现有基线，提高准确率。
conclusion: 领域自适应的摘要与聚类感知检索可有效弥合KB检索语义鸿沟。
---

## Abstract
Retrieving relevant knowledge base (KB) articles for enterprise support cases is difficult due to the semantic mismatch between noisy, verbose case descriptions and concise KB content. We present FineKB, a domain-adaptive issue–summarization and cluster-aware retrieval framework that addresses this gap through (i) a finetuned LLM trained on teacher-generated pseudo-summaries to normalize heterogeneous case narratives, (ii) per-KB multi-centroid clustering that models the diverse sub-problems associated with each KB article, and (iii) a confidence-adaptive hybrid inference mechanism that augments high-confidence vector search with selective content lookup and LLM reasoning for ambiguous cases. At inference time, raw case text is embedded and matched against this summary-structured index, avoiding runtime summarization while improving alignment. Experiments on large-scale enterprise data show that FineKB achieves 65.39\% Recall@3, substantially outperforming KB-content dense retrieval (42.73\%). To support reproducible research on noisy-to-structured retrieval, we release FineKB-Vectors, a vectorized dataset containing case-summary and KB-article embeddings.

---

## 论文详细总结（自动生成）

# FineKB 论文中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- 企业支持场景中，用户提交的 case 描述通常冗长、口语化且带有大量噪声，而知识库（KB）文章往往简洁、规范化，两者之间存在严重的**语义鸿沟**，导致基于传统密集检索的方法难以准确匹配到相关 KB 文章。
- 现有检索方法大多直接对原始 KB 内容建立索引，忽视了问题描述与 KB 表述之间在长度、风格和粒度上的不一致性。
- 因此，论文旨在构建一个**领域自适应、能够将“噪声化问题描述”对齐到“结构化 KB 文章”** 的检索框架，以提升企业支持知识库的检索准确性和鲁棒性。

## 2. 论文提出的方法论

FineKB 是一个三部分组成的检索框架：

- **（i）问题摘要规范化（Issue Summarization）**
  - 使用**教师模型生成伪摘要**作为训练目标，微调一个轻量级 LLM，
  - 使模型学会将异构、冗长的 case 叙述转换为统一、简洁的问题摘要，
  - 从而在语义上更接近 KB 文章的表述风格。

- **（ii）每 KB 多质心聚类（Per-KB Multi-Centroid Clustering）**
  - 对每个 KB 文章关联的不同用户问题子场景进行聚类，
  - 为每篇文章构建多个质心向量，以建模同一个 KB 文章可能对应的多种不同子问题，
  - 从而提升索引的表达能力与匹配覆盖度。

- **（iii）置信度自适应混合推理（Confidence-Adaptive Hybrid Inference）**
  - 推理时，先对原始 case 文本做嵌入，并在“摘要结构化的索引”上进行检索；
  - 若向量检索的置信度高，则直接返回结果；
  - 若置信度低（即歧义 case），则引入**选择性内容查找**和**LLM 推理**进行补充判断。
  - 这样做避免在推理阶段运行 LLM 摘要，降低时延，同时保持对齐质量。

> 整体流程：原始 case 文本 → 嵌入 → 与摘要和质量中心索引匹配 → 按置信度决定是否启用混合推理 → 返回候选 KB 文章。

## 3. 实验设计

- **数据集 / 场景**：使用了**大规模企业支持数据**（具体规模未在摘要中说明），并发布了去标识化的向量数据集 **FineKB-Vectors**，其中包含 case-summary 嵌入和 KB 文章嵌入，用于支持可复现研究。
- **Benchmark 任务**：企业支持场景下的“噪声问题描述 → 相关 KB 文章”检索任务。
- **对比方法**：摘要中明确提到与 **KB-content dense retrieval**（直接用 KB 内容做密集检索）进行对比。
- **主要指标**：Recall@3。
  - FineKB：**65.39%**
  - KB-content dense retrieval：**42.73%**
  - 相对提升显著。

## 4. 资源与算力

- 摘要和元数据中**未明确说明**使用的 GPU 型号、数量、训练时长、微调 LLM 的参数量级等具体算力信息。
- 仅提到使用了“finetuned LLM”和“教师生成的伪摘要”，但未给出训练开销细节。
- 若有需要，需查阅论文全文以获取资源配置信息。

## 5. 实验数量与充分性

- 从摘要可见，论文报告了**至少一个核心实验**（Recall@3 对比），并提及发布了数据集用于后续验证。
- 但摘要中**没有明确列举多组实验**（如不同领域、不同规模的消融、多指标评估、不同检索基线的对比等），因此仅凭摘要难以判断实验的完整性和充分性。
- 若实验仅包含单一大规模数据集上的一个 Recall 指标，则缺乏对鲁棒性、泛化性和各组件贡献的深度验证；是否公平还需依赖全文的对照设置与消融细节。

## 6. 主要结论与发现

- FineKB 通过**领域自适应的摘要规范化**与**聚类感知索引**，能够有效弥合噪声 case 描述与简洁 KB 文章之间的语义鸿沟。
- 在真实企业数据上，FineKB 将 Recall@3 从 42.73% 提升到 65.39%，说明该框架显著优于直接基于 KB 内容的密集检索。
- 发布 FineKB-Vectors 数据集，为企业支持领域的噪声到结构化检索研究提供公开基准资源。

## 7. 优点

- **问题定位准确**：紧扣企业支持场景中“噪声描述 vs 简洁 KB”的核心痛点，具有实际应用价值。
- **方法设计巧妙**：
  - 利用教师模型生成伪摘要，降低人工标注成本；
  - 多质心聚类能覆盖同一 KB 文章的不同子问题，提高召回能力；
  - 置信度自适应混合推理在保证效率的同时增强歧义样本的处理能力。
- **避免推理阶段摘要开销**：通过离线构建摘要结构化索引，推理时仅做向量匹配，兼顾效果与效率。
- **开放数据资源**：释放向量化数据集，有利于后续研究对比和复现。

## 8. 不足与局限

- **信息透明度有限**：摘要未披露数据规模、领域范围、KB 文章与 case 数量、基线实现细节、多个评估指标（如 MRR、NDCG、精确率等），难以全面评估优劣。
- **泛化性未验证**：实验仅面向企业支持 KB，是否适用于其他领域或跨领域场景尚不明确。
- **伪摘要质量依赖**：教师模型生成的伪摘要质量直接影响微调效果，若教师存在偏差，可能传播到系统中。
- **聚类与混合推理的额外复杂度**：多质心聚类和 LLM 推理的引入会带来索引构建和推理时延/成本，论文未说明这些开销的具体影响。
- **消融与敏感性分析缺失**：从摘要看，未交代各组件的独立贡献、置信度阈值的影响、聚类数量选择等关键实验，严谨性和可解释性有待增强。

（完）

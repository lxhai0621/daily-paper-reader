---
title: "KG-Infused RAG: Augmenting Corpus-Based RAG with External Knowledge Graphs"
title_zh: KG-Infused RAG：用外部知识图谱增强基于语料库的RAG
authors: "Dingjun Wu, Yukun Yan, Zhenghao Liu, Zhiyuan Liu, Maosong Sun"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=vhDOprq9Hf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 将既有知识图谱与语料段落结合，进行多源检索与生成
tldr: 现有RAG要么只用文本语料而忽略结构化知识，要么自建知识图谱成本高且可靠性低。KG-Infused RAG将预训练的大规模知识图谱直接引入RAG，利用传播激活在外部知识图谱上检索相关结构化知识，并用其扩展查询、与语料段落融合，形成可解释的多源检索。该方法在提升RAG事实准确性与检索质量的同时保持了结构化知识的语义可解释性，有效弥合了文本与知识图谱之间的鸿沟。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG忽视结构化知识，而自建知识图谱成本高昂且可靠性不足。
method: 借助传播激活在外部知识图谱上检索结构化知识，并用于查询扩展和多源段落融合。
result: 在检索与生成质量上优于纯文本RAG，且结构化知识带来可解释性提升。
conclusion: 利用既有知识图谱可低成本增强RAG的结构化知识利用能力。
---

## Abstract
Retrieval-Augmented Generation (RAG) improves factual accuracy by grounding responses in external knowledge. However, existing RAG methods either rely solely on text corpora and neglect structural knowledge, or build ad-hoc knowledge graphs (KGs) at high cost and low reliability. To address these issues, we propose **KG-Infused RAG**, a framework that incorporates pre-existing large-scale KGs into RAG and applies *spreading activation* to enhance both retrieval and generation. 
KG-Infused RAG directly performs spreading activation over external KGs to retrieve relevant structured knowledge, which is then used to expand queries and integrated with corpus passages, enabling interpretable and semantically grounded multi-source retrieval. We further improve KG-Infused RAG through preference learning on sampled key stages of the pipeline. 
Experiments on five QA benchmarks show that KG-Infused RAG consistently outperforms vanilla RAG (by 3.9% to 17.8%). Compared with KG-based approaches such as GraphRAG and LightRAG, our method obtains structured knowledge at lower cost while achieving superior performance. Additionally, integrating KG-Infused RAG with Self-RAG and DeepNote yields further gains, demonstrating its effectiveness and versatility as a plug-and-play enhancement module for corpus-based RAG methods.

---

## 论文详细总结（自动生成）

## KG-Infused RAG：用外部知识图谱增强基于语料库的RAG

### 1. 核心问题与整体含义（研究动机和背景）
- **背景**：检索增强生成（RAG）通过外部知识来提升事实准确性，但现有方法存在明显短板：
  - **纯文本RAG**：只依赖文本语料，忽略结构化知识（如实体、关系），难以处理需要复杂推理和关系理解的问题。
  - **自建知识图谱的 KG-RAG**：虽能引入结构化信息，但构建成本高、可靠性低，且往往针对特定任务临时构建，缺乏通用性。
- **核心问题**：如何以低成本、高可靠的方式，将现有的大规模知识图谱高效融入 RAG，既提升检索与生成质量，又保持结构化知识的语义可解释性？
- **总体含义**：本文提出一种“即插即用”的增强模块，利用预训练好的大规模外部知识图谱来辅助基于语料库的 RAG，弥合文本与结构化知识之间的鸿沟。

### 2. 方法论：核心思想、关键技术细节与流程
- **核心思想**：直接在外部知识图谱上执行**传播激活（spreading activation）**，检索与查询相关的结构化知识子图，并用这些知识来扩展查询、融合语料段落，从而实现可解释的多源检索。
- **关键技术细节**：
  - **外置知识图谱**：直接使用已有的通用大规模知识图谱，免去自建图谱的高昂成本。
  - **传播激活机制**：从查询中的实体出发，沿图结构传递激活值，筛选出与查询语义相关的实体和关系，形成结构化知识片段。
  - **查询扩展**：将检索到的结构化知识转化为文本形式的扩展信息，与原始查询拼接，用于后续的语料检索。
  - **多源融合**：将知识图谱检索结果与文本语料检索结果进行融合，作为生成器的上下文输入。
  - **偏好学习优化**：在流水线的关键阶段（如查询扩展、知识选择等）构造正负样本，通过偏好学习进一步优化整个框架的各个环节。
- **流程概述**：输入查询 → 在外部知识图谱上执行传播激活 → 获得结构化知识 → 用结构化知识扩展查询 → 并行检索语料库 → 将知识片段与语料段落融合 → 生成回答。

### 3. 实验设计
- **数据集/场景**：使用 **5 个问答（QA）基准数据集**（具体名称未在摘要中列出），覆盖不同的问答类型和领域。
- **对比方法**：
  - **基线**：vanilla RAG（纯文本语料 RAG）。
  - **知识图谱方法**：GraphRAG、LightRAG（自建或内部图谱方法）。
  - **集成验证**：将 KG-Infused RAG 与 Self-RAG、DeepNote 等现有 RAG 方法结合，验证其通用性。
- **评估维度**：检索质量（如召回率/命中率）与生成质量（如事实准确性、回答正确性），同时考察结构化知识带来的可解释性。

### 4. 资源与算力
- 论文摘要及提供的元数据中**未明确说明**使用的 GPU 型号、数量、训练时长等算力信息。
- 仅能推断该方法相比自建图谱的 KG 方法**成本更低**，但具体计算资源消耗（如额外推理开销）未给出定量描述。

### 5. 实验数量与充分性
- **实验组数**：至少包括——
  - 在 5 个 QA 基准上与 vanilla RAG 的主对比（5组）。
  - 与 GraphRAG、LightRAG 的对比（2组）。
  - 与 Self-RAG、DeepNote 的集成实验（2组或更多）。
  - 偏好学习对流水线关键阶段的优化效果（可能存在消融，但摘要未详述）。
- **充分性评价**：
  - **优点**：多数据集、多基线、多集成场景，能够较全面地展示方法的有效性和通用性。
  - **不足**：摘要未提供消融实验细节（如不同知识图谱规模、传播激活步数的影响），未给出误差线或显著性检验，也未报告失败案例或限制分析，因此实验的细致程度和客观性信息有限。

### 6. 主要结论与发现
- **性能提升显著**：在 5 个 QA 基准上，KG-Infused RAG 相比 vanilla RAG 提升 **3.9% 到 17.8%**，说明引入外部结构化知识能有效改善 RAG 的检索与生成质量。
- **优于图谱类方法**：相比 GraphRAG、LightRAG，该方法能以更低成本获取结构化知识，并取得更优性能。
- **即插即用**：与 Self-RAG、DeepNote 结合后性能进一步提升，证明其可作为通用增强模块，适配现有基于语料库的 RAG 方法。
- **可解释性**：通过显式使用知识图谱中的实体和关系，检索和生成过程更具语义可解释性。

### 7. 优点
- **低成本利用结构化知识**：直接使用预训练的大规模知识图谱，规避自建图谱的高成本和不稳定问题。
- **多源信息融合**：将文本语料与结构化知识结合，兼顾全局语义和关系推理。
- **可解释性强**：传播激活过程与知识图谱路径明确，便于追溯模型依据。
- **通用性强**：作为插件式模块，可与多种现有 RAG 方法（Self-RAG、DeepNote）集成，易于部署。
- **优化手段新颖**：将偏好学习应用于流水线关键阶段，而非简单端到端训练，更有针对性地提升各环节质量。

### 8. 不足与局限
- **实验细节缺失**：论文摘要未提供 5 个数据集的具体名称、规模与类型，无法评估领域覆盖的广泛性。
- **算力信息不透明**：未报告推理或训练的资源消耗，难以评估实际部署成本。
- **消融不充分**：未系统展示不同组件（传播激活步数、查询扩展方式、融合策略）的贡献，也未比较不同外部知识图谱的影响。
- **潜在偏差风险**：仅使用 QA 任务验证，未涉及长文生成、多跳推理、金融/医疗等专业领域；可能存在对特定知识图谱的依赖，若图谱缺失相关实体则性能可能下降。
- **真实场景验证不足**：未讨论知识图谱更新、动态查询、大规模工业部署等实际问题。

（完）

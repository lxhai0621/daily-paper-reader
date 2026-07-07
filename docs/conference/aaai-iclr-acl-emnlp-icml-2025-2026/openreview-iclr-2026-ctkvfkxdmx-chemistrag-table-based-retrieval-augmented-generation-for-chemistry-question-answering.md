---
title: "ChemisTRAG: Table-based Retrieval-Augmented Generation for Chemistry Question Answering"
title_zh: ChemisTRAG：面向化学问答的基于表格的检索增强生成
authors: "Gongyao Jiang, Qiong Luo"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=ctkVFKXDMX"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于表格的化学问答RAG
tldr: 化学领域RAG面临实体名称和表示格式变化的挑战。ChemisTRAG将化学信息显式存储为表格，查询时先提取化学实体，再从表格中选择相关行。这种方法避免了文本检索中的对齐问题，在化学问答任务上取得了优越性能。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 化学RAG中实体对齐困难，文本检索易受命名变化影响。
method: 将化学信息存储为表格，查询时提取实体并选择相关表格行。
result: 在化学问答上取得优越性能。
conclusion: 表格化知识库能有效提升化学RAG的效果。
---

## Abstract
Recent work has shown that retrieval-augmented generation (RAG) improves the performance of large language models (LLMs) for question answering on chemistry. However, existing chemistry RAG techniques are mainly based on text. It is challenging for the retriever to align the information about chemical entities between the query and the underlying corpora, especially if the naming and representation formats change. To address this problem, we propose ChemisTRAG, a RAG system in which information about chemical entities and reactions is stored explicitly as tables in the knowledge base (KB). Upon a query, ChemisTRAG first extracts chemical entities from the query and then selects relevant rows from the tabular KB. This way, the alignment processing is simplified and the accuracy is improved regardless of different naming conventions of compounds. To balance accurate answer retrieval for exact matches and robust reasoning for similar matches, we propose an adaptive reasoning process for the LLM: it first generates a reasoning prototype, then adapts the reasoning path to retrieval results, and finally infers the final answer contextualized on the example reasoning path. We have constructed a dataset of more than 38,000 compounds and 23,000 reactions from the recent five years of patents, and generated eight types of question-answering tasks to evaluate our system. Results show that ChemisTRAG consistently outperforms text-based RAG across all eight tasks, particularly in handling diverse chemical representations like SMILES and IUPAC.

---

## 论文详细总结（自动生成）

# ChemisTRAG 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：检索增强生成（RAG）已被证明能提升大语言模型（LLM）在化学问答上的性能。但现有化学RAG技术主要基于文本检索，面临化学实体名称和表示格式（如SMILES、IUPAC名称）多样化的挑战，检索器难以对齐查询与语料库中的化学实体信息。
- **核心问题**：如何克服化学实体命名和表示变化带来的对齐困难，提升化学领域问答的准确性和鲁棒性。
- **整体含义**：提出一种基于表格化知识库的RAG系统，将化学信息显式存储为表格，通过实体提取和行选择简化对齐过程，从而提升性能。

## 2. 方法论

- **核心思想**：将化学实体和反应信息显式存储为表格形式，查询时先提取化学实体，再从表格知识库中选择相关行，避免文本检索中的命名歧义。
- **关键技术细节**：
  - **知识库构建**：将化合物和反应信息组织成结构化表格，每行对应一个实体或反应，列包含属性（如SMILES、IUPAC名称、分子式、反应条件等）。
  - **查询处理**：输入自然语言问题，先用NER或规则提取化学实体（如化合物名称、SMILES字符串）；然后基于提取的实体在表格中进行精确或模糊匹配，选择相关行。
  - **自适应推理过程**：LLM先生成一个推理原型，再根据检索结果调整推理路径，最后结合示例推理路径给出最终答案。此设计平衡了精确匹配（exact matches）的准确检索与相似匹配（similar matches）的鲁棒推理。
- **算法流程（文字说明）**：
  1. 构建包含38,000+化合物和23,000+反应的表格知识库。
  2. 用户提问 → 实体提取模块识别其中的化学实体。
  3. 表格检索模块根据实体选择相关行（可支持SMILES、IUPAC等多种表示）。
  4. LLM进行自适应推理：首先生成推理原型，然后根据检索结果调整，最终得出答案。

## 3. 实验设计

- **数据集**：从近五年（论文写作时最近五年）的专利中构建，包含38,000+化合物和23,000+反应。生成了八种类型的问答任务（未具体列出八种类型，但涵盖不同化学表示和问题形式）。
- **基准（Benchmark）**：基于文本的RAG系统（text-based RAG）作为对比基线。
- **对比方法**：主要对比文本基RAG，未提及其他基线（如纯LLM、其他RAG变体）。
- **评估指标**：未明确提及具体指标（推测为准确率或F1等），但结果显示ChemisTRAG在所有八种任务上一致优于文本基RAG。

## 4. 资源与算力

- 论文中未明确提及使用的GPU型号、数量、训练时长等算力信息。仅提到构建了数据集并进行了实验，但未对资源使用做说明。

## 5. 实验数量与充分性

- **实验数量**：八种不同类型的问答任务上的对比实验。未提及消融实验或敏感性分析。
- **充分性**：实验覆盖了多种化学表示（SMILES、IUPAC等），但对比方法单一（仅文本基RAG），缺少与其他先进化学RAG方法或表格基方法的对比。消融实验（如单独验证实体提取、自适应推理的作用）未提及。因此实验充分性一般，客观性尚可但不够全面。

## 6. 主要结论与发现

- ChemisTRAG在化学问答任务上一致优于文本基RAG，尤其在处理SMILES、IUPAC等多样化化学表示时优势明显。
- 表格化知识库能有效解决化学实体对齐困难，简化检索流程并提升准确性。
- 自适应推理过程有助于平衡精确匹配与相似匹配，提升鲁棒性。

## 7. 优点

- **方法创新**：首次将化学知识显式存储为表格用于RAG，直接应对命名变化问题。
- **简单有效**：实体提取+表格行选择比文本检索更直接，对齐复杂度降低。
- **自适应推理**：结合原型生成与路径调整，增强了LLM的推理灵活性。
- **数据集构建**：基于近五年专利构建大规模真实数据，具实际应用价值。

## 8. 不足与局限

- **对比方法单一**：仅与文本基RAG对比，未与更先进的RAG变体（如基于知识图谱、图检索等）或纯LLM对比。
- **消融实验缺失**：未拆解分析各组件（实体提取、表格检索、自适应推理）的贡献。
- **实验覆盖有限**：虽八种任务，但未提供具体任务定义和指标细节，难以复现验证。
- **未公开资源与代码**：缺乏可复现性保障。
- **应用限制**：仅针对化学领域，表格构建需人工或半自动标注，扩展至其他领域成本高。
- **未考虑规模扩展**：未讨论表格知识库随数据量增长时的检索效率问题。

（完）

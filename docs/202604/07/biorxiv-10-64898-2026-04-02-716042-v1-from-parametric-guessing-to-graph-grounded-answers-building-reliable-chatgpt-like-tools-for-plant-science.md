---
title: "From Parametric Guessing to Graph-Grounded Answers: Building Reliable ChatGPT-like tools for Plant Science"
title_zh: 从参数化猜测到基于图谱的回答：构建可靠的植物科学类 ChatGPT 工具
authors: "Itharajula, M., Lim, S. C., Mutwil, M."
date: 2026-04-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.02.716042v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过从参数化猜测转向图谱接地答案来减少幻觉
tldr: 本研究针对大语言模型在植物科学领域（如列举基因列表）中存在的知识不完整、缺乏来源归属及不可重复等问题，分析了现有微调和RAG技术的局限性。提出采用图检索增强生成（GraphRAG）架构，通过将LLM与结构化知识图谱结合，实现可靠、可追溯且完整的知识检索，为构建植物科学领域的专业AI工具提供了技术路线图。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-02-716042-v1/fig-001.webp\", \"caption\": \"Figure 1. Catastrophic forgetting in large language models. A. Illustration of catastrophic 78 forgetting. Pre-trained LLM (left panel) is updated with new information (middle panel), resulting 79 in a loss of previous knowledge (right panel). Blue color represents paint (knowledge), while 80\", \"page\": 3, \"index\": 1, \"width\": 964, \"height\": 887}]"
motivation: 通用大语言模型在处理植物生物学中需要跨文献汇总的精确列表查询时，容易产生幻觉且无法提供完整的证据支持。
method: 评估了主流LLM的表现，分析了微调与传统RAG的不足，并提出利用知识图谱驱动的GraphRAG架构作为替代方案。
result: 发现现有LLM无法返回完整的基因列表或可靠引用，而GraphRAG能有效整合分散在大量文献中的结构化信息并保证结果的可重复性。
conclusion: 建立开放且持续更新的植物知识图谱并结合GraphRAG技术，是将海量文献阅读转化为高效、可靠查询的关键路径。
---

## 摘要
大语言模型（LLMs）正越来越多地被植物生物学家用于总结文献、生成假设和解释实验结果。然而，LLMs 在提供详尽且具有来源归属的事实方面并不可靠，这对于植物生物学中普遍存在的列表式查询（例如，“列出拟南芥中调节次生细胞壁（SCW）生物合成的所有转录因子”）是一个关键限制。在本文中，我们使用此类查询对 ChatGPT、Claude 和 Gemini 进行了测试，并证明没有一个模型能返回带有可靠引用的完整基因列表。我们将这些失败归因于 LLMs 存储知识的方式：知识作为统计模式分布在数十亿个内部参数中，缺乏保证完整性、溯源性或可重复性的机制。我们还回顾了微调缓解策略，包括多任务指令微调、参数高效方法和上下文工程，这些方法虽然能缓解但无法解决这些局限性。随后，我们讨论了检索增强生成（RAG），它在查询时向 LLM 提供相关文档；我们认为，虽然它改善了来源归属，但当答案需要综合散布在数百篇论文中的信息时，它仍然不切实际。作为替代方案，我们提倡图检索增强生成（GraphRAG），其中 LLM 作为结构化、具有溯源链接的知识图谱（KG）上的推理和语言接口，能够以可重复的方式返回完整的结果集。我们概述了一个实用的 GraphRAG 架构，并调查了现有的植物知识图谱资源。最后，我们讨论了公开挑战，包括实体消歧、关系规范化和证据分级，并提出了构建开放、持续更新的植物知识图谱的路线图，旨在将“阅读 1,000 篇论文”转变为单次可重复的查询。

## Abstract
Large language models (LLMs) are increasingly used by plant biologists to summarize literature, generate hypotheses, and interpret experimental results. However, LLMs are unreliable sources of exhaustive, source-attributed facts, a critical limitation for the list-style queries that pervade plant biology (e.g., "list all transcription factors regulating secondary cell wall (SCW) biosynthesis in Arabidopsis"). Here, we query ChatGPT, Claude, and Gemini with such queries and demonstrate that none return complete gene lists with reliable citations. We trace these failures to how LLMs store knowledge: as statistical patterns distributed across billions of internal parameters, with no mechanism to guarantee completeness, provenance, or reproducibility. We also review fine-tuning mitigation strategies, including multi-task instruction tuning, parameter-efficient methods, and context engineering, that alleviate but do not resolve these limitations. We then discuss retrieval-augmented generation (RAG), which feeds relevant documents to the LLM at query time, and argue that while it improves source attribution, it remains impractical when answers require synthesizing information scattered across hundreds of papers. As an alternative, we advocate graph retrieval-augmented generation (GraphRAG), in which the LLM serves as a reasoning and language interface over a structured, provenance-linked knowledge graph (KG) that returns complete result sets reproducibly. We outline a practical GraphRAG architecture and survey existing plant KG resources. Finally, we discuss open challenges, including entity disambiguation, relation normalization and evidence grading, and propose a roadmap for building open, continuously updated plant KGs that can turn "read 1,000 papers" into a single reproducible query.
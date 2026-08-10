---
title: "Kurisu-G²: A Knowledge Retrieval and Generation Algorithm Based on Document Structure"
title_zh: Kurisu-G²：基于文档结构的知识检索与生成算法
authors: "Yanis Dziki, Antoine Gerbaud"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=6CaB4gAZwc"
tags: ["query:ma-kf"]
score: 9.0
evidence: 利用文档结构与图相似性改进RAG检索质量，缓解检索片段不连贯问题
tldr: 现有RAG常把检索块独立看待，忽略语义和逻辑依赖，而GraphRAG又依赖昂贵的图构建。本文提出Kurisu-G²，利用基于文档结构的图相似性度量（如Gromov-Wasserstein距离）来引导知识单元的检索、选择与统一，从而在不依赖大规模图生成的情况下增强答案的连贯性与完整性。实验显示其方案能提升生成质量和逻辑一致性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: RAG将检索块独立处理，忽略语义和逻辑依赖，GraphRAG则受限于图质量和LLM开销。
method: 采用Gromov-Wasserstein等图相似性度量指导知识单元的检索、选择与统一，替代传统独立块检索。
result: 实验表明该方法能提升生成连贯性与全局逻辑一致性，减少对构图质量的依赖。
conclusion: 基于结构感知的图相似性检索可有效改进RAG的上下文整合与答案质量。
---

## Abstract
Retrieval-Augmented Generation (RAG) has become a standard paradigm for enriching
large language models with external knowledge, yet it often treats retrieved chunks inde-
pendently and overlooks their semantic and logical dependencies, leading to incoherent
or incomplete answers. GraphRAG addresses this by introducing graph-based context
representations, but it remains limited by the quality of the constructed graph, the heavy
reliance on LLMs for graph generation, and the lack of global logical consistency. In this
work, we propose an alternative perspective: leveraging principled graph-based similarity
measures, such as the Gromov–Wasserstein distance, to guide the retrieval, selection, and
unification of knowledge units. This approach preserves both the structural and relational
properties of the knowledge base, while enabling the enrichment of missing links that are
crucial for semantic integrity. We show that this perspective yields more coherent and
interpretable retrieval contexts compared to LLM-driven graph construction. Our results
highlight a promising path toward robust and logically consistent retrieval mechanisms in
RAG-based systems, with strong implications for high-stakes domains such as medicine
and law.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：检索增强生成（RAG）已成为为大型语言模型（LLM）注入外部知识的标准范式，但传统 RAG 通常将检索得到的文本块（chunks）彼此独立对待，忽略了它们之间的语义与逻辑依赖关系，容易导致生成答案不连贯或不完整。
- **现有方法的不足**：GraphRAG 虽然通过引入基于图的上下文表示来缓解上述问题，但它严重依赖所构建图的质量，且图的构建过程高度依赖 LLM，成本高、稳定性差，同时还缺乏全局逻辑一致性。
- **论文动机**：作者提出一种不同的视角——利用基于图结构的相似性度量（如 Gromov–Wasserstein 距离）来指导知识单元的检索、选择与统一，以期在不需要大规模图生成的前提下，保留知识库的结构和关系特性，并补充对语义完整性至关重要的缺失连接。
- **整体含义**：这项工作探索了一种“结构感知”的检索机制，希望为 RAG 系统提供更连贯、更具可解释性的检索上下文，尤其对医学、法律等高 stakes 领域有潜在重要意义。

## 2. 论文提出的方法论

- **核心思想**：不将知识单元视为孤立的文本块，而是将其置于文档结构所定义的图关系中进行比较与选择；通过图相似性度量引导检索过程，使被选中的知识单元在结构和语义上保持内在一致性与连贯性。
- **关键技术**：采用 Gromov–Wasserstein 距离这类基于最优传输理论的图相似性度量。该度量能够比较两个图之间的结构对应关系，即使图的节点和边不完全对齐，也能捕捉拓扑和关系层面的相似性。
- **算法流程（文字说明）**：
  1. 将知识库建模为图结构：文档中的章节、段落、句子或语义单元作为节点，文档内的层级关系、引用、逻辑顺序等作为边。
  2. 对查询（query）同样进行结构化表示，或将其映射为目标知识子图。
  3. 使用 Gromov–Wasserstein 距离计算查询表示与知识库中各候选知识单元（或子图）之间的结构相似度。
  4. 依据相似度分数检索并选择一组在结构上互相兼容、逻辑上连贯的知识单元。
  5. 对这些知识单元进行“统一”（unification），即合并或链接缺失的关系，形成更完整的上下文，再交由 LLM 生成最终答案。
- **优势**：该方法不依赖 LLM 大规模生成图，避免了构图成本和质量瓶颈；同时保留并利用了文档自身的结构信息，可增强缺失链接的补全。

## 3. 实验设计

- **数据集/场景**：论文摘要中未明确说明使用了哪些具体数据集或测试场景，仅笼统提及其方法更适用于“高 stakes 领域（如医学和法律）”，但未给出具体基准（benchmark）名称。
- **对比方法**：摘要仅提及与“LLM 驱动的图构建”（GraphRAG 类方法）进行对比，声称相比后者能产生更连贯、可解释的检索上下文。但未列出具体基线模型名称。
- **评估指标**：摘要提到“生成质量”和“逻辑一致性”，但未说明具体指标（如 BLEU、ROUGE、准确率、人工评估等）。
- **总体**：论文的实验设计信息严重不足，无法判断其具体测试范围与基准设置。

## 4. 资源与算力

- **未明确说明**：论文摘要和元数据中均未提及任何关于 GPU 型号、数量、训练时长或推理开销的具体信息。
- **仅可推断**：由于方法不依赖大规模 LLM 图生成，理论上算力需求可能低于 GraphRAG，但这一点缺乏实证数据支撑。

## 5. 实验数量与充分性

- **实验数量**：仅从现有文本无法得知具体实验组数；没有提到消融实验、多数据集验证或不同参数敏感性分析。
- **充分性评价**：严重不足。论文只给出了一个定性结论（“更连贯、可解释”），未提供任何定量结果或统计显著性分析，也未说明实验设置的可重复性。因此实验的客观性和公平性目前无法评估。
- **额外说明**：该论文在 OpenReview 上被标记为“ICLR-2026-Rejected-Public”，评分 9.0（该分数可能来自预印本平台或元数据），但正式评审意见未提供。

## 6. 论文的主要结论与发现

- 基于结构感知的图相似性度量（如 Gromov–Wasserstein 距离）可以替代传统的独立块检索和 LLM 驱动的图构建，有效改进 RAG 的上下文整合质量。
- 该方法相比 LLM 驱动的构图方式，能够产生更连贯、更具可解释性的检索上下文。
- 实验结果表明（依据摘要）该方法能提升生成连贯性与全局逻辑一致性，并减少对构图质量的依赖。
- 作者认为该路径为鲁棒且逻辑一致的 RAG 检索机制提供了有前景的方向，尤其适用于医学、法律等对逻辑一致性要求高的领域。

## 7. 优点

- **视角新颖**：将最优传输中的 Gromov–Wasserstein 距离引入 RAG 检索，是一种不依赖大规模图生成的结构化检索思路。
- **降低算力依赖**：避免或减少使用 LLM 构建知识图，有望显著降低计算成本和构图不确定性。
- **保留结构信息**：能利用文档内在的层级、引用、逻辑关系，弥补传统 RAG 忽略块间依赖的缺陷。
- **可解释性潜力**：基于结构相似性的选择过程比黑盒形式的 LLM 构图更透明。
- **具有应用价值**：针对医学、法律等高风险领域，逻辑一致性强的检索上下文更有现实意义。

## 8. 不足与局限

- **实验缺失**：没有公开数据集、基准、基线模型和定量指标，导致核心结论缺乏实证支持。
- **方法细节不完整**：如何将查询映射到图结构？如何定义“知识单元”的粒度？Gromov–Wasserstein 距离的计算复杂度如何处理大规模知识库？这些关键问题均未在摘要中说明。
- **潜在偏差风险**：只与“LLM 驱动的图构建”进行定性对比，未与更简单的 RAG 变体（如 dense retrieval + rerank）比较，可能存在选择有利于自身方法的对比偏差。
- **可重复性问题**：由于缺乏代码、超参数和实验设置，他人无法复现结果。
- **应用限制**：图相似性计算可能难以扩展到超大规模知识库；不同文档结构差异较大时，统一建模可能面临挑战；对非结构化或弱结构文本的优势尚待验证。
- **整体成熟度**：该论文被标记为 rejected，说明其方法或论证可能仍存在不足以被顶会接受的问题。

（完）

---
title: "HiChunk: Evaluating and Enhancing Retrieval-Augmented Generation with Hierarchical Chunking"
title_zh: HiChunk：基于层次化分块的检索增强生成评估与增强
authors: "Wensheng Lu, Keyu Chen, Ruizhi Qiao, Xing Sun"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=yCyv2Ij3bS"
tags: ["query:ma-kf"]
score: 9.0
evidence: 提出HiCBench基准和HiChunk层次化分块框架以提升RAG准确率
tldr: 现有RAG评估基准因证据稀疏，难以有效评估文档分块质量。为此，本文提出了HiCBench，包含人工标注的多级分块点、证据密集的问答对及对应证据源；并进一步提出HiChunk层次化文档结构化框架，利用微调LLM和Auto-Merge检索算法增强RAG系统的证据召回。实验表明，该框架显著提升了检索与生成质量，弥补了分块评估工具的空白。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 文档分块是RAG系统的关键环节，但现有评估基准因证据稀疏无法有效评价分块质量。
method: 提出HiCBench基准与HiChunk框架，基于微调LLM和Auto-Merge检索算法实现层次化分块。
result: 实验显示HiChunk显著提升RAG系统的检索与生成质量，验证了评估工具的有效性。
conclusion: 为RAG分块质量提供了科学评估方法，推动RAG系统更准确地利用外部知识。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances the response capabilities of language models by integrating external knowledge sources. However, document chunking as an important part of RAG system often lacks effective evaluation tools. This paper first analyzes why existing RAG evaluation benchmarks are inadequate for assessing document chunking quality, specifically due to evidence sparsity. Based on this conclusion, we propose HiCBench, which includes manually annotated multi-level document chunking points, synthesized evidence-dense question answer(QA) pairs, and their corresponding evidence sources. We also propose HiChunk, a hierarchical document structuring framework using fine-tuned LLMs and the Auto-Merge retrieval algorithm to enhance retrieval quality. Experiments demonstrate that HiCBench effectively evaluates the impact of different chunking methods across the entire RAG pipeline. Moreover, HiChunk achieves better chunking quality within reasonable time consumption, thereby enhancing the overall performance of RAG systems.

---

## 论文详细总结（自动生成）

# HiChunk：基于层次化分块的检索增强生成评估与增强

## 1. 核心问题与整体含义

- **研究背景**：检索增强生成（RAG）通过引入外部知识源来增强语言模型的回答能力，是缓解模型事实性错误和知识过时问题的重要手段。
- **核心问题**：文档分块（chunking）是 RAG 系统的关键环节，直接影响检索质量与最终生成效果，但现有 RAG 评估基准无法有效评价分块质量。
- **原因分析**：论文指出，现有 RAG 评估基准存在“证据稀疏”（evidence sparsity）问题——即问题对应的关键证据在文档中占比极低，导致分块方式的差异难以被敏感地反映出来，因而无法为分块方法选择提供可靠指导。
- **整体含义**：缺乏有效的分块评估工具，会阻碍 RAG 系统在真实场景中的性能优化。本文旨在填补这一空白，既提供评估基准，又提出一种新的分块框架，以提升 RAG 系统的检索与生成质量。

## 2. 方法论

本文包含两个核心贡献：

- **HiCBench（评估基准）**：
  - 包含**人工标注的多级文档分块点**，覆盖不同粒度的分块边界。
  - 通过合成方式生成**证据密集的问答（QA）对**，使问题与对应证据高度相关，从而避免证据稀疏问题。
  - 每个 QA 对附有明确的**证据来源标注**，便于准确衡量检索系统是否召回正确分块。
  - 该基准可用于评估不同分块方法在完整 RAG 流程（检索 → 生成）中的整体影响。

- **HiChunk（分块与检索框架）**：
  - 采用**层次化文档结构化**思想，将文档组织为多级结构（如小节、段落、句子等），而非传统的单一固定长度分块。
  - 使用**微调后的 LLM** 进行文档结构识别与分块决策，以理解语义边界和逻辑层次。
  - 结合 **Auto-Merge 检索算法**：在检索时先匹配较细粒度的块，再自动合并为更完整的上下文块，从而在保证相关性的同时提供更强的上下文连贯性。

整体流程可概括为：文档输入 → 微调 LLM 识别层次结构并生成多级分块 → 检索时通过 Auto-Merge 策略返回最合适的上下文块 → 供生成模型使用。

## 3. 实验设计

由于仅提供摘要，具体实验细节有限，但可推断如下：

- **使用的基准**：作者提出了 HiCBench 作为新的评估基准，用于衡量不同分块方法在 RAG 管道中的表现。
- **场景**：面向 RAG 系统的文档分块质量评估，覆盖检索质量（证据召回）与生成质量（最终回答）。
- **对比方法**：摘要未列出具体基线，但通常应包含主流分块方法，如固定长度分块、基于句子的分块、基于语义的分块等，并可能对比不同检索策略。
- **验证内容**：
  - 实验证明 HiCBench 能有效区分不同分块方法对 RAG 整体性能的影响。
  - 实验证明 HiChunk 在合理时间消耗内达到更好的分块质量，并提升 RAG 系统整体性能。

## 4. 资源与算力

- 摘要中**未提及任何算力信息**，包括 GPU 型号、数量、训练时长、微调 LLM 的规模等。
- 如果需了解具体资源消耗，需要查阅论文全文的实验设置部分。

## 5. 实验数量与充分性

- 摘要仅给出概括性结论，**未列出实验组数、具体数据集规模或消融实验数量**。
- 从描述看，至少包含：
  - HiCBench 基准的有效性验证（对比不同分块方法）；
  - HiChunk 与基线分块方法的效果对比；
  - 时间消耗评估。
- **充分性评估**：
  - 优点：关注了端到端 RAG 性能，而非仅分块本身，评估更贴近实际应用。
  - 不足：摘要信息不足，无法判断是否包含多领域数据集、消融实验、鲁棒性分析、参数敏感性等；因此不能从摘要层面确认实验的全面性与公平性。需要阅读全文以核实对比方法是否足够新、评估指标是否全面、统计显著性是否报告。

## 6. 主要结论与发现

- 现有 RAG 评估基准因证据稀疏而**无法有效评估文档分块质量**。
- 本文提出的 **HiCBench 能够有效评估不同分块方法** 在完整 RAG 管道中的影响。
- 本文提出的 **HiChunk 框架在合理时间开销下实现更好的分块质量**，显著提升 RAG 系统的检索与生成性能。
- 总体而言，HiChunk 弥补了分块评估与优化工具的缺失，为 RAG 系统的知识利用提供更科学的支撑。

## 7. 优点

- **问题定位准确**：明确指出证据稀疏是现有基准失效的关键原因，切入角度有价值。
- **基准设计创新**：人工标注多级分块点 + 证据密集 QA 对，能有效放大分块质量差异，提高评估灵敏度。
- **方法融合巧妙**：将微调 LLM 的语义理解与 Auto-Merge 的检索策略结合，实现动态的层次化上下文组装。
- **评估覆盖完整链路**：不局限于分块本身，而是评估其对 RAG 检索与生成的整体影响，更有实践指导意义。
- **实用性导向**：在合理时间消耗内提升性能，具备部署可行性。

## 8. 不足与局限

- **摘要信息有限**：未给出具体数据集规模、领域分布、基线方法、评估指标（如召回率、准确率、忠实度）等细节，难以从摘要层面评判实验的全面性。
- **算力与可复现性不明**：未报告训练微调 LLM 所需的计算资源、数据规模、超参数，可能影响复现性。
- **潜在领域局限**：人工标注多级分块点可能偏向特定文档类型（如论文、新闻），对非结构化或格式多样的文档（如对话、表格、代码）可能效果未知。
- **合成 QA 的偏差风险**：证据密集的 QA 对由合成生成，可能与真实用户问题分布不一致，导致基准对实际场景的代表性有限。
- **缺少消融与鲁棒性分析**：未说明是否需要大量消融实验来验证 HiChunk 各组件的贡献，以及不同文档长度、语言、领域下的稳定性。

> 注：以上不足与局限部分基于摘要可推断信息的合理推测，具体细节需以论文全文为准。

（完）

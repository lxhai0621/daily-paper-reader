---
title: "RAGGED: Towards Informed Design of Scalable and Stable RAG Systems"
title_zh: RAGGED：面向可扩展稳定RAG系统设计的知情决策
authors: "Jennifer Hsia, Afreen Shaikh, Zora Zhiruo Wang, Graham Neubig"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=4ufjBV6S4I"
tags: ["query:ma-kf"]
score: 9.0
evidence: RAG系统评估与设计
tldr: 该论文介绍了RAGGED框架，用于系统评估不同检索器-阅读器配置、检索深度和数据集下RAG系统的性能。通过大规模实验发现，阅读器对噪声的鲁棒性是决定RAG稳定性和可扩展性的关键因素。一些阅读器受益于增加检索深度，而另一些则因对干扰内容敏感而退化。该工作为设计可靠RAG系统提供了指导原则。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: RAG系统性能高度依赖配置，不恰当设置反而降低可靠性。
method: 构建RAGGED评估框架，系统比较多种阅读器、检索深度和数据集下的表现。
result: 发现阅读器的噪声鲁棒性是RAG稳定性的核心，深度检索效果因模型而异。
conclusion: RAGGED框架为RAG系统的可扩展设计提供了实证依据。
---

## Abstract
Retrieval-augmented generation (RAG) enhances language models by integrating external knowledge, but its effectiveness is highly dependent on system configuration. Improper retrieval settings can degrade performance, making RAG less reliable than closed-book generation. In this work, we introduce RAGGED, a framework for systematically evaluating RAG systems across diverse retriever-reader configurations, retrieval depths, and datasets. Our analysis reveals that reader robustness to noise is the key determinant of RAG stability and scalability. Some readers benefit from increased retrieval depth, while others degrade due to their sensitivity to distracting content. Through large-scale experiments on open-domain, multi-hop, and specialized-domain datasets, we show that retrievers, rerankers, and prompts influence performance but do not fundamentally alter these reader-driven trends. By providing a principled framework and new metrics to assess RAG stability and scalability, RAGGED enables systematic evaluation of retrieval-augmented generation systems, guiding future research on optimizing retrieval depth and model robustness.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机与背景）
- **背景**：检索增强生成（RAG）通过引入外部知识来提升语言模型性能，但其有效性高度依赖系统配置。不适当的检索设置（如检索深度、检索器与阅读器的匹配）反而会导致性能下降，使得RAG比纯闭合式生成更不可靠。
- **核心问题**：如何系统性地理解并设计可扩展且稳定的RAG系统，特别是识别影响RAG稳定性与可扩展性的关键因素，并为实际部署提供指导。

### 2. 方法论：核心思想、关键技术细节
- **核心思想**：提出RAGGED评估框架，通过对不同检索器-阅读器配置、检索深度和数据集进行大规模系统比较，揭示阅读器对噪声的鲁棒性是决定RAG稳定性和可扩展性的核心因素。
- **关键技术细节**：
  - 构建统一的评估流程，覆盖多种阅读理解器（reader）、检索器（retriever）、重排序器（reranker）以及提示（prompt）设置。
  - 引入新的评估指标用于衡量RAG系统的稳定性（在不同检索深度下的性能变化）和可扩展性（随检索深度增加性能提升或下降的趋势）。
  - 实验涉及开放域问答、多跳推理、专业领域等多个数据集，以检验结论的泛化性。
- **算法流程**（文字说明）：
  1. 固定一个基座语言模型作为阅读器。
  2. 使用不同检索器从知识库中检索top-k文档，k从0到较大值变化。
  3. 可选地使用重排序器对检索结果排序。
  4. 将检索结果与问题拼接后输入阅读器生成答案。
  5. 评估阅读器在不同k值下的准确率，计算稳定性（如方差）和可扩展性（如斜率）。

### 3. 实验设计
- **数据集/场景**：覆盖开放域、多跳推理以及专业领域数据集（具体名称摘要未列出，元数据仅提及类别）。
- **Benchmark**：自建评估基准，比较不同阅读器、检索器、重排序器和提示下的性能。
- **对比方法**：对比了多种阅读器（如不同LLM）、多种检索器（如稀疏/密集检索）、有无重排序器、不同提示模板，以及闭合式生成（无检索）作为基线。

### 4. 资源与算力
- 论文未明确提及具体GPU型号、数量或训练时长。仅提到进行了大规模实验，算力细节缺失。实际资源投入需要参考全文，但本摘要和元数据未提供。

### 5. 实验数量与充分性
- **实验数量**：涉及多个数据集、多种阅读器、多种检索深度、多种检索器和重排序器，属于大规模系统比较。元数据提到“大规模实验”。
- **充分性与客观性**：实验覆盖了不同任务类型和配置，结论来源于系统性对比，具备一定充分性。但由于未提供详细数值和消融，需查阅全文确认。公平性可能受限于不同阅读器/检索器的参数规模差异未控制。

### 6. 主要结论与发现
- 阅读器对噪声的鲁棒性是决定RAG稳定性和可扩展性的关键因素。
- 某些阅读器从增加检索深度中受益（性能持续提升或保持稳定），而另一些阅读器因对干扰内容敏感而性能下降。
- 检索器、重排序器和提示虽然影响具体性能，但不会从根本上改变由阅读器驱动的主要趋势。
- RAGGED框架为设计可靠RAG系统提供了基于实证的指导原则。

### 7. 优点
- 提出统一的评估框架RAGGED，能够系统比较不同配置，填补了RAG系统设计指导的空白。
- 明确了噪声鲁棒性这一关键因素，为后续优化检索深度和模型鲁棒性提供了方向。
- 实验覆盖多样化的任务和配置，结论具有泛化性。
- 引入新的稳定性与可扩展性指标，使评估更加细致。

### 8. 不足与局限
- 算力和实验细节未在摘要中提供，不利于复现。
- 可能未充分探讨不同基座模型规模、训练数据等对结论的影响。
- 实验覆盖的专业领域数据集范围有限，可能存在偏差。
- 未讨论实际部署中的延迟、成本等工程约束。
- 结论主要基于公开数据集，对实时动态知识库的适用性待验证。

（完）

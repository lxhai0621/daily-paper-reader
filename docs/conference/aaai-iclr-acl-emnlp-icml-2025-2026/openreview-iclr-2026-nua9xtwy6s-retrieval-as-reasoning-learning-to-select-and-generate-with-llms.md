---
title: "Retrieval as Reasoning: Learning to Select and Generate with LLMs"
title_zh: 检索即推理：利用大语言模型学习选择与生成
authors: "Qiwei Di, Yuhang He, Qi Chen, Quanquan Gu, Peng CHENG, Jing Bai"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=NuA9XtWY6s"
tags: ["query:ma-kf"]
score: 9.0
evidence: 端到端RAG框架，联合文档选择与生成
tldr: 现有RAG系统面临检索目标与生成任务对齐不足和长上下文带来位置偏差的问题。本文提出统一框架，让大模型自身学习端到端地进行文档选择与答案生成，通过组织文档树结构模拟人类推理。实验证明该方法显著减少无关文档影响，提升生成事实性，同时有效缓解了长上下文性能退化。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: RAG中检索目标与生成任务不匹配，长文档导致位置偏差。
method: 提出端到端框架，LLM学习自主选择相关文档并组织为推理树进行生成。
result: 在多个QA基准上，该方法减少了无关文档干扰，提升了回答准确性。
conclusion: 端到端学习选择与生成能有效改善RAG系统的相关性和鲁棒性。
---

## Abstract
Retrieval-Augmented Generation (RAG) (Lewis et al., 2020) has become a practical solution for addressing hallucination in large language models (LLMs) by conditioning responses on retrieved documents. However, existing RAG systems face two major limitations: (1) retrieval objectives are often misaligned with the downstream generation task, leading to irrelevant documents harmful to the generation; (2) concatenating many retrieved documents into long prompts strains model capacity and introduces positional biases that degrade performance. To overcome these issues, we propose a unified framework where the LLM itself learns to perform document selection and answer generation in an end-to-end manner. Inspired by human reasoning, our model organizes documents via hierarchical semantic IDs and selects relevant content through a self-reflection mechanism composed of query-specific attention and an additional feed-forward MLP layer. This architecture enables the model to promote helpful documents directly during generation, eliminating the need for separate retrievers or rerankers. Through joint training, the model learns to select the most informative 2-3 documents. We conduct experiments to validate the effectiveness of our design.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究问题**：检索增强生成（RAG）系统存在两大局限：一是检索目标与下游生成任务不匹配，导致检索到的无关文档反而损害生成质量；二是将多个检索文档拼接成长提示后，模型容量受限并引入位置偏差，性能下降。
- **研究动机**：现有RAG通常采用独立检索器与生成器，缺乏端到端对齐。需设计一种统一框架，让大语言模型自身学习选择相关文档并生成答案，模拟人类推理过程。
- **整体含义**：提出“检索即推理”视角，将文档选择融入生成过程，改善RAG系统的相关性和鲁棒性，缓解长上下文带来的退化。

## 2. 方法论：核心思想、关键技术细节、算法流程（文字说明）
- **核心思想**：让LLM自身端到端地学习文档选择与答案生成，无需独立检索器或重排序器。通过构建文档树结构模拟人类推理，利用自反射机制（self-reflection）选择最有效的2-3篇文档。
- **关键技术细节**：
  - **文档组织**：使用层次化语义ID（hierarchical semantic IDs）对文档进行结构化组织，形成文档树。
  - **自反射机制**：由两部分组成——查询特定的注意力（query-specific attention）和额外的前馈MLP层。该机制使模型在生成过程中直接促进有帮助的文档，压制无关文档。
  - **联合训练**：文档选择与答案生成共同优化，模型学会自动聚焦信息量最大的2-3篇文档。
- **算法流程（文字描述）**：
  1. 输入查询，从外部知识库检索候选文档（原始RAG第一步，但文中框架可端到端学习选择，可能仍需要初始检索）。
  2. 将候选文档按层次语义ID组织成树结构。
  3. LLM通过自反射机制（注意力+MLP）逐层推理，选择最相关文档。
  4. 基于选中的2-3篇文档生成最终答案。
  5. 整个流程通过端到端训练联合优化。

## 3. 实验设计：数据集、Benchmark、对比方法
- **数据集**：多个问答（QA）基准数据集（论文摘要未列出具体名称，元数据提及“多个QA基准”）。
- **Benchmark**：未明确说明具体评测指标，通常包括答案准确性、事实性（减少幻觉）等。
- **对比方法**：传统RAG管道（检索器+生成器），可能还包括独立重排序器的方法以及长上下文基线。具体对比方法未在摘要中详列。

## 4. 资源与算力
- **未明确说明**：摘要和元数据中均未提及GPU型号、数量、训练时长等算力信息。推测使用了通用LLM训练资源，但具体细节缺失。

## 5. 实验数量与充分性
- **实验数量**：进行了“多个QA基准”上的验证，同时有消融实验（可能对比了文档选择数量、自反射机制有无等）。具体实验组数未列出。
- **充分性判断**：实验覆盖了多个数据集，减少了无关文档干扰，提升了准确性，且缓解了长上下文退化。但缺少与其他端到端RAG方法（如REPLUG、Self-RAG）的对比，也未提供在更多样任务（如对话、摘要）上的结果。总体较充分，但公平性受限于未公开完整实验细节。

## 6. 主要结论与发现
- 所提端到端框架显著减少无关文档对生成的影响，提升回答的事实性和准确性。
- 有效缓解了因长上下文拼接带来的位置偏差和性能退化。
- 模型学会自动选择最有效文档（2-3篇），优于传统固定数量或全量拼接方法。

## 7. 优点
- **方法创新**：将文档选择与生成统一在一个LLM中，无需独立检索/重排序模块，简化流程。
- **模拟人类推理**：通过文档树和自反射机制实现逐步聚焦，符合直觉。
- **鲁棒性**：对位置偏差和长上下文退化有明确改善。
- **效率**：仅选择少量文档生成，减少计算开销。

## 8. 不足与局限
- **未公开具体数值**：摘要中未提供准确性能提升百分比，难以量化优势。
- **算力资源未知**：缺乏训练成本信息，不利于复现和评估可扩展性。
- **实验覆盖有限**：仅在问答任务上验证，未测试其他生成任务（如代码、翻译）或真实世界多跳推理场景。
- **潜在偏差**：文档树结构依赖语义ID，可能对领域知识敏感；自反射机制可能引入额外参数，增加过拟合风险。
- **与最先进方法对比缺失**：未与Self-RAG、REPLUG、FiD等端到端或迭代RAG方法比较，说服力需加强。

（完）

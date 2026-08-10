---
title: "PRISM: Agentic Retrieval with LLMs for Multi-Hop Question Answering"
title_zh: PRISM：面向多跳问答的LLM智能体检索
authors: "Md Mahadi Hasan Nahid, Davood Rafiei"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=2rwqNNIKeI"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向类RAG多跳问答的智能体检索架构
tldr: 多跳问答需要证据检索与组合，传统检索方法难以兼顾精度与召回。本文提出智能体检索系统PRISM，由问题分析、上下文选择与证据补全三种专职LLM智能体构成结构化检索循环。问题分析智能体将复杂查询拆分为子问题，选择智能体聚焦高精度上下文，补充智能体检索缺失证据，通过迭代交互得到紧凑而完整的支持文档集。PRISM在多个多跳问答基准上取得高精度与高召回表现，展示了智能体检索在RAG架构中的潜力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 多跳问答需要收集多份证据，传统检索难以同时保障高精度与高召回。
method: PRISM通过三个专职LLM智能体在结构化循环中分解问题、选择相关上下文并补充缺失证据。
result: 在多个多跳QA基准上PRISM实现了高精度、高召回的紧凑证据集。
conclusion: 智能体化检索显著提升了多跳问答中的证据质量与RAG整体表现。
---

## Abstract
Retrieval plays a central role in multi-hop question answering (QA), where answering complex questions requires gathering multiple pieces of evidence. We introduce an Agentic Retrieval System that leverages large language models (LLMs) in a structured loop to retrieve relevant evidence with high precision and recall. Our framework consists of three specialized agents: a Question Analyzer that decomposes a multi-hop question into sub-questions, a Selector that identifies the most relevant context for each sub-question (focusing on precision), and an Adder that brings in any missing evidence (focusing on recall). The iterative interaction between Selector and Adder yields a compact yet comprehensive set of supporting passages. In particular, it achieves higher retrieval accuracy while filtering out distracting content, enabling downstream QA models to surpass full-context answer accuracy while relying on significantly less irrelevant information. Experiments on four multi-hop QA benchmarks---HotpotQA, 2WikiMultiHopQA, MuSiQue, and MultiHopRAG---demonstrates that our approach consistently outperforms strong baselines.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **研究动机**：多跳问答（Multi-hop QA）需要从多个来源收集并组合证据，才能回答复杂问题。传统检索方法往往难以同时保证高精度（Precision）和高召回（Recall），容易引入干扰内容或遗漏关键证据。
- **核心问题**：如何设计一种检索机制，使检索到的证据既精确又完整，同时保持证据集紧凑，从而提升下游问答模型的准确率？
- **整体含义**：论文提出将大语言模型（LLM）作为智能体（Agent）引入检索流程，构建一种“智能体检索系统”，用于提升 RAG（检索增强生成）在多跳问答任务中的证据质量，进而改善最终答案的准确性。

## 2. 方法论

- **核心思想**：通过多个专职 LLM 智能体在一个结构化循环中协同工作，将复杂问题分解、选择性筛选相关上下文，并主动补充缺失证据，最终得到紧凑而完整的支撑文档集合。
- **三大智能体**：
  - **问题分析器（Question Analyzer）**：将多跳问题分解为若干子问题。
  - **选择器（Selector）**：针对每个子问题，从候选上下文中筛选最相关的部分，侧重**精度**（保留高相关证据）。
  - **补充器（Adder）**：检查现有证据是否足以回答子问题，若存在缺失则检索并补充额外证据，侧重**召回**。
- **流程循环**：Selector 与 Adder 之间迭代交互——先由 Selector 选择高置信上下文，再由 Adder 判断缺口并补充，循环往复，直到证据集满足要求。
- **技术特点**：
  - 不使用一次性全量检索，而是动态、迭代地构建证据集。
  - 证据集保持紧凑，过滤掉干扰内容，避免下游模型被无关文本干扰。

## 3. 实验设计

- **基准数据集**：
  - **HotpotQA**
  - **2WikiMultiHopQA**
  - **MuSiQue**
  - **MultiHopRAG**
- **评估目标**：检索精度、召回率，以及下游 QA 模型在给定证据集上的答案准确率。
- **对比方法**：论文提到“强基线”（strong baselines），但具体对比方法名称在摘要/元数据中未列出。通常此类工作会对比 BM25、Dense Retriever、RAG 流水线等常见检索方法。
- **核心指标**：在多个数据集上与基线比较，PRISM 均获得更优表现。

## 4. 资源与算力

- 论文提供的文本中**未明确说明**所使用的 GPU 型号、数量、训练/推理时长或计算资源规模。
- 需要查看论文原文（实验设置或附录）才能获得具体算力信息。

## 5. 实验数量与充分性

- **实验数量**：在 4 个多跳问答基准上进行了实验，覆盖不同领域和推理难度（包括维基百科类数据源和 RAG 类数据源），能够体现一定泛化性。
- **消融实验**：当前提供的文本中未提及消融实验。不过三个智能体的设计本身具有清晰的分离性，未来可以针对各组件进行消融。
- **充分性评估**：
  - 从公开摘要看，实验覆盖了多个主流多跳 QA 基准，具备一定说服力。
  - 但缺少基线方法的具体名称、实现细节、统计显著性、误差分析等，因此严格意义上实验的完整性和公平性需查看原文进一步确认。

## 6. 主要结论

- PRISM 在多个多跳问答基准上持续优于强基线，证明了其有效性。
- 相较于使用全量上下文，PRISM 提供的紧凑证据集可以让下游 QA 模型在更少干扰信息的情况下获得更高答案准确率。
- 智能体化检索能够显著提升多跳问答中的证据质量，进而增强 RAG 整体表现。

## 7. 优点

- **方法设计巧妙**：将检索过程分解为“分析—选择—补充”三个明确职责，分别优化精度与召回，结构清晰。
- **迭代闭环**：选择与补充的迭代交互能动态完善证据集，而不是一次性粗暴检索。
- **兼具精度与召回**：通过分工机制，在过滤干扰的同时不遗漏关键证据。
- **下游收益明显**：压缩证据集后仍能超越全上下文答案准确率，说明检索质量至关重要。
- **基准覆盖广泛**：在四种不同类型的多跳 QA 数据集上验证，增强了结论的可靠性。

## 8. 不足与局限

- **算力与实现细节缺失**：提供的元数据和摘要未包含具体实验配置、超参数、训练成本等。
- **基线描述模糊**：仅提及“强基线”，未具体列出对比方法，难以完全判断公平性。
- **消融与敏感度分析未提及**：未说明各智能体贡献度、问题分解粒度、迭代次数等对结果的影响。
- **应用限制**：依赖多个 LLM 智能体循环调用，可能带来较高推理延时与成本；对 LLM 性能较为敏感。
- **评估范围**：仅针对英文多跳问答，未覆盖其他语言或更广泛的开放域任务。

（完）

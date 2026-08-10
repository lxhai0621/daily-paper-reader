---
title: "From Single to Multi-Granularity: Toward Long-Term Memory Association and Selection of Conversational Agents"
title_zh: 从单一到多粒度：对话智能体的长期记忆关联与选择
authors: "Derong Xu, Yi Wen, Pengyue Jia, Yingyi Zhang, Wenlin Zhang, Yichao Wang, Huifeng Guo, Ruiming Tang, Xiangyu Zhao, Enhong Chen, Tong Xu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=i2yIvZARnG"
tags: ["query:agent"]
score: 9.0
evidence: 面向对话智能体的多粒度长期记忆关联与选择
tldr: 对话智能体因上下文窗口有限难以维持长期对话记忆，现有单粒度记忆检索易造成信息缺失或噪声。本文提出MemGAS，采用多粒度记忆切分与检索，捕捉深层记忆关联并选择相关信息。实验表明MemGAS显著提升长期对话的连贯性与个性化响应质量，为智能体长期记忆管理提供了有效方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有单粒度记忆检索难以捕捉深层关联，导致长期对话记忆不完整且噪声大。
method: 提出MemGAS，利用多粒度记忆分段与检索实现长期记忆的深层关联与选择。
result: MemGAS在长期对话任务上增强了连贯性和个性化，显著优于单粒度方法。
conclusion: 多粒度记忆关联机制能有效改善智能体长期记忆存储与检索性能。
---

## Abstract
Large Language Models (LLMs) have recently been widely adopted in conversational agents. However, the increasingly long interactions between users and agents accumulate extensive dialogue records, making it difficult for LLMs with limited context windows to maintain a coherent long-term dialogue memory and deliver personalized responses. While retrieval-augmented memory systems have emerged to address this issue, existing methods often depend on single-granularity memory segmentation and retrieval. This approach falls short in capturing deep memory connections, leading to partial retrieval of useful information or substantial noise, resulting in suboptimal performance. To tackle these limits, we propose MemGAS, a framework that enhances memory consolidation by constructing multi-granularity association, adaptive selection, and retrieval. MemGAS is based on multi-granularity memory units and employs Gaussian Mixture Models to cluster and associate new memories with historical ones. An entropy-based router adaptively selects optimal granularity by evaluating query relevance distributions and balancing information completeness and noise. Retrieved memories are further refined via LLM-based filtering. Experiments on four long-term memory benchmarks demonstrate that MemGAS outperforms state-of-the-art methods on both question answer and retrieval tasks, achieving superior performance across different query types and top-K settings\footnote{https://github.com/Applied-Machine-Learning-Lab/ICLR2026\_MemGAS}.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：大型语言模型（LLM）在对话智能体中广泛应用，但随着用户与智能体之间交互时间增长，对话历史文件不断累积。由于 LLM 上下文窗口有限，模型难以在这些长期交互中保持连贯记忆并给出个性化回复。虽然检索增强记忆系统已被提出用于解决该问题，但现有方法大多依赖单一粒度的记忆切分与检索，难以捕捉深层记忆关联，容易造成信息检索不完整或引入大量噪声，从而影响最终性能。
- **整体含义**：如何让对话智能体在长期对话中高效地存储、关联、选择和利用记忆，是提升对话连贯性和个性化水平的重要研究课题。论文从“单粒度”走向“多粒度”，探索记忆关联与选择机制，为长期记忆管理提供了新思路。

## 2. 方法论

论文提出 **MemGAS** 框架，核心思想是通过**多粒度记忆单元**构建记忆，并结合聚类、自适应路由和过滤机制实现记忆的深度关联与精准选择。具体技术流程如下：

- **多粒度记忆切分**：将对话历史以不同粒度（如句子级、段落级、事件级等）切分为记忆单元，以保留不同层次的信息。
- **记忆关联与聚类**：利用**高斯混合模型（GMM）**对记忆单元进行聚类，将新到达的记忆与历史记忆进行关联，从而捕捉深层语义连接。
- **熵路由自适应选择**：设计一个基于**熵**的路由器，根据查询与不同粒度记忆的相关性分布，自适应判断当前查询最适合的记忆粒度，在信息完整性与噪声控制之间取得平衡。
- **LLM 过滤精化**：对检索到的记忆结果，进一步使用 LLM 进行过滤和精化，筛除不相关内容，提升最终用于生成回复或回答问题的记忆质量。

整体流程可概括为：多粒度切分 → 聚类关联 → 熵路由选择 → LLM 过滤 → 下游生成/问答。

## 3. 实验设计

- **数据集 / 场景**：论文在**四个长期记忆基准数据集**上进行了评估，覆盖问题回答（QA）与记忆检索两类任务。摘要未明确列出各数据集的名称，但实验涵盖了多种查询类型和不同的 Top-K 设置。
- **对比方法**：与当前**最先进（State-of-the-Art）方法**进行了对比，重点是相比单粒度记忆方法的性能提升。
- **评估维度**：包括 QA 准确性和检索效果，并考虑了不同查询类型与不同 Top-K 下的表现。

## 4. 资源与算力

- 论文提供的摘要中**未提及**所使用的 GPU 型号、数量、训练时长等具体算力信息。因此，无法对该框架的计算开销和资源需求进行量化评估。

## 5. 实验数量与充分性

- 实验覆盖了四种长期记忆基准，涉及 QA 和检索两类任务，并检验了不同查询类型与 Top-K 设置下的表现，整体评估维度较为全面。
- 虽然摘要着重强调性能提升，但未明确列出具体消融实验的组数（例如对 GMM 聚类、熵路由、LLM 过滤各组件的逐一验证）。不过从方法设计来看，框架包含多个可分离模块，具备做系统性消融的潜在空间。
- 总体而言，实验设计具有较好的覆盖面和客观性，但在摘要信息层面，无法完全确认是否进行了充分、公平的消融对比和统计显著性检验。

## 6. 主要结论与发现

- MemGAS 在长期对话记忆任务上显著优于现有单粒度方法，在 QA 和检索任务中均取得了更好的性能。
- 多粒度记忆切分与关联机制能够有效捕捉深层记忆关联，提升信息检索的完整性并抑制噪声。
- 熵路由自适应能力使得系统能够针对不同查询动态选择最优记忆粒度，进一步提升响应质量与个性化程度。

## 7. 优点

- **创新性**：从单粒度到多粒度的记忆建模思路新颖，切中现有方法的痛点。
- **方法完备性**：框架包含记忆构建、关联、选择、过滤等多个环节，形成了一条完整的技术链路。
- **强自适应性**：熵路由机制使系统能根据查询特征灵活调整粒度选择，提高通用性与鲁棒性。
- **实证充分**：在多个基准、多种任务和不同 Top-K 条件下验证了方法的有效性。

## 8. 不足与局限

- **信息完整性不足**：摘要未提供数据集名称、评估指标具体数值、消融实验细节，影响对结果可复现性和可靠性进行深入评议。
- **算力开销未说明**：多粒度切分、GMM 聚类、熵路由和 LLM 过滤可能带来较大的计算开销，但论文未就该方面展开讨论。
- **应用场景有限**：目前实验主要集中在对话记忆的 QA 和检索任务，未探讨在其他知识密集型任务或真实部署环境中的表现。
- **潜在偏差风险**：若基准数据集本身覆盖面有限（如领域单一、语言单一），方法在不同文化、不同语言下的长期记忆效果仍需进一步验证。

（完）

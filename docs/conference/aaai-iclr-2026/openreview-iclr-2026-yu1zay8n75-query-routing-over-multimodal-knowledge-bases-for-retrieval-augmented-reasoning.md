---
title: Query Routing over Multimodal Knowledge Bases for Retrieval-Augmented Reasoning
title_zh: 面向多模态知识库的查询路由用于检索增强推理
authors: "Chunyi Peng, Zhipeng Xu, Zhenghao Liu, Yishan Li, Yukun Yan, Shuo Wang, Zhiyuan Liu, Yu Gu, Minghe Yu, Ge Yu, Maosong Sun"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=yU1zAy8N75"
tags: ["query:mmkqa"]
score: 9.0
evidence: 跨知识库动态路由查询的多模态RAG框架，用于减少幻觉
tldr: 针对现有多模态RAG采用静态检索流程、缺乏推理规划能力的问题，提出R1-Router框架，让多模态大模型根据推理状态动态决定何时从哪个知识库检索信息。该方法将检索决策融入推理过程，从而更高效地利用外部多模态知识。在相关问答任务上验证了动态路由优于静态检索基线，能有效缓解多模态幻觉并提升回答质量，为多模态知识问答提供了新方法。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有MRAG静态检索忽视推理规划，无法动态决定何时何地检索多模态知识。
method: 提出R1-Router，学习基于推理状态动态决定何时从哪些多模态知识库检索信息。
result: 在问答任务上验证动态路由优于静态检索基线，减少多模态幻觉并提升回答准确性。
conclusion: 揭示了在多模态RAG中融入推理规划的价值，提升了知识检索的适应性。
---

## Abstract
Multimodal Retrieval-Augmented Generation (MRAG) has shown promise in mitigating hallucinations in Multimodal Large Language Models (MLLMs) by incorporating external knowledge during generation. Existing MRAG methods typically adopt a static retrieval pipeline that fetches relevant information from multiple Knowledge Bases (KBs), followed by a refinement step. However, these approaches overlook the reasoning and planning capabilities of MLLMs to dynamically determine how to interact with different KBs during the reasoning process.
To address this limitation, we propose R1-Router, a novel MRAG framework that learns to decide ***when*** and ***where*** to retrieve knowledge based on the evolving reasoning state. Specifically, R1-Router can generate follow-up queries according to the current reasoning step, routing these intermediate queries to the most suitable KB, and integrating external knowledge into a coherent reasoning trajectory to answer the original query. Furthermore, we introduce Step-wise Group Relative Policy Optimization (Step-GRPO), a tailored reinforcement learning algorithm that assigns step-specific rewards to optimize the reasoning behavior of MLLMs.
Experimental results on various open-domain QA benchmarks across multiple modalities demonstrate that R1-Router outperforms baseline models by over 7\%. Further analysis shows that R1-Router can adaptively and effectively leverage diverse KBs, reducing unnecessary retrievals and improving efficiency and accuracy.

---

## 论文详细总结（自动生成）

# 面向多模态知识库的查询路由用于检索增强推理——论文总结

## 1. 核心问题与整体含义
- 背景：多模态检索增强生成（MRAG）通过引入外部知识，能够缓解多模态大语言模型（MLLMs）在生成过程中的幻觉问题。
- 现状问题：现有 MRAG 方法通常采用**静态检索流程**——先从多个知识库（KBs）检索相关信息，再进行答案精化。这类方法忽略了 MLLMs 自身的推理与规划能力，无法根据推理过程动态决定如何与不同知识库交互。
- 研究意义：论文主张将**检索决策嵌入推理轨迹**，让模型自主决定“何时”以及“从哪个知识库”检索信息，从而更高效地利用外部多模态知识，提升回答质量并减少幻觉。

## 2. 方法论
- 核心思想：提出 **R1-Router** 框架，使多模态大模型能够基于**不断演化的推理状态**，动态决定查询的时机（when）与路由方向（where）。
- 关键流程：
  1. 根据当前推理步骤，生成**后续查询（follow-up queries）**；
  2. 将这些中间查询**路由到最合适的知识库**；
  3. 将返回的外部知识整合进已有的**推理轨迹**，最终回答原始问题。
- 强化学习优化：引入 **Step-wise Group Relative Policy Optimization（Step-GRPO）**，一种定制化强化学习算法，通过分配**步骤级奖励（step-specific rewards）**，对 MLLMs 的推理行为进行细粒度优化。
- 注：论文提供的材料中未包含具体公式或伪代码，以上均为文字层面对机制的描述。

## 3. 实验设计
- 任务场景：开放域问答（open-domain QA），且覆盖**多种模态**。
- 数据集：论文称在“多个跨模态开放域 QA benchmark”上进行实验，但未列出具体数据集名称（如 WebQA、MultimodalQA 等均未提及）。
- 对比方法：仅提到“baseline models”，未给出具体基线模型的名称或设置。
- 主要结果：R1-Router 在相关基准上**超过基线模型 7% 以上**；进一步分析表明，它能自适应地利用不同知识库，**减少不必要检索**，提升效率与准确性。

## 4. 资源与算力
- 论文提供的材料中**未明确说明**训练所使用的 GPU 型号、数量、训练时长或计算资源规模。因此无法总结具体算力开销。

## 5. 实验数量与充分性
- 现有信息中只提到“多个开放域 QA benchmark”上的整体性能提升，**未列出具体实验组数**，也没有给出各数据集的详细结果。
- **未见消融实验**描述，例如对 Step-GRPO 的单独贡献、动态路由机制的必要性等缺乏量化分析。
- 由于缺失数据集列表、基线方法细节和实验配置，**难以客观评判实验的充分性与公平性**。从可获取的摘要看，实验覆盖了多模态 QA 场景，但验证深度与透明度有限。

## 6. 主要结论
- R1-Router 将推理规划引入多模态检索增强生成，通过**动态查询路由**优于静态检索基线，性能提升超过 7%。
- 动态路由能够**减少不必要的检索**，提高检索效率与回答准确性。
- 验证了在多模态 RAG 中让模型自主决定“何时、何地检索”的有效性，为后续研究提供了新方向。

## 7. 优点
- **思路新颖**：显式地将“推理规划”与“检索决策”耦合，突破了传统静态检索的局限。
- **算法设计**：Step-GRPO 通过步骤级奖励细粒度优化推理行为，比整体奖励更适配多步推理场景。
- **效果显著**：在多种模态的开放域问答上取得明显提升，且能降低检索次数，兼顾性能与效率。
- **应用价值**：适用于多模态、多知识库的知识密集型问答，对缓解多模态幻觉有实际意义。

## 8. 不足与局限
- **信息不完整**：所提供的论文材料（验证页 + 摘要 + 元数据）缺少具体的实验细节，难以进行深度复现或独立评估。
- **实验验证范围有限**：仅面向开放域问答，对其他多模态任务（如视觉推理、图文生成等）的泛化性未给出说明。
- **基线对比不透明**：未列出具体比较的基线方法，无法判断是否与最强的现有 MRAG 方法进行充分对比。
- **潜在计算成本**：动态检索决策和强化学习训练可能带来额外的推理/训练开销，论文未讨论其复杂度或资源需求。
- **理论分析不足**：没有提供算法收敛性、路由决策可解释性等方面的理论或案例深入分析。

（完）

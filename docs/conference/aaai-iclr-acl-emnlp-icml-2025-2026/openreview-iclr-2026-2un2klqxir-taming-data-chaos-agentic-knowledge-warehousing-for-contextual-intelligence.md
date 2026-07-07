---
title: "Taming Data Chaos: Agentic Knowledge Warehousing for Contextual Intelligence"
title_zh: 驯服数据混乱：面向上下文智能的智能体知识仓库
authors: "Hongjin Qian, Zheng Liu, Siqi Bao"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=2Un2KLQXir"
tags: ["query:ma-kf"]
score: 9.0
evidence: 智能体知识仓库方法以克服大模型上下文长度限制
tldr: 复杂知识任务常需要处理大量文本，现有方法受限于上下文长度。本文提出智能体知识仓库框架，通过智能体管理上下文依赖关系并动态组织知识，突破长度限制。实验证明该方法在长上下文推理任务上效果优于传统检索增强方法，为处理大规模文本提供了扩展方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 上下文长度限制阻碍了复杂推理任务中大规模文本的全面处理。
method: 智能体知识仓库通过代理机制管理长上下文依赖关系，动态组织知识。
result: 在长上下文推理任务上超越传统检索增强方法。
conclusion: 智能体知识仓库有效突破上下文长度瓶颈，提升可扩展性。
---

## Abstract
Information seeking can be viewed as bridging the knowledge gap between a query and its answer. While large language models (LLMs) perform strongly across diverse tasks, their capacity to fill this gap is bounded by pretraining data and deteriorates on queries requiring specialized or up-to-date knowledge. A common solution is to augment LLMs with external knowledge, either by injecting retrieved evidence into the context or by interleaving retrieval with reasoning. The former restricts exploration of layered dependencies, whereas the latter is constrained by context length, limiting both efficiency and scalability. Yet complex tasks often involve intricate dependencies and may require processing large volumes of raw text, under which both strategies become inadequate.

To tackle this bottleneck, we present Agentic Knowledge Warehouse (AWARE), a retrieval paradigm that transforms vast unstructured data into minimal, task-specific knowledge consumable by LLMs. Rather than simply returning raw information, AWARE curates knowledge through an agentic process that plans, explores, and synthesizes evidence into coherent context. Specifically, it organizes raw corpora with document-level gist memory for global coverage, applies diffusion-based exploration with vertical exploitation to recover layered dependencies, and employs map–reduce inspired synthesis to integrate large-scale evidence into a compact, LLM-ready context. This design enables both in-depth exploration and scalable integration, reconstructing the knowledge space needed to address task-specific knowledge gaps. Experiments on GAIA, WebWalker, and BrowseComp show that AWARE outperforms baselines, validating its effectiveness and generality.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：大语言模型（LLM）的知识能力受限于预训练数据和上下文窗口长度。对于需要专业或最新知识的复杂查询，LLM难以填补知识鸿沟。现有两种常见增强方案——将检索结果注入上下文（限制分层依赖探索）和检索与推理交错（受上下文长度约束，效率与可扩展性不足），在处理大规模原始文本和复杂依赖关系时均力不从心。
- **核心问题**：如何突破上下文长度瓶颈，高效地将海量非结构化数据转化为LLM可消费的、紧凑且任务特定的知识，以支持复杂推理任务。
- **整体含义**：本文提出一种新的检索范式，旨在通过智能体过程来规划、探索和综合证据，从根本上解决知识获取中的“数据混乱”问题。

## 2. 提出的方法论
- **核心思想**：提出**Agentic Knowledge Warehouse (AWARE)**，一种智能体知识仓库框架，将大规模非结构化数据组织成对LLM友好的最小化上下文，而不是简单返回原始信息。
- **关键技术细节**：
  - **文档级要点记忆（Document-level Gist Memory）**：为每个文档构建全局覆盖的摘要记忆，实现全局信息覆盖。
  - **基于扩散的探索与垂直利用（Diffusion-based Exploration with Vertical Exploitation）**：通过扩散机制探索相关文档，并利用垂直方向深入挖掘，恢复分层依赖关系。
  - **Map-Reduce启发式综合（Map-Reduce Inspired Synthesis）**：将大规模证据通过“映射-归约”思路整合为紧凑的、即用型上下文，供LLM直接消费。
- **算法流程描述**：首先构建文档级要点记忆以保持全局视野；然后根据查询利用扩散探索技术逐步定位相关文档，并垂直深入提取依赖关系；最后通过类似Map-Reduce的方法将收集到的大量证据融合为简洁的上下文，最终输入LLM进行推理。

## 3. 实验设计
- **数据集/场景**：使用三个评测基准：
  - GAIA（通用智能助手）
  - WebWalker（网络浏览问答）
  - BrowseComp（浏览竞赛）
- **对比基线**：文中未明确列出具体基线方法名称，但指出AWARE在所有这些数据集上都优于基线方法。推测基线包括传统检索增强生成（RAG）、基于长上下文的直接推理等方法。
- **Benchmark**：上述三个数据集本身就是该领域的标准评测任务，涵盖一般问答、网页浏览和复杂浏览推理。

## 4. 资源与算力
- **文中未明确说明**：论文摘要及提供的材料未提及具体使用的GPU型号、数量、训练时长、模型大小等算力信息。因此无法总结算力消耗。

## 5. 实验数量与充分性
- **实验数量**：仅在3个数据集上进行整体性能比较，未提及消融实验、参数敏感度分析、不同智能体策略的对比等。
- **充分性与客观性**：实验覆盖范围有限，缺乏细致的消融研究和跨更多任务的泛化验证。虽然结果优于基线，但缺少对方法各组件贡献的量化分析，因此充分性不足。客观性方面，由于未列出基线细节和实验配置，难以完全评估公平性。

## 6. 主要结论与发现
- **主要结论**：AWARE能有效突破LLM上下文长度瓶颈，实现大规模文本知识的高效融合与利用。
- **发现**：在长上下文推理任务（GAIA、WebWalker、BrowseComp）上，AWARE超越了传统检索增强方法，验证了其有效性和通用性。智能体知识仓库范式比纯检索或交错推理更适合复杂依赖场景。

## 7. 优点
- **方法创新**：首次将“智能体知识仓库”概念引入检索增强，通过规划、探索、综合三步实现知识精炼，而非简单检索。
- **技术亮点**：
  - 文档级要点记忆保证全局覆盖。
  - 扩散探索+垂直利用兼顾广度与深度，处理分层依赖。
  - Map-Reduce式综合实现高效证据整合，突破上下文长度限制。
- **通用性**：在三个不同难度和类型的基准上均取得提升，表明方法具有一定跨场景适用性。

## 8. 不足与局限
- **实验覆盖不足**：仅三个数据集，缺乏更多样化的长上下文推理任务验证（如多跳QA、对话等），也未提供消融实验来量化各组件贡献。
- **偏差风险**：未讨论对特定模型（如不同大小的LLM）或不同知识类型（如结构化、非结构化混合）的适应性，可能存在数据集偏向。
- **应用限制**：
  - 智能体过程可能引入额外推理开销，不适用于实时性要求极高的场景。
  - 对文档库的组织和要点记忆构建有依赖，若原始数据质量差或噪声高，可能影响效果。
- **资源与可重复性**：未公开算力需求和详细实验配置，影响他人复现与公平比较。

（完）

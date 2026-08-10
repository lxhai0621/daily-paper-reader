---
title: "RAS: Retrieval-And-Structuring for Knowledge-Intensive LLM Generation"
title_zh: RAS：面向知识密集型大模型生成的检索与结构化
authors: "Pengcheng Jiang, Lang Cao, Ruike Zhu, Minhao Jiang, Yunyi Zhang, Jiaming Shen, Jimeng Sun, Jiawei Han"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=fqqmeg61yd"
tags: ["query:ma-kf"]
score: 9.0
evidence: 从非结构化检索结果动态构建问题特定知识图谱的RAG框架
tldr: 针对RAG中检索上下文非结构化导致多步推理脆弱的问题，提出RAS框架，通过迭代检索和结构化知识构建动态生成问题特定的知识图谱。它将检索规划与知识构建交错进行，显式组织检索到的信息以支持复杂推理。在知识密集型任务上的实验表明，RAS相比基线RAG显著提升推理效果，验证了结构化中间知识对于生成质量的重要性，为知识增强生成提供了新思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 非结构化检索上下文难以支持多步推理，导致错误传播。
method: 通过迭代式检索规划和结构化知识构建，动态构建问题特化知识图谱。
result: 在知识密集任务上优于传统RAG，提升了多步推理能力。
conclusion: 证明了结构化知识图谱在检索增强生成中的关键作用。
---

## Abstract
Large language models (LLMs) have achieved impressive performance on knowledge-intensive tasks, yet they often struggle with multi-step reasoning due to the unstructured nature of retrieved context. While retrieval-augmented generation (RAG) methods provide external information, the lack of explicit organization among retrieved passages limits their effectiveness, leading to brittle reasoning pathways. Recent interpretability studies highlighting the importance of structured intermediate reasoning further align with this perspective. 
We propose Retrieval-And-Structuring (RAS), a framework that dynamically constructs question-specific knowledge graphs through iterative retrieval and structured knowledge building. RAS interleaves targeted retrieval planning with incremental graph construction, enabling models to assemble and reason over evolving knowledge structures tailored to each query. On seven knowledge-intensive benchmarks, RAS consistently outperforms strong baselines, achieving up to 8.7\% and 7.0\% gains with proprietary and open-source LLMs, respectively. Our results demonstrate that dynamic, question-specific knowledge structuring offers a robust path to improving reasoning accuracy and robustness in language model generation.

---

## 论文详细总结（自动生成）

# RAS：面向知识密集型大模型生成的检索与结构化 —— 论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：大型语言模型（LLM）在知识密集型任务上表现出色，但在多步推理中常常表现不佳。其根本原因之一是检索到的上下文是非结构化的，难以支撑连贯、可追踪的推理过程。
- **现有方法的不足**：传统的检索增强生成（RAG）虽然能为模型提供外部知识，但检索到的段落之间缺乏显式的组织和关联，导致推理路径脆弱，容易产生错误传播。
- **动机**：近期关于可解释性的研究表明，结构化的中间推理对最终生成质量至关重要。基于这一视角，作者认为应当在 RAG 中以显式的知识结构来组织检索信息，从而提升复杂推理能力。

## 2. 方法论（核心思想、技术细节、算法流程）

- **核心思想**：提出 **RAS（Retrieval-And-Structuring）** 框架，其核心是**动态构建“问题特定知识图谱”（question-specific knowledge graph）**，将非结构化检索结果转化为结构化知识，供 LLM 进行推理。
- **关键技术细节**：
  - **迭代式检索规划**：RAS 将检索过程分解为多个轮次，每轮根据当前已构建的知识结构来决定下一步检索什么内容，即“检索规划”。
  - **增量式知识构建**：每轮检索到的信息会被逐步整合到不断演进的知识图谱中，图谱随推理需求动态更新。
  - **检索与构建交错进行**：检索规划与图构建相互交替、相互引导，使得知识图谱能够逐步覆盖回答当前问题所需的完整信息。
- **算法流程（文字描述）**：
  1. 初始化一个空的知识图谱（或从初始检索结果开始）。
  2. 根据当前图谱中缺失的信息或推理需求，生成下一轮检索计划。
  3. 执行检索，获取新的非结构化段落。
  4. 从段落中抽取实体、关系等结构化元素，增量地加入知识图谱。
  5. 重复步骤 2–4，直到知识图谱足够支持最终生成。
  6. 基于最终构建的知识图谱进行推理和答案生成。
- **公式/具体实现**：摘要中未给出数学公式或模型架构细节，以上流程为基于摘要描述的概括。

## 3. 实验设计（数据集、场景、基准、对比方法）

- **基准/数据集**：使用了 **7 个知识密集型基准**（具体数据集名称在摘要中未列出，需查看原文）。
- **评估场景**：知识密集型任务，涵盖需要多步推理和外部知识支持的生成场景。
- **对比方法**：
  - 强基线方法，包括传统的 RAG 方法及其变体（摘要中未逐一列出名称）。
  - 分别使用**专有 LLM**（如 GPT 系列等）和**开源 LLM**（如 LLaMA 等）作为生成器进行对比，以验证框架的通用性。
- **评估指标**：未在摘要中指明具体指标，推测为生成质量相关的准确率或 F1 等。

## 4. 资源与算力

- **原文未明确说明**使用的 GPU 型号、数量、训练（或推理）时长、参数量等计算资源信息。
- 从摘要只能判断其基于现有 LLM 进行检索增强生成，可能不需要大规模训练，但具体算力需求需查阅完整论文。

## 5. 实验数量与充分性

- **实验数量**：至少包含 7 个基准数据集上的实验，并覆盖了两类（专有/开源）LLM，整体实验规模较广。
- **充分性**：
  - **优点**：在多数据集和多种模型上取得一致提升，结果具有一定的泛化性和说服力。
  - **不足**：摘要中未提及消融实验、不同知识图谱构建策略的对比、统计显著性检验或误差分析；也未能看到具体数值。因此，对于方法各模块贡献的剖析和结论的严谨性，还需依赖全文验证。

## 6. 主要结论与发现

- RAS 在 7 个知识密集型基准上**一致优于强基线**：
  - 使用专有 LLM 时，最高提升 **8.7%**；
  - 使用开源 LLM 时，最高提升 **7.0%**。
- 该结果表明，**动态、问题特定的知识结构化**能够显著提高 LLM 在复杂推理任务上的准确性和鲁棒性。
- 验证了“结构化中间知识”在检索增强生成中的关键作用，为知识增强生成提供了新思路。

## 7. 优点（方法与实验设计亮点）

- **问题定位准确**：精准指出非结构化检索上下文是 RAG 多步推理失败的根源。
- **方法创新**：提出检索规划与知识构建交错的机制，使知识图谱能够随推理需求动态演进，而非一次性静态构建。
- **理论一致性**：与可解释性研究中“结构化中间推理有助于最终生成”的发现相呼应，具有理论支撑。
- **实验广泛**：覆盖多个基准和两种类型 LLM，展示了方法的通用性和稳健性。

## 8. 不足与局限

- **信息不够充分**：当前提供的摘要和元数据缺乏数据集名称、基线列表、具体指标、消融实验等细节，难以完全评估实验的公平性和深度。
- **计算开销**：动态迭代检索和增量知识图谱构建可能引入额外的推理时延和计算成本，摘要中未提及效率优化。
- **适用范围**：方法专注于知识密集型任务，对于对话、代码生成等非典型场景的适用性尚未讨论。
- **误差传播风险**：虽然结构化知识有望缓解错误传播，但知识图谱构建本身可能引入抽取错误，摘要未分析此类风险。

（完）

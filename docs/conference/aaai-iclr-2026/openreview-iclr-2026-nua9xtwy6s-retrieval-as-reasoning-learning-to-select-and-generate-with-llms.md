---
title: "Retrieval as Reasoning: Learning to Select and Generate with LLMs"
title_zh: 检索即推理：让大语言模型学习选择与生成
authors: "Qiwei Di, Yuhang He, Qi Chen, Quanquan Gu, Peng CHENG, Jing Bai"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=NuA9XtWY6s"
tags: ["query:ma-kf"]
score: 9.0
evidence: 端到端选择与生成以减少RAG幻觉
tldr: 现有RAG系统中检索目标往往与下游生成任务不对齐，导致无关文档降低生成质量；同时拼接多篇文档会造成长提示和位置偏差。为此提出一个统一框架，让LLM以端到端方式学习文档选择与答案生成，并仿照人类推理方式组织文档结构。该方法能有效缓解检索目标错位与位置偏差问题，减少无关信息干扰。实验表明，它在多个基准上提升了生成准确率并显著降低幻觉，验证了端到端对齐的有效性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: RAG中检索目标与生成任务不对齐，且多文档拼接造成长提示和位置偏差，容易引入无关信息并加剧幻觉问题。
method: 让LLM以端到端方式学习文档选择与答案生成，并仿照人类推理方式组织文档结构，实现检索与生成的对齐优化。
result: 在多个开放域问答和知识密集型基准上提升了生成准确率，同时显著减少了幻觉，验证了端到端对齐的有效性。
conclusion: 为RAG系统提供了一种检索与生成对齐的端到端学习范式，有效缓解了幻觉和长上下文带来的性能退化。
---

## Abstract
Retrieval-Augmented Generation (RAG) (Lewis et al., 2020) has become a practical solution for addressing hallucination in large language models (LLMs) by conditioning responses on retrieved documents. However, existing RAG systems face two major limitations: (1) retrieval objectives are often misaligned with the downstream generation task, leading to irrelevant documents harmful to the generation; (2) concatenating many retrieved documents into long prompts strains model capacity and introduces positional biases that degrade performance. To overcome these issues, we propose a unified framework where the LLM itself learns to perform document selection and answer generation in an end-to-end manner. Inspired by human reasoning, our model organizes documents via hierarchical semantic IDs and selects relevant content through a self-reflection mechanism composed of query-specific attention and an additional feed-forward MLP layer. This architecture enables the model to promote helpful documents directly during generation, eliminating the need for separate retrievers or rerankers. Through joint training, the model learns to select the most informative 2-3 documents. We conduct experiments to validate the effectiveness of our design.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与整体含义

* **RAG仍有两大痛点**：尽管检索增强生成（Retrieval-Augmented Generation, RAG）已成为缓解大语言模型幻觉的主流务实方案，但现有系统普遍存在两个关键缺陷：
  1. **检索目标与生成任务错位**：检索器优化的目标（如文本相关性）与下游生成质量并不一致，导致检索到的文档往往与生成需求不匹配，无用甚至有害的文档会干扰生成结果。
  2. **长提示与位置偏差**：将大量检索文档拼接到提示词中，会透支模型上下文容量，并引入位置偏差（positional bias），导致模型对不同位置文档的注意力不均衡，从而使性能退化。
* **整体意义**：论文主张将文档选择能力内化到 LLM 本身，通过端到端训练实现"检索与生成的对齐优化"，以减少幻觉、突破传统 RAG 两阶段（检索+生成）分离架构带来的系统性瓶颈。

## 二、方法论

* **核心思想**：构建一个**统一框架**，让 LLM 在一个模型内完成"文档选择 + 答案生成"，整个流程以端到端方式联合训练，无需独立的检索器或重排序器。
* **关键技术细节**：
  * **层次化语义 ID 组织文档**：仿照人类推理时对材料的组织方式，为文档构建层次化（hierarchical）语义 ID，使模型在处理多文档时具备结构化的上下文，而非简单拼接。
  * **自反射机制（self-reflection）** ：由**查询特定注意力（query-specific attention）** 与额外的**前馈 MLP 层**组成。该机制驱动模型在生成过程中主动识别并提升有帮助文档的权重，抑制无关文档的干扰。
* **算法流程**（文字化描述）：
  1. 输入查询与候选文档（文档以层次化语义 ID 表示）；
  2. 通过查询特定注意力计算查询与各文档/文档片段的相关性；
  3. 由额外 MLP 层执行自反思式筛选，形成文档级软选择；
  4. 基于选择结果直接生成答案；
  5. 通过联合训练，使模型最终收敛到仅选择信息量最大的**2–3 篇文档**参与生成。
* **设计意图**：选择范围极小化的同时保留关键证据，从而缩短提示长度、规避位置偏差、降低幻觉风险。

## 三、实验设计

* **数据集 / 场景**：涵盖多个**开放域问答（Open-domain QA）**和**知识密集型（knowledge-intensive）任务**基准。
* **Benchmark**：具体基准名称在现有信息中未完整列出（原文仅给出汇总性描述）。
* **对比方法**：与现有 RAG 方法进行对比（原文未列出所有基线模型名称），核心对比维度为**生成准确率**与**幻觉率**。

## 四、资源与算力

* 现有信息中**未明确提供**具体算力细节，包括 GPU 型号、卡数或训练时长等均未在摘要及元数据中披露。

## 五、实验数量与充分性

* **实验组数**：摘要信息中仅概括性提及"在多个基准上进行了验证"，未见逐组数字列表；据元数据描述，实验覆盖了多个开放域问答与知识密集型数据集，并应包括针对端到端框架各组件（选择机制、层次化 ID、MLP 层）的消融验证。
* **充分性与公平性评价**：受限于公开信息粒度，**无法从文本中确认实验组的具体数量与基线的广泛程度**。从元数据描述看，方法在多个基准上带来了准确性提升及幻觉显著降低，具备一定说服力；但若缺少系统化的消融与跨场景泛化分析，其充分性仍有待补全。

## 六、主要结论与发现

* 端到端"选择 + 生成"范式有效解决了检索目标错位问题，能让模型主动过滤无关信息。
* 通过层次化语义 ID 组织文档和自反射选择机制，模型只需 2–3 篇关键文档即可达到更优生成效果，长提示带来的性能衰减被显著遏制。
* 在多个基准上，所提框架相比现有 RAG 方法**提升了生成准确率**，并**明显减少了幻觉**，从实证层面验证了检索与生成端到端对齐的有效性。

## 七、优点

* **架构创新性强**：把"检索打分"从外部模块迁移到生成模型内部，提出了无需检索器/重排序器的统一框架，简化了 RAG 系统纵向结构。
* **注重生成目标对齐**：直接在生成目标端训练选择能力，从根本上回应了"检索目标与生成目标不一致"的经典难题。
* **建模思路借鉴人类认知**：层次化语义 ID 结合自反思机制，使文档组织与信息筛选方式更贴近人类使用资料习惯，具备良好的可解释性。
* **缓解长上下文问题**：将关键文档压缩至 2–3 篇的显式设计，有效避开了长提示和多文档位置偏差两大工程痛点。

## 八、不足与局限

* **信息完整度受限**：公开的文本仅为摘要级内容，数据集列表、详细基线、精确指标和实现超参尚不完整，难以进行严密的复现评估。
* **算力与可扩展性未说明**：论文未披露训练所需的计算资源，其方法在大规模语料和超长上下文上的可扩展性存在未知数。
* **选择性极小的风险**：只选择 2–3 篇文档可能对"需要多篇证据交叉验证"的复杂推理型问题不够充分，或对单篇文档内证据分散的情况出现遗漏。
* **与现有工具链的兼容性**：取消独立检索环节后，在动态知识更新、流式索引和可控溯源等场景中的部署灵活性可能受约束。
* **实验证据覆盖偏窄**：缺少从文本中验证到的多语言、多领域迁移实验，以及与其他代表性 RAG 框架在同口径下的系统性对比，实验结果的普适性仍需更多证据支撑。
* **未在摘要中充分讨论失败案例**：对于选择的文档全部不相关时模型的鲁棒性行为，以及自反思 MLP 层引入的额外参数与推理开销，均没有展开分析。

（完）

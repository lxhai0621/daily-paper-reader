---
title: "AssoMem: Scalable Memory QA with Multi-Signal Associative Retrieval"
title_zh: AssoMem：基于多信号联想检索的可扩展记忆问答
authors: "Kai Zhang, Xinyuan Zhang, Ejaz Ahmed, Hongda Jiang, Caleb Kumar, Kai Sun, Zhaojiang Lin, Sanat Sharma, Shereen Oraby, AARON COLAK, Ahmed A Aly, Anuj Kumar, Xiaozhong Liu, Xin Luna Dong"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=ZCjWUBwCwE"
tags: ["query:agent"]
score: 9.0
evidence: 基于联想记忆图和多信号检索的长时记忆问答方法
tldr: 大规模记忆问答中，仅依赖语义相似度检索在相似密集场景下容易失效。AssoMem构建以对话话语为节点的联想记忆图，并自动提取线索锚定记忆组织。融合相关性、重要性和时间对齐等多重检索信号，通过自适应互信息融合策略实现重要性感知排序。实验表明该方法在长对话记忆检索和问答上显著优于现有记忆管理系统，为AI助手的长时记忆调用提供了可扩展方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 相似密集环境下基于语义距离的检索难以从大规模对话记忆中准确召回相关信息。
method: 构建联想记忆图并对接自动提取线索，融合相关性、重要性与时间对齐信号进行自适应互信息融合排序。
result: AssoMem在长对话记忆QA基准上取得了显著的准确性提升，尤其在高相似度场景下表现优异。
conclusion: 多信号联想检索与记忆图结构可显著增强AI助手的长期记忆问答能力，具有良好可扩展性。
---

## Abstract
Accurate recall from large-scale memories remains a core challenge for memory-augmented AI assistants performing question answering (QA), especially in similarity-dense scenarios where existing methods mainly rely on semantic distance to the query for retrieval. Inspired by how humans link information associatively, we propose AssoMem, a novel framework constructing an associative memory graph that anchors dialogue utterances to automatically extracted clues. This structure provides a rich organizational view of the conversational context and facilitates importance-aware ranking. Further, AssoMem integrates multi-dimensional retrieval signals—relevance, importance, and temporal alignment—using an adaptive mutual information (MI)-driven fusion strategy. Extensive experiments across three benchmarks and a newly introduced dataset, MeetingQA, demonstrate that AssoMem consistently outperforms state-of-the-art baselines, verifying its superiority in context-aware memory recall.

---

## 论文详细总结（自动生成）

根据提供的论文元数据与摘要（注：全文 PDF 被验证页面拦截，以下总结基于可见的标题、摘要、TLDR 及结构化字段），现对论文进行结构化分析。

## 1. 核心问题与整体含义

- **研究背景**：大规模记忆增强的 AI 助手在回答问题时，需要从海量长期对话记忆中准确召回相关信息。现有方法主要依赖查询与记忆之间的**语义距离**进行检索。
- **核心问题**：在**相似密集场景**（即大量记忆在语义上彼此接近）下，仅靠语义相似度检索容易导致误召回或漏召回，难以区分真正相关与表面相似的记忆。
- **整体含义**：提出一种模仿人类联想记忆机制的检索框架，以改善 AI 助手的长期记忆问答能力，使其在复杂、高相似度的对话记忆中仍能保持高准确率，并具备可扩展性。

## 2. 方法论

- **核心思想**：借鉴人类将信息进行关联性组织的认知方式，构建**联想记忆图**作为记忆组织与检索的基础。
- **关键技术**：
  - **联想记忆图构建**：以对话话语为节点，将话语锚定到**自动提取的线索（clues）**上，形成丰富的图结构，提供对话上下文的组织视图。
  - **多信号融合**：整合三类互补的检索信号：
    - **相关性**：与查询的语义关联程度；
    - **重要性**：记忆在整体对话图中的关键程度；
    - **时间对齐**：记忆发生时间与查询时间之间的匹配关系。
  - **自适应互信息（MI）驱动融合**：采用自适应的互信息策略，对三类信号进行动态加权融合，实现**重要性感知的排序**，而非简单加权求和。
- **算法流程（文字描述）**：输入查询 → 在联想记忆图上定位候选记忆 → 分别计算相关性、重要性、时间对齐三个信号 → 通过自适应互信息融合计算综合评分 → 按评分排序并召回最相关记忆 → 用于回答生成。

## 3. 实验设计

- **数据集 / 场景**：
  - 使用了 **三个既有基准**（论文未给出具体名称，属于既有长期记忆 QA 或对话记忆检索基准）；
  - 新增了一个数据集 **MeetingQA**，用于补充验证方法在会议类长对话记忆场景下的表现。
- **对比方法**：与 **state-of-the-art 基线**（现有记忆管理系统/检索方法）进行比较。
- **评估方式**：在多个基准上测量问答准确率或召回准确率，尤其关注高相似度场景下的表现。

## 4. 资源与算力

- 提供的元数据与摘要中**未提及任何算力信息**，包括 GPU 型号、数量、训练时长、参数量等。
- 因此，无法判断实验的计算成本或训练效率，也无法评估方法在资源受限环境下的可行性。

## 5. 实验数量与充分性

- **实验数量**：从可见信息看，涉及 **3 个基准 + 1 个新数据集**，属于跨场景、多基准验证。但元数据中未列出每个基准上的具体实验组数、消融实验数量或统计显著性检验。
- **充分性讨论**：
  - **优点**：多基准 + 新数据集增加了结论的普适性；
  - **不足**：缺少消融实验细节（如各信号单独效果、MI 融合策略 vs 简单融合），也未报告方差/多次运行结果，因此无法完全评估方法的鲁棒性和各组件贡献。
  - **公平性**：声称“一致优于 SOTA”，但缺乏对基线设置、超参数调整、检索后处理等细节的说明，客观公平性尚待验证。

## 6. 主要结论与发现

- AssoMem 在多个长期对话记忆 QA 基准上** consistently outperforms** 现有 SOTA 方法。
- 在**高相似度场景**下，联想记忆图 + 多信号融合的优势尤其明显，说明该方法能有效缓解语义密集带来的检索歧义。
- 验证了**多信号联想检索**与**记忆图结构**对于 AI 助手长期记忆调用的有效性，并具有较好的**可扩展性**。

## 7. 优点

- **方法新颖**：将联想记忆图引入记忆检索，区别于纯向量相似度检索，更贴近人类记忆组织方式。
- **多信号融合设计合理**：同时考虑相关性、重要性、时间对齐三个维度，且采用自适应互信息融合，而非固定权重，有助于动态适应不同查询场景。
- **引入新数据集 MeetingQA**：丰富了评测资源，为后续研究提供了新场景。
- **问题定位准确**：聚焦“相似密集场景”这一实际痛点，具有现实价值。

## 8. 不足与局限

- **信息不完整**：由于全文无法获取，无法确认更多技术细节、公式推导及实验设置。
- **基准具体性不足**：三个既有基准的名称、规模、任务形式未在可见信息中列出，削弱了可复现性。
- **缺乏消融与敏感性分析**：未说明各信号单独贡献、融合策略对比、图构建参数影响等，不利于判断哪些设计最为关键。
- **偏差风险**：新数据集 MeetingQA 的质量、难度、标注口径未知，可能存在领域偏差；且“优于 SOTA”的宣称缺乏统计检验支撑。
- **应用限制**：方法依赖自动线索提取和图构建，线索提取质量可能成为瓶颈；在极端大规模记忆下的计算开销和时间成本未讨论，可扩展性仅有定性描述。

（完）

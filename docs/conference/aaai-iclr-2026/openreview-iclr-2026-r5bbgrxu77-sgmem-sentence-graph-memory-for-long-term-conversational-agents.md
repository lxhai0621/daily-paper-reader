---
title: "SGMem: Sentence Graph Memory for Long-Term Conversational Agents"
title_zh: SGMem：面向长期对话智能体的句子图记忆
authors: "Yaxiong Wu, Yongyue Zhang, Sheng Liang, Yong Liu"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=r5BbGRXU77"
tags: ["query:agent"]
score: 9.0
evidence: 句子图记忆为长期对话智能体跨粒度组织并检索对话上下文
tldr: 长期对话智能体需要管理超出上下文窗口的对话历史，但现有抽取式或摘要式记忆难以跨粒度组织检索。SGMem将对话表示为分块单元内的句子级图，捕捉回合、轮次和会话层面的关联，并将检索到的原始对话与生成的摘要、事实和洞察结合提供给LLM。在LongMemEval和LoCoMo等基准上，SGMem提升了长对话记忆检索的一致性与回答质量。该工作为长期对话智能体记忆管理提供了图结构的新方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有记忆方法难以在对话多粒度上组织和检索相关上下文，影响长期对话智能体的回答质量。
method: 构建分块单元内的句子级图记忆，融合原始对话与生成摘要、事实、洞察，实现跨粒度一致性检索。
result: 在LongMemEval和LoCoMo上，SGMem在长期对话记忆评测中取得领先的记忆检索与回答性能。
conclusion: 句子图记忆结构可有效提升长期对话智能体的记忆组织和检索能力，增强上下文连贯性。
---

## Abstract
Long-term conversational agents require effective memory management to handle dialogue histories that exceed the context window of large language models (LLMs). Existing methods based on fact extraction or summarization reduce redundancy but struggle to organize and retrieve relevant information across different granularities of dialogue and generated memory. We introduce SGMem (Sentence Graph Memory), which represents dialogue as sentence-level graphs within chunked units, capturing associations across turn-, round-, and session-level contexts. By combining retrieved raw dialogue with generated memory such as summaries，facts and insights, SGMem supplies LLMs with coherent and relevant context for response generation. Experiments on LongMemEval and LoCoMo show that SGMem consistently improves accuracy and outperforms strong baselines in long-term conversational question answering.

---

## 论文详细总结（自动生成）

# SGMem：句子图记忆用于长期对话智能体 — 论文中文总结

> 说明：本次可获取的论文内容仅包含标题、作者、摘要及少量元数据，未包含正文、实验细节、公式与算法伪代码等信息。以下总结严格基于现有材料，并在信息缺失处予以明确标注。

## 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：长期对话智能体需要处理超出大语言模型（LLM）上下文窗口的对话历史，因此必须依赖有效的记忆管理机制。
- **现有方法不足**：已有的基于事实抽取或摘要的方法虽然降低了信息冗余，但难以在对话的不同粒度（如单个回合、整轮对话、整个会话）之间进行有效的组织和检索，导致相关信息在回答时可能缺失或错位。
- **核心问题**：如何设计一种记忆结构，既能跨粒度捕捉对话之间的关联，又能为 LLM 提供连贯且相关的上下文，从而提升长期对话问答的准确性。
- **整体意义**：通过引入图结构记忆，为长期对话智能体的记忆管理提供了一种新思路，有助于缓解上下文窗口限制带来的信息遗忘问题。

## 2. 方法论：核心思想、关键技术细节与流程

- **模型名称**：SGMem（Sentence Graph Memory，句子图记忆）。
- **核心思想**：将对话表示为**分块单元内的句子级图**，以句子为节点、句子间的语义/结构关系为边，从而显式建模对话中的关联结构。
- **多粒度关联**：该图结构能够捕捉**回合级（turn-level）、轮次级（round-level）和会话级（session-level）** 的上下文关联，实现跨粒度的信息组织。
- **结合原始与生成记忆**：检索时，SGMem 将**检索到的原始对话片段**与**生成的记忆**（包括摘要、事实和洞察）一起提供给 LLM，以提供更丰富、连贯的上下文。
- **算法流程（根据摘要推断）**：
  1. 将长对话按块（chunk）切分；
  2. 在每个块内构建句子级图，提取句子间关联；
  3. 针对不同粒度的对话单元建立索引或表示；
  4. 在回答问题时，根据问题检索最相关的图节点/子图，并同时召回原始对话片段与预先生成的摘要、事实和洞察；
  5. 将上述信息拼接为上下文，输入 LLM 生成最终回复。
- **公式或伪代码**：摘要中未提供，因此本文不包含具体公式或算法步骤细节。

## 3. 实验设计：数据集、基准与对比方法

- **基准（Benchmark）**：
  - **LongMemEval**：用于评估长期对话记忆能力的基准；
  - **LoCoMo**：另一个长期对话建模与记忆评测数据集。
- **任务**：长期对话问答（long-term conversational question answering）。
- **对比方法**：摘要中仅提到“strong baselines”（强基线），未列出具体基线名称（如基于抽取式或摘要式记忆的方法等）。
- **评估指标**：主要报告“准确率（accuracy）”的提升，具体指标细节未给出。
- **实验结果概述**：SGMem 在 LongMemEval 和 LoCoMo 上均“持续提升准确率”，并优于强基线。

## 4. 资源与算力

- **现有材料中未提及**任何关于 GPU 型号、数量、训练时长、参数量或推理开销的信息。
- 元数据中仅包含论文发表信息（2025-09-16）和来源标记（ICLR-2026-Rejected-Public），与算力无关。
- **结论**：无法从提供内容中总结资源与算力使用情况，需获取全文后方可补充。

## 5. 实验数量与充分性

- **实验数量**：摘要只明确提到在两个基准（LongMemEval、LoCoMo）上的实验，未提及具体实验组数。
- **消融实验**：未在摘要中提及是否有消融实验（如去掉图结构、去掉生成记忆组合等）。
- **充分性与客观性评估**：
  - **不足**：缺少对实验细节（如数据划分、基线配置、统计显著性、误差范围等）的说明，无法判断实验是否充分；
  - **客观性风险**：摘要由作者自述，且该论文标记为“ICLR-2026-Rejected-Public”（尽管评分显示 9.0，但仍遭拒绝），可能存在评审对其说服力或严谨性的质疑；
  - 因此，基于现有信息只能确认 SGMem 在所述两个基准上表现良好，但无法验证实验设计的完整性与公平性。

## 6. 主要结论与发现

- SGMem 通过句子级图结构能够**有效提升长期对话记忆的组织和检索能力**。
- 将原始对话与生成记忆（摘要、事实、洞察）相结合，可以为 LLM 提供**更连贯、更相关的上下文**，从而改善回答质量。
- 在 LongMemEval 和 LoCoMo 上，SGMem 相比强基线具有一致的准确率提升。
- 核心发现：**对话记忆的图结构表示有助于跨粒度检索，优于单纯的事实抽取或摘要方法**。

## 7. 优点（方法与实验设计的亮点）

- **创新性**：将句子级图引入对话记忆管理，突破了传统抽取/摘要方法在粒度组织上的局限。
- **多粒度建模**：显式覆盖回合、轮次、会话三个层级，符合对话本身的分层结构。
- **组合检索**：融合原始对话与生成记忆，兼顾了具体细节与高层抽象信息，有助于回答需要不同类型记忆的问题。
- **普遍性**：在多个公开长期对话基准上验证效果，表明方法具有一定泛化能力。

## 8. 不足与局限

- **信息不完整**：由于只获得摘要，缺少方法细节、超参数设置、基线实现及具体实验结果表格，难以深入评估其技术贡献。
- **实验覆盖有限**：仅提到两个基准，未说明是否在更多场景（如多轮任务型对话、跨会话对话、中文对话等）下测试。
- **消融与鲁棒性缺失**：未提供消融实验、不同图构建策略的影响、对图规模/计算开销的分析等，难以判断各组件独立贡献。
- **计算成本不透明**：句子级图构建与检索可能引入额外显存和延迟，但未给出相关资源报告。
- **应用限制**：图结构记忆的构建可能依赖语义相似度计算或额外模型，对于非常长的对话流可能产生规模爆炸问题；且原始对话与生成记忆的权重如何平衡、如何避免生成记忆中的事实错误，均未在摘要中讨论。
- **论文状态**：元数据显示该论文被 ICLR 2026 拒绝（尽管用户评分显示 9.0），虽然评分不代表最终结论，但可能反映存在某些实验或写作层面的不足。

（完）

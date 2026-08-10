---
title: "MA-RAG: Multi-Agent Retrieval-Augmented Generation via Collaborative Chain-of-Thought Reasoning"
title_zh: MA-RAG：基于协同思维链推理的多智能体检索增强生成
authors: "Thang Viet Nguyen, Peter Chin, Yu-Wing Tai"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=Yc9LTfD7DY"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于多智能体协同思维链推理的RAG框架
tldr: 针对复杂信息寻求任务中的查询歧义和证据稀疏问题，MA-RAG将RAG流程拆分为计划、分步定义、抽取和问答等多个专业智能体，以协同思维链推理逐子任务处理。该方法通过任务感知推理缓解了检索文档中的间接证据和跨源信息整合难题。在复杂问答场景中，MA-RAG显著提升了检索与回答的准确性和鲁棒性，展示了多智能体协作在RAG架构中的潜力。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG在复杂查询中常因歧义和间接证据不足而失效，需要更智能的任务分解与协作机制。
method: 构建由Planner、Step Definer、Extractor和QA Agent组成的多智能体RAG框架，通过协同思维链逐步分解并解决检索与推理问题。
result: 在复杂信息寻求任务上，MA-RAG相比传统RAG方法和单环节优化方法取得了更好的准确率和鲁棒性。
conclusion: 多智能体协同思维链推理能有效应对RAG中的歧义和证据稀疏挑战，为下一代检索增强生成提供了新范式。
---

## Abstract
We present MA-RAG, a Multi-Agent framework for Retrieval-Augmented Generation (RAG) that addresses the inherent ambiguities and reasoning challenges in complex information-seeking tasks. Unlike conventional RAG methods that rely on either end-to-end fine-tuning or isolated component enhancements, MA-RAG orchestrates a collaborative set of specialized AI agents: Planner, Step Definer, Extractor, and QA Agents, to tackle each stage of the RAG pipeline with task-aware reasoning. Ambiguities may arise from underspecified queries, sparse or indirect evidence in retrieved documents, or the need to integrate information scattered across multiple sources. MA-RAG mitigates these challenges by decomposing the problem into subtasks, such as query disambiguation, evidence extraction, and answer synthesis, and dispatching them to dedicated agents equipped with chain-of-thought prompting. These agents communicate intermediate reasoning and progressively refine the retrieval and synthesis process. Our design allows fine-grained control over information flow without any model fine-tuning. Crucially, agents are invoked on demand, enabling a dynamic and efficient workflow that avoids unnecessary computation. This modular and reasoning-driven architecture enables MA-RAG to deliver robust, interpretable results. Experiments on multi-hop and ambiguous QA benchmarks demonstrate that MA-RAG outperforms state-of-the-art training-free baselines and rivals fine-tuned systems, validating the effectiveness of collaborative agent-based reasoning in RAG.

---

## 论文详细总结（自动生成）

# MA-RAG 论文中文总结

## 1. 核心问题与整体含义

- **研究动机**：传统检索增强生成（RAG）方法在面对复杂信息寻求任务时，容易受到查询歧义、文档中证据稀疏或间接、以及需要跨多个来源整合信息的挑战。现有方案要么依赖端到端微调，要么仅对单个组件进行优化，缺乏对整体流程的协同推理能力。
- **问题本质**：需要一种无需微调、模块化且能动态适应任务复杂度的 RAG 框架，以提升复杂查询下的检索准确性和回答质量。
- **整体含义**：论文提出 MA-RAG，通过多智能体协作和思维链推理，将 RAG 管道分解为多个子任务，由专用智能体逐步处理，从而更鲁棒地应对歧义和证据不足的问题，为下一代 RAG 提供了新范式。

## 2. 方法论

- **核心思想**：使用多个专门化的 AI 智能体协作完成 RAG 全流程，每个智能体负责一个子任务，并通过链式思维（Chain-of-Thought）推理逐步细化信息流。
- **智能体组成**：
  - **Planner（规划器）**：负责任务分解与全局规划。
  - **Step Definer（步骤定义器）**：将规划转化为可执行的子任务步骤。
  - **Extractor（抽取器）**：从检索到的文档中提取与子任务相关的证据。
  - **QA Agent（问答智能体）**：综合抽取证据，生成最终答案。
- **关键技术细节**：
  - 智能体之间传递中间推理结果，协同完成查询消歧、证据抽取和答案合成。
  - 采用**按需调用（on-demand）** 机制：并非所有智能体每次都执行全部流程，而是根据任务复杂度动态触发，避免不必要的计算。
  - 全程无需模型微调，依赖提示词和智能体协作实现精细控制。
- **算法流程（文字描述）**：
  1. 输入复杂查询 → Planner 分析歧义与需求，生成任务计划。
  2. Step Definer 将计划拆解为明确的子步骤。
  3. 针对每个子步骤，Extractor 在检索文档中定位间接或分散证据。
  4. QA Agent 结合各步骤的提取结果进行推理，生成答案。
  5. 整个流程通过链式思维提示驱动，中间推理结果在智能体间共享，逐步修正和完善。

## 3. 实验设计

- **数据集/场景**：论文提及使用了**多跳问答（multi-hop QA）** 和**歧义问答（ambiguous QA）** 基准。但所给资料中未列出具体数据集名称（如 HotpotQA、MuSiQue、AmbigQA 等）。
- **对比方法**：
  - **无训练（training-free）基线方法**：对比了当前最先进的无需微调的 RAG 方法。
  - **微调系统（fine-tuned systems）**：也作为对比参照，用于衡量 MA-RAG 的性能上限。
- **评估指标**：未在提供的文本中明确给出具体指标（如 EM、F1、准确率等），推测为标准问答指标。
- **总体设计**：属于端到端框架级评测，侧重验证多智能体协作推理在复杂问答场景中的有效性。

## 4. 资源与算力

- **未明确说明**：提供的论文元数据和摘要中**没有提及**使用的 GPU 型号、数量、训练时长或推理资源消耗。
- 仅可推断：由于方法强调“无需微调”，训练阶段可能不涉及大规模算力；但推理阶段的多智能体调用可能产生额外计算开销。具体资源需求无法从现有信息中得知。

## 5. 实验数量与充分性

- **实验数量**：所给资料中未列出具体实验组数、消融实验细节或数据集数量。仅笼统提到“在 multi-hop 和 ambiguous QA 基准上进行了实验”。
- **充分性评估**：
  - **优点**：对比了训练-free 和微调两类方法，具有一定代表性。
  - **不足**：缺少具体数据集名称、实验结果数值、消融分析、误差分析以及不同智能体贡献度分析。因此，**实验证据的充分性和客观性无法从现有信息中完全确认**。
  - 若要证明框架的普遍性，还需要更多样的任务覆盖（如开放域问答、事实验证）和更细致的组件消融。

## 6. 主要结论与发现

- MA-RAG 在复杂信息寻求任务上显著优于当前最先进的**无训练基线**。
- 与需要微调的系统相比，MA-RAG 能达到**可比的性能**，证明了“无需微调的多智能体协同推理”可以媲美微调方案。
- 验证了任务感知推理、按需调用和模块化设计在 RAG 中的有效性与效率。
- 强调框架的**鲁棒性**和**可解释性**，能够通过智能体分工和链式推理缓解查询歧义与证据稀疏问题。

## 7. 优点

- **无需微调**：模型参数不变，仅通过提示和多智能体协作完成任务，部署成本低。
- **模块化设计**：各智能体职责清晰，便于分工、调试和扩展。
- **按需调用**：动态工作流避免不必要的计算，兼顾效率与效果。
- **协同思维链**：智能体之间传递中间推理，增强了复杂问题上的逻辑连贯性。
- **可解释性**：每一步骤由明确的智能体处理，中间结果可追踪，有助于理解模型行为。
- **性能领先**：在训练-free 方法中达到 SOTA，且能匹敌微调系统，具有很强的实用潜力。

## 8. 不足与局限

- **实验细节缺失**：未提供具体数据集名称、指标数值、基线设置及消融实验，难以独立复现和全面评估。
- **算力资源未披露**：没有报告推理开销或计算成本，无法评估方法在大规模场景下的工程可行性。
- **任务覆盖有限**：主要集中在多跳和歧义问答，对其他类型的复杂信息寻求任务（如时序推理、多模态检索）尚未验证。
- **潜在偏差风险**：智能体协作依赖大型语言模型的提示词敏感性，可能在不同模型或提示模板下性能波动较大。
- **动态调用机制的有效性**：缺乏与固定流程的对比证据，无法确定按需调用的收益是否有统计显著性。
- **被拒稿背景**：该论文标注为“ICLR-2026-Rejected-Public”，可能说明评审认为其创新性或验证充分性存在一定问题，需谨慎看待结论的普适性。

（完）

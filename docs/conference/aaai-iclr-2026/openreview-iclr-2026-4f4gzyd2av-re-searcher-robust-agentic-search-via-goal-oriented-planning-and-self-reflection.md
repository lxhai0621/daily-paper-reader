---
title: "RE-Searcher: Robust Agentic Search via Goal-oriented Planning and Self-reflection"
title_zh: RE-Searcher：面向目标进行规划与自我反思的稳健智能体搜索
authors: "Daocheng Fu, Jianbiao Mei, Licheng Wen, Xuemeng Yang, Cheng Yang, Rong Wu, Tao Hu, Siqi Li, Yufan Shen, Xinyu Cai, Pinlong Cai, Botian Shi, Yong Liu, Yu Qiao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=4f4gzyD2Av"
tags: ["query:ma-kf"]
score: 8.0
evidence: 集成外部搜索工具并具备目标规划与自我反思的智能体搜索方法
tldr: 基于LLM的智能体在接入外部搜索工具后，容易因查询表述微小变化而陷入低效轨迹。RE-Searcher提出系统分析环境复杂度对搜索行为的影响，并设计目标导向规划与自我反思机制来增强搜索智能体。该方法在面对复杂搜索环境时能够更稳定地规划查询并纠正错误路径，从而提升知识密集型问答的效果。该工作展示了外部API集成与智能体自反思结合的价值。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 智能体接入外部搜索工具后，查询表述的微小变化会显著影响搜索轨迹和最终性能。
method: 提出目标导向规划与自我反思机制，训练搜索智能体在复杂环境中稳定选择查询并纠正偏差。
result: RE-Searcher在复杂搜索任务中提升了鲁棒性和答案准确性，减少了错误累积。
conclusion: 目标导向规划与自我反思可显著提升智能体在外部工具环境中的稳定性和任务成功率。
---

## Abstract
Large language models (LLMs) excel at knowledge-intensive question answering and reasoning, yet their real-world deployment remains constrained by knowledge cutoff, hallucination, and limited interaction modalities. Augmenting LLMs with external search tools helps alleviate these issues, but it also exposes agents to a complex search environment in which small, plausible variations in query formulation can steer reasoning into unproductive trajectories and amplify errors. We present a systematic analysis that quantifies how environmental complexity induces fragile search behaviors and, in turn, degrades overall performance. To address this challenge, we propose a simple yet effective approach to instantiate a search agent, RE-Searcher. During search, RE-Searcher explicitly articulates a concrete search goal and subsequently reflects on whether the retrieved evidence satisfies that goal. This combination of goal-oriented planning and self-reflection enables RE-Searcher to resist spurious cues in complex search environments and perform robust search. Extensive experiments show that our method improves search accuracy and achieves state-of-the-art results. Perturbation studies further demonstrate substantial resilience to noisy or misleading external signals, mitigating the fragility of the search process. We believe these findings offer practical guidance for integrating LLM-powered agents into more complex interactive environments and enabling more autonomous decision-making.

---

## 论文详细总结（自动生成）

# RE-Searcher：面向目标规划与自我反思的稳健智能体搜索——论文总结

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）在知识密集型问答（knowledge-intensive QA）与推理任务中表现出色，但其实际部署受限于三大瓶颈——**知识截止（knowledge cutoff）**、**幻觉（hallucination）** 以及**有限的外部交互模态**。
- **既有尝试**：将 LLM 与外部搜索工具集成是缓解上述问题的常见方案，能够让模型动态获取最新、更广泛的信息。
- **关键问题**：接入外部搜索工具后，智能体暴露于**高度复杂的搜索环境**中，导致 `查询表述的微小、看似合理的变动` 就足以将推理引入低效甚至错误的轨迹，并在多步搜索中**逐步放大错误**。这种对查询措辞的脆弱敏感性，是制约搜索智能体在实际场景中稳定性的核心问题。
- **研究意义**：本文旨在系统量化"环境复杂度如何诱发搜索行为的脆弱性"，并提出相应方法提升智能体在复杂交互环境中的鲁棒性，为 LLM 智能体的实际部署与自主决策提供指导。

## 2. 方法论：RE-Searcher

### 2.1 核心思想

RE-Searcher 的核心思路是：**在搜索进程中显式引入"目标"概念，并围绕目标进行规划与验证**。其基本假设是——如果搜索智能体能明确知道自己"要什么"（具体搜索目标），并能持续检查"是否已经找到"（检索证据是否满足目标），就能有效抵抗复杂环境中的干扰性/误导性信号，避免被无关或虚假信息带偏。

### 2.2 两大关键技术机制

- **目标导向规划（Goal-oriented Planning）**：在搜索的每一步，智能体被要求显式阐明一个**具体的、可操作的搜索目标**（而非笼统的查询意图），并以此目标为基准生成或修正实际的搜索查询。这一机制迫使模型将模糊的检索任务分解为有方向的探索步骤，降低查询表述微小变化对搜索轨迹的扰动。
- **自我反思（Self-reflection）**：在获得检索结果后，智能体对"检索到的证据是否真正满足了既定搜索目标"进行显式评估。若证据不足或偏离目标，则触发**纠偏机制**——调整查询方向、重新规划搜索策略；若目标已达成，则进入答案生成阶段。可将其理解为一种**内部验证回路**：目标驱动查询，证据反验目标，形成闭环。
- **协同机制**：规划负责"指明方向"，反思负责"检查是否偏航"，两者组合使 RE-Searcher 能够在复杂环境中有意识地**抵抗虚假线索（spurious cues）**，并在错误累积之前及时纠正路径。

### 2.3 公式与算法流程

论文摘要中未提供具体的数学公式、伪代码或模型结构细节，但可基于描述将整体算法流程概括为以下循环：

1. **初始化**：接收用户问题，设定初始搜索意图。
2. **目标规划**：基于当前状态（问题、已有证据、反思结果），显式生成一个具体搜索目标。
3. **查询生成**：依据该目标生成搜索查询并调用外部搜索工具。
4. **证据收集**：获取检索结果。
5. **自我反思**：判断检索证据是否满足步骤 2 中设定的目标：
   - **满足** → 进入最终答案生成；
   - **不满足** → 分析差距，回到步骤 2 重新规划（或调整查询）。
6. **答案生成**：以最终证据为基础生成回答。

## 3. 实验设计

### 3.1 数据集与基准（Benchmark）

- 摘要中仅笼统提及 "Extensive experiments" 和 "state-of-the-art results"，但**未列出具体使用的数据集名称**（如 HotpotQA、Natural Questions、MuSiQue 等）、基准规模或评估协议。
- 从研究问题推断，实验应覆盖**知识密集型多跳问答**类任务，但具体 benchmark 细节在摘要中不可见。

### 3.2 对比方法与评估维度

- **对比方法**：摘要未明确列出基线方法，但从 "achieves state-of-the-art results" 推断，应对比了至少包括：直接 LLM 问答（无搜索）、传统检索增强生成（RAG）方法、以及若干已有的 LLM 搜索智能体方法。
- **扰动研究（Perturbation Studies）**：除常规准确性评估外，还设计了针对噪声/误导性外部信号的扰动实验，专门验证对**搜索过程脆弱性**的缓解效果。

## 4. 资源与算力

- **未披露**：论文摘要中**完全没有提及**使用的 GPU 型号、数量、训练时长、参数量或计算成本等资源信息。
- 这是一个显著的透明度缺口。对依赖大模型微调的智能体方法而言，训练/推理成本是实际部署的关键考量，缺少此信息使得复现成本难以预估。

## 5. 实验数量与充分性评估

- **实验数量**：摘要层面可确认的实验包括：① 主实验（达到 SOTA）；② 扰动/鲁棒性实验。完整的消融实验（如仅用目标规划、仅用自我反思、两者组合）虽符合方法设计的需要，但摘要未明确提及。
- **充分性与客观性**：
  - **积极面**：扰动研究直接针对论文提出的"脆弱性"核心问题设计，评估逻辑与问题定义高度一致，具备较好的针对性。
  - **不确定面**：未披露数据集清单与基线方法，无法从摘要层面判断实验覆盖的广泛性（如是否包含多领域、多难度任务）以及对比的公平性（如是否与同等规模的搜索智能体方法对齐计算资源）。
- **总体评价**：实验设计框架合理，但**证据披露不充分**，在缺少完整实验章节的情况下难以对其充分性做出最终判定。

## 6. 主要结论与发现

1. **实现系统性量化分析**：论文提供了"环境复杂性 → 脆弱搜索行为 → 整体性能下降"这一因果链的量化证据，明确了问题的存在与严重性。
2. **方法有效性验证**：RE-Searcher 在复杂搜索任务中**显著提升搜索准确率**，并在基准上达到 **SOTA 性能**。
3. **鲁棒性显著增强**：扰动实验表明，该方法对含噪或误导性的外部信号具有**实质性抵抗力**，有效降低了搜索进程的脆弱性、遏制了错误的逐步累积。
4. **实践启示**：目标导向规划 + 自我反思的组合，为将 LLM 智能体安全地集成到更复杂的交互式环境、实现更自主的决策，提供了可行且有效的设计范式。

## 7. 方法亮点与优势

- **问题定义精准**：将"查询表述微小变化引发性能大幅波动"这一实际痛点，提升为可量化分析的科学问题，切入点具有实用价值。
- **方法简洁有效**：目标规划与自我反思是概念上清晰、实现上低复杂度的机制，不引入复杂外部模块，具备较强的可推广性与可复现潜力。
- **针对性强**：设计直接回应已识别的脆弱性问题——规划防止走偏、反思及时纠错，逻辑闭环完整。
- **鲁棒性验证充分（方向上）**：专门的扰动实验设计，体现了对真实搜索环境中噪声、误导信息等不利因素的关注，超越常规仅关注平均准确率的评估方式。
- **广泛的适用启示**：该范式不局限于搜索场景，对 Agent 在其他工具交互环境（数据库操作、代码执行、API 调用）中的稳健性设计均具参考价值。

## 8. 不足与局限性

### 8.1 实验层面

- **关键细节缺失**：数据集、基线与评估协议未在摘要中报告，外部无法验证实验的全面性、基线选择的公平性及结果的可重复性。
- **消融证据不明确**：未确认是否提供了消融实验来分离"目标规划"与"自我反思"各自的独立贡献。
- **扰动实验范围未知**：未说明噪声/误导性信号的具体类型、注入方式与强度梯度，难以判断鲁棒性提升的边界。

### 8.2 资源透明性

- **计算成本完全未披露**，对于面向实际部署的智能体方法而言，这是一个不可忽视的信息缺失。

### 8.3 方法局限

- **依赖 LLM 的自我评估能力**：自我反思环节依赖模型对其已获取证据的准确判断。若模型本身对"是否满足目标"的判断存在偏差，纠偏机制可能失效甚至引入新错误（即"反思幻觉"）。
- **额外推理开销**：显式的目标规划与反思增加了每步搜索的推理成本与延迟，摘要未讨论其效率成本与收益的权衡。
- **应用范围有限**：方法在知识密集型问答场景中验证，对更复杂的多模态环境、交互式长任务或目标模糊场景中的适用性尚待验证。

### 8.4 其他

- 本文被 **ICLR 2026 拒稿**（评分为 8.0）。高评分伴随拒稿，提示评审意见中可能包含摘要之外的经验性不足（如实验覆盖度、数据规模、新颖性定位等）。
- 本次分析基于的公开文本为摘要级信息，完整方法细节（提示词设计、训练目标、搜索 API 配置）均不可见，因此本总结受限于可得信息范围，不能完全替代对全文的评估。

---

（完）

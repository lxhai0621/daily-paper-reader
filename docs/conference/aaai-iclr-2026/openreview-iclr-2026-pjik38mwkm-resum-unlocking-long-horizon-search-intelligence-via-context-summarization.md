---
title: "ReSum: Unlocking Long-Horizon Search Intelligence via Context Summarization"
title_zh: ReSum：通过上下文摘要解锁长时程搜索智能
authors: "Xixi Wu, Kuan Li, Yida Zhao, Liwen Zhang, Litu Ou, Huifeng Yin, Zhongwang Zhang, Xinmiao Yu, Ding-Chu Zhang, Yong Jiang, Pengjun Xie, Fei Huang, Minhao Cheng, Shuai Wang, Hong Cheng, Jingren Zhou"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=PjIK38mwKm"
tags: ["query:agent"]
score: 9.0
evidence: ReSum采用周期性上下文摘要与GRPO管理长时程搜索
tldr: LLM Web智能体在执行复杂查询时受上下文预算限制，传统ReAct方法易在到达解前耗尽。ReSum周期性将增长的历史交互转换为紧凑的推理状态，绕过上下文限制，同时保留先前发现。并提出ReSum-GRPO对分段轨迹进行强化学习，使范式可适应，大幅扩展可探索的搜索周期。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM Web智能体受限于上下文长度，复杂查询在耗尽预算前难以求解。
method: ReSum提出周期性上下文摘要压缩交互历史，并用GRPO强化学习适配，形成长时程搜索范式。
result: 实验表明ReSum能显著延长探索时间并提升知识密集型查询的求解率。
conclusion: 上下文摘要化能突破LLM Web智能体的长度约束，支持无限期探索。
---

## Abstract
Large Language Model (LLM)-based web agents demonstrate strong performance on knowledge-intensive tasks but are hindered by context window limitations in paradigms like ReAct. Complex queries involving multiple entities, intertwined relationships, and high uncertainty demand extensive search cycles that rapidly exhaust context budgets before reaching solutions. To overcome this challenge, we introduce ReSum, a novel paradigm that enables indefinite exploration through periodic context summarization. ReSum converts growing interaction histories into compact reasoning states, maintaining awareness of prior discoveries while bypassing context constraints. For paradigm adaptation, we propose ReSum-GRPO, integrating GRPO with segmented trajectory training and advantage broadcasting to familiarize agents with summary-conditioned reasoning. Extensive experiments on web agents across three benchmarks demonstrate that ReSum delivers an average absolute improvement of 4.5% over ReAct, with further gains of 8.2% following ReSum-GRPO training. Notably, with only 1K training samples, the ReSum-GRPO-trained 30B model achieves 33.3% Pass@1 on BrowseComp-zh and 18.3% on BrowseComp-en, showing competitive performance with leading open-source web agents.

---

## 论文详细总结（自动生成）

## 一、核心问题与研究动机

- 基于大语言模型（LLM）的 Web 智能体在知识密集型任务上表现出色，但受限于上下文窗口长度。
- 传统 ReAct 等范式在应对涉及多实体、复杂关系和高度不确定性的查询时，需要大量交互步骤，容易在得出答案之前耗尽上下文预算，导致任务失败。
- 论文指出，如何突破上下文长度的约束、支持长期持续探索，是当前 LLM Web 智能体面临的关键瓶颈。

## 二、方法论：ReSum 与 ReSum-GRPO

**核心思想：**

- 提出 ReSum 范式，通过周期性上下文摘要将不断增长的交互历史压缩为紧凑的推理状态，从而绕过上下文长度限制，同时保留此前探索获得的关键发现，支持“无限期”的搜索行为。

**技术细节：**

- ReSum 周期性触发摘要机制：每当交互历史接近上下文预算时，将当前历史摘要化为一个精简的“推理状态”，智能体基于该状态继续后续搜索。
- 为了适应这一新范式，提出了 ReSum-GRPO 训练方法：
  - 采用分段轨迹训练，将长轨迹拆分为多个段落；
  - 引入优势广播（advantage broadcasting）机制，使每个段落都能获得合理的强化信号；
  - 通过 GRPO（Group Relative Policy Optimization）与摘要条件化推理相结合，让模型学会在摘要状态下继续决策。

**流程说明：**

1. 智能体按 ReAct 或类似方式执行搜索，记录交互历史；
2. 当上下文接近限制时，触发摘要生成，将历史压缩为推理状态；
3. 智能体基于摘要状态继续搜索，重复此过程直至得出答案；
4. 训练阶段，通过分段轨迹和优势广播，用 GRPO 优化策略，使模型适应摘要条件化的推理模式。

## 三、实验设计

- 使用三个 Web 智能体基准测试进行评测，涵盖中英文知识密集型问答场景。
- 对比方法：以 ReAct 作为主要基线方法，也与其他主流开源 Web 智能体进行对比。
- 主要实验结果：
  - ReSum 相对 ReAct 平均绝对提升 4.5%；
  - 经 ReSum-GRPO 训练后，进一步获得 8.2% 的提升；
  - 仅使用 1K 训练样本，ReSum-GRPO 训练的 30B 模型在 BrowseComp-zh 上取得 33.3% Pass@1，在 BrowseComp-en 上取得 18.3% Pass@1。
- 数据规模：训练数据量很小（仅 1K 样本），说明方法的样本效率较高。

## 四、资源与算力

- 论文提供的元数据和摘要中**未明确说明**使用的 GPU 型号、数量、训练时长等具体算力信息。
- 仅可知训练数据规模为 1K 样本，模型大小为 30B 参数，可在较小数据量下完成训练。

## 五、实验数量与充分性

- 实验覆盖了三个基准（包括中英文场景），并包含消融性对比（ReSum vs. ReAct、ReSum vs. ReSum-GRPO），可验证各模块的贡献。
- 训练样本仅 1K，结合 30B 模型在多个基准上取得有竞争力的结果，实验具备一定的说服力。
- 但从摘要信息来看，论文未披露更多细节（如不同摘要频率的消融、不同模型规模的扩展实验、计算开销分析等），实验的全面性有限。

## 六、主要结论

- 周期性上下文摘要可以显著突破 LLM Web 智能体的上下文长度约束，使其能够执行更长时程的搜索任务。
- 结合 GRPO 与分段轨迹训练，可以使智能体快速适应摘要条件化的推理模式，进一步提升求解率。
- ReSum 在低训练成本下（1K 样本）即可达到与领先开源 Web 智能体相当的性能，验证了其高效性和可扩展性。

## 七、优点

- 思路简洁有效：用摘要机制直接解决上下文窗口瓶颈，概念清晰、易于落地。
- 训练高效：仅需 1K 训练样本即可获得显著提升，具有较高的样本效率和实用价值。
- 兼容性强：ReSum 作为范式可叠加在现有智能体框架上（如 ReAct），并通过 GRPO 进一步优化。
- 实验结果有增量性：在多个基准上均体现出一致的性能提升，跨越语言和任务差异。

## 八、不足与局限

- 算力信息缺失：论文未说明训练使用的硬件资源与训练时间，难以评估实际部署成本。
- 摘要信息可能丢失细节：长时程搜索中，摘要不可避免地会压缩甚至丢失某些中间细节，在需要精确多跳推理的任务中可能存在风险。
- 基准覆盖有限：仅报告了知识密集型问答类任务，尚未验证在指令执行、工具调用等更广泛 Web 任务类型上的泛化能力。
- 可扩展性存疑：30B 模型在 1K 样本下表现良好，但更大或更小模型的表现趋势未在摘要中体现。
- 实验充分性有待加强：未提供更多消融细节（如摘要触发频率、摘要长度、训练策略对比等），实验透明度有限。

（完）

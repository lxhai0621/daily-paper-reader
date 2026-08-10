---
title: "Mnemosyne: An Unsupervised, Human-Inspired Long-Term Memory Architecture for Edge-Based LLMs"
title_zh: Mnemosyne：面向边缘LLM的无监督类人长期记忆架构
authors: "Aneesh Jonelagadda, Christina Hahn, Haoze Zheng, Salvatore Penachio"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=PpvYXkHf1t"
tags: ["query:agent"]
score: 9.0
evidence: 面向LLM的长期记忆存储与检索架构，包含图结构存储和概率召回机制
tldr: 现有LLM记忆系统依赖扩展上下文或静态检索，在边缘设备上不可行。本文提出名为Mnemosyne的无监督类人长期记忆架构，采用图结构存储、物质与冗余过滤、记忆提交与剪枝机制，以及带时间衰减和刷新过程的概率召回。该架构还从固定长度的记忆图子集中高效生成核心摘要，以捕捉用户个性。实验表明它在边缘设备上实现了高效且自然的长期记忆对话，为资源受限场景下的记忆增强提供了一条新路径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有LLM记忆系统多用暴力上下文扩展或静态检索，难以在边缘受限设备上运行。
method: 提出类人记忆机制：图结构存储、过滤与剪枝、概率召回和时间衰减刷新，并生成核心摘要。
result: 在边缘设备上实现高效的长期记忆对话，记忆存储与召回兼顾资源约束和自然交互。
conclusion: 以人类记忆为灵感的结构化无监督记忆架构可显著提升边缘LLM的长期记忆能力。
---

## Abstract
Long-term memory is essential for natural, realistic dialogue. However, current large language model (LLM) memory systems rely on either brute-force context expansion or static retrieval pipelines that fail on edge-constrained devices. We introduce Mnemosyne, an unsupervised, human-inspired long-term memory architecture designed for edge-based LLMs. Our approach uses graph-structured storage, modular substance and redundancy filters, memory committing and pruning mechanisms, and probabilistic recall with temporal decay and refresh processes modeled after human memory. Mnemosyne also introduces a concentrated "core summary" efficiently derived from a fixed-length subset of the memory graph to capture the user's personality and other domain-specific long-term details such as, using healthcare application as an example, post-recovery ambitions and attitude towards care. Unlike existing retrieval-augmented methods, Mnemosyne is designed for use in longitudinal healthcare assistants, where repetitive and semantically similar but temporally distinct conversations are limited by naive retrieval. In experiments with longitudinal healthcare dialogues, Mnemosyne demonstrates the highest win rate of 65.8\% in blind human evaluations of realism and long-term memory capability compared to a baseline RAG win rate of 31.1\%. Mnemosyne also achieves current highest LoCoMo benchmark scores in temporal reasoning and single-hop retrieval compared to other same-backboned techniques. Further, the average overall score of 54.6\% was second highest across all methods, beating commonly used Mem0 and OpenAI baselines among others. This demonstrates that improved factual recall, enhanced temporal reasoning, and much more natural user-facing responses can be feasible with an edge-compatible and easily transferable unsupervised memory architecture.

---

## 论文详细总结（自动生成）

# Mnemosyne：面向边缘LLM的无监督类人长期记忆架构

## 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：长期记忆对于自然、真实的对话至关重要，但现有大语言模型（LLM）的记忆系统主要依赖两种方式：
  - **暴力扩展上下文（brute-force context expansion）**：将大量历史对话直接塞入上下文窗口，成本高、不可持续。
  - **静态检索流水线（static retrieval pipelines）**：如传统RAG，检索方式固定，难以处理语义相似但时间不同、重复出现的对话场景。
- **核心矛盾**：上述方法在资源受限的边缘设备（edge-constrained devices）上不可行，而纵向医疗护理助手等场景恰恰需要长期记忆能力，且对话往往具有“重复但时间上不同”的特征，朴素检索效果不佳。
- **论文目标**：提出一种可在边缘设备上运行、无需监督、受人类记忆机制启发的长期记忆架构，以提升事实回忆、时间推理和对话自然度。

## 2. 方法论：核心思想、关键技术细节

- **总体思路**：模仿人类记忆的认知机制，构建无监督的图结构记忆系统，而非依赖大规模上下文或静态检索。
- **核心组件**：
  - **图结构存储（Graph-structured storage）**：将记忆组织为图，节点和边表示事件、实体及语义关系，支持结构化查询与多跳推理。
  - **物质与冗余过滤（Substance and redundancy filters）**：模块化过滤机制，剔除无意义或重复的信息，保留高价值记忆。
  - **记忆提交与剪枝（Memory committing and pruning）**：决定哪些信息写入长期记忆，并根据重要性或时效性动态剪枝，控制存储规模。
  - **概率召回（Probabilistic recall）**：模拟人类记忆的提取过程，引入**时间衰减**（temporal decay）和**刷新机制**（refresh processes），使得记忆的可用性随时间变化，近期或经常被刷新的记忆更易被召回。
- **核心摘要（Core summary）**：
  - 从记忆图的一个**固定长度子集**中高效生成浓缩的“核心摘要”，用于捕捉用户的**个性特征**及领域相关的长期细节。
  - 示例：在医疗应用场景中，核心摘要可包含患者康复后的目标（post-recovery ambitions）和对护理的态度（attitude towards care）。
- **算法流程简述**（文字描述）：
  1. 新对话输入 → 经物质与冗余过滤，提取有意义的信息；
  2. 将信息提交为记忆图中的节点/边（记忆提交）；
  3. 定期或按规则对记忆图进行剪枝，删除冗余或低价值记忆；
  4. 查询时，从记忆图中以概率方式召回相关记忆，结合时间衰减与刷新调整权重；
  5. 从记忆图固定长度子集中生成核心摘要，用于个性化响应。

## 3. 实验设计：数据集、基准与对比方法

- **数据集/场景**：
  - **纵向医疗护理对话（longitudinal healthcare dialogues）**：主要评估场景，模拟长期护理中重复、语义相似但时间不同的对话。
  - **LoCoMo benchmark**：用于评估长期对话记忆能力，包括时间推理和单跳检索等任务。
- **评估方式**：
  - **盲人评估（blind human evaluations）**：对回复的**真实感**（realism）和**长期记忆能力**进行成对比较，计算胜率（win rate）。
  - **LoCoMo基准分数**：与基于相同主干（same-backboned）的其他技术比较时间推理和单跳检索指标。
- **对比方法**：
  - 基线RAG（Baseline RAG）。
  - Mem0（常用记忆方法）。
  - OpenAI基线（OpenAI baselines）。
  - 其他同主干的长期记忆技术（未列出具体名称）。

## 4. 资源与算力

- **文中未明确说明**使用了多少GPU型号、数量、训练时长或推理资源。
- 但论文强调架构为**边缘设备设计**，因此推断其计算开销低于云端大规模模型，但原文未提供具体硬件配置或能耗数据。

## 5. 实验数量与充分性

- **主要实验**：
  1. 纵向医疗护理对话上的盲人人工评估（对比Mnemosyne vs 基线RAG），得到胜率65.8% vs 31.1%。
  2. LoCoMo基准上的时间推理与单跳检索任务（与其他同主干方法对比）。
  3. 与Mem0、OpenAI等方法的整体分数对比（平均总分54.6%，排名第二）。
- **充分性分析**：
  - **覆盖度**：包含人工评估和基准测试，覆盖了记忆能力的主要维度（事实召回、时间推理、自然度）。
  - **不足**：未提供消融实验（如去除时间衰减、去除剪枝等组件的单独贡献），也未在多样化领域（除医疗外）验证泛化性。
  - **公平性**：盲人评估设计较好，但对手数量和具体配置透明度有限；同一主干的对比有助于控制变量，但未详细说明其他方法调优情况。

## 6. 主要结论与发现

- Mnemosyne在长期记忆对话中**显著优于基线RAG**，盲人评估胜率65.8% vs 31.1%，表明用户感知的真实感和记忆能力更强。
- 在LoCoMo基准上，Mnemosyne在**时间推理和单跳检索**上取得当前最高分数（与其他同主干技术相比）。
- 平均整体分数54.6%，为所有方法中**第二高**，超过了常见的Mem0和OpenAI基线。
- 结论：以人类记忆为灵感的**无监督、边缘兼容**的图结构记忆架构，可以在资源受限设备上实现**更高的事实回忆、更强的时间推理和更自然的人机交互**，并且易于迁移。

## 7. 优点

- **创新性**：将人类记忆机制（时间衰减、刷新、概率召回）引入边缘LLM记忆系统，不同于暴力上下文扩展或静态RAG。
- **实用性**：面向边缘设备设计，强调无监督和可迁移性，适合纵向医疗等资源受限但需要长期记忆的场景。
- **结构优势**：图结构存储天然支持多跳关系和时间推理，核心摘要机制能高效捕捉用户个性与领域细节。
- **实验设计**：采用盲人评估，结果直观；LoCoMo基准提供标准化对比；与多种主流方法对比，增强了说服力。

## 8. 不足与局限

- **实验覆盖有限**：主要围绕医疗对话场景，其他领域（如教育、娱乐）的泛化性未验证。
- **缺乏消融研究**：未单独分析物质过滤、冗余过滤、剪枝、时间衰减、刷新等模块各自贡献，无法判断哪些组件最关键。
- **算力信息缺失**：未报告训练/推理的硬件需求、内存占用或延迟数据，难以直接评估“边缘兼容”的实际程度。
- **对比公平性存疑**：对基线RAG和Mem0/OpenAI的具体实现、调参程度和上下文窗口使用方式未详细说明，可能影响对比公平性。
- **潜在偏差风险**：人工评估的主观性、评估者数量与多样性未披露；LoCoMo基准上的“同主干”限定可能导致无法体现跨架构优势。
- **记忆图规模管理**：虽然提出了剪枝，但长期运行下图结构的增长边界和存储上限未明确分析，边缘设备风险仍存。

（完）

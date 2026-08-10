---
title: "Tool Cache Agent: Accelerating LLM Agent Through Intelligent Tool Call Caching"
title_zh: 工具缓存智能体：通过智能工具调用缓存加速LLM智能体
authors: Jiwoong Kwon
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=tX3YcbNa5w"
tags: ["query:ma-kf"]
score: 8.0
evidence: 针对LLM智能体工具调用的缓存优化，加速外部工具/API交互
tldr: LLM智能体需要动态调用工具和多步流程，工具调用优化对其效率至关重要。本文提出ToolCacheAgent，一个自适应的“智能体之智能体”，自动为工作流中的各工具生成缓存计划，明确可缓存性、过期时间和工具间失效规则，确保有状态执行中的正确性。通过持续监控运行时信号并调整缓存策略，该方法显著降低响应时间和冗余计算，为工具增强型智能体提供更高效的执行机制。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM智能体工具调用频繁且存在大量冗余计算，响应时间成为瓶颈。
method: 提出ToolCacheAgent，自动为工具调用生成缓存计划，动态维护过期与失效规则。
result: 显著提升工具调用响应速度，减少冗余计算，同时保持状态化执行正确性。
conclusion: 面向工具调用的自适应缓存是提升LLM智能体实际运行效率的有效手段。
---

## Abstract
The rapid advancement of large language models (LLMs) is driving the emergence of LLM agents. Unlike standalone LLMs, these agents interact dynamically with their environment, employing tools, multi-step processes, and even multiple LLMs to enhance functionality. Optimizing tool usage is critical for LLM agents. In this paper, we introduce ToolCacheAgent, an adaptive “agent-for-agents” that automatically caches tool call results to improve response time and reduce redundant computation. For each tool in the agent workflow, ToolCacheAgent generates a caching plan that specifies cacheability, expiration, and inter-tool invalidation rules to maintain correctness in stateful executions. It continuously monitors runtime signals and adapts its cache policies to handle shifting workloads and memory pressure. We evaluate ToolCacheAgent across a range of agent workloads with diverse tool usage patterns and observe up to a 1.69$\times$ latency speed-up without compromising accuracy.

---

## 论文详细总结（自动生成）

# ToolCacheAgent 论文详细总结

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）的快速发展催生了LLM智能体（LLM Agent）。与独立使用的LLM不同，智能体需要与环境动态交互，涉及工具调用、多步流程，乃至多个LLM协同工作，以实现更复杂的功能。
- **核心问题**：工具调用是LLM智能体执行任务的关键路径，但外部工具/API调用往往开销较大且存在大量冗余计算——同一工具的相同或相似请求可能被反复执行，导致响应时间成为智能体实际部署中的显著瓶颈。
- **整体含义**：该论文瞄准"智能体运行效率"这一实际部署痛点，提出通过智能缓存工具调用结果的方式，在不损害执行正确性的前提下减少冗余计算、加速智能体响应，属于LLM智能体系统优化方向的重要探索。

## 2. 论文提出的方法论

- **核心思想**：提出ToolCacheAgent，一个自适应的"智能体之智能体"（agent-for-agents），自动为工作流中的工具调用生成缓存计划并动态维护，从而兼顾效率与正确性。
- **关键机制**：
  - **缓存计划生成**：为智能体工作流中的每一个工具自动生成缓存方案，具体包含三方面——
    - *可缓存性（cacheability）*：判断该工具的调用结果是否适用于缓存；
    - *过期时间（expiration）*：为缓存条目设置合理的有效期；
    - *工具间失效规则（inter-tool invalidation rules）*：某些工具的执行可能导致其他工具的缓存结果失效，需定义工具间的依赖与失效关系。
  - **正确性保障**：通过上述失效规则，确保在**有状态执行（stateful executions）**中，缓存的使用不会导致过时或错误的工具结果被复用。
  - **自适应策略调整**：持续监控运行时信号（如工作负载变化、内存压力），动态调整缓存策略以适配不同的运行环境。
- **流程说明**：论文提供的摘要中未披露具体公式或算法伪代码，但从描述可推断其流程为：分析工作流 → 识别工具依赖 → 生成缓存与失效计划 → 运行中持续监控 → 基于反馈动态调整缓存策略。

## 3. 实验设计

- **实验场景**：论文使用了**多种智能体工作负载（a range of agent workloads），覆盖多样化的工具使用模式（diverse tool usage patterns）**。
- **Benchmark/数据集**：摘要中**未明确说明**使用了哪些具体的基准数据集或标准benchmark（如GAIA、AgentBench、WebArena等均未提及）。
- **对比方法**：从摘要来看，**未明确列出与哪些基线方法进行了对比**，但根据研究定位可推测基线可能包括无缓存版本、固定缓存策略或人工配置缓存等方案，具体细节待原文确认。
- **评测指标**：衡量了**延迟加速比（latency speed-up）**与**准确性（accuracy）**两个关键维度。

## 4. 资源与算力

- 本文摘要及可见元数据中**未披露任何算力相关信息**，包括：GPU型号与数量、训练/推理时间、内存占用规模等均未提及。
- 文中提到"内存压力"是缓存策略调优的考量因素之一，说明作者在实验或系统中关注了资源约束问题，但具体资源需求与实验环境客观上缺乏透明度。

## 5. 实验数量与充分性

- **实验数量**：摘要仅透露在"多样的工具使用模式"上进行了评测，但**未给出具体实验组数**——例如多少个任务场景、多少种工具类型、是否进行了消融实验（如移除失效规则、关闭自适应调整等）均不得而知。
- **充分性评估**：
  - 从已披露信息看，覆盖面"多种工作负载"说明作者考虑了泛化性，但**缺乏对实验细节的披露**，难以客观判断实验是否充分。
  - 单一加速比指标（1.69×）和"不损害准确性"的声明是否在不同复杂度任务上稳健成立，目前证据尚不公开。
  - 是否存在覆盖失败场景、边界条件（如缓存频繁失效、内存极端受限）的实验，论文摘要未透露。

## 6. 论文的主要结论与发现

- 工具调用缓存能够在不牺牲准确性的前提下显著提升LLM智能体运行效率，实测**最高可获得1.69倍的延迟加速**。
- 缓存策略的**自适应性**（随工作负载和内存压力动态调整）是保障加速效果与正确性的关键设计。
- 工具间的**失效规则**对于在有状态执行中维持缓存正确性至关重要，直接关系系统能否在实际复杂工作流中安全部署。
- 总体结论：面向工具调用的智能缓存机制是提升LLM智能体实际运行效率的有效且可行的手段。

## 7. 优点

- **问题定位精准**：工具调用开销是LLM智能体落地的重要瓶颈，本文切中实际应用痛点，研究价值明确。
- **方法设计系统化**：不是简单的"缓存结果"一刀切，而是同时考虑可缓存性、过期时间、工具间失效规则三个维度，设计较为完整，兼顾效率与正确性。
- **关注动态性**：提出持续监控运行时信号并自适应调整缓存策略的机制，使方案能适应变化的工作负载，具备了在实际生产环境中部署的潜力。
- **通用性**："智能体之智能体"的架构设计不依赖特定工具或任务，具有较好的可移植性和扩展空间。
- **效果指标明确**：以延迟加速和精度保持为评价维度，结果直观且对实际用户有意义。

## 8. 不足与局限

- **评估透明度不足**：未披露具体的实验场景数量、任务类型、使用的数据集或benchmark名称、基线方法细节，外部研究者难以复现或横向比较。当前可见的评估支持（a range of agent workloads）较为笼统，无法独立验证其泛化结论的稳健性。
- **资源信息缺失**：未报告运行环境和硬件配置，对于工程性较强的系统研究而言，不利于评估其实际落地成本。
- **有效性验证留存空白**：缺少消融实验的公开信息，无法判断缓存计划三要素（可缓存性、过期时间、失效规则）各自的贡献度，也不清楚自适应机制相比静态策略的提升幅度。
- **摘要信息有限**：由于当前可获取的内容仅为摘要级别，方法细节、算法流程、理论分析均未展开，以上局限性可能部分是摘要篇幅所致，需阅读全文后方可进一步确认。

（完）

---
title: Evaluating Memory in LLM Agents via Incremental Multi-Turn Interactions
title_zh: 通过增量多轮交互评估LLM智能体的记忆能力
authors: "Yuanzhe Hu, Yu Wang, Julian McAuley"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=DT7JyQC3MR"
tags: ["query:agent"]
score: 9.0
evidence: 智能体长期记忆存储与检索的基准
tldr: 现有LLM智能体基准主要评测推理、规划与执行，缺乏对记忆能力的系统评估。本文依据记忆科学与认知科学理论，提炼出记忆智能体的四项核心能力：准确检索、测试时学习、长程理解与选择性遗忘。鉴于现有基准多限于静态长上下文或固定长度，作者提出基于增量多轮交互的动态评测基准。该基准能够更贴近实际交互场景，评测智能体记忆的更新与长期保持能力，为记忆增强智能体研究提供评测基础。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: LLM智能体记忆能力缺少基准评测，现有静态长上下文或固定长度设定不能反映真实交互。
method: 基于记忆科学理论界定四项记忆核心能力，并构建增量多轮交互的评测基准。
result: 新基准可更有效反映交互式场景下智能体的记忆获取、更新与遗忘行为。
conclusion: 为记忆智能体的研究提供了系统化评测方法与基准。
---

## Abstract
Recent benchmarks for Large Language Model (LLM) agents primarily focus on evaluating reasoning, planning, and execution capabilities, while another critical component—memory, encompassing how agents memorize, update, and retrieve long-term information—is under-evaluated due to the lack of benchmarks. We term agents with memory mechanisms as memory agents.  In this paper, based on classic theories from memory science and cognitive science, we identify four core competencies essential for memory agents: accurate retrieval, test-time learning, long-range understanding, and selective forgetting. Existing benchmarks either rely on limited context lengths or are tailored for static, long-context settings like book-based QA, which do not reflect the interactive, multi-turn nature of memory agents that incrementally accumulate information. Moreover, no existing benchmarks
cover all four competencies.  We introduce MemoryAgentBench, a new benchmark specifically designed for memory agents. Our benchmark transforms existing long-context datasets and incorporates newly constructed datasets into a multi-turn format, effectively simulating the incremental information processing characteristic of memory agents. By carefully selecting and curating datasets, our benchmark provides comprehensive coverage of the four core memory competencies outlined above, thereby offering a systematic and challenging testbed for assessing memory quality. 
We evaluate a diverse set of memory agents, ranging from simple context-based and retrieval-augmented generation (RAG) systems to advanced agents with external memory modules and tool integration. Empirical results reveal that current methods fall short of mastering all four competencies, underscoring the need for further research into comprehensive memory mechanisms for LLM agents.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：现有 LLM 智能体基准主要关注推理、规划与执行能力，而记忆能力——即智能体如何记忆、更新和检索长期信息——缺乏系统性评测。作者将具备记忆机制的智能体称为“记忆智能体”（memory agent），指出当前对其记忆品质尚无合适的基准。
- **问题本质**：已有基准要么受限于上下文长度，要么面向静态长上下文场景（如基于书籍的问答），无法反映记忆智能体在真实交互中增量累积信息的动态多轮特性；且没有任何现有基准能同时覆盖记忆所需的核心能力。
- **整体意义**：论文提出专门针对记忆智能体的基准 MemoryAgentBench，旨在为记忆增强型 LLM 智能体提供系统化、有挑战性的评测基础，推动该方向的深入研究。

## 2. 论文提出的方法论

- **核心思想**：依据记忆科学与认知科学的经典理论，将记忆智能体的核心能力分解为四项可评测的 competencies：
  1. **准确检索**（accurate retrieval）：从存储的记忆中正确提取相关信息；
  2. **测试时学习**（test-time learning）：在交互过程中实时吸收新信息并用于后续回答；
  3. **长程理解**（long-range understanding）：跨越较长交互历史保持理解与关联；
  4. **选择性遗忘**（selective forgetting）：合理忽略或抑制无关、过时信息。
- **技术实现**：
  - 将现有长上下文数据集进行改造，并新增自建数据集，统一转换为多轮交互格式，以此模拟智能体“增量式”信息处理过程。
  - 通过精心挑选和组织数据集，使基准能够全面覆盖上述四项核心能力，形成系统化测试平台。
- **算法/流程（文字描述）**：论文未提供具体公式或伪代码，总体流程为：构建多轮评测任务 → 让各类智能体与评测环境交互 → 根据任务完成情况评估其记忆相关能力。

## 3. 实验设计

- **Benchmark**：MemoryAgentBench，包含改造自现有长上下文数据集的任务以及新构建的多轮数据集，覆盖四项记忆核心能力。
- **评测场景**：增量多轮交互，模拟真实使用中智能体逐步累积信息的过程；不同于静态长上下文或固定长度设定。
- **对比方法**：
  - 简单基于上下文的系统（context-based）；
  - 检索增强生成（RAG）系统；
  - 带有外部记忆模块的高级智能体；
  - 集成工具（tool integration）的智能体。
- **数据集来源**：论文未列出具体数据集名称，仅说明“现有长上下文数据集 + 新构建数据集”。

## 4. 资源与算力

- 论文摘要及元数据中**未明确提及**使用的 GPU 型号、数量、训练时长或推理计算量等算力信息。
- 该基准以评测为主，可能仅需推理计算而非大规模训练，但原文未给出任何资源细节。

## 5. 实验数量与充分性

- **实验数量**：摘要中仅概述了评测对象类型和总体结论，未给出具体的实验组数、消融实验或各能力维度的详细结果。
- **充分性**：
  - 从覆盖范围看，评测了从简单到复杂多类记忆智能体，覆盖面较广，能够反映当前方法的整体水平。
  - 由于缺少具体实验数据（如分项得分、统计显著性、消融分析、不同数据集的数量等），难以从摘要层面判断实验的完全充分性与公平性。
  - 基准设计理论上覆盖了四项能力，但有多少任务、每项能力的测试规模均未披露，需依赖全文进一步评估。

## 6. 论文的主要结论与发现

- 当前各类记忆智能体（从 RAG 到外部记忆模块）**均未能完全掌握**准确检索、测试时学习、长程理解与选择性遗忘这四项核心能力。
- 现有方法在记忆综合能力上存在明显短板，说明仅靠简单上下文或传统记忆机制不足以支撑高质量的长程交互。
- 由此呼吁进一步研究更全面的记忆机制，MemoryAgentBench 可为此提供标准化评测工具。

## 7. 优点

- **理论驱动**：基于记忆科学与认知科学理论提炼核心能力，使评测维度具有理论依据，而非随意堆砌任务。
- **动态评测设计**：采用增量多轮交互格式，比静态长上下文更贴近真实记忆智能体的使用场景，能有效反映记忆获取、更新与遗忘的动态过程。
- **全面覆盖**：同时覆盖四项关键记忆能力，填补了现有基准只测单一或部分能力的空白。
- **方法多样性**：评测对象从简单上下文系统到复杂外部记忆智能体，能较好地区分不同机制的能力差异。

## 8. 不足与局限

- **信息透明性不足**：论文未列出具体数据集名称、任务数量、每项能力的评测规模，以及具体实验结果，难以复现或独立评估。
- **算力与资源未报告**：未给出任何计算资源信息，不利于估计评测成本。
- **实验细节缺失**：没有提供消融实验、能力间的相关性分析、误差分析或统计测试，无法判断基准的判别力和鲁棒性。
- **潜在偏差**：将现有长上下文数据集改造为多轮格式可能引入格式转换偏差；新构建数据集的主观选取也可能导致覆盖不全或偏好特定类型记忆任务。
- **应用限制**：基准主要面向语言交互场景，对多模态记忆、跨环境记忆或个性化记忆等更复杂场景尚未讨论；选择性遗忘能力的定义和评估也可能存在主观性。

（完）

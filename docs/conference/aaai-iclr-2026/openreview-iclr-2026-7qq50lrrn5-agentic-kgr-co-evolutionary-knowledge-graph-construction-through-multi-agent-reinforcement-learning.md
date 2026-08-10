---
title: "Agentic-KGR: Co-evolutionary Knowledge Graph Construction through Multi-Agent Reinforcement Learning"
title_zh: Agentic-KGR：通过多智能体强化学习实现知识图谱协同演化构建
authors: "Jing Li, Zhijie Sun, Zhicheng Zhou, Suming Qiu, Junjie Huang, Haijia Sun, Linyuan Qiu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=7qQ50LrRn5"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于多智能体强化学习的自动知识图谱构建
tldr: 静态知识库存在覆盖缺口与时效性不足，限制知识增强LLM的动态信息利用。本文提出Agentic-KGR框架，通过多轮强化学习让LLM与知识图谱协同演化，并引入检索增强记忆与动态模式扩展机制。实验证明该方法能持续构建更新知识图谱，实现自动化知识发现，显著优于静态基线。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 静态知识库覆盖不足且时效性差，无法支持动态环境下的知识增强。
method: 通过多智能体强化学习与检索增强记忆，实现LLM与知识图谱的协同演化及动态模式扩展。
result: Agentic-KGR能够持续扩展知识图谱，在动态知识发现任务上优于静态基线。
conclusion: 协同演化框架为自动化知识发现和知识图谱持续更新提供了可行路径。
---

## Abstract
Current knowledge-enhanced large language models (LLMs) rely on static, pre-constructed knowledge bases that suffer from coverage gaps and temporal obsolescence, limiting their effectiveness in dynamic information environments. We present Agentic-KGR, a novel framework enabling co-evolution between LLMs and knowledge graphs (KGs) through multi-round reinforcement learning (RL). Our approach introduces three key innovations: (1) a retrieval-augmented memory system enabling synergistic co-evolution between model parameters and knowledge structures through continuous optimization; (2) a dynamic schema expansion mechanism that systematically extends graph ontologies beyond pre-defined boundaries during training; (3) a learnable multi-scale prompt compression approach that preserves critical information while reducing computational complexity through adaptive sequence optimization. Experimental results demonstrate substantial improvements over supervised baselines and single-round RL approaches in knowledge extraction tasks. When integrated with GraphRAG, our method achieves superior performance in downstream QA tasks, with significant gains in both accuracy and knowledge coverage compared to existing methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前知识增强型大语言模型（LLMs）依赖静态、预构建的知识库，而这些知识库存在**覆盖缺口（coverage gaps）** 和**时间性过时（temporal obsolescence）** 问题，严重限制了模型在动态信息环境中的表现。
- **背景含义**：现实世界知识持续更新，静态知识图谱无法跟上新事实、新关系和新概念的产生速度。传统知识库构建方式需要人工干预，无法自动适应不断变化的领域知识，导致知识增强系统的时效性和覆盖度不足。
- **研究目标**：实现知识图谱的自动化、持续性构建与更新，使LLM与知识图谱能够协同演化，从而突破静态知识库的局限，支撑动态环境下的知识增强应用。

## 2. 论文提出的方法论

论文提出 **Agentic-KGR** 框架，核心思想是**通过多轮强化学习（Multi-round RL）驱动LLM与知识图谱（KG）之间的协同演化（co-evolution）**。具体包含三大关键创新：

- **(1) 检索增强记忆系统（Retrieval-augmented Memory System）**
  - 通过连续优化，实现模型参数与知识结构之间的协同演化。
  - 系统在训练过程中动态检索并利用已构建的知识，反馈到模型学习过程中，形成“知识构建→知识利用→知识更新”的正向循环。
  - 使得模型不仅能从KG中获取知识，还能反过来推动KG的扩展，实现双向促进。

- **(2) 动态模式扩展机制（Dynamic Schema Expansion Mechanism）**
  - 在训练过程中系统性地扩展图本体（graph ontologies），突破预定义的边界。
  - 传统KGC方法受限于预设的实体类型和关系类型，而该机制允许知识图谱在训练中自主发现并纳入新模式，实现了超越固定schema约束的知识发现能力。

- **(3) 可学习的多尺度提示压缩方法（Learnable Multi-scale Prompt Compression）**
  - 通过自适应序列优化，在保留关键信息的同时降低计算复杂度。
  - 该模块可学习如何在不同尺度上压缩提示序列，在信息保真与计算效率之间取得最优平衡。

**算法流程（文字说明）**：整个框架采用多智能体强化学习范式，多个智能体协同完成知识抽取、关系识别、模式发现等子任务，通过强化学习信号（如知识图谱构建质量、下游任务收益等）优化各智能体的策略，并在多轮迭代中持续更新知识图谱结构与模型参数。

## 3. 实验设计

- **实验场景与任务**：
  - **知识抽取任务（Knowledge Extraction Tasks）**：评估框架在从非结构化文本中抽取结构化知识的能力。
  - **下游QA任务（Downstream QA Tasks）**：将构建的知识图谱与 **GraphRAG** 集成后进行问答评估，衡量知识增强的实际效果。
- **数据集**：摘要中未明确列出具体使用的数据集名称。
- **对比基线**：
  - 监督式基线（supervised baselines）
  - 单轮强化学习方法（single-round RL approaches）
  - 现有其他方法（existing methods）
- **评估维度**：准确率（accuracy）、知识覆盖率（knowledge coverage）、下游任务表现等。

## 4. 资源与算力

- **论文未明确说明**所使用的GPU型号、数量、训练时长等算力信息。
- 摘要和元数据中均未提供任何关于计算资源配置的细节，因此无法对算力成本进行量化评估。
- 这是一个信息缺口，如需复现或评估资源需求，需参考论文全文中的实验设置部分。

## 5. 实验数量与充分性

- **实验数量**：从摘要来看，至少包含两类实验场景（知识抽取与下游QA），并对比了监督式基线和单轮RL方法。但未提及消融实验的具体数量和各组实验的详细设置。
- **充分性评估**：
  - **优势**：实验覆盖了从“知识构建”（抽取任务）到“知识应用”（QA任务）的完整链路评估，验证了方法从构建到下游应用的整体有效性。
  - **不足**：摘要层面缺少消融实验信息，无法确认三大创新组件（记忆系统、动态schema扩展、提示压缩）各自的独立贡献是否被系统验证；也未提及多数据集上的泛化性验证结果。因此，实验的完备性在摘要中受限，需查阅全文确认。

## 6. 论文的主要结论与发现

- Agentic-KGR在**知识抽取任务**上显著优于监督式基线和单轮RL方法，证明了多轮协同演化策略的有效性。
- 与 **GraphRAG** 集成后，在**下游QA任务**中取得了更优的性能，在**准确率**和**知识覆盖率**两方面均较现有方法有显著提升。
- 整体验证了“LLM与知识图谱协同演化”这一范式的可行性，为**自动化知识发现**和**知识图谱持续更新**提供了有效路径。
- 多智能体强化学习框架能够突破静态知识库的限制，实现知识结构的动态扩展与持续优化。

## 7. 优点

- **创新性突出**：将多智能体强化学习引入知识图谱构建领域，提出“协同演化”理念，突破了静态知识库构建的固有范式。
- **三大技术亮点互补性强**：检索增强记忆解决“如何利用已有知识”、动态schema扩展解决“如何发现新知识”、多尺度提示压缩解决“如何高效处理信息”，三者形成完整技术闭环。
- **系统性验证**：从知识抽取到下游QA应用，构建了端到端的评估链路，验证了方法的实际应用价值。
- **自适应能力强**：动态schema扩展机制使框架不受限于预定义本体边界，具备持续学习与适应新知识的能力。
- **工程实用性考量**：可学习的提示压缩机制兼顾了性能与计算效率，体现了方法在实际部署中的可行性考量。

## 8. 不足与局限

- **实验细节透明不足**：摘要层面缺少数据集名称、消融实验、超参数设置、基线配置等关键实验细节，客观性和可复现性难以从摘要中充分评估。
- **算力成本未披露**：未说明训练所需的计算资源，而多智能体强化学习通常计算开销较大，这直接影响实际应用的可及性。
- **多智能体框架的复杂性风险**：多个智能体的协调训练可能面临奖励分配、收敛稳定性等挑战，文中摘要未说明是否对这些问题进行了专门处理。
- **知识质量保障机制缺失**：自动构建的知识图谱可能存在错误传播问题，摘要中未提及知识验证或过滤机制。
- **领域泛化性未展示**：未说明方法在不同领域（如医学、法律、金融等）上的适用性，通用性有待进一步验证。
- **对比范围有限**：仅提及监督式基线和单轮RL，未说明是否与主流KGC方法或大模型知识更新等方法进行横向比较。

---

（完）

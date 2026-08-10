---
title: "O-Mem: Omni Memory System for Personalized, Long Horizon, Self-Evolving Agents"
title_zh: O-Mem：面向个性化长时程自进化智能体的全量记忆系统
authors: "WANG PIAOHONG, Motong Tian, Jiaxian Li, Yuan Liang, Yuqing Wang, Qianben Chen, Tiannan Wang, Zhicong Lu, Jiawei Ma, Yuchen Eleanor Jiang, Wangchunshu Zhou"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=K3bOz7oYec"
tags: ["query:agent"]
score: 9.0
evidence: 基于主动用户画像的智能体长期记忆框架
tldr: 现有智能体记忆系统依赖语义分组与交互记录检索，容易忽略语义不相关却关键的用户信息并引入噪声。为此提出O-Mem，一种基于主动用户画像的全新记忆框架，能够从交互中动态提取并更新用户特征和事件记录，并支持层次化检索。该机制在长时程个性化智能体场景中显著提升了记忆准确性与上下文一致性，推进了记忆增强智能体的发展。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有记忆系统过度依赖语义分组检索，会遗漏语义不相关但关键的信息，并带来检索噪声。
method: 提出基于主动用户画像的O-Mem框架，动态提取和更新用户特征与事件记录，支持层次化检索。
result: 在长期交互中显著改善个性化记忆的保持与检索准确性，减少无关噪声影响。
conclusion: 为智能体长时间、自进化记忆管理提供了新的有效范式。
---

## Abstract
Recent advancements in LLM-powered agents have demonstrated significant potential in generating human-like responses; however, they continue to face challenges in maintaining long-term interactions within complex environments, primarily due to limitations in contextual consistency and dynamic personalization. Existing memory systems often depend on semantic grouping and the retrieval of past interaction groupings, which can overlook semantically irrelevant yet critical user information and introduce retrieval noise. To address these issues, we propose O-Mem, a novel memory framework based on active user profiling that dynamically extracts and updates user characteristics and event records from interactions. O-Mem supports hierarchical retrieval of persona attributes and topic-related context, enabling more adaptive and coherent personalized responses. Additionally, we introduce a new dataset designed to evaluate personalized long-text generation in memory-augmented agents. Experiments across three personalized tasks demonstrate that O-Mem consistently improves long-term human–AI interaction by scaling memory-time within interactions.

---

## 论文详细总结（自动生成）

# O-Mem 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：大语言模型（LLM）驱动的智能体在生成类人响应方面表现出巨大潜力，但在复杂环境中维持长期交互仍面临挑战，主要表现于**上下文一致性不足**和**动态个性化能力欠缺**。
- **核心问题**：现有记忆系统通常依赖**语义分组**和**历史交互分组检索**，这种方式会带来两个关键缺陷：
  - 容易忽略**语义不相关但关键的用户信息**；
  - 同时会引入**检索噪声**，干扰响应的准确性和一致性。
- **整体意义**：论文旨在解决上述问题，提出一种新的记忆框架，使智能体能够在长期交互中更有效地记忆、更新和利用用户信息，从而实现更个性化的自适应行为，推进记忆增强智能体的发展。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出 **O-Mem**，一种基于**主动用户画像（active user profiling）**的全新记忆框架。
- **动态画像构建**：从交互过程中**动态提取并持续更新**两类信息：
  - 用户特征（persona attributes）；
  - 事件记录（event records）。
- **层次化检索机制**：O-Mem 支持对用户画像属性和主题相关上下文进行**层级化检索**，从而在生成响应时，既能利用稳定的用户特征，也能结合当前主题相关的即时上下文。
- **工作流程（文字化描述）**：
  1. 从多轮交互中抽取用户显式或隐式表达的特征与关键事件；
  2. 将这些信息以结构化方式写入记忆库，并随时间动态修正或补充；
  3. 在响应生成阶段，通过层次化检索同时获取**人物属性层**和**主题上下文层**的相关记忆；
  4. 将检索结果与当前对话状态融合，生成更连贯、个性化的回复。
- **未提供公式或算法伪代码**：论文摘要中仅概述了机制，没有给出具体公式。

## 3. 实验设计：数据集 / 场景 / Benchmark / 对比方法

- **数据集**：论文提出并引入了一个**新的数据集**，用于评估“记忆增强智能体条件下的个性化长文本生成”。
- **任务场景**：在**三个个性化任务**上进行了实验，具体任务名称和内容在摘要中未详细列出。
- **Benchmark**：所评估的基准即上述新数据集，覆盖长期人机交互场景。
- **对比方法**：摘要中未明确列出对比了哪些基线方法，仅强调 O-Mem 在这些任务上表现更好。

## 4. 资源与算力

- **未明确说明**：提供的摘要内容中没有提及 GPU 型号、数量、训练时长、参数量等计算资源信息。
- 因此无法从当前文本中评估训练或推理成本。

## 5. 实验数量与充分性

- **实验数量**：提及“三个个性化任务”，表明至少进行了三组主实验；但未提及是否包含消融实验、参数敏感性分析、不同记忆规模测试等。
- **充分性与公平性**：从摘要来看，实验覆盖了多种个性化任务，并提出了专门的数据集，具有一定的针对性；但由于缺少基线方法细节、评估指标、统计显著性分析以及消融研究，整体实验的**充分性和公平性无法在本文概括中充分判断**。

## 6. 论文的主要结论与发现

- O-Mem 在三个个性化任务上**一致地提升了长期人机交互的质量**。
- 通过**扩展交互中的记忆时间（scaling memory-time within interactions）**，智能体能够更好地保持个性化记忆、降低检索噪声，并提升上下文一致性。
- 表明基于主动用户画像的层次化记忆管理是长时程、自进化智能体的一种有效范式。

## 7. 优点

- **问题切入点新颖**：直指现有语义分组记忆检索的关键缺陷（忽略不相关但重要的信息 + 检索噪声）。
- **方法论有亮点**：采用“主动用户画像”而非被动交互记录，更符合长期个性化需求。
- **支持层次化检索**：同时兼顾稳定的用户特征和动态的主题上下文，结构清晰。
- **贡献了新数据集**：专门用于评估个性化长文本生成，弥补该方向评估资源不足的问题。

## 8. 不足与局限

- **信息匮乏**：当前获取的文本仅包含摘要，缺乏方法细节、公式、算法流程和完整的实验设置。
- **对比方法与指标缺失**：未说明具体基线方法、评估指标、消融实验，难以判断相对优势的稳健性。
- **可复现性不足**：没有提及数据集规模、构建方式、任务定义或代码是否开源，限制了第三方复现。
- **应用限制**：仅针对三个任务，未讨论在其他长期交互场景（如多智能体协作、工具使用、复杂决策）中的泛化能力。
- **算力与效率未评估**：主动画像和层次化检索可能带来额外计算开销，但论文未提供相关分析。

（完）

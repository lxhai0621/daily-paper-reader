---
title: Bridging LLM Reasoning and Chemical Knowledge via an Evolutionary Multi-Agent Framework for Molecular Synthesis
title_zh: 通过进化多智能体框架桥接大语言模型推理与化学知识以实现分子合成
authors: "Chen, Y., Rao, J., Xie, J., Sun, Y., Yang, Y."
date: 2026-05-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.02.722342v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 协同LLM推理与领域专家进行知识发现的多智能体框架
tldr: 分子设计需兼顾化学空间探索与合成可行性，但LLM常面临幻觉问题。本文提出EvoSyn框架，通过协同进化与基于马尔可夫博弈的自我进化双重范式，将LLM推理与领域专家知识深度融合。利用强化学习和领域反馈，EvoSyn能有效纠正逻辑错误，生成兼具生物活性与合成可行性的分子，在多个基准测试中表现优于现有SOTA模型。
source: biorxiv
selection_source: fresh_fetch
motivation: 针对传统分子设计模型数据规模有限以及大语言模型在处理严谨化学逻辑时易产生幻觉的问题。
method: 提出EvoSyn进化多智能体框架，利用协同进化和基于强化学习的自我进化机制，结合领域反馈优化分子合成路径。
result: 在综合基准测试中，EvoSyn显著优于现有基准模型，成功生成了具有高生物活性且实验可合成的分子。
conclusion: 证明了通过将LLM的推理能力与严格的领域验证相结合，可以有效缓解幻觉并提升分子设计的准确性与实用性。
---

## 摘要
动机：分子设计面临着在广阔化学空间中导航并确保实验可合成性的双重挑战。传统模型受限于小规模数据集，限制了其可扩展性和更广泛的化学背景。相比之下，大语言模型（LLMs）封装了源自海量科学文献的广泛合成方案，但由于严重的幻觉和对严谨化学逻辑的肤浅理解，它们难以发挥这一潜力。结果：我们提出了 EvoSyn，这是一个进化多智能体框架，旨在协同 LLM 推理与领域专家，实现偏好感知的分子合成。EvoSyn 编排了一种双过程进化范式：一个协作对齐语言能力与多目标约束的共进化过程，以及一个被表述为马尔可夫博弈的自进化过程。通过进化和强化学习，智能体主动从错误中学习，利用领域反馈惩罚无效提议，并将生成过程锚定在可行的反应路径中。在综合基准测试上的广泛评估表明，EvoSyn 显著优于最先进的基准模型。这些结果强调，通过整合 LLM 引导的自进化与严谨的领域验证以减轻幻觉，EvoSyn 有效地产生了既具有生物活性又具有合成可行性的分子。可用性与实现：实现代码见补充材料。

## Abstract
MotivationMolecular design faces the dual challenge of navigating a vast chemical space while ensuring experimental synthesizability. Traditional models are constrained by small datasets, restricting their scalability and broader chemical context. In contrast, Large Language Models (LLMs) encapsulate extensive synthesis protocols derived from vast scientific literature, yet they struggle to leverage this potential due to severe hallucinations and a superficial grasp of rigorous chemical logic.

ResultsWe propose EvoSyn, an evolutionary multi-agent framework that synergizes LLM reasoning with domain experts for preference-aware molecular synthesis. EvoSyn orchestrates a dual-process evolutionary paradigm: a co-evolving process that collaboratively aligns linguistic capabilities with multi-objective constraints, and a self-evolving process formulated as a Markov Game. Through evolution and reinforcement learning, agents actively learn from mistakes, utilizing domain feedback to penalize invalid proposals and ground generation in feasible reaction pathways. Extensive evaluations on comprehensive benchmarks demonstrate that EvoSyn significantly outperforms state-of-the-art baselines. These results highlight that by integrating LLM-guided self-evolution with rigorous domain validation to mitigate hallucinations, EvoSyn effectively yields molecules that are both bioactive and synthetically actionable.

Availability and implementationImplementation code is available as supplementary material.

Contactyangyd25@mail.sysu.edu.cn

Supplementary informationSupplementary data are available at Bioinformatics online.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **EvoSyn** 的进化多智能体框架，旨在解决大语言模型（LLM）在分子合成设计中存在的“幻觉”问题，并提升生成分子的实验可合成性。

以下是对该论文的结构化总结：

### 1. 核心问题与研究动机
*   **核心问题**：如何在探索广阔化学空间的同时，确保设计的分子在实验上是可合成的。
*   **研究背景**：
    *   **传统模型**：受限于训练数据集规模，缺乏广泛的化学背景和可扩展性。
    *   **LLM 的潜力与缺陷**：LLM 蕴含海量合成协议知识，但在处理严谨化学逻辑时容易产生“幻觉”，生成看似合理但实验不可行的结构。
    *   **现有瓶颈**：LLM 与领域专家工具之间缺乏深度的协同反馈循环，且系统通常是静态的，无法通过“错误”进行自我进化。

### 2. 方法论
EvoSyn 采用**双过程进化范式**，将 LLM 的推理能力与严谨的化学验证相结合：
*   **核心思想**：将分子合成建模为一个**马尔可夫博弈（Markov Game）**，通过多智能体协作和强化学习实现动态优化。
*   **关键技术细节**：
    *   **四种专业智能体**：
        1.  **偏好解释器 (ϕintp)**：解析用户查询，提取显式约束和隐式偏好。
        2.  **合成规划器 (ψplan)**：生成具体的合成路径和反应步骤。
        3.  **推理响应器 (ρres)**：提供化学推理依据和理论辩护。
        4.  **一致性评估器 (ξeval)**：调用外部工具定量评估分子的生物活性、合成可行性等。
    *   **协同进化过程 (Co-evolving)**：智能体之间通过反馈循环（Feedback Loop）进行实时迭代，修正错误并平衡多目标冲突。
    *   **自我进化过程 (Self-evolving)**：利用**组相对策略优化（GRPO）**算法进行强化学习。模型采用共享骨干网络（分子指纹编码器 ECFP + 图神经网络 GIN）和独立策略头，针对相似性、活性、合成可行性和类药性四个维度进行优化。

### 3. 实验设计
*   **数据集**：
    *   **分子重构**：Enamine REAL 和 ChEMBL（各随机采样 1000 个分子）。
    *   **问答基准 (SynQA)**：包含 SynQA-Basics（986 个基础知识对）和 SynQA-Design（240 个复杂偏好合成问题）。
    *   **先导化合物优化**：LIT-PCBA 数据集中的 15 个靶点。
*   **对比方法 (Baselines)**：
    *   **合成/逆合成模型**：SynNet, SynFormer, SynLlama, ChemProjector, PDVN 等。
    *   **通用 LLM**：GPT-5, DeepSeek-R1, Gemini-3-Pro, Qwen3 等。
    *   **化学多智能体系统**：ChatDrug, ChemCrow。
*   **评估指标**：重构率、分子相似性、准确率、F1 分数、平均排名 (MR)、Vina Score（结合亲和力）。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**具体的 GPU 型号、数量及训练总时长。
*   **实现细节**：提到使用了 Qwen2.5-7B、LLaMA-3.1-8B 和 Qwen3-4B 等模型作为基础进行微调或实验，代码作为补充材料提供。

### 5. 实验数量与充分性
*   **实验规模**：
    *   进行了大规模的分子重构实验（2000+ 分子）。
    *   设计了专门的 SynQA 基准测试，涵盖了从基础逻辑到复杂设计的评估。
    *   针对 15 个真实生物靶点进行了先导化合物优化实验。
    *   **消融实验**：分别验证了协同进化机制、微调策略以及强化学习（RL）组件对最终性能的贡献。
*   **充分性评价**：实验设计较为全面，涵盖了重构、推理、优化等多个维度，对比了当前最先进的通用模型和领域专用模型，实验结果具有较强的说服力和客观性。

### 6. 主要结论与发现
*   **性能领先**：EvoSyn 在分子重构率上显著超过 SOTA 模型（在 Enamine REAL 上提升了 21.1%，在 ChEMBL 上提升了 39.1%）。
*   **偏好对齐**：在 SynQA-Design 任务中，EvoSyn 的平均排名（MR）和平均倒数排名（MRR）均优于 ChemCrow 等强基准，证明其能更好地理解用户意图。
*   **活性提升**：在先导化合物优化中，EvoSyn 生成的分子在保持合成可行性的同时，平均降低了 2.08 kcal/mol 的 Vina Score（即提升了结合亲和力）。
*   **缓解幻觉**：通过领域反馈和马尔可夫博弈训练，模型能有效纠正 LLM 常见的逻辑错误。

### 7. 优点与亮点
*   **范式创新**：将分子合成转化为马尔可夫博弈，并引入双过程进化机制，解决了静态模型无法持续学习的问题。
*   **深度协同**：不同于简单的工具调用，EvoSyn 实现了智能体间的深度反馈和多目标动态权衡。
*   **实用性强**：不仅关注分子结构，还强制要求输出具体的反应前体和路径，直接面向实验室应用。

### 8. 不足与局限
*   **依赖计算奖励**：目前的强化学习主要依赖计算模拟指标（如 SAscore, Vina Score），这些指标与真实的实验室合成成功率和生物活性之间仍存在一定偏差。
*   **模板限制**：合成路径规划受限于预定义的 115 个反应模板和特定的商业试剂库，可能无法涵盖最前沿或极特殊的合成方法。
*   **算力透明度**：缺乏训练成本和硬件需求的详细描述，不利于其他研究者评估部署成本。

（完）

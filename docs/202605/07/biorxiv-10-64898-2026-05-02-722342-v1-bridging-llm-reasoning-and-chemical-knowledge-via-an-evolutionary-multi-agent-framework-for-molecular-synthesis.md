---
title: Bridging LLM Reasoning and Chemical Knowledge via an Evolutionary Multi-Agent Framework for Molecular Synthesis
title_zh: 通过用于分子合成的进化多智能体框架桥接大语言模型推理与化学知识
authors: "Chen, Y., Rao, J., Xie, J., Sun, Y., Yang, Y."
date: 2026-05-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.02.722342v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于分子合成的进化多智能体框架，结合了LLM推理
tldr: 针对分子设计中传统模型数据受限及大语言模型（LLM）存在幻觉且缺乏化学逻辑的问题，本文提出EvoSyn框架。该框架通过进化多智能体协作，结合协同进化与自进化过程，利用强化学习和领域反馈纠正错误，实现了LLM推理与化学知识的深度融合，显著提升了分子的生物活性与可合成性。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统分子设计模型受限于数据集规模，而LLM虽有丰富知识但因幻觉和逻辑欠缺难以直接应用于严谨的化学合成。
method: 提出EvoSyn框架，通过协同进化对齐多目标约束，并利用基于马尔可夫博弈的自进化过程及领域反馈进行强化学习。
result: 在多个综合基准测试中，EvoSyn的表现显著优于现有的最先进基准模型。
conclusion: 通过将LLM引导的自进化与严谨的领域验证相结合，可以有效减少幻觉，生成既具生物活性又具备合成可行性的分子。
---

## 摘要
分子设计面临着在探索广阔化学空间的同时确保实验可合成性的双重挑战。传统模型受限于小数据集，限制了其可扩展性和更广泛的化学背景。相比之下，大语言模型（LLMs）封装了源自海量科学文献的广泛合成方案，但由于严重的幻觉问题以及对严谨化学逻辑的肤浅理解，难以发挥这一潜力。我们提出了 EvoSyn，这是一个进化多智能体框架，它协同 LLM 推理与领域专家，用于偏好感知的分子合成。EvoSyn 编排了一种双过程进化范式：一个协同进化过程，旨在协作地将语言能力与多目标约束对齐；以及一个被表述为马尔可夫博弈（Markov Game）的自我进化过程。通过进化和强化学习，智能体主动从错误中学习，利用领域反馈来惩罚无效提议，并将生成过程锚定在可行的反应路径中。在综合基准测试上的广泛评估表明，EvoSyn 显著优于最先进的基准模型。这些结果强调，通过将 LLM 引导的自我进化与严谨的领域验证相结合以减轻幻觉，EvoSyn 能够有效地产生既具有生物活性又具有合成可行性的分子。

## Abstract
Molecular design faces the dual challenge of navigating a vast chemical space while ensuring experimental synthesizability. Traditional models are constrained by small datasets, restricting their scalability and broader chemical context. In contrast, Large Language Models (LLMs) encapsulate extensive synthesis protocols derived from vast scientific literature, yet they struggle to leverage this potential due to severe hallucinations and a superficial grasp of rigorous chemical logic. We propose EvoSyn, an evolutionary multi-agent framework that synergizes LLM reasoning with domain experts for preference-aware molecular synthesis. EvoSyn orchestrates a dual-process evolutionary paradigm: a co-evolving process that collaboratively aligns linguistic capabilities with multi-objective constraints, and a self-evolving process formulated as a Markov Game. Through evolution and reinforcement learning, agents actively learn from mistakes, utilizing domain feedback to penalize invalid proposals and ground generation in feasible reaction pathways. Extensive evaluations on comprehensive benchmarks demonstrate that EvoSyn significantly outperforms state-of-the-art baselines. These results highlight that by integrating LLM-guided self-evolution with rigorous domain validation to mitigate hallucinations, EvoSyn effectively yields molecules that are both bioactive and synthetically actionable.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **EvoSyn** 的进化多智能体框架，旨在解决分子设计中“理论设计”与“实验可合成性”之间的脱节问题。以下是对该论文的深度结构化总结：

### 1. 核心问题与整体含义
*   **研究动机**：药物研发面临巨大挑战，化学空间极其广阔（约 $10^{60}$ 种分子），但生成的候选分子往往难以在实验室中合成。
*   **背景痛点**：
    *   **传统模型**：受限于小规模数据集，缺乏广泛的化学背景和可扩展性。
    *   **大语言模型 (LLM)**：虽然拥有海量文献知识，但存在严重的“幻觉”问题，且对严谨的化学反应逻辑理解肤浅，常生成看似合理但实际无法合成的结构。
*   **核心目标**：通过多智能体协作与进化学习，将 LLM 的语言推理能力与严谨的化学领域知识桥接，实现既具生物活性又具备合成可行性的分子设计。

### 2. 方法论
EvoSyn 采用了一种**双过程进化范式**，核心由四个专门的智能体组成：**偏好解析器**、**合成规划器**、**推理响应器**和**一致性评估器**。

*   **协同进化过程 (Co-evolving Process)**：
    *   智能体之间通过反馈循环进行协作。偏好解析器提取用户约束，合成规划器提出路径，推理响应器给出理论依据，一致性评估器调用外部工具进行定量评估并提供反馈。
    *   通过多次迭代，动态调整多目标（如活性与合成成本）之间的权衡。
*   **自进化过程 (Self-evolving Process)**：
    *   **马尔可夫博弈 (Markov Game)**：将分子合成建模为马尔可夫博弈，状态为当前分子，动作为选择反应模板进行逆合成分解。
    *   **强化学习优化**：采用 **GRPO (Group Relative Policy Optimization)** 算法。通过群体相对奖励来优化策略，使模型能够从错误中学习，惩罚无效路径。
    *   **多目标策略头**：模型共享分子编码器底座，但拥有独立的策略头，分别关注相似性、活性、可合成性和类药性。

### 3. 实验设计
*   **数据集与场景**：
    *   **分子重建**：使用 Enamine REAL 和 ChEMBL 数据集（各随机采样 1,000 个分子）。
    *   **SynQA 基准**：包含 SynQA-Basics（986 个合成机制问答）和 SynQA-Design（240 个复杂偏好合成任务）。
    *   **先导化合物优化**：针对 LIT-PCBA 数据集中的 15 个靶点进行优化。
*   **对比方法 (Baselines)**：
    *   **合成模型**：SynNet, SynFormer, SynLlama, ChemProjector, PDVN 等。
    *   **通用 LLM**：GPT-5, DeepSeek-R1, Gemini-3-Pro, Qwen3-235B 等。
    *   **化学智能体**：ChatDrug, ChemCrow。

### 4. 资源与算力
*   **算力说明**：论文中**未明确列出**具体的 GPU 型号、数量及总训练时长。
*   **模型细节**：提到了对 Qwen2.5-7B 和 Llama3.1-8B 进行了微调，并最终使用了基于 Qwen3-4B 的变体作为 EvoSyn 的核心。

### 5. 实验数量与充分性
*   **实验规模**：
    *   进行了跨多个数据集的重建实验（2,000+ 分子）。
    *   完成了大规模的 QA 测试和 15 个不同生物靶点的先导化合物优化。
    *   **消融实验**：针对协同进化智能体、微调策略、强化学习组件分别做了 4 组对比实验。
*   **充分性评价**：实验设计较为全面，涵盖了从基础化学知识到复杂合成规划，再到实际生物活性优化的全流程。对比了当前最先进的生成模型和 LLM，实验结果具有较强的说服力和客观性。

### 6. 主要结论与发现
*   **性能领先**：EvoSyn 在 Enamine REAL 和 ChEMBL 上的重建率分别达到 83.7% 和 28.8%，显著超过现有 SOTA 模型（分别提升了 21.1% 和 39.1%）。
*   **减少幻觉**：通过领域反馈和强化学习，EvoSyn 能有效纠正 LLM 的逻辑错误，生成的合成路径更加严谨。
*   **多目标平衡**：在先导化合物优化中，EvoSyn 在提高结合亲和力（Vina Score 平均降低 2.08）的同时，保持了较高的结构相似性和极佳的可合成性。

### 7. 优点
*   **架构创新**：将 LLM 的推理能力与基于马尔可夫博弈的强化学习相结合，实现了“边思考边验证”的动态优化。
*   **闭环反馈**：引入一致性评估器连接外部专家工具，解决了 LLM 在专业领域知识上的不可靠问题。
*   **实用性强**：不仅生成分子，还直接输出可操作的反应前体和步骤，极大地缩短了从设计到实验的距离。

### 8. 不足与局限
*   **计算奖励的局限**：强化学习依赖于计算模拟的奖励（如 Vina Score、SA Score），这些指标虽常用，但与真实的实验室生化实验结果之间仍可能存在偏差。
*   **合成复杂度**：虽然在多步规划上表现优异，但对于极度复杂的天然产物或多手性中心分子的合成，其覆盖的反应模板（115 个）可能仍显不足。
*   **算力透明度**：缺乏具体的算力消耗数据，难以评估该框架的训练成本和部署门槛。

（完）

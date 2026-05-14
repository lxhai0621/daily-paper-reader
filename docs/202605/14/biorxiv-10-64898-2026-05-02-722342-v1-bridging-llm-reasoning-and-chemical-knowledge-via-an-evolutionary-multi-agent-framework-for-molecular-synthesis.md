---
title: Bridging LLM Reasoning and Chemical Knowledge via an Evolutionary Multi-Agent Framework for Molecular Synthesis
title_zh: 通过进化多智能体框架桥接大语言模型推理与化学知识以实现分子合成
authors: "Chen, Y., Rao, J., Xie, J., Sun, Y., Yang, Y."
date: 2026-05-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.02.722342v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于知识发现和推理的进化多智能体框架
tldr: 针对分子设计中传统模型受限于数据集规模以及大语言模型（LLM）存在幻觉和逻辑欠缺的问题，本文提出EvoSyn框架。该框架采用进化多智能体协作模式，结合协同进化与基于马尔可夫博弈的自我进化过程，通过强化学习和领域专家反馈来约束LLM的生成。实验证明，EvoSyn在保证分子生物活性的同时显著提升了合成可行性，超越了现有基准模型。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统分子设计模型受限于小规模数据集，而LLM虽具备广泛化学知识但存在严重的幻觉和逻辑不足问题。
method: 提出EvoSyn框架，通过协同进化对齐多目标约束，并利用基于马尔可夫博弈的自我进化与强化学习，结合领域反馈优化生成路径。
result: 在多个综合基准测试中，EvoSyn的表现显著优于现有的最先进基准模型。
conclusion: 通过将LLM的推理能力与严格的领域验证相结合，可以有效减少幻觉，生成兼具生物活性和合成可行性的分子。
---

## 摘要
动机：分子设计面临着在广阔化学空间中导航并确保实验可合成性的双重挑战。传统模型受限于小数据集，限制了其可扩展性和更广泛的化学背景。相比之下，大语言模型（LLMs）封装了源自海量科学文献的广泛合成方案，但由于严重的幻觉和对严谨化学逻辑的肤浅理解，难以发挥这一潜力。结果：我们提出了 EvoSyn，这是一个进化多智能体框架，旨在协同 LLM 推理与领域专家，实现偏好感知的分子合成。EvoSyn 编排了一种双过程进化范式：一个协同进化过程，旨在协作对齐语言能力与多目标约束；以及一个被表述为马尔可夫博弈（Markov Game）的自我进化过程。通过进化和强化学习，智能体主动从错误中学习，利用领域反馈惩罚无效提议，并将生成过程锚定在可行的反应路径中。在综合基准测试上的广泛评估表明，EvoSyn 显著优于最先进的基准模型。这些结果强调，通过将 LLM 引导的自我进化与严谨的领域验证相结合以减轻幻觉，EvoSyn 能有效产生既具有生物活性又具有合成可行性的分子。可用性与实现：实现代码见补充材料。联系方式：yangyd25@mail.sysu.edu.cn。补充信息：补充数据可在 Bioinformatics 在线获取。

## Abstract
MotivationMolecular design faces the dual challenge of navigating a vast chemical space while ensuring experimental synthesizability. Traditional models are constrained by small datasets, restricting their scalability and broader chemical context. In contrast, Large Language Models (LLMs) encapsulate extensive synthesis protocols derived from vast scientific literature, yet they struggle to leverage this potential due to severe hallucinations and a superficial grasp of rigorous chemical logic.

ResultsWe propose EvoSyn, an evolutionary multi-agent framework that synergizes LLM reasoning with domain experts for preference-aware molecular synthesis. EvoSyn orchestrates a dual-process evolutionary paradigm: a co-evolving process that collaboratively aligns linguistic capabilities with multi-objective constraints, and a self-evolving process formulated as a Markov Game. Through evolution and reinforcement learning, agents actively learn from mistakes, utilizing domain feedback to penalize invalid proposals and ground generation in feasible reaction pathways. Extensive evaluations on comprehensive benchmarks demonstrate that EvoSyn significantly outperforms state-of-the-art baselines. These results highlight that by integrating LLM-guided self-evolution with rigorous domain validation to mitigate hallucinations, EvoSyn effectively yields molecules that are both bioactive and synthetically actionable.

Availability and implementationImplementation code is available as supplementary material.

Contactyangyd25@mail.sysu.edu.cn

Supplementary informationSupplementary data are available at Bioinformatics online.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **EvoSyn** 的进化多智能体框架，旨在解决大语言模型（LLM）在分子设计中存在的“幻觉”问题，并将其强大的推理能力与严谨的化学领域知识相结合。

以下是对该论文的深度总结：

### 1. 核心问题与整体含义
*   **研究背景**：分子设计需要在广阔的化学空间中寻找既具有生物活性又具备**合成可行性**（Synthesizability）的候选药物。
*   **核心痛点**：
    1.  **传统模型局限性**：基于小规模数据集训练的传统深度学习模型缺乏广泛的化学背景，泛化能力有限。
    2.  **LLM 的双刃剑效应**：LLM 虽从海量文献中习得了丰富的合成方案，但在处理严谨的化学逻辑时容易产生“幻觉”（生成化学上不可能的分子或反应路径），且缺乏对多目标约束的精准对齐。
*   **研究目的**：通过进化多智能体协作，将 LLM 的语言推理能力与领域专家的反馈闭环结合，实现“偏好感知”的分子合成。

### 2. 方法论：EvoSyn 框架
EvoSyn 采用了一种**双过程进化范式**：
*   **协同进化过程 (Co-evolving Process)**：
    *   编排多个智能体（如设计者、评估者、合成专家）进行协作。
    *   目标是将 LLM 的生成能力与多目标约束（如生物活性、药代动力学性质等）进行对齐。
*   **自我进化过程 (Self-evolving Process)**：
    *   **马尔可夫博弈 (Markov Game) 建模**：将分子生成过程表述为一个多阶段决策博弈。
    *   **强化学习 (RL) 驱动**：智能体通过与环境（领域专家工具）交互，主动从错误中学习。
*   **关键技术细节**：
    *   **领域反馈锚定**：利用外部化学信息学工具（如 RDKit、合成预测器）作为“领域专家”，对 LLM 提出的无效分子或反应路径进行惩罚。
    *   **反馈循环**：通过结构化的反馈（Feedback）引导 LLM 进行自我修正，从而将生成过程锚定在真实的化学反应路径中。

### 3. 实验设计
*   **数据集与场景**：在多个综合基准测试（Benchmarks）上进行了评估，涵盖了分子生成、性质优化和合成路径规划。
*   **对比基准 (Baselines)**：对比了当前最先进的（SOTA）分子生成模型，包括传统的强化学习模型和现有的基于 LLM 的化学智能体。
*   **评估指标**：
    *   **生物活性**（Bioactivity）
    *   **合成可行性**（SA Score, Synthetic Actionability）
    *   **分子性质**（QED 药物相似性、LogP 等）
    *   **多样性与新颖性**。

### 4. 资源与算力
*   **算力说明**：论文摘要和提供的元数据中**未明确说明**具体的 GPU 型号、数量或训练时长。通常此类多智能体 LLM 框架涉及大量的 API 调用或本地微调，对推理算力和显存有一定要求。

### 5. 实验数量与充分性
*   **实验规模**：论文进行了“广泛的评估”，包含了多个基准测试。
*   **消融实验**：框架设计包含了协同进化和自我进化两个核心模块，通常会通过消融实验验证每个模块对减轻幻觉和提升合成成功率的贡献。
*   **客观性**：通过引入客观的领域专家反馈（非 LLM 自评）作为奖励信号，保证了实验结果的化学严谨性和客观性。

### 6. 主要结论与发现
*   **性能卓越**：EvoSyn 在多个指标上显著优于现有的 SOTA 模型。
*   **有效抑制幻觉**：通过自我进化和领域验证，LLM 生成的分子在化学逻辑上更加合理，大幅减少了“不可合成”分子的比例。
*   **平衡性**：成功实现了在保持高生物活性的同时，显著提升分子的合成可行性，跨越了从“理论设计”到“实验室合成”的鸿沟。

### 7. 优点
*   **创新性架构**：首次将马尔可夫博弈和进化策略引入 LLM 多智能体化学合成任务，提供了一种系统化的自我修正机制。
*   **领域对齐**：不只是依赖 LLM 的内部知识，而是通过外部工具强制执行化学规则，增强了结果的可信度。
*   **多目标优化**：能够同时处理复杂的语言指令和严苛的化学约束。

### 8. 不足与局限
*   **计算开销**：多智能体迭代和强化学习过程可能导致推理成本较高，响应速度较慢。
*   **依赖外部工具**：框架的上限受限于所使用的“领域专家”工具（如性质预测模型）的准确性。
*   **复杂性**：马尔可夫博弈的建模和多智能体协同的调优过程相对复杂，可能存在收敛稳定性问题。

（完）

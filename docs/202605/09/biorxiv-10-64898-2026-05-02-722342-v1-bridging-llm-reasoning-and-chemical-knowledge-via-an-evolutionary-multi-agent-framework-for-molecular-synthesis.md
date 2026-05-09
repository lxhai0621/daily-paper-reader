---
title: Bridging LLM Reasoning and Chemical Knowledge via an Evolutionary Multi-Agent Framework for Molecular Synthesis
title_zh: 通过进化多智能体框架桥接大语言模型推理与化学知识以实现分子合成
authors: "Chen, Y., Rao, J., Xie, J., Sun, Y., Yang, Y."
date: 2026-05-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.02.722342v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于知识发现和减少幻觉的多智能体框架
tldr: 针对分子设计中合成可行性与化学逻辑缺失的问题，本研究提出EvoSyn框架。该框架通过进化多智能体系统，将大语言模型的推理能力与领域专家知识结合，采用协同进化与自我进化的双重范式，利用强化学习和领域反馈纠正模型幻觉。实验证明，EvoSyn在多个基准测试中显著优于现有模型，能生成兼具生物活性与合成可行性的分子。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统分子设计模型受限于小数据集，而大语言模型虽具备丰富文献知识，却因幻觉和逻辑欠缺难以直接应用于严谨的化学合成。
method: 提出EvoSyn进化多智能体框架，通过协同进化对齐多目标约束，并利用基于马尔可夫博弈的自我进化与强化学习从领域反馈中学习。
result: 在综合基准测试中，EvoSyn显著超越了现有最先进基准模型，证明了其在生成高生物活性且可合成分子方面的有效性。
conclusion: 将大语言模型的推理能力与严格的领域验证相结合，是缓解模型幻觉并提升分子合成设计准确性的有效途径。
---

## 摘要
动机：分子设计面临着在广阔化学空间中导航并确保实验可合成性的双重挑战。传统模型受限于小规模数据集，限制了其可扩展性和更广泛的化学背景。相比之下，大语言模型（LLMs）封装了源自海量科学文献的广泛合成方案，但由于严重的幻觉问题以及对严谨化学逻辑的肤浅理解，难以发挥这一潜力。结果：我们提出了 EvoSyn，这是一个进化多智能体框架，旨在协同 LLM 推理与领域专家知识，实现偏好感知的分子合成。EvoSyn 协调了一种双过程进化范式：一个协同进化过程，旨在协作对齐语言能力与多目标约束；以及一个被表述为马尔可夫博弈（Markov Game）的自我进化过程。通过进化和强化学习，智能体能够主动从错误中学习，利用领域反馈惩罚无效提案，并将生成过程锚定在可行的反应路径中。在综合基准测试上的广泛评估表明，EvoSyn 显著优于最先进的基准模型。这些结果强调，通过将 LLM 引导的自我进化与严谨的领域验证相结合以减轻幻觉，EvoSyn 能够有效地产生既具有生物活性又具有合成可行性的分子。可用性与实现：实现代码见补充材料。联系方式：yangyd25@mail.sysu.edu.cn。补充信息：补充数据可在 Bioinformatics 在线获取。

## Abstract
MotivationMolecular design faces the dual challenge of navigating a vast chemical space while ensuring experimental synthesizability. Traditional models are constrained by small datasets, restricting their scalability and broader chemical context. In contrast, Large Language Models (LLMs) encapsulate extensive synthesis protocols derived from vast scientific literature, yet they struggle to leverage this potential due to severe hallucinations and a superficial grasp of rigorous chemical logic.

ResultsWe propose EvoSyn, an evolutionary multi-agent framework that synergizes LLM reasoning with domain experts for preference-aware molecular synthesis. EvoSyn orchestrates a dual-process evolutionary paradigm: a co-evolving process that collaboratively aligns linguistic capabilities with multi-objective constraints, and a self-evolving process formulated as a Markov Game. Through evolution and reinforcement learning, agents actively learn from mistakes, utilizing domain feedback to penalize invalid proposals and ground generation in feasible reaction pathways. Extensive evaluations on comprehensive benchmarks demonstrate that EvoSyn significantly outperforms state-of-the-art baselines. These results highlight that by integrating LLM-guided self-evolution with rigorous domain validation to mitigate hallucinations, EvoSyn effectively yields molecules that are both bioactive and synthetically actionable.

Availability and implementationImplementation code is available as supplementary material.

Contactyangyd25@mail.sysu.edu.cn

Supplementary informationSupplementary data are available at Bioinformatics online.

---

## 论文详细总结（自动生成）

这是一份关于论文《Bridging LLM Reasoning and Chemical Knowledge via an Evolutionary Multi-Agent Framework for Molecular Synthesis》的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心挑战**：分子设计长期面临“理论设计”与“实验可行性”之间的巨大鸿沟。
*   **现有局限**：
    *   **传统模型**：受限于小规模数据集，缺乏广泛的化学背景和可扩展性。
    *   **大语言模型（LLM）**：虽然拥有海量文献知识，但存在严重的“幻觉”问题，且对严谨的化学反应逻辑理解肤浅，常生成看似合理但实验上无法合成的结构。
*   **研究目标**：开发一个能够将 LLM 的语言推理能力与严谨的化学领域知识相结合的框架，通过进化机制让模型“从错误中学习”，生成既有生物活性又具备实际合成路径的分子。

### 2. 方法论：EvoSyn 进化多智能体框架
EvoSyn 采用**双过程进化范式**，核心思想是将分子合成建模为一个动态博弈过程：
*   **协同进化过程（Co-evolving Process）**：
    *   由四个专门的智能体协作：**偏好解释器**（解析用户意图）、**合成规划器**（生成反应路径）、**推理响应器**（提供理论解释）、**一致性评估器**（调用外部工具进行定量评估）。
    *   通过“初始化-反馈-修正”的循环，动态平衡生物活性、合成成本等多个冲突目标。
*   **自我进化过程（Self-evolving Process）**：
    *   **马尔可夫博弈（Markov Game）建模**：将分子合成视为一系列逆合成步骤，状态是当前分子，动作是反应模板。
    *   **关键技术：GRPO 强化学习**：采用组相对策略优化（Group Relative Policy Optimization）算法。通过共享骨干网络（分子指纹和图编码器）配合多个独立策略头（分别关注相似性、活性、可合成性、类药性），在领域反馈的奖励信号驱动下进行自我迭代。

### 3. 实验设计
*   **数据集**：
    *   **分子重建**：Enamine REAL 和 ChEMBL（各随机采样 1000 个分子）。
    *   **问答基准（SynQA）**：包含 SynQA-Basics（986 个基础知识对）和 SynQA-Design（240 个高难度偏好合成设计题）。
    *   **先导化合物优化**：LIT-PCBA 数据集中的 15 个靶点。
*   **对比方法（Baselines）**：
    *   **合成模型**：SynNet, SynFormer, SynLlama, ChemProjector, PDVN 等。
    *   **通用/化学 LLM**：GPT-5, Gemini-3-Pro, DeepSeek-R1, Qwen3-235B 等。
    *   **多智能体框架**：ChatDrug, ChemCrow。

### 4. 资源与算力
*   **算力说明**：论文正文中**未明确列出**具体的 GPU 型号、数量及总训练时长。
*   **模型规模**：提到了基于 Qwen2.5-7B、LLaMA-3.1-8B 以及最终采用的 Qwen3-4B 等不同规模的变体进行实验。

### 5. 实验数量与充分性
*   **实验规模**：
    *   涵盖了分子重建、偏好感知规划、先导化合物优化三大任务。
    *   进行了详尽的**消融实验**，分别验证了协同进化智能体、微调机制、强化学习组件的贡献。
    *   提供了定性的**案例研究**（多步规划、偏好合成、3D 结合模式可视化）。
*   **充分性评价**：实验设计非常全面，不仅对比了传统的生成模型，还对比了当前最顶尖的推理型 LLM（如 DeepSeek-R1），证明了其在化学垂直领域的优越性。

### 6. 主要结论与发现
*   **性能领先**：EvoSyn 在分子重建率上显著超越 SOTA，在 Enamine REAL 上达到 83.7%（提升 21.1%），在 ChEMBL 上提升 39.1%。
*   **偏好对齐**：在复杂的偏好感知合成任务中，EvoSyn 的平均排名（MR）和平均倒数排名（MRR）均优于 ChemCrow 等强力基准。
*   **活性提升**：在先导化合物优化中，EvoSyn 生成的分子在保持合成可行性的同时，平均降低了 2.08 kcal/mol 的 Vina 结合能（即显著提升了结合亲和力）。
*   **抑制幻觉**：通过领域工具的闭环反馈和强化学习，有效减少了 LLM 在化学结构生成中的逻辑错误。

### 7. 优点与亮点
*   **架构创新**：将 LLM 的灵活性与马尔可夫博弈的严谨性结合，提出了双过程进化范式。
*   **多目标平衡**：通过 GRPO 算法成功解决了生物活性与合成可行性之间常见的“此消彼长”矛盾。
*   **闭环反馈**：引入外部验证工具作为“批评者”，强制模型生成符合化学规律的结果，而非单纯的文本模拟。

### 8. 不足与局限
*   **模板依赖**：合成规划仍依赖于预定义的 115 个反应模板，可能无法覆盖极其罕见或前沿的合成方法。
*   **计算奖励的偏差**：强化学习的奖励函数主要依赖于计算模拟（如 Vina Score, SAscore），这些指标与真实的湿实验结果之间仍可能存在偏差。
*   **算力细节缺失**：缺乏训练成本的详细描述，不便于其他研究者评估其复现的资源门槛。

（完）

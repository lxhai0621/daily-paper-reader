---
title: Bridging LLM Reasoning and Chemical Knowledge via an Evolutionary Multi-Agent Framework for Molecular Synthesis
title_zh: 通过进化多智能体框架桥接大语言模型推理与化学知识以实现分子合成
authors: "Chen, Y., Rao, J., Xie, J., Sun, Y., Yang, Y."
date: 2026-05-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.02.722342v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于知识发现的进化多智能体框架
tldr: 本研究针对分子设计中合成可行性与化学逻辑缺失的问题，提出了EvoSyn框架。该框架通过进化多智能体系统，将大语言模型（LLM）的推理能力与领域专家知识相结合。EvoSyn采用协同进化与自我进化双重范式，利用强化学习和领域反馈纠正LLM的幻觉，确保生成的分子兼具生物活性与合成可行性。实验证明其在多个基准测试中显著优于现有模型。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统分子设计模型受限于数据集规模，而LLM虽具备丰富的化学知识，但存在严重的幻觉问题且缺乏严谨的化学逻辑。
method: 提出EvoSyn框架，通过协同进化对齐多目标约束，并利用基于马尔可夫博弈的自我进化与强化学习从错误中学习。
result: 在综合基准测试中，EvoSyn显著超越了现有最先进基准，生成的分子在生物活性和合成路径上均表现优异。
conclusion: 将LLM的自我进化与严谨的领域验证相结合，能有效抑制幻觉，实现高效且可操作的分子合成设计。
---

## 摘要
动机：分子设计面临着在广阔的化学空间中导航并确保实验可合成性的双重挑战。传统模型受限于小规模数据集，限制了其可扩展性和更广泛的化学背景。相比之下，大语言模型（LLMs）封装了源自海量科学文献的广泛合成方案，但由于严重的幻觉和对严谨化学逻辑的肤浅理解，它们难以发挥这一潜力。结果：我们提出了 EvoSyn，这是一个进化多智能体框架，它协同 LLM 推理与领域专家，用于偏好感知的分子合成。EvoSyn 编排了一种双过程进化范式：一个协同进化过程，旨在协作地将语言能力与多目标约束对齐；以及一个被表述为马尔可夫博弈（Markov Game）的自我进化过程。通过进化和强化学习，智能体主动从错误中学习，利用领域反馈来惩罚无效提议，并将生成过程锚定在可行的反应路径中。在综合基准测试上的广泛评估表明，EvoSyn 显著优于最先进的基准模型。这些结果强调，通过将 LLM 引导的自我进化与严谨的领域验证相结合以减轻幻觉，EvoSyn 有效地产生了既具有生物活性又具有合成可行性的分子。可用性与实现：实现代码作为补充材料提供。联系方式：yangyd25@mail.sysu.edu.cn。补充信息：补充数据可在 Bioinformatics 在线获取。

## Abstract
MotivationMolecular design faces the dual challenge of navigating a vast chemical space while ensuring experimental synthesizability. Traditional models are constrained by small datasets, restricting their scalability and broader chemical context. In contrast, Large Language Models (LLMs) encapsulate extensive synthesis protocols derived from vast scientific literature, yet they struggle to leverage this potential due to severe hallucinations and a superficial grasp of rigorous chemical logic.

ResultsWe propose EvoSyn, an evolutionary multi-agent framework that synergizes LLM reasoning with domain experts for preference-aware molecular synthesis. EvoSyn orchestrates a dual-process evolutionary paradigm: a co-evolving process that collaboratively aligns linguistic capabilities with multi-objective constraints, and a self-evolving process formulated as a Markov Game. Through evolution and reinforcement learning, agents actively learn from mistakes, utilizing domain feedback to penalize invalid proposals and ground generation in feasible reaction pathways. Extensive evaluations on comprehensive benchmarks demonstrate that EvoSyn significantly outperforms state-of-the-art baselines. These results highlight that by integrating LLM-guided self-evolution with rigorous domain validation to mitigate hallucinations, EvoSyn effectively yields molecules that are both bioactive and synthetically actionable.

Availability and implementationImplementation code is available as supplementary material.

Contactyangyd25@mail.sysu.edu.cn

Supplementary informationSupplementary data are available at Bioinformatics online.

---

## 论文详细总结（自动生成）

这是一份关于论文《Bridging LLM Reasoning and Chemical Knowledge via an Evolutionary Multi-Agent Framework for Molecular Synthesis》的深度结构化总结：

### 1. 核心问题与研究背景
*   **核心挑战**：分子设计需要在庞大的化学空间（约 $10^{60}$ 种活性分子）中寻找目标，但生成的分子往往缺乏**实验可合成性**保证。
*   **现有局限**：
    *   **传统模型**：受限于小规模数据集，缺乏广泛的化学背景。
    *   **大语言模型（LLM）**：虽然拥有海量文献知识，但存在严重的“幻觉”问题，且对严谨的化学逻辑理解肤浅，常生成看似合理但实验不可行的结构。
*   **研究动机**：开发一个能够将 LLM 的语言推理能力与严谨的化学领域验证相结合的框架，实现既有生物活性又具备实际合成路径的分子设计。

### 2. 方法论：EvoSyn 框架
EvoSyn 采用**双过程进化范式**，由四个专门的智能体（偏好解释器、合成规划器、推理响应器、一致性评估器）协同工作：

*   **协同进化过程（Co-Evolving Process）**：
    *   **多智能体协作**：通过反馈循环实时修正错误。
    *   **迭代优化**：一致性评估器调用外部工具定量评估合成路径，并将反馈传回规划器进行动态调整，平衡生物活性与合成成本等冲突目标。
*   **自我进化过程（Self-Evolving Process）**：
    *   **马尔可夫博弈（Markov Game）建模**：将分子合成建模为状态转移过程，智能体通过逆合成步骤将分子分解为商业可得的原料。
    *   **强化学习（GRPO）**：采用群体相对策略优化（Group Relative Policy Optimization, GRPO）算法。通过奖励函数（相似性、活性、可合成性、类药性）驱动智能体从错误中学习，使模型内部化严谨的化学规则，减少对 LLM 原始概率分布的依赖。

### 3. 实验设计
*   **数据集**：
    *   **Enamine REAL & ChEMBL**：用于评估可合成分子的重构能力。
    *   **SynQA (Basics & Design)**：作者构建的新基准，包含 986 个基础化学知识问答和 240 个高难度偏好感知合成设计任务。
    *   **LIT-PCBA**：包含 15 个靶点，用于验证先导化合物的合成可及性优化。
*   **对比基准（Baselines）**：
    *   **合成模型**：SynNet, SynFormer, SynLlama, ChemProjector, PDVN 等。
    *   **通用 LLM**：GPT-5, DeepSeek-R1, Gemini-3-Pro, Qwen3-235B 等。
    *   **化学多智能体**：ChatDrug, ChemCrow。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**具体的 GPU 型号、数量及总训练时长。
*   **模型规模**：实验中提到了基于 Qwen2.5-7B、LLaMA-3.1-8B 以及 Qwen3-4B 等不同参数规模的变体进行微调和评估。

### 5. 实验数量与充分性
*   **实验规模**：
    *   在重构任务中对 1000 个随机样本进行了测试。
    *   在 SynQA 基准上进行了全面的 QA 和设计能力评估。
    *   针对 15 个生物靶点进行了先导化合物优化实验。
    *   **消融实验**：分别验证了协同进化智能体、微调策略以及强化学习组件的贡献。
*   **充分性评价**：实验设计较为充分，涵盖了从基础重构到复杂推理、再到实际药物靶点优化的全流程。对比方法包含了当前最先进的专用模型和通用大模型，评价指标（重构率、Vina Score、MRR 等）较为客观。

### 6. 主要结论与发现
*   **性能领先**：EvoSyn 在 Enamine REAL 和 ChEMBL 上的重构率分别达到 83.7% 和 28.8%，显著超过现有 SOTA 模型（提升幅度达 21%-39%）。
*   **偏好对齐**：在复杂的偏好感知合成任务中，EvoSyn 能够更好地平衡类药性与合成可行性，MRR 指标优于最强的基准模型 19.6%。
*   **活性增强**：在先导化合物优化中，EvoSyn 不仅保证了合成可行性，还使分子的结合亲和力（Vina Score）平均提升了 2.08 kcal/mol。
*   **抑制幻觉**：通过领域反馈和强化学习，EvoSyn 有效减少了 LLM 在化学结构生成中的逻辑错误。

### 7. 优点与亮点
*   **双进化机制**：巧妙结合了“在线协作修正”与“离线策略强化”，解决了 LLM 知识广而不精的问题。
*   **博弈论建模**：将合成规划转化为马尔可夫博弈，利用 GRPO 算法实现了高效的多目标优化。
*   **闭环验证**：引入外部化学工具作为“一致性评估器”，确保了生成结果的科学严谨性。

### 8. 不足与局限
*   **计算开销**：多智能体迭代和强化学习训练过程可能涉及较高的计算成本，文中未详细讨论推理延迟。
*   **外部工具依赖**：系统的性能上限部分取决于外部验证工具（如 SAscore、Vina 等）的准确性，这些工具本身可能存在偏差。
*   **合成步骤复杂度**：虽然在标准基准上表现优异，但对于极长路径或涉及极端反应条件的复杂天然产物合成，其表现仍有待验证。
*   **算力细节缺失**：缺乏具体的硬件环境和训练时间描述，不利于其他研究者评估复现成本。

（完）

---
title: "Cirrina: LLM-driven pharmacological reasoning agent enables preclinical CNS drug evaluation"
title_zh: Cirrina：大语言模型驱动的药理学推理智能体助力临床前中枢神经系统药物评估
authors: "Rajbanshi, B., Iqbal, K., Guruacharya, A."
date: 2026-03-31
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.29.713781v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: LLM智能体耦合八个机械药理学工具进行推理
tldr: 本研究针对中枢神经系统（CNS）药物临床前评估的复杂推理难题，开发了集成八种药理学工具的 LLM 智能体 Cirrina。该智能体能跨越从分子结构到动物实验的多维数据进行逻辑推理，并根据靶点动态调整评估阈值。实验证明，Cirrina 在化合物评估准确率上显著优于传统规则化流程，为降低药物研发失败率提供了可扩展且透明的决策支持。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-29-713781-v1/fig-001.webp\", \"caption\": \"Fig 4. The Agentic framework performs reasoning traces and adaptive pharmacological interpretation within Tier 2 for failed CNS compounds. Based on these reasoning pathways, the agent recommended (a) CAUTION for Atabecestat. (b) NO-GO for Semagacestat. These traces reveal the underlying logic used to navigate complex pharmacological data that fixed rules might overlook.\", \"page\": 7, \"index\": 1, \"width\": 979, \"height\": 577}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-29-713781-v1/fig-002.webp\", \"caption\": \"Fig 1. Architectural Schematic of Agentic vs. Deterministic Frameworks. Both architectures process data through a five-tier input structure. The Agentic framework utilizes an LLM orchestrator to manage eight specialized tools, while the Deterministic framework relies on a singular baseline tool. Both systems generate decision outputs categorized as GO, CAUTION, or NO-GO. Notably, the Agentic framework provides granular reasoning traces to justify its decision-making, a feature absent in the deterministic pipeline.\", \"page\": 3, \"index\": 2, \"width\": 979, \"height\": 447}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-29-713781-v1/fig-003.webp\", \"caption\": \"Fig 5. Superiority of pharmacological reasoning over fixed rules in discordant cases. Analysis of cases where the two architectures disagreed (discordant cases) highlights the robustness of the agentic approach.(a) In divergence analysis for the cases of conflicting recommendations, the Agentic framework was correct 75% of the time, compared to 10% for the deterministic pipeline.(b) A case study of Atabecestat serves as a representative example where the agent’s reasoning successfully outperformed the fixed-rule deterministic model.\", \"page\": 8, \"index\": 3, \"width\": 852, \"height\": 712}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-29-713781-v1/fig-004.webp\", \"caption\": \"Fig 2. Computational engine validation. (a) Allometric scaling validation for PK parameters (n = 20). Predictions within 3-fold error: CL 75%, Vd 95%, t1/2 100%, F 100%. (b) Predicted vs. observed logBB correlation (R = 0.781); 69.9% within 0.5 log units. (c) Kp,brain fold-error analysis (GMFE = 2.21); 80% within 3-fold. Outliers (risperidone, fluoxetine, duloxetine) likely reflect transporter interactions. (d) Receptor occupancy validation across 73 comparisons and 14 targets (R = 0.385); 35.6% within 20% absolute error. (e) Safety and transporter prediction balanced accuracy: hERG 0.86, P-gp 0.56, BCRP 0.69, LAT1 0.63. (f) Conformal PK coverage of 92.2% at 90% nominal confidence, with interval widths ranging 1.0–4.4x. (g) End-to-end uncertainty propagation coverage of 33.6%, well below the 90% target, reflecting compounding uncertainty across multi-tool reasoning. (h) Parameter sensitivity ranking: Kp,brain (0.684) and fu,plasma (0.660) are the dominant drivers, followed by Ki and Vd (0.577), F (0.542), and t1/2 (0.51).\", \"page\": 4, \"index\": 4, \"width\": 1004, \"height\": 797}]"
motivation: 中枢神经系统药物开发面临多维约束相互作用的复杂推理挑战，传统基于固定规则的评估方法难以应对复杂的药理环境。
method: 开发了名为 Cirrina 的 LLM 智能体，通过集成八种机械药理学工具，实现从分子结构到动物 PK/PD 数据的跨层级逻辑推理与阈值动态调整。
result: "在 181 种化合物的验证中，Cirrina 达到了 68% 的评估准确率，远高于传统确定性流程的 31%，且在分歧案例中表现出更强的推理正确性。"
conclusion: Cirrina 为临床前药物评价提供了一个可扩展且有据可查的推理框架，能有效识别潜在失败风险，显著优化药物研发的决策效率。
---

## 摘要
评估临床前候选药物是否有效并非一个预测问题，而是一个推理问题。同样的数值输出，根据靶点和治疗背景的不同，需要不同的解释。中枢神经系统（CNS）药物开发是这一推理问题中最具挑战性的实例。例如，化合物必须穿过血脑屏障，抵抗外排转运，并在满足安全边际的剂量下实现充足的受体占有率。这些约束条件相互交织，需要仔细解读。在本文中，我们展示了 Cirrina，一个与八种机制药理学工具耦合的大语言模型（LLM）智能体，能够对输入数据进行跨维度推理，从而提供更好的决策和详尽的推理轨迹记录。该 LLM 智能体能够跨越从 SMILES 到动物 PK/PD 测量的多个数据层级进行推理，并根据特定靶点的要求调整阈值。在 181 种 CNS 化合物的验证中，其准确率达到 68%，而基于规则的确定性流程准确率仅为 31%。在 103 个不一致的案例中，该智能体的推理在 75% 的情况下是正确的，而确定性流程仅为 10%。Cirrina 为临床前决策提供了一个可扩展且有据可查的框架，能够有效识别通用阈值容易忽略的易失败候选药物，从而降低临床开发周期中的失败风险。

## Abstract
Assessing whether a preclinical drug candidate will work is not a prediction problem but a reasoning problem. The same numerical output warrants different interpretations depending on the target and therapeutic context. CNS drug development presents the most demanding instance of this reasoning problem. For example, a compound must cross the blood-brain barrier, resist efflux transport, and achieve adequate receptor occupancy at a dose that clears safety margins. The constraints interact with each other in a web that needs careful interpretation. Here, we show that Cirrina, an LLM agent coupled to eight mechanistic pharmacology tools, can reason across the input data to provide better decisions and a well documented reasoning trace. The LLM agent reasons across multiple data tiers from SMILES to animal PK/PD measurements adjusting thresholds based on target-specific requirements. Validated against 181 CNS compounds, it achieved a 68% accuracy compared to a rule-based deterministic pipeline of 31% accuracy. In 103 discordant cases, the agent's reasoning was correct in 75% of instances compared to only 10% for deterministic pipelines. Cirrina provides a scalable, documented framework for preclinical decision-making, effectively identifying failure-prone candidates that generic thresholds overlook, and thereby reducing the chances of failure along the clinical development cycle.

---

## 论文详细总结（自动生成）

这是一份关于论文《Cirrina: LLM-driven pharmacological reasoning agent enables preclinical CNS drug evaluation》的结构化总结：

### 1. 论文的核心问题与整体含义
*   **核心问题**：中枢神经系统（CNS）药物的临床前评估不仅是一个“预测”问题，更是一个复杂的“推理”问题。传统的基于固定阈值（如 logP 或受体占有率的硬性指标）的评估方法无法适应不同靶点和治疗背景下的复杂药理环境，导致临床前决策的失败率居高不下。
*   **整体含义**：论文提出了 **Cirrina**，这是一个由大语言模型（LLM）驱动的药理学推理智能体。它通过集成多种机械药理学工具，模拟人类专家的逻辑，对药物的有效性和安全性进行跨维度的动态评估，旨在提高临床前候选药物筛选的准确性和透明度。

### 2. 论文提出的方法论
*   **核心思想**：将 LLM 作为“协调者（Orchestrator）”，耦合 **8 个专门的机械药理学工具**，实现从分子结构（SMILES）到动物 PK/PD 数据的全流程推理。
*   **关键技术细节**：
    *   **五层输入结构**：从 Tier 1（分子结构/体外数据）到 Tier 5（动物实验/安全性数据）逐步深入。
    *   **八大工具集成**：包括异速生长缩放（PK 参数预测）、血脑屏障渗透性预测（logBB/Kp,brain）、受体占有率（RO）计算、安全性与转运体预测（hERG, P-gp 等）、保形预测（Conformal PK）、不确定性传播分析以及参数敏感性分析。
    *   **动态推理引擎**：LLM 不仅仅调用工具，还会根据靶点特性调整评估阈值（例如，对于高亲和力药物，可以容忍较低的脑渗透率），并生成可解释的推理轨迹（Reasoning Traces）。

### 3. 实验设计
*   **数据集**：使用了包含 **181 种 CNS 化合物** 的验证集，涵盖了已获批药物和在临床阶段失败的药物（如 Atabecestat, Semagacestat）。
*   **Benchmark（基准）**：对比了**确定性流程（Deterministic Pipeline）**，即基于固定规则和硬性阈值的传统自动化评估系统。
*   **评估指标**：决策准确率（GO/NO-GO/CAUTION）、推理逻辑的正确性、预测值与观测值的相关性（R值）、倍数误差（Fold-error）等。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**具体的 GPU 型号、数量或训练时长。由于 Cirrina 主要是基于 LLM 智能体框架（利用现有 LLM 的推理能力）并集成药理学计算工具，其核心开销可能在于 LLM API 的调用和药理学模型的数值模拟，而非从头训练大型模型。

### 5. 实验数量与充分性
*   **实验规模**：
    *   对 181 种化合物进行了端到端的评估。
    *   针对 103 个智能体与传统规则产生分歧的“不一致案例”进行了深入分析。
    *   对 PK 预测、脑渗透、受体占有率等多个子模块进行了独立验证（如 73 组 RO 比较，14 个不同靶点）。
*   **充分性评价**：实验设计较为充分，不仅有宏观的准确率对比，还有针对特定失败案例（Case Study）的微观推理分析。通过引入不确定性传播和敏感性分析，增强了实验的客观性和科学性。

### 6. 论文的主要结论与发现
*   **性能飞跃**：Cirrina 的评估准确率达到 **68%**，远高于传统确定性流程的 **31%**。
*   **分歧处理能力**：在两者意见不一致的 103 个案例中，Cirrina 的推理在 **75%** 的情况下是正确的，而传统流程仅为 10%。
*   **动态调整的必要性**：实验证明，固定阈值往往会误杀具有潜力的药物或漏掉明显的风险点，而 LLM 能够根据药理背景灵活调整判断标准。
*   **透明度**：智能体提供的推理轨迹（Reasoning Traces）为决策提供了可审计的依据，有助于研发团队理解“为什么”做出该决策。

### 7. 优点
*   **范式创新**：将药物评估从单纯的数值预测转向逻辑推理，更符合药理学家的实际工作模式。
*   **高度集成**：成功整合了 8 种不同功能的药理学工具，实现了多源异构数据的统一处理。
*   **可解释性**：生成的推理轨迹解决了 AI 在药物研发中“黑盒”决策的痛点。
*   **鲁棒性**：在处理复杂、矛盾的数据时表现出比固定规则更强的韧性。

### 8. 不足与局限
*   **不确定性传播挑战**：实验显示端到端的不确定性覆盖率仅为 33.6%，远低于 90% 的目标，说明多工具耦合时误差会累积。
*   **工具依赖性**：智能体的表现高度依赖于底层 8 个工具的准确性（如 P-gp 转运体预测的准确率仍有提升空间）。
*   **幻觉风险**：尽管有工具约束，但 LLM 在解释复杂药理现象时仍可能存在逻辑偏差或产生误导性陈述。
*   **应用范围**：目前主要集中在 CNS 领域，其在肿瘤、免疫等其他复杂疾病领域的通用性尚待验证。

（完）

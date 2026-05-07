---
title: Interpreting Omics Data Analysis with Large Language Models for Disease Target and Drug Discovery
title_zh: 利用大语言模型解释组学数据分析以进行疾病靶点和药物发现
authors: "XU, Z., Chen, W., Ren, W., Xu, T., Amaechin, S., Khan, R., Chen, Y., Province, M., Payne, P., Li, F."
date: 2026-05-05
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.30.721768v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 将模式约束的多模型LLM检索与数值组学数据分析相结合
tldr: 本研究提出名为Text-to-Target的溯源感知框架，旨在解决LLM在疾病靶点发现中缺乏定量证据的问题。该框架将多模型LLM检索与数值组学分析相结合，通过模态感知融合技术将候选基因分类并生成受拓扑约束的假设。在阿尔茨海默病和胰腺癌的评估中，该方法成功识别了具有显著生物学支持的靶点和策略，实现了从检索到验证的全流程可审计性，为药物研发提供了可重复的发现架构。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统的组学分析难以整合海量文献知识，而纯文本LLM在靶点优先级排序上缺乏队列特异性的定量证据支持。
method: 提出Text-to-Target框架，通过模式约束的LLM检索与组学分析融合，并利用网络拓扑约束进行多阶段假设生成。
result: 在胰腺癌和阿尔茨海默病实验中，该框架生成的候选基因和治疗策略均获得了DepMap和CRISPRbrain等数据库的显著验证支持。
conclusion: 该研究证明了组学证据与LLM检索相结合的架构能有效扩展机制搜索空间，并保持发现过程的可解释性与可审计性。
---

## 摘要
在生物医学科学发现中，综合文献中的先验知识是解释数值组学数据分析以进行疾病靶点识别和药物发现的关键组成部分。仅靠大语言模型（LLMs）可以快速从生物医学文本中检索疾病机制，但如果没有特定队列的定量证据，纯文本输出对于靶点和药物优先级排序来说往往过于笼统且不可靠。在此，我们提出了一种具有来源感知能力的“文本到靶点”（Text-to-Target）框架，该框架将受模式约束的多模型 LLM 检索与数值组学数据分析相结合。其核心设计是一个模态感知融合步骤：将候选对象划分为重叠支持的锚点、仅检索到的隐藏枢纽以及网络涌现的新颖节点，然后在拓扑约束下将其传播到分阶段的假设和策略生成中。我们在阿尔茨海默病（AD）和胰腺导管腺癌（PDAC）中对该模型进行了评估。在 PDAC 中，该工作流产生了一个包含 75 个基因的平衡候选库和 23 个策略组合，在靶点水平和策略水平上均获得了显著的 DepMap 支持。在 AD 中，更严格的候选控制产生了一个包含 34 个基因的紧凑库和 14 个策略；在扩展的 CRISPRbrain 注册库下，两个靶点水平轴均表现显著，且具有较强的策略水平富集。在这两种疾病中，最终策略都保持了对候选池的完整来源闭环，实现了从检索人工制品到验证输出的端到端可审计性。这些结果支持了一种可迁移的发现架构，其中组学证据约束生物活性，LLM 检索扩展机制搜索空间，而网络感知融合则保留了可解释性。该框架为双疾病靶点优先级排序提供了可重复的基础，并激发了通过智能体证据刷新循环实现文献与机制持续一致性的动力。

## Abstract
In biomedical scientific discovery, synthesizing prior knowledge from the literature is an essential component of interpreting numerical omics data analyses for disease target identification and drug discovery. Large language models (LLMs) alone can rapidly retrieve disease mechanisms from biomedical text, but text-only outputs are general and unreliable for target and drug prioritization without cohort-specific quantitative evidence. Herein, we propose a provenance-aware Text-to-Target framework that couples schema-constrained multi-model LLM retrieval with numeric omics data analysis. The key design is a modality-aware fusion step: candidates are partitioned into overlap-supported anchors, retrieval-only hidden hubs, and network-emergent novelty nodes, then propagated into staged hypothesis and strategy generation under topology constraints. We evaluate the model in Alzheimer's disease (AD) and pancreatic ductal adenocarcinoma (PDAC). In PDAC, the workflow produced a balanced 75-gene candidate universe and a 23-strategy portfolio, with significant DepMap support at both target level and strategy level. In AD, stricter candidate controls yielded a compact 34-gene universe and 14 strategies; under an expanded CRISPRbrain registry, both target-level axes were significant , with strong strategy-level enrichment. Across both diseases, final strategies preserved full provenance closure to the candidate pool, enabling end-to-end auditability from retrieval artifacts to validation outputs. These results support a transferable discovery architecture in which omics evidence constrains biological activity, LLM retrieval expands mechanistic search space, and network-aware fusion preserves interpretability. The framework provides a reproducible basis for dual-disease target prioritization and motivates continuous literature-mechanism concordance with agentic evidence-refresh loops.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **Text-to-Target** 的溯源感知框架，旨在通过大语言模型（LLM）与单细胞组学数据的深度融合，加速疾病靶点识别和药物发现。

以下是对该论文的结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：在生物医学发现中，如何将海量但非结构化的文献知识（由 LLM 提取）与高噪声、特定队列的定量组学数据（数值分析）有效结合？
*   **研究动机**：
    *   **组学局限性**：单细胞组学能检测表达差异，但难以直接转化为可测试的机制性靶点。
    *   **LLM 局限性**：纯文本 LLM 检索速度快，但容易产生幻觉，且缺乏特定病理样本的定量证据支持。
    *   **人工瓶颈**：目前专家手动整合这两类信息的过程缓慢、难以标准化且易遗漏。
*   **整体含义**：该研究试图建立一个可审计、可重复的自动化工作流，实现从“文本检索”到“网络推理”再到“策略验证”的端到端发现。

### 2. 方法论：核心思想与技术细节
该框架采用分阶段集成循环，核心步骤如下：
*   **多模态提取**：
    *   **语言分支**：使用 LLM 组合（如 GPT-5、Gemini 2.5-pro、DeepSeek-r1）通过受模式约束（Schema-constrained）的提示词，检索特定细胞类型的靶点、通路和机制。
    *   **组学分支**：利用 **PathFinder**（一种基于图变换器的推理引擎）将单细胞差异表达信号（DEG）转化为加权的细胞内/间信号传导网络。
*   **来源感知融合（象限划分）**：将候选基因分为四个象限（实际重点讨论前三个）：
    *   **Q1 (Anchors)**：LLM 检索与组学网络共同支持的锚点。
    *   **Q2 (Hidden Hubs)**：仅由 LLM 检索支持，但在当前组学网络中未体现的潜在枢纽。
    *   **Q3 (Novelty Nodes)**：仅由组学网络发现，LLM 未提及的新颖节点（通过桥接分析排序）。
*   **拓扑约束下的假设生成**：
    *   LLM 首先基于 Q1 和 Q2 构建基础机制序列。
    *   随后根据网络拓扑约束（如路径长度、方向性），将 Q3 节点插入序列中，升级为多靶点治疗策略。
*   **药物关联层**：将生成的机制骨架与药物证据账本匹配，生成带有证据极性（支持/矛盾）的交互式可视化网络。

### 3. 实验设计
*   **测试床（Testbeds）**：
    *   **胰腺导管腺癌 (PDAC)**：高对比度基准，关注恶性上皮细胞与微环境的信号。
    *   **阿尔茨海默病 (AD)**：低对比度基准，关注神经胶质细胞状态转换和细胞间通讯。
*   **验证资源**：
    *   **PDAC**：使用 **DepMap** 数据库，通过 69 个 PDAC 模型评估靶点选择性漏洞和依赖性。
    *   **AD**：使用 **CRISPRbrain** 注册库，评估基因在神经变性相关筛选中的得分。
*   **对比与基准**：主要通过**置换检验（Permutation Testing）**生成随机基因集作为基准，验证所提策略的统计显著性。

### 4. 资源与算力
*   **算力说明**：文中提到了 PathFinder 模型的训练参数（6 层 Transformer、8 个注意力头、25 个 Epoch、Batch Size 为 4），但**未明确说明具体的 GPU 型号、数量或总训练时长**。
*   **模型使用**：使用了多个前沿 LLM 家族（GPT、Gemini、DeepSeek）作为推理引擎。

### 5. 实验数量与充分性
*   **实验规模**：
    *   在 PDAC 中生成了 75 个候选基因和 23 条治疗策略。
    *   在 AD 中生成了 34 个候选基因和 14 条治疗策略。
*   **充分性评价**：
    *   **跨疾病验证**：涵盖了肿瘤和神经退行性疾病，证明了框架的可迁移性。
    *   **统计严谨性**：采用了全局和局部两个层面的置换检验，确保发现不是随机巧合。
    *   **客观性**：通过与独立的第三方扰动数据库（DepMap/CRISPRbrain）对比，提供了客观的外部验证。

### 6. 主要结论与发现
*   **显著的验证结果**：PDAC 策略在 DepMap 中表现出极强的显著性（$p = 0.00019996$，$z = 8.9883$）；AD 策略在扩展的 CRISPRbrain 注册库中同样显著。
*   **机制发现**：识别了如 EGFR-STAT3 耦合（PDAC）和 STAT3 介导的神经炎症反馈环（AD）等关键轴。
*   **来源闭环**：所有最终策略均可追溯至原始检索人工制品或组学证据，实现了全流程的可审计性。

### 7. 优点与亮点
*   **模态感知融合**：不只是简单的列表交集，而是通过“象限”设计区分了已知共识、潜在枢纽和新颖发现。
*   **拓扑约束**：在 LLM 生成假设时强制引入网络拓扑限制，有效减少了 LLM 的生物学幻觉。
*   **端到端溯源**：每个靶点和策略都带有来源标签，方便科研人员回溯证据链。
*   **动态更新潜力**：提出了“智能体证据刷新循环”的概念，支持文献知识的持续更新。

### 8. 不足与局限
*   **数据模态限制**：目前主要依赖转录组数据，尚未充分整合蛋白质组学、代谢组学或空间组学信息。
*   **经典惯性（Canonical Inertia）**：LLM 倾向于保留广为人知的生物学模体，可能遗漏特定治疗压力下的上下文相关重连（如文中提到的 SRC 家族路径）。
*   **验证依赖性**：发现的质量高度依赖于下游验证数据库（如 DepMap）的覆盖范围和质量。
*   **因果性缺失**：转录组信号更多是关联性的，框架本身无法直接证明因果充分性，仍需湿实验验证。

（完）

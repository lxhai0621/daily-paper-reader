---
title: "Talk2QSP: Deriving Executable Scenarios from Unstructured Literature via Human-in-the-Loop Agents"
title_zh: Talk2QSP：通过人机协同智能体从非结构化文献中推导可执行场景
authors: "Kazemeini, A., Prieto, J., Balaji Kuttae, S., Siokis, A., Singh, G., Passban, P., Andreani, T."
date: 2026-05-11
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.06.723244v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 从非结构化文献中提取场景的智能体框架
tldr: 本研究提出Talk2QSP框架，旨在解决将非结构化文献转化为可执行QSP模型场景的难题。该框架利用LLM、语义接地和人机协同技术，将文本干预自动映射为精确参数配置。实验证明，该系统能可靠处理多剂量和单位转换等复杂任务，显著优于独立LLM，提升了药研仿真的自动化水平。
source: biorxiv
selection_source: fresh_fetch
motivation: 解决将非结构化文献描述的临床场景转化为可执行、可重复的QSP模型干预措施的挑战。
method: 开发了一个结合LLM驱动的场景提取器、双智能体映射器和人机协同策略的智能体框架。
result: 在多个动力学模型和专家场景测试中，系统准确解析了包括多剂量干预和单位转换在内的所有复杂任务。
conclusion: 专家与智能体系统的协作能有效解决生物学歧义，实现比独立LLM更可靠的QSP模型场景转化。
---

## 摘要
定量系统药理学 (QSP) 模型在药物研发中发挥着内在的干预作用，作为可执行的因果系统，用于设计、评估和替代临床试验。然而，将 QSP 部署为实验规划引擎仍受限于将临床或临床前场景的非结构化文献描述转化为可重现、可模拟的模型干预的难度。针对这一问题，我们提出了一个基于智能体的框架，通过自动提取和执行源自文献的场景，将 QSP 模型转化为可干预的实验系统。该框架结合了模型实体的语义接地（semantic grounding）、大语言模型 (LLM) 驱动的场景提取器以及双智能体场景映射器。我们的流水线不依赖于不透明的单次推理，而是通过离散、可验证的工作单将自由文本干预转换为精确的参数配置。此外，我们的动态人机协同 (HITL) 策略使建模者能够交互式地解决生物学歧义。在四个不同的动力学常微分方程 (ODE)/QSP 模型和七个由领域专家 (SME) 策划的文献场景中，我们的模型将所有选定场景解析为正确的、可执行的参数更改，包括多剂量干预、单位换算、无操作场景以及由歧义触发的 HITL 案例，证明了专家与智能体系统之间的结构化协作可以解决独立的原始系统生物学标记语言 (SBML) 推理 LLM 调用无法可靠处理的场景。

## Abstract
Quantitative Systems Pharmacology (QSP) models play an inherently interventional role in pharmaceutical research and development, functioning as executable causal systems for designing, evaluating, and replacing clinical trials. However, deploying QSP as an experimental planning engine remains constrained by the difficulty of translating unstructured literature descriptions of clinical or preclinical scenarios into reproducible, simulation-ready model interventions. Motivated by this issue, we propose an agent-based framework that operationalizes QSP models as intervention-ready experimental systems by automatically extracting and executing literature-derived scenarios. The framework combines semantic grounding of model entities with a large language model (LLM)-driven Scenario Extractor and a dual-agent Scenario Mapper. Rather than relying on opaque, single-shot reasoning, our pipeline converts free-text interventions into precise parameter configurations through discrete, verifiable work orders. Moreover, our dynamic Human-in-the-Loop (HITL) strategy empowers modelers to resolve biological ambiguities interactively. Across four diverse kinetic ordinary differential equation (ODE)/QSP models and seven Subject Matter Expert (SME)-curated literature scenarios, our model resolved all selected scenarios into correct executable parameter changes, including multi-dose interventions, unit conversions, no-op scenarios, and ambiguity-triggered HITL cases, demonstrating that structured collaboration between experts and agentic systems can resolve scenarios that standalone raw Systems Biology Markup Language (SBML) reasoning LLM calls handle unreliably.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **Talk2QSP** 的智能体框架，旨在通过大语言模型（LLM）和人机协同机制，将非结构化的生物医学文献自动转化为可执行的定量系统药理学（QSP）模型场景。

以下是对该论文的深度总结：

### 1. 核心问题与整体含义
*   **研究背景**：QSP 模型是药物研发中用于模拟临床试验、评估药物干预效果的关键工具。然而，将文献中描述的临床方案（如“每隔 12 小时给药 50mg，持续 5 天”）转化为模型可识别的参数配置（如 SBML 文件中的具体数值和方程）是一个高度依赖人工、耗时且易出错的过程。
*   **核心问题**：如何弥合“非结构化自然语言描述”与“结构化、可执行的数学模型参数”之间的鸿沟，实现药研仿真的自动化和标准化。

### 2. 方法论
Talk2QSP 采用了一个多阶段的智能体（Agent）架构，核心流程包括：
*   **语义接地（Semantic Grounding）**：将 QSP 模型中的实体（物种、参数、反应）映射到标准生物医学本体中，为 LLM 提供上下文理解基础。
*   **场景提取器（Scenario Extractor）**：利用 LLM 从自由文本中提取干预措施（如剂量、频率、时长），并生成离散、可验证的“工作单”（Work Orders）。
*   **双智能体场景映射器（Dual-agent Scenario Mapper）**：
    *   **提议者（Proposer）**：建议如何将提取的干预措施映射到具体的模型参数。
    *   **审核者（Reviewer）**：检查映射的逻辑一致性和生物学合理性。
*   **动态人机协同（HITL）策略**：当系统遇到生物学歧义（例如一个术语对应多个模型参数）时，会主动暂停并请求人类专家干预，确保最终执行的准确性。
*   **执行引擎**：将最终确定的参数配置应用于基于常微分方程（ODE）的模型，生成可模拟的场景。

### 3. 实验设计
*   **测试模型**：选用了 4 个具有代表性的动力学模型，涵盖了从简单的 Lotka-Volterra 模型到复杂的 QSP 模型。
*   **测试场景**：由领域专家（SME）从真实文献中策划了 7 个复杂场景，包括：
    *   **多剂量干预**：涉及复杂的给药时间表。
    *   **单位转换**：将文献中的物理单位转换为模型所需的标准单位。
    *   **无操作（No-op）场景**：测试系统识别无关信息的能力。
    *   **歧义触发场景**：测试 HITL 机制的有效性。
*   **基准对比（Benchmark）**：对比了“独立、单次推理的 LLM（直接处理 SBML）”与“Talk2QSP 框架”。

### 4. 资源与算力
*   **算力说明**：论文中未明确提及具体的 GPU 型号、数量或训练时长。由于该框架主要基于 LLM 驱动的智能体推理（Inference-based Agentic Framework），而非从头训练大模型，其核心开销在于 API 调用和推理逻辑。
*   **模型使用**：虽然未详述硬件，但提到了使用 LLM（推测为 GPT-4 等量级模型）作为推理引擎。

### 5. 实验数量与充分性
*   **实验规模**：实验涵盖了 4 个模型和 7 个深度策划的专家场景。
*   **充分性评价**：虽然从样本绝对数量上看较小，但每个场景都代表了药研中的典型挑战（如单位换算、歧义处理）。实验设计具有较高的定性深度，通过消融式观察（对比独立 LLM）证明了框架在处理复杂逻辑时的优越性。对于概念验证（PoC）阶段的研究，其实验设计是客观且具有说服力的。

### 6. 主要结论与发现
*   **超越单次推理**：传统的“单次 LLM 调用”在处理复杂的 SBML 逻辑和生物学歧义时表现不可靠，容易产生幻觉或错误映射。
*   **结构化协作的价值**：通过将任务分解为提取、映射、审核和人工确认，Talk2QSP 能够 100% 准确地解析所有选定场景。
*   **HITL 的必要性**：专家干预是解决生物学命名歧义、确保模型仿真结果具有科学意义的关键。

### 7. 优点
*   **透明度与可验证性**：生成的“工作单”使建模者可以清晰地看到每一步转换逻辑，而非“黑盒”操作。
*   **鲁棒性**：能够处理复杂的单位换算和多剂量逻辑，这是目前许多自动化工具的短板。
*   **通用性**：框架不依赖于特定的 QSP 模型，具有较强的跨模型迁移潜力。

### 8. 不足与局限
*   **规模限制**：目前仅在 7 个专家场景上进行了验证，尚未在大规模文献库上进行高通量测试。
*   **LLM 依赖**：系统的性能高度依赖于底层 LLM 的推理能力，且 API 调用可能存在成本和隐私合规问题。
*   **复杂模型挑战**：对于包含数千个参数的超大型 QSP 模型，语义接地和映射的搜索空间会急剧增加，可能导致推理效率下降。

（完）

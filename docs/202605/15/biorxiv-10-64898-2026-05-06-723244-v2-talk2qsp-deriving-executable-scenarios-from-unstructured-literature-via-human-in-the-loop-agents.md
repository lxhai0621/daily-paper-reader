---
title: "Talk2QSP: Deriving Executable Scenarios from Unstructured Literature via Human-in-the-Loop Agents"
title_zh: Talk2QSP：通过人机协同智能体从非结构化文献中推导可执行场景
authors: "Kazemeini, A., Prieto, J., Balaji Kuttae, S., Siokis, A., Singh, G., Passban, P., Andreani, T."
date: 2026-05-15
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.06.723244v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 从非结构化文献中提取场景的智能体框架
tldr: 本研究针对定量系统药理学（QSP）模型在将非结构化文献转化为可执行仿真场景时的困难，提出了Talk2QSP框架。该框架结合大语言模型、语义接地技术和人机协同（HITL）策略，通过场景提取器和映射器将自由文本干预转化为精确的参数配置。实验证明，该系统能有效处理多剂量干预和单位转换等复杂任务，显著提升了模型部署的自动化与准确性，为药物研发提供了高效的实验规划引擎。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在解决将非结构化文献描述的临床或临床前场景转化为可重复、可仿真的QSP模型干预措施的挑战。
method: 开发了一个结合LLM驱动的场景提取器、双智能体映射器及人机协同策略的框架，将自由文本转化为精确的参数配置。
result: 在四种动力学模型和七个专家策划场景的测试中，该框架成功解析了包括多剂量干预、单位转换和歧义处理在内的所有执行场景。
conclusion: 专家与智能体系统的结构化协作能够有效解决独立LLM难以处理的生物学歧义，实现从文献到可执行QSP场景的可靠转化。
---

## 摘要
定量系统药理学 (QSP) 模型在药物研发中发挥着固有的干预作用，作为可执行的因果系统，用于设计、评估和替代临床试验。然而，将 QSP 部署为实验规划引擎仍受限于将临床或临床前场景的非结构化文献描述转化为可重现、可模拟的模型干预的难度。针对这一问题，我们提出了一个基于智能体的框架，通过自动提取和执行源自文献的场景，将 QSP 模型转化为可干预的实验系统。该框架结合了模型实体的语义接地（semantic grounding）、大语言模型 (LLM) 驱动的场景提取器以及双智能体场景映射器。我们的流水线不依赖于不透明的单次推理，而是通过离散、可验证的工作单将自由文本干预转换为精确的参数配置。此外，我们的动态人机协同 (HITL) 策略使建模者能够交互式地解决生物学歧义。在四个不同的动力学常微分方程 (ODE)/QSP 模型和七个由领域专家 (SME) 策划的文献场景中，我们的模型将所有选定场景解析为正确的、可执行的参数变更，包括多剂量干预、单位换算、无操作场景以及由歧义触发的 HITL 案例，证明了专家与智能体系统之间的结构化协作可以解决独立的原始系统生物学标记语言 (SBML) 推理 LLM 调用无法可靠处理的场景。

## Abstract
Quantitative Systems Pharmacology (QSP) models play an inherently interventional role in pharmaceutical research and development, functioning as executable causal systems for designing, evaluating, and replacing clinical trials. However, deploying QSP as an experimental planning engine remains constrained by the difficulty of translating unstructured literature descriptions of clinical or preclinical scenarios into reproducible, simulation-ready model interventions. Motivated by this issue, we propose an agent-based framework that operationalizes QSP models as intervention-ready experimental systems by automatically extracting and executing literature-derived scenarios. The framework combines semantic grounding of model entities with a large language model (LLM)-driven Scenario Extractor and a dual-agent Scenario Mapper. Rather than relying on opaque, single-shot reasoning, our pipeline converts free-text interventions into precise parameter configurations through discrete, verifiable work orders. Moreover, our dynamic Human-in-the-Loop (HITL) strategy empowers modelers to resolve biological ambiguities interactively. Across four diverse kinetic ordinary differential equation (ODE)/QSP models and seven Subject Matter Expert (SME)-curated literature scenarios, our model resolved all selected scenarios into correct executable parameter changes, including multi-dose interventions, unit conversions, no-op scenarios, and ambiguity-triggered HITL cases, demonstrating that structured collaboration between experts and agentic systems can resolve scenarios that standalone raw Systems Biology Markup Language (SBML) reasoning LLM calls handle unreliably.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **Talk2QSP** 的框架，旨在利用大语言模型（LLM）和人机协同（Human-in-the-Loop, HITL）智能体，将非结构化的生物医学文献自动转化为定量系统药理学（QSP）模型的可执行仿真场景。

以下是对该论文的深度总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：在药物研发中，QSP 模型（通常以常微分方程 ODE 形式存在）是模拟临床试验的关键工具。然而，将临床文献中描述的干预措施（如“每两周静脉注射 10mg/kg 药物，持续三个月”）转化为模型中具体的参数配置和初始状态变更，目前高度依赖人工，且极易出错、难以重现。
*   **研究动机**：现有的 LLM 在直接处理复杂的系统生物学标记语言（SBML）文件时，往往无法准确理解生物学实体的语义，也难以处理复杂的给药方案（如多剂量、单位换算）。本研究旨在建立一个自动化桥梁，将自然语言描述的实验场景转化为精确的模型指令。

### 2. 方法论：核心思想与关键技术
Talk2QSP 采用了一种基于智能体的多阶段流水线，核心思想是将“理解”与“执行”分离，并通过人机协作解决歧义。
*   **语义接地（Semantic Grounding）**：首先对 QSP 模型中的实体（物种、参数、反应）进行标准化标注，将其映射到生物本体论，使智能体能理解模型组件的生物学含义。
*   **场景提取器（Scenario Extractor）**：利用 LLM 从非结构化文本中提取干预元数据，包括药物名称、剂量数值、单位、给药频率、持续时间和给药途径。
*   **双智能体场景映射器（Dual-agent Scenario Mapper）**：
    *   **搜索智能体（Searcher Agent）**：在模型实体中搜索与提取到的干预措施最匹配的参数或物种。
    *   **精炼智能体（Refiner Agent）**：验证搜索结果的逻辑一致性，并处理单位换算（如将 mg/kg 转换为模型所需的摩尔浓度）。
*   **人机协同（HITL）策略**：当系统检测到高度歧义（例如一个药物对应多个模型参数）或置信度较低时，会主动向人类专家提问，由专家进行决策。
*   **可验证工作单（Work Orders）**：最终输出不是模糊的代码，而是离散的、可验证的指令集，用于更新模型状态。

### 3. 实验设计
*   **测试模型**：选用了 4 个具有代表性的动力学模型，涵盖了从简单的 Lotka-Volterra 模型到复杂的药代动力学/药效动力学（PK/PD）模型。
*   **测试场景**：由领域专家（SME）从真实文献中策划了 7 个典型场景，包括：
    *   单次/多次给药方案。
    *   涉及复杂单位换算的干预。
    *   “无操作（No-op）”场景（测试系统是否会过度拟合）。
    *   故意设置的歧义场景（测试 HITL 触发机制）。
*   **基准对比**：对比了“独立 LLM 直接推理 SBML”的方法，证明了结构化智能体框架在处理生物学逻辑上的优越性。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**具体的 GPU 型号、数量或训练时长。由于该框架主要基于 LLM（如 GPT 系列）的 API 调用和推理，而非从头训练大型模型，其核心开销在于 API 调用次数和提示词工程（Prompt Engineering）。

### 5. 实验数量与充分性
*   **实验规模**：实验涵盖了 4 个模型和 7 个深度策划的场景。
*   **充分性评价**：虽然从统计学角度看样本量（场景数）较小，但这些场景是针对 QSP 建模中的“痛点”精心设计的（如单位换算、多剂量逻辑）。实验设计具有较强的针对性和定性分析价值，足以证明该框架在处理复杂逻辑分支时的有效性。

### 6. 主要结论与发现
*   **超越单次推理**：简单的 LLM 调用无法可靠地处理 SBML 模型，而 Talk2QSP 通过分解任务显著提高了准确性。
*   **HITL 的必要性**：在生物学领域，歧义是常态。通过引入人机协同，系统能够解决 LLM 无法通过上下文自行判断的参数映射问题。
*   **端到端自动化**：该框架成功实现了从“阅读文献”到“运行仿真”的闭环，能够处理包括多剂量时间表在内的复杂执行逻辑。

### 7. 优点
*   **结构化设计**：将非结构化文本转化为“工作单”，增加了过程的可解释性和可审计性。
*   **单位感知**：内置了强大的单位换算逻辑，这是生物仿真中的常见错误来源。
*   **灵活性**：不绑定于特定模型，只要模型符合 SBML 等标准格式即可应用。

### 8. 不足与局限
*   **规模化挑战**：对于包含数千个反应的超大型 QSP 模型，智能体在搜索空间过大时可能会出现性能下降或幻觉。
*   **依赖 LLM 基础能力**：系统的上限受限于底层 LLM 对生物医学文本的理解能力。
*   **评估指标单一**：目前主要依赖专家评估结果的正确性，缺乏在大规模自动化基准测试集上的定量表现数据。

（完）

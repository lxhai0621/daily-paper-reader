---
title: "Talk2QSP: Deriving Executable Scenarios from Unstructured Literature via Human-in-the-Loop Agents"
title_zh: Talk2QSP：通过人机回环智能体从非结构化文献中推导可执行场景
authors: "Kazemeini, A., Prieto, J., Balaji Kuttae, S., Siokis, A., Singh, G., Passban, P., Andreani, T."
date: 2026-05-11
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.06.723244v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 从非结构化文献中提取场景的智能体框架
tldr: 定量系统药理学（QSP）模型在药物研发中至关重要，但将非结构化文献转化为可执行模拟极具挑战。本文提出Talk2QSP框架，利用LLM驱动的代理系统结合语义落地和人机协同策略，将自由文本干预转化为精确参数配置。该框架通过可验证的工作单处理复杂指令，显著提升了文献到模型执行的自动化水平。
source: biorxiv
selection_source: fresh_fetch
motivation: 解决将非结构化临床或临床前文献描述转化为可重复、可模拟的QSP模型干预措施的难题。
method: 提出一种结合语义落地、LLM驱动的场景提取器、双代理映射器及人机协同策略的代理框架。
result: 在4个动力学模型和7个专家策划场景中，成功实现了包括多剂量干预和单位换算在内的所有复杂场景解析。
conclusion: 专家与代理系统的结构化协作能有效解决独立LLM难以处理的生物学歧义，实现可靠的模型场景转化。
---

## 摘要
定量系统药理学（QSP）模型在药物研发中发挥着固有的干预作用，作为可执行的因果系统，用于设计、评估和替代临床试验。然而，将 QSP 部署为实验规划引擎仍受限于将临床或临床前场景的非结构化文献描述转化为可重现、可模拟的模型干预的难度。针对这一问题，我们提出了一个基于智能体的框架，通过自动提取和执行源自文献的场景，将 QSP 模型转化为可干预的实验系统。该框架结合了模型实体的语义落地、大语言模型（LLM）驱动的场景提取器（Scenario Extractor）以及双智能体场景映射器（Scenario Mapper）。我们的流水线不依赖于不透明的单次推理，而是通过离散、可验证的工作单将自由文本干预转换为精确的参数配置。此外，我们的动态人机回环（HITL）策略使建模人员能够交互式地解决生物学歧义。在四个不同的动力学常微分方程（ODE）/QSP 模型和七个由领域专家（SME）策划的文献场景中，我们的模型将所有选定场景解析为正确的、可执行的参数变更，包括多剂量干预、单位换算、无操作（no-op）场景以及由歧义触发的 HITL 案例。这表明，专家与智能体系统之间的结构化协作可以解决那些仅靠原始系统生物学标记语言（SBML）推理的 LLM 调用无法可靠处理的场景。

## Abstract
Quantitative Systems Pharmacology (QSP) models play an inherently interventional role in pharmaceutical research and development, functioning as executable causal systems for designing, evaluating, and replacing clinical trials. However, deploying QSP as an experimental planning engine remains constrained by the difficulty of translating unstructured literature descriptions of clinical or preclinical scenarios into reproducible, simulation-ready model interventions. Motivated by this issue, we propose an agent-based framework that operationalizes QSP models as intervention-ready experimental systems by automatically extracting and executing literature-derived scenarios. The framework combines semantic grounding of model entities with a large language model (LLM)-driven Scenario Extractor and a dual-agent Scenario Mapper. Rather than relying on opaque, single-shot reasoning, our pipeline converts free-text interventions into precise parameter configurations through discrete, verifiable work orders. Moreover, our dynamic Human-in-the-Loop (HITL) strategy empowers modelers to resolve biological ambiguities interactively. Across four diverse kinetic ordinary differential equation (ODE)/QSP models and seven Subject Matter Expert (SME)-curated literature scenarios, our model resolved all selected scenarios into correct executable parameter changes, including multi-dose interventions, unit conversions, no-op scenarios, and ambiguity-triggered HITL cases, demonstrating that structured collaboration between experts and agentic systems can resolve scenarios that standalone raw Systems Biology Markup Language (SBML) reasoning LLM calls handle unreliably.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **Talk2QSP** 的智能体框架，旨在解决定量系统药理学（QSP）领域中，如何将非结构化文献描述自动转化为可执行模型模拟场景的难题。以下是对该论文的深度结构化总结：

### 1. 论文的核心问题与整体含义
*   **研究动机**：QSP 模型是药物研发中模拟临床试验的关键工具，但目前将文献中的临床/前临床场景（如给药方案、患者群体特征）转化为模型参数配置的过程高度依赖人工，且存在不可重现、易出错、单位换算复杂以及模型参数语义不明等障碍。
*   **核心问题**：如何利用大语言模型（LLM）自动化地从非结构化文本中提取实验场景，并将其精确映射到复杂的数学模型（如 SBML 格式的 ODE 模型）中，同时解决生物学歧义。

### 2. 论文提出的方法论
Talk2QSP 采用分阶段的智能体流水线，包含三个核心模块：
*   **实体定义器 (Entity Definer)**：
    *   **上下文增强**：通过 BASICO 接口解析 SBML 模型，并调用外部数据库（如 UniProt、OLS）获取本体注释，解决模型参数命名模糊的问题。
    *   **多轮精炼描述**：利用 LLM 生成实体的生物学定义，并通过“自评价-反馈”循环进行多轮修正，生成结构化的 JSON 字典和压缩语义索引。
*   **场景提取器 (Scenario Extractor)**：
    *   **三阶段设计**：1) 局部提取（滑动窗口处理文本块）；2) 全文合成（合并重复项，构建连贯描述）；3) 评判引导精炼（Judge-Refiner 架构，确保提取结果有据可查）。
*   **场景映射器 (Scenario Mapper)**：
    *   **双智能体架构**：由 **编排智能体 (Orchestrator)** 拆解任务为“工作单”，**求解智能体 (Solver)** 执行具体计算。
    *   **工具链集成**：求解智能体可调用字典查询、语义搜索、**Python REPL 计算器**（处理单位换算）以及 **人机回环 (HITL) 中断**（在遇到关键歧义时请求专家干预）。

### 3. 实验设计
*   **实验对象**：选取了 4 个具有代表性的 QSP 模型（来自 BioModels 数据库，编号 512, 537, 788, 913），涵盖骨关节炎疼痛、克罗恩病、双特异性抗体治疗和实体瘤等领域。
*   **测试场景**：由领域专家（SME）策划了 7 个复杂场景，包括多剂量干预、需要中间计算的参数调整、单位换算以及“无操作”场景。
*   **基准对比 (Benchmark)**：对比了 **OpenAI o3** 模型在仅提供原始 SBML 文件和场景文本情况下的单次推理表现（o3 SBML Baseline）。

### 4. 资源与算力
*   **模型使用**：主要使用 **GPT-4o-mini**（用于大部分推理任务）和 **GPT-4o-nano**（用于轻量级语义搜索）。
*   **算力说明**：文中未明确提及具体的 GPU 型号或训练时长，因为该框架基于现有的商业 LLM API 进行推理和智能体编排，而非从头训练模型。实验通过设置 `temperature=0` 和固定随机种子来保证可重复性。

### 5. 实验数量与充分性
*   **实验规模**：共进行了 7 组端到端案例研究。
*   **充分性评价**：虽然实验绝对数量较少，但覆盖了 QSP 建模中最常见的痛点（如单位不一致、参数名误导、复杂的动力学关联计算）。
*   **客观性**：通过与专家标注的“地面真值（Ground Truth）”对比 Delta 值（参数差异），评价标准客观。对比实验显示，Talk2QSP 在处理复杂逻辑和避免幻觉方面显著优于单次调用的强推理模型（o3）。

### 6. 论文的主要结论与发现
*   **自动化可行性**：Talk2QSP 成功将所有 7 个复杂场景解析为正确的参数变更。
*   **HITL 的必要性**：在处理 SBML 模型中缺失单位定义或文献与模型单位冲突（如质量 vs 摩尔浓度）时，动态的人机回环机制是确保模拟可靠性的关键。
*   **超越单次推理**：传统的 LLM（即使是 o3 这种强推理模型）在面对长参数名、复杂单位换算时容易产生幻觉或计算错误，而结构化的智能体协作能有效规避这些问题。

### 7. 优点
*   **语义落地**：通过外部本体数据库增强了对模型参数的理解，解决了“黑盒”参数名的问题。
*   **可验证性**：将复杂的映射任务拆解为离散的工作单，每一步计算（通过 Python REPL）和决策都可追溯。
*   **灵活性**：支持人机协作，既能实现严谨的数学推导，也能根据专家建议适配非标准的建模习惯。

### 8. 不足与局限
*   **模态限制**：目前仅支持文本提取，无法处理文献中包含关键实验数据的图表（Figures）。
*   **数据集规模**：由于缺乏大规模标注的 QSP 场景数据集，目前的评估仍局限于小规模的人工策划集。
*   **依赖性**：高度依赖闭源 LLM 的 API 性能，且对于极其复杂的参数扫掠（Parameter Sweeps）处理能力尚待验证。
*   **应用范围**：目前主要针对 SBML 格式的模型，对于其他格式或非 ODE 模型的适配性未提及。

（完）

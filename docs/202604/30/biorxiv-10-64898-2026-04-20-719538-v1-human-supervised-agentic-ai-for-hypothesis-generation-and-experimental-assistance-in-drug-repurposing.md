---
title: Human-supervised Agentic AI for Hypothesis Generation and Experimental Assistance in Drug Repurposing
title_zh: 人机协作的智能体 AI 用于药物重定向中的假设生成与实验辅助
authors: "Huynh, D.-L., Asp, E., Ballante, F., Puigvert, J. C., DeGrave, A., Karki, R., Nader, K., Östling, P., Pokharel, B., Rietdijk, J., Schlotawa, L., Schmidt, L., Seal, S., Seashore-Ludlow, B., Aittokallio, T., Spjuth, O."
date: 2026-04-22
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719538v1.full.pdf"
tags: ["query:ma-kf"]
score: 10.0
evidence: 用于药物再利用的具有情境记忆和RAG的分层多智能体系统
tldr: 针对药物重定位全生命周期的复杂需求，本研究开发了RepurAgent，这是一个由人类监督的层级化多智能体AI系统。该系统通过协调研究、预测、数据和报告四个专业子智能体，结合长短期记忆与检索增强生成技术，实现了从假设生成到实验设计的全流程自动化。在白血病、新冠肺炎及多重硫酸酯酶缺乏症的验证中，该系统展现了极高的准确性与效率，显著提升了药物研发的成功率。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统的计算药物重定位主要集中在假设生成，难以覆盖从实验设计到数据分析的完整研发周期。
method: 开发了包含主管、规划及四个专业子智能体的层级化系统，并引入人类在环设计与检索增强生成技术。
result: "系统在AML路径识别中达到97%的准确率，在新冠药物筛选中AUC-ROC达0.98，并为罕见病筛选出82个高置信度候选药物。"
conclusion: 智能体AI能够有效支持药物重定位的全生命周期，是加速药物研发和实验协作的强有力工具。
---

## 摘要
计算药物重定向主要集中在快速假设生成上，然而实际应用涵盖了更广泛的生命周期，从候选药物建议到实验设计、分析测定数据以及迭代优化候选药物。在此，我们证明了智能体 AI 可以覆盖这一完整范畴。为此，我们开发了 RepurAgent，这是一个分层多智能体 AI 系统，由一个监督智能体和一个规划智能体组成，通过人机协同设计，协调四个专业子智能体（研究、预测、数据和报告），并具备情景记忆和检索增强生成功能。该系统基于 REMEDi4ALL 联盟开发的特定于药物重定向的数据、工具和标准操作程序。我们在涵盖重定向生命周期不同阶段的三个场景中验证了该智能体系统：在急性髓系白血病中，RepurAgent 找回了 Google Co-Scientist 识别出的高达 97% 的疾病相关通路，并在 60 分钟内完成了工作流；在回顾性 COVID-19 抗病毒筛选中，RepurAgent 作为自适应实验协作伙伴，在没有预设阈值的情况下，以高达 0.98 的 AUC-ROC 对化合物进行优先级排序，并标记出人工审查中遗漏的混杂因素；对于多重硫酸酯酶缺乏症，它从 5000 个化合物中筛选出 82 个高置信度候选药物，并得到了领域专家的进一步证实。这些结果表明，智能体 AI 可以支持从假设生成到实验分析的整个药物重定向生命周期。RepurAgent 已开源并部署在 https://repuragent.serve.scilifelab.se/。

## Abstract
Computational drug repurposing has largely been focused on rapid hypothesis generation, yet real-world applications span a far broader lifecycle, from drug candidate suggestion to designing experiments, analyzing assay data, and iteratively refining candidates. Here, we demonstrate that agentic AI can fulfill this entire scope. To this end, we developed RepurAgent, a hierarchical multi-agent AI system comprising a supervisor agent and a planning agent that coordinate four specialized sub-agents -- research, prediction, data, and report -- through a human-in-the-loop design, with episodic memory and retrieval-augmented generation. The system is grounded in data, tools, and standard operating procedures specific for drug repurposing, developed within the REMEDi4ALL consortium. We validated the agentic system across three scenarios spanning the various stages within the repurposing lifecycle: in Acute Myeloid Leukemia, RepurAgent recovered up to 97% of disease-relevant pathways identified by Google Co-Scientist, completing the workflow within 60 minutes; in a retrospective COVID-19 antiviral screen, RepurAgent acted as an adaptive experimental collaborator, prioritizing compounds with AUC-ROC up to 0.98 without predefined thresholds and flagging confounders missed in manual review; and for Multiple Sulfatase Deficiency, it prioritized 82 high-confidence candidates from 5000 compounds, which were further corroborated by domain experts. These results demonstrate that agentic AI can support across the full drug repurposing lifecycle, from hypothesis generation to experimental analysis. RepurAgent is open source and deployed at https://repuragent.serve.scilifelab.se/.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **RepurAgent** 的人机协作多智能体 AI 系统，旨在解决药物重定向（Drug Repurposing）过程中计算工具碎片化、无法覆盖从假设生成到实验分析全生命周期的问题。

以下是对该论文的结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：传统的计算药物重定向方法（如知识图谱、机器学习预测）通常只关注单一环节（如预测候选药物），而忽略了真实世界中从数据整合、实验设计、结果分析到迭代优化的完整闭环。
*   **研究动机**：药物研发周期长、成本高，且现有的计算工具缺乏协同。作者希望利用大语言模型（LLM）的智能体（Agentic）能力，构建一个能够像人类科学家一样规划、调用工具并处理复杂实验流程的系统。

### 2. 方法论：核心思想与技术细节
RepurAgent 采用分层多智能体架构，核心思想是**“人类监督下的自主协作”**。
*   **分层架构**：
    *   **规划智能体 (Planning Agent)**：将自然语言任务分解为多步工作流，供人类科学家审查。
    *   **监督智能体 (Supervisor Agent)**：负责任务调度，协调四个专业子智能体。
    *   **四个子智能体**：**研究 (Research)**（实时检索文献/数据库）、**预测 (Prediction)**（ADMET 属性预测）、**数据 (Data)**（编写 Python 代码分析实验数据）、**报告 (Report)**（汇总发现）。
*   **关键技术**：
    *   **ReAct 模式**：结合推理（Reasoning）与行动（Acting），动态调用外部工具。
    *   **三层记忆架构**：包括工作记忆（会话内状态）、短期记忆（上下文）和**长期情景记忆**（跨会话的成功经验检索）。
    *   **检索增强生成 (RAG)**：将 REMEDi4ALL 联盟制定的**标准操作程序 (SOPs)** 向量化，引导智能体遵循实验室规范。
    *   **工具集成**：集成了知识图谱生成器 (KGG)、Chemical Annotator、CPSign（保形预测模型）等专业工具。

### 3. 实验设计：场景、Benchmark 与对比
论文通过三个具有代表性的案例验证系统性能：
*   **场景 1：急性髓系白血病 (AML)**（端到端假设生成）：
    *   **Benchmark**：Google 的 Co-Scientist 流程。
    *   **对比方法**：Vanilla LLMs（原生大模型，如 GPT-4o）。
    *   **评估指标**：通路覆盖率（Recall/Precision/Jaccard Index）。
*   **场景 2：COVID-19 抗病毒筛选**（实验数据分析）：
    *   **数据集**：包含 5275 种化合物的真实实验数据（细胞成像、细胞病变效应等）。
    *   **对比方法**：人类专家的手动筛选决策。
    *   **评估指标**：AUC-ROC 曲线。
*   **场景 3：多重硫酸酯酶缺乏症 (MSD)**（罕见病优先级排序）：
    *   **挑战**：数据极度稀缺。
    *   **验证方式**：领域专家对筛选出的 82 个高置信度候选药物进行定性评估。
*   **消融实验**：针对规划智能体，测试了 SOP 检索、文献搜索和情景记忆对计划质量的影响。

### 4. 资源与算力
*   **模型使用**：主要基于 OpenAI 的 API（GPT-4o 用于规划，GPT-4o-mini 用于子任务）。
*   **算力说明**：论文**未明确提及**具体的本地 GPU 训练算力（如型号、数量），因为该系统本质上是一个基于 API 的智能体编排框架，而非从头训练基础模型。其运行成本主要体现在 API 调用费用和推理延迟上。

### 5. 实验数量与充分性
*   **实验规模**：
    *   进行了 15 个规划请求的评估，每个配置运行 10 次（共 800 次运行）。
    *   对 RAG 系统进行了 200 个查询的基准测试。
    *   三个案例涵盖了从常见癌症到传染病再到超罕见病的不同数据环境。
*   **充分性评价**：实验设计较为充分，通过统计学检验（Kruskal-Wallis, Mann-Whitney U）验证了工具增强的显著性。对比 Google Co-Scientist 的实验展示了其在工业级任务中的竞争力。

### 6. 主要结论与发现
*   **效率提升**：RepurAgent 在 60 分钟内完成了人类专家需要数周才能完成的数据分析和候选药物排序。
*   **准确性**：在 COVID-19 案例中，其自动排序与专家决策的吻合度极高（AUC-ROC 达 0.986）。在 AML 案例中，找回了 Co-Scientist 识别出的 97% 的相关通路。
*   **纠错能力**：系统能自动识别实验中的混杂因素（如细胞毒性导致的假阳性），这是纯预测模型无法做到的。
*   **规划能力**：工具增强（SOP + 记忆）使规划质量提升了 32%，但仍需人类在环（Human-in-the-loop）以确保 100% 可靠。

### 7. 优点（亮点）
*   **全生命周期覆盖**：打破了“仅预测”的局限，实现了从文献调研到代码编写分析实验数据的全流程。
*   **SOP 引导**：通过 RAG 引入行业标准操作程序，使 AI 的推理更符合科学规范而非“幻觉”。
*   **透明度与可追溯性**：系统展示完整的推理链和工具调用过程，方便科学家审计。
*   **开源与部署**：提供了在线平台和开源代码，具有很强的实用价值。

### 8. 不足与局限
*   **缺乏前瞻性验证**：目前的案例多为回顾性分析（Retrospective），筛选出的新候选药物（如 MSD 案例）尚未经过实际的湿实验验证。
*   **API 依赖**：系统高度依赖闭源模型 API，可能存在隐私风险和成本波动。
*   **基准测试偏差**：由于 LLM 的训练数据可能包含已发表的药物重定向研究，在进行回顾性测试时可能存在“数据泄露”风险。
*   **复杂规划瓶颈**：尽管有增强，自主规划在处理极度复杂的科学任务时仍需人类频繁干预。

（完）

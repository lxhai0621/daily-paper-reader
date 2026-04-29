---
title: Human-supervised Agentic AI for Hypothesis Generation and Experimental Assistance in Drug Repurposing
authors: "Huynh, D.-L., Asp, E., Ballante, F., Puigvert, J. C., DeGrave, A., Karki, R., Nader, K., Östling, P., Pokharel, B., Rietdijk, J., Schlotawa, L., Schmidt, L., Seal, S., Seashore-Ludlow, B., Aittokallio, T., Spjuth, O."
date: 2026-04-22
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719538v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.5
evidence: 具有情境记忆和检索增强生成的层级多智能体系统
tldr: 本研究针对药物重定向全生命周期支持不足的问题，开发了RepurAgent系统。这是一个层级化多智能体AI框架，通过监督和规划智能体协调研究、预测、数据和报告四个子智能体，并引入人机协作、情境记忆与RAG技术。实验证明，该系统在AML、新冠肺炎及罕见病研究中表现卓越，能高效生成假设并辅助实验分析，显著缩短研发周期，是药物重定向领域的有力工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的计算药物重定向方法大多局限于快速生成假设，无法覆盖从实验设计到数据分析的完整研发周期。
method: 提出RepurAgent系统，利用层级化多智能体架构和人机协作模式，整合特定领域的工具与标准操作程序。
result: "系统在多项任务中表现优异，包括在AML研究中达到97%的通路恢复率，以及在新冠药物筛选中实现0.98的AUC-ROC。"
conclusion: 智能体AI能够贯穿药物重定向的整个生命周期，通过自动化与人类监督的结合，大幅提升药物研发的效率和可靠性。
---

## Abstract
Computational drug repurposing has largely been focused on rapid hypothesis generation, yet real-world applications span a far broader lifecycle, from drug candidate suggestion to designing experiments, analyzing assay data, and iteratively refining candidates. Here, we demonstrate that agentic AI can fulfill this entire scope. To this end, we developed RepurAgent, a hierarchical multi-agent AI system comprising a supervisor agent and a planning agent that coordinate four specialized sub-agents -- research, prediction, data, and report -- through a human-in-the-loop design, with episodic memory and retrieval-augmented generation. The system is grounded in data, tools, and standard operating procedures specific for drug repurposing, developed within the REMEDi4ALL consortium. We validated the agentic system across three scenarios spanning the various stages within the repurposing lifecycle: in Acute Myeloid Leukemia, RepurAgent recovered up to 97% of disease-relevant pathways identified by Google Co-Scientist, completing the workflow within 60 minutes; in a retrospective COVID-19 antiviral screen, RepurAgent acted as an adaptive experimental collaborator, prioritizing compounds with AUC-ROC up to 0.98 without predefined thresholds and flagging confounders missed in manual review; and for Multiple Sulfatase Deficiency, it prioritized 82 high-confidence candidates from 5000 compounds, which were further corroborated by domain experts. These results demonstrate that agentic AI can support across the full drug repurposing lifecycle, from hypothesis generation to experimental analysis. RepurAgent is open source and deployed at https://repuragent.serve.scilifelab.se/.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **RepurAgent** 的人机协作多智能体 AI 系统，旨在解决药物重定向（Drug Repurposing）过程中工具碎片化、无法覆盖全生命周期的问题。

以下是对该论文的结构化总结：

### 1. 核心问题与研究动机
*   **核心问题**：传统的计算药物重定向方法主要集中在“假设生成”（即预测候选药物）这一单一环节，而忽略了药物研发的完整生命周期，包括实验设计、多源数据整合、实验结果分析、混杂因素检测以及候选药物的迭代优化。
*   **研究动机**：现有的知识图谱（KG）、机器学习模型和文献挖掘工具彼此孤立，导致科学家在整合异构数据和处理实验反馈时负担沉重。研究者希望通过“智能体 AI”（Agentic AI）构建一个能够自主规划、调用工具并与人类协作的连续工作流系统。

### 2. 方法论
*   **核心思想**：采用层级化多智能体架构，通过“规划-执行-监督”的闭环模式，将复杂的药物重定向任务分解为可管理的子任务。
*   **关键技术细节**：
    *   **多智能体架构**：包含一个**规划智能体**（负责制定工作流）、一个**监督智能体**（负责协调）以及四个专业子智能体：**研究智能体**（文献/数据库检索）、**预测智能体**（ADMET 属性预测）、**数据智能体**（Python 代码生成与实验分析）和**报告智能体**（结果汇总）。
    *   **推理模式**：采用 **ReAct**（Reasoning and Acting）模式，使智能体能够动态选择工具并根据中间结果调整策略。
    *   **记忆架构**：设计了三层记忆系统，包括工作记忆（会话内状态）、短期记忆（对话上下文）和**长期情节记忆**（存储成功的任务分解经验，通过向量检索辅助未来规划）。
    *   **检索增强生成（RAG）**：系统集成了 REMEDi4ALL 联盟开发的**标准操作程序（SOPs）**，确保 AI 的推理符合实验室规范和科学标准。
    *   **工具集成**：整合了知识图谱生成器（KGG）、化学注释器、CPSign（共形预测模型）等专业生物医药工具。

### 3. 实验设计
*   **应用场景**：
    1.  **急性髓系白血病（AML）**：端到端的候选药物生成与通路分析。
    2.  **COVID-19 抗病毒筛选（回顾性）**：对 5275 种化合物的实验数据进行自动化分析、排名和混杂因素检测。
    3.  **多重硫酸酯酶缺乏症（MSD，超罕见病）**：在数据极度稀缺的情况下，通过文献推理进行药物优先级排序。
*   **Benchmark 与对比方法**：
    *   **AML 场景**：对比了 **Google Co-Scientist**（专家密集型管线）和 6 种 **Vanilla LLMs**（如 GPT-4o 直接生成）。
    *   **COVID-19 场景**：对比了人类专家的手动分析结果（Asp et al. 2025）。
    *   **消融实验**：针对规划智能体，测试了 SOP 检索、文献搜索和情节记忆对规划质量的影响。

### 4. 资源与算力
*   **算力说明**：论文未详细列出本地 GPU 训练算力。
*   **模型使用**：系统主要基于 OpenAI 的 API 构建，规划智能体使用 **GPT-4o**，其他智能体使用 **GPT-4o-mini**。
*   **部署**：系统作为开源 Web 应用部署在 SciLifeLab Serve 上。

### 5. 实验数量与充分性
*   **实验规模**：
    *   在规划能力评估中，使用了 15 个任务请求（5 个真实案例，10 个合成案例），每种配置运行 10 次，共计数百次运行。
    *   使用了 Kruskal-Wallis 检验和带 Holm 校正的 Mann-Whitney U 检验进行统计显著性分析。
*   **充分性评价**：实验覆盖了从常见癌症到超罕见病、从纯计算预测到实验数据分析的多个维度，实验设计较为客观、公平，特别是消融实验有力证明了各组件的贡献。

### 6. 主要结论与发现
*   **性能卓越**：在 AML 案例中，RepurAgent 恢复了 Google Co-Scientist 识别的 **97%** 的相关通路，且在 60 分钟内完成。
*   **分析精准**：在 COVID-19 筛选中，系统在无预设阈值的情况下实现了 **0.98** 的 AUC-ROC，与专家选择高度一致，并发现了人工复核遗漏的混杂因素（如细胞毒性导致的假阳性）。
*   **罕见病突破**：在 MSD 案例中，系统从 5000 种化合物中筛选出 82 种高置信度候选药，其中一种得到了领域专家的独立实验验证。
*   **人机协作必要性**：消融实验显示，即使是性能最好的配置，规划质量得分也仅为 0.651，证明了“人机回环”（Human-in-the-loop）在复杂科学任务中的不可或缺性。

### 7. 优点
*   **全生命周期覆盖**：打破了以往工具只管预测不管分析的局限。
*   **知识扎根（Grounding）**：通过 RAG 引入 SOP，使 AI 行为受到科学规范的约束，而非仅仅依赖 LLM 的参数记忆。
*   **透明与可追溯**：系统展示完整的推理链条和工具调用过程，方便科学家审计。
*   **高效性**：将数周的人工分析工作缩短至分钟级。

### 8. 不足与局限
*   **前瞻性验证不足**：AML 和 MSD 的候选药物尚未进行大规模湿实验验证（部分受限于知识产权）。
*   **模型依赖**：系统高度依赖闭源的 GPT 系列模型，其性能受限于底层模型的更新和 API 稳定性。
*   **基准缺失**：目前领域内缺乏公认的端到端智能体评估基准，导致跨系统比较具有挑战性。
*   **幻觉风险**：尽管有工具约束，但在处理极其复杂的文献推理时，仍存在产生科学幻觉的潜在风险。

（完）

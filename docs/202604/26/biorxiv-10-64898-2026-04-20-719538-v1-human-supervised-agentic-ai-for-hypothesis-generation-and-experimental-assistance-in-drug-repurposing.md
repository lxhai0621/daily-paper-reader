---
title: Human-supervised Agentic AI for Hypothesis Generation and Experimental Assistance in Drug Repurposing
authors: "Huynh, D.-L., Asp, E., Ballante, F., Puigvert, J. C., DeGrave, A., Karki, R., Nader, K., Östling, P., Pokharel, B., Rietdijk, J., Schlotawa, L., Schmidt, L., Seal, S., Seashore-Ludlow, B., Aittokallio, T., Spjuth, O."
date: 2026-04-22
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719538v1.full.pdf"
tags: ["query:ma-kf"]
score: 10.0
evidence: 具有情节记忆和检索增强生成的药物再利用多智能体AI系统
tldr: RepurAgent利用具有RAG和记忆功能的层级多智能体系统，实现了自动化的药物再利用工作流。
source: biorxiv
selection_source: fresh_fetch
motivation: 具有情节记忆和检索增强生成的药物再利用多智能体AI系统。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Computational drug repurposing has largely been focused on rapid hypothesis generation, yet real-world applications span a far broader lifecycle, from drug candidate suggestion to designing experiments, analyzing assay data, and iteratively refining candidates. Here, we demonstrate that agentic AI can fulfill this entire scope. To this end, we developed RepurAgent, a hierarchical multi-agent AI system comprising a supervisor agent and a planning agent that coordinate four specialized sub-agents -- research, prediction, data, and report -- through a human-in-the-loop design, with episodic memory and retrieval-augmented generation. The system is grounded in data, tools, and standard operating procedures specific for drug repurposing, developed within the REMEDi4ALL consortium. We validated the agentic system across three scenarios spanning the various stages within the repurposing lifecycle: in Acute Myeloid Leukemia, RepurAgent recovered up to 97% of disease-relevant pathways identified by Google Co-Scientist, completing the workflow within 60 minutes; in a retrospective COVID-19 antiviral screen, RepurAgent acted as an adaptive experimental collaborator, prioritizing compounds with AUC-ROC up to 0.98 without predefined thresholds and flagging confounders missed in manual review; and for Multiple Sulfatase Deficiency, it prioritized 82 high-confidence candidates from 5000 compounds, which were further corroborated by domain experts. These results demonstrate that agentic AI can support across the full drug repurposing lifecycle, from hypothesis generation to experimental analysis. RepurAgent is open source and deployed at https://repuragent.serve.scilifelab.se/.
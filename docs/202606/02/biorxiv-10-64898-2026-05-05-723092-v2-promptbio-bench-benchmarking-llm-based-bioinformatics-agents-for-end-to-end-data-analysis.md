---
title: "PromptBio-Bench: Benchmarking LLM-based Bioinformatics Agents for End-to-End Data Analysis"
title_zh: PromptBio-Bench：基于大语言模型的生物信息学代理在端到端数据分析中的基准评测
authors: "Guo, W., Zhang, M., Han, B., Ma, Y., Leng, Y., Hebbar, S., Zhou, X., Gu, W., Yang, X., Dhar, S."
date: 2026-06-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.05.723092v2.full.pdf"
tags: ["query:agent"]
score: 6.0
evidence: 基于大语言模型的智能体
tldr: 大型语言模型（LLM）智能体有望自动化生物信息学分析，但缺乏系统评估。为此，我们提出PromptBio-Bench，一个包含244个专家策划任务的综合评估套件，并设计了结构化文件比较与评分框架。评估三个顶级生物信息学智能体发现，Biomni和ToolsGenie性能相当，且所有智能体随任务难度增加准确性显著下降。PromptBio-Bench为追踪智能体生物信息学进展提供了关键基准设施。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有LLM生物信息学智能体缺乏系统评估，无法衡量其实际应用准备度。
method: 构建244个专家任务的PromptBio-Bench套件与结构化文件评分框架。
result: Biomni与ToolsGenie表现相当，但所有智能体在高难度任务上准确性显著下降。
conclusion: PromptBio-Bench为生物信息学智能体进展提供了可追踪的基准。
---

## 摘要
基于大语言模型（LLM）的代理在自动化生物信息学工作流方面具有变革潜力；然而，对其能力的系统评估仍然有限，阻碍了对其实用应用准备情况的清晰评估。我们提出了PromptBio-Bench，这是一个包含244个专家精心策划任务的综合评估套件，任务涵盖不同难度级别的生物信息学和数据科学领域，并提供了一个结构化文件比较和评分评估框架，用于与专家参考答案文件进行比较。对三种最先进的生物信息学代理的评估显示，Biomni和ToolsGenie的表现相当，所有代理的准确率随着任务难度的增加而显著下降。随着基础模型和代理框架的不断发展，PromptBio-Bench为系统跟踪代理式生物信息学的进展提供了宝贵的基准基础设施。

## Abstract
Large language model (LLM)-based agents hold transformative potential for automating bioinformatics workflows; however, systematic evaluations of their capabilities remain limited, hindering a clear assessment of their readiness for real-world application. We introduce PromptBio-Bench, a comprehensive evaluation suite of 244 expert-curated tasks spanning bioinformatics and data science at varied difficulty levels, and an evaluation framework for structured file comparison and scoring against expert reference answer files. Evaluation of three state-of-the-art bioinformatics agents revealed comparable performance between Biomni and ToolsGenie, with all agents showing a marked decline in accuracy as task difficulty increased. As foundation models and agent frameworks continue to evolve, PromptBio-Bench provides a valuable benchmark infrastructure for systematically tracking progress in agentic bioinformatics.
---
title: Reproducible and shareable bioinformatics pipelines from natural-language prompts
title_zh: 从自然语言提示生成可重现和可共享的生物信息学流程
authors: "Kim, H.-M., Jeong, H., Mekonnen, A. M., Kim, Y., Oh, Y., Lee, H., Jung, C., Park, J."
date: 2026-06-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.28.719125v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 基于LLM的从自然语言提示生成可复现管线的平台，集成外部工具
tldr: 大语言模型生成的生物信息学流水线难以复现和共享。Autopipe通过模型上下文协议（MCP）引导LLM生成容器化流水线，支持远程服务器执行和结果可视化。平台包含桌面应用、在线注册表、Web查看器和CLI工具。将自然语言对话转化为可重复执行且可分享的工作流。
source: biorxiv
selection_source: fresh_fetch
motivation: 解决大语言模型生成的生物信息学流水线不可复现、不可远程执行和难以共享的问题。
method: 构建Autopipe平台，通过MCP协议引导LLM生成容器化流水线，并集成远程执行与可视化。
result: 开发了桌面应用、在线注册表、Web结果查看器和CLI工具，实现流水线的全流程管理。
conclusion: 将自然语言交互分析转化为可重复、可共享的容器化工作流，提升生物信息学研究可靠性。
---

## 摘要
大语言模型（LLM）正越来越多地被用于生成生物信息学流程，并从自然语言提示中进行分析。然而，由于LLM驱动对话的非确定性和本地执行环境的异质性，生成的分析往往难以在不同会话间重现，并且无法在远程高性能计算（HPC）服务器上运行、共享或复用。我们提出Autopipe平台，它引导任何兼容模型上下文协议（MCP）的LLM来生成、执行和发布保留源代码、可重新执行的容器化流程。Autopipe使用户能够在任何本地远程服务器上执行生物信息学流程——依托面向无服务器管理经验的研究人员的全面设置文档——并通过可扩展的基于Web的查看器可视化结果。Autopipe平台包含四个组件：一个带有嵌入式MCP服务器的桌面应用程序用于流程管理和远程执行、一个用于流程和插件发现的在线注册中心、一个基于Web的结果查看器，以及一个用于定制查看器插件的CLI工具。Autopipe将对话式分析转化为可重新执行和可共享的工作流程。Autopipe免费提供于https://autopipe.org/。

## Abstract
Large language models (LLMs) are increasingly used to generate bioinformatics pipelines and to carry out analyses from natural-language prompts. However, the resulting analyses are often difficult to reproduce across sessions, owing to the non-deterministic nature of LLM-driven conversations and heterogeneity of local execution environments, and cannot run on remote high-performance computing (HPC) servers or be shared and reused. We present Autopipe, a platform that guides any Model Context Protocol (MCP) - compatible LLM to produce, execute, and publish source-preserved, re-executable containerized pipelines. Autopipe enables users to execute bioinformatics pipelines on any on-premises remote servers - supported by comprehensive setup documentation aimed at researchers without prior server-administration experience - and to visualize results through an extensible web-based viewer. The Autopipe platform comprises four components: a desktop application with an embedded MCP server for pipeline management and remote execution, an online registry for pipeline and plugin discovery, a web-based result viewer, and a CLI tool for customizing viewer plugins. Autopipe turns conversational analysis into re-executable and shareable workflows. Autopipe is freely available at https://autopipe.org/.
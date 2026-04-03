---
title: Searching the Druggable Genome using Large Language Models
title_zh: 使用大语言模型搜索可成药基因组
authors: "Schimmelpfennig, L. E., Cannon, M., Cody, Q., McMichael, J., Coffman, A., Kiwala, S., Krysiak, K. J., Wagner, A. H., Griffith, M., Griffith, O. L."
date: 2026-04-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.01.18.700012v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过模型上下文协议将大语言模型与外部数据库API集成
tldr: 本研究针对药物-基因相互作用数据库（DGIdb）查询门槛高的问题，开发了DGIdb模型上下文协议（MCP）服务器。该工具使大语言模型（LLM）能够通过自然语言直接访问DGIdb API，获取最新的生物医学知识。实验证明，该方法显著提升了LLM在处理复杂药物基因组学问题时的准确性和实时性，为临床和科研提供了更便捷的交互方式。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-01-18-700012-v2/fig-001.webp\", \"caption\": \"Figure 1. Joint use of the CIViC MCP and DGIdb MCP servers for drug candidate selection 201 with Claude. A user asks, “What genes can cause resistance to Ibrutinib in Chronic Lymphocytic 202 Leukemia, and what alternative drugs can target them?” The LLM: (1) extracts the users intent 203\", \"page\": 10, \"index\": 1, \"width\": 1052, \"height\": 1183}]"
motivation: 传统的DGIdb数据库需要结构化查询，限制了非专业用户通过自然语言获取药物-基因相互作用信息的效率。
method: 开发了基于模型上下文协议（MCP）的服务器，将DGIdb API集成到大语言模型中，实现自然语言到数据库查询的自动转换。
result: 该MCP服务器使LLM能够实时访问外部结构化资源，显著增强了其回答需要精确生物医学知识问题的能力。
conclusion: 通过MCP协议连接LLM与专业数据库，是提升AI在生物医学领域实用性和准确性的有效途径。
---

## 摘要
可成药基因组（druggable genome）涵盖了已知或预测与药物相互作用的基因。药物-基因相互作用数据库（DGIdb）为发现这些相互作用并将其情境化提供了一个综合资源，支持广泛的研究和临床应用。目前，DGIdb 主要通过结构化的 Web 界面和 API 调用进行访问，这要求用户将自然语言问题转化为特定于数据库的查询模式。为了实现通过自然语言使用 DGIdb，我们开发了 DGIdb 模型上下文协议（MCP）服务器，该服务器允许大语言模型（LLMs）通过 DGIdb API 获取最新信息。我们证明了 MCP 服务器显著增强了大语言模型回答需要从结构化外部资源中提取准确、最新生物医学知识的问题的能力。可用性与实现：DGIdb MCP 服务器的详细信息见 https://github.com/griffithlab/dgidb-mcp-server，并包含通过 Claude 桌面应用程序访问该服务器的说明。

## Abstract
The druggable genome encompasses the genes that are known or predicted to interact with drugs. The Drug-Gene Interaction Database (DGIdb) provides an integrated resource for discovering and contextualizing these interactions, supporting a broad range of research and clinical applications. DGIdb is currently accessed through structured web interfaces and API calls, requiring users to translate natural-language questions into database-specific query patterns. To allow for the use of DGIdb through natural language, we developed the DGIdb Model Context Protocol (MCP) server, which allows large language models (LLMs) access to up-to-date information through the DGIdb API. We demonstrate that the MCP server greatly enhances an LLM's ability to answer questions requiring accurate, up-to-date biomedical knowledge drawn from structured external resources. Availability and implementation: The DGIdb MCP server is detailed at https://github.com/griffithlab/dgidb-mcp-server and includes instructions for accessing the server through the Claude desktop app.

---

## 论文详细总结（自动生成）

### 论文总结：使用大语言模型搜索可成药基因组

#### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：如何让大语言模型（LLM）能够准确、实时地访问结构化的生物医学数据库，以解决其内部知识陈旧、易产生幻觉（Hallucination）以及无法处理复杂结构化查询的问题。
*   **研究背景**：药物-基因相互作用数据库（DGIdb）是精准医疗的重要资源，但其传统的访问方式（Web界面或API）要求用户具备结构化查询知识。在处理如“获得性耐药性分析”等复杂临床问题时，研究人员需要手动整合多个基因和药物列表，效率低下。

#### 2. 论文提出的方法论
*   **核心思想**：利用**模型上下文协议（Model Context Protocol, MCP）**构建一个桥梁（MCP服务器），将 DGIdb 的结构化数据能力直接暴露给 LLM。
*   **关键技术细节**：
    *   **MCP 服务器架构**：部署在 Cloudflare 上，提供四个核心工具，通过预定义的 GraphQL 查询与 DGIdb API 交互。
    *   **功能模块**：包括药物信息查询（FDA状态、分类）、基因信息查询（类别、成药性属性）以及药物-基因相互作用查询。
    *   **排序机制**：返回的相互作用结果根据 FDA 批准状态和 DGIdb 交互评分（基于证据强度和特异性）进行排序。
    *   **实体标准化**：为了处理拼写差异和别名，服务器集成了 VICC 标准化服务，并使用 **Dice 系数（Dice’s coefficient）**对双字母组合（bigrams）进行相似度评分，实现输入归一化。

#### 3. 实验设计
*   **实验场景与数据集**：
    1.  **分类任务**：从 DGIdb 中分层抽样 100 种药物，要求模型识别其 FDA 批准状态、是否为免疫疗法、是否为抗肿瘤药。
    2.  **隐式调用测试**：在不明确指示使用 DGIdb 的情况下，观察模型是否会主动调用 MCP 工具。
    3.  **多跳推理任务（Multi-hop）**：结合 **CIViC MCP**（癌症变异解释数据库）和 **DGIdb MCP**，处理如“识别导致伊布替尼耐药的基因并寻找替代药物”的复杂问题。
*   **Benchmark 与对比方法**：以 **GPT-5**（注：文中提及，可能指代当时最先进模型版本）作为基座模型，对比“原生 LLM”与“增强型 LLM（挂载 MCP）”的表现。
*   **评价指标**：F1 分数（分类准确性）、Precision/Recall、以及 **NDCG**（归一化折损增益，用于衡量排序质量）。

#### 4. 资源与算力
*   **算力说明**：论文**未明确说明**具体的 GPU 型号、数量或训练时长。
*   **实现环境**：MCP 服务器运行在 Cloudflare Workers 上（强调了其轻量化和低内存占用），LLM 端主要提及了 Claude 桌面应用和 GPT 系列模型的使用。

#### 5. 实验数量与充分性
*   **实验规模**：
    *   100 种药物的属性分类实验。
    *   50 组随机选择的“疾病-疗法”组合用于多跳推理测试。
*   **充分性评价**：实验设计较为充分，涵盖了从基础信息检索到复杂逻辑推理的多个维度。通过对比实验证明了 MCP 在提升准确率和排序质量方面的显著作用。实验过程客观，使用了标准的信息检索指标（如 NDCG）。

#### 6. 论文的主要结论与发现
*   **性能提升**：挂载 DGIdb MCP 后，LLM 在药物分类任务中的加权 F1 分数从 0.75 提升至 **0.99**。
*   **多跳推理能力**：在寻找耐药替代药物的任务中，F1 分数从 0.14 飙升至 **0.95**，NDCG 从 0.19 提升至 **0.93**。
*   **提示词依赖性**：发现 LLM 并不总是自动调用 MCP。如果提示词中未明确提及“DGIdb”，模型倾向于使用其不可靠的内部知识，导致准确率下降（尤其是针对不常见的复杂分子）。
*   **协同效应**：证明了多个 MCP 服务器（如 CIViC + DGIdb）可以协同工作，支持复杂的生物医学推理工作流。

#### 7. 优点
*   **标准化与互操作性**：采用 MCP 协议，使得不同实验室开发的工具可以轻松集成到同一个 LLM 环境中。
*   **实时性与准确性**：通过 API 实时获取最新数据，彻底解决了 LLM 知识滞后的问题，并提供了可追溯的证据链接。
*   **易用性**：将复杂的生物信息学查询简化为自然语言对话，降低了科研门槛。

#### 8. 不足与局限
*   **提示词敏感性**：模型对是否调用工具的判断不够智能，高度依赖用户在提示词中明确指定数据源。
*   **覆盖范围限制**：目前仅限于 DGIdb 提供的工具集，对于更广泛的生物医学问题，仍需开发更多的 MCP 插件。
*   **潜在偏差**：如果底层数据库（如 DGIdb）存在收录偏差，LLM 的回答也会继承这些偏差。
*   **应用限制**：目前主要展示了在 Claude 等桌面端的集成，大规模自动化流水线的稳定性尚待验证。

（完）

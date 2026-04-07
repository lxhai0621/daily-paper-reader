---
title: "CIViC MCP: Integrating Large Language Models with the Clinical Interpretations of Variants in Cancer"
title_zh: CIViC MCP：将大语言模型与癌症变异临床解释集成
authors: "Schimmelpfennig, L. E., Cody, Q., McMichael, J., Coffman, A., Khanfar, M., Li, J., Yao, J., Saliba, J., Danos, A., Kiwala, S., Wagner, A. H., Sanz-Cruzado, J., Lever, J., Griffith, M., Griffith, O. L."
date: 2026-04-07
pdf: "https://www.biorxiv.org/content/10.1101/2025.10.13.682185v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过大语言模型以自然语言对接API
tldr: 本研究开发了 CIViC MCP 服务器，旨在将大型语言模型（LLM）与“癌症变异临床解释”（CIViC）知识库集成。通过模型上下文协议（MCP），用户可以使用自然语言直接与 CIViC API 交互，从而快速总结和分析专家策划的癌症分子变异生物学及临床意义。该工具显著提升了复杂变异信息的检索效率，并提供了开源实现和在线聊天机器人。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-10-13-682185-v2/fig-001.webp\", \"caption\": \"\", \"page\": 9, \"index\": 1, \"width\": 1299, \"height\": 1398}]"
motivation: 旨在解决用户在 CIViC 知识库中建立复杂信息连接的难题，通过自然语言交互提升癌症变异解读的效率。
method: 开发了基于模型上下文协议（MCP）的服务器，将 CIViC API 与 LLM（如 Claude 和 GPT）无缝对接。
result: 实现了通过自然语言对专家策划的癌症变异数据进行快速总结和查询，并提供了开源代码及在线聊天工具。
conclusion: CIViC MCP 为临床医生和研究人员提供了一种更直观、高效的方式来利用高质量的癌症基因组学知识。
---

## 摘要
摘要：癌症变异临床解释 (CIViC) 知识库提供了一个社区驱动的开源平台，用于讨论癌症分子变异的生物学和临床意义。为了使用户能够在 CIViC 信息之间建立复杂的联系，我们开发了 CIViC 模型上下文协议 (MCP) 服务器，该服务器允许用户通过大语言模型 (LLMs) 以自然语言与 CIViC API 进行交互，从而促进对专家策划的癌症变异解释进行快速总结。可用性与实现：CIViC MCP 服务器的详细信息见 https://github.com/griffithlab/civic-mcp-server。该仓库包含了通过 Claude 桌面应用（我们推荐的方法；见补充图 1）访问服务器以及使用 GPT-5 进行本地托管的说明，并提供了一个用于直接查询 MCP 服务器的 Python 脚本。我们还为 CIViC 用户提供了一个支持 MCP 的聊天机器人，网址为 https://civicdb.org/mcp-chat。

## Abstract
Summary: The Clinical Interpretation of Variants in Cancer (CIViC) knowledgebase provides a community-driven, open-source platform for discussing the biological and clinical significance of molecular variants in cancer. To enable users to make complex connections between CIViC information, we developed the CIViC Model Context Protocol (MCP) server, which allows users to interface with the CIViC API through natural language via large language models (LLMs), facilitating the rapid summarization of expertly curated cancer variant interpretations. Availability and implementation: The CIViC MCP server is detailed at https://github.com/griffithlab/civic-mcp-server. The repository includes instructions for accessing the server through the Claude desktop app (our recommended approach; Supplementary Figure 1) and hosting it locally with GPT-5, as well as a Python script for directly querying the MCP server. We also provide an MCP-supported Chatbot for CIViC users at https://civicdb.org/mcp-chat.

---

## 论文详细总结（自动生成）

这篇论文介绍了一种名为 **CIViC MCP** 的工具，旨在通过“模型上下文协议”（Model Context Protocol, MCP）将大语言模型（LLM）与“癌症变异临床解释”（CIViC）专业知识库进行深度集成。以下是对该论文的结构化总结：

### 1. 论文的核心问题与整体含义
*   **研究背景**：精准肿瘤学依赖于对癌症分子变异的临床解读。CIViC 是一个社区驱动的开源知识库，存储了大量专家策划的变异证据。
*   **核心问题**：虽然 LLM 擅长处理自然语言，但在处理高度专业、实时更新且结构复杂的生物医学数据时存在三大挑战：
    1.  **幻觉风险**：LLM 可能会编造临床细节或参考文献。
    2.  **知识滞后**：预训练数据无法覆盖最新的研究进展。
    3.  **理解偏差**：LLM 难以准确把握 CIViC 特有的复杂数据模型（如“分子谱”或“断言”）。
*   **整体含义**：通过开发 MCP 服务器，研究者为 LLM 提供了一个标准化的、直接访问 CIViC 结构化数据的通道，从而实现准确、可追溯且高效的癌症变异信息检索与总结。

### 2. 论文提出的方法论
*   **核心思想**：利用 **Model Context Protocol (MCP)** 协议，在 LLM 和 CIViC 的 GraphQL API 之间建立一个中介服务器。
*   **关键技术细节**：
    *   **预定义查询工具**：为了避免 LLM 直接编写 GraphQL 查询语句时出现语法错误，服务器预定义了两个核心工具：`get_variant_evidence`（检索具体研究证据）和 `get_variant_assertions`（检索高层级临床总结）。
    *   **实体标准化（Normalization）**：用户输入的非规范名称（如药物别名、癌症俗称）会通过 **Dice 系数（Dice’s coefficient）** 算法与 CIViC 的首选标签进行匹配。
    *   **外部本体集成**：利用 VICC 基因标准化服务、疾病本体（Disease Ontology）和 NCI 词表（NCI Thesaurus）构建别名列表，确保匹配的准确性。
    *   **可追溯性**：每个生成的回答都包含 CIViC 原始链接和 PubMed ID，方便用户核实。

### 3. 实验设计
*   **实验场景**：受控分类任务。给定一个“变异-癌症类型-疗法”的三元组，要求模型判断该组合在 CIViC 中是否存在支持性的临床意义证据。
*   **数据集**：从 CIViC 中随机抽取了 **100 个三元组**。
*   **对比方法（Benchmark）**：
    1.  **GPT-5 独立模式**：仅依靠模型预训练知识回答。
    2.  **GPT Agent 模式**：通过模拟浏览器导航和搜索网页来获取信息。
    3.  **GPT-5 + CIViC MCP**：通过 MCP 服务器直接调用结构化 API。
*   **评估指标**：准确率（Accuracy）、加权 F1 分数、响应延迟（Latency）。

### 4. 资源与算力
*   **算力说明**：文中**未明确提及**具体的 GPU 型号、数量或训练时长。
*   **实现环境**：MCP 服务器托管在 **Cloudflare Workers** 上（利用其轻量、快速的特性）。实验主要涉及推理和 API 调用，而非模型训练。

### 5. 实验数量与充分性
*   **实验规模**：使用了 100 组随机抽样的测试用例。
*   **充分性评价**：
    *   **优点**：实验设计了三种模式的对比，涵盖了目前 LLM 获取外部信息的主要方式（原生知识、网页浏览、结构化 API），对比维度较为全面。
    *   **局限**：100 组样本量对于生物医学领域的大规模验证来说相对较小，且主要集中在分类任务上，未对长文本总结的质量进行大规模量化评估。

### 6. 论文的主要结论与发现
*   **性能飞跃**：**GPT-5 + MCP** 的表现远超其他模式，准确率达到 **0.95**，加权 F1 分数为 **0.98**。相比之下，GPT-5 独立模式的准确率仅为 0.30。
*   **效率优势**：MCP 模式的响应时间（约 43 秒）与独立模式相当，但比 Agent 模式（约 425 秒）快了近 **10 倍**。
*   **可靠性**：通过直接访问 API，显著降低了幻觉风险，并提供了精确的文献引用。

### 7. 优点
*   **标准化**：采用 MCP 协议，使其易于集成到 Claude 或 GPT 等多种主流 LLM 客户端中。
*   **低延迟**：相比于耗时的网页爬取（Agent 模式），结构化 API 调用极大地提升了用户体验。
*   **鲁棒性**：通过实体标准化处理了生物医学领域常见的命名歧义问题。

### 8. 不足与局限
*   **灵活性受限**：目前采用预定义查询而非让 LLM 动态生成查询，虽然保证了稳定性，但限制了处理极其复杂或非预期问题的能力。
*   **实体匹配风险**：Dice 系数虽然计算快，但在处理极度相似或复杂的别名时，准确性可能不如更复杂的语义匹配算法。
*   **应用范围**：目前仅限于 CIViC 数据库，尚未实现跨多个生物医学数据库（如 ClinVar, OncoKB）的联合检索。

（完）

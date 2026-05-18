---
title: "TogoMCP: Natural Language Querying of Life-Science Knowledge Graphs via Schema-Guided LLMs and the Model Context Protocol"
title_zh: TogoMCP：通过模式引导的 LLM 和模型上下文协议实现生命科学知识图谱的自然语言查询
authors: "Kinjo, A. R., Yamamoto, Y., Bustamante-Larriet, S., Labra-Gayo, J. E., Fujisawa, T."
date: 2026-05-17
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.19.713030v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过LLM和模型上下文协议查询生命科学知识图谱
tldr: 针对生命科学知识图谱查询门槛高的问题，本研究开发了TogoMCP系统。该系统利用模型上下文协议（MCP）和元数据互操作交换（MIE）文件，为大语言模型提供动态模式上下文。通过将实体解析与SPARQL生成分离的两阶段工作流，显著提升了自然语言转查询语句的准确性，在多数据库基准测试中表现优异。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统的生命科学知识图谱查询需要复杂的SPARQL知识和对特定数据库模式的深入理解，限制了非专业研究者的使用。
method: 采用MCP协议构建推理引擎，结合MIE文件提供动态模式上下文，并实施实体解析与SPARQL生成分离的两阶段工作流。
result: "在包含23个数据库的基准测试中，TogoMCP显著优于基线模型，胜率超过80%，且MIE模式文件对性能提升贡献最大。"
conclusion: 简洁且动态交付的模式上下文对于提升LLM查询性能至关重要，而程序化引导则在降低错误风险和减少方差方面发挥互补作用。
---

## 摘要
查询由 DBCLS 维护的 RDF Portal 知识图谱（该图谱汇集了约 60 个生命科学数据库）需要精通 SPARQL 和特定数据库的 RDF 模式，这使得大多数研究人员难以利用这一资源。大语言模型（LLMs）原则上可以将自然语言问题转化为可执行的 SPARQL，但由于缺乏模式层面的上下文，它们经常会伪造不存在的谓词，或者无法将实体名称解析为特定数据库的标识符。我们提出了 TogoMCP，该系统将 LLM 重塑为一种协议驱动的推理引擎，通过模型上下文协议（MCP）编排专用工具。其设计中有两个关键机制：(i) MIE（元数据互操作性交换）文件，这是一种简洁的 YAML 文档，在查询时动态地为 LLM 提供每个目标数据库的结构和语义上下文；(ii) 一个两阶段工作流，将通过外部 REST API 进行的实体解析与模式引导的 SPARQL 生成相分离。在涵盖 5 种类型和 23 个数据库的 50 个生物学问题的基准测试中，TogoMCP 相比无辅助的基准模型取得了显著提升（Cohen's d = 1.82, Wilcoxon p < 0.001），对于具有精确、可验证答案的问题类型，胜率超过 80%。消融研究表明，所有组件配置都带来了显著改进，其中 MIE 模式文件对每个问题的平均得分贡献最大（相对于无 MIE 情况，Δ = +0.50，双侧 Wilcoxon p = 0.067；90% bootstrap 置信区间 [+0.04, +0.94] 不包含零）；加载相关 MIE 文件的单行指令即可获得与完整程序协议相同的平均提升，而协议还额外降低了下行风险（失败率 1.6% 对比 4.8%，Fisher p = 0.036）。这些结果提出了一个通用的设计原则：对于平均得分表现而言，简洁、动态交付的模式上下文比复杂的编排逻辑更有价值，而程序性引导在缩小方差方面起到了补充作用。

## Abstract
Querying the RDF Portal knowledge graph maintained by DBCLS, which aggregates approximately 60 life-science databases, requires proficiency in both SPARQL and database-specific RDF schemas, placing this resource beyond the reach of most researchers. Large Language Models (LLMs) can, in principle, translate natural-language questions into executable SPARQL, but without schema-level context, they frequently fabricate non-existent predicates or fail to resolve entity names to database-specific identifiers. We present TogoMCP, a system that recasts the LLM as a protocol-driven inference engine orchestrating specialized tools via the Model Context Protocol (MCP). Two mechanisms are essential to its design: (i) the MIE (Metadata-Interoperability-Exchange) file, a concise YAML document that dynamically supplies the LLM with each target database's structural and semantic context at query time; and (ii) a two-stage workflow separating entity resolution via external REST APIs from schema-guided SPARQL generation. On a benchmark of 50 biologically grounded questions spanning five types and 23 databases, TogoMCP achieved a large improvement over an unaided baseline (Cohen's d = 1.82, Wilcoxon p < 0.001), with win rates exceeding 80% for question types with precise, verifiable answers. An ablation study shows that all component configurations deliver significant improvements, with MIE schema files providing the largest marginal contribution on mean per-question score ({Delta} = +0.50 relative to a no-MIE condition, two-sided Wilcoxon p = 0.067; 90% bootstrap CI [+0.04, +0.94] excludes zero); a one-line instruction to load the relevant MIE file recovers the same mean improvement as a full procedural protocol, while the protocol additionally reduces downside risk (loss rate 1.6% vs. 4.8%, Fisher p = 0.036). These results suggest a general design principle: concise, dynamically delivered schema context is more valuable than complex orchestration logic for mean-score performance, while procedural guidance plays a complementary role in narrowing variance.

---

## 论文详细总结（自动生成）

这是一份关于论文《TogoMCP：通过模式引导的 LLM 和模型上下文协议实现生命科学知识图谱的自然语言查询》的深度结构化总结：

### 1. 论文的核心问题与整体含义
*   **研究背景**：生命科学领域积累了海量的知识图谱（KG），如 DBCLS 维护的 RDF Portal 整合了 60 多个数据库。
*   **核心问题**：尽管这些资源价值巨大，但普通研究人员难以利用。主要障碍在于：
    1.  **技术门槛高**：需要精通复杂的 SPARQL 查询语言。
    2.  **模式复杂性**：不同数据库的 RDF 模式（Schema）各异，难以记忆。
    3.  **LLM 的局限性**：通用大语言模型在处理此类任务时，经常会伪造不存在的谓词（幻觉），或无法将自然语言中的实体（如基因名）准确映射到数据库特定的标识符（ID）。
*   **整体含义**：本研究旨在开发一个名为 **TogoMCP** 的系统，通过引入标准化的元数据交换格式和模型交互协议，降低生命科学数据的查询门槛，实现从自然语言到准确 SPARQL 查询的自动化转化。

### 2. 论文提出的方法论
TogoMCP 的核心思想是将 LLM 从单纯的文本生成器转变为一个**协议驱动的推理引擎**。
*   **关键技术细节**：
    *   **模型上下文协议 (MCP)**：采用 Anthropic 开发的 MCP 协议，允许 LLM 动态调用外部工具（如数据库搜索、模式检索、SPARQL 执行）。
    *   **MIE (Metadata-Interoperability-Exchange) 文件**：这是一种简洁的 YAML 格式文档，专门为 LLM 设计。它描述了数据库的类、谓词、示例查询及实体解析方法，作为“即时上下文”提供给模型。
    *   **两阶段工作流**：
        1.  **实体解析阶段**：利用外部 REST API（如 TogoID, TogoVar）将自然语言中的实体转换为数据库内部 ID。
        2.  **SPARQL 生成阶段**：在 MIE 文件提供的模式引导下，结合解析出的 ID 生成并执行 SPARQL。
*   **算法流程**：用户输入问题 -> LLM 识别目标数据库 -> 通过 MCP 加载对应的 MIE 文件 -> 调用实体解析工具获取 ID -> 生成 SPARQL -> 执行并返回结果。

### 3. 实验设计
*   **数据集/场景**：构建了一个包含 **50 个生物学问题**的基准测试集，涵盖 5 种查询类型（单数据库检索、跨数据库关联、统计分析等）。
*   **覆盖范围**：涉及 **23 个不同的生命科学数据库**（如 UniProt, PDB, ChEMBL, ClinVar 等）。
*   **对比方法 (Baselines)**：
    1.  **Vanilla LLM**：无辅助的 Claude 3.5 Sonnet。
    2.  **Prompt-only**：仅在提示词中加入 MIE 内容，不使用 MCP 协议。
    3.  **Full TogoMCP**：结合 MCP 协议、MIE 文件和两阶段工作流的完整系统。

### 4. 资源与算力
*   **模型使用**：主要实验基于 **Claude 3.5 Sonnet** (version 20241022)。
*   **算力说明**：论文**未明确说明**具体的 GPU 硬件型号或训练时长。由于该系统基于现有的 LLM API 进行推理和工具调用（Zero-shot/Few-shot 模式），而非从头训练模型，因此其核心算力消耗在于 API 调用和后端数据库服务器的响应。

### 5. 实验数量与充分性
*   **实验规模**：进行了 50 组核心基准测试，并针对不同组件（MIE 文件、MCP 协议、两阶段流程）进行了**消融实验**。
*   **充分性评价**：
    *   **优点**：实验设计较为严谨，使用了 Cohen's d 效应量和 Wilcoxon 符号秩检验进行统计显著性分析。
    *   **局限**：50 个问题对于复杂的生命科学领域来说样本量相对较小，但覆盖了 23 个数据库，具有较好的代表性。
    *   **公平性**：通过对比“仅提示词”和“协议驱动”两种模式，客观地评估了 MCP 协议本身的边际贡献。

### 6. 论文的主要结论与发现
*   **性能提升显著**：TogoMCP 相比基准模型取得了巨大进步（Cohen's d = 1.82），在可验证答案的问题上胜率超过 80%。
*   **MIE 的核心作用**：消融实验证明，**简洁且动态交付的模式上下文（MIE 文件）是对性能提升贡献最大的因素**（平均分提升 0.50）。
*   **协议的稳定性价值**：虽然简单的提示词也能提升平均分，但 **MCP 协议显著降低了极端错误的发生率**（失败率从 4.8% 降至 1.6%），增强了系统的鲁棒性。
*   **解耦的重要性**：将实体解析与查询生成分离，有效解决了 LLM 在处理生物医学标识符时的幻觉问题。

### 7. 优点
*   **架构优雅**：利用 MCP 协议实现了工具与模型的标准化解耦，易于扩展到更多数据库。
*   **MIE 创新**：提出了一种“对 LLM 友好”的轻量级模式描述格式，比传统的 OWL 或 RDFS 更高效。
*   **实用性强**：直接解决了生命科学领域 RDF 数据“看得见、查不到”的痛点。

### 8. 不足与局限
*   **样本量限制**：基准测试仅包含 50 个问题，可能无法完全覆盖所有复杂的边缘情况。
*   **模型依赖**：系统性能高度依赖于底层 LLM（如 Claude 3.5）的推理能力，在较弱的模型上表现可能大幅下降。
*   **成本与延迟**：多次 API 调用和工具交互会增加查询的响应时间和经济成本。
*   **模式维护**：虽然 MIE 文件简洁，但当底层数据库模式发生重大变化时，仍需人工或半自动地更新这些文件。

（完）

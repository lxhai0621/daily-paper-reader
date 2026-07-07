---
title: Learning API Functionality from In-Context Demonstrations for Tool-based Agents
title_zh: 从上下文演示中学习API功能以用于工具型智能体
authors: "Bhrij Patel, Ashish Jagmohan, Aditya Vempaty"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.994.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 从演示中学习API功能以支持工具型智能体
tldr: 该论文提出从上下文演示中直接学习API功能的新范式，解决了工具型智能体因文档缺失、过时或不一致而难以调用外部API的问题。通过从专家智能体和自探索收集演示，并研究演示需传递的信息，实验表明该方法能有效使智能体学会使用未知API，显著提升智能体集成外部工具的可靠性和泛化能力。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.994/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1639, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.994/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 810, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.994/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.994/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1638, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.994/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1293, \"height\": 1720, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.994/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1574, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.994/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1235, \"height\": 669, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 628, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 734, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 706, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1664, \"height\": 1490, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1249, \"height\": 1169, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 991, \"height\": 780, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.994/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1097, \"height\": 1271, \"label\": \"Table\"}]"
motivation: 智能体依赖API文档，但文档常缺失、过时或不一致，阻碍了通用智能体的开发。
method: 提出从上下文演示中学习API功能，无需文档，通过收集专家和自我探索演示。
result: 实验证明从演示中学习可使智能体成功完成API调用任务。
conclusion: 为无文档场景下的智能体API集成提供了可行方向。
---

## Abstract
Digital tool-based agents, powered by Large Language Models (LLMs), that invoke external Application Programming Interfaces (APIs) often rely on documentation to understand API functionality. However, such documentation is frequently missing, outdated, privatized, or inconsistent—hindering the development of reliable, general-purpose agents. In this work, we propose a new research direction: learning of API functionality directly from in-context demonstrations. This task is a new paradigm applicable in scenarios without documentation. Using API benchmarks, we collect demonstrations from both expert agents and from self-exploration. To understand what information demonstrations must convey for successful task completion, we extensively study how the number of demonstrations and the use of LLM-generated summaries and evaluations affect the task success rate of the API-based agent. Our experiments across 3 datasets and 6 models show that learning functionality from in-context demonstrations remains a non-trivial challenge, even for state-of-the-art LLMs. We find that providing explicit function calls and natural language critiques significantly improves the agent’s task success rate due to more accurate parameter filling. We analyze failure modes, identify sources of error, and highlight key open challenges for future work in documentation-free, self-improving, API-based agents.

---

## 论文详细总结（自动生成）

好的，以下是对给定论文“Learning API Functionality from In-Context Demonstrations for Tool-based Agents”的结构化中文总结。

---

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：当前由大型语言模型驱动的工具型智能体（Tool-based Agents）在执行任务时，通常依赖外部API的文档（Documentation）来理解每个函数的功能和参数信息。然而，现实世界中的API文档经常**缺失、过时、私有化或不一致**，这严重阻碍了通用、可靠智能体的开发。
- **核心问题**：如何在**完全没有文档**的情况下，使API智能体能够学会使用未知的函数。
- **整体含义**：论文提出并定义了一个**全新的研究范式**——直接从**上下文演示（In-Context Demonstrations）** 中学习API的功能，旨在解决文档依赖带来的根本性局限，为构建无文档、自改进的通用智能体铺平道路。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：放弃对预写API文档的依赖，转而利用现成的函数调用演示（例如来自代码库或日志的轨迹）来教导智能体。智能体通过阅读和分析这些演示，**实例化**每个API的功能和参数含义。
- **关键技术细节与流程**：
    1.  **演示收集与定义**：从两个来源收集演示。
        - **专家演示**：来自使用过原始文档的“专家”智能体的成功任务轨迹。
        - **自探索经验**：智能体在训练任务中自行探索、执行函数时获得的经验（包括成功和失败的尝试）。
    2.  **演示信息处理与表示**：通过多种方法将演示“喂给”智能体。
        - **直接演示**：将原始的任务经历和函数调用序列直接放入上下文。
        - **生成文档**：使用一个LLM根据演示来生成函数的功能描述文档。
        - **生成文档+示例调用**：结合了生成的文档和原演示中的函数调用示例。
    3.  **自探索与自我改进**：
        - 智能体先在训练任务上进行自探索，收集执行经验。
        - **LLM评估器**：关键创新点。引入一个LLM作为评估员，对每次函数调用进行**自然语言批评**，指出参数填充、调用顺序等错误，提供更丰富的反馈（而不仅仅是成功/失败的标量奖励）。
        - **更新文本化表征**：基于原始专家演示和自探索经验（及其评估结果），用多种方法更新智能体的API理解，如直接追加经验、更新生成文档、重写文档以及生成经验总结指南。
- **公式与算法（文字说明）**：
    - 论文将任务完成建模为一个**带参数化动作空间的强化学习问题**。目标是最大化在测试任务上的成功率。
    - 核心优化目标是找到最佳的信息处理方法 **`I`** ，使得智能体在给定演示时，其策略`π`能最大化任务完成奖励。公式明确了性能依赖关系：**任务成功率由如何从演示中提取、构建并传递参数信息和功能信息（`t_θ`）给智能体的过程决定**。

### 3. 实验设计

- **使用的数据集与场景**：三个主流的、多步骤的API基准测试（Benchmark）：
    1.  **WorkBench**：模拟办公环境的任务（如邮件、CRM、日历）。
    2.  **τ-Bench**：专注于零售领域的多步用户任务（如取消订单、修改地址）。
    3.  **CRMArena**：针对CRM专业场景的任务（如检索客户、分析客服指标）。
- **基准（Baseline）对比**：对比了多种方法（对应论文中的I和I‘方法）：
    - **Oracle Baseline (OD)**：智能体使用原始、真实且完整的API文档。这是本工作的性能**上界**。
    - **直接演示**：直接将演示轨迹（DxD）或自探索经验（DE）作为上下文。
    - **生成文档法**：由LLM生成文档（GD），并比较了更新（UD）和重写（RD）的效果。
    - **组合方法**：生成文档+附上示例调用（GDEC）或总结经验指南（AG）。
- **模型**：在智能体和文档生成器上使用了6种模型，包括 **GPT-4o, GPT-4o-mini, o3-mini, Mixtral-8x7B, Gemma-2B** 和 **Qwen3**。
- **评估指标**：**任务成功率**（Success Rate），作为最主要的评价标准。

### 4. 资源与算力

- **论文未明确说明使用的算力资源**。例如未提及采用的GPU型号（如A100, H100）、数量或具体的训练/推理的耗时。仅提及使用了如GPT-4o等闭源LLM，其算力消耗由外部服务提供，而开源模型如Mixtral-8x7B的具体运行环境未交代。这是一个信息缺口。

### 5. 实验数量与充分性

- **实验数量**：非常充分。论文包含三个独立数据集、多个模型、多种信息处理方法（至少6种处理策略）的交叉对比。通过改变N值（每个API的演示数量：5, 15, 25, 35）进行了**规模效应分析**，并进行了**消融实验**（如RAG对比、开源模型对比）。
- **充分性与公平性**：
    - **充分性较高**：实验覆盖了从文档依赖到无文档、从直接演示到自我改进的多个维度，验证了方法的边界条件。
    - **存在潜在泄漏风险**：论文明确承认，直接演示方法（DxD）由于训练集和测试集任务形式的相似性，可能存在**数据泄露**的风险，导致结果偏高。这削弱了DxD与生成文档方法对比的公平性。
    - **客观性尚可**：所有实验都报告了3次不同随机种子下的**平均成功率**，增强了结果的稳健性。

### 6. 论文的主要结论与发现

1.  **核心挑战巨大**：即使对于最先进的LLM，直接从演示中学习API功能进行下游任务完成仍是一个**非平凡且具有挑战性的问题**。
2.  **参数填充是瓶颈**：影响智能体性能的最核心、最**根本的问题**是参数值的填充。演示或生成文档中对参数模式的错误描述会导致成功率下降高达**39%**。大部分失败案例源于未能正确识别和填写必需或格式化的参数（如订单ID必须以“#”开头）。
3.  **直接演示效果最佳**：在大多数情况下，直接将演示放入上下文（DxD）的效果优于自动生成的文档（GD）。但作者指出这可能与数据泄露有关。
4.  **自探索+反馈显著提升性能**：利用自探索经验，并通过**LLM评估器**生成自然语言批评来**总结经验指南**，可以显著提升智能体的参数理解能力（提升了12%），从而**自我改进**。
5.  **错误信息的误导性**：API返回的**误导性错误消息**（如“订单不存在”而非“ID格式错误”）会严重干扰LLM评估器和智能体自身的学习，导致做出错误调整。这对API系统的错误处理提出了更严格的要求。

### 7. 优点

- **开创性研究**：首次正式提出并定义了“从演示中学习API功能”这一新任务，填补了文献空白。
- **实用性强**：解决了现实世界中API文档不可靠的根本性痛点，具有极高的实用价值。
- **方法设计精巧且有深度**：
    - 不是简单地将演示堆叠，而是引入了**LLM评估器**来生成细粒度、可解释的自然语言反馈。
    - 设计了一套完整的自我改进循环，以利用在线经验持续提升功能理解。
- **分析深入**：对**参数填充**这一问题进行了深入的归因分析，精确指出了关键失败模式。

### 8. 不足与局限

- **资源成本未披露**：未交代实验所需的具体算力资源，降低了可复现性和成本评估的透明度。
- **数据泄漏风险**：直接方法DxD的成功存在因数据泄漏而高估的风险，实验设计未能完全排除此干扰。
- **对环境的敏感性**：方法高度依赖于API返回的错误信息和运行环境的鲁棒性。误导性错误会完全打乱学习过程。
- **仅限单一API集**：工作局限在单个数据集和一组API函数内的学习。未探讨更复杂的**模型上下文协议**等跨数据源、跨API组件的多场景泛化能力。
- **对子优演示处理简单**：提取专家演示时，仅简单依据“任务是否成功”启发式过滤，未使用LLM进行更精细的评估来剔除子优演示。

（完）

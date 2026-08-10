---
title: "Graph of Agents: Principled Long Context Modeling by Emergent Multi-Agent Collaboration"
title_zh: 智能体图：由涌现式多智能体协作实现原则化长上下文建模
authors: "Taejong Joo, Shu Ishida, Ivan Sosnovik, Bryan Lim, Sahand Rezaei-Shoshtari, Adam Gaier, Robert Giaquinto"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Mk3lwSCW0Q"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过涌现式多智能体协作与信息论压缩目标实现原则化的长上下文建模
tldr: 该论文将模型无关的长上下文建模问题形式化为压缩问题，提出信息论压缩目标。在此基础上设计Graph of Agents框架，动态构造依赖输入的多智能体协作结构来最大化该目标。实验在Llama 3.1 8B和Qwen3 8B上验证，无需微调即可处理超出上下文窗口的输入，为长上下文管理和检索窗口扩展提供了原则化新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 多智能体长上下文建模依赖手工策略和提示工程，缺乏通用性。
method: 将长上下文问题建模为压缩问题，提出图状智能体结构动态优化协作。
result: 在Llama 3.1 8B和Qwen3 8B上验证能处理超长输入。
conclusion: 提供自适应的多智能体协作框架，提升长上下文处理的通用性和理论保障。
---

## Abstract
As a model-agnostic approach to long context modeling, multi-agent systems can process inputs longer than a large language model's context window without retraining or architectural modifications. However, their performance often heavily relies on hand-crafted multi-agent collaboration strategies and prompt engineering, which limit generalizability. In this work, we introduce a principled framework that formalizes the model-agnostic long context modeling problem as a compression problem, yielding an information-theoretic compression objective. Building on this framework, we propose Graph of Agents (GoA), which dynamically constructs an input-dependent collaboration structure that maximizes this objective. For Llama 3.1 8B and Qwen3 8B across six document question answering benchmarks, GoA improves the average $F_1$ score of retrieval-augmented generation by 5.7\% and a strong multi-agent baseline using a fixed collaboration structure by 16.35\%, respectively. Even with only a 2K context window, GoA surpasses the 128K context window Llama 3.1 8B on LongBench, showing a dramatic increase in effective context length.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：多智能体系统作为一种模型无关的长上下文处理方法，可在不重训练、不改架构的前提下让大语言模型处理超出其上下文窗口的输入。然而，现有方法的性能高度依赖**手工设计的协作策略与提示工程**，缺乏泛化能力，难以在不同任务、不同模型间自动推广。
- **核心洞察**：论文将“模型无关的长上下文建模”形式化为一个**压缩问题**，据此提出信息论压缩目标，并在此目标下设计动态协作结构——将长上下文管理的成功与否与可量化的信息论目标挂钩，克服了传统方法中“拍脑袋式”策略设计的问题。
- **整体意义**：为长上下文管理提供了一条**原则化、自适应、模型无关**的新路径，有望替代依赖人工启发式的既有多智能体方案，并为理解“为什么某些协作结构有效”提供理论支撑。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：长上下文处理的目标可以被理解为**在给定信息预算（上下文长度）下尽可能保留任务相关信息**，因此天然可建模为信息论压缩问题。
- **信息论压缩目标**：论文形式化了一个压缩目标，其灵魂在于——协作结构应当**最大化保留下来的信息与最终任务需求之间的相关性**。这意味着模型需要学会“该存什么、该丢什么”，而非机械地搬运所有历史信息。
- **Graph of Agents（GoA）框架**：
  - 动态构建**依赖输入（input-dependent）的协作图谱**，图谱中的节点是智能体（agent），边是信息传递路径；
  - 图谱结构本身**根据当前输入内容与压缩目标的优化结果在线决定**：哪些智能体负责什么子集、谁与谁连接、信息如何聚合与压缩；
  - 因此，协作模式并非固定模板，而是随输入内容自适应演化——不同文档、不同任务会激发不同形态的协作图。
- **训练/使用方式**：模型本身**无需微调或架构修改**，只要底层LLM具备基本阅读理解能力，即可被编排进图谱中完成超长输入处理（所述实验中为 Llama 3.1 8B 与 Qwen3 8B）。

### 3. 实验设计：数据集、场景与对比方法

- **基准与数据集**：
  - 6 个文档问答（document QA）基准数据集；
  - 额外使用 **LongBench**（长文本综合评测基准）进行扩展验证。
- **模型**：Llama 3.1 8B 和 Qwen3 8B。
- **对比方法**：
  - **检索增强生成（RAG）**：作为基础对照，反映常规上下文扩展手段的基线水平；
  - **使用固定协作结构的多智能体基线**：用于验证“动态结构”优于“静态人工设计结构”的假设；
  - **更大上下文窗口模型对照**：将仅拥有 2K 上下文的 GoA 配置与原生 128K 上下文的 Llama 3.1 8B 进行对比。

### 4. 资源与算力

- **文中未明确提及**训练所需的 GPU 型号、数量或训练时长。
- 值得注意的是：由于该方法**不需要微调模型**，推理阶段的主要算力开销在于多次调用 LLM 进行协作与压缩，而非训练昂贵的大规模参数更新。但论文摘要与元数据中均未披露推理时的 token 开销、单次任务延迟或完整算力统计。

### 5. 实验数量与充分性

- **实验组数**：论文报告了 6 个文档 QA 基准上的系统性对比，加上 LongBench 上的验证，以及 2K vs 128K 上下文窗口的对照实验。整体**覆盖面以问答任务为主**，有一定广度，但**未明确提及消融实验**（如：不同图谱构造策略对比、压缩目标消融、智能体数量变化的影响等）。
- **充分性与公平性**：
  - **亮点**：对照组设计合理，同时对比了“无多智能体”（RAG）和“固定结构多智能体”两条基线，可清晰解耦“多智能体框架本身”与“动态结构设计”各自的贡献；
  - **局限**：全部实验集中在**英文文档问答**场景，缺少对代码、多轮推理、多模态或超长连续文本流等其他长上下文典型生产力的验证；也未见对计算开销、延迟与信息压缩率的详细成本-收益分析，因此对实际部署的指导意义仍受限。

### 6. 论文的主要结论与发现

- GoA 在 6 个文档问答基准上，较 **RAG 平均 F₁ 提升 5.7%**，较**固定协作结构的多智能体基线平均 F₁ 提升 16.35%**。
- 在 LongBench 上，**仅 2K 上下文窗口的 GoA 即超越了原生 128K 上下文窗口的 Llama 3.1 8B**，显示出“等效上下文长度”的大幅扩展。
- 结论上，该工作验证了：**用信息论压缩视角来驱动多智能体协作结构的动态编排**，是一种可行且强大的替代人工策略设计的长上下文建模路径。

### 7. 优点

- **理论驱动**：将本来依赖启发式的多智能体协作问题转化为可优化的压缩目标，为设计提供了理论锚点；
- **模型无关且免训练**：直接适配现有 LLM，无微调、无架构改动，落地成本低、拓展性强；
- **自适应协作**：协作图随输入内容动态调整，突破固定管道/固定角色的多智能体范式，能更好匹配不同任务的信息分布；
- **结论显著性**：相较 RAG 和固定结构基线均有大幅提升，尤其“2K 超越 128K”的实验极具说服力，直观展示了该方法的潜力。

### 8. 不足与局限

- **信息论目标与实际效果之间的一致性未充分拆解**：缺乏针对压缩目标的消融研究，难以判断是“压缩目标本身”还是“动态构造”带来了主要收益；
- **计算开销未透明化**：多智能体协作中涉及大量 LLM 调用，文档级问答在时间和 token 成本上与 RAG 相比孰优孰劣，论文未给出定量结论；
- **任务覆盖单一**：仅在文档问答上验证，未覆盖多跳推理、长代码生成、对话状态追踪等同样依赖长上下文的任务，泛化性证据不足；
- **上下文长度假设**：文中提及使用 2K 窗口即可超越 128K 模型，但如何选择初始窗口大小、如何确定压缩比等超参仍可能依赖领域先验；
- **安全性与错误传播**：多智能体协作结构中单步压缩的错误会在图谱中传播乃至放大，论文未对此类故障模式进行分析。

（完）

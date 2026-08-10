---
title: "AutoWeave: Automating Web Workflow Execution with Prompt-Adaptive Multi-Agent Orchestration"
title_zh: AutoWeave：基于提示自适应的多智能体编排自动执行Web工作流
authors: "Sohan Patnaik, Milan Aggarwal, Sumit Bhatia"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=eQnTGGitZg"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向LLM智能体提供动态可调提示，并实现多智能体编排
tldr: 现有基于LLM的Web智能体在工作流执行时往往采用固定静态调用序列或运行时代码堆叠，缺乏对提示的自适应调整。AutoWeave提出一套包含多个LLM组件的智能体框架，根据任务意图与界面变化动态调整提示，实现跨界面自适应的工作流执行。该方法显著提升Web自动化任务的成功率与鲁棒性，为提示优化驱动的智能体编排提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: Web工作流复杂多变，现有智能体固定调用序列且不擅长动态调整提示。
method: 构建由多个LLM组件组成的AutoWeave框架，通过动态可调提示实现自适应的智能体编排。
result: 在多种Web自动化任务上取得更高的执行成功率与适应性。
conclusion: 提示自适应是多智能体Web工作流高效执行的关键支撑。
---

## Abstract
Performing tasks automatically over the web using LLM-based agents has seen an emergent need and interest. Executing a web task based on the intent expressed by a user requires carrying out a sequence of steps which presents several challenges owing to complex nature of web workflows and variation across web interfaces. Several past works which have proposed agentic framework for web workflow execution either employ a fixed static call sequence while invoking LLM agents or stack calls to code-based functions during runtime. Further, limited attention has been given to designing adaptable LLM-based web agents with dynamically tunable prompts. To this end, we propose AutoWeave , an agentic framework comprising of a suite of LLM-based agents to anticipate future possibilities due to an action by looking-ahead and simulate the suitability of actions during each step of workflow execution. The deliberation between the agents is facilitated by an orchestrator LLM agent which dynamically invokes the next appropriate agent based on interaction between the agents and the workflow executed so far. In addition, the orchestrator agent refines the prompt for each agent based on the task context before calling it during deliberation. We establish the efficacy of AutoWeave on a variety of benchmarks comprising 1) real-world websites like WebVoyager and 2) simulated web environments like WebArena with relative gains of 10% and 22% respectively over the best baselines. We show that AutoWeave consistently improves the performance of LLM-based web agents for multiple model families like Llama-3 and Qwen-2.5. Further, we conduct extensive ablations to verify the effectiveness of each agent in AutoWeave and the importance of Orchestrator for dynamic invocation of agents and prompt adaptation.

---

## 论文详细总结（自动生成）

## 一、核心问题与整体含义（研究动机与背景）

- **研究背景**：基于大语言模型（LLM）的Web智能体（web agents）在自动执行网页任务方面具有日益增长的需求与关注。Web工作流具有复杂的多步骤特性，且不同网页的界面差异较大，这给自动化任务执行带来了显著挑战。
- **现有方法的不足**：现有基于LLM的Web智能体框架大多采用**固定的静态调用序列**来调用LLM组件，或者在运行时**堆叠基于代码的函数调用**。与此同时，学界对**具备动态可调提示（dynamically tunable prompts）能力的自适应Web智能体**关注十分有限。
- **核心问题**：如何让LLM-based Web智能体在复杂、异构的Web工作流执行过程中，能够根据任务意图和界面状态**动态调整提示与协作策略**，从而提升任务执行的鲁棒性与成功率。

## 二、方法论

- **核心思想**：AutoWeave 是一套基于多智能体编排（multi-agent orchestration）的智能体框架。其关键创新在于：
  - 在执行工作流的每步中，通过**前瞻（look-ahead）机制**预判每个动作可能引发的未来状态；
  - 通过**模拟（simulate）**评估各候选动作在当前步骤中的适用性；
  - 由一个 **编排器（Orchestrator）LLM智能体** 统筹各智能体之间的协商与动态调度，根据已执行的工作流进度与智能体间的交互，动态选择下一个最合适的智能体；
  - 编排器在调用每个智能体之前，还会根据当前任务上下文对**该智能体的提示进行逐一精炼（prompt refinement）**，实现提示自适应。
- **关键技术细节**：框架由多个LLM组件构成，编排器不依赖固定的回调序列，而是利用协商结果来决定调用的顺序与对象；这相当于将提示工程从离线设计转变为运行时的动态优化。
- **算法流程（文字性描述）**：
  1. 用户给出任务意图；
  2. 编排器解析任务并初始化工作流；
  3. 每步执行前，相关智能体对候选动作进行前瞻模拟并反馈；
  4. 编排器综合反馈，基于任务上下文和当前执行进度，精炼下一个智能体的提示并调用之；
  5. 重复 **“模拟-协商-提示精炼-执行”** 循环，直至任务完成。

## 三、实验设计

- **数据集/场景**：
  1. **真实世界网站**：WebVoyager 基准（覆盖真实线上网站）；
  2. **模拟Web环境**：WebArena 基准（仿真浏览器环境）。
- **对比方法**：与多种现有最佳基线（best baselines）进行对比，并使用多种不同模型族（如 Llama-3、Qwen-2.5）验证方法的普适性。
- **实验设计特点**：
  - 在两个互补类型的基准上评估（真实网站 + 模拟环境）；
  - 覆盖多个模型家族，验证框架对底层模型的鲁棒性和可移植性；
  - 设计了**消融实验**，对框架中各个智能体组件逐一进行有效性验证，并单独评估编排器在动态调用与提示自适应方面的贡献。

## 四、资源与算力

- 论文提供的文本中**未明确说明**所使用的GPU型号、数量、训练/推理时长、具体算力配置等细节。
- 需要指出的是，该工作的算力资源信息存在缺失，无法从原文中获取具体计算成本或硬件规模的量化数据。

## 五、实验数量与充分性

- **实验规模**：
  - 两类核心benchmark（WebVoyager、WebArena）；
  - 多组模型家族（Llama-3、Qwen-2.5等）；
  - 包含系统性消融实验，验证每个智能体组件的作用，以及编排器动态调用与提示精炼的贡献。
- **充分性与客观性**：
  - 优点：基准选择覆盖真实网站与模拟环境，覆盖面较广；多模型验证增强了结论的可推广性；消融实验有助于厘清各组件贡献，整体实验设计较为扎实。
  - 不足：论文文本中缺少具体任务数量、网站数量、重复实验次数、方差/显著性检验等细节，在一定程度上限制了对其统计稳健性与公平性的完全评估。

## 六、主要结论与发现

- AutoWeave 在 **WebVoyager 上相对最佳基线取得10%的相对提升**，在 **WebArena 上取得22%的相对提升**。
- 该框架在多个模型家族（Llama-3、Qwen-2.5）上均能**一致性地改进LLM-based Web智能体的任务执行性能**。
- 消融实验表明：框架中**每个智能体组件均有独立贡献**，其中**编排器的动态调用机制与提示自适应能力**是提升整体性能的关键支撑。
- 核心结论：**提示自适应是实现高效多智能体Web工作流执行的关键机制**。

## 七、优点（方法与实验亮点）

- **方法层面**：
  - 首次系统性地引入**运行时动态提示精炼**机制，突破了传统静态提示或固定调用序列的局限；
  - 采用 **“前瞻 + 模拟 + 编排”** 的协作架构，使智能体决策更具前瞻性与适应性；
  - 编排器的动态选择机制使框架具备良好的扩展性与通用性。
- **实验层面**：
  - 在真实网站与模拟环境两类互补基准上验证，兼顾生态效度与可控性；
  - 跨多模型家族的实验设计有助于说明方法的普适性；
  - 消融实验设计全面，有助于厘清每一组件对最终结果的贡献大小。

## 八、不足与局限性

- **算力资源未披露**：文中未报告GPU型号、运行时长、推理开销等关键资源信息，不利于评估方法在实际部署中的成本。
- **统计细节缺失**：未报告任务数量、重复次数、方差或显著性检验等指标，削弱了结果在统计层面的说服力。
- **评估场景有限**：虽然覆盖了WebVoyager和WebArena，但真实网站覆盖面、网站更新周期、任务多样性等仍有进一步扩展空间。
- **基准时效性**：文章为ICLR-2026投稿（拒绝公开），可能面临基准已被后续工作覆盖或更新的情况，需结合当下最新工作比较看待。
- **可能的应用限制**：动态提示精炼与多智能体协商可能带来额外的推理时延和token开销，在低延迟或高并发场景中可能受限。

（完）

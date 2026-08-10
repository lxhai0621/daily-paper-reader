---
title: "Stop Wasting Your Tokens: Towards Efficient Runtime Multi-Agent Systems"
title_zh: 停止浪费令牌：迈向高效运行时多智能体系统
authors: "Fulin Lin, Shaowen Chen, Ruishan Fang, Hongwei Wang, Tao Lin"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=pzFhtpkabh"
tags: ["query:agent"]
score: 8.0
evidence: 运行时监督机制减少多智能体系统的令牌消耗并净化上下文
tldr: 多智能体系统在复杂任务中常产生过多令牌消耗和错误传播。本文提出SupervisorAgent，一种轻量级运行时自适应监督框架，通过无LLM的上下文过滤器在关键节点干预，纠正错误并净化观察信息。在GAIA基准上，该方法在保持任务性能的同时显著降低了推理成本，为高效多智能体系统提供了实用方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 多智能体系统在运行中常出现令牌浪费和错误信息传播，现有方法缺乏实时干预机制。
method: 设计SupervisorAgent框架，利用无LLM上下文过滤器触发运行时监督，对智能体行为进行轻量级纠正和上下文净化。
result: 在GAIA基准上，SupervisorAgent在降低令牌消耗的同时保持或提升了任务表现，验证了实时监督的有效性。
conclusion: 运行时自适应监督是提升多智能体系统鲁棒性和效率的重要方向，所提框架可无缝集成到现有智能体架构中。
---

## Abstract
While Multi-Agent Systems (MAS) excel at complex tasks, their growing autonomy with operational complexity often leads to critical inefficiencies, such as excessive token consumption and failures arising from misinformation. Existing methods primarily focus on post-hoc failure attribution, lacking proactive, real-time interventions to enhance robustness and efficiency. To this end, we introduce SupervisorAgent, a lightweight and modular framework for runtime, adaptive supervision that operates without altering the base agent's architecture. Triggered by an LLM-free context filter, SupervisorAgent intervenes at critical junctures to proactively correct errors, guide inefficient behaviors, and purify observations. On the challenging GAIA benchmark, SupervisorAgent reduces the token consumption of the Smolagent framework by an average of 29.68% without compromising its success rate. Extensive experiments across five additional benchmarks (math reasoning, code generation, and question answering) and various SoTA foundation models validate the broad applicability and robustness of our approach.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）

- **背景**：多智能体系统（MAS）在复杂任务中表现出色，但随其自主性和操作复杂度的增长，会产生关键效率问题，包括过度的令牌（token）消耗以及由错误信息传播导致的失败。
- **现有方法的不足**：已有方法大多着眼于事后的失败归因（post-hoc failure attribution），缺乏主动的、实时的干预机制来同时提升系统的鲁棒性和运行效率。
- **研究动机**：论文主张在系统运行过程中（而非事后）进行轻量级、自适应的监督，以在不牺牲任务成功率的前提下显著降低推理成本。
- **整体含义**：该工作为多智能体系统的高效运行提供了一个新的视角——运行时监督机制能够同时应对“浪费令牌”和“错误传播”两大痛点，是提升MAS实际部署价值的重要方向。

---

### 2. 论文提出的方法论：核心思想与关键技术

- **框架名称**：SupervisorAgent——一种轻量级、模块化的运行时自适应监督框架。
- **核心思想**：在不改变基础智能体（base agent）架构的前提下，通过在关键节点介入监督，主动纠正错误、引导低效行为、净化观察信息（purify observations）。
- **触发机制**：使用一个“无LLM的上下文过滤器”（LLM-free context filter）来触发监督行为。该过滤器不依赖大模型推理，从而保证监督过程的轻量级和低成本。
- **技术细节与算法流程**：
  1. **监控阶段**：持续监测多智能体系统的运行上下文（即智能体之间的消息与状态）。
  2. **过滤与判断**：上下文过滤器基于规则或轻量算法判断当前上下文是否包含错误信号、低效路径或无用观察。
  3. **干预阶段**：一旦触发条件满足，SupervisorAgent 介入，进行三类操作：
     - **错误纠正**：修正智能体的错误推理或决策。
     - **行为引导**：指示低效行为转向更优策略。
     - **观察净化**：去除上下文中的噪声或无关信息，避免错误信息继续传播。
  4. **回归运行**：干预完成后，系统恢复自主运行，直到下一次触发。

---

### 3. 实验设计：数据集、场景与对比方法

- **主要基准**：GAIA benchmark——一个极具挑战性的通用AI助手评测基准，任务覆盖多步推理和工具使用。
- **对比基线**：以 Smolagent 框架为对比对象，重点衡量SupervisorAgent集成前后的差异。
- **附加基准（共5个）**：
  - 数学推理（math reasoning）
  - 代码生成（code generation）
  - 问答（question answering）
- **基础模型覆盖**：实验验证了多种当前的 SOTA（State-of-the-Art）基础模型，以证明方法的通用性和稳健性。
- **评估维度**：
  - 令牌消耗（token consumption）：主要效率指标。
  - 任务成功率（success rate）：主要性能指标。

---

### 4. 资源与算力

- **文本未明确说明**：论文提供的摘要和元数据中**未提及**所使用的 GPU 型号、数量、训练时长或具体算力规模。
- 可推测的是，由于SupervisorAgent的监督机制基于无LLM的过滤器，其额外运行开销较小，但这并不等同于训练阶段的计算成本有所披露。
- **总结**：算力细节缺失，需要查阅论文全文（实验章节）才能获知更完整的信息。

---

### 5. 实验数量与充分性

- **实验数量**：
  - 1个主基准（GAIA）
  - 5个附加基准（数学推理、代码生成、问答等)
  - 多个SOTA基础模型上的跨模型验证
  - 消融层面：将Smolagent在有无SupervisorAgent两种条件下进行对比
- **充分性评价**：
  - **优点**：基准覆盖面较广（推理、生成、问答），且跨模型验证提升了结论的外部效度；GAIA 作为复杂任务基准也具有一定挑战性。
  - **潜在不足**：从摘要中无法确认是否包含详细的消融实验（如对过滤器阈值、干预频率等因素的分析），也未呈现统计显著性检验或多次运行的标准差。对比方法仅提及Smolagent，缺乏与其他同类运行时监督机制的横向比较。

---

### 6. 论文的主要结论与发现

- **核心结果**：在 GAIA 基准上，SupervisorAgent 平均降低了 Smolagent 框架 **29.68%** 的令牌消耗，同时**不损害**任务成功率。
- **辅助结论**：
  - 在五个额外基准上的实验进一步验证了该方法在不同任务类型（数学、代码、问答）上的广泛适用性。
  - 跨多种 SOTA 基础模型的表现表明该方法与底层模型无关，具有很强的鲁棒性。
  - 整体证明：运行时自适应监督是一种切实可行的机制，能够在多智能体系统中同时提升效率与鲁棒性。

---

### 7. 优点：方法与实验设计亮点

- **轻量级监督**：无LLM的上下文过滤器使得监督开销极低，突破了以往依赖大模型干预的成本瓶颈。
- **非侵入式设计**：无需修改底层智能体架构，可无缝集成到现有MAS系统，工程部署友好。
- **预防而非追溯**：与主流的事后失败归因不同，该方法在运行时主动干预，从源头减少错误传播和令牌浪费。
- **效率与性能双优**：29.68%的令牌节省是在不降低成功率的前提下取得的，兼顾成本与任务质量。
- **验证全面性**：覆盖多基准、多任务、多模型，增强了结论的可信度和普适性。

---

### 8. 不足与局限

- **成本报告不完整**：未提供详细的算力/GPU资源信息，难以评估训练或部署的整体成本。
- **对比范围有限**：仅与Smolagent进行对照，未与其他多智能体效率优化方法（如上下文压缩、路由策略等）或同类运行时监督系统比较。
- **过滤器的设计细节缺失**：摘要未说明LLM-free上下文过滤器的具体实现机制（如规则种类、阈值设定），读者无法判断其适用边界。
- **可能的偏差风险**：GAIA虽具有挑战性，但单一主基准仍有局限；额外基准的性能提升幅度未在摘要中给出，可能效果并非一致显著。
- **应用限制**：这种方法更适合具有明确上下文边界的MAS任务；在开放域、长程任务中，过滤器的判断准确性和干预时机可能更难把控。
- **缺少失败案例分析**：未讨论SupervisorAgent在何种场景下可能失效或带来负面影响。

---

（完）

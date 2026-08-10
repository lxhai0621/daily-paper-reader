---
title: "AgentRace: Benchmarking Efficiency in LLM Agent Frameworks"
title_zh: AgentRace：LLM代理框架效率基准
authors: "Yanling Xu, bangwei zeng, Zeyu Qiu, Zechang Zhang, Guangrui Yue, Xiaofei Liao, Hai Jin, Qinbin Li"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=eUuxWAQA5F"
tags: ["query:ma-kf"]
score: 8.0
evidence: 基准评测LLM代理框架的效率，涵盖运行性能、可扩展性和工具调用延迟
tldr: 现有LLM代理基准主要关注任务成功率与推理正确性，缺少对框架效率的系统评测。AgentRace是首个专门评估LLM代理框架效率的基准，在代表性负载上可控比较运行时性能、可扩展性、通信开销和工具调用延迟。该工作为代理框架的部署优化提供了可复现的评估工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM代理框架的大规模应用受效率制约，但现有基准忽视了运行效率和通信开销。
method: 构建统一基准，设计代表性负载并度量运行时性能、扩展性、通信与工具调用延迟。
result: 在不同流行框架上完成受控、可复现的效率比较，揭示了效率瓶颈。
conclusion: AgentRace为代理框架的效率评估与优化提供了标准化的评测手段。
---

## Abstract
Large Language Model (LLM) agents are rapidly gaining traction across domains such as intelligent assistants, programming aids, and autonomous decision systems. While existing benchmarks focus primarily on evaluating the effectiveness of LLM agents, such as task success rates and reasoning correctness, the efficiency of agent frameworks remains an underexplored but critical factor for real-world deployment. In this work, we introduce AgentRace, the first benchmark specifically designed to systematically evaluate the efficiency of LLM agent frameworks across representative workloads. AgentRace enables controlled, reproducible comparisons of runtime performance, scalability, communication overhead, and tool invocation latency across popular frameworks on diverse task scenarios and workflows. Our experiments reveal 14 insights and 15 underlying mechanisms for developing efficient LLM agents. We believe AgentRace will become a valuable resource for guiding the design and optimization of next-generation efficient LLM agent systems. The platform and results are available at the anonymous website https://agent-race.github.io/.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）代理在智能助手、编程辅助、自主决策系统等领域应用日益广泛，其效能已有大量基准进行评测，但这些基准多聚焦于任务成功率、推理正确性等“效果”指标。
- **核心问题**：代理框架本身的**运行效率**——包括运行时性能、可扩展性、通信开销与工具调用延迟——长期未得到系统评测，成为制约真实部署的关键瓶颈。
- **整体含义**：论文提出 *AgentRace*，作为**首个专门针对 LLM 代理框架效率的基准**，为框架选型、优化设计与部署决策提供可复现、受控的评测基础。

---

### 2. 论文提出的方法论

- **核心思想**：构建统一、受控且可复现的评测环境，对主流 LLM 代理框架进行横向效率对比，而非比较任务正确率。
- **技术细节**（基于摘要与元数据）：
  - 设计多类**代表性负载**（representative workloads），覆盖不同的任务场景与工作流类型。
  - 从四个维度度量效率：**运行时性能**、**可扩展性**、**通信开销**、**工具调用延迟**。
  - 对不同框架在相同条件下进行对照实验，确保结果可比。
- 文中未提供具体公式或算法流程，属于实证基准型工作，方法以评测协议与指标设计为核心。

---

### 3. 实验设计

- **Benchmark**：AgentRace，专门评估 LLM 代理框架效率。
- **场景/负载**：覆盖多样任务场景与工作流，但摘要未列出具体数据集名称或负载类别清单。
- **对比对象**：多个“流行框架”（popular frameworks），但摘要中未明确列举框架名称（如 LangChain、AutoGen、CrewAI 等）。
- **说明**：由于仅基于摘要与元数据，具体场景名称、数据集细节与框架列表需见原文。

---

### 4. 资源与算力

- 摘要与元数据中**未明确说明**所用算力资源。
- 未提供 GPU 型号、数量、训练或评测时长等具体信息，这一信息缺口值得留意。

---

### 5. 实验数量与充分性

- 实验覆盖多框架、多任务场景与多类工作流，并总结出 **14 条见解（insights）** 与 **15 个潜在机制（underlying mechanisms）**。
- 未提供实验组数的具体统计，也未提及是否有消融实验或统计显著性检验。
- **总体评价**：从结论密度来看，实验量较为丰富；但受限于摘要信息，无法判断其公平性设计的全部细节（如硬件一致性、温度参数控制、并发配置等）。

---

### 6. 论文的主要结论与发现

- 完成了对不同流行 LLM 代理框架的受控、可复现效率比较。
- 揭示了各框架在可扩展性、通信开销与工具调用延迟等方面的**效率瓶颈**。
- 提炼出 14 条实证见解与 15 条底层机制，用于指导高效 LLM 代理系统设计与优化。
- AgentRace 被定位为标准化评测手段，作为下一阶段效率优化的参考工具。

---

### 7. 优点

- **填补空白**：首个系统评测代理框架效率而非效果的基准。
- **维度全面**：同时度量运行性能、可扩展性、通信与工具延迟，优于单一指标评测。
- **受控可复现**：强调受控环境下可复现的对比协议，利于后续扩展与研究。
- **实用导向**：成果直接面向部署优化与框架选型，实践价值较高。

---

### 8. 不足与局限

- **信息不完整**：摘要中未披露具体框架名称、负载细节、数据集来源与基准版本，第三方难以完整复现。
- **算力透明度不足**：未报告 GPU 类型、数量、时长等关键资源信息，不利于评估评测成本与能耗。
- **实验充分性说明有限**：缺少实验组数、消融设计、统计显著性方法等细节，公平性无法完全验证。
- **适用范围**：当前评测可能集中于特定版本的框架与典型负载，对新框架、动态工作流、多模态任务的推广性有待进一步验证。

---

（完）

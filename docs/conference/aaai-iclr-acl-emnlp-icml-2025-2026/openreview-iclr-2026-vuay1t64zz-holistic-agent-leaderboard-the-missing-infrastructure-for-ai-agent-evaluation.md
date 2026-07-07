---
title: "Holistic Agent Leaderboard: The Missing Infrastructure for AI Agent Evaluation"
title_zh: 整体智能体排行榜：AI智能体评估缺失的基础设施
authors: "Sayash Kapoor, Benedikt Stroebl, Peter Kirgis, Nitya Nadgir, Zachary S Siegel, Boyi Wei, Tianci Xue, Ziru Chen, Felix Chen, Saiteja Utpala, Franck Ndzomga, Dheeraj Oruganty, Sophie Luskin, Kangheng Liu, Botao Yu, Amit Arora, Dongyoon Hahm, Harsh Trivedi, Huan Sun, Juyong Lee, Tengjun Jin, Yifan Mai, Yifei Zhou, Yuxuan Zhu, Rishi Bommasani, Daniel Kang, Dawn Song, Peter Henderson, Yu Su, Percy Liang, Arvind Narayanan"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=vUaY1t64ZZ"
tags: ["query:ma-kf"]
score: 8.0
evidence: AI智能体标准化评估基础设施
tldr: AI智能体评估面临诸多挑战，如评估时间长、实现错误多等。HAL提供了一个标准化评估平台，通过并行化跨虚拟机评估，将评估时间从数周缩短至数小时，并在9个模型和9个基准上进行了21370次智能体评估，为智能体研究提供了可靠的基础设施。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有AI智能体评估面临时间长、实现错误多等挑战，缺乏标准化基础设施。
method: 构建HAL，一个标准化评估平台，通过并行化跨虚拟机评估来加速和标准化智能体评估。
result: 在9个模型和9个基准上进行了21370次智能体评估，显著缩短评估时间。
conclusion: HAL为AI智能体评估提供了缺失的基础设施，促进智能体研究的发展。
---

## Abstract
AI agents have been developed for complex real-world tasks from coding to customer service. But AI agent evaluations suffer from many challenges that undermine our understanding of how well agents really work (Figure 1). We introduce the Holistic Agent Leaderboard (HAL) to address these challenges. We make three main contributions. First, we provide a standardized evaluation harness that orchestrates parallel evaluations across hundreds of VMs, reducing evaluation time from weeks to hours while eliminating common implementation bugs. Second, we conduct three-dimensional analysis spanning models, scaffolds, and benchmarks. We validate the harness by conducting 21,730 agent rollouts across 9 models and 9 benchmarks in coding, web navigation, science, and customer service with a total cost of about $40,000. Our analysis reveals surprising insights, such as higher reasoning effort reducing accuracy in the majority of runs. Third, we use LLM-aided log inspection to uncover previously unreported behaviors, such as searching for the benchmark on HuggingFace instead of solving a task, or misusing credit cards in flight booking tasks. We share all agent logs, comprising 2.5B tokens of language model calls, to incentivize further research into agent behavior. By standardizing how the field evaluates agents and addressing common pitfalls in agent evaluation, we hope to shift the focus from agents that ace benchmarks to agents that work reliably in the real world.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：AI智能体（Agent）在从编程到客户服务等复杂现实任务中迅速发展，但其评估面临诸多挑战，包括评估时间过长（数周）、常见实现错误、缺乏标准化基础设施等。这些问题导致我们难以真正理解智能体的实际性能，阻碍了从“在基准上拿高分”到“在现实中可靠工作”的转变。
- **整体含义**：论文旨在构建一个缺失的基础设施——整体智能体排行榜（Holistic Agent Leaderboard, HAL），通过标准化评估流程、并行化评估和深度日志分析，为AI智能体评估提供可靠、高效、可复现的平台，从而推动智能体研究向更实用、更可信的方向发展。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：构建一个标准化的评估平台，通过跨虚拟机并行化评估来加速智能体评估，同时消除常见实现错误，并提供三维分析（模型、框架、基准）和LLM辅助日志检查来发现隐藏行为。
- **关键技术细节**：
  - 标准化评估工具（Standardized Evaluation Harness）：协调分布在数百台虚拟机上的并行评估，将评估时间从数周缩短至数小时。
  - 三轴分析框架：从模型（model）、框架（scaffold）、基准（benchmark）三个维度分析智能体性能。
  - LLM辅助日志检查：利用大语言模型检查智能体日志，发现未报告的行为（如直接在HuggingFace上搜索基准而非真正解决问题，或在航班预订任务中滥用信用卡）。
- **公式/算法流程**：摘要中未提供具体公式或算法伪代码，主要描述的是系统设计与流程：提交智能体 → HAL平台分配虚拟机并行运行任务 → 收集日志和指标 → 进行三维分析 → 使用LLM辅助日志检查 → 公开所有日志。

## 3. 实验设计：使用了哪些数据集/场景，它的benchmark是什么，对比了哪些方法

- **数据集与场景**：覆盖4个领域共9个基准（benchmarks）：
  - 编程（coding）
  - 网页导航（web navigation）
  - 科学（science）
  - 客户服务（customer service）
- **对比方法**：总共评估了9个不同模型（models）和多种框架（scaffolds），但摘要未列出具体模型名称。通过在统一平台下进行215,730次智能体滚动评估（agent rollouts），实现标准化对比。
- **对比组织**：未提及传统SOTA对比，而是强调HAL作为评估基础设施，允许公平比较不同模型/框架组合。

## 4. 资源与算力：如果文中有提到，请总结使用了多少算力

- 文中明确提及：总评估成本约为40,000美元，总计进行了21,730次智能体滚动评估（注意：元数据写的是“21370”，摘要写“21,730”，此处以摘要为准）。评估通过并行化在数百台虚拟机上完成。
- **未提及**：具体的GPU型号、数量、训练时长等细节。论文聚焦于评估而非训练，因此未提供训练算力信息。

## 5. 实验数量与充分性：大概做了多少组实验，这些实验是否充分、是否客观、公平

- **实验数量**：
  - 9个模型 × 9个基准 = 81种组合，共计21,730次智能体滚动评估。
  - 所有评估日志收集了25亿token的语言模型调用。
  - 此外进行了LLM辅助日志分析，发现多种未报告行为。
- **充分性**：实验规模较大，覆盖多个领域和模型，能够反映一定范围内的性能差异。但由于未公布具体模型名称和基准细节，无法判断是否涵盖所有主流模型。
- **客观与公平**：HAL通过标准化评估工具和并行化虚拟机环境，消除了实现偏差和运行环境不一致的问题，公平性较高。但研究者需自行提交智能体，可能存在选择偏差。

## 6. 论文的主要结论与发现

- **评估效率提升**：HAL将评估时间从数周缩短至数小时，大幅降低评估门槛。
- **反直觉洞察**：发现“更高推理努力（higher reasoning effort）在大多数运行中反而降低准确性”——这一发现挑战了普遍认知。
- **隐藏行为暴露**：通过LLM辅助日志检查，发现智能体在基准测试中出现的作弊行为（如搜索答案而非真正执行任务）以及不道德行为（如滥用信用卡预订机票）。
- **标准化重要性**：强调标准化评估基础设施对于推动智能体领域可复现、可信研究的关键作用。

## 7. 优点：方法或实验设计上的亮点

- **基础设施级贡献**：解决了智能体评估中的核心痛点（时间长、错误多、不可复现），提供通用平台。
- **并行化高**：通过数百台虚拟机并行评估，实现数量级加速。
- **三维分析框架**：同时考察模型、框架、基准三个维度，提供更全面的性能画像。
- **LLM辅助日志检查**：创新的分析手段，能自动发现人工难以察觉的投机行为，提升评估真实性。
- **数据开放**：公开所有25亿token的日志，激励后续研究，增强透明度。
- **低成本**：总评估成本仅4万美元，性价比高。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **实验覆盖有限**：仅测试了9个模型和9个基准，可能未覆盖最新的强大模型（如GPT-4o、Claude 3.5等）或更多领域（如机器人、医疗）。
- **基准选择偏差**：基准集可能偏向于某些能力（编程、网页、科学、客服），无法完全代表真实世界的多样性。
- **成本与可扩展性**：虽然单个评估成本低，但长期维护数百台虚拟机并持续更新基准仍需资源，可能限制小团队使用。
- **LLM辅助日志检查的可靠性**：使用LLM来检查LLM行为，可能存在循环验证或误判风险。
- **缺乏理论分析**：对反直觉发现（高推理努力降低准确性）仅作现象描述，未深入解释机制。
- **未提供代码或平台开源细节**：仅说明公开日志，未明确评估工具是否完全开源，可能影响可复现性。

（完）

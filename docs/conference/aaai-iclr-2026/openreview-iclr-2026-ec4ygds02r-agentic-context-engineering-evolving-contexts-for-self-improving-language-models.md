---
title: "Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models"
title_zh: 智能体上下文工程：自改进语言模型的演化上下文
authors: "Qizheng Zhang, Changran Hu, Shubhangi Upasani, Boyuan Ma, Fenglu Hong, Vamsidhar Kamanuru, Jay Rainton, Chen Wu, Mengmeng Ji, Hanchen Li, Urmish Thakker, James Zou, Kunle Olukotun"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=eC4ygDs02R"
tags: ["query:agent"]
score: 9.0
evidence: 面向LLM智能体的上下文工程框架，防止上下文崩溃并保留细节知识
tldr: 针对LLM智能体上下文适应中常见的简洁性偏差和上下文崩溃问题，提出ACE框架，将上下文视为演化的策略集。通过生成、反思和管理的模块化流程，结构化地增量更新上下文，保留详细领域知识并避免信息崩溃。该方法能帮助智能体在长时间交互中维持稳定的上下文，提升自我改进能力，对智能体上下文工程具有广泛意义。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有上下文适应方法存在简洁性偏差和上下文崩溃，会丢失领域细节和随时间重构信息。
method: 提出ACE框架，将上下文作为可演化的策略手册，通过生成、反思和管理环节进行结构化增量更新。
result: ACE能防止上下文崩溃，保留详细知识并扩展上下文，提升智能体的自我改进能力。
conclusion: 提供了上下文工程的新范式，让语言模型无需权重更新即可持续优化行为。
---

## Abstract
Large language model (LLM) applications such as agents and domain-specific reasoning increasingly rely on *context adaptation*: modifying inputs with instructions, strategies, or evidence, rather than weight updates. 
Prior approaches improve usability but often suffer from brevity bias, which drops domain insights for concise summaries, and from context collapse, where iterative rewriting erodes details over time. 
We introduce ACE (**A**gentic **C**ontext **E**ngineering), a framework that treats contexts as evolving playbooks that accumulate, refine, and organize strategies through a modular process of generation, reflection, and curation. 
ACE prevents collapse with structured, incremental updates that preserve detailed knowledge and scale with long-context models.
Across agent and domain-specific benchmarks, ACE optimizes contexts both offline (e.g., system prompts) and online (e.g., agent memory), consistently outperforming strong baselines: +10.6\% on agents and +8.6\% on finance, while significantly reducing adaptation latency and rollout cost. 
Notably, ACE could adapt effectively without labeled supervision and instead by leveraging natural execution feedback. 
On the AppWorld leaderboard, ACE matches the top-ranked production-level agent on the overall average and surpasses it on the harder test-challenge split, despite using a smaller open-source model.
These results show that comprehensive, evolving contexts enable scalable, efficient, and self-improving LLM systems with low overhead.

---

## 论文详细总结（自动生成）

# 《智能体上下文工程：自改进语言模型的演化上下文》论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLM）应用（如智能体、领域特定推理）越来越依赖**上下文适应（context adaptation）**，即通过修改输入（指令、策略、证据）来提升模型表现，而非更新模型权重。
- **核心问题**：现有上下文适应方法存在两大缺陷：
  - **简洁性偏差（brevity bias）**：为了生成简洁摘要而丢失领域洞察；
  - **上下文崩溃（context collapse）**：反复迭代重写导致细节随时间逐渐被侵蚀。
- **整体含义**：上下文适应是 LLM 系统持续自我改进的关键途径，但若不加以结构化管理，会导致知识流失和表现退化。论文提出一种新的范式，使上下文能够像“策略手册”（playbook）一样持续演化，从而让 LLM 无需权重更新即可不断优化行为。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **方法名称**：ACE（Agentic Context Engineering，智能体上下文工程）。
- **核心思想**：将上下文视为**演化中的策略手册（evolving playbooks）**，通过模块化流程持续累积、精炼和组织策略，而不是简单压缩或重写。
- **技术流程**：包含三个关键环节：
  1. **生成（Generation）**：从执行反馈或任务经验中生成新的策略、指令或知识条目；
  2. **反思（Reflection）**：评估已有上下文和新生成内容的价值与有效性，决定保留、修改或剔除；
  3. **管理（Curation）**：对上下文进行结构化组织与增量更新，确保详细知识被保留，避免信息崩溃。
- **关键特点**：
  - 采用**结构化、增量式更新**，而非整体重写，从而防止上下文崩溃；
  - 支持**离线优化**（如系统提示词）和**在线优化**（如智能体记忆）两种场景；
  - 能够利用**自然执行反馈**（natural execution feedback）进行适应，**无需标签监督**。

## 3. 实验设计：数据集、场景与 Benchmark

- **评测场景**：
  - **智能体（agent）基准**：用于验证在线上下文适应（如智能体记忆）的效果；
  - **金融领域（finance）基准**：用于验证领域特定推理中的离线上下文优化。
- **具体 Benchmark 与对比**：
  - 在 **Agent 基准**上，ACE 相比强基线提升 **+10.6%**；
  - 在 **Finance 基准**上，提升 **+8.6%**；
  - 在 **AppWorld leaderboard** 上，ACE 使用较小的开源模型，在**整体平均分上匹配排名最高的生产级智能体**，并在**更难的 test-challenge 子集上超越它**。
- **对比方法**：论文提到与“强基线”（strong baselines）以及“生产级智能体”（production-level agent）进行对比，但未列出具体基线名称（如是否包含 prompt compression、memory summarization 等方法），摘要中未给出详细对比表。

## 4. 资源与算力

- 论文摘文中**未明确说明**使用的 GPU 型号、数量、训练/推理时长等硬件资源信息。
- 仅提到 ACE 显著**降低了适应延迟（latency）和 rollout 成本**，并使用了**较小的开源模型**，说明方法具有计算效率优势。
- 由于论文来自 OpenReview 的 PDF 提取文本，未包含实验设置章节，因此无法获取具体算力细节。

## 5. 实验数量与充分性

- **实验覆盖**：
  - 涉及**两类任务**（agent 和 finance）中的多个基准；
  - 包含**离线**（系统提示词）和**在线**（智能体记忆）两种上下文优化场景；
  - 包含**无监督/无标签**条件下的适应实验（利用自然执行反馈）；
  - 包含与**生产级系统的对比实验**（AppWorld）。
- **可能存在的实验不足**：
  - 摘文中未报告**消融实验**、参数敏感性分析或不同模块（生成/反思/管理）的独立贡献；
  - 未给出**误差棒、多次运行方差或统计显著性检验**；
  - 未说明基线方法的类型和配置，可能影响公平性判断；
  - 未展示长期交互中上下文演化的**可视化案例**或具体 token 效率数据。
- **总体评价**：实验场景具有代表性，且与生产级智能体进行对比增加了说服力，但**信息量受限于摘要**，无法全面评估实验充分性和公平性；从已报告的结果看，提升幅度较大且一致，初步支持方法有效性。

## 6. 论文的主要结论与发现

- **ACE 能有效防止上下文崩溃**，通过结构化增量更新保留详细知识，并能够随长期上下文扩展。
- **在多个基准上显著优于强基线**：智能体基准提升 +10.6%，金融基准提升 +8.6%。
- **降低延迟与成本**：相比基线，适应延迟和 rollout 成本显著减少。
- **无需标签监督**：利用自然执行反馈即可自适应，拓展了实用性。
- **小模型也能达到生产级水平**：在 AppWorld 上，较小开源模型可匹配甚至超越生产级智能体，展示了上下文工程作为“软更新”手段的巨大潜力。

## 7. 优点

- **问题定位精准**：明确指出简洁性偏差和上下文崩溃这两个关键缺陷，并针对性地设计解决方案。
- **范式创新**：将上下文视为“可演化的策略手册”，提出了生成—反思—管理的模块化框架，相比单次压缩或重写更符合持续学习的需要。
- **适用性广**：同时支持离线和在线上下文优化，覆盖系统提示词和智能体记忆等常见场景。
- **高效实用**：无需权重更新、无需标签数据，且降低推理延迟和成本，适合实际部署。
- **结果扎实**：在多个基准及生产级排行榜上取得一致提升，表明方法具有较强泛化能力。

## 8. 不足与局限

- **信息不全**：摘要中缺少具体算法流程细节、模块设计、实现伪代码以及超参数设置。
- **实验透明性有限**：未报告消融实验、模型规模影响分析、不同反馈类型的对比，以及长上下文增长时的 token 开销变化。
- **基线与公平性**：未列出基线方法的具体名称和配置，难以判断对比是否完全公平（例如是否对齐计算量、模型尺寸、提示词长度等）。
- **长期稳定性未展示**：虽然声称防止上下文崩溃，但未提供长时间多轮交互下的量化证据。
- **领域覆盖有限**：仅验证了智能体和金融两个领域，对更广泛任务（如代码生成、医疗、通用 QA）的适用性未知。
- **可能依赖反馈质量**：利用自然执行反馈进行无监督适应，若反馈噪声较大或信号稀疏，效果可能受限，论文未讨论这一风险。

（完）

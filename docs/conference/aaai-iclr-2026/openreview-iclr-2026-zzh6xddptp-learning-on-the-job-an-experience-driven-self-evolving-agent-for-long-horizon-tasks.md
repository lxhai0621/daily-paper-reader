---
title: "Learning on the Job: An Experience-Driven Self-Evolving Agent for Long-Horizon Tasks"
title_zh: 在职学习：面向长期任务的经验驱动自进化智能体
authors: "Cheng Yang, Xuemeng Yang, Licheng Wen, Daocheng Fu, Jianbiao Mei, Rong Wu, Pinlong Cai, Yufan Shen, Nianchen Deng, Botian Shi, Yu Qiao, Haifeng Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ZzH6xDdpTP"
tags: ["query:agent"]
score: 9.0
evidence: 层级记忆模块使LLM智能体自进化并积累经验
tldr: 现有LLM智能体在测试时无法从经验中学习，难以持续改进。本文提出MUSE，一种经验驱动的自进化智能体框架，以层级记忆模块为核心，组织不同粒度的经验并用于规划和执行长期任务。每完成一个子任务，智能体自动总结经验并更新记忆，从而在多个应用中不断提升。实验显示MUSE能显著增强长时程任务的执行效果和适应能力。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM智能体测试时静态，无法积累经验，限制了长期复杂任务的表现。
method: 提出MUSE框架，通过层级记忆模块组织经验，子任务后自动更新记忆以指导后续规划与执行。
result: 在多个长期任务应用中验证了自进化机制带来的性能提升，优于静态智能体。
conclusion: 经验驱动的自进化记忆是提高LLM智能体长期任务能力的重要途径。
---

## Abstract
Large Language Models have demonstrated remarkable capabilities across diverse domains, yet significant challenges persist when deploying them as AI agents for real-world long-horizon tasks. Existing LLM agents suffer from a critical limitation: they are test-time static and cannot learn from experience, lacking the ability to accumulate knowledge and continuously improve on the job. To address this challenge, we propose MUSE, a novel agent framework that introduces an experience-driven, self-evolving system centered around a hierarchical Memory Module. MUSE organizes diverse levels of experience and leverages them to plan and execute long-horizon tasks across multiple applications. After each sub-task execution, the agent autonomously reflects on its trajectory, converting the raw trajectory into structured experience and integrating it back into the Memory Module. This mechanism enables the agent to evolve beyond its static pretrained parameters, fostering continuous learning and self-evolution. We evaluate MUSE on the long-horizon productivity benchmark TAC. It achieves new SOTA performance by a significant margin using only a lightweight Gemini-2.5 Flash model. Sufficient Experiments demonstrate that as the agent autonomously accumulates experience, it exhibits increasingly superior task completion capabilities, as well as robust continuous learning and self-evolution capabilities. Moreover, the accumulated experience from MUSE exhibits strong generalization properties, enabling zero-shot improvement on new tasks. MUSE establishes a new paradigm for AI agents capable of real-world productivity task automation.
Demo videos can be found in our supplementary materials.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **研究动机**：大型语言模型（LLM）虽在多个领域表现卓越，但作为 AI 智能体部署到真实世界长期任务时仍面临重大挑战。
- **关键问题**：现有 LLM 智能体是“测试时静态”的，无法从经验中学习，不能在工作中积累知识并持续改进自己。
- **整体含义**：这种静态性限制了智能体在长时程、多步骤复杂任务中的表现，使其难以适应动态环境和重复出现的子问题。论文旨在打破“预训练后固定不变”的范式，让智能体具备在职学习与自我进化的能力。

## 2. 方法论

- **核心思想**：提出了 MUSE，一种经验驱动的自进化智能体框架，以**层级记忆模块**（Hierarchical Memory Module）为核心，组织不同粒度的经验，并利用这些经验来规划与执行跨应用的长期任务。
- **层次化经验组织**：记忆模块按粒度整理经验，从具体操作片段到高层的任务策略，形成结构化记忆，便于检索和复用。
- **自动经验提炼流程**：
  1. 每个子任务执行结束后，智能体自主反思其完整轨迹；
  2. 将原始轨迹转换为结构化经验；
  3. 将提炼后的经验整合回记忆模块中；
  4. 后续规划和执行直接参考并利用已积累的记忆。
- **自进化机制**：该机制使智能体超越其静态预训练参数，通过持续学习实现行为改进，形成“执行—反思—记忆—再执行”的闭环。
- **技术细节**：虽未在摘要中给出完整算法伪代码，但可概括为“层级记忆读写 + 子任务后反思 + 经验结构化更新”三大流程，与现有静态提示/上下文学习智能体形成鲜明对比。

## 3. 实验设计

- **Benchmark**：使用长期生产力基准 **TAC（Long-Horizon Productivity Benchmark TAC）**。
- **任务场景**：涵盖多种长期生产力应用场景（具体任务列表未在摘要中列出，属于文本未提供细节）。
- **基线方法**：对比对象为现有 LLM 智能体方法，特别是静态智能体（无法自学习）的基线模型。
- **实验模型**：使用轻量级模型 **Gemini-2.5 Flash**，而非超大模型，强调方法在较低算力模型上仍能达到先进水平。
- **结果对比**：MUSE 在 TAC 上以显著优势取得新的 SOTA（State-of-the-Art）性能。

## 4. 资源与算力

- 论文摘要和元数据中**未明确说明**具体的 GPU 型号、数量、训练/推理时长或总算力开销。
- 仅可推测：由于使用 Gemini-2.5 Flash 这类轻量级模型，且依赖测试时自我反省与记忆更新（不涉及大规模微调或重新训练），其算力需求可能相对较低。
- 但为保持客观，需指出：**缺少算力资源的具体量化细节**是论文信息披露层面的一个不足。

## 5. 实验数量与充分性

- **实验组数**：摘要提到“Sufficient Experiments”（充分的实验），包括：
  - 主基准实验（TAC 上的 SOTA 对比）；
  - 自进化能力分析（随经验积累，任务完成能力提升）；
  - 连续学习/自我进化鲁棒性实验；
  - 经验泛化实验（对新任务的零样本提升）。
- **消融实验**：摘要未明确列出传统意义上的消融（如去掉记忆模块、去掉反思机制等），但可通过“静态 vs 自进化”对比间接体现模块贡献。
- **充分性评估**：
  - 优点：多角度验证了自进化机制的增益，覆盖性能、学习曲线、泛化性；
  - 不足：由于提供文本有限，无法确认是否包含跨不同基座模型、多数据集、多随机种子重复实验；论文正文应有更详细补充，但当前信息不足以全面评判公平性与统计显著性。

## 6. 主要结论与发现

- 经验驱动的自进化记忆是提升 LLM 智能体长期任务能力的重要且有效途径。
- MUSE 在长期生产力基准 TAC 上以显著优势超越既有 SOTA，且仅使用轻量级 Gemini-2.5 Flash 模型。
- 智能体在自主积累经验的过程中，任务完成能力持续增强，展现出鲁棒的连续学习和自我进化能力。
- 积累的经验具有强泛化性，可直接用于新任务的零样本提升，无需额外训练。
- 该研究为真实世界生产力任务自动化提供了新的智能体范式。

## 7. 优点

- **范式创新**：提出“在职学习”概念，打破测试时静态限制，让智能体在任务执行过程中持续进化。
- **层级记忆设计**：按粒度组织经验，兼顾具体操作和抽象策略，提升知识复用效率。
- **轻量高效**：仅用 Gemini-2.5 Flash 即达 SOTA，体现方法与模型规模解耦，成本可控。
- **闭环自动更新**：无需人工标注或外部监督，智能体自主反思、提炼并更新经验，自动化程度高。
- **泛化能力突出**：积累的经验可迁移到新任务，实现零样本提升，具有实际部署价值。
- **评估角度完整**：同时衡量最终性能、学习曲线、连续学习鲁棒性和泛化性，证据链较丰富。

## 8. 不足与局限

- **资源信息缺失**：未明确报告 GPU、训练/推理时长、能耗等算力细节，影响复现和成本评估。
- **基准覆盖有限**：仅依赖 TAC 一个 benchmark，缺少在更多真实世界任务或开放式环境中的验证。
- **实验细节不透明**：摘要未提供消融实验的具体设置、统计显著性检验、误差范围等，难以从当前文本中判断实验的统计严谨性。
- **模型依赖风险**：使用特定商业模型（Gemini-2.5 Flash），未说明方法是否对基座模型的推理/反思能力高度敏感，结论可能不完全适用于更弱或更强的模型。
- **长期记忆管理问题**：未讨论记忆规模增长带来的检索效率、冗余、遗忘或冲突等问题。
- **理论保障缺失**：自进化机制缺乏收敛性、稳定性或理论性能保证，存在错误经验固化导致性能恶化的可能。
- **应用边界**：主要面向生产力任务，对高风险、多智能体协作或需要硬约束的场景未做说明。

（完）

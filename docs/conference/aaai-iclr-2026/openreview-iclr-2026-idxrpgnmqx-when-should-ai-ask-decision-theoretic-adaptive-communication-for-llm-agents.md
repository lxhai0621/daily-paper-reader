---
title: "When Should AI Ask: Decision-theoretic Adaptive Communication for LLM Agents"
title_zh: AI何时该提问：面向LLM智能体的决策论自适应通信
authors: "Yijiang River Dong, Tiancheng Hu, Zheng Hui, Caiqi Zhang, Ivan Vulić, Andreea Bobu, Nigel Collier"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=idXrPgNmqx"
tags: ["query:ma-kf"]
score: 8.0
evidence: LLM智能体决策何时提问澄清，在自主行动与用户成本之间取得平衡
tldr: 真实用户查询常信息不完备，LLM智能体需要决定是自主行动还是向用户澄清，过多询问会影响体验。本文提出一个决策论自适应通信框架，依据查询歧义度、任务风险和用户认知负荷三大情境因素动态判断澄清必要性，并用信息价值方法在推理时权衡澄清的期望效用与沟通成本。该方法可减少不必要的提问，同时避免高风险错误，使智能体协作更高效、更符合用户预期。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 用户查询常不完备，智能体在自主行动风险与过多提问之间面临两难。
method: 构建决策论框架，基于查询歧义、任务风险和认知负荷，用信息价值衡量澄清必要性。
result: 在推理时动态决定是否澄清，在降低沟通成本的同时避免高风险错误。
conclusion: 将澄清视为信息价值决策可使LLM智能体的交互更自适应、更用户友好。
---

## Abstract
Large language model (LLM) agents are increasingly used to assist people with complex tasks, but real-world user queries are often underspecified. When information is missing, agents face a dilemma: act autonomously and risk costly mistakes, or ask too many clarifying questions and frustrate the user. We propose a decision-theoretical framework for adaptive communication that dynamically determines when clarification is necessary based on three contextual factors: query ambiguity, task risk, and user cognitive load. 
Our approach instantiates this framework with a Value of Information (VoI) method that, at inference time, explicitly weighs the expected utility of clarification against its communication cost. Unlike existing confidence thresholds or heuristic prompting approaches, our method requires no task-specific tuning and adapts flexibly across domains and stakes. In experiments on 20 Questions, medical diagnosis, flight recommendation, and Webshop, our adaptive strategies consistently achieve higher utility than baselines, asking fewer unnecessary queries and requiring no hand-tuned thresholds. These results establish a principled foundation for building LLM agents that are not only competent actors, but also strategic communicators able to adapt their behavior to user context and task stakes for more reliable real-world collaboration.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：真实世界中的用户查询往往信息不完备（underspecified），而大语言模型（LLM）智能体在辅助用户完成复杂任务时，会面临一个两难困境：
  - 若自主行动，可能因信息缺失而犯错，尤其在风险较高的场景下代价高昂；
  - 若频繁向用户提问澄清，又会增加用户认知负担和沟通成本，损害使用体验。
- **核心问题**：智能体如何动态、智能地判断“何时应该主动询问用户”，在自主行动的风险与过多提问的成本之间取得最优平衡。
- **整体意义**：该研究将LLM智能体从“仅具备任务执行能力”提升为“具备策略性沟通能力”的协作伙伴，使其能够根据用户上下文和任务风险调整沟通行为，为更可靠的人机协作奠定基础。

## 2. 方法论：决策论自适应通信框架

- **核心思想**：将“是否澄清”建模为一个决策论问题，而非依赖固定阈值或启发式提示。
- **三个关键情境因素**：
  1. **查询歧义度（Query Ambiguity）**：当前信息不完备的程度；
  2. **任务风险（Task Risk）**：因错误执行而可能造成的负面后果大小；
  3. **用户认知负荷（User Cognitive Load）**：询问用户需要付出的注意力与时间成本。
- **关键技术细节**：采用**信息价值（Value of Information, VoI）**方法，在推理（inference）阶段显式权衡：
  - 澄清带来的期望效用增益（即避免错误带来的收益）；
  - 与询问用户所需的沟通成本。
- **决策逻辑**：仅在“澄清的期望收益 > 沟通成本”时才发起询问；否则选择自主行动。
- **无需任务特定调参**：与现有的置信度阈值或启发式提示方法不同，该方法不需要针对具体任务手动调节阈值，可跨领域、跨风险等级灵活迁移。
- **算法流程（文字描述）**：
  1. 接收用户的不完备查询；
  2. 评估当前查询的歧义程度；
  3. 估算任务风险（错误代价）与用户认知负荷（提问成本）；
  4. 计算澄清的期望效用与不澄清的期望效用；
  5. 比较两者，若澄清净收益为正则提问，否则自主执行。

## 3. 实验设计

- **数据集 / 场景**：共4个不同的交互式任务环境：
  - **20 Questions（二十问）**：经典信息获取游戏，测试智能体判断何时提问；
  - **Medical Diagnosis（医疗诊断）**：高风险场景，需权衡误诊风险与提问负担；
  - **Flight Recommendation（航班推荐）**：包含多种约束和偏好的推荐场景；
  - **Webshop（网络购物）**：开放域商品检索与推荐，模拟真实在线购物。
- **Benchmark**：各任务环境下的期望效用（utility）作为主要评价指标，衡量任务成功率与沟通成本的综合收益。
- **对比方法**：
  - **置信度阈值方法（confidence thresholds）**：基于模型置信度决定是否提问；
  - **启发式提示方法（heuristic prompting）**：通过提示词手工设定询问策略；
  - 本文提出的**基于信息价值的自适应策略（VoI-based）**。

## 4. 资源与算力

- 论文提供的文本摘要中**未明确说明**使用的GPU型号、数量、训练时长或推理算力资源。
- 仅从描述判断，该方法的VoI计算发生在推理阶段，可能不需要大量额外训练，但具体的硬件配置和运行成本信息缺失。

## 5. 实验数量与充分性

- **实验覆盖**：在4个差异显著的任务场景（游戏、医疗、航班、电商）上进行测试，覆盖了低风险到高风险、多轮交互到单轮决策等多种情形，具有较强的领域多样性。
- **对比完整性**：与两种主流基线（阈值法、提示法）相比，验证了方法无需手动调参的优势。
- **充分性评价**：
  - 场景多样性较好，但**未说明每个场景中任务实例的数量**、是否包含消融实验（如移除某一情境因素后的效果）、是否进行敏感性分析或用户研究。
  - 缺乏对“查询歧义度”“任务风险”“认知负荷”三个因素各自贡献的消融验证。
  - 总体而言，实验设计初步证明了方法的有效性和通用性，但在统计显著性和细粒度分析方面信息不足，可能仍需更多实验支撑。

## 6. 主要结论与发现

- 基于信息价值的自适应通信策略在**所有4个任务**中均持续获得比基线更高的效用。
- 该方法能**减少不必要的询问**，同时**避免高风险错误**，在沟通成本与任务安全之间取得更优平衡。
- 与依赖阈值或提示的方法相比，**无需针对任务进行手工调参**，即可适应不同领域和不同风险等级。
- 结论表明：将澄清视为“信息价值”决策，能够让LLM智能体从被动执行者转变为主动且战略性的沟通者，实现更可靠、更符合用户预期的协作。

## 7. 优点

- **理论扎实**：将通信决策建立在决策论和信息价值框架之上，具有明确的数学基础和可解释性。
- **动态且自适应**：能够根据任务风险、歧义度和用户负担实时调整提问策略，而非静态规则。
- **免调参**：突破了传统阈值方法对人工调参的依赖，增强了跨任务泛化能力。
- **平衡性好**：同时考虑了“少问”的用户体验和“不问”的风险后果，兼顾效率和安全性。
- **评估场景多样**：涵盖游戏、医疗、推荐、电商等不同风险领域，提高了结论的普适性。

## 8. 不足与局限

- **算力与资源信息缺失**：未报告具体的硬件配置、推理开销或计算成本，难以评估实际部署成本。
- **实验细节不完整**：摘要中未提供任务实例数量、评测指标的具体定义、基线的具体实现方式以及是否进行统计显著性检验。
- **缺少消融与敏感性分析**：未明确验证三个情境因素各自的贡献，也未探讨不同风险等级、不同用户模型下的鲁棒性。
- **用户建模简化**：对“用户认知负荷”的量化可能依赖简化假设，真实用户的疲劳程度、耐心和偏好差异可能更复杂。
- **未涉及多轮长期交互**：4个场景中有些可能是短期任务，对于长期协作中的记忆、反馈累积和信任建立等维度未展开讨论。
- **应用边界**：信息价值方法依赖对“风险代价”和“沟通成本”的准确估计，在实际开放域中这些估计可能难以精确获取，从而影响决策质量。
- **英文原文未给出错误分析或失败案例**，对方法在何种情况下失效的讨论不足。

（完）

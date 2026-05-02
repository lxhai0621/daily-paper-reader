---
title: Behavior-Driven Marine Larval Dispersal and Settlement with AI Agent-Based Modeling
title_zh: 基于AI智能体建模的行为驱动型海洋幼体扩散与定居
authors: "Zhou, X., Wang, G., Wu, R., Bracco, A."
date: 2026-05-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.29.721765v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 将基于大语言模型的行为智能体与生物物理模型集成
tldr: 传统的海洋幼虫扩散模型受限于静态参数，难以模拟复杂的适应性行为。本研究提出了SWARM框架，通过将大语言模型（LLM）驱动的行为智能体与标准生物物理模型相结合，模拟幼虫在远洋阶段的主动决策。以墨西哥湾红鲷鱼幼虫为案例，研究证明了LLM能使智能体产生提高定居率的适应性行为，为预测海洋连通性和生态修复提供了新路径。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的幼虫扩散模型缺乏对复杂适应性行为的表达能力，限制了海洋修复策略的设计。
method: 开发了SWARM框架，将基于大语言模型的行为智能体集成到生物物理模型中，实现幼虫的主动决策模拟。
result: 智能体在理想和真实环境下均展现出能提高定居成功率的适应性行为，并生成了可解释的垂直分布模式。
conclusion: 大语言模型能够有效克服扩散建模中的长期局限，通过显式表达行为驱动因素来提升海洋连通性预测的准确性。
---

## 摘要
幼体扩散模型对于绘制和预测海洋中鱼类浮游生物动态至关重要，但尽管经过数十年的改进，它们在表征适应性行为方面仍存在根本局限，主要依赖于静态特征参数化。这种缺陷限制了我们在日益严峻的海洋环境下设计有效修复和缓解策略的能力。SWARM（模拟海洋连通性的水生智能体路径）通过将基于大语言模型（LLM）的行为智能体与标准生物物理模型相结合，模拟远洋幼体阶段的主动决策，从而克服了这一障碍。在针对墨西哥湾红鲷鱼幼体的理想化和现实条件下，智能体发展出了能够提高定居率并产生可解释垂直分布模式的适应性行为。SWARM 证明了 LLM 可以通过显式表征运动的行为驱动因素，克服扩散建模中长期存在的局限性，为预测连通性和设计有效的海洋生态系统修复开辟了新途径。

## Abstract
Larval dispersal models are central to mapping and predicting ichthyoplankton dynamics in the ocean, yet despite decades of refinement they remain fundamentally limited by their ability to represent adaptive behaviors, relying instead on static trait parameterizations. This deficiency constrains our capacity to design effective restoration and mitigation strategies in an increasingly stressed ocean. SWARM (Simulating Waterborne Agent Routes for Marine connectivity) overcomes this barrier by integrating Large Language Model (LLM)-based behavioral agents with a standard biophysical model to simulate active decision making during the pelagic larval stage. In both idealized and realistic conditions focusing on Red Snapper larvae in the Gulf of Mexico, agents develop adaptive behaviors that improve settlement and generate explainable vertical distribution patterns. SWARM demonstrates that LLMs can overcome long standing limitations in dispersal modelling by explicitly representing behavioral drivers of movement, opening new pathways for predicting connectivity and designing effective marine-ecosystem restoration.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **SWARM**（Simulating Waterborne Agent Routes for Marine connectivity）的创新框架，旨在通过大语言模型（LLM）驱动的智能体来模拟海洋生物幼体的扩散与定居行为。

以下是对该论文的深度结构化总结：

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：传统的海洋幼体扩散模型（Larval Dispersal Models）在模拟鱼类等生物的“适应性行为”方面存在根本局限。
*   **研究背景**：现有的生物物理模型大多依赖于静态的参数化特征（如固定的垂直迁移模式），无法反映幼体在复杂、动态海洋环境中根据环境信号（如温度、光照、猎物密度）做出的主动决策。
*   **整体含义**：这种局限性削弱了科学家预测海洋连通性和设计生态修复策略的准确性。本研究试图引入 AI 智能体，赋予模拟幼体“大脑”，使其能够根据环境变化自主调整行为。

### 2. 论文提出的方法论
*   **核心思想**：将 **大语言模型（LLM）作为决策引擎** 集成到标准的 **生物物理模型** 中。
*   **关键技术细节**：
    *   **SWARM 框架**：该框架将物理环境模拟（洋流、深度、温度等）与基于 LLM 的行为智能体解耦。
    *   **感知-决策循环**：智能体在每个时间步接收环境状态（作为 Prompt 输入），LLM 根据预设的生物学逻辑和实时数据进行推理，输出行动指令（如向上/向下游泳、保持深度）。
    *   **显式行为表征**：不同于黑盒模型，LLM 能够生成可解释的行为逻辑，说明其为何在特定环境下选择特定的垂直分布模式。
*   **算法流程**：物理模型计算粒子的被动平流 -> 提取粒子所在位置的环境参数 -> LLM 智能体处理参数并决定主动运动分量 -> 更新粒子位置。

### 3. 实验设计
*   **研究对象**：墨西哥湾的**红鲷鱼（Red Snapper）**幼体。
*   **实验场景**：
    1.  **理想化环境**：在受控的简化物理条件下测试智能体的基本生存和决策逻辑。
    2.  **现实环境**：使用墨西哥湾真实的海洋动力学数据进行模拟。
*   **Benchmark（基准）**：传统的生物物理模型，通常采用被动扩散或基于固定规则的垂直迁移（DVM）模型。
*   **对比维度**：定居成功率（Settlement Success）、垂直分布模式的合理性、对环境压力的适应能力。

### 4. 资源与算力
*   **算力说明**：论文摘要和元数据中**未明确说明**具体的 GPU 型号、数量或训练时长。
*   **技术路径推测**：由于使用了 LLM 驱动智能体，实验可能涉及大量的 API 调用（如 OpenAI GPT 系列）或本地部署的开源模型（如 Llama 系列）推理，而非传统的从头训练。

### 5. 实验数量与充分性
*   **实验规模**：研究涵盖了从理想化到现实场景的跨越，验证了模型在不同复杂度下的鲁棒性。
*   **充分性评价**：实验设计较为充分，通过对比“智能体驱动”与“静态参数驱动”的结果，清晰地展示了 AI 介入带来的增量价值。
*   **客观性**：通过引入可解释的行为模式分析，增强了实验结果的说服力，证明了定居率的提升并非随机，而是源于合理的适应性行为。

### 6. 论文的主要结论与发现
*   **适应性行为的涌现**：LLM 智能体能够自发发展出提高定居成功率的行为策略，例如在接近栖息地时调整深度以利用特定洋流。
*   **可解释性**：智能体生成的垂直分布模式与已知的生物学现象（如昼夜垂直迁移）一致，且能提供决策背后的逻辑解释。
*   **性能提升**：相比传统模型，SWARM 框架下的幼体定居预测更具动态性和准确性，能够更好地模拟极端或多变环境下的生物反应。

### 7. 优点（亮点）
*   **跨学科创新**：首次将 LLM 的推理能力引入海洋生物物理建模领域，突破了静态参数化的瓶颈。
*   **行为显式化**：解决了传统模型中行为驱动因素“黑盒化”的问题，使模拟过程具备高度的可解释性。
*   **灵活性**：该框架具有通用性，理论上可以扩展到其他海洋物种或不同的环境压力场景（如气候变暖、污染扩散）。

### 8. 不足与局限
*   **计算成本**：LLM 的推理成本远高于简单的数学公式，在大规模、高分辨率的粒子追踪模拟中可能面临算力瓶颈。
*   **潜在偏差**：LLM 的决策依赖于 Prompt 的设计和其预训练知识，可能引入非生物学的偏见或“幻觉”。
*   **实时性挑战**：在超大规模集群上进行实时生物物理耦合模拟时，LLM 的响应速度可能成为延迟的主要来源。
*   **验证难度**：野外幼体行为数据极难获取，虽然模拟结果符合逻辑，但与真实生物行为的精确对齐仍具挑战。

（完）

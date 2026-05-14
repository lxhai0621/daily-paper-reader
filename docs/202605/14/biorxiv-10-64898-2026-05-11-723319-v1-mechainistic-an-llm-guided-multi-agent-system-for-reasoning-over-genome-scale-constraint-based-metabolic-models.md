---
title: "MechAInistic: An LLM-guided Multi-Agent System for Reasoning over Genome-Scale Constraint-Based Metabolic Models"
title_zh: MechAInistic：一种用于全基因组规模约束性代谢模型推理的 LLM 引导多智能体系统
authors: "Loecker, J., Pujara, N., Bryant, W., Puniya, B. L., Packrisamy, P., Hamed, A., Helikar, T."
date: 2026-05-13
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.11.723319v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于代谢模型推理的多智能体系统
tldr: 针对代谢模型分析门槛高的问题，本文开发了MechAInistic系统。该系统采用LLM驱动的多智能体架构，能将自然语言指令转化为可执行的代谢分析工作流。它支持通路对比、扰动分析及药物靶点探索，并在类风湿性关节炎和多发性硬化症研究中成功识别出潜在重定位药物，实现了从自然语言到可重复生物学发现的转化。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在降低约束性代谢建模的技术门槛，使研究人员能通过自然语言进行复杂的生物学机制分析。
method: 构建了一个基于大语言模型的多智能体系统，利用“架构师-评审员”模式将自然语言问题转化为模型驱动的可执行工作流。
result: 在类风湿性关节炎和多发性硬化症的案例研究中，系统成功识别出Devimistat和Ivosidenib作为潜在的重定位药物。
conclusion: MechAInistic有效结合了LLM的推理能力与机械建模的严谨性，为加速生物医学发现提供了可重复的自动化工具。
---

## 摘要
约束性代谢建模是研究细胞状态和疾病机制基础的有力方法，但其有效应用需要大量的计算专业知识和对多步分析的仔细协调。我们开发了 MechAInistic 以降低这一门槛，使研究人员能够用自然语言提出复杂的生物学问题。利用大语言模型，MechAInistic 是一个围绕“架构师-评审员”（Architect-Reviewer）模式组织的多智能体系统，它将自然语言问题转化为可执行的、基于模型的流程，并生成结构化报告。该系统支持多种任务，包括通路比较、扰动分析、药物靶点探索以及跨配对代谢模型状态的基于文献的解释。我们在两个药物重利用案例中测试了 MechAInistic。对于类风湿性关节炎（RA）患者与健康对照组配对的初始 B 细胞，该系统量化了驱动疾病的代谢重连，利用拓扑枢纽过滤和鲁棒性分析对候选反应进行了优先级排序，并发现 Devimistat 是一个潜在的重利用候选药物，其通过三羧酸循环（TCA 循环）中的 2-氧代戊二酸脱氢酶发挥作用。在多发性硬化症（MS）与健康对照组配对的 CD4+ Th17 细胞研究中，相同的流程将 NADP 依赖性异柠檬酸脱氢酶确定为最佳单一靶点，并提出 ivosidenib 作为 FDA 批准的重利用候选药物。总之，这些结果表明 MechAInistic 直接与机制建模对接，并将大语言模型的推理转化为可重复的生物学发现。MechAInistic 可在 https://mechainistic.dtih.org 访问。

## Abstract
Constraint-based metabolic modeling is a powerful way to study the mechanistic basis of cellular states and disease, but its effective use demands substantial computational expertise and careful coordination of multi-step analyses. We developed MechAInistic to lower this barrier and enable researchers to ask complex biological questions in natural language. Harnessing large language models, MechAInistic is a multi-agent system organized around an Architect-Reviewer pattern that transforms a natural-language question into an executable, model-grounded workflow and generates a structured report. The system supports a variety of tasks, including pathway comparison, perturbation analysis, drug-target exploration, and literature-grounded interpretation across paired metabolic model states. We tested MechAInistic on two drug-repurposing use cases. For Naive B cells from Rheumatoid Arthritis (RA) paired with healthy controls, the system quantified the metabolic rewiring driving disease, prioritized candidate reactions using topological hub filtering and robustness analysis, and surfaced Devimistat as a potential repurposing candidate acting through 2-oxoglutarate dehydrogenase in the TCA cycle. In a paired CD4+ Th17 cell study from Multiple Sclerosis (MS) and healthy controls, the same workflow identified NADP-dependent isocitrate dehydrogenase as the optimal single target and proposed ivosidenib as an FDA-approved repurposing candidate. Together, these results show that MechAInistic interfaces directly with mechanistic modeling and turns large language model reasoning into reproducible biological discovery. MechAInistic is accessible at https://mechainistic.dtih.org.

---

## 论文详细总结（自动生成）

### 论文总结：MechAInistic 多智能体代谢模型推理系统

#### 1. 核心问题与整体含义（研究动机和背景）
约束性代谢模型（Constraint-Based Models, CBMs）是研究细胞代谢状态和疾病机制的强大工具。然而，有效使用 CBMs 存在极高的技术门槛：研究人员不仅需要深厚的生物学背景，还必须精通编程（如 Python/MATLAB）、数值优化、模型配置以及复杂的代谢网络解释。
**MechAInistic** 的研究动机在于消除这一障碍。它旨在开发一个由大语言模型（LLM）引导的多智能体系统，让非计算专业的生物医学研究人员能够通过**自然语言**提出复杂的生物学问题，并获得基于严谨计算模型和文献支持的结构化分析报告。

#### 2. 方法论：核心思想与关键技术流程
MechAInistic 的核心思想是将 LLM 的逻辑推理能力与专业的计算建模工具（如 COBRApy）相结合，通过“架构师-评审员”（Architect-Reviewer）模式确保分析的严谨性。

*   **多智能体架构**：
    *   **Architect（架构师）**：负责将用户的自然语言查询分解为分析计划，提出工具调用指令，并最终汇总生成报告。
    *   **Reviewer（评审员）**：对 Architect 提出的计划和中间证据进行批判性评估，通过打分机制（1-10分）决定是否进入下一步或重新生成计划。
    *   **Task（任务助手）**：负责具体的辅助工作，如生成 PubMed 搜索查询、将复杂的 JSON 工具输出总结为简洁的文本，以节省上下文窗口。
*   **关键技术流程**：
    1.  **计划开发**：Architect 制定工作流，Reviewer 根据完整性、工具适用性等维度打分。
    2.  **迭代合成与执行**：系统调用工具箱（包含通量平衡分析 FBA、扰动模拟、药物靶点查找等），Task 智能体总结结果。
    3.  **结果评估**：Reviewer 验证证据是否足以回答问题。
    4.  **报告生成**：生成包含定量数据、机制解释、文献支持和局限性说明的 Markdown 报告。
*   **工具集成**：集成了 COBRApy、HiGHS 求解器、BiGG 数据库、DGIdb（药物靶点数据库）和 PubMed。

#### 3. 实验设计：数据集、场景与 Benchmark
*   **实验场景**：
    *   **案例一：类风湿性关节炎（RA）**。使用配对的健康与 RA 患者 Naive B 细胞代谢模型。
    *   **案例二：多发性硬化症（MS）**。使用配对的健康与 MS 患者 CD4+ Th17 细胞代谢模型。
*   **任务目标**：识别能够将疾病状态代谢通量恢复至健康状态的单一药物疗法，同时最小化脱靶影响。
*   **Benchmark（对比方法）**：
    *   将 MechAInistic 与通用 LLM 系统进行对比，包括 **Claude (Anthropic)**、**ChatGPT (OpenAI)**、**Copilot (Microsoft)** 和 **Gemini (Google)**。
*   **评估指标**：采用“九轴评估量表”，包括模型忠实度（是否真的解析了 JSON 模型）、方法可重复性、计算证据（是否有通量值）、文献证据、任务完成度等。

#### 4. 资源与算力
*   **算力平台**：系统默认使用**国家研究平台（National Research Platform, NRP）**提供的 OpenAI 兼容端点，该平台对学术研究人员免费。
*   **模型配置**：实验中使用了 Qwen、Kimi 和 Gemma 等模型的组合。
*   **具体参数**：文中未明确指出具体的 GPU 型号、数量或训练时长。由于 MechAInistic 是一个基于现有 LLM API 的推理编排系统，而非从头训练模型，其算力消耗主要集中在推理阶段的 Token 使用上（文中补充材料提供了各步骤的 Token 计数）。

#### 5. 实验数量与充分性
*   **实验规模**：针对两个复杂的免疫学案例进行了深度端到端测试，并对 4 个主流通用 LLM 进行了横向对比。
*   **充分性评估**：
    *   **客观性**：通过九轴量表进行定性与定量结合的评估，揭示了通用 LLM 在处理结构化模型文件时的“幻觉”和执行错误（如 Claude 在处理同工酶逻辑时的错误）。
    *   **公平性**：所有对比系统均使用相同的输入文件和提示词。
    *   **局限**：虽然案例研究非常深入，但实验仅限于两个疾病场景，未来可能需要更多样化的细胞类型和代谢任务来验证其泛化能力。

#### 6. 主要结论与发现
*   **药物发现**：在 RA 案例中，系统识别出线粒体代谢重连是关键，并推荐了实验性药物 **Devimistat (CPI-613)**；在 MS 案例中，系统识别出 IDH1/IDH2 为关键靶点，并推荐了 **Ivosidenib**。
*   **架构优势**：证明了“架构师-评审员”模式能有效减少 LLM 的逻辑跳跃。通用 LLM 虽然能生成看似合理的生物学叙述，但在模型解析、通量计算和逻辑一致性方面经常失败。
*   **机制性 AI**：展示了 LLM 不应作为直接的“答案引擎”，而应作为复杂科学工作流的“编排层”。

#### 7. 优点
*   **模型接地（Grounding）**：强制要求 LLM 的推理必须基于可执行的计算工具和上传的 JSON 模型，而非仅凭预训练权重。
*   **透明度与可审计性**：生成的报告提供了从原始问题到工具调用、定量输出再到文献支持的完整审计链。
*   **降低门槛**：实现了从自然语言到专业代谢分析（如 MOMA 扰动分析）的自动化转化。

#### 8. 不足与局限
*   **模型依赖性**：分析结果高度依赖于输入代谢模型的质量。如果模型本身存在注释缺失或反应错误，系统无法自动修复。
*   **文献幻觉风险**：尽管有 Task 智能体辅助，但在验证中仍发现了一处文献引用不匹配的情况，说明人工复核仍不可或缺。
*   **交互限制**：目前的界面更倾向于单次任务处理，尚不支持开放式的多轮科学对话。
*   **外部依赖**：系统性能受限于外部数据库（如 PubMed, DGIdb）的可用性和 API 响应速度。

（完）

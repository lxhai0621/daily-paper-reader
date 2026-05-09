---
title: Benchmarking and behavioral characterization of LLM agents for protein design
title_zh: 蛋白质设计的 LLM 智能体基准测试与行为表征
authors: "Kim, J., Romero, P. A."
date: 2026-05-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.06.723381v1.full.pdf"
tags: ["query:agent"]
score: 9.0
evidence: 在科学工具使用工作流中评估大模型智能体
tldr: 本研究针对蛋白质设计领域缺乏标准化评估框架的问题，提出了BioDesignBench基准测试，包含76个涵盖抗体、酶和荧光蛋白等专家策划的任务。通过评估四种前沿大模型智能体，发现其表现虽优于硬编码流程但仍不及人类专家。研究深入分析了智能体的行为特征，揭示了其在评估深度和探索持续性上的不足，并证明通过强制多指标评估可显著提升性能，为AI蛋白质工程提供了重要的评估资源和开源工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 科学发现中的大模型智能体在复杂蛋白质设计工作流中缺乏标准化的性能与行为评估框架。
method: 提出了包含76个专家任务的BioDesignBench基准，并结合人类基线和工具使用轨迹指标对四种前沿智能体进行系统评估。
result: 最强智能体表现优于确定性流程但仍逊于专家，且存在评估过浅、缺乏方案对比和过早终止探索等行为局限。
conclusion: 智能体的性能瓶颈主要源于行为模式而非基础能力，通过强化多指标评估可显著提升其在蛋白质设计中的实际表现。
---

## 摘要
大语言模型 (LLMs) 正越来越多地被部署为科学发现的智能体，但目前缺乏评估其在科学工作流中性能和行为的标准框架。蛋白质设计提供了一个极具挑战性的测试案例，因为现代工作流结合了随机生成模型、结构预测系统和基于物理的评估工具，需要大量的候选方案探索和筛选。在此，我们介绍了 BioDesignBench，这是一个包含 76 个专家策划的蛋白质设计任务的基准，涵盖了抗体、酶、荧光蛋白、结合剂和支架，并提供了人类和非 LLM 基准以及源自工具使用轨迹的行为指标。我们在多种蛋白质设计工作流中评估了四个前沿 LLM 智能体，发现最强的智能体超过了确定性的硬编码流水线，但始终低于专家水平。尽管智能体通常会选择合适的工具，但它们对候选设计的评估过于浅薄，很少比较替代方案，并且过早终止探索。引导式工作流提高了工具覆盖率，但未能增加评估深度。强制执行更深层次的多指标评估显著提高了智能体的性能，这表明这些局限性是行为上的，而非根本的能力约束。我们发布了 BioDesignBench、开源参考智能体和公共排行榜，作为评估和改进蛋白质工程 AI 智能体的社区资源。

## Abstract
Large language models (LLMs) are increasingly deployed as agents for scientific discovery, but standardized frameworks for evaluating their performance and behaviour in scientific workflows are lacking. Protein design provides a demanding test case because modern workflows combine stochastic generative models, structure prediction systems, and physics-based evaluation tools that require extensive candidate exploration and filtering. Here we introduce BioDesignBench, a benchmark of 76 expert-curated protein design tasks spanning antibodies, enzymes, fluorescent proteins, binders, and scaffolds, together with human and non-LLM baselines and behavioural metrics derived from tool-use traces. We evaluate four frontier LLM agents across diverse protein design workflows and find that the strongest agents surpass deterministic hardcoded pipelines but consistently underperform expert practice. Although agents generally select appropriate tools, they evaluate candidate designs too shallowly, rarely compare alternatives, and terminate exploration prematurely. Guided workflows improve tool coverage but not evaluation depth. Enforcing deeper multi-metric evaluation substantially improves agent performance, demonstrating that these limitations are behavioural rather than fundamental capability constraints. We release BioDesignBench, open-source reference agents, and a public leaderboard as a community resource for evaluating and improving AI agents for protein engineering.

---

## 论文详细总结（自动生成）

### 论文总结：蛋白质设计的 LLM 智能体基准测试与行为表征 (BioDesignBench)

#### 1. 核心问题与整体含义（研究动机和背景）
随着大语言模型（LLM）智能体在科学发现中的应用日益广泛，如何评估其在复杂、多步骤科学工作流中的表现成为一个紧迫问题。蛋白质设计是一个极佳的测试场，因为它不仅需要调用工具，还需要在随机性极强的生成模型、结构预测和物理评估工具之间进行复杂的迭代、筛选和优化。
**核心问题：** 现有的评估往往只关注最终结果，缺乏对智能体如何使用工具、为何失败以及其行为模式与人类专家差异的深入理解。论文旨在通过建立标准化基准，揭示 LLM 智能体在处理随机性科学任务时的行为瓶颈。

#### 2. 核心方法论
*   **BioDesignBench 基准：** 包含 76 个专家策划的任务，涵盖抗体、酶、荧光蛋白、结合剂和支架五大类，分为“从头设计 (de novo)”和“重新设计 (redesign)”两种意图。
*   **MCP 工具生态系统：** 利用模型上下文协议 (Model Context Protocol, MCP) 封装了 17 种蛋白质设计工具（如 RFdiffusion, AlphaFold2/3, ProteinMPNN, Rosetta 等），提供统一的函数调用接口。
*   **智能体架构：** 采用 ReAct（推理+行动）范式，智能体在“计划-调用-评估-迭代”循环中运行。
*   **两种展示模式：** 
    *   **非引导模式 (Unguided)：** 仅列出原子工具描述，要求智能体自主发现工作流。
    *   **引导模式 (Guided)：** 对工具进行功能分组，提供组合工作流（如“预测并评分”）和使用提示。
*   **评分准则 (Rubric)：** 100 分制，包含方法论 (20)、编排 (15)、质量 (35)、可行性 (15)、新颖性 (5) 和多样性 (10)。其中“质量”通过算法自动评分（基于 Boltz-2 预测指标），“编排”等主观维度由 LLM 评审团 (PoLL) 评分。

#### 3. 实验设计
*   **数据集/场景：** 76 个任务均源自 2024-2026 年的最新文献（以确保不在模型训练集中）。
*   **对比方法（11 种条件）：**
    *   **LLM 智能体：** DeepSeek V3, GPT-5, Claude Sonnet 4.5, Gemini 2.5 Pro（均在引导和非引导模式下测试）。
    *   **基线：** 确定性硬编码流水线 (Hardcoded Pipeline)、人类专家 (Human Expert)、人类先知 (Human Oracle，定义性能上限)。
*   **行为指标：** 统计工具覆盖率（是否调用了正确的阶段）和评估深度（生成的候选数量、使用的评估指标种类、是否进行筛选）。

#### 4. 资源与算力
*   **算力平台：** 实验使用了杜克大学计算集群 (Duke Compute Cluster, DCC) 的计算资源。
*   **具体细节：** 文中未明确列出 LLM 推理的具体 GPU 型号或总训练时长（因为主要使用 API 调用的前沿模型），但提到了工具调用预算（如 DeepSeek V3 在干预实验中平均每任务约 33-35 次工具调用）。

#### 5. 实验数量与充分性
*   **实验规模：** 总计 836 次任务-条件观察（76 任务 × 11 条件）。
*   **干预实验：** 在 18 个分层抽样的任务子集上进行了“强制深度评估”的受控实验。
*   **充分性评价：** 实验设计非常充分且严谨。采用了 Wilcoxon 符号秩检验进行统计显著性分析，并设置了 5 层防御机制（如 8-gram 重叠审计）来防止数据污染。通过对比“计算量匹配”的对照组，排除了性能提升仅源于算力增加的可能性。

#### 6. 主要结论与发现
*   **性能超越硬编码：** 最强的智能体（DeepSeek V3 和 GPT-5）在得分上超过了固定的硬编码流水线，证明了 LLM 编排的灵活性优势。
*   **评估深度瓶颈：** 智能体与人类专家的主要差距在于“评估深度”。智能体倾向于将随机生成工具视为“确定性预测器”，很少生成多个候选方案进行对比，几乎从不丢弃次优设计（过滤率为 0）。
*   **引导模式的局限：** 引导模式能显著提高工具覆盖率（找对工具），但无法自发增加评估深度（用好工具）。
*   **行为而非能力限制：** 通过提示词强制智能体进行多指标评估和筛选，性能显著提升（DeepSeek V3 +9.3分，GPT-5 +15.9分），说明智能体具备深层评估能力，只是在默认状态下未表现出来。

#### 7. 优点与亮点
*   **行为表征：** 不只看分数，还深入分析了智能体在工具使用轨迹上的行为特征（如“浅层评估”）。
*   **标准化接口：** 引入 MCP 协议，为科学智能体与复杂生物信息学工具的交互提供了可扩展的标准。
*   **防污染机制：** 针对 LLM 评估中常见的数据泄露问题，设计了极其严格的审计和任务选择流程。
*   **开源贡献：** 发布了 BioDesignBench 基准、排行榜和开源参考智能体，具有很强的社区价值。

#### 8. 不足与局限
*   **缺乏湿实验验证：** 所有评估均基于 *in silico*（计算机模拟）指标，虽然与实验结果相关，但未经实验室真实合成验证。
*   **人类基线单一：** 人类专家基线仅代表单一从业者水平，可能存在个体偏差。
*   **任务覆盖：** 尽管涵盖了 5 类蛋白质，但对于更复杂的蛋白质复合物或动态功能设计的覆盖仍有提升空间。
*   **模型时效性：** 论文中提到的 GPT-5、Claude 4.5 等型号及 2026 年的时间戳暗示这可能是一个前瞻性或模拟未来场景的研究（注：基于当前 2024 年背景）。

（完）

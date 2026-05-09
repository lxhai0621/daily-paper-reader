---
title: "Open-Rosalind: Tool-First Biomedical LLM Agents with Process-Aware Benchmarking"
title_zh: Open-Rosalind：具有过程感知基准测试的工具优先型生物医学大语言模型智能体
authors: "Wang, L."
date: 2026-05-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.06.722404v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 具有工作流约束的工具优先生物医学LLM智能体
tldr: Open-Rosalind是一个面向生物医学领域的工具优先型LLM智能体系统，旨在平衡灵活性与科研问责制。该系统遵循证据导向、追踪完整、工作流约束和显式工具中介四大原则。研究还推出了配套的BioBench基准，不仅评估准确率，还关注工具使用正确性和追踪完整性。实验证明，工具优先执行是提升性能的关键，且约束性工作流能显著减少弱模型的失败率。
source: biorxiv
selection_source: fresh_fetch
motivation: 针对生物医学研究中通用智能体的灵活性与科研问责制之间的冲突，探索可审计的约束型智能体系统。
method: 提出了Open-Rosalind系统及其四大运行原则，并开发了包含工具正确性和追踪完整性指标的BioBench过程感知基准。
result: "工具优先执行使准确率提升了19.3至26.4个百分点，且通过针对性修复，在独立测试集上的准确率从17.8%提升至53.3%。"
conclusion: Open-Rosalind证明了工具优先和工作流约束在构建可审计生物医学智能体中的重要性，为提升科研智能体的可靠性提供了实证框架。
---

## 摘要
大语言模型正越来越多地被用作科学智能体，然而，通用智能体所受益的灵活性可能与生物医学研究所需的可追溯性相冲突。我们研究了生物医学智能体是否可以围绕可审计的约束而非不受限的自主性来构建。我们提出了 Open-Rosalind，这是一个工具优先的生物智能体系统，围绕四个运行原则设计：基于证据的输出、轨迹完整性、受工作流约束的执行，以及针对事实性主张的显式工具调解。为了评估这些原则，我们引入了 Open-Rosalind BioBench，这是一个过程感知基准，不仅衡量任务准确性，还衡量工具正确性、引用存在性、轨迹完整性和失败率。在严格的内部基准测试中，参考流水线实现了 81.4% 的准确率和完整的执行轨迹。在多模型消融实验和配对复制中，移除工具会导致准确率下降 19.3 到 26.4 个百分点，这表明工具优先执行是性能最强且最稳定的贡献因素。受限工作流还减少了在自由形式工具使用方面表现较弱的模型的低端失败。然而，一个独立于作者的 30 任务留出集最初揭示了部署模型严重的外部有效性崩溃。在诊断出五个路由和归一化故障并应用针对性修复后，留出集准确率从 17.8% 提高到 53.3%，且与无工具基准线相比最令人担忧的负面结果也消失了。综上所述，这些结果将 Open-Rosalind 定位为对可审计生物医学智能体的实证研究，而非声称仅靠协议约束就能保证卓越性能。

## Abstract
Large language models are increasingly used as scientific agents, yet the flexibility that benefits general-purpose agents can conflict with the accountability required in biomedical research. We study whether biomedical agents can be organized around auditable constraints rather than unconstrained autonomy. We present Open-Rosalind, a tool-first bio-agent system designed around four operational principles: evidence-grounded outputs, trace completeness, workflow-constrained execution, and explicit tool mediation for factual claims. To evaluate these principles, we introduce Open-Rosalind BioBench, a process-aware benchmark that measures not only task accuracy but also tool correctness, citation presence, trace completeness, and failure rate. On a strict in-house benchmark, the reference pipeline achieves 81.4% accuracy with complete execution traces. In multi-model ablations and paired replications, removing tools reduces accuracy by 19.3 to 26.4 percentage points, indicating that tool-first execution is the strongest and most stable contributor to performance. Constrained workflows also reduce lower-tail failures for models that are weak at free-form tool use. However, an author-independent 30-task hold-out initially revealed severe external-validity collapse on the deployment model. After diagnosing five routing and normalization failures and applying targeted fixes, hold-out accuracy improved from 17.8% to 53.3%, and the most concerning negative comparison against a no-tool baseline disappeared. Taken together, these results frame Open-Rosalind as an empirical study of auditable biomedical agents, rather than as a claim that protocol constraints alone guarantee superior performance.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **Open-Rosalind** 的生物医学大语言模型（LLM）智能体系统。以下是对该论文的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心冲突**：通用 LLM 智能体追求的“灵活性”与生物医学研究要求的“问责制（Accountability）”之间存在冲突。
*   **研究动机**：在科学研究中，一个主张必须是可验证、可审计且可重现的。通用智能体往往在输出中混淆了参数化记忆（幻觉风险）与工具获取的事实，且执行过程缺乏透明度。
*   **整体含义**：论文提出，生物医学智能体不应追求不受限的自主性，而应围绕“可审计的约束”进行设计。Open-Rosalind 旨在建立一种“设计契约”，确保每一个事实都有据可查，每一步操作都可回溯。

### 2. 方法论：核心思想与关键技术
Open-Rosalind 建立在**四大运行原则**之上，并通过分层架构实现：
*   **核心思想**：
    1.  **工具优先执行**：LLM 不作为知识库，仅作为工具输出的合成器。
    2.  **证据导向输出**：所有事实性主张必须带有指向工具来源（如 UniProt ID、PubMed ID）的内联引用。
    3.  **追踪完整性**：强制记录所有路由决策、工具调用和原始返回值的结构化轨迹。
    4.  **工作流约束执行**：放弃自由形式的规划，采用预定义的、有步数限制的技能（Skills）和模板化工作流。
*   **关键技术细节**：
    *   **原子工具与 MCP 接口**：基于 Model Context Protocol (MCP) 封装生物数据库（UniProt, Entrez）和本地计算工具。
    *   **确定性技能（Skills）**：将原子工具组合成处理特定任务（如序列分析、突变评估）的确定性流水线。
    *   **混合路由（Hybrid Router）**：优先使用基于规则的预过滤器处理明确查询，仅对复杂自然语言使用 LLM 意图分类。
    *   **多步任务框架（Harness）**：使用固定模板（如 `protein_research`）编排多步任务，强制执行硬性的步数上限。

### 3. 实验设计
*   **数据集/场景**：
    *   **Open-Rosalind BioBench**：包含 91 个任务实例（折叠为 59 个唯一根任务），涵盖序列分析、蛋白质注释、文献检索和突变评估。
    *   **外部留出集（Hold-out）**：由独立 LLM 生成的 30 个任务，用于测试外部有效性。
*   **基准测试（Benchmark）指标**：
    *   除了**任务准确率**外，还引入了**过程感知指标**：工具正确性、引用存在性、轨迹完整性和失败率。
*   **对比方法**：
    *   **Full Pipeline**（Open-Rosalind 全功能版）。
    *   **ReAct Baseline**（使用相同工具但无约束的自由规划模式）。
    *   **No_tool**（仅靠 LLM 参数化知识回答）。
    *   **消融实验**：移除引用（No_cite）、移除模板（No_template）。

### 4. 资源与算力
*   **算力说明**：论文未提及模型训练过程，因为该研究侧重于智能体框架。
*   **推理资源**：实验主要使用 `google/gemma-4-26b-a4b-it`（通过 OpenRouter 访问），并对比了包括 `GPT-5-mini` 在内的 6 个模型系列。
*   **环境**：后端使用 Python，前端使用 React，数据存储使用 SQLite。

### 5. 实验数量与充分性
*   **实验规模**：总计进行了 **1,770 次运行**（6 个模型系列 × 5 种消融条件 × 59 个任务）。
*   **充分性评价**：实验设计较为充分。通过多模型消融验证了框架的普适性，通过配对复制实验进行了统计显著性检验（p ≤ 10⁻⁴）。特别值得称赞的是，作者包含了一个“诊断与修复”周期，诚实地展示了系统在面对外部留出集时的初始崩溃及修复过程，这在同类论文中较为罕见且客观。

### 6. 主要结论与发现
*   **工具是性能核心**：移除工具会导致准确率下降 19.3% 至 26.4%，证明“工具优先”是生物医学任务中最稳定的性能提升手段。
*   **约束提升稳定性**：对于在自由规划（ReAct）中表现较弱的模型（如 GPT-5-mini），受限工作流显著减少了灾难性失败，准确率提升了 35.3%。
*   **外部有效性挑战**：初始测试显示系统对自然语言的鲁棒性不足（准确率一度仅 17.8%），通过修复路由和查询归一化逻辑，准确率回升至 53.3%。
*   **权衡取舍**：虽然约束提高了可审计性，但在某些任务上，其准确率仍略低于灵活性更高的 ReAct 模式。

### 7. 优点
*   **原则导向设计**：将“可审计性”作为第一优先级，而非盲目追求准确率。
*   **过程感知评估**：BioBench 不仅看结果，还看过程（工具使用是否正确、是否有引用），更符合科研规范。
*   **高度透明**：开源了系统、基准测试以及所有实验的执行轨迹（Traces）。
*   **实事求是的态度**：详细记录了外部验证失败后的修复过程，为后续研究提供了宝贵的工程经验。

### 8. 不足与局限
*   **基准规模较小**：59 个根任务和 30 个留出任务的规模相对较小，且部分任务由 LLM 生成而非完全由人类专家标注。
*   **灵活性受限**：手写的任务模板虽然保证了重现性，但也限制了系统处理超出预定义工作流任务的能力。
*   **路由依赖性**：系统的有效性高度依赖于第一步的路由准确性，一旦路由错误，后续步骤将完全失效。
*   **外部 API 依赖**：虽然轨迹可审计，但由于依赖实时外部 API（如 PubMed），实现“比特级”的完全重现仍有挑战。

（完）

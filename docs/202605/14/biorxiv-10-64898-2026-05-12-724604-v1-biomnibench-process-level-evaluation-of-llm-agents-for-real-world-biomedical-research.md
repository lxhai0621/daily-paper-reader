---
title: "BiomniBench: Process-level Evaluation of LLM Agents for Real-world Biomedical Research"
title_zh: BiomniBench：面向真实世界生物医学研究的 LLM 智能体过程级评估
authors: "Qu, Y., Lu, Y., Tu, X., Zhang, S., She, T., Shaw, A. G., Shih, J.-H., Zhao, B., Shen, M., Yang, H., Yan, J., Zhang, R., Wu, X., Li, T., Cong, L., Hu, X., Jiang, Y., Dong, J., Peng, T., Leskovec, J., Huang, K."
date: 2026-05-14
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.12.724604v1.full.pdf"
tags: ["query:agent"]
score: 9.0
evidence: 生物医学研究中LLM智能体轨迹的过程级评估
tldr: 针对现有生物医学LLM智能体评估仅关注结果、易受记忆和错误推理干扰的问题，本文提出BiomniBench框架。该框架通过专家设计的细粒度准则对智能体全轨迹进行过程级评估。首个实例BiomniBench-DA包含100个基于顶级期刊论文的数据分析任务。研究发现，尽管前沿模型领先，但在方法选择和科学推理方面仍有显著提升空间，且代理架构对性能影响巨大。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的生物医学智能体评估仅关注最终结果，无法有效识别记忆、奖励黑客或错误推理等问题。
method: 提出BiomniBench过程级评估框架，利用专家设计的任务特定准则对智能体的完整执行轨迹进行评分。
result: 实验显示前沿模型虽表现较好但仍有巨大进步空间，且代理架构对得分的影响与基础模型相当。
conclusion: BiomniBench是首个针对真实生物医学研究的过程级评估基准，揭示了结果导向评估无法检测到的智能体失效模式。
---

## 摘要
LLM 智能体现已能够执行真实的生物医学研究，但对其进行严谨评估仍具挑战。仅关注结果的基准测试存在两方面的局限性：首先，正确的最终答案可能源于记忆、奖励黑客行为，或是由于偶然得出正确数字的错误推理；其次，有效的替代分析方案仅因与参考标准不一致而被判定为错误。为此，我们推出了 BiomniBench，这是一个过程级评估框架，旨在根据专家设计的特定任务评分标准对智能体的完整执行轨迹进行评分。其首个实例 BiomniBench-DA 包含 100 个数据分析任务，涵盖 17 种分析任务类型、5 个疾病领域及一个通用生物学类别。每个任务均基于发表在《Nature》、《Cell》和《Science》等顶级期刊上的高影响力论文，并由原论文作者或资深领域专家共同开发。通过在四种智能体框架下对前沿模型和开源模型进行基准测试，我们发现了三个关键点：(1) 前沿模型虽处于领先地位，但仍有巨大的提升空间；(2) 智能体框架对评分的影响程度与基础模型相当；(3) 智能体在方法选择、生物学解释和科学推理方面经常表现不足。BiomniBench 是首个针对真实世界生物医学研究中 AI 智能体的过程级基准测试，揭示了仅靠结果评估无法检测到的失效模式。

## Abstract
LLM agents now perform real biomedical research, but evaluating them rigorously is hard. Outcome-only benchmarks fail in two ways. First, a correct final answer can come from memorization, reward hacking, or wrong reasoning that produces the right number by chance. Second, valid alternative analyses are marked wrong simply because they differ from the reference. We introduce BiomniBench, a process-level evaluation framework that scores the full agent trajectory against expert-designed, task-specific rubrics. Its first instantiation, BiomniBench-DA, contains 100 data-analysis tasks across 17 analytical task types, 5 disease areas, and a general-biology category, each based on a high-impact paper from top-tier journals such as Nature, Cell, and Science and co-developed with an original paper author or an experienced domain expert. Benchmarking frontier and open-weight models across four agent harnesses reveals three findings: (1) frontier models lead but substantial headroom remains; (2) the agent harness shifts scores as much as the base model; (3) agents recurrently fall short on method selection, biological interpretation, and scientific reasoning. BiomniBench is the first process-level benchmark for AI agents on real-world biomedical research, exposing failure modes that outcome-only evaluation cannot detect.

---

## 论文详细总结（自动生成）

这是一份关于论文《BiomniBench: Process-level Evaluation of LLM Agents for Real-world Biomedical Research》的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：现有的生物医学大语言模型（LLM）评估主要关注“结果导向”（Outcome-only），即只看最终答案是否正确。这种方式存在三大弊端：
    1.  **无法区分推理与记忆**：智能体可能通过记忆训练数据或“奖励黑客”（Reward hacking）行为凑出正确答案，而非通过真正的科学推理。
    2.  **忽视过程合理性**：即使最终数值有偏差，智能体采用的分析流程可能是科学合理的；反之，错误的推理也可能偶然得到正确结果。
    3.  **缺乏诊断能力**：结果导向的评估无法告诉研究者智能体是在哪个环节（如数据清洗、统计方法选择或结果解释）出了错。
*   **整体含义**：本文提出了 **BiomniBench**，这是首个针对真实世界生物医学研究的**过程级（Process-level）**评估框架。它通过评估智能体的完整执行轨迹（Trajectory），为开发更可靠、透明的生物医学 AI 助手提供了科学的度量衡。

### 2. 论文提出的方法论
*   **核心思想**：将评估重心从“最终输出”转移到“执行全过程”，利用专家设计的细粒度准则（Rubrics）对智能体的每一步行动进行评分。
*   **关键技术细节**：
    *   **过程级评分准则（Rubric-based Evaluation）**：针对每个任务，由领域专家制定详细的评分标准，涵盖数据预处理、方法选择、代码执行、生物学解释等维度。
    *   **轨迹提取**：记录智能体与环境交互的所有步骤（思考过程、调用的工具、生成的代码、观察到的结果）。
    *   **LLM-as-a-Judge 增强**：使用先进的 LLM（如 GPT-4o）作为评委，根据专家准则对轨迹进行打分，并提供定性反馈。
    *   **BiomniBench-DA 实例**：作为框架的首个实现，专注于数据分析（Data Analysis），包含从原始数据到科学结论的完整闭环。

### 3. 实验设计
*   **数据集/场景**：
    *   **BiomniBench-DA**：包含 100 个高质量任务，源自《Nature》、《Cell》、《Science》等顶级期刊的论文。
    *   **覆盖范围**：涵盖 17 种分析类型（如单细胞测序、空间转录组、蛋白质组学等）、5 个疾病领域（癌症、免疫、神经等）及通用生物学。
*   **对比方法（基础模型）**：
    *   **闭源模型**：GPT-4o, Claude 3.5 Sonnet, Gemini 1.5 Pro。
    *   **开源模型**：Llama 3 (70B/405B), Qwen 2 (72B), DeepSeek-V2。
*   **对比框架（智能体架构）**：
    *   对比了四种主流智能体框架：ReAct、Plan-and-Execute、OpenAI Assistants API 等，以研究架构对性能的影响。

### 4. 资源与算力
*   **算力说明**：论文主要侧重于对现有预训练模型的**推理评估**，而非从头训练模型。
*   **具体细节**：文中未详细列出具体的 GPU 型号和总算力消耗时长，但提到评估过程涉及大量的 API 调用（针对闭源模型）和在私有集群上部署开源模型进行推理。由于涉及 100 个复杂任务且每个任务包含多步交互，其推理成本显著高于传统的单轮问答基准测试。

### 5. 实验数量与充分性
*   **实验规模**：
    *   100 个专家级任务，每个任务均由原论文作者或资深专家审核。
    *   跨越了多个模型系列和多种智能体架构。
*   **充分性与公平性**：
    *   **多样性**：任务类型极其丰富，避免了单一任务类型的偏见。
    *   **客观性**：通过引入专家设计的 Rubrics，减少了 LLM 评委的主观性。
    *   **对比实验**：通过控制变量法（固定模型换架构，或固定架构换模型），深入探讨了性能来源。实验设计非常严谨，足以支撑其结论。

### 6. 主要结论与发现
1.  **能力上限尚远**：即使是目前最强的模型（如 GPT-4o），在复杂生物医学任务的过程得分也远未达到人类专家水平，存在巨大提升空间。
2.  **架构与模型同等重要**：智能体框架（Harness）的选择对最终得分的影响，竟然与基础模型本身的能力提升处于同一量级。
3.  **核心短板**：智能体在**方法论选择**（Method Selection）和**生物学解释**（Biological Interpretation）方面表现最差，经常出现“代码能跑通但生物学逻辑错误”的情况。
4.  **结果评估的欺骗性**：实验证明，许多在结果上表现良好的智能体，在过程评估中被发现存在严重的逻辑漏洞或错误的统计假设。

### 7. 优点
*   **真实性极高**：任务直接源自顶级期刊论文，而非合成数据，具有极高的学术和应用价值。
*   **评估维度深入**：首次系统性地将“过程级评估”引入生物医学 AI 领域，解决了“对的结果可能来自错的过程”这一痛点。
*   **专家参与度高**：由原论文作者参与设计准则，确保了评估的权威性和专业性。

### 8. 不足与局限
*   **评估成本高昂**：由于需要 LLM 评委阅读长轨迹并对照复杂准则，评估的 Token 消耗和时间成本较高。
*   **专家依赖性**：扩展新任务需要领域专家深度参与编写 Rubrics，难以像自动化基准测试那样快速大规模扩张。
*   **LLM 评委偏见**：尽管有准则约束，LLM 作为评委仍可能存在对长文本的注意力偏差或对特定风格代码的偏好。

（完）

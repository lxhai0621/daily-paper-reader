---
title: "Towards autonomous biology: Compiler-Verified Protocols as a Foundation for Real World AI Execution"
title_zh: 迈向自主生物学：编译器验证的协议作为现实世界 AI 执行的基础
authors: "Song, R., Fu, Y., Zhao, Z., Yu, J., Yuan, Q., Chen, C.-T."
date: 2026-05-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.05.720956v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于生物学闭环发现的自主AI智能体
tldr: "本研究针对生物实验协议依赖模糊自然语言导致的复现性差等问题，提出了生物协议语言（BPL）及其自动生成管线BPL-COGEN。BPL具备原生生物类型系统，能通过编译器验证物理一致性；BPL-COGEN结合大模型与编译器实现协议的自动纠错与转化。实验证明该方法在300篇Nature Protocols上达到95.1%的保真度，并在湿实验中验证了跨平台的可靠性，为生物学具身智能奠定了基础。"
source: biorxiv
selection_source: fresh_fetch
motivation: 传统生物实验协议依赖模糊的自然语言描述，导致实验在准确性、验证和跨平台移植方面存在严重缺陷。
method: 开发了具有生物原生类型系统的领域特定语言BPL，并结合300亿参数大模型与确定性编译器构建了自动纠错生成管线BPL-COGEN。
result: "在300篇Nature Protocols基准测试中达到95.1%的保真度，并通过湿实验成功实现了跨平台和跨设备的协议复现。"
conclusion: 该研究建立的编译器验证协议生成管线，是实现生物学领域物理具身人工智能自主执行的关键前提。
---

## 摘要
人工智能已从分析实验数据发展到自主生成假设、设计实验并协调闭环发现。然而，从计算推理到物理执行的转化仍受限于实验协议，在生物学领域，实验协议仍依赖于模糊的自然语言描述：而其他工程学科在几十年前就已放弃这种媒介，转而采用经过编译器验证的规范语言。这种缺陷在三个维度上削弱了可重复性：协议准确性、执行前验证和跨平台移植性。现有的形式化方法仅解决了这些挑战的子集，在表达能力与严谨性、移植性与标准化、或易用性与溯源性之间进行权衡。在此，我们介绍了生物协议语言（BPL），这是一种具有生物原生类型系统的领域特定语言，其中每个数值都带有物理单位，每种试剂都声明其物理形态，每个容器都维持编译器跟踪的状态，从而使隐含的假设必须被明确陈述，且物理上不可能的操作在编译时就会被拒绝。我们进一步开发了 BPL-COGEN，这是一个将经过微调的 300 亿参数语言模型与确定性编译器耦合在“生成-验证-修复”闭环中的流水线，通过编译器诊断迭代修正从自然语言标准操作程序（SOP）到 BPL 的翻译，直到满足所有物理、维度和状态约束。在 300 篇已发表的 Nature Protocols 论文基准测试中，BPL-COGEN 针对源协议（作为基准真相）实现了 95.1 的总体保真度得分。在 GFP 表达库构建和 HPLC 到 UHPLC 方法迁移的湿实验及跨平台验证中，证实了单一 BPL 源代码在手动和液体处理器辅助环境下均能实现可重复的执行。研究结果建立了一种生成编译器验证协议的新型流水线，这是生物学中具身 AI 的必要前提。

## Abstract
Artificial intelligence has advanced from analyzing experimental data to autonomously generating hypotheses, designing experiments, and coordinating closed loop discovery. Yet the translation from computational reasoning to physical execution remains bottlenecked by the experimental protocol, which in biology still relies on ambiguous natural-language descriptions: a medium other engineering disciplines abandoned decades ago in favor of compiler verified specification languages. This deficit fragments reproducibility along three axes: protocol accuracy, pre-execution verification, and cross platform portability. Existing formalisms address only subsets of these challenges, trading expressiveness for rigor, portability for standardization, or usability for provenance. Here we introduce the Biology Protocol Language (BPL), a domain specific language with a biology-native type system in which every quantity carries physical units, every reagent declares its physical form, and every container maintains compiler-tracked state, so that implicit assumptions must be stated explicitly and physically impossible operations are rejected at compile time. We further develop BPL-COGEN, a pipeline that couples a fine tuned 30 billion parameter language model with the deterministic compiler in a closed generate validate repair loop, iteratively correcting the translation from natural language SOPs to BPL through compiler diagnostics until all physical, dimensional, and state constraints are satisfied. On a benchmark of 300 published Nature Protocols papers, BPL COGEN achieved an overall fidelity score of 95.1 against the source protocols as ground truth. Wet-lab experiment and cross-platform validation in GFP expression library construction and HPLC to UHPLC method translation confirmed that a single BPL source yielded reproducible execution across manual and liquid handler assisted contexts. The results established a novel pipeline that generates compiler-verified protocols, which is an essential prerequisite for physically embodied AI in biology.

---

## 论文详细总结（自动生成）

这篇论文提出了一种名为 **BPL (Biology Protocol Language)** 的领域特定语言及其自动生成管线 **BPL-COGEN**，旨在解决生物实验协议因自然语言描述模糊而导致的不可复现性问题，为生物学领域的具身智能（Embodied AI）提供物理一致性的执行基础。

以下是对该论文的详细总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：生物实验协议目前主要依赖自然语言（SOPs），这种媒介具有天然的**模糊性**，导致实验在准确性、预执行验证和跨平台移植性（如从人工操作到自动化液体处理机器人）方面存在严重缺陷。
*   **研究背景**：随着 AI 开始自主生成假设和设计实验，如何将计算推理准确转化为物理执行成为了“自主生物学”的瓶颈。其他工程学科早已采用编译器验证的规范语言，而生物学仍缺乏一种既能被 AI 理解又能通过物理约束验证的标准化协议语言。

### 2. 方法论：核心思想与技术细节
*   **BPL (Biology Protocol Language)**：
    *   **原生生物类型系统**：每个数值都带有物理单位（如体积、温度），每种试剂都有物理形态声明，每个容器都有编译器跟踪的状态。
    *   **物理一致性检查**：编译器会在编译阶段拒绝物理上不可能的操作（例如：将 10ml 液体加入 1.5ml 离心管，或在未声明试剂的情况下进行移液）。
*   **BPL-COGEN 管线**：
    *   **生成-验证-修复（Generate-Validate-Repair）闭环**：
        1.  **生成**：使用一个经过微调的 **300 亿参数（30B）** 大规模语言模型，将自然语言协议翻译为 BPL 代码。
        2.  **验证**：使用确定性编译器对生成的 BPL 代码进行静态分析和物理约束检查。
        3.  **修复**：如果编译失败，编译器产生的诊断信息（报错原因）会反馈给 LLM，引导其迭代修正代码，直到通过验证。

### 3. 实验设计：数据集、Benchmark 与对比
*   **数据集/Benchmark**：研究者构建了一个包含 **300 篇已发表的《Nature Protocols》论文** 的基准测试集，将其作为“地面真值”（Ground Truth）来评估翻译的准确性。
*   **评估指标**：主要使用**保真度得分（Fidelity Score）**，衡量生成的 BPL 协议与原始复杂协议的一致性。
*   **湿实验验证场景**：
    *   **GFP（绿色荧光蛋白）表达库构建**：验证协议在复杂分子生物学流程中的有效性。
    *   **色谱方法迁移**：将 HPLC（高效液相色谱）方法迁移至 UHPLC（超高效液相色谱），验证跨设备的可移植性。
*   **对比维度**：对比了手动执行与液体处理机器人辅助执行的效果，验证单一 BPL 源代码在不同平台上的表现。

### 4. 资源与算力
*   **模型规模**：明确提到了使用了 **300 亿参数（30B）** 的语言模型。
*   **算力细节**：论文摘要及提取文本中**未明确说明**具体的 GPU 型号、数量或训练时长。通常此类规模的模型微调需要高性能计算集群（如 A100 或 H100 显卡阵列）。

### 5. 实验数量与充分性
*   **实验规模**：
    *   **基准测试**：涵盖了 300 篇顶刊协议，样本量在生物信息学协议转换领域属于较大规模，具有较强的代表性。
    *   **保真度**：达到了 95.1% 的高分，证明了管线的鲁棒性。
*   **充分性评价**：实验设计较为全面，不仅有大规模的代码生成评估，还包含了从“干实验”（代码生成）到“湿实验”（实验室验证）的闭环，且涵盖了跨平台（人工 vs 自动化）的对比，实验设计客观且公平。

### 6. 主要结论与发现
*   **BPL-COGEN 的有效性**：通过编译器反馈循环，可以显著提升 LLM 生成复杂生物协议的准确性，克服了纯 LLM 生成代码时常出现的逻辑或物理错误。
*   **跨平台一致性**：证明了单一的 BPL 源代码可以作为“单一真理来源”，在不同实验室环境和设备之间实现高可靠性的实验复现。
*   **自主生物学基石**：该研究为 AI 智能体直接操控物理实验室设备提供了一套可验证的“指令集”，是实现生物学具身智能的关键前提。

### 7. 优点：亮点与创新
*   **物理感知（Physics-aware）**：不同于通用的编程语言，BPL 将物理约束（单位、容量、状态）嵌入类型系统，从源头杜绝了不可执行的指令。
*   **闭环纠错机制**：利用编译器诊断信息指导 LLM 修复，模仿了人类程序员编写代码的过程，极大地提高了生成协议的可用性。
*   **现实世界验证**：不仅停留在理论或模拟阶段，通过《Nature Protocols》基准测试和真实的湿实验证明了实用价值。

### 8. 不足与局限
*   **LLM 依赖性**：尽管有编译器校验，但初始生成的质量仍高度依赖于 30B 模型的微调效果，对于极度冷门或复杂的实验步骤，可能需要更多迭代。
*   **BPL 学习曲线**：虽然 BPL 旨在简化描述，但对于不具备编程背景的传统生物学家来说，阅读和手动修改 BPL 代码仍存在一定门槛。
*   **硬件适配层**：虽然 BPL 实现了逻辑上的跨平台，但要真正驱动不同的机器人，仍需要针对每种硬件编写底层的驱动适配（Driver/Executor），这部分工作的通用性在文中未详细展开。

（完）

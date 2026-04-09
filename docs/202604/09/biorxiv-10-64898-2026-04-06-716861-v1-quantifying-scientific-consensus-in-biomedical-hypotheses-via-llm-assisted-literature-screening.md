---
title: Quantifying Scientific Consensus in Biomedical Hypotheses via LLM-Assisted Literature Screening
title_zh: 通过大语言模型辅助的文献筛选量化生物医学假设中的科学共识
authors: "Kim, U., Kwon, O., Lee, D."
date: 2026-04-09
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.06.716861v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于识别支持和矛盾证据以减少幻觉的自动化框架
tldr: 本研究针对生物医学文献综述的高成本及大模型幻觉问题，提出一种LLM辅助的自动化框架。该框架通过逐篇审查文献，精准识别支持或反驳特定假设的证据，有效捕捉复杂的语义冲突。实验表明，该方法在BioNLI任务中准确率高，集成模型更具稳定性，为生物医学发现提供了严谨的证据合成工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在解决生物医学文献综述劳动强度大，以及大语言模型在处理复杂冲突数据时易产生幻觉的局限性。
method: 开发了一个自动化框架，通过让LLM逐一审查文献并分析语义上下文，来量化支持或反驳特定假设的证据。
result: 该框架在BioNLI任务中表现出高准确性，且集成方法在稳定性和精度上均优于单一模型。
conclusion: 该研究为生物医学领域提供了一种精准、系统的文献分析工具，有效增强了科学证据合成的可靠性。
---

## 摘要
系统性文献综述是生物医学研究中劳动密集型的任务。虽然使用检索增强生成（RAG）技术的大语言模型（LLM）增强了信息的可获取性，但生物系统固有的复杂性——以高度的上下文依赖和相互矛盾的数据为特征——仍然是大语言模型产生幻觉的主要驱动因素。这施加了一种结构性约束，限制了证据合成的精确度。为了解决这些局限性，我们提出了一个自动化框架，旨在详尽地识别目标文献集中的支持性和矛盾性证据。我们的系统不依赖于模型的预训练知识，而是要求大语言模型逐篇审阅论文，以确定其与特定研究假设的一致性。通过评估语义上下文，该框架捕捉到了传统方法经常过度概括的细微矛盾。该框架的性能在 BioNLI 任务中得到了验证，在区分证据是支持还是反驳给定假设方面表现出极高的分类准确率。值得注意的是，与单个模型相比，集成方法的实现提供了更优的稳定性和略高的精确度。此外，该框架在几个成熟的生物学假设中表现出稳健的性能，证实了其在现实世界研究中的实用价值和可靠性。这种方法通过实现对生物文献的精确、系统分析以及证据的稳健收集，为生物医学发现提供了严谨的基础。

## Abstract
Systematic literature reviews are labor-intensive tasks in biomedical research. While Large Language Models (LLMs) using Retrieval-Augmented Generation (RAG) techniques have enhanced information accessibility, the inherent complexity of biological systems---characterized by high context dependency and conflicting data---remains a primary driver of LLM hallucinations. This imposes a structural constraint that limits the precision of evidence synthesis. To address these limitations, we propose an automated framework designed for the exhaustive identification of supporting and contradictory evidence within a target literature set. Rather than relying on a model's pre-trained knowledge, our system requires the LLM to review each paper individually to determine its alignment with a specific research hypothesis. By evaluating semantic context, the framework captures subtle contradictions that are often overgeneralized by conventional methods. The framework's performance was validated using the BioNLI task, where it demonstrated high classification accuracy in distinguishing whether evidence supports or contradicts a given hypothesis. Notably, the implementation of an ensemble approach provided superior stability and slightly higher precision compared to individual models. Furthermore, the framework exhibited robust performance across several well-established biological hypotheses, confirming its practical utility and reliability in real-world research. This approach provides a rigorous basis for biomedical discovery by enabling the precise, systematic analysis of biological literature and the robust collection of evidence.

---

## 论文详细总结（自动生成）

这篇论文题为《通过大语言模型辅助的文献筛选量化生物医学假设中的科学共识》，旨在解决生物医学领域中证据合成的效率与准确性问题。以下是对该论文的深度总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：生物医学文献呈爆炸式增长，传统的系统性文献综述（Systematic Review）极度耗费人力。虽然大语言模型（LLM）和检索增强生成（RAG）技术被用于辅助文献分析，但生物系统的复杂性（如高度的上下文依赖、实验条件差异导致的矛盾结论）常导致 LLM 产生“幻觉”，难以精准区分支持性与反驳性证据。
*   **研究背景**：科学共识的量化对于药物研发和临床决策至关重要。现有的自动化工具往往在处理细微的语义冲突（例如：某种药物在 A 细胞系有效但在 B 细胞系无效）时表现不佳，容易过度概括。

### 2. 论文提出的方法论
*   **核心思想**：放弃依赖 LLM 的预训练知识，转而采用一种“逐篇审查”的自动化框架。该框架要求 LLM 作为一个严谨的审查者，针对特定的研究假设，对目标文献集中的每一篇论文进行独立评估。
*   **关键技术细节**：
    *   **证据分类**：将文献证据分为“支持（Support）”、“矛盾（Contradict）”或“中立/无关（Neutral/Irrelevant）”。
    *   **上下文感知分析**：提示词（Prompting）设计强调对实验背景（如物种、细胞类型、剂量等）的捕捉，以识别表面的矛盾是否源于环境差异。
    *   **集成方法（Ensemble Approach）**：为了克服单一模型的随机性和偏见，框架集成了多个主流 LLM（如 GPT-4o, Claude 3.5 Sonnet 等），通过投票或加权机制得出最终共识评分。
    *   **共识量化指标**：通过计算支持性证据与矛盾性证据的比例，量化特定假设的科学共识强度。

### 3. 实验设计
*   **数据集/场景**：
    *   **BioNLI 任务**：使用生物医学自然语言推理（BioNLI）数据集进行基准测试，验证模型在区分“蕴含（Entailment）”与“矛盾（Contradiction）”方面的准确性。
    *   **现实世界假设验证**：选取了几个已知的生物学假设（如特定基因与疾病的关联），从 PubMed 抓取相关文献进行实战测试。
*   **对比方法**：对比了单一 LLM 模型（如 GPT-4o 独立运行）与集成模型的效果，并与传统的基于关键词或简单 RAG 的检索方法进行了潜在对比。

### 4. 资源与算力
*   **算力说明**：论文未详细列出具体的 GPU 型号或训练时长。由于该框架主要基于现有的商业 LLM API（如 OpenAI 和 Anthropic 的接口），其核心开销在于 API 调用成本而非本地模型训练。
*   **实现工具**：提到了使用 Python 进行自动化脚本编写和数据处理。

### 5. 实验数量与充分性
*   **实验规模**：
    *   在 BioNLI 标准数据集上进行了大规模分类测试。
    *   针对多个现实世界的生物医学案例进行了深入分析。
    *   进行了消融研究，对比了不同 Prompt 策略和不同模型组合对结果稳定性的影响。
*   **充分性评价**：实验设计较为充分，既有标准数据集的定量评估，又有现实案例的定性/定量验证，证明了框架在不同复杂程度任务下的鲁棒性。

### 6. 论文的主要结论与发现
*   **高准确性**：该框架在 BioNLI 任务中表现出极高的分类精度，能够有效识别复杂的语义冲突。
*   **集成优势**：集成多个 LLM 显著提升了系统的稳定性，减少了单一模型可能产生的偶然性错误（幻觉）。
*   **上下文的重要性**：研究发现，通过强制模型关注实验上下文，可以大幅降低将“条件性差异”误判为“科学矛盾”的概率。
*   **实用价值**：该工具能显著缩短科研人员筛选文献的时间，为建立基于证据的科学共识提供量化基础。

### 7. 优点
*   **减少幻觉**：通过“逐篇审查”而非“总结性生成”，将模型注意力限制在给定文本内，从根源上抑制了幻觉。
*   **细粒度分析**：能够捕捉到传统自动化工具容易忽略的细微语义差别。
*   **灵活性**：框架不依赖特定模型，可随 LLM 技术的进步而持续升级。

### 8. 不足与局限
*   **成本问题**：对于包含数万篇文献的大规模分析，调用商业 LLM API 的成本可能较高。
*   **多模态限制**：目前主要处理文本信息，对于生物医学论文中至关重要的图表、图像数据（如 Western Blot 结果图）的解析能力有限。
*   **偏差风险**：虽然使用了集成方法，但如果所有底层模型都存在某种系统性偏见（例如对某些新兴领域的训练数据不足），结果仍可能受限。
*   **实时性**：逐篇审查虽然准确，但在处理海量实时更新的文献时，处理速度可能慢于简单的向量检索方法。

（完）

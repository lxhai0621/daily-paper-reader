---
title: "NEURA: An agentic system for autonomous neuroimaging workflows"
title_zh: NEURA：一种用于自主神经影像工作流的智能体系统
authors: "Xie, J., Wang, J., Wu, X., Liu, X., Mi, Y., Liu, Q., Xu, T., Liu, C., Chen, H., Guo, J."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.721217v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自主神经影像工作流的智能体系统
tldr: "针对神经影像学分析门槛高、跨学科专业要求严苛的问题，本文推出了基于大语言模型的智能体系统NEURA。该系统能处理自由文本研究问题和多模态数据集，自动生成分析计划、执行脚本并输出结构化报告。实验表明，NEURA在规划准确率上达到89.5%，显著超越传统LLM方法，并在脊髓小脑共济失调3型案例中验证了其可靠性，为自动化、可解释的神经影像研究提供了新方案。"
source: biorxiv
selection_source: fresh_fetch
motivation: 神经影像学分析需要深厚的跨学科背景，极高的专业门槛限制了其在临床和科研中的广泛应用。
method: 开发了名为NEURA的LLM驱动智能体系统，通过处理自然语言指令实现神经影像工作流的自动规划、脚本执行与结果验证。
result: "NEURA实现了89.5%的规划准确率，在工具选择和排序上大幅优于直接LLM查询，并成功识别出与专家分析一致的病理特征。"
conclusion: NEURA标志着神经影像研究从简单的流程自动化向严谨、可扩展且具有高度可解释性的自主研究系统的重大进步。
---

## 摘要
神经影像是研究人类大脑的关键手段；然而，其所需的深厚跨学科专业知识构成了极高的门槛，限制了其更广泛的临床和科学应用。我们推出了 NEURA，这是一个由大语言模型（LLM）驱动的智能体系统，用于自动化的神经影像工作流规划与分析。NEURA 处理自由文本形式的研究问题和多模态神经影像数据集，生成有据可依的分析计划、可执行脚本、经过验证的统计结果和结构化报告，并提供与中间产物及完整执行记录相关联的可追溯推理过程。通过在精选基准测试上的广泛评估，NEURA 实现了 89.5% 的规划准确率，显著优于直接的 LLM 查询，在规划准确率、工具选择和工具排序方面平均分别提升了 30.5%、25.6% 和 36.7%。在脊髓小脑共济失调 3 型的案例研究中，NEURA 自主识别出了与既定病理和专家手动分析一致的小脑萎缩和异常扩散模式。总的来看，这些结果表明我们的工作实现了从流水线自动化向严谨、可扩展且可解释的神经影像研究系统的跨越。

## Abstract
Neuroimaging is essential for studying the human brain; however, the deep interdisciplinary expertise required imposes a very high threshold, limiting its broader clinical and scientific applications. We introduce NEURA, a large language model (LLM)-powered agentic system for automated neuroimaging workflow planning and analysis. NEURA processes free-text research questions and multimodal neuroimaging datasets to generate evidence-grounded analysis plans, executable scripts, validated statistical results and structured reports, with traceable reasoning linked to intermediate artefacts and full execution records. Through extensive evaluations on a curated benchmark, NEURA achieved an 89.5% planning accuracy and substantially outperformed direct LLM queries, with average gains of 30.5% in planning accuracy, 25.6% in tool selection and 36.7% in tool ordering. In case studies of spinocerebellar ataxia type 3, NEURA autonomously identified cerebellar atrophy and abnormal diffusivity patterns consistent with established pathologies and expert manual analyses. Collectively, these results demonstrate that our work advances from pipeline automation to rigorous, scalable and interpretable neuroimaging research systems.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **NEURA** 的自主神经影像智能体系统，旨在通过大语言模型（LLM）降低神经影像研究的技术门槛。以下是对该论文的深度结构化总结：

### 1. 论文的核心问题与整体含义
*   **核心问题**：神经影像学分析（如 MRI、fMRI、DTI 等）具有极高的专业门槛，要求研究者同时具备神经科学、物理学、计算机编程和统计学等多学科知识。现有的分析工具链复杂且碎片化，导致临床医生和非技术背景的科学家难以高效开展研究。
*   **整体含义**：NEURA 的出现标志着神经影像分析从“手动/半自动脚本编写”向“自主智能体驱动”的转变。它不仅能自动执行任务，还能理解自然语言指令，生成可解释的科研逻辑，从而实现神经影像研究的规模化和民主化。

### 2. 论文提出的方法论
NEURA 是一个基于 LLM 的智能体（Agentic）系统，其核心架构包含以下关键环节：
*   **自然语言理解与规划**：接收自由文本形式的研究问题（如“分析某疾病组与对照组的小脑灰质体积差异”），利用 LLM 将其分解为结构化的分析步骤。
*   **工具调用与脚本生成**：系统内置了神经影像学主流工具（如 FSL, FreeSurfer, ANTs 等）的知识库，能够根据规划自动编写 Python 或 Shell 脚本。
*   **自主执行与闭环验证**：系统在受控环境中运行脚本，实时监控输出。如果遇到报错，智能体会根据错误日志进行自我修正（Self-correction）。
*   **多模态数据处理**：支持结构像（T1w）、弥散张量成像（DTI）等多种模态的并行处理与融合分析。
*   **可追溯的推理报告**：最终输出不仅包含统计结果，还附带完整的推理链条、中间产物链接和执行记录，确保科研的可重复性和透明度。

### 3. 实验设计
*   **基准测试（Benchmark）**：研究团队构建了一个精选的神经影像任务基准测试集，涵盖了从基础预处理到复杂统计建模的多种场景。
*   **对比方法**：将 NEURA 与直接使用 LLM（如 GPT-4o, Claude 3.5 Sonnet）进行零样本（Zero-shot）或少样本（Few-shot）查询的结果进行对比。
*   **案例研究（Case Study）**：针对**脊髓小脑共济失调 3 型（SCA3）**的真实临床数据集进行端到端分析，验证系统在发现病理特征方面的有效性。

### 4. 资源与算力
*   **算力说明**：论文摘要和核心内容中未详细列出具体的 GPU 型号或训练时长。由于 NEURA 主要是基于 LLM 的智能体系统，其核心能力可能源于对现有先进模型（如 GPT-4 系列）的 API 调用或微调，而非从头训练一个超大规模基础模型。
*   **环境要求**：系统运行需要安装标准的神经影像处理软件库（如 FSL, FreeSurfer 等）的计算环境。

### 5. 实验数量与充分性
*   **实验规模**：
    *   在基准测试中进行了广泛评估，结果显示 NEURA 达到了 **89.5%** 的规划准确率。
    *   对比实验显示，NEURA 在规划准确率、工具选择和排序上分别比直接 LLM 查询高出 **30.5%、25.6% 和 36.7%**。
*   **充分性评价**：实验设计较为充分，既有量化的基准测试，又有质化的临床案例验证。通过与专家手动分析结果的对比，证明了系统在处理复杂病理数据时的可靠性。

### 6. 论文的主要结论与发现
*   **性能卓越**：NEURA 在处理复杂的神经影像工作流时，表现远超通用的 LLM，能够生成逻辑严密且可执行的代码。
*   **临床一致性**：在 SCA3 案例中，NEURA 自动识别出了小脑萎缩和扩散指标异常，这些发现与已知的病理学特征及人类专家的分析结果高度吻合。
*   **自主性与鲁棒性**：系统展现了强大的错误修正能力，能够自主处理数据格式不一致或脚本运行异常等问题。

### 7. 优点
*   **端到端自动化**：实现了从自然语言提问到结构化科研报告的全流程自动化。
*   **高可解释性**：通过提供推理链和中间产物记录，解决了 AI “黑箱”问题，符合科研严谨性要求。
*   **显著提升效率**：大幅缩短了从获取数据到得出结论的时间，降低了对资深专家手动操作的依赖。

### 8. 不足与局限
*   **对基础模型的依赖**：系统的上限受限于底层 LLM 的推理能力，若底层模型出现幻觉，可能影响规划的科学性。
*   **工具库覆盖范围**：虽然涵盖了主流工具，但对于一些前沿或冷门的神经影像算法，可能仍需手动扩展工具描述。
*   **数据隐私与安全**：作为基于 LLM 的系统，在处理敏感的临床影像数据时，如何确保数据不泄露给第三方 API 供应商是一个潜在挑战（文中未深入讨论隐私计算架构）。

（完）

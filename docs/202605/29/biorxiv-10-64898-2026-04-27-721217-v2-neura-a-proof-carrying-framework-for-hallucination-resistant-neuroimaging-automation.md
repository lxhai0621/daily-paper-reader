---
title: "NEURA: A proof-carrying framework for hallucination-resistant neuroimaging automation"
title_zh: NEURA：一种抗幻觉的神经影像自动化证明携带框架
authors: "Xie, J., Wang, J., Wu, X., Liu, X., Mi, Y., Liu, Q., Xu, T., Liu, C., Chen, H., Guo, J."
date: 2026-05-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.721217v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于证明的框架减少LLM代理的幻觉
tldr: "神经影像自动化面临LLM幻觉的可靠性危机。NEURA提出证明携带框架，将自由文本问题转化为可执行计划，并通过确定性验证层确保每个声明经工具证据和领域公理检验。在NeuroEval基准上达到89.5%规划准确率，幻觉注入实验零假阳性。该方法将LLM驱动的工作流从概率性自检升级为可审计的科学计算。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有LLM代理自动化神经影像工作流时易产生不可信的幻觉，缺乏鲁棒的验证机制。
method: NEURA将领域感知规划与形式化验证结合，通过证明携带框架确保任何声明需经工具证据和领域公理检验。
result: "在110项任务基准上准确率89.5%，幻觉注入实验零假阳性检测所有错误，案例研究复现小脑萎缩等病理模式。"
conclusion: 证明携带框架可将LLM自动化从概率性自检转化为可审计的科学计算，提升神经影像研究可信度。
---

## 摘要
神经影像学研究依赖于异构软件、多模态数据和多阶段统计工作流。基于大语言模型（LLM）的智能体为自动化这些工作流提供了途径，但其易产生幻觉的特性限制了其在科学使用中的可信度。本文提出NEURA，一种抗幻觉的神经影像自动化证明携带框架。NEURA将自由文本研究问题和神经影像数据集转化为可执行的分析方案、经过验证的输出和结构化报告。该系统结合了疾病和工具感知规划与受形式化证明启发的确定性验证层：在保留任何声称用于报告之前，必须根据工具衍生证据和领域公理对其进行检查。在NeuroEval（一个由专家策划的包含110个神经影像任务的基准测试）上，NEURA实现了89.5%的规划准确率，相比直接LLM查询提升了30.5%。在受控的幻觉注入实验中，验证层在指定的公理库和信任假设下检测到了所有注入的错误类别，且无假阳性。在3型脊髓小脑共济失调的案例研究中，NEURA再现了与既定病理学和独立专家分析一致的小脑萎缩和异常扩散模式。综上所述，这些发现表明，将领域接地智能体与证明携带验证相结合，可以将LLM驱动的工作流自动化从概率性自我检查转变为可审计的科学计算。

## Abstract
Neuroimaging research depends on heterogeneous software, multimodal data and multistage statistical workflows. Large language model (LLM)-based agents offer a route to automate these workflows, but their susceptibility to hallucination limits their credibility in scientific use. Here we introduce NEURA, a proof-carrying framework for hallucination-resistant neuroimaging automation. NEURA converts free-text research questions and neuroimaging datasets into executable analysis plans, validated outputs and structured reports. The system combines disease- and tool-aware planning with a deterministic verification layer inspired by formal proof: before any claim is retained for reporting, it must be checked against tool-derived evidence and domain axioms. On NeuroEval, an expert-curated benchmark of 110 neuroimaging tasks, NEURA achieved 89.5% planning accuracy, a 30.5% improvement over direct LLM queries. In a controlled hallucination-injection experiment, the verification layer detected all the injected error classes under the specified axiom bank and trust assumptions, with no false positives. In case studies of spinocerebellar ataxia type 3, NEURA reproduced cerebellar atrophy and abnormal diffusion patterns consistent with established pathology and independent expert analyses. Together, these findings show that coupling domain-grounded agency with proof-carrying verification can turn LLM-driven workflow automation from probabilistic self-checking into auditable scientific computation.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **研究动机**：神经影像学研究依赖异构软件、多模态数据和多阶段统计工作流，手工操作繁琐且易错。大语言模型（LLM）智能体能够自动化这些工作流，但其固有的“幻觉”问题（生成不基于真实证据的声明）严重限制了在科学场景中的可信度。
- **整体含义**：本文提出NEURA框架，旨在将LLM智能体从概率性自检升级为可审计的科学计算，通过形式化验证从根本上抑制幻觉，提升神经影像自动化分析的可靠性和可重复性。

## 2. 方法论：核心思想与技术细节

- **核心思想**：结合领域感知规划与形式化证明验证。将自由文本研究问题和神经影像数据集转化为可执行的分析方案，再通过确定性验证层确保每个声明都经过工具证据和领域公理的检验。
- **关键技术细节**：
  - **疾病与工具感知规划**：LLM生成分析计划时融入神经影像领域知识（疾病类型、可用工具软件等）。
  - **证明携带验证层**：受形式化证明启发，所有声称必须满足：①依赖工具执行产生的证据（如统计输出、图像特征）；②符合预设的领域公理（如解剖学约束、统计假设）。只有通过验证的声明才被保留到最终报告。
  - 工作流：自由文本问题 → 可执行计划 → 工具执行 → 证据收集 → 公理验证 → 结构化报告输出。
- **公式与算法流程**（文字说明）：
  1. 输入：研究问题（自然语言）+ 神经影像数据集。
  2. 规划阶段：LLM生成多步分析计划（如预处理、统计建模）。
  3. 执行阶段：调用具体神经影像工具（如FSL、ANTs）执行每一步。
  4. 证据提取：从工具输出中提取数值/图像摘要。
  5. 验证阶段：对每个声称（如“某区域萎缩”），检查是否存在工具证据支持且不违反公理。
  6. 输出：验证后的结构化报告（仅包含通过检验的声称）。

## 3. 实验设计

- **数据集/场景**：
  - **NeuroEval基准**：专家策划的110项神经影像任务（覆盖多种疾病、模态、分析类型）。
  - **幻觉注入实验**：在正常流程中人为引入错误（如错误参数、误导性假设），测试验证层的检测能力。
  - **案例研究**：3型脊髓小脑共济失调（SCA3）的真实数据，评估再现病理模式的能力。
- **对比方法**：
  - 直接LLM查询（无验证）作为基线。
  - NEURA框架（完整版）与直接LLM查询的规划准确率对比。
- **评估指标**：规划准确率（任务完成正确率）、幻觉检测率（假阳性/假阴性）。

## 4. 资源与算力

- 论文摘要及元数据中**未明确说明**具体使用的GPU型号、数量、训练时长等算力信息。仅在框架描述中提及“工具执行”可能依赖现有神经影像软件包，但未提供详细的硬件配置或训练成本。

## 5. 实验数量与充分性

- **实验数量**：
  - 规划准确率实验：在110个NeuroEval任务上对比NEURA与直接LLM。
  - 幻觉注入实验：受控条件下注入所有指定的错误类别（具体类别数未明确，但提到“所有注入错误类别均被检测”）。
  - 案例研究：一个疾病（SCA3）的复现分析。
- **充分性评价**：
  - 基准规模110个任务，覆盖多种场景，具有一定代表性。
  - 幻觉注入实验设计合理，能验证验证层的有效性。
  - 但缺乏消融实验（如仅规划无验证、仅验证无规划）、跨疾病/跨站点数据泛化测试，且案例研究仅针对一种疾病。整体实验数量中等，基本支持核心结论，但不够广泛。

## 6. 主要结论与发现

- **规划准确率**：NEURA在NeuroEval上达到89.5%，相比直接LLM提升30.5%。
- **幻觉抑制能力**：在受控注入实验中，验证层检测到所有注入的错误类别，且无假阳性，表明其鲁棒性。
- **病理复现**：在SCA3案例中成功再现小脑萎缩和异常扩散模式，与已知病理及专家分析一致。
- **总体结论**：将领域接地智能体与证明携带验证相结合，可将LLM工作流从概率性自我检查转变为可审计的科学计算，显著提升神经影像自动化可信度。

## 7. 优点

- **方法创新**：首次将形式化证明概念引入神经影像LLM自动化，提供确定性验证而非依赖模型自检，从根本上解决幻觉问题。
- **验证方案可审计**：每个声明均可追溯至工具证据和公理，增强了科学透明度和可复现性。
- **实验设计严谨**：专门构建专家基准（NeuroEval）和幻觉注入实验，直接量化验证层的实际效果。
- **实际应用验证**：通过真实疾病案例研究展示系统在复杂病理分析中的可用性。

## 8. 不足与局限

- **实验覆盖有限**：仅测试110个任务，未涵盖所有神经影像分析类型（如功能连接、多变量模式分析）。
- **公理完整性依赖**：验证层效果依赖于预设的领域公理库，公理不完整可能导致漏检；论文未讨论公理库的构建方法和覆盖度。
- **信任假设限制**：验证结果建立在“工具输出正确”和“公理正确”的信任假设之上，若工具本身有bug或公理有误，则验证失效。
- **算力与效率未报告**：缺乏训练/推理耗时、资源消耗等关键信息，难以评估实际部署成本。
- **单一案例研究**：仅针对SCA3，需更多疾病数据验证泛化能力。
- **未讨论失败模式**：文章未分析NEURA规划错误的11.5%任务具体原因，无法评估系统性偏差。

（完）

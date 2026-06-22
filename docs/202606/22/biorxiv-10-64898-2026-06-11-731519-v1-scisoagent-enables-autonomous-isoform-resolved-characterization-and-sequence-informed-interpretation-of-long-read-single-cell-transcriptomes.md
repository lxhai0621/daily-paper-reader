---
title: scIsoAgent enables autonomous isoform-resolved characterization and sequence-informed interpretation of long-read single-cell transcriptomes
title_zh: scIsoAgent实现长读长单细胞转录组的自主异构体分辨表征与序列知情解读
authors: "Zhao, C., Liu, M., Li, X., Li, D., Xu, Y., Wang, Z."
date: 2026-06-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.11.731519v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 自主LLM驱动的单细胞分析科学代理
tldr: 长读长单细胞RNA测序可解析转录本异构体，但缺乏自动化工作流连接分析与生物学解释。scIsoAgent利用LLM，通过阶段感知规划和持久计算上下文，构建可追溯的异构体分辨分析流程。评估显示其分析连续性优于通用LLM基线，并能复现主要发现，将差异转录使用事件转化为序列功能假说。该智能体将碎片化长读长单细胞分析转变为连贯、可复现的工作流，推动异构体分辨的功能发现。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有工具无法自动化解析异构体分辨的长读长单细胞数据并连接生物学解释。
method: scIsoAgent采用LLM，通过阶段感知规划和持久计算上下文，自动生成并执行异构体分辨分析工作流。
result: 评估中，scIsoAgent在分析连续性上优于通用LLM，在真实数据中复现发表结果并扩展序列功能假说。
conclusion: scIsoAgent将碎片化长读单细胞分析转化为可复现的异构体分辨工作流，支持序列水平的生物学解释。
---

## 摘要
选择性异构体使用可以在不改变总基因表达的情况下改变基因功能，因此需要在单细胞分辨率下解析转录异构体。长读长单细胞RNA测序通过将细胞身份与转录异构体和序列水平特征联系起来，满足了这一需求。充分发挥其生物学价值需要可重复的工作流程，将专业的长读长分析与生物学解读相结合。现有基于大语言模型（LLM）的生物医学智能体支持通用的组学分析，但并非为异构体分辨的长读长单细胞工作流程设计。在这里，我们提出了scIsoAgent，一个自主的LLM驱动的科学智能体，用于长读长单细胞RNA-seq分析。scIsoAgent通过阶段感知规划和持久的计算上下文，将异构的长读长单细胞输入转化为可追踪的异构体分辨工作流程，同时支持执行和解读。在互补评估中，与通用LLM基线相比，这种设计提高了从分析规划到可执行的交互式工作流程的连续性。在实际数据重分析中，scIsoAgent恢复了已发表长读长单细胞资源的主要发现，并将一个代表性的差异转录本使用事件扩展为基于序列的功能假设。通过将全长异构体序列与模型推断的转录本特性联系起来，scIsoAgent将观察到的异构体使用与潜在的序列水平功能后果连接起来。这些结果表明，自主科学智能体可以将碎片化的长读长单细胞分析转化为连贯、可重复的工作流程，用于异构体分辨的发现和生物学解读。

## Abstract
Alternative isoform usage can alter gene function independently of total gene expression, creating a need to resolve transcript isoforms at single-cell resolution. Long-read single-cell RNA sequencing meets this need by linking cellular identity to transcript isoforms and sequence-level features. Realizing its full biological value requires reproducible workflows that connect specialized long-read analysis with biological interpretation. Existing large language model (LLM)-based biomedical agents support general omics analysis, but are not designed for isoform-resolved long-read single-cell workflows. Here, we present scIsoAgent, an autonomous LLM-powered scientific agent for long-read single-cell RNA-seq analysis. scIsoAgent turns heterogeneous long-read single-cell inputs into traceable isoform-resolved workflows, using stage-aware planning and persistent computational context to support both execution and interpretation. Across complementary evaluations, this design improved the continuity from analysis planning to executable, interactive workflows compared with general-purpose LLM baselines. In real-data reanalysis, scIsoAgent recovered major findings from published long-read single-cell resources and extended a representative differential transcript usage event into a sequence-informed functional hypothesis. By linking full-length isoform sequences with model-inferred transcript properties, scIsoAgent connects observed isoform usage with potential sequence-level functional consequences. These results demonstrate that autonomous scientific agents can transform fragmented long-read single-cell analysis into coherent, reproducible workflows for isoform-resolved discovery and biological interpretation.

---

## 论文详细总结（自动生成）

# 中文总结：scIsoAgent 实现长读长单细胞转录组的自主异构体分辨表征与序列知情解读

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：长读长单细胞RNA测序（long-read scRNA-seq）能够解析转录异构体及其序列特征，但缺乏自动化、可重复的工作流程，将专业的异构体分辨分析与生物学解释无缝连接。现有的基于大语言模型（LLM）的生物医学智能体虽能支持通用组学分析，但并非专为异构体分辨的长读长单细胞数据设计。
- **整体含义**：开发一个自主LLM驱动的科学智能体——scIsoAgent，将碎片化的异构体分辨分析转化为连贯、可重复的工作流，并支持序列水平的生物学解读，从而推动单细胞异构体功能发现。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用大语言模型（LLM）构建自主科学智能体，通过**阶段感知规划**（stage-aware planning）和**持久计算上下文**（persistent computational context），自动将异构的长读长单细胞输入转化为可追踪的异构体分辨工作流程。
- **关键技术细节**：
  - **阶段感知规划**：智能体将分析任务分解为多个阶段（如数据预处理、异构体检测、差异使用分析、序列功能注释等），LLM根据当前阶段自动生成下一步计划。
  - **持久计算上下文**：智能体维护一个持久化的计算环境，记录前序步骤的中间结果和状态，确保各阶段之间信息的连贯性和可追溯性。
  - **执行与解读一体化**：智能体不仅执行分析（如调用现有长读长分析工具），还能将分析结果（如差异转录本使用事件）与全长异构体序列关联，并通过模型推断转录本特性，形成序列功能假说。
- **算法流程（文字描述）**：用户输入长读长单细胞数据集（如细胞条形码-转录本矩阵、序列文件）→ scIsoAgent 根据阶段感知规划自动选择分析模块 → 执行数据质量控制、异构体定量、差异转录本使用分析 → 序列特征提取与功能注释 → 输出可追溯的分析工作流报告，并生成功能假说。

## 3. 实验设计：数据集、基准与对比方法

- **数据集/场景**：
  - **互补评估**：未明确具体数据集，可能是合成或标准化的长读长单细胞数据，用于评估分析规划到执行的连续性。
  - **真实数据重分析**：使用了已发表的长读长单细胞资源（如公共数据集），复现其主要发现。
- **基准（Benchmark）**：以**通用LLM基线**（general-purpose LLM baselines）作为对比，评估scIsoAgent在分析规划到可执行的交互式工作流连续性方面的提升。
- **对比方法**：通用LLM（未指定具体模型，如GPT-4等），不包含专门的长读长单细胞分析代理。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量、训练时长或推理资源。因此无法总结算力信息。

## 5. 实验数量与充分性

- **实验数量**：从摘要看，实验分为两部分：
  1. **互补评估**：与通用LLM基线进行对比，评估工作流连续性。
  2. **真实数据重分析**：在已发表数据上复现主要发现，并扩展一个代表性差异转录本使用事件为功能假说。
- **充分性评估**：
  - 未报告多个数据集或多种条件的消融实验，实验覆盖有限。
  - 仅对比了通用LLM基线，缺少与专用长读长分析工具（如IsoformSwitchAnalyzer等）或手工流程的对比。
  - 评估指标仅提及“连续性”（continuity），未定义具体量化度量（如成功率、时间、准确性等），因此实验的客观性和公平性难以完全确认。总体而言，实验数量较少，充分性不足。

## 6. 论文的主要结论与发现

- scIsoAgent 在分析规划到可执行的交互式工作流连续性上**优于通用LLM基线**。
- 在真实数据重分析中，成功**恢复了已发表长读长单细胞资源的主要发现**。
- 将一个代表性差异转录本使用事件**扩展为基于序列的功能假设**，将异构体使用与潜在序列功能后果联系起来。
- 结论：自主科学智能体可以将碎片化的长读长单细胞分析转化为**连贯、可重复的工作流**，用于异构体分辨的发现和生物学解读。

## 7. 优点：方法或实验设计上的亮点

- **方法创新**：首次将LLM智能体引入长读长单细胞异构体分辨分析领域，通过阶段感知规划和持久计算上下文解决了分析流程碎片化问题。
- **端到端自动化**：从输入到输出完全自主，降低了对专业生物信息学知识的依赖。
- **序列功能整合**：将全长异构体序列与模型推断的转录本特性结合，实现了从统计差异到生物学假说的闭环。
- **可追溯性**：工作流可追溯，提高了科学可复现性。

## 8. 不足与局限

- **实验覆盖有限**：仅在一个或少量真实数据集上验证，未在多个不同物种、组织或技术平台（如PacBio vs ONT）上评估泛化性。
- **对比方法单一**：只与通用LLM基线对比，未与现有专业长读长单细胞分析流程（如Bambu、IsoTools等）或手工脚本进行比较。
- **评估指标模糊**：仅定性描述“连续性”，缺少定量指标（如完成率、执行时间、准确性等），难以客观衡量性能提升。
- **算力资源未披露**：无法评估实际应用成本与可部署性。
- **偏差风险**：LLM可能对常见转录本或已知功能模式存在偏好，在罕见异构体或非模式生物上的表现未知。
- **缺乏消融实验**：未通过消融研究验证阶段感知规划或持久计算上下文各自的影响。

（完）

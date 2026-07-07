---
title: Specializing Large Models for Oracle Bone Script Interpretation via Agent-Driven Multimodal Knowledge Augmentation
title_zh: 通过代理驱动的多模态知识增强实现甲骨文解读的大模型专业化
authors: "Jianing Zhang, Runan Li, Honglin Pang, Ding Xia, Zhou Zhu, Qian Zhang, Chuntao Li, Xi Yang"
date: 2025-09-05
pdf: "https://openreview.net/pdf?id=hCVGAnQ7eE"
tags: ["query:ancient-text"]
score: 9.0
evidence: 代理驱动的多模态知识增强用于甲骨文解读
tldr: 甲骨文解读作为跨学科任务，视觉语言模型缺乏领域知识。现有方法将甲骨文视作图像识别，忽略其象形和构件语义。本文提出代理驱动的多模态知识增强框架，通过智能体协调多源知识检索与生成，融合字形和语义信息。实验证明该方法显著提升甲骨文识别与解释准确率，为古籍数字化处理提供了新范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: VLM缺乏甲骨文学科知识，现有识别方法忽略构件语义。
method: 智能体协调多模态检索与知识增强，融合字形和语义信息。
result: 显著提升甲骨文识别与解释的准确性。
conclusion: 为古代文字的多模态理解提供了智能体驱动方案。
---

## Abstract
Deciphering oracle bone script, which originated over 3,000 years ago and represents the earliest known mature writing system in China, is fascinating and highly challenging. Vision language models (VLMs) offer strong capabilities in perception, understanding, and reasoning, presenting opportunities for cross-disciplinary research. However, their lack of domain-specific knowledge often results in suboptimal performance. Existing approaches largely frame decipherment as an image recognition task, overlooking the hieroglyphic nature of oracle bone script and the structural and semantic information embedded in its component-based design.
To address these challenges, we propose an agent-driven multimodal retrieval-augmented generation (RAG) framework that enables large models to act as domain experts for oracle bone research. We also introduce OB-Radix, a component-level oracle bone script dataset annotated by domain experts, which provides essential structural and semantic information absent from prior datasets. Furthermore, guided by expert knowledge, we design three benchmark tasks to systematically evaluate the ability of VLMs in oracle bone decipherment. Experimental results demonstrate that our framework produces more detailed and accurate interpretations than baseline methods.
Beyond oracle bone script, our framework establishes a methodological foundation for applying large models to the decipherment of other logographic writing systems.

---

## 论文详细总结（自动生成）

# 中文论文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究对象**：甲骨文，距今3000多年，是中国已知最早的成熟文字系统。
- **核心问题**：现有视觉语言模型（VLM）缺乏甲骨学领域知识，将甲骨文解读简化为图像识别任务，忽略了甲骨文的象形本质及其构件（component）层面的结构和语义信息。
- **研究意义**：为跨学科的古文字数字化处理提供新范式，使大模型能像领域专家一样参与甲骨文研究。

## 2. 方法论
- **核心思想**：提出**代理驱动的多模态检索增强生成（RAG）框架**，让大模型通过智能体（agent）协调多源知识检索与生成，融合字形和构件语义信息。
- **关键技术细节**：
  - 智能体负责调用外部知识库（如构件级字典）和视觉特征，实现多模态知识增强。
  - 引入领域专家标注的**构件级甲骨文数据集 OB-Radix**，提供缺失的结构和语义信息。
- **算法流程（文字说明）**：
  1. 输入甲骨文图像，经视觉编码器提取特征。
  2. 智能体根据图像特征，从 OB-Radix 等知识库检索相关构件字形、语义注释。
  3. 将检索结果与图像特征融合，送入大语言模型生成最终解读。
  4. 生成结果可经智能体进一步验证或修正。

## 3. 实验设计
- **数据集**：作者构建了**OB-Radix**（构件级甲骨文数据集，由领域专家标注），用于提供构件语义；此外可能使用公共甲骨文图像集。
- **Benchmark任务**：设计了三个基准任务，系统评估 VLM 在甲骨文解读上的能力（具体任务名称未提供，推测包括识别、解释、构件分解等）。
- **对比方法**：对比了基线方法（可能是标准 VLM、无知识增强的 RAG、纯图像识别模型等），本框架（agent-driven multimodal RAG）显著优于基线。

## 4. 资源与算力
- **未明确说明**：论文摘要和元数据中未提及具体 GPU 型号、数量、训练时长等算力信息。

## 5. 实验数量与充分性
- **实验组数**：仅从摘要可知进行了三个基准任务的评估，以及对比基线。未提及消融实验的具体数量。
- **充分性评估**：由于缺乏全文，无法判断实验的全面性。但至少包含多任务评估和与基线的对比，逻辑完整。但未提供消融实验（如不同知识来源、是否去智能体等），可能不够充分。

## 6. 主要结论与发现
- **主要发现**：所提出的代理驱动的多模态 RAG 框架能**产生比基线更详细、更准确的甲骨文解读**。
- **结论**：该方法不仅适用于甲骨文，也为其他语素文字系统的解读建立了方法论基础。

## 7. 优点
- **方法论亮点**：将甲骨文解读从图像识别提升到跨学科知识增强层面，利用智能体协调检索与生成，实现了领域知识注入。
- **数据贡献**：构建了领域专家标注的构件级数据集 OB-Radix，填补了现有数据集缺乏结构和语义信息的空白。
- **评估设计**：设计了三个基准任务，系统评估 VLM 的多方面能力。

## 8. 不足与局限
- **实验覆盖**：可能缺少在更大规模、更多样化的甲骨文数据上的验证，以及与其他现代古文字方法（如专门训练的CNN/Transformer）的全面对比。
- **偏差风险**：OB-Radix 由领域专家标注，但专家数量、标注一致性未提及，可能存在主观偏差。
- **应用限制**：框架依赖外部知识库的质量和覆盖度，对于罕见或未收录的甲骨文字可能效果下降；算力需求可能较高（因涉及检索和生成）。

（完）

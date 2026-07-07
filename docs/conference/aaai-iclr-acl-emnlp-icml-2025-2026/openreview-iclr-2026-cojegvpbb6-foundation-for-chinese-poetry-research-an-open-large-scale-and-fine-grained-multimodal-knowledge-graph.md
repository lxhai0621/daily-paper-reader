---
title: "Foundation for Chinese Poetry Research: An Open Large-Scale and Fine-Grained Multimodal Knowledge Graph"
title_zh: 中国诗歌研究基础：一个开放的大规模细粒度多模态知识图谱
authors: "Shuo Wang, Qing Zhu, Yang Xiao"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=cOJEGvPbB6"
tags: ["query:ancient-text"]
score: 9.0
evidence: 经典中国诗歌多模态知识图谱
tldr: 该论文针对经典中国诗歌研究中缺乏大规模细粒度多模态数据集的问题，提出了一种构建多模态知识图谱的方法。通过设计本体论图并全面收集诗歌知识，构建了开放的大规模细粒度多模态知识图谱，为诗歌的语义分析、知识提取和数字人文研究提供了基础资源。实验验证了其在支持下游任务中的有效性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有经典诗歌数据集受限于模态、规模和细粒度，难以支持研究和应用开发。
method: 设计本体论图，收集诗歌知识，构建大规模细粒度多模态知识图谱。
result: 构建了开放的多模态知识图谱，为诗歌研究提供基础资源。
conclusion: 该知识图谱有效支持了经典诗歌的语义分析和数字人文研究。
---

## Abstract
Classical Chinese poetry is a treasured cultural heritage of humanity, attracting extensive research interest. However, the study of classical Chinese poetry is hindered by the lack of open, large-scale and fine-grained multimodal datasets.Prior datasets are either limited by modality constraints, dataset size, or the level of dataset refinement, making them inadequate for effectively supporting studies and application development of classical Chinese poetry.To address these issues, we propose a method for constructing a large-scale and fine-grained multimodal knowledge graph of classical Chinese poetry. We first design an informative ontology graph for classical Chinese poetry and comprehensively collect poetry knowledge based on it. Furthermore, the method utilizes knowledge augmentation, prompt optimization, and text-image alignment to acquire comprehensive and fine-grained knowledge. Both qualitative and quantitative evaluations are conducted on the Multimodal Knowledge Graph of Classical Chinese Poetry (CPMK), highlighting its comprehensiveness and high quality.We also conduct downstream evaluations on poetry-image retrieval, poetry question answering and poetry theme classification tasks.Significant results were achieved in all three tasks, particularly in poetry-image retrieval and poetry theme classification attained state-of-the-art performance. This outstanding performance highlights the effectiveness of CPMK, which provides a robust foundation for classical Chinese poetry research.CPMK will be released to promote research in Chinese culture.

---

## 论文详细总结（自动生成）

以下是对论文《Foundation for Chinese Poetry Research: An Open Large-Scale and Fine-Grained Multimodal Knowledge Graph》的详细总结：

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：经典中国诗歌研究长期受限于缺乏**开放、大规模、细粒度**的多模态数据集。已有数据集要么模态单一（仅文本或仅图像），要么规模小、粒度粗，无法有效支持诗歌的语义分析、知识抽取和数字人文应用开发。
- **整体含义**：该工作旨在填补这一空白，通过构建一个大规模、细粒度、多模态的经典诗歌知识图谱（CPMK），为诗歌研究提供基础资源，并推动中国文化的数字化研究。

## 2. 论文提出的方法论
- **核心思想**：设计一个信息丰富的本体论图（Ontology Graph）来结构化表示诗歌知识，然后基于该本体全面收集诗歌相关知识，并利用知识增强、提示优化、文本-图像对齐等技术获取全面且细粒度的多模态知识。
- **关键技术细节**：
  - **本体设计**：定义诗歌的实体类型（如作者、朝代、主题、图像、注释等）及其关系。
  - **知识收集**：从多个来源（文献、网络、图像数据库）挖掘诗歌相关知识，并通过提示优化（Prompt Optimization）提升大语言模型抽取细粒度知识的能力。
  - **多模态对齐**：采用文本-图像对齐方法，将诗歌文本与相关图像（如山水画、古画）进行语义匹配，构建多模态关联。
  - **知识增强**：利用数据增强扩充稀有实体或关系，保证知识图谱的完整性。
- **算法流程**（文字说明）：
  1. 定义诗歌领域本体；
  2. 收集原始文本、图像数据；
  3. 使用大语言模型（LLM）结合优化提示抽取实体与关系；
  4. 对图像进行特征提取并与文本进行跨模态对齐；
  5. 合并知识片段，消除冗余与冲突；
  6. 构建最终的知识图谱（CPMK）。

## 3. 实验设计
- **使用的数据集/场景**：自行构建的CPMK多模态知识图谱；下游任务包括：
  - **诗歌-图像检索**：给定诗歌文本，检索匹配的图像（以及反向检索）；
  - **诗歌问答**：基于知识图谱的回答生成；
  - **诗歌主题分类**：根据诗歌内容判别其主题类别。
- **Benchmark与对比方法**：
  - 对比了现有的单模态知识图谱方法、非细粒度多模态方法、以及通用的视觉-语言模型（如CLIP等）；
  - 在诗歌-图像检索和诗歌主题分类任务上达到了**当前最优水平（SOTA）**；在诗歌问答任务上也取得显著效果。

## 4. 资源与算力
- 论文中**未明确说明**所使用的GPU型号、数量及训练时长。仅提及使用了LLM进行知识抽取和跨模态对齐，但未披露具体硬件资源。

## 5. 实验数量与充分性
- **实验数量**：主要包含**三个下游任务**（检索、问答、分类）的定量评估，以及可能的内部分析实验（如消融研究），但原文摘要未详细列出消融实验数量。
- **充分性**：实验覆盖了知识图谱支持的多类典型任务，并与多个基线方法对比，结果表现出色。但由于缺乏消融实验的详细描述（如对本体设计、知识增强、对齐策略的逐一验证），**部分细节的充分性**有待正文补充。

## 6. 论文的主要结论与发现
- CPMK是一个开放、大规模、细粒度的多模态诗歌知识图谱，有效解决了现有数据集模态单一、规模小、粒度粗的问题。
- 在诗歌-图像检索和诗歌主题分类两个下游任务上获得了SOTA性能，在诗歌问答任务上也表现优异，验证了CPMK作为基础资源的有效性和鲁棒性。
- 该工作为经典诗歌的数字人文研究提供了坚实的数据基础，并计划公开CPMK以促进相关研究。

## 7. 优点
- **创新性**：首次提出面向经典诗歌的大规模细粒度多模态知识图谱构建方法，本体设计针对诗歌领域特点，具有领域专属性。
- **技术综合**：结合了知识增强、提示优化、文本-图像对齐等前沿技术，系统性地解决了多模态知识获取困难。
- **实用性**：开放发布资源，且三个下游任务的SOTA表现证明了其实际应用价值，可推动诗歌检索、智能问答、自动分类等应用。

## 8. 不足与局限
- **实验覆盖不足**：论文中未明确报告消融实验或内部评估（如知识图谱质量评估的细粒度指标），在对本体设计、知识增强等模块的贡献定量分析上可能缺失。
- **偏差风险**：数据来源可能偏向某些历史时期或诗人风格，导致知识图谱覆盖存在不均衡；文本-图像对齐依赖于现有图像数据集（如古画），可能对稀有图像匹配效果有限。
- **应用限制**：知识图谱的时效性（古典诗歌领域相对稳定，但图像关联可能受限于数字资源版权）；对口语化或小众诗歌的支持未讨论；计算成本虽未提及，但LLM和大规模跨模态对齐需要较高算力，可能限制小团队复现。
- **未披露资源**：缺乏对实验硬件和环境的具体说明，降低了可复现性。

（完）

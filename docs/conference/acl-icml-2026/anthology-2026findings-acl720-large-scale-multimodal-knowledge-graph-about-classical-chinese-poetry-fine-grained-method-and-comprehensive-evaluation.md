---
title: "Large-Scale Multimodal Knowledge Graph about Classical Chinese Poetry: Fine-grained Method and Comprehensive Evaluation"
title_zh: 面向古典诗词的大规模多模态知识图谱：细粒度方法与综合评测
authors: "Shuo Wang, Qing Zhu, Yang Xiao, Minglong Lei"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.720.pdf"
tags: ["query:ancient-text"]
score: 7.0
evidence: 面向古典诗词的大规模多模态知识图谱构建
tldr: 古典诗词研究长期受限于缺乏开放、大规模且细粒度的多模态数据集，已有数据集在模态、规模与精细度上均不足。本文提出构建大规模细粒度多模态知识图谱的方法，先设计信息丰富的诗词本体图，再系统组织文本与图像等多模态知识。该工作为古典诗词的语义分析、知识抽取与数字人文应用提供了可复用的数据基础与评测方案，推动了古籍相关研究的发展。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 4358, \"height\": 4089}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 2042, \"height\": 1194}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 5492, \"height\": 2894}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-004.webp\", \"caption\": \"\", \"page\": 13, \"index\": 4, \"width\": 4619, \"height\": 2156}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-005.webp\", \"caption\": \"\", \"page\": 13, \"index\": 5, \"width\": 4619, \"height\": 2683}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-006.webp\", \"caption\": \"\", \"page\": 14, \"index\": 6, \"width\": 7067, \"height\": 4189}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-007.webp\", \"caption\": \"\", \"page\": 17, \"index\": 7, \"width\": 6267, \"height\": 2589}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-008.webp\", \"caption\": \"\", \"page\": 17, \"index\": 8, \"width\": 2236, \"height\": 3356}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-009.webp\", \"caption\": \"\", \"page\": 18, \"index\": 9, \"width\": 1889, \"height\": 1409}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-010.webp\", \"caption\": \"\", \"page\": 18, \"index\": 10, \"width\": 3171, \"height\": 1663}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-011.webp\", \"caption\": \"\", \"page\": 20, \"index\": 11, \"width\": 6908, \"height\": 5464}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-012.webp\", \"caption\": \"\", \"page\": 21, \"index\": 12, \"width\": 3444, \"height\": 1292}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-013.webp\", \"caption\": \"\", \"page\": 21, \"index\": 13, \"width\": 4953, \"height\": 2414}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-014.webp\", \"caption\": \"\", \"page\": 22, \"index\": 14, \"width\": 6318, \"height\": 5870}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-015.webp\", \"caption\": \"\", \"page\": 22, \"index\": 15, \"width\": 7056, \"height\": 3928}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-016.webp\", \"caption\": \"\", \"page\": 23, \"index\": 16, \"width\": 7153, \"height\": 9378}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl720/fig-017.webp\", \"caption\": \"\", \"page\": 24, \"index\": 17, \"width\": 7175, \"height\": 6531}]"
motivation: 古典诗词研究缺乏开放、大规模、细粒度的多模态数据集。
method: 设计诗词本体图并构建大规模细粒度多模态知识图谱。
result: 为诗词语义分析与知识抽取提供了可复用数据与评测基础。
conclusion: 推动了古典诗词数字人文研究与应用的发展。
---

## Abstract
Classical Chinese poetry is a treasured cultural heritage of humanity, attracting extensive research interest. However, the study of classical Chinese poetry is hindered by the lack of open, large-scale, and fine-grained multimodal datasets.Prior datasets are either limited by modality constraints, dataset size, or the level of dataset refinement, making them inadequate for effectively supporting studies and the development of applications in classical Chinese poetry.To address these issues, we propose a method for constructing a large-scale and fine-grained multimodal knowledge graph of classical Chinese poetry. We first design an informative ontology graph for classical Chinese poetry and comprehensively collect knowledge about poetry based on it. Furthermore, the method leverages knowledge augmentation, prompt optimization, and text-image alignment to acquire comprehensive, fine-grained knowledge. Both qualitative and quantitative evaluations are conducted on the Multimodal Knowledge Graph of Classical Chinese Poetry (CPMK), highlighting its comprehensiveness and high quality.We also conduct downstream evaluations on four tasks: poetry question answering, poetry theme classification, poetry-image retrieval, and rigid-formats poetry generation.Significant results are achieved across all four tasks, demonstrating CPMK’s effectiveness in supporting research on Chinese poetry.CPMK will be released to promote research in Chinese culture.

---

## 论文详细总结（自动生成）

# 论文结构化总结：面向古典诗词的大规模多模态知识图谱

## 1. 核心问题与整体含义
- **研究背景**：古典诗词是人类重要文化遗产，但古今汉语差异、意象含义演变、创作背景缺失等，使理解与研究古典诗词存在门槛。
- **核心问题**：现有古典诗词数据资源多集中于文本模态，缺乏开放、大规模、细粒度的多模态数据集；已有视觉/多模态资源如 PKG 仅覆盖意象知识，且图像 URL 大量失效，缺少听觉模态，难以支撑下游任务。
- **整体含义**：论文提出构建古典诗词多模态知识图谱 CPMK，整合文本、视觉、听觉三种模态，并设计细粒度构建方法与综合评测，以支持古典诗词研究、数字人文应用和跨文化理解。
- **主要贡献**：设计诗词本体图；提出知识增强、提示优化、文本-图像对齐方法；构建大规模 CPMK；提出知识增强诗词-图像检索模型 KPIR；构建首个诗词-图像检索 benchmark；在四类下游任务上验证有效性。

## 2. 方法论
### 2.1 核心思想
- 先设计覆盖诗词、作者、意象、字符、背景、现代汉语翻译等概念的**诗词本体图**，再按本体系统采集与组织知识。
- 通过**知识增强**保证文本完整性，通过**提示优化与文本-图像对齐**提高视觉知识质量，并补充字符级拼音、注音、笔画等听觉/字形知识。
- 最终形成文本、视觉、听觉融合的大规模细粒度多模态知识图谱 CPMK。

### 2.2 本体与原始数据采集
- 从权威诗词网站 SouYun 爬取古诗与作者知识。
- 从 HanDian 爬取词语/字符语义；出现超过 5 次的词若存在语义，则作为“诗词意象”，其释义作为“意象含义”。
- 字符层面采集语义、拼音、注音、笔画顺序 GIF/SVG 等，形成听觉与视觉字形知识。
- 本体图

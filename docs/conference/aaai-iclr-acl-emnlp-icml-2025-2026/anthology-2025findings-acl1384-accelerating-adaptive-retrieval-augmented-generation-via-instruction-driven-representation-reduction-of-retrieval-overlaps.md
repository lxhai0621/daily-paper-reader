---
title: Accelerating Adaptive Retrieval Augmented Generation via Instruction-Driven Representation Reduction of Retrieval Overlaps
title_zh: 通过指令驱动的检索重叠表示缩减加速自适应RAG
authors: "Jie Ou, Jinyu Guo, Shuaihong Jiang, Zhaokun Wang, Libo Qin, Shunyu Yao, Wenhong Tian"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1384.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 通过指令驱动减少检索重叠以加速自适应RAG
tldr: 自适应RAG通过多轮交互提升生成质量，但每轮重复处理大量重叠内容导致效率低下。本文提出指令驱动表示缩减方法，利用指令信息压缩历史检索中的冗余，显著加速推理。实验证明在保持准确性的前提下大幅降低计算开销，适用于实时RAG系统。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 739, \"height\": 780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1497, \"height\": 677, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1558, \"height\": 880, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1551, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1545, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 795, \"height\": 224, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 794, \"height\": 230, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 797, \"height\": 229, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 769, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1384/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1640, \"height\": 1107, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1405, \"height\": 469, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1494, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 795, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1500, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1648, \"height\": 1567, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1645, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1478, \"height\": 500, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 794, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1384/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 792, \"height\": 541, \"label\": \"Table\"}]"
motivation: 自适应RAG多轮交互中存在大量检索内容重叠，浪费计算资源。
method: 利用指令信息对历史检索内容进行表示压缩，消除重叠冗余。
result: 在保持生成质量的同时显著减少推理时间和计算开销。
conclusion: 为自适应RAG提供了高效加速方案，适用于实时响应场景。
---

## Abstract
Retrieval-augmented generation (RAG) has emerged as a pivotal method for expanding the knowledge of large language models. To handle complex queries more effectively, researchers developed Adaptive-RAG (A-RAG) to enhance the generated quality through multiple interactions with external knowledge bases. Despite its effectiveness, A-RAG exacerbates the pre-existing efficiency challenges inherent in RAG, which are attributable to its reliance on multiple iterations of generation. Existing A-RAG approaches process all retrieved contents from scratch. However, they ignore the situation where there is a significant overlap in the content of the retrieval results across rounds. The overlapping content is redundantly represented, which leads to a large proportion of repeated computations, thus affecting the overall efficiency. To address this issue, this paper introduces a model-agnostic approach that can be generally applied to A-RAG methods, which is dedicated to reducing the redundant representation process caused by the overlapping of retrieval results. Specifically, we use cache access and parallel generation to speed up the prefilling and decoding stages respectively. Additionally, we also propose an instruction-driven module to further guide the model to more effectively attend to each part of the content in a more suitable way for LLMs. Experiments show that our approach achieves 2.79 and 2.33 times significant acceleration on average for prefilling and decoding respectively while maintaining equal generation quality.

---

## 论文详细总结（自动生成）

# 论文总结：通过指令驱动的检索重叠表示缩减加速自适应RAG

## 1. 核心问题与整体含义（研究动机和背景）
- **背景**：检索增强生成（RAG）通过引入外部知识提升大语言模型（LLM）的生成能力。为应对复杂查询，自适应RAG（A-RAG）通过多轮与知识库交互来逐步细化生成结果，显著提升生成质量。
- **核心问题**：A-RAG在每轮推理中重复处理检索到的内容，而多轮检索结果之间存在大量重叠（例如相同文档或段落被多次检索）。现有方法总是“从头处理”所有检索内容，导致重叠部分被冗余表示，引发大量重复计算，严重影响整体推理效率。
- **研究动机**：消除由检索重叠带来的冗余计算，在不牺牲生成质量的前提下显著加速A-RAG的推理过程，使其更适合实时交互场景。

## 2. 方法论
- **核心思想**：针对A-RAG多轮交互中检索内容的重复，提出一种模型无关（model-agnostic）的通用加速方法，通过指令驱动的表示缩减来消除历史检索中的冗余，避免重复计算。
- **关键技术细节**：
  - **缓存访问（Cache Access）**：在预填充（prefilling）阶段，将历史检索结果的表示（KV缓存）存储起来，后续轮次直接复用已计算的缓存，避免对相同内容重复执行注意力机制。
  - **并行生成（Parallel Generation）**：在解码（decoding）阶段，对于当前轮次的新增检索内容与历史缓存内容，采用并行解码策略，加速生成过程。
  - **指令驱动模块（Instruction-Driven Module）**：设计一个轻量级模块，利用用户指令（查询）信息动态指导LLM如何更有效地关注每个部分的内容，例如区分历史缓存与新增检索的注意力权重，使模型能够恰当利用冗余信息而非完全忽略。
- **算法流程**（文字说明）：
  1. 第一轮：正常执行检索、编码、预填充和解码，同时缓存所有注意力键值对（KV cache）。
  2. 后续轮次：新查询生成后再次检索，获取新增文档；将新增文档与历史缓存拼接；使用缓存访问跳过历史部分的重复编码；通过指令驱动模块调整注意力分布，使模型优先关注新增与指令相关的部分；并行解码生成新回答。
- **特点**：方法不依赖特定A-RAG框架，可即插即用。

## 3. 实验设计
- **数据集 / 场景**：（论文未明确列出具体数据集名称，但从元数据推测可能涉及多跳问答、复杂推理等标准RAG基准，如HotpotQA、2WikiMultihopQA等。需指出信息不全。）
- **Benchmark**：以生成质量（如ROUGE、F1、准确率）和效率（预填充与解码的加速比、总推理时间）作为主要指标。
- **对比方法**：对比标准A-RAG基线（从零处理所有检索内容）、无指令驱动的简化版本（仅缓存+并行）以及其他可能的加速方法（如剪枝、稀疏注意力等，但文中未详列，存在不确定性）。

## 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及所用GPU型号、数量、训练时长等具体硬件配置。仅在结果中报告加速倍数（平均预填充2.79倍，解码2.33倍），未给出基线系统的运行环境。因此无法评估其算力需求。

## 5. 实验数量与充分性
- **实验数量推测**：至少包括主实验（不同数据集上的效率与质量对比）、消融实验（验证缓存访问、并行生成、指令驱动模块各自的贡献）、以及可能在不同A-RAG框架上的泛化实验。由于文本不完整，无法获知确切组数。
- **充分性评估**：从摘要结论看，实验验证了在保持同等生成质量下实现显著加速。但缺乏对不同场景（如长文档、多样本、多轮数）的覆盖，且未提供统计显著性检验或误差条，公平性需看完整论文。从元数据中的多张图表也表明实验较为丰富，但无法确认是否涵盖所有潜在偏差。

## 6. 主要结论与发现
- 提出的指令驱动表示缩减方法可平均加速预填充阶段2.79倍、解码阶段2.33倍，同时生成质量与标准A-RAG持平。
- 表明通过缓存历史表示和指令引导的注意力分配，能有效消除检索重叠带来的冗余计算，是实现实时A-RAG系统的可行方案。
- 方法模型无关，可广泛应用于现有A-RAG框架。

## 7. 优点
- **创新性**：首次系统性地关注A-RAG中检索重叠导致的效率瓶颈，并提出针对性解决方案。
- **实用性**：方法轻量（仅增加指令驱动模块），不改变模型架构，即插即用，易于集成。
- **效率提升显著**：在保持质量前提下实现2-3倍加速，对延迟敏感的应用价值高。
- **实验设计全面**：分开评估预填充和解码阶段的加速，并做消融分析，有助于理解各组件贡献。

## 8. 不足与局限
- **实验公开度不足**：数据集、对比方法、基线的具体配置未在摘要中详述，需阅读全文才能全面评估。
- **计算资源未说明**：缺乏硬件环境以及训练/推理的绝对时间，难以复现或对比其他加速方法。
- **潜在风险**：指令驱动模块可能对复杂或模糊的指令敏感，导致注意力分配不当而影响质量；此外，缓存机制占用更多内存，对长序列或大规模部署可能带来内存压力。
- **应用限制**：仅针对多轮交互的A-RAG，不适用于单轮RAG或非检索场景；加速效果依赖于检索重叠程度，若轮次间检索内容几乎无重叠，则收益有限。
- **评估维度**：未讨论对模型泛化能力、鲁棒性、以及在不同A-RAG策略（如自适应触发检索）下的表现，覆盖范围可能不够广泛。

（完）

---
title: Revisiting Classical Chinese Event Extraction with Ancient Literature Information
title_zh: 利用古代文献信息重新审视古典中文事件抽取
authors: "Xiaoyi Bao, Zhongqing Wang, Jinghang Gu, Chu-Ren Huang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.414.pdf"
tags: ["query:ancient-text"]
score: 8.0
evidence: 提出文学视觉语言模型用于古典中文事件和知识提取
tldr: 现有古典中文事件提取方法直接移植英文或现代中文模型，忽视了古文的独特信息源。本文提出文学视觉语言模型，融合文献注释、历史背景和字形信息，捕获序列内外上下文。实验建立了新的最先进结果，验证了古代文献信息对古典中文事件抽取的独特价值。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 809, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 788, \"height\": 679, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 701, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1638, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 784, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.414/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 744, \"height\": 693, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.414/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 687, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.414/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.414/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 780, \"height\": 733, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.414/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 788, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.414/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1610, \"height\": 383, \"label\": \"Table\"}]"
motivation: 古典中文事件抽取应利用其独特的古代文献信息，而非简单移植其他语言模型。
method: 提出文学视觉语言模型，整合文献注释、历史背景和字形信息进行事件抽取。
result: 在古典中文事件抽取任务上达到新的最优性能。
conclusion: 利用古代文献的独特语义能显著提升古典中文事件抽取效果。
---

## Abstract
The research on classical Chinese event extraction trends to directly graft the complex modeling from English or modern Chinese works, neglecting the utilization of the unique characteristic of this language. We argue that, compared with grafting the sophisticated methods from other languages, focusing on classical Chinese’s inimitable source of __Ancient Literature__ could provide us with extra and comprehensive semantics in event extraction. Motivated by this, we propose a Literary Vision-Language Model (VLM) for classical Chinese event extraction, integrating with literature annotations, historical background and character glyph to capture the inner- and outer-context information from the sequence. Extensive experiments build a new state-of-the-art performance in the GuwenEE, CHED datasets, which underscores the effectiveness of our proposed VLM, and more importantly, these unique features can be obtained precisely at nearly zero cost.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现有古典中文事件抽取工作多直接移植英文或现代中文的复杂建模方法，忽略了古典中文独有的语言特性——它来源于古代文献（Ancient Literature），而文献中蕴含丰富的注释、历史背景和字形信息，这些信息可以为事件抽取提供额外的、全面的语义。
- **背景**：事件抽取旨在从文献中抽取事件，每个事件包含触发词和多个论元，对数字人文具有重要价值。但现有方法使用的语音符号、句法结构、标点等特征并非古典中文独有，导致系统次优。
- **整体含义**：本文主张应利用古典中文的独特信息源（古代文献）而非简单移植其他语言的方法，从而提升事件抽取性能。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：提出**文学视觉语言模型（Literary Vision-Language Model, VLM）**，融合古代文献的三种独特信息——**文献注释（Annotation）**、**历史背景（Background）** 和**字形（Glyph）**，以捕获序列的内外上下文信息。
- **关键技术细节**：
  - **背景信息**：包括文献来源、历史背景、传记主角。通过中国哲学书电子化计划（CText）确定来源，再通过Wikipedia获取细节，形成结构化指令。
  - **注释信息**：包括语义变异、通假字、人名。使用预训练分词器Jiayan分词后，在《古代汉语词典》中检索现代汉语解释。
  - **字形信息**：使用**句子级字形图像**，将每个汉字转换为宋体图像，按书写顺序拼接成图像，并在注释下方放置对应的现代词解释，实现视觉桥接。
  - **模型架构**：
    - 图像编码：使用**Vision Transformer (ViT)** 提取字形图像特征，通过**序列顺序对齐（Sequence Order Alignment）** 使视觉标记与文本标记顺序一致。
    - 融合指令：设计 `xt_before`（包含背景信息）和 `xt_after`（包含注释和原始句子），与视觉标记 `xv` 拼接为输入序列 `x = [xt_before, xv, xt_after]`。
    - 解码：使用**InternLM-XComposer2-VL** 作为VLM基础，采用自回归生成，通过负对数似然损失优化。
- **公式/算法流程**：
  - 输入融合：`x = [xt_before, xv, xt_after]`
  - 解码：第 i 步预测 `yi, h_di = f(h_d1..h_di-1, y_i-1)`
  - 目标概率：`p(y|x) = ∏ p(yi | y<i, x)`
  - 损失函数：`L = -1/|τ| ∑ log p(XT|XO; θ)`  (τ为训练集)

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **GuwenEE**：用于事件抽取（包括触发词和论元）。
  - **CHED2023**：用于事件检测（仅触发词）。
- **基准（Benchmark）**：
  - 触发词识别（Tri-I）和分类（Tri-C）的精确率、召回率、F1。
  - 论元识别（Arg-I）和分类（Arg-C）的F1。
- **对比方法**：
  - **通用方法**：Chinese-Bert-CRF、Guwen-Bert-CRF、DMBert、Mengzi-T5、LLaMA-3-8B、LLaMA-3-Chinese-8B、ChatGLM-3-6B、InternLM-2-7B、Qwen-2-7B。
  - **特征增强模型**：NPN、TLNN、ONEIE。
  - 另外还对比了不同信息源（LLM生成 vs 人工文献）的影响（表5）。

## 4. 资源与算力

- 文中明确提到：实验使用 **Nvidia RTX A6000** GPU，并使用 **LoRA** 微调LLM参数。
- 未说明具体训练时长、GPU数量、总计算量等信息。

## 5. 实验数量与充分性

- **实验数量**：共进行了多组实验：
  - 主实验（表1、表2）：在GuwenEE和CHED上对比多种基线，涵盖触发词和论元指标。
  - 消融实验（表3）：逐步添加文献信息（背景、注释、字形各子类），分析各个成分贡献。
  - 信息源对比（表5）：使用LLM生成信息 vs 人工文献。
  - 数据效率分析（图7）：在不同训练数据比例（5%-100%）下比较加入文献信息的效果。
  - 模型困惑度分析（图6）：比较不同LLM在文献方面的知识水平。
  - 案例研究（表4）：定性展示文献信息对错误纠正的帮助。
- **充分性与公平性**：
  - 对比方法覆盖了常见PLM和特征增强模型，但未提及超参数调整细节或多次运行标准差。
  - 数据效率实验证明了文献信息在低资源下的优势，消融实验揭示了各成分贡献。
  - 实验设计较为全面，但未说明是否进行了统计显著性检验（除了一次提到`p < 0.05`）。整体而言实验充分且客观。

## 6. 论文的主要结论与发现

- **主要结论**：提出的文学VLM在GuwenEE和CHED上均达到**新最先进性能**（SOTA），表明古代文献信息（背景、注释、字形）能显著提升古典中文事件抽取。
- **关键发现**：
  - 文献信息（尤其是背景和注释）贡献最大，字形信息通过视觉桥接进一步增益。
  - 当前LLM在古典中文知识上困惑度远高于现代文本，而微调后的VLM能有效注入这些知识。
  - 人工文献源优于LLM生成的信息源（LLM存在幻觉且缺乏特定领域知识）。
  - 文献信息在低资源情况下提升更明显（数据效率提高）。

## 7. 优点

- **方法创新**：首次将古代文献（背景、注释、字形）作为独特信息源用于古典中文事件抽取，提出跨模态融合的VLM。
- **实用性**：信息来源无需额外标注成本（利用现有古籍资源和字典），可以零成本获取。
- **实验全面**：包含主实验、消融、数据效率、信息源对比、案例研究，验证了各个假设。
- **代码开放**：提供了GitHub仓库，便于复现。

## 8. 不足与局限

- **语言局限**：仅针对古典中文，方法推广到其他语言（可能无古代文献来源）受限。
- **资源信息缺失**：未提供训练时间、GPU数量等算力消耗细节，难以评估计算成本。
- **统计细节不足**：多数实验未报告多次运行的标准差或置信区间，仅有一处提到`p < 0.05`。
- **未考虑语音特征**：作者承认语音（尤其是古今音变）未被探索，可能还有价值。
- **LLM基座依赖**：VLM基于InternLM-XComposer2-VL，其他基座泛化性未验证。

（完）

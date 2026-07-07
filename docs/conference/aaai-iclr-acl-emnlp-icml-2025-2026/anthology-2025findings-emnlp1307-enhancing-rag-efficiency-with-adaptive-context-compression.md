---
title: Enhancing RAG Efficiency with Adaptive Context Compression
title_zh: 通过自适应上下文压缩提升RAG效率
authors: "Shuyu Guo, Shuo Zhang, Zhaochun Ren"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1307.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 自适应上下文压缩提升RAG效率
tldr: RAG系统常因长检索上下文导致高推理成本，现有固定压缩率方法不灵活。本文提出ACC-RAG框架，根据输入复杂度动态调整压缩率，结合分层压缩器和上下文选择器保留最小充分信息。在Wikipedia和五个QA数据集上，ACC-RAG在保持准确率的同时显著降低了推理开销，为管理长上下文和优化检索窗口提供了实用方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 795, \"height\": 676, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1449, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 645, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 914, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 793, \"height\": 586, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 729, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 694, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1628, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 773, \"height\": 852, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 849, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 787, \"height\": 560, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 811, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1287, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 705, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1307/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 721, \"height\": 307, \"label\": \"Table\"}]"
motivation: RAG长上下文带来高推理成本，固定压缩率不适应不同复杂度的查询。
method: 提出ACC-RAG，包含分层压缩器和上下文选择器，动态调整压缩率。
result: 在多个数据集上，ACC-RAG在保持精度的同时显著降低推理代价。
conclusion: 自适应压缩是优化RAG效率和上下文管理的有效技术。
---

## Abstract
Retrieval-augmented generation (RAG) enhances large language models (LLMs) with external knowledge but incurs significant inference costs due to lengthy retrieved contexts. While context compression mitigates this issue, existing methods apply fixed compression rates—over-compressing simple queries or under-compressing complex ones. We propose Adaptive Context Compression for RAG (ACC-RAG), a framework that dynamically adjusts compression rates based on input complexity, optimizing inference efficiency without loss of accuracy. ACC-RAG combines a hierarchical compressor (for multi-granular embeddings) with a context selector to retain minimal sufficient information, akin to human skimming. Evaluated on Wikipedia and five QA datasets, ACC-RAG outperforms fixed-rate methods and unlocks >4× faster inference versus standard RAG while maintaining or improving accuracy.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：检索增强生成（RAG）通过引入外部知识提升大语言模型（LLM）性能，但检索到的长上下文会导致高昂的推理成本，且可能超出上下文窗口限制。现有上下文压缩方法（如词法压缩、嵌入压缩）通常采用固定压缩率，导致对简单问题过度压缩（丢失必要信息）或对复杂问题压缩不足（保留冗余），缺乏灵活性。
- **目标**：提出一种自适应上下文压缩框架，根据输入复杂度动态调整压缩率，在不损失准确率的前提下优化推理效率。

## 2. 方法论

### 核心思想
- **类比人类略读**：模仿人类阅读时先快速浏览再决定是否继续深入的方式，将压缩过程解耦为离线固定率压缩和在线动态选择。
- **框架组成**：分层压缩器（Hierarchical Compressor）+ 自适应选择器（Adaptive Selector）。

### 关键技术细节
- **分层压缩器**：
  - 对每个文档 \(d_i\) 以固定压缩率 \(\tau\) 生成多粒度嵌入序列 \(E_i = [e^{(1)}_i, \dots, e^{(m_i)}_i]\)（\(m_i = \lfloor L_i/\tau \rfloor\)）。
  - 训练分两阶段：① 预训练（自编码 + 语言建模，优化负对数似然损失）；② 微调（自蒸馏，最小化教师分布与学生分布的KL散度）。
  - **多粒度训练**：在多个粒度 \(B = \{b_1,\dots,b_k\}\) 上联合优化，使得前序嵌入包含更关键信息，后续补充细节。损失函数为各粒度重建误差之和。

- **自适应选择器**：
  - **推理流程**：查询嵌入 \(E_q\) 与所有文档嵌入拼接后，按粒度序列 \(B\) 逐步截取子序列 \(E_{1:b_t}\)，与 \(E_q\) 一同输入解码器，获得隐藏状态 \(H_t\)；选择器基于 \(H_t\) 判断上下文是否充分（输出1停止，0继续）。
  - **训练**：使用强化学习（REINFORCE），从解码器不同粒度下的生成结果中合成训练数据（标签由生成答案与标准答案的匹配决定），奖励函数为：若选择器在某粒度停止且该粒度答案正确则+1，否则-1。

## 3. 实验设计

### 数据集与场景
- **语料库**：Wikipedia 2018年12月快照，DPR预处理，分为21,015,324个128令牌的文档块。
- **下游任务**：五个开放域QA数据集：Natural Questions (NQ)、TriviaQA、WebQuestions (WQ)、CuratedTREC (TREC)、SQuAD v1.1。
- **基准（Benchmark）**：统一上述语料和任务，消除以往方法因训练数据规模、任务混合不同带来的不公平比较。

### 对比方法
- **全微调方法**：AutoCompressor（仅语言建模）、COCOM（联合优化压缩器与解码器）。
- **即插即用方法**：xRAG（极端压缩，1个token）、ICAE（不同压缩率×128、×16、×4）。
- **基线**：仅LLM（无检索）、标准RAG（无压缩）。

### 评价指标
- **有效性**：Match (M) —— 参考答案是否出现在模型生成输出中。
- **效率**：首令牌推理时间 (First Token Inference Time, FTIT)，聚焦压缩方法对预填充阶段的影响。

## 4. 资源与算力

- **基础模型**：主实验使用 Mistral-7B-Instruct-v0.2；可扩展性实验使用 Llama3.2-3B-Instruct 和 Llama3.1-8B-Instruct。
- **训练硬件与时长**：
  - 压缩器预训练：1×A100 80G GPU，约20小时。
  - 压缩器微调：1×A6000 48G GPU，约50小时。
  - 选择器训练：1×A6000 48G GPU，约1小时。
- **框架**：PyTorch + Hugging Face Transformers；检索器使用 ColBERT-v2。

## 5. 实验数量与充分性

- **主实验**：在5个数据集上对比10种以上方法（含不同压缩率变体），报告M和FTIT。
- **消融与分析实验**（共约10组）：
  - 压缩率分析（不同τ对累计M的影响）。
  - 训练策略消融（预训练/微调任务、自蒸馏 vs. 指令跟随）。
  - 粒度序列选择（G0~G3共4种，及组合）。
  - 选择器架构消融（有无RL、注意力、分段嵌入、粒度特征）。
  - 推理验证（压缩器有无选择器对比）。
  - 框架组合（不同压缩机与不同选择策略共12种组合）。
  - RAG集成分析（弹性率、提升率）。
  - OOD分析（未见支持文档、域外查询（HotpotQA、FEVER））。
  - 可扩展性分析（Llama3-3B/8B）。
  - 额外计算开销分析。
- **充分性评价**：实验设计全面，覆盖了方法的核心方面（压缩器、选择器、整体框架），并统一了训练数据与评估流程，确保了公平性。但作者指出选择器性能仍是瓶颈，且缺乏受控条件实验。

## 6. 主要结论与发现

- ACC-RAG在所有压缩基线中取得最佳M分数（平均35.23），显著高于次优方法（ICAE×4的26.13）。
- 与标准RAG相比，ACC-RAG在4个数据集上精度相当或更优，同时推理速度提升4倍以上（FTIT从3371ms降至697ms）。
- 多粒度训练策略能有效将关键信息压缩至前序嵌入，从而允许选择器更早停止，提高效率。
- 选择器使用强化学习训练优于监督学习，注意力机制和嵌入设计有助于提升分类准确率。
- 框架可扩展至不同规模的LLM（Llama3系列），仍保持约4-5倍加速与<10%的准确率差异。

## 7. 优点

- **动态适应性**：首次将压缩率与查询复杂度关联，避免固定率方法的过压缩或欠压缩问题。
- **模块化解耦**：离线压缩与在线选择分离，降低推理计算开销，且压缩机可复用。
- **统一Benchmark**：系统性地标准化训练语料、任务与评估指标，解决了以往研究可比性差的问题。
- **训练策略创新**：多粒度联合优化 + 自蒸馏微调（避免指令跟随对生成分布的干扰），显著提升信息保留。
- **效率与效果平衡**：在保持甚至提升准确率的同时实现>4×推理加速，具有实用价值。

## 8. 不足与局限

- **选择器是瓶颈**：选择器的预测准确率（约70.75%）是整体性能的最大限制因素，进一步提升选择器可解锁更大潜力。
- **缺乏受控条件实验**：本文未对自适应机制进行严格受控条件的分析（如不同复杂度查询的压缩率分布）。
- **压缩器与选择器分离训练**：未尝试联合优化，可能导致两者之间对齐不足，影响整体性能。
- **模型与文本长度限制**：仅在小模型（7B级）和短文本（128令牌块）上实验，未探索更大模型（如70B）或更长上下文（如多跳推理），限制了泛化结论。
- **潜在风险**：文本压缩为嵌入可能造成信息失真，且继承RAG固有的检索偏差、知识陈旧、对抗性注入等风险。

（完）

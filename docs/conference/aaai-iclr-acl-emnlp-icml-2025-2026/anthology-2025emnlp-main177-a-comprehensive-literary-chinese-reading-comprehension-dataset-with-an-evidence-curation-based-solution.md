---
title: A Comprehensive Literary Chinese Reading Comprehension Dataset with an Evidence Curation Based Solution
title_zh: 一个全面的文言文阅读理解数据集及基于证据策展的解决方案
authors: "Dongning Rao, Rongchu Zhou, Peng Chen, Zhihua Jiang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.177.pdf"
tags: ["query:ancient-text"]
score: 8.0
evidence: 提出文言文阅读理解数据集CRISIS和基于证据策展的VIRTUAL方法
tldr: 文言文阅读理解面临数据稀缺、输入长、问题需深入理解等挑战。本文构建了最大规模的CRISIS数据集，并提出VIRTUAL方法：通过证据策展、选项打乱和基于抽象意义表示的从句分割，解决信息过载、顺序偏差和复杂问题。实验表明该方法显著提升了阅读理解性能。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.177/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1636, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.177/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1574, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.177/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 687, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.177/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 719, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.177/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 671, \"height\": 2607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.177/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1047, \"height\": 2586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.177/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1543, \"height\": 912, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 832, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 557, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 693, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1450, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 767, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 616, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 593, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 623, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 583, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1636, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1595, \"height\": 1694, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1291, \"height\": 420, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1047, \"height\": 2586, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.177/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1576, \"height\": 1664, \"label\": \"Table\"}]"
motivation: 文言文阅读理解存在数据稀缺、长输入和深入推理的挑战。
method: 构建最大文言文数据集CRISIS，提出VIRTUAL方法包括证据策展、选项打乱和AMR从句分割。
result: VIRTUAL方法显著提升文言文阅读理解准确率。
conclusion: 大规模高质量数据集和证据策展方法能有效推动文言文自然语言处理研究。
---

## Abstract
Low-resource language understanding is challenging, even for large language models (LLMs). An epitome of this problem is the CompRehensive lIterary chineSe readIng comprehenSion (CRISIS), whose difficulties include limited linguistic data, long input, and insight-required questions. Besides the compelling necessity of providing a larger dataset for CRISIS, excessive information, order bias, and entangled conundrums still haunt the CRISIS solutions. Thus, we present the eVIdence cuRation with opTion shUffling and Abstract meaning representation-based cLauses segmenting (VIRTUAL) procedure for CRISIS, with the largest dataset. While the dataset is also named CRISIS, it results from a three-phase construction process, including question selection, data cleaning, and a silver-standard data augmentation step, which augments translations, celebrity profiles, government jobs, reign mottos, and dynasty to CRISIS. The six steps of VIRTUAL include embedding, shuffling, abstract beaning representation based option segmenting, evidence extracting, solving, and voting. Notably, the evidence extraction algorithm facilitates literary Chinese evidence sentences, translated evidence sentences, and annotations of keywords with a similarity-based ranking strategy. While CRISIS congregates understanding-required questions from seven sources, the experiments on CRISIS substantiate the effectiveness of VIRTUAL, with a 7 percent hike in accuracy compared with the baseline. Interestingly, both non-LLMs and LLMs have order bias, and abstract beaning representation based option segmenting is constructive for CRISIS.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **任务定义**：文言文阅读理解（CRISIS）是一项低资源语言理解任务，要求在文言文段落基础上回答需要深入理解的问题（而非简单事实记忆）。
- **主要挑战**：
  - 数据稀缺：文言文训练语料不足。
  - 长输入：平均段落长度达637.6字，选项平均53.5字。
  - 深入推理：问题需要基于文本细节进行推断，而非常识。
  - 现有方法的困难：信息过载（文献检索碎片化）、顺序偏差（模型在不同选项排列下表现不一致）、复杂问题纠缠（选项中包含多个子句难以分解）。
- **研究目标**：构建最大规模的文言文阅读理解数据集，并提出一套系统性解决方案（VIRTUAL），以提升模型在该任务上的准确性和公平性。

## 2. 论文提出的方法论

### 核心思想
VIRTUAL（eVIdence cuRation with opTion shUffling and Abstract meaning representation-based cLauses segmenting）通过“证据策展”、“选项打乱”和“基于抽象意义表示的从句分割”三个关键组件，解决上述三大挑战。

### 关键技术细节

1. **句子嵌入（Embedding）**：使用GuwenBERT将段落中的句子和问题中的子句编码为向量，并存储于FAISS向量数据库。
2. **选项打乱（Shuffling）**：将原始选项顺序循环移位两次（如ABCD→BCDA→CDAB），生成三种顺序，用于后续分别求解并投票，以消除顺序偏差。
3. **基于AMR的选项分割（AMR-based Segmenting）**：利用AMR解析器将每个选项分解为若干语义子句（例如选项A“臧霸曾为吕布效力，曹操擒捉吕布以后，臧霸为避祸藏匿起来；后来他又被曹操捕获，曹操不计前嫌，对他委以重任，任命他为琅邪相”分割为6个子句）。
4. **证据提取（Evidence Extracting）**：基于相似度排名，从段落中选取与每个子句最相关的文言文句子、现代文翻译句子以及关键词注释（具有可选项），组成证据列表。算法参数包括：文言文证据数（#s）、现代文证据数（#t）、是否包含关键词注释（withAnnotations）。
5. **求解（Solving）**：使用LLM（如Qwen）基于零样本、单样本或思维链（COT）三种提示策略回答：对于每个子句判断对错，计算选项正确率作为分数，若平局则回退到零样本。
6. **投票（Voting）**：对三种选项顺序下的答案进行多数投票，得到最终答案。

### 算法流程（文字说明）
- 输入：文言文段落、问题、四个选项。
- 输出：答案（A/B/C/D）。
- 步骤：
  1. 对段落句子和选项分句进行嵌入并存储。
  2. 生成三种选项顺序。
  3. 对每个顺序的每个选项，进行AMR分割得到子句列表。
  4. 对每个子句，执行证据提取算法（算法1）：从段落中选取top-k个最相似的文言文句子、翻译句子（可选含关键词注释）。
  5. 将证据连同问题、段落、选项送入LLM，使用指定提示策略得到该顺序下的答案。
  6. 对三种顺序的答案进行多数投票，输出最终答案。

## 3. 实验设计

### 数据集
- **CRISIS**：自建最大文言文阅读理解数据集，共4,415道多选题，来源于7个公开资源（ACRE、CCLUE、WYWEB、高考、AGIEval、AC-Eval、E-Eval）。答案分布均衡（A:B:C:D≈1:1:1:1）。包含数据增强：现代文翻译、名人简介、官职说明、年号说明、朝代信息（均由LLM生成，为银标准）。

### Benchmark与对比方法
- **非LLM基线**：EVERGREEN（基于BERT编码+卷积+集成）。
- **LLM基线**：Qwen-plus-0806、ERNIE-4.0-8K、GPT-4o、GLM-4、o1-mini。
- **评价指标**：分类准确率（Overall及按难度分层：简单/中等/复杂）。

### 实验类型
1. **模型对比**：VIRTUAL（基于Qwen-plus）与所有基线对比。
2. **消融实验**：逐一去除关键组件（关键词注释、文言文证据、翻译证据、AMR分割、打乱与投票）。
3. **证据组合测试**：不同数量的文言文证据和现代文证据组合对准确率的影响。
4. **泛化性测试**：在C3（现代中文阅读理解数据集）上验证VIRTUAL的通用性。
5. **提示策略对比**：零样本、单样本、单样本+增强数据、思维链。
6. **不同时间跨度准确率**：按古代、中古、近古三个时间段分析。
7. **开源小模型实验**：DeepSeek-R1-Distill-Qwen-7B、DeepSeek-R1-Distill-Llama-8B、Llama-2-7B。

## 4. 资源与算力

- **训练环境**：Ubuntu 20.04.1 LTS, Intel Core i9-10900K CPU, 2×RTX 3090 GPU。
- **训练耗时**：EVERGREEN模型训练约15分钟。
- **API开销**：使用Qwen-plus-0806 API，总计花费约300美元（输入$0.4/百万token，输出$1/百万token）。
- 论文未详细说明所有LLM实验的GPU数量或运行时间，仅提及小模型实验是在本地RTX 3090上进行。

## 5. 实验数量与充分性

- **实验组数**：约9组主要实验（包括模型对比表1、消融表2、证据组合表3、泛化表4、提示策略表5、时间跨度表6、小模型表7，以及Perplexity分析图6）。此外还有详细的案例分析和附件中的额外实验。
- **充分性评估**：
  - **正面**：消融实验覆盖了所有核心组件；证据组合测试探索了超参数；泛化测试验证了方法跨领域适用性；提示策略对比全面；小模型测试了方法的可迁移性。
  - **不足**：
    - 所有LLM实验均为单次运行，未报告多次运行的统计波动（论文承认“稳定性超出范围”）。
    - 仅使用了5种LLM，未涵盖更多主流模型（如Claude、Gemini等）。
    - 小模型实验显示VIRTUAL导致性能下降，但未深入分析原因（如长文本超限）。
    - 难度分层基于Qwen的log概率，未能验证此分层对其他模型是否公平。

## 6. 主要结论与发现

- VIRTUAL在CRISIS数据集上达到80.8%准确率，比最佳基线Qwen-plus（73.1%）提升7.7%。
- 所有模型均存在顺序偏差（选项顺序影响结果），选项打乱与投票能有效缓解。
- AMR-based选项分割对复杂问题（准确率提升8%）和总体准确率均有正向贡献。
- 证据提取中结合文言文与现代文证据比单独使用一种效果更好；关键词注释贡献较小。
- 泛化测试显示VIRTUAL在现代中文数据集C3上也优于Qwen-plus（98.7% vs 96.7%）。
- 提示策略中单样本（不含增强数据）最好，思维链反而下降。
- 近古（宋明清）时期的问题准确率最低（79.5%），可能因考题设计导致难度更高。

## 7. 优点

- **数据集规模最大**：CRISIS包含4,415题，覆盖从先秦到清代的广泛时间跨度，且提供多种数据增强（翻译、名人、官职等），为后续研究提供了丰富资源。
- **方法创新性强**：将证据策展、选项打乱、AMR分割三者有机结合，系统性地解决了文言文理解的三个核心痛点。
- **实验设计全面**：进行了详尽的消融、超参搜索、泛化、提示策略对比，结论扎实。
- **发现重要现象**：明确揭示了LLM和非LLM在文言文阅读中的顺序偏差，为后续公平性研究提供参考。
- **可复现性好**：代码开源，数据来源公开，使用主流LLM API和开源模型。

## 8. 不足与局限

- **数据偏差**：
  - 标签可能包含人为错误（人类标注者分歧）。
  - LLM生成的增强数据（翻译、简介等）仅银标准，可能引入噪声。
  - 所有实验仅单次运行，未统计方差，结果可能不稳定。
- **实验覆盖不足**：
  - 仅测试5种LLM，未涵盖Claude、Gemini等近期强模型；小模型实验显示VIRTUAL可能不适用于较小模型（因输入更长）。
  - 未进行跨语言泛化测试（仅在中文现代RC上测试）。
- **方法局限**：
  - VIRTUAL增加了输入长度（加入证据），对于上下文窗口较小的模型可能产生性能下降（论文已提及）。
  - AMR分割依赖外部工具（可能存在错误传播）。
  - 提示策略中COT效果差，作者未深入分析原因（可能是子句判断任务本身不适合长链推理）。
- **伦理与公平性**：
  - 大多数源数据集许可未明确，仅AGIEval和AC-Eval为MIT许可，CCLUE为Apache-2.0。
  - 标注者为中国研究生，可能存在文化或教育背景导致的偏差。
- **应用限制**：目前仅适用于选择题设置，无法直接推广到自由回答或其他生成式理解任务。

（完）

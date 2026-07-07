---
title: "BIRD: Bronze Inscription Restoration and Dating"
title_zh: BIRD：青铜铭文修复与断代
authors: "Wenjie Hua, Hoang H Nguyen, Gangyan Ge"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1073.pdf"
tags: ["query:ancient-text"]
score: 9.0
evidence: 青铜铭文修复与断代，面向古代中文文本
tldr: 早期中国青铜铭文残缺且难以断代，传统方法依赖专家。本文构建了BIRD数据集，并提出基于异体字感知的掩码语言建模框架，集成领域自适应预训练和字形网络（Glyph Net），将字素与异体字关联。实验表明该方法有效提升了铭文修复和断代的准确率，推动了古籍数字化的进一步发展。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1073/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 772, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1073/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 727, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1073/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 750, \"height\": 572, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1073/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1073/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 702, \"height\": 428, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 831, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1628, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 806, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1436, \"height\": 1177, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1220, \"height\": 1172, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1073/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1662, \"height\": 937, \"label\": \"Table\"}]"
motivation: 早期中国青铜铭文片段残缺且缺乏可靠的自动断代方法。
method: 构建BIRD数据集，提出异体字感知掩码语言模型，结合字形网络和领域自适应预训练。
result: 实验证明该模型在铭文修复和断代任务上显著优于基线。
conclusion: 结合领域知识和预训练模型可有效处理古代文字修复与断代任务。
---

## Abstract
Bronze inscriptions from early China are fragmentary and difficult to date. We introduce BIRD (Bronze Inscription Restoration and Dating), a fully encoded dataset grounded in standard scholarly transcriptions and chronological labels. We further propose an allograph-aware masked language modeling framework that integrates domain- and task-adaptive pretraining with a Glyph Net (GN), which links graphemes and allographs. Experiments show that GN improves restoration, while glyph-biased sampling yields gains in dating.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：中国青铜时代（约前21–前3世纪）的青铜铭文常因出土损坏而残缺不全，且年代归属不确定。传统修复与断代依赖古文字专家的字形对比和上下文推断，过程费时且难以规模化。
- **NLP挑战**：① **低资源**：虽已公布近2万篇铭文，但大多极短（过半不超过3个字符），有效训练数据稀疏。② **异体字（allography）** ：同一字素（grapheme）有多种写法（如“祈”字从商到东周有多个异体），当前编码将它们视为不同词元，阻碍了模型泛化。
- **本文贡献**：构建首个全编码的青铜铭文数据集 **BIRD**（41k tokens），并配套字素-异体字资源 **Glyph Net**（1,078对）；提出异体字感知的掩码语言模型框架，结合领域自适应预训练（DAPT）和任务自适应预训练（TAPT），显著提升修复与断代的准确性。

## 2. 方法论
- **核心思想**：利用预训练语言模型（如SikuRoBERTa）进行掩码语言建模（MLM），并通过专用模块处理低资源和异体字问题。
- **关键技术细节**：
  - **DAPT**：在同期的传世先秦文献（2.09M tokens，40种作品）上进行领域自适应预训练，冻结底部六层以稳定训练。
  - **TAPT**：在BIRD铭文语料上进行任务自适应预训练，全部层解冻。
  - **Glyph Net (GN)**：从古文字学研究中构建字素与异体字的对应关系，通过传递闭包形成字族，新字形对齐到字族质心。
  - **GN感知掩码与替换**：在MLM过程中，偏向于掩盖和替换字族内的异体字，促进字族级特征学习。
  - **步长掩码（stride-based masking）**：针对铭文极短的特点（中位数4个字符），采用步长掩码确保每个序列最多丢失一个词元。
- **损失函数**：总损失为 `L = (1-α)L_MLM + αL_GN`，其中 `L_GN` 通过对同一字族的预测分布取平均来实现正则化，α在训练中逐步调度。

## 3. 实验设计
- **数据集与基准**：对比基线包括 **BiLSTM**（序列模型）、**SVM**（文本分类）、**mBERT**、**XLM-RoBERTa (base/large)**、**SikuRoBERTa**（领域专用）。
- **任务**：
  - **修复（Restoration）**：在零样本的未见字形上，以式掩码后预测完整字符，评估指标为 **Exact@K**（精确匹配）和 **Family@K**（字族内匹配）。
  - **断代（Dating）**：微调线性分类头，预测王朝级（商、西周、春秋、战国）和更细分的时期级（早、中、晚），报告准确率、宏F1及层次化分数。
- **超参数**：步长、学习率等通过贝叶斯搜索（Weights & Biases）调优（表8）。

## 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量及训练时长。仅提及“涉及相对小规模模型，计算成本有限”（Ethics Statement），故无法提供具体算力细节。

## 5. 实验数量与充分性
- **实验数量**：大量实验覆盖：
  - 多种骨干（4种） × 多种适应方案（无适应、DAPT_only、TAPT_only、TAPT_from_DAPT等） × 消融组件（GN、bias）。
  - 修复任务报告了6种指标（表3），断代任务报告了10种指标（表4）。
  - 额外消融表（表9、10、11）分析表示聚类质量与各组件贡献。
- **充分性**：实验设计全面，包括零样本评估、步长调优、消融研究、案例验证（胡簋修复），对比基线多样，结果客观公平。
- **不足**：未包含更多样化的PLM（如基于古文的大模型）或更大规模的预训练语料。

## 6. 主要结论与发现
- **SikuRoBERTa 表现最佳**：在零样本修复任务中，Exact@1达48.50%，Family@10达72.86%，远超BiLSTM和multilingual模型；在断代任务中，王朝准确率85.19%，层次化时期F1达63.55%。
- **领域预训练优于多语言预训练**：仅使用先秦文献进行DAPT即可带来显著提升，SikuRoBERTa在修复和断代上均领先。
- **Glyph Net 有效提升修复**：加入GN的配置在Exact@1上比纯TAPT提高约1个百分点，字族内一致性表征提升。
- **模型学习了语法和上下文**：修复正确集中在固定格式（如器物名、时间词），错误多发生在语义相近的字词上，但仍保持正确语法类别。
- **断代难点**：春秋战国时期错误较多，公式化表达跨时期混淆；但跨远期的严重误判罕见。

## 7. 优点
- **首个全编码NLP就绪数据集**：BIRD填补了青铜铭文NLP研究的空白，完全编码、去重、过滤、标注年代，公开可用。
- **Glyph Net 设计新颖**：将古文字学知识（异体字关系）无缝融入MLM框架，通过字族正则化促进泛化，而非简单忽略异体性。
- **消融实验全面**：系统比较了DAPT、TAPT、GN、bias等组件的单独与组合效果，在修复、表示质量、断代三个维度验证。
- **零样本评估合理**：在未见字形上测试，模拟真实考古场景，避免数据泄露。
- **案例研究（胡簋）**：展示实际修复效果，并与专家注解对比，增强实用说服力。

## 8. 不足与局限
- **数据稀疏与长尾**：罕见字素性能受限，泛化能力有待提升（倚赖未来如数据增强或少样本方法）。
- **字形建模仍浅**：GN仅基于组别偏置，未考虑更严格的古文字约束（如假借字关系、声旁信息）。
- **缺乏音韵信息**：青铜铭文常使用通假借字，纯词元模型无法捕获音系替换规律。
- **无法利用局部字形信息**：铭文破损时，可见的子部首无法被MLM嵌入利用；未来可引入IDS（表意文字描述序列）进行结构感知建模。
- **未整合考古多模态信息**：传统断代依赖器形、纹饰等，本文仅使用文本，与专家实践仍有差距。
- **模型预测仅作辅助**：应被视为初步假设，最终解读需经古文字学家核实。
- **实验环境未明确**：算力细节缺失，限制了可复现性评估。

（完）

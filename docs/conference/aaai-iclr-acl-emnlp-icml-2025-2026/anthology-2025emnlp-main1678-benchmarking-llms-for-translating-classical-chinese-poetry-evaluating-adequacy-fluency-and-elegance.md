---
title: "Benchmarking LLMs for Translating Classical Chinese Poetry: Evaluating Adequacy, Fluency, and Elegance"
title_zh: 古诗英译的LLM基准评估：充分性、流畅性与优雅性
authors: "Andong Chen, Lianzhang Lou, Kehai Chen (陈科海), Xuefeng Bai (白雪峰), Yang Xiang, Muyun Yang (杨沐昀), Tiejun Zhao (赵铁军), Min Zhang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1678.pdf"
tags: ["query:ancient-text"]
score: 9.0
evidence: 古典诗歌翻译及RAT方法
tldr: 现有LLM在古诗英译任务中表现不足，难以同时保证充分性、流畅性和优雅性。PoetMT基准评估了多个LLM，并提出RAT（检索增强翻译）方法，通过检索相关知识提升翻译质量。实验表明RAT显著优于基线，推动了古典诗歌自动翻译研究。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 429, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 510, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 760, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1647, \"height\": 799, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 775, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 801, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 727, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 723, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 724, \"height\": 334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1678/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 808, \"height\": 653, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1480, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 619, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 669, \"height\": 568, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 788, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 740, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 793, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 785, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 805, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 772, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 797, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 712, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 715, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 734, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 754, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 613, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 692, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1678/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1646, \"height\": 297, \"label\": \"Table\"}]"
motivation: LLM在翻译古典诗歌时难以兼顾充分性、流畅性和优雅性。
method: 提出RAT，一种检索增强翻译方法，利用外部知识提升古诗翻译质量。
result: RAT在PoetMT基准上显著优于现有LLM。
conclusion: RAT有效提升了古典诗歌翻译的多个维度。
---

## Abstract
Large language models (LLMs) have shown remarkable performance in general translation tasks. However, the increasing demand for high-quality translations that are not only adequate but also fluent and elegant. To assess the extent to which current LLMs can meet these demands, we introduce a suitable benchmark (PoetMT) for translating classical Chinese poetry into English. This task requires not only adequacy in translating culturally and historically significant content but also a strict adherence to linguistic fluency and poetic elegance. Our study reveals that existing LLMs fall short of this task. To address these issues, we propose RAT, a Retrieval-Augmented machine Translation method that enhances the translation process by incorporating knowledge related to classical poetry. Additionally, we propose an automatic evaluation metric based on GPT-4, which better assesses translation quality in terms of adequacy, fluency, and elegance, overcoming the limitations of traditional metrics.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有大规模语言模型（LLM）在通用翻译任务中表现优异，但能否同时满足“充分性（adequacy）、流畅性（fluency）和优雅性（elegance）”这三个翻译质量要求？尤其针对古典中文诗歌英译这一极具挑战性的任务。
- **研究动机**：古典中文诗歌承载深厚的历史文化，要求翻译既准确传达文化内涵（充分性），又严格符合韵律、结构等语言规范（流畅性），还要保留简练含蓄的审美价值（优雅性）。现有LLM在这些方面存在不足。
- **整体含义**：首次系统评估LLM在古典诗歌翻译中的表现，揭示其局限性，并提出改进方法（RAT），为未来文学翻译和LLM能力提升提供基准和方向。

## 2. 论文提出的方法论

### 核心思想
采用**检索增强翻译（Retrieval-Augmented Translation, RAT）**，利用外部古典诗歌知识库为LLM提供上下文支持，以弥补模型在历史文化知识、韵律结构等方面的不足。

### 关键技术细节
- **知识库构建**：收集30,000条古典诗歌知识条目，包括历史背景、朝代、现代汉语翻译、作者介绍、现代汉语分析、诗歌类型等。
- **两阶段工作流**：
  1. **第一阶段**（检索与选择）：
     - **Retriever**：通过字符串匹配从知识库中检索与待译诗歌相关的多条知识。
     - **Selector**：基于LLM（如GPT-4）过滤检索结果中的无关内容，提炼最相关的历史背景、作者信息等。
  2. **第二阶段**（翻译与整合）：
     - **Translator**：使用六种不同类型的知识分别生成六个候选翻译（每种知识对应一个翻译结果）。
     - **Voter**：基于LLM从六个候选翻译中选择质量最高的句子并拼接成完整译文。
     - **Extractor**：进一步过滤Voter输出中的噪声，得到最终译文。

- **自动评估指标**：提出基于GPT-4的评分方法，从“声音美（BS）”、“形式美（BF）”、“意义美（BM）”三个维度对翻译打分（1-5分），并计算平均分LLM-Avg。

### 算法流程（文字说明）
1. 输入源诗文本。
2. 使用Retriever从知识库中检索六类知识（历史背景、朝代、现代汉语翻译、作者介绍、现代汉语分析、诗歌类型）。
3. Selector过滤无关知识，保留最相关的知识。
4. Translator分别利用每类知识生成六个翻译候选。
5. Voter综合比较六个候选，选出每句最佳翻译并拼接。
6. Extractor移除额外噪声，输出最终译文。

## 3. 实验设计

### 数据集/场景
- **PoetMT基准**：包含608首古典诗歌（197首唐诗、189首宋词、222首元曲）及其专家翻译（许渊冲）。构建了：
  - **语篇级翻译测试**：评估完整诗歌的充分性、流畅性和优雅性。
  - **句子级充分性测试**：758个包含历史文化知识和常识的句子，每个句子以三元组 (s, tc, te) 形式给出源句、正确翻译和错误翻译，用于评估充分性。

### 对比方法
- **基线**：零样本翻译（Zero-shot）、5-shot、Rerank（重排名）、Refine（迭代精炼）、MAD（多智能体辩论）、EAPMT（基于解释的翻译）、Dual-Reflect（双学习反馈）。
- **LLM模型**：闭源模型（ChatGPT、GPT-4）、开源模型（Llama3-8B、Vicuna-7B）、中文LLM（Qwen-72B）。

### 评估指标
- **传统自动指标**：BLEU（1-4）、COMET、BLEURT。
- **LLM自动指标**：LLM-BS、LLM-BF、LLM-BM、LLM-Avg（基于GPT-4评分）。
- **人工评估**：对50个样本进行1-5分打分（包含BS、BF、BM），并计算ACC（句子级充分性正确率）。

## 4. 资源与算力

**未明确说明具体算力**。论文中未提及使用的GPU型号、数量或训练时长。仅提到使用了GPT-4（通过API gpt-4-0613）、ChatGPT（gpt-3.5-turbo）、以及开源模型（Llama3-8B、Vicuna-7B、Qwen-72B）进行推理，未涉及模型训练过程。

## 5. 实验数量与充分性

### 实验数量
- **主要实验结果**（表3）：在PoetMT基准上比较了多种方法（如Zero-shot、5-shot、Rerank、MAD、Dual-Reflect、EAPMT、RAT）在GPT-4、ChatGPT、Vicuna-7B、Llama3-8B、Qwen-72B上的表现，报告了COMET、BLEURT、LLM-BM/BS/BF/LLM-Avg、BLEU-1/2/3/4等指标。
- **充分性评估**（表4）：在句子级测试集上比较了多种方法的LLM-BM、Human-BM和ACC。
- **数据污染验证**（表5）：评估PoetMT诗歌是否存在于训练数据中（通过BLEU分数）。
- **不同知识类型影响实验**（图5）：分别使用每种知识类型测试对BS/BF/BM的影响。
- **消融实验**：
  - 现代汉语翻译的影响（表6）。
  - RAT各组件消融（表8）：w/o selector、w/o voter、w/o extractor。
- **不同诗歌类型难度分析**（图6）：唐诗、宋词、元曲的LLM-BS/BF/BM对比。
- **手动错误分析**（表9, 10）：50个样本的翻译质量分类及错误类型分析。
- **评估指标相关分析**（表2）：计算LLM指标与人工指标的相关性（Pearson、Spearman、Kendall）。
- **多参考BLEU实验**（附录D.3表12）。
- **小模型集成实验**（附录D.2表11）。

### 充分性客观性评估
- **充分性**：实验覆盖了多种LLM（闭源和开源）、多种对比方法、多个评估维度（传统指标和新型LLM指标），并进行了消融、错误分析、相关性验证，较为全面。
- **客观性**：人工评估由5名有经验的翻译专家进行，并经过校准；但未提及人工评估的Kappa一致性系数，可能存在偏差。数据污染检验采用BLEU，但BLEU在诗歌上可能不敏感。
- **公平性**：对比方法均使用相同的基础模型（如ChatGPT/GPT-4），RAT基于ChatGPT，但未明确是否对对比方法也使用了相同的基础模型设置（如温度、最大长度）。不过，RAT是唯一额外使用外部知识的方法，对比方法均未使用知识库，因此对比合理。

## 6. 论文的主要结论与发现

1. **现有LLM在古典诗歌翻译中表现不足**：在PoetMT基准上，即使是GPT-4也难以同时保证充分性、流畅性和优雅性。传统自动指标（BLEU、COMET、BLEURT）与人工判断相关性极低，而基于GPT-4的LLM指标相关性高（Pearson r=0.85 for LLM-BM）。
2. **RAT方法显著提升翻译质量**：在几乎所有指标上，RAT均优于所有基线方法。例如，在GPT-4上RAT的LLM-Avg达到4.0（基线最高3.8），BLEU-4从1.7提升到2.2。
3. **充分性方面**：RAT在句子级充分性测试中ACC达69.9%（直接翻译为60.5%），Human-BM达3.9（基线最高3.8）。
4. **知识类型的影响**：现代汉语翻译知识贡献最大，但多知识集成（RAT）优于仅用单类知识。
5. **不同诗歌类型难度差异**：唐诗相对易译（结构严谨、简短），宋词和元曲更难保持形式与韵律。
6. **数据污染风险低**：PoetMT诗歌不太可能被包含在LLM训练数据中（BLEU得分极低）。
7. **主要错误类型**：多义词处理、缺乏文化背景、长句结构混乱、低频词汇翻译错误。

## 7. 优点

- **任务新颖**：首次提出古典诗歌翻译的专门基准（PoetMT），填补了LLM评估在该领域的空白。
- **评价体系创新**：基于“充分性、流畅性、优雅性”三维度设计自动评估指标（LLM-BS/BF/BM），与人工高度相关，优于传统指标。
- **方法实用有效**：RAT通过检索外部知识显著提升翻译质量，且无需额外训练，可即插即用。
- **实验全面**：涵盖多种LLM、多种对比方法、多维度评估（传统+LLM+人工）、消融、错误分析等，结论扎实。
- **数据集开源**：PoetMT数据集基于公共领域诗歌，将开源发布，促进后续研究。

## 8. 不足与局限

- **评估指标的主观性**：尽管LLM指标与人工相关高，但“优雅性”本身主观性强，人工评估可能存在个体差异（虽进行了校准，但未报告信度指标如Cohen's Kappa）。
- **知识库构建依赖现代汉语**：知识库中的现代汉语翻译、分析等可能引入自身偏差，影响翻译结果。
- **计算成本**：RAT涉及多次调用LLM（检索、选择、翻译、投票、提取），计算开销较大；文中未报告实际推理时间或成本。
- **泛化性**：实验仅针对古典中文诗歌英译，是否适用于其他文学体裁或语言对（如法语诗歌英译）未知。
- **RAT依赖外部知识库**：知识库覆盖范围有限（30,000条），对于冷门或未收录的诗歌可能无法提供有效知识。
- **实验局限性**：
  - 人工评估仅50个样本，样本量较小。
  - 未对比RAT与其他检索增强翻译方法（如直接使用知识库进行prompt）。
  - 未评估RAT在不同基础模型（如GPT-4）上的表现差异是否因模型而异（RAT主要基于ChatGPT）。
  - 消融实验仅针对ChatGPT，未在其他模型上验证。
- **版权声明**：虽然称诗歌在公共领域，但翻译（许渊冲译文）可能存在版权问题，需确认。
- **未涉及多参考翻译评估**：主实验中BLEU仅使用单个参考译文，虽然附录中做了多参考测试但未纳入主要结论。

（完）

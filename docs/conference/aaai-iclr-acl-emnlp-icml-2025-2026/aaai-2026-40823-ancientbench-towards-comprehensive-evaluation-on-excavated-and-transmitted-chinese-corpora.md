---
title: "AncientBench: Towards Comprehensive Evaluation on Excavated and Transmitted Chinese Corpora"
title_zh: "AncientBench:面向出土与传世中国文献的综合评估"
authors: "Zhihan Zhou, Daqian Shi, Rui Song, Lida Shi, Xiaolei Diao, Hao Xu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40823/44784"
tags: ["query:ancient-text"]
score: 9.0
evidence: 古代文献评估基准，涵盖出土与传世文献
tldr: 现有中文基准主要针对现代汉语和传世古文，缺乏对出土文献的评估。AncientBench填补了这一空白，从字形、语义等多维度评估大模型对古代文字的理解能力。该基准为数字人文研究提供了标准化的评测体系，推动了古籍数字化处理技术的进步。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基准忽略出土文献，需要专门评估大模型对古代文字的理解能力。
method: 构建包含出土和传世文献的多维基准，设计字形、语义等评估维度。
result: 提供标准化的评测指标，可评估大模型在出土文献上的表现。
conclusion: 该基准填补了出土文献评估空白，对古籍数字人文研究具有重要意义。
---

## Abstract
Comprehension of ancient texts plays an important role in archaeology and understanding of Chinese history and civilization. The rapid development of large language models needs benchmarks that can evaluate their comprehension of ancient characters. Existing Chinese benchmarks are mostly targeted at modern Chinese and transmitted documents in ancient Chinese, but the part of excavated documents in ancient Chinese is not covered. To meet this need, we propose the AncientBench, which aims to evaluate the comprehension of ancient characters, especially in the scenario of excavated documents. The AncientBench is divided into four dimensions, which correspond to the four competencies of ancient character comprehension: glyph comprehension, pronunciation comprehension, meaning comprehension, and contextual comprehension. The benchmark also contains ten tasks, including radical, phonetic radical, homophone, cloze, translation, and more, providing a comprehensive framework for evaluation. We convened archaeological researchers to conduct experimental evaluations, proposed an ancient model as baseline, and conducted extensive experiments on the currently best-performing large language models. The experimental results reveal the great potential of large language models in ancient textual scenarios as well as the gap with humans. Our research aims to promote the development and application of large language models in the field of archaeology and ancient Chinese language.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：现有中文NLP基准（如MMLU、CMMLU、CLUE等）主要评估现代汉语或传世古文的理解能力，完全忽略了**出土文献**（甲骨文、金文、楚简等）。这些文献具有原始、真实、未经过后世传抄篡改的特点，对于研究古代汉字和历史文化至关重要。目前大语言模型（LLM）对出土文献的理解能力缺乏系统评估。
- **研究动机**：填补评估空缺，构建一个涵盖传世文献和出土文献的全面基准，以推动LLM在考古学和古文字研究中的应用。
- **整体含义**：提出AncientBench，首次将出土文献纳入NLP评估体系，定义了古文字理解的四个核心能力（字形、读音、语义、语境），并构建了10个子任务的标准测试集。

### 2. 方法论：核心思想、关键技术细节
- **核心思想**：从**能力维度**和**任务层级**两个角度设计基准。能力维度包括：字形理解、读音理解、语义理解、语境理解；任务层级从字符级（字形/读音）到词语级（语义）再到句子级（语境），难度递增。
- **关键技术细节**：
  - **古文字数字化三阶段方法**：
    1. 图像处理：通过计算机视觉提取每个古文字部件的特征信息和空间关系，构建古文字知识图谱。
    2. 统一字体编码：从字体库提取字形和编码信息，去重，形成集成的字符编码表。
    3. 缺失字符新编码：将图像处理获得的字形信息与字符编码表比对，对已存在字符沿用Unicode，对未记录字符则生成新Unicode编码。
  - **数据来源**：甲骨文、金文、楚简、《说文解字》、《汉语大字典》以及一系列先秦传世文献。
  - **题目构建原则**：
    - 统一评价标准：所有任务均为选择题。
    - 难度分层：依据任务类型、数据年代、选项设计区分难度。例如，甲骨文部件的识别比战国文字更难；正确选项的干扰项由相似意义的部件替换生成。
    - 权威性：邀请考古领域专家对题目进行审核。
- **算法流程**（文字说明）：
  1. 获取古文字图像 → 2. 提取部件特征与空间关系 → 3. 生成字符知识图谱 → 4. 重建矢量图 → 5. 与现有字体编码表比对去重 → 6. 缺失字符分配新编码 → 7. 整合完整的字符编码表 → 8. 基于该编码表构建10个任务的选择题。

### 3. 实验设计：数据集/场景、Benchmark、对比方法
- **数据集/场景**：
  - **AncientBench**：共28,707道选择题，覆盖10个任务（部首识别、部首含义、读音识别、声旁识别、同音字识别、出土文献词语理解、传世文献词语理解、完形填空、通假字识别、翻译）。数据主要来自先秦时期（夏、商、周、春秋、战国），侧重甲骨、金文、楚简。
  - **场景**：零样本（zero-shot）和少样本（few-shot，5样本）两种评估。
- **Benchmark**：AncientBench自身作为基准，包含四个能力维度和10个任务。
- **对比方法**：
  - **人类表现**：邀请5名考古与人工智能交叉领域的研究生完成50道题（每个任务5题），取平均准确率和答题时间。
  - **LLM模型（共9个）**：
    - Llama-3-8B-Instruct
    - GLM-4-9b-Chat
    - Qwen-7B/14B-Chat
    - Baichuan2-7B/13B-Chat
    - Yi-1.5-9B-Chat
    - Xunzi-Qwen-Chat
    - Tonggu-7b-Chat
    - Yi-1.5-9B-Ancient（本文提出的微调模型）
  - **本文提出的基线模型（Ancient Model）**：在Yi-1.5-9B-Chat基础上使用自建的问答对数据集进行全参数微调，获得Yi-1.5-9B-Ancient。

### 4. 资源与算力
- 文中明确说明：所有实验在运行Ubuntu操作系统、配备**ascend-d910b NPU**（华为昇腾910B）的机器上执行。
- 微调设置：batch size = 2，学习率 = 1e⁻⁵。但未提及使用的具体NPU数量、训练时长（epoch数等）。未提供零样本和少样本推理的算力配置。

### 5. 实验数量与充分性
- **实验数量**：
  - 零样本：9个LLM + 人类 + 1个微调模型，在10个任务上报告平均准确率（共10+1=11组零样本结果）。
  - 少样本：同样9个LLM + 人类 + 1个微调模型，报告10个任务的平均准确率（共11组少样本结果）。
  - 微调模型训练：1组（使用了全参数微调）。
  - 缺失消融实验：未进行针对不同微调数据量、不同基座模型、不同训练策略的消融。
- **充分性判断**：
  - 优势：覆盖多种主流中文LLM，对比了人类表现，区分了零样本和少样本。任务设计涵盖古文字理解的多个维度，较为全面。
  - 不足：仅使用了一块NPU（文中“executed on the machine”暗示单机），未说明训练轮次；未进行超参数调优实验；未评估模型规模对结果影响的统计显著性；未设计混淆因素控制（如选项顺序）。总体而言，实验设计基本合理，但缺乏深入的消融分析和统计验证，客观性尚可，公平性因无随机化或并行运算可能略有偏差。

### 6. 主要结论与发现
- LLM在AncientBench上的平均准确率低于人类（人类55.13%，最佳LLM Qwen-14B-Chat为51.00%）。
- **字形和读音理解**：LLM与人类差距巨大（人类分别76.66%和50.00%，最佳模型分别为53.01%和31.70%），说明LLM缺乏对古文字形音信息的有效编码。
- **语义理解**：LLM反而超过人类（GLM4-9b-chat达69.71%，人类仅38.33%），可能因为该任务更依赖记忆力，而非视觉识别。
- **语境理解**：两者差距不明显（人类55.55%，最佳模型Llama3-8B-Instruct达62.41%）。
- **参数规模**：增大参数规模（如14B vs 7B）有助于提升语义和语境理解，但对字形和读音提升有限。
- **微调效果**：提出的Yi-1.5-9B-Ancient在零样本下平均分达50.28%，优于相同规模的其他模型（Yi-1.5-9B-Chat为48.81%），但在语境理解上略有下降，说明微调可能部分损害原有 embedding。
- **少样本提升**：多数模型在少样本下性能微升（如Yi-1.5-9B-Chat提升1.99%），但Baichuan2和Qwen系列反而下降，表明模型对少量示例的适应能力不一。

### 7. 优点（方法或实验设计亮点）
- **首次引入出土文献**：在NLP评估中填补了该类文献的空白，具有开创性。
- **多维能力设计**：从字形、读音、语义、语境四个维度系统评估，覆盖字符、词语、句子多个层次。
- **数字化方法创新**：提出三阶段数字化+新编码策略，解决了出土文献字符在计算机中无法表示或编码冲突的问题。
- **题目构建精细化**：通过替换相似部件生成干扰项，提升题目难度区分度；并邀请考古专家审核，保证权威性。
- **人类基线**：提供了考古领域研究人员的表现作为参照，使评估更贴近实际应用需求。
- **基线模型**：微调出一个专门的古文字模型，验证了古文字知识注入的有效性，为后续研究提供基准。

### 8. 不足与局限
- **实验覆盖不全**：
  - 只评估了9个LLM，未覆盖更新更大的模型（如GPT-4、Claude、DeepSeek等闭源模型）。
  - 未对微调策略进行消融（如不同数据量、不同训练步数、不同学习率）。
  - 少样本设置仅用了5个示例，未探究不同shot数的影响。
- **偏差风险**：
  - 数据来源偏重先秦时期，可能无法代表全部出土文献。
  - 题目选项设计人为构造干扰项，存在主观偏好。
  - 人类评估样本量小（仅5人，每人50题），统计显著性可能不足。
- **应用限制**：
  - 选择题格式限制了评估形式，无法全面反映模型生成或解释能力。
  - 数字化方法依赖图像处理，对于模糊或残缺的古文字效果未知。
  - 微调模型在语境理解上出现性能下降，说明知识注入可能破坏原始表示，需要更鲁棒的方法。
- **计算资源信息不足**：未提供微调的总时长、能耗等，不利于可重复性。

（完）

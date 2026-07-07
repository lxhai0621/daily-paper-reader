---
title: "RACQC: Advanced Retrieval-Augmented Generation for Chinese Query Correction"
title_zh: RACQC：面向中文查询纠错的先进检索增强生成技术
authors: "Jinbo Su, Lingzhe Gao, Wei Li, Shihao Liu, Haojie Lei, Xinyi Wang, Yuanzhao Guo, Ke Wang, Daiting Shi, Dawei Yin"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.36.pdf"
tags: ["query:ma-kf"]
score: 10.0
evidence: 基于检索增强生成的中文查询纠错系统
tldr: 该论文提出RACQC系统，将检索增强生成（RAG）与多任务学习相结合，用于中文查询纠错。通过实体中心化RAG引入动态知识检索，解决了大语言模型在开放域中对罕见实体泛化差和时变实体适应不良的问题。实验表明该系统显著减少了过度纠正，提升了查询准确性和用户搜索体验。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.36/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.36/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1598, \"height\": 625, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.36/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 538, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 771, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1657, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 823, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 567, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 712, \"height\": 126, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 709, \"height\": 126, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.36/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 778, \"height\": 174, \"label\": \"Table\"}]"
motivation: 现有LLM在中文拼写检查中难以处理罕见实体和时变实体，导致过度纠正，用户体验差。
method: 构建实体中心化检索增强生成（RAG）模块，结合多任务学习，动态检索相关知识以纠正查询错误。
result: 在开放域搜索数据集上，RACQC显著降低了过度纠正率，提升了罕见实体和时间敏感实体的纠正准确率。
conclusion: RAG技术可有效提升中文查询纠错系统的泛化能力和时效性，对搜索引擎优化有重要价值。
---

## Abstract
In web search scenarios, erroneous queries frequently degrade users’ experience through irrelevant results, underscoring the pivotal role of Chinese Spelling Check (CSC) systems. Although large language models (LLMs) exhibit remarkable capabilities across many tasks, they face critical challenges in the CSC scenario: (1) poor generalization to rare entities in open-domain searches, and (2) failure to adapt to temporal entity variations due to static parameters, resulting in serious over-correction issues. To tackle this, we present RACQC, a C hinese Q uery C orrection system with R etrieval- A ugmented Generation (RAG) and multi-task learning. Specifically, our approach (1) integrates dynamic knowledge retrieval through entity-centric RAG to address rare entities and innovatively proposes an entity-title collaborative corpus, and (2) employs contrastive correction tasks to mitigate LLM over-correction tendencies. Furthermore, we propose MDCQC, a M ulti- D omain C hinese Q uery C orrection benchmark to test the model’s entity correction capabilities. Extensive experiments on several datasets show that RACQC significantly outperforms existing baselines in CSC tasks. Specifically, RACQC achieves a maximum improvement of +9.92% on the search scenario benchmark and +3.2% on the general-domain dataset under the F 1 metric.

---

## 论文详细总结（自动生成）

# RACQC：面向中文查询纠错的先进检索增强生成技术——论文总结

## 1. 核心问题与研究动机
- **背景**：在真实网络搜索场景中，用户常因输入错误或知识缺失提交错误的查询（如同音字、形近字、多字少字等），导致搜索结果与用户意图严重偏离。中文拼写检查（Chinese Spelling Check, CSC）系统旨在检测并纠正此类错误，对搜索引擎至关重要。
- **核心问题**：大语言模型（LLM）在CSC任务上面临两大挑战：
  - **对开放域中罕见实体泛化差**：LLM对长尾或新出现的实体（如动漫角色、新上映影视剧）缺乏知识。
  - **无法适应实体随时间变化**：由于参数静态，LLM倾向于**过度纠正**（over-correction），将正确的非常见实体误改为常见词，严重破坏用户体验。
- **现有不足**：主流CSC方法（BERT类、Seq2Seq、LLM）在真实搜索场景下效果不佳，且缺乏针对实体级纠错的公开基准。

## 2. 方法论
### 2.1 总体框架：RACQC
RACQC（Retrieval-Augmented Generation for Chinese Query Correction）将检索增强生成（RAG）与多任务学习相结合，包含两个训练阶段：
- **第一阶段：多任务训练**——通过五种互补的纠错任务增强LLM的基础CSC能力。
- **第二阶段：有监督微调（SFT）与推理**——利用实体-标题语料库进行RAG，为LLM提供外部知识，减少过度纠正。

### 2.2 多任务训练数据（五种任务）
1. **错误检测（Error Detection）**：二分类任务，判断查询是否包含错误（标签 `Ded(s) ∈ {0,1}`）。
2. **纠错评分（Error Correction Scoring）**：二分类任务，判断给定候选纠错结果是否正确（标签 `Decs(s,c) ∈ {0,1}`）。
3. **纠错生成（Error Correction Generation）**：输入错误查询，输出所有正确纠错结果中的任意一个。
4. **纠错重排序（Error Correction Re-ranking）**：从多个候选（至少4个，含正例和负例）中选出最佳结果。
5. **思维链（Chain of Thought, CoT）**：利用GPT-4生成纠错思考过程并人工复核，让模型学习复杂场景下的推理步骤。

**负样本生成算法（Algorithm 1）**：基于混淆集（从在线场景挖掘），通过随机替换或交换字符生成负例。

### 2.3 检索增强生成（RAG）技术细节
- **语料库构建**：从WuDao数据集及真实线上数据中提取**网页标题**及其中的**命名实体**，经过NER提取和二次验证（实体在相似标题中出现≥5次才保留），构建**实体-标题协同语料库**。
- **检索方法**：使用bge-large-zh-v1.5模型对查询进行向量化，在语料库中检索余弦相似度最高的**前4条**结果。
- **整合方式**：在SFT和推理阶段，将检索到的语料信息作为上下文输入LLM，增强其对罕见和时变实体的识别能力。

### 2.4 提出的基准：MDCQC
- **Multi-Domain Chinese Query Correction benchmark**：源自真实搜索引擎查询日志，经人工标注，涵盖10个领域（F&G、MED、NEW、LIF、EDU、BOK、CAR、MUS、TEC、OTHER），共4000+条样例，包含**实体级错误**和**长度不匹配错误**，专为测试模型在真实搜索场景中的实体纠错能力而设计。

## 3. 实验设计
### 3.1 使用数据集
| 数据集 | 类型 | 规模/领域 |
|--------|------|-----------|
| LEMON | 通用CSC数据集 | 7个领域（GAM、ENC、COT、MEC、CAR、NOV、NEW） |
| MCSC | 医学领域CSC数据集 | 来自搜索日志的专业标注 |
| MDCQC | 本文提出的多领域搜索场景基准 | 10个领域，4000+条 |

### 3.2 对比方法
- **传统方法**：N-gram语言模型（KenLM）
- **BERT类模型**：BERT、Soft-Masked BERT
- **闭源LLM**：GPT-4、ERNIE-4.0
- **近期LLM方法**：TIPA（基于Qwen2-1.5B的字符级对齐方法）
- **本文方法变体**：
  - RACQC（完整系统，base model为Qwen2-1.5B）
  - RACQC w/o RAG（去掉RAG模块）
  - Qwen2-1.5B+SFT+RAG（直接SFT+RAG）
  - RACQC迁移至LLAMA3-1B

### 3.3 评估指标
- 精确率（P）、召回率（R）、F1分数（F1），按字符级别计算。

## 4. 资源与算力
- **GPU**：所有实验在**8张NVIDIA A100 80GB GPU**上进行。
- **训练细节**：多任务训练1个epoch，SFT训练3个epoch；Adam优化器，初始学习率1e-5，batch size 64。
- **未明确说明总训练时长**，但提及使用40M样本进行多任务训练（1:1正负比），400K样本用于SFT阶段。

## 5. 实验数量与充分性
- **主实验**：在MDCQC、MCSC、LEMON三个数据集上对比多个基线，报告P/R/F1。
- **消融实验**（第5.1节）：逐一移除五种多任务任务（ec gene、ec scoring、ed、ec rerank、CoT），观察性能变化。
- **语料库构建实验**（第5.2节）：对比实体-only、标题-only、实体-标题三种语料配置的影响。
- **迁移性实验**（第5.3节）：将base model从Qwen2-1.5B替换为LLAMA3-1B，验证方法通用性。
- **效率分析**（第5.4节）：对比RACQC与各基线的平均延迟，并报告线上优化效果（4.14倍加速）。
- **案例研究**（第5.5节）：展示两个具体纠错案例，说明RAG如何帮助纠正长尾实体。
- **线上实验**（第5.6节）：在真实搜索引擎上部署，采用Query变化率、跳出率、用户满意度三个指标进行A/B测试。
- **补充分析**：在附录中进一步分析长尾/时变实体分布（表9）、过度纠正缓解情况（表10）。

**充分性评价**：实验覆盖全面，既包含离线标准评测，也包含线上真实效果验证；消融实验细致（5个子任务逐一去除）、语料类型对比（3种）、模型迁移验证（2种base model）、效率优化验证，且所有结果均以公平的metric呈现。唯一欠缺的是未报告多次实验的标准差，但整体设计严谨、结论可靠。

## 6. 主要结论与发现
1. **RACQC在三个数据集上均达到SOTA**：在搜索场景基准MDCQC上F1提升+9.92%，在通用数据集LEMON上F1提升+3.2%。
2. **多任务训练显著增强LLM的CSC能力**：五种任务相互补充，其中纠错生成任务最重要（移除后性能下降最大）。
3. **RAG有效缓解过度纠正**：在MDCQC和MCSC上RAG带来显著提升（+5~10% F1），但在LEMON上提升有限（因LEMON中大多数实体常见，LLM已能覆盖）。
4. **实体-标题协同语料最优**：仅用实体或仅用标题效果均不如两者结合。
5. **方法可迁移**：将base model从Qwen2-1.5B换成LLAMA3-1B后仍保持显著优势。
6. **线上部署有效**：QCR降低1%，BR提升1.5%，USR提升1.15%，用户搜索体验得到改善。

## 7. 优点
- **问题针对性极强**：精准定位LLM在CSC中的过度纠正问题，并设计了实体中心化的RAG方案解决罕见实体和时变实体。
- **多任务学习设计新颖**：五种任务覆盖了从检测、评分、生成、重排序到推理链的完整纠错流程，且消融证实了每个任务的必要性。
- **语料构建有创新**：实体-标题协同语料同时利用了标题的丰富上下文和实体的精确性，并通过二次验证保证质量。
- **实验全面且贴近真实场景**：不仅使用通用基准，还构建了真实搜索日志的MDCQC基准，并进行了线上部署验证。
- **效率优化实际**：通过INT-8量化、缓存、大小模型协作等策略，使系统满足线上低延迟要求。

## 8. 不足与局限
- **语言局限性**：仅针对中文，对英文或其他语言的纠错可能不适用（论文明确提及）。
- **检索策略相对简单**：仅采用文本向量化+余弦相似度检索，更先进的方法（如知识图谱检索）可能进一步提升性能。
- **多任务训练增加额外开销**：需要人工构造五种任务的数据（40M样本），训练代价较大，未来需改进效率。
- **实验覆盖偏差**：MDCQC基准虽来自真实搜索日志，但仅选取“线上系统难以处理的代表性查询”，样本可能存在偏向，不一定代表整体分布。此外，未报告统计显著性检验（如p值）。
- **对LLM基座模型依赖**：虽然迁移实验验证了通用性，但最终性能仍受基座模型能力制约（如GPT-4在零样本下表现不佳）。
- **RAG依赖语料库质量**：语料库需定期更新以覆盖新实体，维护成本较高。

（完）

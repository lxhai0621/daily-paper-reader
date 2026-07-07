---
title: "Dialogue-RAG: Enhancing Retrieval for LLMs via Node-Linking Utterance Rewriting"
title_zh: 对话式RAG：通过节点链接话语重写增强大语言模型检索
authors: "Qiwei Li, Teng Xiao, Zuchao Li, Ping Wang, Mengjia Shen, Hai Zhao"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1191.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过话语重写增强对话RAG检索
tldr: 针对对话中省略与指代导致RAG检索不准确的问题，本文提出Dialogue-RAG，采用节点链接迭代推理的不完整话语重写方法，补全关键信息以增强检索。实验证明该框架有效提升检索精度和生成质量，为对话RAG提供高效解决方案。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 955, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1493, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 783, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 781, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 779, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 812, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1191/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 810, \"height\": 641, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1627, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 727, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 804, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1629, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1653, \"height\": 448, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 691, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1191/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1499, \"height\": 597, \"label\": \"Table\"}]"
motivation: 对话场景中省略和指代现象导致RAG检索不准确。
method: 提出轻量级节点链接迭代推理模型，进行不完整话语重写以补全关键信息。
result: 在多个对话数据集上提升了检索准确率和生成质量。
conclusion: 对话RAG通过话语重写可有效缓解模糊信息问题。
---

## Abstract
Large Language Models (LLMs) and Retrieval Augmented Generation (RAG) methods have demonstrated significant potential on tasks across multiple domains. However, ellipses and coreferences, as common phenomena in dialogue scenes, pose challenges to LLMs’ understanding and RAG’s retrieval accuracy. The previous works ignore the negative impact of this fuzzy data on RAG system.We explore the capabilities of LLMs and RAG systems in dialogue scenarios and use Incomplete Utterance Rewriting (IUR) to complete the key information in dialogue to enhance retrieval.Besides, we propose a lightweight IUR model for query rewriting. It is an end-to-end framework for node linking and iterative inference, incorporating two newly proposed probing semantic features derived from generative pre-training. This framework treats IUR as a series of link decisions on the input sequence and the incrementally constructed rewriting outputs.To test the performance of RAG system in the model multi-round dialogue scenario, we construct an RAG dialogue dataset on English and Chinese, Dialogue-RAG-MULTI-v1.0.Experiment results show that utterance rewriting can effectively improve the retrieval and generation ability of RAG system in dialogue scenes. Experiments on IUR tasks demonstrate the excellent performance of our lightweight IUR method.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：在对话场景中，省略（ellipsis）和指代（coreference）现象频繁出现，导致用户查询不完整或模糊。这既影响大语言模型（LLM）对语义的准确理解，也严重降低检索增强生成（RAG）系统的检索准确率，进而影响生成质量。前人工作忽视了这种模糊数据对RAG系统的负面影响。
- **研究动机**：通过不完整话语重写（Incomplete Utterance Rewriting，IUR）补全对话中的关键信息，增强RAG的检索能力，从而提升整体对话问答性能。
- **整体含义**：提出 **Dialogue-RAG** 框架，将IUR作为增强RAG检索的前置模块，并设计轻量级IUR模型实现高效重写，同时构建中英文对话RAG数据集以填补评估空白。

## 2. 方法论
### 核心思想
- 将对话历史与当前不完整话语作为输入，通过轻量级IUR模型生成自包含的完整查询，再用该查询进行知识库检索，最后将检索结果与重写后查询拼接为提示模板，输入LLM生成答案。
- IUR模型将重写任务转化为**有向图解析**任务，通过节点链接（node linking）确定上下文中的短语跨度（span link）和插入位置（insertion link），从而以低复杂度完成重写。

### 关键技术细节
- **有向图建模**：将上下文和话语拼接为序列，每个词视为节点。定义两种链接：span link（确定待插入短语在上下文中的起止词）和insertion link（确定插入位置的话语左端词）。总复杂度从 \(O(m \times m \times n)\) 降至 \(O((m+n)^2)\)。
- **节点链接解析器**：使用双线性注意力（biaffine scorer）对头尾节点对进行评分，通过多类交叉熵损失训练链接标签（span、insert、NONE）。
- **上下文相似性特征（CSF）**：基于GPT的生成式语言模型，计算上下文生成分布与插入位置生成分布的KL散度，衡量某位置词插入的合理性。
- **重写一致性特征（RCF）**：利用GPT预测概率，评估插入词与局部片段形成有效句子的可能性。
- **特征集成**：CSF和RCF分别扩增至 \((m+n) \times (m+n)\) 维度，加到双线性评分中，帮助模型决策。

### 算法流程文字说明
1. 输入对话历史 \(U_c\) 和当前话语 \(u_i\)，拼接为单序列。
2. 通过序列编码器（BiLSTM或Transformer）得到上下文表示。
3. 使用两个独立FFN分别映射出头节点和尾节点表示。
4. 计算双线性得分，并加上CSF和RCF，得到每个头尾对的关系标签概率。
5. 根据解析出的span link和insertion link，从上下文中提取短语插入到话语指定位置，生成重写后的完整查询 \(Ru_i\)。
6. 计算 \(Ru_i\) 与知识库所有分块的余弦相似度，选取Top-k分块。
7. 将重写查询与检索内容拼接为提示模板，输入LLM生成最终回答。

## 3. 实验设计
### 数据集
- **自建对话RAG数据集**：Dialogue-RAG-MULTI-v1.0（中英双语），包含多轮问答对和检索知识库。训练集约24k轮对话/226k问答对，测试集约1k轮对话/8k问答对，其中省略/指代比例超过60%。
- **IUR任务数据集**：CANARD（英文任务导向对话）、REWRITE（中文开放域对话）、MULTI（英文多轮）、TASK（中文任务型）。
- **检索对比数据集**：CoQA、TOPIOCQA、OR-QuAC。

### Benchmark与对比方法
- **RAG系统对比**：无IUR/无RAG、RAG w/o IUR、RAG w/ GPT-4o-mini few-shot IUR、GLM-RAG、AAR、Adaptive-RAG、IRCot、DRAGON+。
- **IUR任务对比**：传统模型（L-Ptr、L-Ptr-Gen、RUN等）、LLM（Qwen2-7B、ChatGLM3-6B、DeepSeek-V3、GPT-4o-mini）的zero-shot/few-shot。
- **评估指标**：BLEU、ROUGE、BERTScore（RAG）；BLEU、ROUGE、EM（IUR）；检索：Accuracy、Recall、MRR@5。

## 4. 资源与算力
- 文中提及：
  - 非LLM模型在单块 **GeForce RTX 3090** 显卡上测试。
  - LLM模型（如Qwen2.5-7B、ChatGLM3-6B、Llama3-8B）部署在 **两张GeForce RTX 3090** GPU上。
  - 训练使用Adam优化器，最大200个epoch，早停策略。
- **未明确说明**：具体训练时长、总GPU小时数、分布式训练细节等。因此无法量化总算力消耗。

## 5. 实验数量与充分性
- **实验组数**：涵盖多个维度。
  - 主RAG结果（表2）：8种方法对比，含消融。
  - 检索对比（图3）：3个数据集上两种设置。
  - IUR任务（表3、4、8、9）：超过10种基线，覆盖不同语言/领域。
  - 消融实验（表5、6）：CSF/RCF特征、有向图建模。
  - 重写速度对比（图4）。
  - 不同基座模型实验（附录表7）：Qwen2.5和Llama3。
  - 案例分析（附录表10）。
- **充分性评估**：
  - **充分**：数据集多样（4个IUR数据集+3个检索数据集+1个自建RAG数据集），基线覆盖传统SOTA和主流LLM，消融验证特征有效性，速度测试体现效率优势。
  - **公平**：与已有方法采用相同数据划分，复现设置一致；LLM使用相同few-shot样本数（3）进行对比。
  - **客观**：自动指标（BLEU、ROUGE、EM、BERTScore）公开可量化，案例定性展示差异。

## 6. 主要结论与发现
1. **话语重写显著提升RAG性能**：使用IUR后，检索准确率从37.80%提升至77.54%，GPT-4评分从4.89提升至7.70。
2. **轻量级IUR模型优于LLM方案**：所提节点链接模型在IUR任务（CANARD、REWRITE）上全面超越传统模型和LLM few-shot结果，且速度快（比RUN快3倍以上，比LLM快数十倍）。
3. **CSF和RCF特征的有效性**：消融实验验证两个特征对解析质量和最终改写效果均有正向贡献。
4. **有向图建模降低复杂度**：将IUR转化为有向图解析，大幅简化推理，使模型高效且轻量。
5. **新数据集填补评估空白**：Dialogue-RAG-MULTI-v1.0提供含省略/指代的真实对话RAG测试环境。

## 7. 优点
- **方法创新性**：首次将有向图解析引入IUR，并设计两种基于GPT的探测特征（CSF、RCF），无需额外训练即可辅助链接决策。
- **效率优越**：轻量级模型（BiLSTM+小网络），重写速度远超LLM，适合RAG流水线中对延迟敏感的场景。
- **实验全面**：覆盖多语言、多领域、多任务，消融严谨，案例充实。
- **数据集贡献**：手动构建中英文多轮对话RAG数据集，含高比例模糊现象，为后续研究提供基准。
- **实践意义**：直接解决对话RAG中的实际痛点，可即插即用于现有RAG系统。

## 8. 不足与局限
- **实验覆盖偏差**：
  - 仅测试了基于ChatGLM3-6B的主RAG结果，虽在附录补充了Qwen2.5和Llama3，但主要结论依赖单一基座模型，泛化性待验证。
  - 检索结果对生成的负面影响未被深入探讨（如错误改写反而误导LLM），论文limitation部分已承认。
- **方法局限**：
  - 当前仅处理插入式改写，无法处理需要生成新词（非上下文词）的情况，需额外后处理（如语法纠错）。
  - CSF/RCF特征依赖GPT模型，虽轻量但仍需预训练模型推理，引入一定计算开销。
- **数据集局限**：
  - 自建数据集的训练/开发集由DeepSeek-V3生成后人工审核，可能存在噪声。
  - 知识库仅基于网页爬取，领域覆盖有限。
- **应用限制**：
  - 对于极短或极长的对话上下文，有向图建模的复杂度依然可能成为瓶颈。
  - 未考虑对话中多义词、跨轮长程指代等更复杂情形。

（完）

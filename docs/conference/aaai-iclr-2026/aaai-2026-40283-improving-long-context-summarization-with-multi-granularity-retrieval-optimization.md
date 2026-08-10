---
title: Improving Long-Context Summarization with Multi-Granularity Retrieval Optimization
title_zh: 通过多粒度检索优化改进长上下文摘要
authors: "Xueyu Chen, Kaitao Song, Zifan Song, Dongsheng Li, Cairong Zhao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40283/44244"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于多粒度摘要优化的检索增强生成，提升RAG准确性和文档级连贯理解
tldr: 现有RAG通常基于孤立片段检索，难以整合文档内部信息，限制了长文档连贯理解任务的性能。受人类阅读时逐步整合已有知识的认知过程启发，本文提出层级式两阶段摘要信息检索方法HTSIR，先在文档内进行多粒度摘要检索，再基于摘要信息回答查询。实验证明该方法在长上下文摘要和问答任务上显著优于基线RAG，为提升RAG准确性和相关性提供了有效技术方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40283/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 856, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40283/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1811, \"height\": 778, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40283/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1819, \"height\": 430, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 880, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 879, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 876, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 871, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 877, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 873, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 861, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40283/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1819, \"height\": 227, \"label\": \"Table\"}]"
motivation: RAG基于孤立片段响应查询，缺乏文档内信息整合，长文档理解性能受限。
method: 提出HTSIR方法，采用层级两阶段摘要信息检索，将多粒度文档摘要融入检索生成流程。
result: 在长上下文摘要与问答任务上显著提升RAG性能，超越基线检索增强方法。
conclusion: 模拟人类整合式阅读的层级摘要检索能有效弥补现有RAG在文档级理解上的不足。
---

## Abstract
Retrieval-Augmented Generation (RAG) is an effective solution to overcome the limitations of Large Language Models (LLMs) in terms of specific-domain knowledge and timely information updates. However, current RAG methods typically respond to queries based on isolated segments, lacking the ability to integrate information within the same document. This undermines performance in real-world tasks requiring coherent understanding across an entire document. Notably, the human brain naturally integrates and summarizes prior knowledge upon reading a given text, progressively formulating a comprehensive understanding. Motivated by this cognitive process, we propose the Hierarchical Two-Stage Summarization-based Information Retrieval (HTSIR) method, which preprocesses the corpus prior to retrieval, summarizes continuous texts to obtain integrated information, and constructs a retrieval tree with varying summary granularities. The retrieved information is then processed by a Reranker based on the current question to serve as a context for LLMs. Additionally, as single-step summarization is often imprecise in query-based summarization tasks, we further apply a Refinement module, allowing LLMs to reflect and revise their output to achieve the final result. By combining HTSIR with GPT-4o mini, we achieve state-of-the-art results on complex question tasks across four long-text datasets (NarrativeQA, QASPER, QuALITY, and QMSum), achieving an improvement of about 6 points on the Question Answering (QA) task in QuALITY-HRAD.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLMs）在生成式AI领域取得了显著成就，但在专业领域知识和最新信息更新方面存在固有局限。检索增强生成（RAG）通过将生成模型与信息检索技术相结合，有效弥补了这些不足。
- **核心问题**：现有RAG方法通常基于**孤立的文本片段**响应查询，缺乏对同一文档内信息的整合能力。具体而言：
  - 传统分段方法（按固定长度、按句子、按段落切分）将文档碎片化，破坏了文本的内在逻辑和结构连贯性；
  - 长文本中存在"lost in the middle"现象，即LLM对输入中间部分信息的利用效率下降；
  - 图结构RAG方法（如GraphRAG、HippoRAG）虽然能缓解上述问题，但知识图谱构建的计算成本极高，需要大量实体关系抽取和资源密集的嵌入预训练。
- **核心洞察**：人类阅读时天然具备**渐进式整合与总结**的认知能力——先读部分文本形成局部理解，再逐步整合为全局认知。作者受此启发，认为文档本身的分层结构（如学术论文的章节划分、小说的叙事逻辑）应被视为重要信息加以利用。
- **整体含义**：本文提出HTSIR（Hierarchical Two-Stage Summarization-based Information Retrieval）方法，通过构建多粒度摘要检索树，使RAG系统能够从不同抽象层次理解和整合文档信息，从而显著提升长文档问答和摘要任务的性能。

## 2. 论文提出的方法论

### 2.1 核心思想

HTSIR的核心思想是：**利用文档自身的层级结构，通过多粒度摘要构建检索树，使检索系统能够同时捕获具体细节（叶子节点）、局部整合信息（中间节点）和全局语义（根节点）**。

### 2.2 HTSIR树构建

检索树由三类节点构成：

- **叶子节点（Leaf Node, X）**：将每个章节按固定长度l切成连续的文本块x_j^i，保留最细粒度的具体信息。
- **根节点（Root Node, S̃）**：对每个章节的整体内容进行摘要，得到粗粒度的全局信息表示。
- **中间节点（Intermediate Node, P）**：对r个连续的叶子节点块进行摘要，获得介于细粒度和粗粒度之间的中间层信息。

**两种情况处理**：

| 文档类型 | 处理方式 |
|---------|---------|
| 有清晰层级结构（如学术论文、技术报告） | 直接利用现有章节划分，对每个章节生成摘要作为根节点 |
| 无清晰层级结构（如小说、散文） | 通过LLM自动将文档划分为若干主题相近的段落，再按同样流程处理 |

### 2.3 折叠树检索策略（Collapsed Tree Search）

- 将所有层级的节点聚合到一个**统一的候选集合C**中；
- 无需逐层遍历和预设每层节点数，直接计算所有节点与查询向量的余弦相似度；
- 相比传统逐层遍历方法，该方法既可动态选择最相关节点，又具有更高的计算效率（可批量计算）。

### 2.4 重排序与响应生成

- 基于余弦相似度取出候选节点后，使用**重排序模型**（如BGE-Reranker、Cohere）重新评估查询与候选文本的语义对齐程度；
- 选择Top-k个最相关节点作为上下文输入LLM，生成最终答案。

### 2.5 反馈驱动的精炼模块（Refinement Module）

- 受self-refine方法启发，设计了可选的反饋循环：
  1. 使用LLM生成初始输出；
  2. 将输出返回给LLM获取反馈；
  3. 结合反馈再次生成，迭代直至满足需求。
- 该模块**无需额外训练**，仅通过提示工程即可实现，特别适用于对细节要求较高的摘要型QA任务。

## 3. 实验设计

### 3.1 数据集

实验覆盖了4个长文本基准数据集，涵盖问答和摘要两类任务：

| 数据集 | 任务类型 | 特点 |
|--------|---------|------|
| NarrativeQA | 阅读理解QA | 基于叙事文本的问答 |
| QASPER | 信息寻求QA | 基于研究论文的问答 |
| QuALITY | 多选QA | 长文本阅读理解（含HARD/EASY子集） |
| QMSum | 会议摘要 | 查询驱动的多领域会议摘要 |

### 3.2 基线与对比方法

- **基础检索器对比**：BM25、SBERT、DPR（各自对比有无HTSIR框架的性能差异）；
- **图结构RAG方法对比**：GraphRAG、HippoRAG、HippoRAG 2；
- **树结构RAG方法对比**：RAPTOR；
- **长序列Transformer方法**：LongRAG、VCC、LED-base + FullText；
- **开源小模型方法**：PEAR、DePaC、SCPT（均基于Llama系列）;
- **其他摘要模型**：UL2、BART-SLED。

### 3.3 评估指标

- 问答任务：Answer F1、EM（Exact Match）、Accuracy；
- 摘要任务：ROUGE-L、BLEU-1。

### 3.4 LLM后端

- 闭源模型：GPT-3.5-Turbo、GPT-4o mini；
- 开源模型：Llama3-8B（结合LoRA微调）。

## 4. 资源与算力

- **原文明确说明**："The experiments can be run on a consumer-grade computer"（实验可在消费级计算机上运行），但**未提供具体的GPU型号、数量、训练时长或显存占用**等详细信息。
- 与图结构RAG方法（GraphRAG、HippoRAG）相比，本文强调HTSIR直接处理原始文本，**无需构建知识图谱**，因此在计算资源消耗上具有显著优势。
- 但论文未提供复杂度分析（时间复杂度/空间复杂度）或具体运行时间的量化对比数据。

## 5. 实验数量与充分性

### 5.1 实验组数量

论文共报告了**约10组主要实验**：

- **表1**：NarrativeQA上三种检索器（BM25、SBERT、DPR）有无HTSIR的对比；
- **表2**：QuALITY-HARD和QASPER上三种检索器有无HTSIR的对比；
- **表3**：NarrativeQA上与图结构方法（GraphRAG、HippoRAG、HippoRAG 2）的对比；
- **表4**：QASPER上与多种先进模型的对比；
- **表5**：QASPER上开源Llama系列模型的对比；
- **表6**：QuALITY-HARD上多种模型的精度对比；
- **表7**：QMSum上摘要质量的ROUGE-L对比；
- **表8**：参数r的消融实验（QuALITY-EASY和QuALITY-HARD）；
- **表9**：树结构各节点层的贡献分析；
- **图3**：不同文本长度和分块数量对摘要生成效果的影响分析。

### 5.2 充分性评估

- **优点**：实验覆盖了多种LLM后端（闭源+开源）、多种检索器（稀疏+稠密）、多类对比方法（图结构、树结构、长序列Transformer），角度较为全面；
- **不足**：
  - 参数r的消融实验仅在QuALITY数据集上进行，缺乏在其他数据集上的验证；
  - 各数据集的模型覆盖不均衡（如QMSum上对比模型较少）；
  - 对图结构方法的比较主要引用已发表结果，未在统一实验环境中复现；
  - Refinement模块的消融分析以定性描述为主，缺少量化指标对比。

## 6. 主要结论与发现

- **HTSIR显著优于基础RAG方法**：无论搭配何种检索器（BM25、SBERT、DPR），加入HTSIR后性能在NarrativeQA、QuALITY、QASPER上均一致提升，验证了多粒度层级摘要的有效性。
- **优于图结构RAG方法**：在NarrativeQA上，HTSIR的F1达37.4%，比HippoRAG 2（25.2%）高出12.2个百分点，比GraphRAG（20.9%）高出16.5个百分点，同时计算成本更低。
- **优于其他树结构方法**：在QASPER上，HTSIR的Answer F1为36.9%，超越RAPTOR（36.7%）0.2个百分点，且不需要主题聚类。
- **在QuALITY-HARD上取得大幅提升**：HTSIR + GPT-4o mini达到74.0%的准确率，较普通GPT-4o mini（72.1%）提升约2个百分点，较此前最优方法VCC（56.0%）提升18个百分点。
- **三种节点信息互补**：单独使用叶子节点（x）或中间节点（p）虽然各自有效，但三者结合时性能最优，说明不同粒度的信息存在互补性；两层节点组合反而因信息冗余导致性能下降。
- **文本摘要长度存在最优区间**：约700-750个token的摘要输入长度可达到最佳性能，过长或过短均导致效果下降。
- **开源小模型同样适用**：使用Llama3-8B LoRA作为基础模型时，HTSIR也可带来约2个百分点的性能提升，验证了方法的通用性。

## 7. 优点

- **认知启发的创新思路**：从人类阅读时渐进式整合理解的认知过程出发，将这一机制转化为多粒度摘要检索树，理念自然且有说服力。
- **充分利用文档内在结构**：不同于一般方法将文档视为无差别文本流，HTSIR将章节层级视为重要信息，更符合学术论文等技术文档的实际特点。
- **计算效率高**：相比图结构RAG方法（GraphRAG、HippoRAG），无需构建知识图谱，直接在原始文本上操作，大幅降低预计算成本；实验可在消费级计算机上运行。
- **折叠树检索策略设计巧妙**：将所有节点聚合后统一计算相似度，避免了逐层遍历时各层检索数量的预设定，简化了工程实现。
- **通用性强**：同时支持有/无明确层级结构的文档类型；兼容闭源大模型和开源小模型；可与任何基础检索器（BM25、SBERT、DPR）自由组合。
- **可选Refinement机制灵活**：可按需启用，无需额外训练即可针对特定任务（如对细节敏感的摘要任务）优化输出。
- **实验覆盖面广**：涉及4个数据集、3类检索器、多种LLM后端、多个先进对比方法，较全面地验证了方法的有效性。

## 8. 不足与局限

- **参数设置依赖人工经验**：论文虽给出了参数确定的一般原则（如l=100、r=2），但超参数选择带有主观性，缺乏自适应的参数调优机制。
- **消融实验覆盖不完整**：
  - 参数r的敏感性仅在QuALITY上验证，未覆盖QASPER等其他数据集；
  - Refinement模块的贡献以定性案例为主，缺乏定量消融数据；
  - 重排序（Reranker）模块自身的贡献未做单独消融。
- **对比公平性有待商榷**：与图结构方法（GraphRAG、HippoRAG）的对比引用了对方论文的结果，且对方使用的底层模型（如Llama-3-70B-Instruct）与本文（GPT-4o mini）不同，可能对公平性构成影响；同时未在同配置下复现这些方法。
- **未报告计算资源细节**：缺少GPU型号、训练/推理时间、显存占用等具体信息，尽管声称可在消费级硬件上运行，但缺少量化支撑。
- **摘要依赖LLM质量**：HTSIR的效果高度依赖摘要生成阶段LLM的质量，若后端LLM能力不足，可能导致摘要信息失真并在层级间传播，论文未讨论这一错误传播风险。
- **应用场景局限**：方法主要针对单文档内的信息整合，对于跨多个文档的推理任务（multi-document reasoning）未做验证；且尚未讨论流式更新文档时树的增量维护问题。
- **缺乏与长上下文LLM的直接对比**：在超长上下文中，直接使用长上下文LLM（如LongRAG所代表的思路）也是一条可行路径，论文未系统比较两种范式在效果和成本上的优劣关系。

（完）

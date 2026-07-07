---
title: Equipping Retrieval-Augmented Large Language Models with Document Structure Awareness
title_zh: 赋予检索增强型大语言模型文档结构感知能力
authors: "Lingnan Xu, Chong Feng (冯冲), Kaiyuan Zhang, Liu Zhengyong, Wenqiang Xu, Fanqing Meng"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1339.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 感知文档结构的检索增强生成，提升检索精度
tldr: 现有检索增强生成（RAG）将检索段落视为孤立文本块，忽略了文档结构信息。本文提出RDR2框架，显式融入结构信息：利用基于大语言模型的路由器动态遍历文档结构树，联合评估内容相关性和层级关系，组装最相关证据。实验证明RDR2显著提升了RAG的准确性和可解释性，尤其适合结构化知识库场景。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1612, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1586, \"height\": 1135, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1637, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1651, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 791, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 726, \"height\": 558, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 669, \"height\": 542, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1667, \"height\": 642, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 810, \"height\": 491, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 722, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1643, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1643, \"height\": 2045, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1645, \"height\": 1689, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1648, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1639, \"height\": 427, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1640, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1638, \"height\": 1078, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1641, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1646, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1147, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1638, \"height\": 1519, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1339/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1633, \"height\": 2036, \"label\": \"Table\"}]"
motivation: 现有RAG忽视文档结构，导致检索段落缺乏上下文关联。
method: 提出RDR2框架，利用LLM路由器动态导航文档结构树以组装最优证据。
result: 在多项下游任务上显著提升RAG准确率，减少了事实性错误。
conclusion: 结构感知是提升RAG系统效果的关键因素，RDR2提供了有效范式。
---

## Abstract
While large language models (LLMs) demonstrate impressive capabilities, their reliance on parametric knowledge often leads to factual inaccuracies. Retrieval-Augmented Generation (RAG) mitigates this by leveraging external documents, yet existing approaches treat retrieved passages as isolated chunks, ignoring valuable structure that is crucial for document organization. Motivated by this gap, we propose R etrieve- D ocument R oute- R ead ( RDR2 ), a novel framework that explicitly incorporates structural information throughout the RAG process. RDR2 employs an LLM-based router to dynamically navigate document structure trees, jointly evaluating content relevance and hierarchical relationships to assemble optimal evidence. Our key innovation lies in formulating document routing as a trainable task, with automatic action curation and structure-aware passage selection inspired by human reading strategies. Through comprehensive evaluation on five challenging datasets, RDR2 achieves state-of-the-art performance, demonstrating that explicit structural awareness significantly enhances RAG systems’ ability to acquire and utilize knowledge, particularly in complex scenarios requiring multi-document synthesis.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有检索增强生成（RAG）系统将检索到的段落视为孤立的文本块，忽略了文档固有的结构信息（如标题、章节层次、父子关系），导致在多文档合成、多跳推理等复杂场景中，知识获取和利用能力受限。
- **背景与动机**：尽管LLMs在参数化知识上表现强大，但仍有事实性错误。RAG通过检索外部文档缓解此问题，但主流方法使用固定分块和扁平上下文，丢失了文档的组织结构。人类阅读时会利用标题导航和层级关系，而现有RAG缺乏这种结构感知能力。因此，论文提出将文档结构显式融入RAG全过程，以提升知识获取与利用效率。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出 **Retrieve-Document Route-Read (RDR²)** 框架，在标准“检索-阅读”流程中插入一个 **文档路由** 阶段，由一个基于LLM的路由器（Router）动态遍历文档结构树，根据内容相关性和层级关系，迭代地选择、展开或拒绝节点，最终组装出最优的段落集提供给阅读器生成答案。
- **关键技术细节**：
  - **文档结构表示**：
    - 定义 **文档结构树（Document Structure Tree, DST）**：包含结构节点（如标题）和内容节点（如段落），每个节点具有id、文本、类型、父节点和子节点列表。
    - 定义 **检索子树（Retrieval SubTree, RST）**：从DST派生，保留完整层级结构，但仅展开与当前路由相关的部分内容节点，以实现稳定范围与动态焦点。
  - **路由模块**：
    - **三种原子动作**：`[ANS]`（选择直接回答问题的内容节点）、`[EXP]`（展开可能相关的结构节点下的子节点）、`[REF]`（停止当前子树的探索）。
    - **动作自动策展**：无需人工标注路由轨迹，仅利用问题+检索到的段落及其文档树，用DeepSeek-v3生成单步路由动作，构成训练数据（23,827个样本）。
    - **训练**：使用LoRA微调Llama-3.1-8B-Instruct作为路由器，以标准下一词预测损失（仅对目标输出计算）训练。
  - **RDR²流程**：
    1. **Retrieve**：用检索器（如Contriever）获取top-k段落及其所属文档。
    2. **Document Route**：对每个文档的RST，路由器迭代执行动作，更新RST状态，积累被标记为`[ANS]`的节点作为路由后段落。
    3. **Read**：将路由后段落与问题拼接，输入阅读器（LLM）生成最终答案。

### 3. 实验设计：数据集、Benchmark、对比方法

- **数据集**：5个知识密集型QA数据集，覆盖不同格式：
  - **TriviaQA**（单答案）、**HotpotQA**（多跳）、**QAMPARI**（列表式）、**ASQA**（歧义性长文）、**ELI5**（开放深度解释）。
- **基准方法**：
  - **无检索**：仅使用阅读器的参数知识。
  - **标准Retrieve-and-Read**：直接使用top-k检索段落。
  - **高级RAG**：包括基于闭源LLM的方法（ASC、ASC-F）和基于开源微调的方法（SELF-REASONING、SELF-RAG、OPEN-RAG、FRONT）。
- **评价指标**：
  - 短答案：EM、F1
  - QAMPARI：F1-5、Recall-5、Precision
  - ASQA：EM、ROUGE-L、Disambig-F1
  - ELI5：Claim Recall（基于NLI的断言召回）
  - 额外：MAUVE（流畅度）、输出长度（简洁性）

### 4. 资源与算力

- **训练硬件**：单个 NVIDIA A100-PCIE-40GB GPU。
- **训练时长**：路由器使用LoRA在Llama-3.1-8B-Instruct上训练3.5个epoch。
- **数据策展**：使用DeepSeek-v3 API生成路由动作（27k条数据），离线构建DST耗时约20分钟（Wikipedia全量，8 CPU核并行）。
- 文中未明确说明总GPU小时数，但训练规模较小（8B模型，LoRA）。

### 5. 实验数量与充分性

- **主要实验**：在5个数据集上对比了多个基线，包括不同阅读器（Llama-2-13B、Llama-3.1-8B、ChatGPT、GPT-4o、DeepSeek-V3）。
- **消融实验**（ASQA上）：对管道架构（无路由器）、路由器信息（无结构、无相似度、无内容）、路由动作（无[EXP]、无[REF]）进行消融。
- **测试时缩放实验**：改变top-k（0~5）和扩展迭代次数（0~5）。
- **鲁棒性实验**：更换检索器（GTR、DPR）、更换路由器（Qwen2.5系列1.5B/3B/7B）、不同阅读器。
- **其他分析**：分块方法对比（Meta-Chunking）、文档深度影响、短格式QA性能。
- **充分性评价**：实验设计全面，覆盖了数据集多样性、组件替换、消融、缩放分析、鲁棒性验证，且与多类SOTA方法公平对比（部分方法复现）。结果充分支持主要结论。

### 6. 论文的主要结论与发现

- RDR²在5个数据集上均取得新SOTA，尤其是在需要多文档合成的复杂场景（如ASQA、QAMPARI）提升显著。
- 结构感知的显式建模持续改进RAG性能，且收益随模型规模扩大保持稳定。
- 路由器仅需问题即可训练（无需答案标注），且能泛化到未见过数据集（如TriviaQA、HotpotQA）。
- 路由器的结构推理能力使其能在测试时通过增加扩展迭代实现性能-计算权衡，无需权重更新。
- 消融证实结构信息、相似性初始化、三大动作（[ANS]、[EXP]、[REF]）均为必要组件。

### 7. 优点

- **方法创新性**：首次将文档结构显式融入RAG的路由过程，提出可训练的文档路由任务，灵感来自人类阅读策略。
- **自动化训练数据构造**：无需人工标注路由轨迹，仅利用问题和检索结果自动生成动作，降低应用门槛。
- **组件模块化**：路由器、检索器、阅读器可独立替换，具有较强的兼容性和泛化性。
- **效率与可扩展性**：通过RST设计、并行路由和可调扩展迭代，实现了性能-计算成本的可控权衡。
- **实验全面性**：覆盖多任务、多指标、多种基线和鲁棒性分析，验证了方法的有效性和通用性。

### 8. 不足与局限

- **文档独立处理**：路由过程对每个文档单独进行，文档数量由初始top-k检索决定，限制了跨文档知识整合。
- **离线成本**：需要为整个数据存储（如Wikipedia）预先构建DST，虽然耗时可接受（20分钟），但增加了部署负担。
- **迭代计算开销**：多步路由增加推理延迟，但可通过控制扩展次数缓解。
- **对扁平文档效果有限**：对于深度≤2的浅层文档，收益较小（+0.4 EM），但这类文档在实践中较少（6.5%）。
- **ELI5上提升有限**：开放深度解释任务本身存在评估困难，方法增益不如其他数据集显著。

（完）

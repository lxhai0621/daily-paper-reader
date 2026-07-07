---
title: "KG-CQR: Leveraging Structured Relation Representations in Knowledge Graphs for Contextual Query Retrieval"
title_zh: KG-CQR：利用知识图谱中的结构化关系表示进行上下文查询检索
authors: "Chi Minh Bui, Ngoc Mai Thieu, Vinh Van Nguyen, Jason J. Jung, Khac-Hoai Nam Bui"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.824.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 知识图谱与RAG检索集成
tldr: 该论文提出KG-CQR框架，利用知识图谱的结构化关系表示增强RAG系统中的检索阶段。通过提取、补全相关子图并生成上下文表示，丰富了复杂查询的语义，解决了现有方法忽略查询端上下文丢失的问题。实验证明KG-CQR显著提升了检索质量，特别是在需要结构化知识的场景中。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 1034, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 784, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 1080, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.824/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 596, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1659, \"height\": 673, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1657, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 814, \"height\": 1110, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 1090, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1657, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1657, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.824/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1658, \"height\": 582, \"label\": \"Table\"}]"
motivation: 现有RAG检索方法忽略查询端上下文丢失，无法利用结构化知识。
method: 提取、补全知识图谱子图，生成语义丰富的查询上下文表示。
result: 显著提升检索质量，尤其在结构化知识场景中。
conclusion: KG-CQR有效融合知识图谱与RAG，提升检索效果。
---

## Abstract
The integration of knowledge graphs (KGs) with large language models (LLMs) offers significant potential to enhance the retrieval stage in retrieval-augmented generation (RAG) systems. In this study, we propose KG-CQR, a novel framework for Contextual Query Retrieval (CQR) that enhances the retrieval phase by enriching complex input queries with contextual representations derived from a corpus-centric KG. Unlike existing methods that primarily address corpus-level context loss, KG-CQR focuses on query enrichment through structured relation representations, extracting and completing relevant KG subgraphs to generate semantically rich query contexts. Comprising subgraph extraction, completion, and contextual generation modules, KG-CQR operates as a model-agnostic pipeline, ensuring scalability across LLMs of varying sizes without additional training. Experimental results on the RAGBench and MultiHop-RAG datasets demonstrate that KG-CQR outperforms strong baselines, achieving improvements of up to 4–6% in mAP and approximately 2–3% in Recall@25. Furthermore, evaluations on challenging RAG tasks such as multi-hop question answering show that, by incorporating KG-CQR, the performance outperforms the existing baseline in terms of retrieval effectiveness.

---

## 论文详细总结（自动生成）

# 论文总结：KG-CQR: Leveraging Structured Relation Representations in Knowledge Graphs for Contextual Query Retrieval

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：在检索增强生成（RAG）系统中，现有检索方法常因查询与文档嵌入空间不对齐而性能不佳。传统方法如查询分解或假设文档生成（HyDE）存在不足：分解可能丢失上下文，HyDE过度依赖LLM生成内容，易引入幻觉，且两者均未有效利用结构化知识。
- **研究动机**：当前大部分工作聚焦于语料端上下文增强（如GraphRAG、HippoRAG），而忽略了查询端的上下文丢失。知识图谱（KG）提供结构化、可解释的事实表示，若能利用KG生成查询的语义丰富上下文，可显著提升检索对齐质量。
- **整体含义**：论文提出KG-CQR框架，通过从语料中心知识图谱中提取并补全相关子图，生成上下文表示以增强查询，实现无需额外训练的模型无关检索增强，在多个基准上取得显著提升。

## 2. 方法论
### 核心思想
- **上下文查询检索（CQR）**：将原始查询与从语料中心KG中生成的上下文表示融合，使查询嵌入更接近文档嵌入空间。
- **关键组件**：三个模块——子图提取、子图补全、上下文生成；以及一个融合机制。

### 关键技术细节
1. **知识图谱构建**：利用LLM（如LLaMA-3.3-70B）从文档中抽取三元组（头实体、关系、尾实体），并引入**文本三元组表示（TTR）**：用LLM将每个三元组转换为自然语言段落，增强语义可理解性。
2. **子图提取**：计算查询嵌入与各TTR嵌入的余弦相似度，选取top-k三元组；再用LLM过滤掉不相关的三元组。
3. **子图补全**：针对提取出的子图中的实体对，使用带束搜索（Beam Search）的BFS算法，在完整KG中寻找语义相关的路径，添加路径上的新三元组，形成更丰富的子图。
4. **上下文生成**：用LLM基于补全后的子图生成一段上下文描述（Context）。
5. **融合机制**：将原始查询嵌入与上下文嵌入加权求和：`v_fuse = α·v_q + (1-α)·v_context`，α设为0.7最优。最终用融合向量与文档向量计算相似度。

### 算法流程（文字说明）
- 输入：查询q、语料中心KG（三元组+TTR）
- 步骤：
  1. 子图提取：计算q与每个TTR的相似度，选top-k，LLM过滤 → 初始子图
  2. 子图补全：对初始子图中所有实体对，执行BFS+Beam Search寻找路径，筛选出语义相关且不重复的三元组，合并为新子图
  3. 上下文生成：LLM基于新子图生成上下文文本
  4. 融合：α融合原始查询和上下文的嵌入，用于最终检索

## 3. 实验设计
### 数据集与场景
- **RAGBench**：约11,000个测试实例，覆盖5个行业领域，用于检索评估。
- **MultiHop-RAG**：2,556个多跳查询，需多步推理。
- **额外多步推理评测**：随机抽取RAGBench 500例，以及HotpotQA、MuSiQue（各500随机样本）。

### 基准方法
- 稀疏检索：BM25
- 密集检索：DPR、BGE
- 查询扩展方法：Query Expansion（QE）、HyDE
- 对比：KG-CQR + 不同检索器（BM25/DPR/BGE）

### 对比方法
- 主实验：BM25/DPR/BGE + QE/HyDE/KG-CQR
- 消融：去掉TTR、去掉子图补全
- 多步推理：IRCoT框架下，BM25 vs KG-CQR+BM25
- 互补性：与HippoRAG2集成

### 评估指标
- 检索：mAP、Recall@5/10/25
- 多步推理：F1、GPT-Score（基于GPT-4o）、平均推理步数（Iter）

## 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量或训练时长。所有实验均为LLM推理（零样本/少样本），无额外训练。KG构建和子图处理依赖LLaMA-3.3-70B等模型，具体算力开销未报告。

## 5. 实验数量与充分性
- **数量**：主表1（16行×2数据集）、表2（3种LLM大小）、表3（消融）、表4（3数据集×3LLM×2检索方式）、表5（与HippoRAG2集成）、图4（延迟）、附录表7-9（不同α超参）、表10-11（错误分析）。总计约10+组实验。
- **充分性**：覆盖了检索性能、推理效果、效率、鲁棒性、互补性、超参分析、案例研究。实验设计合理，对比基线充分，消融验证了各模块贡献。不足：未在跨语言或极窄领域数据集上验证，未报告多次运行标准差（可能因无训练）。

## 6. 主要结论与发现
- **检索性能**：KG-CQR+BGE在RAGBench上达到最佳mAP=0.542、Recall@25=0.675，比BGE基线提升4-6% mAP；在MultiHop-RAG上KG-CQR+BM25取得最高Recall@25=0.532。
- **优于HyDE**：HyDE在复杂数据集上表现不稳定，甚至低于纯BGE；KG-CQR一致提升。
- **消融发现**：去除TTR导致Recall@25下降4个百分点，去除子图补全下降约1个百分点，表明两者均关键。
- **多步推理**：KG-CQR减少了平均推理步数（如HotpotQA上从1.465降至1.280），同时提升F1和GPT-Score，说明上下文增强有助于LLM更快聚焦相关证据。
- **模型无关性**：不同大小LLM（3B～70B）均获得稳定收益，展示了KG-CQR的泛化性。
- **互补性**：与HippoRAG2集成后mAP提升0.027，证明查询端与语料端增强可互补。

## 7. 优点
- **创新性**：提出CQR范式，将KG结构化关系表示用于查询端上下文增强，而非传统语料端增强。
- **模型无关**：整个框架无需微调，可适配任意LLM和检索器，实际部署灵活。
- **效率兼顾**：使用束搜索BFS进行子图补全，在检索质量与计算延迟间取得平衡，优于朴素BFS和HyDE。
- **可解释性**：TTR将结构化三元组转为自然语言，便于LLM理解和生成上下文。
- **实验全面**：涵盖检索、多步推理、消融、互补性、超参、错误分析，论证充分。

## 8. 不足与局限
- **KG构建误差**：依赖LLM进行实体/关系抽取，错误会传播至后续模块，在噪声大的域中KG质量难以保证。
- **计算开销**：子图提取需对所有三元组TTR计算相似度，大规模KG下可能成为瓶颈；虽用束搜索优化，但未详细分析最坏情况复杂度。
- **实验覆盖有限**：仅使用两个基准数据集，未测试跨语言、流式更新或超大规模知识库场景，通用性仍需验证。
- **资源细节缺失**：未披露GPU型号、内存消耗、推理时间等硬件参数，影响可复现性。
- **失败案例分析**：在处理需要细粒度时间推理、对比语义或主观内容时，KG-CQR仍会出现上下文漂移或断裂，表明当前方法对复杂语义建模不够深入。

（完）

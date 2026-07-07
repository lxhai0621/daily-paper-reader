---
title: "Query-Driven Multimodal GraphRAG: Dynamic Local Knowledge Graph Construction for Online Reasoning"
title_zh: 查询驱动的多模态图RAG：面向在线推理的动态局部知识图构建
authors: "Chenyang Bu, Guojie Chang, Zihao Chen, CunYuan Dang, Zhize Wu, Yi He, Xindong Wu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1100.pdf"
tags: ["query:mmkqa"]
score: 9.0
evidence: 查询驱动的多模态图RAG，动态构建局部知识图进行多模态推理
tldr: 现有RAG和GraphRAG受限于静态知识库和多模态数据集成不足。本文提出查询驱动的多模态GraphRAG，根据查询语义动态构建局部知识图，并通过多路径检索和多模态补充，显著提升复杂推理任务的表现。实验证明该方法在需要多模态知识的在线推理中优于强基线。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 650, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1571, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 674, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 733, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1393, \"height\": 2124, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1590, \"height\": 348, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1579, \"height\": 741, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1100/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1635, \"height\": 855, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1100/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 697, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1100/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1259, \"height\": 612, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1100/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1368, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1100/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1100/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1680, \"height\": 550, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1100/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1379, \"height\": 272, \"label\": \"Table\"}]"
motivation: 静态知识库和多模态集成不足限制了RAG在复杂推理中的效果。
method: 动态构建局部知识图，结合多路径检索和多模态信息补充。
result: 在多个多模态推理基准上达到最优性能。
conclusion: 查询驱动的多模态GraphRAG有效结合了图结构和多模态信息。
---

## Abstract
An increasing adoption of Large Language Models (LLMs) in complex reasoning tasks necessitates their interpretability and reliability. Recent advances to that end include retrieval-augmented generation (RAG) and knowledge graph-enhanced RAG (GraphRAG), whereas they are constrained by static knowledge bases and ineffective multimodal data integration. In response, we propose a Query-Driven Multimodal GraphRAG framework that dynamically constructs local knowledge graphs tailored to query semantics. Our approach 1) derives graph patterns from query semantics to guide knowledge extraction, 2) employs a multi-path retrieval strategy to pinpoint core knowledge, and 3) supplements missing multimodal information ad hoc. Experimental results on the MultimodalQA and WebQA datasets demonstrate that our framework achieves the state-of-the-art performance among unsupervised competitors, particularly excelling in cross-modal understanding of complex queries.

---

## 论文详细总结（自动生成）

# 论文总结：Query-Driven Multimodal GraphRAG: Dynamic Local Knowledge Graph Construction for Online Reasoning

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：大型语言模型（LLM）在复杂推理任务中面临可解释性和可靠性挑战。检索增强生成（RAG）和知识图谱增强RAG（GraphRAG）虽能缓解幻觉问题，但现有方法受限于静态知识库和低效的多模态数据集成。静态知识图构建（如自底向上的信息驱动方式）缺乏对用户查询语义的感知，导致图谱粒度过细（计算开销大）或过粗（丢失关键语义），尤其在多模态场景下无法有效整合文本、图像和表格数据。
- **核心问题**：如何动态地、查询驱动地构建局部知识图，以高效整合多模态信息并支持多跳推理，同时提升无监督场景下的跨模态理解能力。
- **整体含义**：受认知科学中自上而下的目标驱动注意机制启发，提出**查询驱动的多模态GraphRAG框架**，通过动态图模式构建、多路径选择性注意和迭代知识精炼，实现高效、可解释的多模态推理。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
### 核心思想
- 借鉴认知科学中的**临时心理模式**和**神经效率原则**，模仿人类问题解决时的选择性注意和迭代调整过程。
- 采用**查询驱动（top-down）** 的知识图构建范式，而非传统的数据驱动（bottom-up）方式，仅提取与查询语义最相关的实体和关系。

### 关键技术细节
#### 阶段一：图模式构建（Stage I: Graph Pattern Construction）
- 根据查询语义，利用LLM生成**模式图 G₁ = (T, R)**，其中T是关键实体类型集合，R是语义关系类型集合。例如查询“Which actors have appeared in Marvel movies?”生成实体类型{Actor, Movie}和关系{ActedIn}。
- 初始模式可能不准确，后续通过迭代精炼修正。

#### 阶段二：多模态选择性注意（Stage II: Multimodal Selective Attention）
- **阶段2.1：模式约束检索（Phase 1: Pattern-Constrained Retrieval）**
  - 根据模式图G₁从多模态知识库中构建**检索图 G₂**，包含两部分：
    - 文本提取：提示LLM从文档中提取符合模式的实体和关系。
    - 跨模态节点锚定：通过标题-实体编辑距离匹配，将图像和表格节点关联到已有实体节点。
- **阶段2.2：查询聚焦线索精炼（Phase 2: Query-Focused Clue Refinement）**
  - 进一步构建**线索图 G₃**，通过**双路径实体检索（DPER）** 和**视觉证据集成（FVLM）** 过滤出高度相关的实体和关系：
    - DPER：结合词汇过滤（编辑距离匹配查询关键词）和语义过滤（BERT计算查询与节点描述的余弦相似度）。
    - FVLM：使用CLIP模型和VLM（如LLaVA）进行图像与查询描述的多阶段匹配。

#### 阶段三：迭代知识精炼（Stage III: Iterative Knowledge Refinement）
- 构建**证据图 G₄**，通过评估-增强-扩展循环（Algorithm 1）：
  - **评估**：LLM判断当前图是否足以回答问题。
  - **增强**：视觉证据增强（VLM提取图像细粒度信息）和表格关系挖掘（LLM从表格中动态提取与查询相关的实体和关系）。
  - **扩展**：通过一跳邻居包含进行图结构广度扩展。
- 最终将G₄与原始查询一同输入LLM进行推理。

#### 关键公式
- 迭代精炼过程：$G^{(t+1)}_4 = f_{\text{update}}(G^{(t)}_4, F_{\text{feedback}})$
- 神经效率原则：计算成本 ∝ 不确定性(G₁)⁻¹，即初始不确定时使用轻量检索，后续高置信时使用精细推理。

## 3. 实验设计
### 数据集与场景
- **MultimodalQA**：包含单模态和多模态问题的问答数据集，评价指标为**Exact Match (EM)** 和**F1**。
- **WebQA**：多跳多模态开放域问答，评价指标为**QA-FL**（流畅性）、**QA-ACC**（关键实体重叠）和综合**QA分数**（QA-FL × QA-ACC的语料级平均）。

### Benchmark与对比方法
- **监督方法**：AR, ID, MGT, MMHQA-ICL, PReasM-Large, HPROPRO, SKURG, vlp-x101fpn, vlp-VinVL, MuRAG。
- **无监督方法**：Vicuna-7B, Llama2Chat-13b, OpenChat-v2-w-13b, MOQAGPT, Binder, OFA-Cap, PROMPTCap。
- 额外对比了图构建方法（KAG, GraphRAG）以及传统RAG和GraphRAG的案例对比。

### 实验设置
- 使用**BGE-M3**做文本嵌入，**CLIP**做图像嵌入。
- LLM部分：Qwen 2.5 72B用于图构建，LLaVA 34B和Gemini-1.5-flash用于跨模态推理。
- 所有方法在同一推理阶段使用相同的GPT-4模型（用于最终答案生成），保证公平。

## 4. 资源与算力
- 论文指出：**所有实验在NVIDIA A100 GPU（80GB显存）上进行**。
- 但**未明确说明使用的GPU数量、训练时长或推理时间**，也未提供详细的算力成本分析。
- 消融实验和案例研究均在同一硬件环境下运行，但缺乏具体的资源消耗定量数据。

## 5. 实验数量与充分性
### 实验组数
- **两个主数据集**（MultimodalQA, WebQA）上的完整性能对比。
- **消融实验**：在MultimodalQA上逐步添加视觉增强、表格挖掘、图像匹配组件，共5种配置（基线→+视觉→+表格→+两者→全模型）。
- **图构建方法对比**：与KAG和GraphRAG比较节点数、边数和EM。
- **案例研究**：两个复杂查询的详细推理过程对比（与MOQAGPT、RAG、GraphRAG）。
- **额外实验**：在单模态数据集HotpotQA和Drop上与Xrag对比，覆盖多指标（ChrF, METEOR, ROUGE, EM等）。
### 充分性与公平性
- **充分**：覆盖了多模态（图像+文本+表格）和单模态场景，消融实验验证了各组件贡献，图构建对比证明了效率提升。
- **公平**：所有对比方法在同一LLM（GPT-4）下测试，RAG/GraphRAG复现时保持相同检索策略和基座模型；超参数设置明确（Top-k值等），但未提供多次运行的标准差统计量。
- **客观**：案例研究展示了具体失败模式和成功原因，增强了可信度。

## 6. 论文的主要结论与发现
- **性能显著提升**：在MultimodalQA上，无监督方法达到68.0% F1和60.3% EM，超越所有无监督基线（如Binder 57.1 F1），甚至超过部分监督方法（如SKURG 64.0 F1）。在WebQA上，QA分数43.63，远超PROMPTCap（34.5）。
- **图构建效率**：相比KAG（137.99节点/218.32边）和GraphRAG（72.31节点/46.65边），本方法仅用59.95节点/38.66边，EM分别提升15.5和8.05个点。
- **多模态集成有效性**：消融实验显示，同时使用视觉增强和表格挖掘后F1提升约6.5%，再叠加图像匹配机制又提升5.4%，证明各组件协同作用。
- **案例验证**：在描述“半张女人脸海报”查询中，本方法通过表格链接和VLM图像分析正确识别电影《Tell Me That You Love Me, Junie Moon》，而基线MOQAGPT仅通过嵌入比较失败。

## 7. 优点
- **创新范式**：首次将认知科学中的“临时心理模式”和“神经效率原则”系统性地引入GraphRAG，实现查询驱动的动态知识图构建，避免了预构建静态图的冗余。
- **高效性与准确性兼得**：通过分阶段处理（模式约束检索→线索精炼→迭代精炼），在早期使用轻量方法快速缩小范围，仅在必要时启用高成本VLM，平衡了计算开销和推理精度。
- **无监督且强泛化**：无需标注数据即可达到甚至超越监督方法的性能，且能推广到纯文本数据集（HotpotQA, Drop）并超越专门设计的RAG方法（Xrag）。
- **可解释性**：通过可视化线索图和证据图，展示了推理链条，增强可信度。

## 8. 不足与局限
- **依赖LLM的初始模式质量**：模式图由LLM生成，若初始模式（G₁）偏差过大，后续迭代可能无法完全纠正，导致前期错误累积。
- **多模态覆盖有限**：当前仅支持图像、文本和表格三种模态，缺乏视频、音频等更多模态；且图像理解依赖预训练的VLM（LLaVA, Gemini），在处理模糊或抽象查询时可能失效。
- **缺乏算力成本量化**：未提供GPU数量、训练时长或推理时延的具体数据，难以对比与其他方法的实际计算效率。
- **实验统计严谨性不足**：未报告多次运行的标准差或置信区间，无法评估结果的稳定性；消融实验仅在MultimodalQA上执行，未在WebQA上验证。
- **对模糊查询敏感**：论文自承对不明确的查询效果下降，缺乏显式的查询澄清或意图分解机制。
- **未充分讨论小样本/零样本泛化**：实验仅涉及中大规模数据集，未测试极度低资源场景（如仅少量文档）下的鲁棒性。

（完）

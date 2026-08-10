---
title: "Personalize Before Retrieve: LLM-based Personalized Query Expansion for User-Centric Retrieval"
title_zh: 检索前个性化：面向用户中心检索的大模型个性化查询扩展
authors: "Yingyi Zhang, Pengyue Jia, Derong Xu, Yi Wen, Xianneng Li, Yichao Wang, Wenlin Zhang, Xiaopeng Li, Weinan Gan, Huifeng Guo, Yong Liu, Xiangyu Zhao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38679/42641"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向RAG的个性化查询扩展，通过保留用户意图提升检索相关性
tldr: 现有RAG查询扩展采用统一策略，忽略用户个性差异，导致检索泛化受限。作者提出检索前个性化方案，利用LLM针对用户表达方式、偏好和历史进行查询扩展，保留个性化意图并适配异构语料。实验证明该方案能有效提升RAG在个性化场景中的检索相关性与生成质量，为面向用户的RAG实践提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38679/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 876, \"height\": 782, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38679/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1835, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38679/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1386, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38679/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1816, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38679/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1811, \"height\": 476, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38679/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1831, \"height\": 803, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38679/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 918, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38679/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 871, \"height\": 787, \"label\": \"Table\"}]"
motivation: RAG统一查询扩展忽视用户个体差异，导致用户中心检索泛化受限。
method: 提出LLM驱动的个性化查询扩展，建模用户表达风格、偏好与历史上下文。
result: 实验表明该方法能提升个性化RAG的检索相关性和系统泛化能力。
conclusion: 检索前的个性化处理能显著改善RAG在用户中心设定的有效性。
---

## Abstract
Retrieval-Augmented Generation (RAG) critically depends on effective query expansion to retrieve relevant information. However, existing expansion methods adopt uniform strategies that overlook user-specific semantics, ignoring individual expression styles, preferences, and historical context. In practice, identical queries in text can express vastly different intentions across users. This representational rigidity limits the ability of current RAG systems to generalize effectively in personalized settings. Specifically, we identify two core challenges for personalization: 1) user expression styles are inherently diverse, making it difficult for standard expansions to preserve personalized intent. 2) user corpora induce heterogeneous semantic structures—varying in topical focus and lexical organization—which hinders the effective anchoring of expanded queries within the user’s corpora space. To address these challenges, we propose Personalize Before Retrieve (PBR), a framework that incorporates user-specific signals into query expansion prior to retrieval. PBR consists of two components: P-PRF, which generates stylistically aligned pseudo feedback using user history for simulating user expression style, and P-Anchor, which performs graph-based structure alignment over user corpora to capture its structure. Together, they produce personalized query representations tailored for retrieval. Experiments on two personalized benchmarks show that PBR consistently outperforms strong baselines, with up to 10% gains on PersonaBench across retrievers. Our findings demonstrate the value of modeling personalization before retrieval to close the semantic gap in user-adaptive RAG systems.

---

## 论文详细总结（自动生成）

好的，我将根据提供的论文内容，生成一篇结构化的中文详细总结。

---

## 论文详细总结：《Personalize Before Retrieve: LLM-based Personalized Query Expansion for User-Centric Retrieval》

### 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：检索增强生成（RAG）系统依赖查询扩展（Query Expansion）来提升检索质量。现有方法（如HyDE、Query2Term等）采用统一的、与用户无关的扩展策略，对所有用户的相同查询生成一致的扩展表示。
- **核心问题**：在实际应用中，不同用户即使提交相同的文本查询，其背后意图也可能截然不同。例如，查询“How would you describe my dietary preferences?”（如何描述我的饮食偏好），注重健康的用户和追求新奇口味的用户期望检索到的信息完全不同。现有统一扩展策略无法捕获这种用户特定的语义差异，导致检索结果与用户真实意图严重不匹配。
- **两个核心挑战**：
    1. **用户表达风格多样性（Expression Style Diversity）**：不同用户的语言习惯、措辞风格、详细程度各不相同，甚至存在隐含的个人化表达范式，标准扩展方法难以保留这种个性化意图。
    2. **用户语料异质性（Heterogeneous Semantic Structures）**：不同用户的个人语料库在主题覆盖、词汇组织、内容粒度上差异巨大，扩展后的查询难以在用户的语料空间中精准“落地”，容易漂移到与用户语境无关的区域。
- **核心思想**：论文提出**“检索前个性化”（Personalize Before Retrieve, PBR）**框架，主张在检索发生之前，就将用户特定的风格、偏好和历史上下文信号注入到查询扩展过程中，从而弥合RAG系统在用户中心设定下的语义鸿沟。

### 2. 方法论：核心思想、关键技术细节与公式

PBR框架采用了三阶段设计，以联合建模用户的“表达风格”（Style）和“语料结构”（Structure），最终生成个性化的查询向量表示。整体框架见图2。

- **阶段一：P-PRF（Personal Style-Aligned Pseudo Relevance Feedback，个性化风格对齐的伪相关性反馈）**
    - **目标**：模拟用户的表达风格与隐含推理逻辑，生成风格对齐的伪反馈。
    - **步骤1（相关子集检索）**：首先从用户完整历史语料 C 中，通过语义相似度检索出与当前查询 q 最相关的 top-k1 条历史语料子集 Hq，以捕获与当前查询相关的用户特质。
    - **步骤2（伪话语生成 - "Roughly"）**：使用LLM（记为 G_utt^LLM），以原始查询 q 和相关历史子句 Hq 为条件，生成 m 条“用户可能会自然说出”的伪话语（Pseudo Utterance），以模拟用户的语气、措辞和细致程度。
    - **步骤3（伪推理生成 - "Logically"）**：使用另一个LLM流水线（记为 G_rea^LLM），生成逐步推理过程 r，以建模用户表达背后的隐含意图和逻辑链路。
    - **核心公式**：伪话语均值表示 f_avg = (1/m) * Σ φ(fi)；伪推理向量 r = φ(r)。

- **阶段二：P-Anchor（Personal Structure-Aligned Semantic Anchoring，个性化结构对齐的语义锚定）**
    - **目标**：捕获用户语料库的整体结构特征，生成代表用户通用偏好的“语义锚点”。
    - **步骤1（语义图构建）**：将用户的语料库编码为一个语义图 G = (C, E)。节点是语料向量 ci；边根据两两节点间的余弦相似度 Sij 构建，仅保留超过阈值 θ 且属于 top-k2 相似邻居的边，形成稀疏邻接矩阵 A。
    - **步骤2（图上个性化排序）**：在图上运行**个性化PageRank**算法，通过迭代计算 π^(t+1) = α·P^T·π^(t) + (1−α)·(1/n)·1（其中 P = norm(A)）来估计每个节点的中心性得分 π。
    - **核心公式**：用户锚点 c_Anchor = Σ πi·ci，即所有语料向量按其中心性得分的加权聚合。

- **阶段三：PBR Fusion（个性化融合模块）**
    - **目标**：将P-PRF生成的风格化伪反馈（伪话语和伪推理）与P-Anchor生成的用户锚点，同原始查询有机结合。
    - **动态权重分配**：设计“个性化且查询特定”的动态权重 w1 和 w2，用于平衡伪话语和伪推理的贡献。权重基于它们与原始查询和用户锚点中点（(q + c_Anchor)/2）的余弦相似度再加上常数1计算，确保正值和光滑插值。
        - w1 = 1 + sim((q + c_Anchor)/2, f_avg)
        - w2 = 1 + sim((q + c_Anchor)/2, r)
    - **最终查询向量**：定义用户特定个性化偏移 Δ_user(q, C) = c_Anchor + w1·f_avg + w2·r。最终个性化查询表示 q* = q + Δ_user(q, C) = q + c_Anchor + w1·f_avg + w2·r。
    - **最终检索**：使用 q* 在用户语料库 C 中基于FAISS进行稠密向量最近邻搜索，返回Top-K相关结果。

### 3. 实验设计：数据集、基准与对比方法

- **数据集（Datasets/Benchmarks）**：
    1. **PersonaBench**：模拟用户在合成私有数据上的个性化查询。包含6个用户，每个用户有独立语料库和约50个富含歧义和个性化语言的查询。包含多个子集：Basic information、Preference (hard)、Social、Preference (easy)。
    2. **LongMemEval**：面向长期交互记忆的基准，包含两个子集：**LongMemEval-s**（短期）和**LongMemEval-m**（长期）。包含500个不同用户的查询，每个查询配对相关记忆语料，侧重硬性事实锚定。
- **评估指标**：Recall@K（R@K）和 NDCG@K（N@K），报告了R@1/3/5和N@1/3/5。
- **对比基线（Baselines）**：共6种。
    - **Base**：无扩展的静态查询检索。
    - **HyDE**：生成假设性文档进行扩展。
    - **Query2Term**：基于关键短语的查询扩展。
    - **MILL**：利用互验证信息进行扩展。
    - **CoT**：利用思维链推理辅助排序。
    - **ThinkQE**：将扩展建模为进化思考过程。
- **实现细节**：所有方法使用 **GPT-4o-mini** 作为LLM，运行5次取结果。实验在3种不同检索骨干下验证，以检验鲁棒性：
    - `multi-qa-MiniLM-L6-cos-v1`
    - `all-MiniLM-L6-v2`
    - `bge-base-en-v1.5`
- **超参数设置**：k1=5, m=5, θ=0.75, k2=10（在PersonaBench和LongMemEval-s上）；LongMemEval-m 因为历史更长，使用更大的 k2=50。

### 4. 资源与算力

- **未明确说明**：论文原文和提供的文本中**未提及**任何关于GPU型号、数量、分布式训练框架、训练时长或推理算力的具体信息。
- **可推断信息**：论文使用GPT-4o-mini作为LLM，推测作者通过API调用完成生成，而非本地部署训练；检索模型中使用了FAISS库（CPU/GPU均可运行）。考虑到文本中所有实验在“运行5次”且未提到大规模训练，可推测总工作量主要集中在对小规模数据集的推理和向量检索上，算力需求相对适中，但具体规模属于未知项。

### 5. 实验数量与充分性

- **实验数量**：实验非常丰富，包含多个层次。
    - **主对比实验**：在2个数据集上的3种检索器配置下，对比了6种基线，并且PersonaBench报告了4个子集，LongMemEval报告了2个子集。
    - **消融实验（表3）**：对PBR整体、P-PRF、P-Anchor三个组件进行了逐模块消融，并在PersonaBench的4个子集下进行。
    - **子组件消融（图3）**：进一步对P-PRF内部的伪话语生成和伪推理生成进行了消融。
    - **参数敏感性分析（图4）**：对P-Anchor的θ和k2进行了敏感性测试。
    - **可视化分析（图5）**：使用t-SNE可视化了查询-向量分布，对比原始查询、HyDE和PBR的性能。
- **充分性评价**：
    - **优点**：实验设计客观且全面。控制了LLM类型（都使用GPT-4o-mini）、涵盖了多个主流检索器骨干、包含了从整体到子组件的深度消融，并进行了参数敏感性分析，统计显著性检验（t-test, p<0.05）也支撑了结论。
    - **局限性**：两个数据集虽然各有侧重，但都基于合成数据，缺乏真实的用户场景验证。此外，仅依赖单一LLM（GPT-4o-mini）生成扩展和推理，缺乏对LLM选择的影响分析。评估指标仅局限于检索层面（R@K、N@K），未涉及最终RAG生成质量（如回答准确性）的端到端评估。

### 6. 主要结论与发现

- **PBR显著优于所有基线**：在PersonaBench上，PBR获得整体平均R@5 0.4527、N@5 0.3819，相比最强基线ThinkQE（0.4098/0.3484）实现了约10%的增益。在所有检索器上、两个数据集上均一致取得最优结果。
- **PBR能解决语义歧义**：在PersonaBench的个性化模糊查询上，PBR通过用户风格化伪反馈和锚定有效降低了歧义。
- **PBR提升硬性事实检索的Top-1精度**：在LongMemEval上，PBR在R@1上显著超过最佳基线，表明风格模拟和结构锚定能更精准地定位长上下文记忆中的正确答案。
- **P-PRF是主要贡献模块**：消融实验显示，移除P-PRF导致性能大幅下降（如all-MiniLM下R@5从0.4516降至0.2860），说明了生成风格化伪查询对于捕获用户意图的核心作用。伪话语有助于提高词汇覆盖，伪推理有助于提高基于目标的推理精度。
- **P-Anchor在结构化语料中价值显著**：在Basic Information和Social等具有清晰结构特征的子集中，P-Anchor贡献明显；但在无明显聚类的Preferences (hard)上可能过拟合。
- **参数敏感性存在最优区间**：θ在0.65-0.75、k2=5时效果最佳；过度传播（θ过大、k2过大）会导致语义漂移。
- **可视化验证了查询语义的接近度**：PBR生成的查询向量在t-SNE空间上更接近各自用户的真实相关语料（GT），且在不同用户间有更大的语义区分度。

### 7. 优点

- **核心创新性强**：首次提出个性化查询扩展框架，明确了“检索前个性化”的重要性。
- **方法设计全面**：同时建模了用户表达风格（P-PRF）和语料结构（P-Anchor），形成了“风格+结构”的双重对齐机制。
- **动态权重设计巧妙**：PBR Fusion模块通过计算语义相似度来动态平衡不同反馈信源的权重，能适应不同查询的语义开放度。
- **工程实践扎实**：实验设置覆盖了多种检索器骨干，采用了统计显著性检验，且提供了代码仓库和扩展版本链接，非常利于后续研究复现。
- **分析视角多元**：不仅包含定量对比，还辅以直观的t-SNE可视化，提升了结果的可解释性。

### 8. 不足与局限

- **实验覆盖广度有限**：仅使用了两个合成基准数据集，缺乏真实用户交互日志或样本，可能无法完全反映现实场景中用户行为的复杂性和噪音。
- **LLM依赖单一性**：所有实验均仅使用GPT-4o-mini，未评估不同规模或类型的LLM对PBR性能的影响，泛化性存疑。
- **评估范围不完整**：实验只停留在检索阶段，没有延伸到下游RAG生成任务，无法验证个性化扩展是否真正提升了最终答案的生成质量（如用户满意度、回答准确率）。
- **P-Anchor模块适用性受限**：研究结果揭示P-Anchor对语料结构高度敏感，在非结构化或缺乏主题簇的语料（如Preferences hard）上可能产生过拟合或增益极低，限制了其在多样化的真实语料上的普适性。
- **算力/成本考量缺失**：框架涉及多次LLM生成调用（伪话语、伪推理）和PageRank算法，但论文未提及在真实大规模用户语料上应用时的推理延迟和计算成本，这在实际部署中可能成为瓶颈。
- **超参数依赖性强**：PBR对θ和k2等超参数较为敏感，不同数据集规模需要调整k2（如LongMemEval-m设定为50），增加了实际应用中的调参负担。

（完）

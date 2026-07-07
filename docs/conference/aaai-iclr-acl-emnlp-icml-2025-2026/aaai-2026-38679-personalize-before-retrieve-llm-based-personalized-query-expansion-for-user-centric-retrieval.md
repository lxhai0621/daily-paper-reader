---
title: "Personalize Before Retrieve: LLM-based Personalized Query Expansion for User-Centric Retrieval"
title_zh: 检索前个性化：基于大语言模型的个性化查询扩展用于用户中心检索
authors: "Yingyi Zhang, Pengyue Jia, Derong Xu, Yi Wen, Xianneng Li, Yichao Wang, Wenlin Zhang, Xiaopeng Li, Weinan Gan, Huifeng Guo, Yong Liu, Xiangyu Zhao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38679/42641"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向用户中心的个性化查询扩展，提升RAG相关性
tldr: 现有检索增强生成中的查询扩展采用统一策略，忽略了不同用户的表达风格、偏好和历史上下文，导致个性化场景下检索不准确。本文提出先个性化后检索的方法，利用大语言模型生成适配用户独特语义的查询扩展。通过解决用户表达多样性和语料异质性，显著提升了RAG系统在个性化设置中的准确率和相关性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 统一查询扩展策略忽视用户个体差异，导致RAG个性化不足。
method: 使用大语言模型根据用户表达风格和历史上下文生成定制查询扩展。
result: 在个性化检索任务中显著提升相关性和准确率。
conclusion: 个性化查询扩展是提升RAG用户适应性的关键。
---

## Abstract
Retrieval-Augmented Generation (RAG) critically depends on effective query expansion to retrieve relevant information. However, existing expansion methods adopt uniform strategies that overlook user-specific semantics, ignoring individual expression styles, preferences, and historical context. In practice, identical queries in text can express vastly different intentions across users. This representational rigidity limits the ability of current RAG systems to generalize effectively in personalized settings. Specifically, we identify two core challenges for personalization: 1) user expression styles are inherently diverse, making it difficult for standard expansions to preserve personalized intent. 2) user corpora induce heterogeneous semantic structures—varying in topical focus and lexical organization—which hinders the effective anchoring of expanded queries within the user’s corpora space. To address these challenges, we propose Personalize Before Retrieve (PBR), a framework that incorporates user-specific signals into query expansion prior to retrieval. PBR consists of two components: P-PRF, which generates stylistically aligned pseudo feedback using user history for simulating user expression style, and P-Anchor, which performs graph-based structure alignment over user corpora to capture its structure. Together, they produce personalized query representations tailored for retrieval. Experiments on two personalized benchmarks show that PBR consistently outperforms strong baselines, with up to 10% gains on PersonaBench across retrievers. Our findings demonstrate the value of modeling personalization before retrieval to close the semantic gap in user-adaptive RAG systems.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）
**研究动机**：当前检索增强生成（RAG）系统中的查询扩展（Query Expansion, QE）方法采用统一策略，忽略了个体用户的表达风格、偏好和历史上下文。相同的文本查询在不同用户间可能表达截然不同的意图，导致检索结果不匹配，限制了RAG在个性化场景中的泛化能力。

**核心挑战**：
- **用户表达风格多样性**：用户使用不同的语言模式（如简洁提示或详细推理），标准扩展难以保留个性化意图。
- **用户语料异质性**：个人语料在主题覆盖、词汇组织上差异大，扩展后的查询难以在用户语义空间中准确锚定。

**整体目标**：提出“先个性化后检索”（Personalize Before Retrieve, PBR）框架，在检索前将用户特定信号融入查询理解，弥合语义鸿沟。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程
**核心思想**：通过两阶段设计融合表达级扩展与结构级对齐，使查询同时反映个人风格和语料语义。

### P-PRF：个人风格对齐的伪相关反馈
- **伪话语生成（粗略）**：基于原始查询 \(q\) 和用户历史子集 \(H_q\)，利用LLM生成 \(m\) 条模拟用户风格的伪话语 \(\{f_1,\dots,f_m\}\)，取其平均嵌入 \(f_{\text{avg}}\) 作为风格信号。
- **伪推理生成（逻辑）**：让LLM生成逐步推理过程 \(r\)，并嵌入为 \(r\)，捕捉用户隐含的推理模式。

### P-Anchor：个人结构对齐的语义锚定
- **图构建**：将用户历史语料编码为节点，基于余弦相似度构建稀疏邻接矩阵 \(A\)（仅保留 top-\(k_2\) 邻居且相似度 \(\geq \theta\)）。
- **图锚点表示**：对图应用PageRank，得到平稳分布 \(\pi\)，计算用户锚点嵌入 \(c_{\text{Anchor}} = \sum_i \pi_i c_i\)，代表语料的结构性中心语义。

### PBR Fusion：融合与最终查询
- **动态权重**：由伪话语与伪推理分别相对于查询和锚点平均的相似度计算 \(w_1, w_2\)。
- **个性化偏移**：\(\Delta_{\text{user}}(q, C) = c_{\text{Anchor}} + w_1 \cdot f_{\text{avg}} + w_2 \cdot r\)。
- **最终查询嵌入**：\(q^* = q + \Delta_{\text{user}}(q, C)\)，然后用faiss进行最近邻检索。

## 3. 实验设计
### 数据集
- **PersonaBench**：6个用户，每个有约50个查询，涉及显式/隐式个性化特征（基本社会信息、偏好、社交等）。
- **LongMemEval**：500个用户查询，分两个子集（-s简版，-m长版），侧重长期互动记忆检索。

### 评价指标
- Recall@K（R@K）和NDCG@K（N@K），主要报告R@5、N@5、R@1等。

### 对比方法（Baselines）
- **Base**：静态查询无扩展
- **HyDE**：生成假设文档扩展
- **Query2Term**：关键词扩展
- **MILL**：互验证扩展
- **CoT**：链式思考
- **ThinkQE**：推理过程扩展

### 实现细节
- 三个检索backbone：`multi-qa-MiniLM-L6-cos-v1`、`all-MiniLM-L6-v2`、`bge-base-en-v1.5`
- LLM统一使用GPT-4o-mini
- 超参数：\(k_1=5, m=5, \theta=0.75, k_2=10\)（LongMemEval-m用\(k_2=50\)）
- 每个实验运行5次

## 4. 资源与算力
论文中未明确说明使用的GPU型号、数量或训练时长。实验部分仅提到使用GPT-4o-mini作为LLM，检索器为预训练模型，未报告具体计算资源开销。因此，无法量化算力消耗。

## 5. 实验数量与充分性
- **整体性能对比**：在PersonaBench和LongMemEval上，使用3种检索backbone，报告了详细指标（表1、表2）。
- **消融实验**：移除P-PRF和P-Anchor的组件消融（表3），以及P-PRF内部的双成分消融（图3）。
- **参数敏感性分析**：对P-Anchor的\(\theta\)和\(k_2\)进行了6×6网格搜索（图4）。
- **可视化案例**：t-SNE图展示查询与Ground Truth的分布（图5）。
- **统计显著性**：对最佳结果进行了t检验（p<0.05）。

**充分性评估**：实验覆盖了多个数据集、多个检索器、多种消融和参数分析，且做了统计检验，较为充分、客观、公平。但未进行跨LLM（如Llama、Claude）的对比，可能影响泛化结论。

## 6. 主要结论与发现
1. **PBR显著优于所有基线**：在PersonaBench上R@5平均0.4527，比最佳基线ThinkQE（0.4098）提升约10%；在LongMemEval上R@1和R@5均有提升。
2. **P-PRF是性能核心**：移除P-PRF导致R@5从0.4516降至0.2860（all-MiniLM），表明风格化伪反馈对个性化检索至关重要。
3. **P-Anchor提供结构化对齐**：移除P-Anchor后N@5从0.3819降至0.3695，尤其在语义结构清晰的子集上作用明显。
4. **适度传播 vs. 过度传播**：\(\theta \in [0.65,0.75], k_2=5\)时性能最佳；过高的\(\theta\)或\(k_2\)引入噪声，导致语义漂移。
5. **可视化证明个性化嵌入**：PBR生成的查询更接近用户对应的Ground Truth，而HyDE和原始查询则聚集在一起，缺乏区分度。

## 7. 优点
- **创新性强**：首次提出“检索前个性化”的查询扩展框架，填补了RAG个性化领域的空白。
- **双支柱设计合理**：P-PRF抓取表达风格与推理逻辑，P-Anchor利用图结构捕捉全局偏好，互补性强。
- **动态融合权重**：根据查询与锚点相关性自适应调节伪反馈贡献，增加灵活性。
- **实验扎实**：多数据集、多检索器、多维度消融，并进行了统计分析，说服力强。
- **代码开源**：提供GitHub链接，有利于复现和后续研究。

## 8. 不足与局限
- **LLM单一性**：仅使用GPT-4o-mini，未验证在其他LLM（如Llama-3、Claude）上的表现，存在模型偏倚风险。
- **计算开销**：PBR需要多次调用LLM（生成伪话语和推理）以及构建图并运行PageRank，可能带来更高延迟，论文未讨论部署效率。
- **PersonaBench数据规模较小**：仅6个用户，可能不足以代表真实世界中用户多样性和语料规模。
- **LongMemEval任务特性**：该数据集更侧重事实性记忆检索，PBR在软个性化上的优势在长上下文中可能被稀释（如R@5提升幅度不如PersonaBench明显）。
- **未对比P-Anchor的替代方法**：例如使用聚类中心或均值作为锚点，缺乏对更简单基线（如直接平均所有用户嵌入）的对比。
- **实验覆盖不全**：未进行跨领域（如电商、医疗）的迁移测试，也未见检索速度或吞吐量比较。

（完）

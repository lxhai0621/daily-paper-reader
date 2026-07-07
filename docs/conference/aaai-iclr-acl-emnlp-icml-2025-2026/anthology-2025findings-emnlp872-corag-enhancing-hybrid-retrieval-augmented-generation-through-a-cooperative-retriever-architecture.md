---
title: "CoRAG: Enhancing Hybrid Retrieval-Augmented Generation through a Cooperative Retriever Architecture"
title_zh: CoRAG：通过协作检索器架构增强混合检索增强生成
authors: "Zaiyi Zheng, Song Wang, Zihan Chen, Yaochen Zhu, Yinhan He, Liangjie Hong, Qi Guo, Jundong Li"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.872.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 混合RAG结合协作检索和全局知识
tldr: 现有混合RAG方法仅从局部邻居或子图检索，可能遗漏全局相关信息。CoRAG通过动态选择知识来源并协作检索，同时利用文本和图结构信息，并考虑文档间相互依赖关系。实验表明CoRAG在多个基准上优于现有混合RAG方法。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 713, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1634, \"height\": 836, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 722, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.872/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 721, \"height\": 634, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1299, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1638, \"height\": 945, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1578, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1662, \"height\": 1645, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1671, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.872/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1464, \"height\": 251, \"label\": \"Table\"}]"
motivation: 现有混合RAG仅从局部检索，遗漏全局相关信息。
method: 提出CoRAG，动态选择知识来源，协作检索文本和图结构信息。
result: CoRAG在多个基准上超越现有混合RAG方法。
conclusion: 协作检索和全局视角能显著提升混合RAG性能。
---

## Abstract
Retrieval-Augmented Generation (RAG) is introduced to enhance Large Language Models (LLMs) by integrating external knowledge. However, conventional RAG approaches treat retrieved documents as independent units, often overlooking their interdependencies. Hybrid-RAG, a recently proposed paradigm that combines textual documents and graph-structured relational information for RAG, mitigates this limitation by collecting entity documents during graph traversal. However, existing methods only retrieve related documents from local neighbors or subgraphs in the knowledge base, which often miss relevant information located further away from a global view. To overcome the above challenges, we propose CoRAG that dynamically chooses whether to retrieve information through direct textual search or explore graph structures in the knowledge base. Our architecture blends different retrieval results, ensuring the potentially correct answer is chosen based on the query context. The textual retrieval components also enable global retrieval by scoring non-neighboring entity documents based on semantic relevance, bypassing the locality constraints of graph traversal. Experiments on semi-structured (relational and textual) knowledge base QA benchmarks demonstrate the outstanding performance of CoRAG.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：传统RAG将检索到的文档视为独立单元，忽略了它们之间的相互依赖关系。混合RAG（Hybrid-RAG）虽然结合了文本和图结构关系信息，但现有方法仅从局部邻居或子图中检索，容易遗漏远离局部范围的全局相关信息。此外，现有方法对不同类型的检索结果缺乏查询感知的选择能力，盲目融合可能导致冗余或冲突信息影响LLM。
- **整体含义**：论文提出CoRAG框架，旨在通过动态选择检索源（文本搜索或图结构探索）并协作融合异构信息，突破局部性约束，实现全局范围内的有效检索，提升半结构化知识库问答（SKBQA）任务的性能。

## 2. 论文提出的方法论

- **核心思想**：设计一种混合专家（Mixture-of-Experts）架构，包含多个基于双编码器的文本检索器和关系检索器，并通过分层门控网络动态分配注意力权重，自适应地融合文本和关系检索结果。
- **关键技术细节**：
  - **主题实体提取**：使用Aho-Corasick自动机算法从问题中识别命名实体（主题实体），基于贪婪匹配优先选择较长字符串。
  - **双检索器设计**：
    - 文本检索器：按实体类型分组，每个类型一个检索器，基于余弦相似度对候选实体文档进行全局评分（不受图结构限制）。
    - 关系检索器：以主题实体为中心，按关系类型分组，仅对邻接实体集进行评分（局部检索）。
  - **分层门控网络**：
    - 文本级门控：为不同实体类型的文本检索器分配权重，输出加权文本分数。
    - 关系级门控：为不同关系类型的关系检索器分配权重，输出加权关系分数。
    - 混合级门控：融合文本分数和关系分数，输出最终预测分数。
  - **训练目标**：使用均方误差（MSE）损失，以ground-truth答案（1/0）作为监督信号。
  - **LLM重排序**：在CoR检索top-k候选实体后，使用LLM（如GPT-4o-mini）对每个实体生成二进制相关性分数，并与CoR分数相加得到最终排序。
- **算法流程**（文字描述）：
  1. 输入问题q，提取主题实体ET。
  2. 对每个候选实体e，分别通过所有文本检索器计算分数向量，经文本门聚合得s^(t)；通过所有关系检索器计算分数向量，经关系门聚合得s^(r)。
  3. 混合门将s^(t)和s^(r)融合，输出预测分数ŝ(q,e)，取top-k得到候选集合Â。
  4. LLM重排序器对Â中每个实体生成二进制分数s'，最终分数ŝ* = ŝ + s'，按ŝ*排序输出最终答案。

## 3. 实验设计

- **数据集**：使用STaRK基准中的三个半结构化知识库QA数据集：
  - **STaRK-Amazon**（电子商务）：约103万实体、944万三元组，9个实体类型，5个关系类型。
  - **STaRK-MAG**（学术）：约187万实体、3980万三元组，4个实体类型，4个关系类型。
  - **STaRK-Prime**（医学）：约12.9万实体、810万三元组，10个实体类型，18个关系类型。
- **评估指标**：Hits@1, Hits@5, Recall@20, MRR（平均倒数排名）。
- **对比方法**：
  - **检索器基线**：DPR（基于RoBERTa和text-ada-002）、Multi-VSS。
  - **RAG基线**：
    - 传统RAG：ReAct、Reflexion、AVATAR、AVATAR-C、AGR。
    - 图RAG：QAGNN、ToG（Think-on-Graph）。
- **实验设置**：门控网络为两层MLP，使用text-ada-002作为编码器（固定），LLM重排序使用GPT-4o-mini。训练5个epoch，学习率1e-4。

## 4. 资源与算力

- 文中明确提及：**所有代码在配备48核CPU和NVIDIA A100 GPU的服务器上执行**。未说明具体GPU数量、训练时长或总计算量。门控网络规模较小（隐藏维度在8-256之间实验），可认为算力需求适中。

## 5. 实验数量与充分性

- **主要实验**：在3个数据集上进行全量对比，报告Hits@1/5、R@20、MRR四个指标。
- **消融实验**：系统性移除文本检索器、关系检索器、混合门，共3组，验证各模块贡献。
- **敏感性分析**：改变门控网络隐藏维度（8-256），在MAG数据集上分析性能变化。
- **案例研究**：展示门控权重的可解释性（Prime数据集）。
- **补充实验**：附录中使用MiniLM-L6、mpnet-base、MiniLM-L12三种不同编码器验证泛化性；在人类生成查询子集上评估。
- **充分性评价**：实验覆盖了多个领域、多种基线、多维度消融和敏感性，设计较为全面。但未与最新大模型（如GPT-4、Llama-3）对比重排序效果，也未在更复杂多跳推理场景中深入评估。

## 6. 论文的主要结论与发现

- CoRAG在所有数据集上优于现有混合RAG方法，尤其在需要深层语义推理的学术（MAG）和医学（Prime）领域提升显著（如MAG上Hits@1相对提升11.4%）。
- 文本检索器和关系检索器均不可或缺，且不同领域对关系信息的依赖程度不同（如医学领域关系检索更重要）。
- 分层门控机制能根据查询自适应选择检索源，具有可解释性（案例中门控权重与问题需求一致）。
- 全局文本检索弥补了图遍历的局部性限制，是性能提升的关键。

## 7. 优点

- **方法创新**：提出动态门控融合文本和关系检索，解决了现有方法盲目融合的问题，且通过全局文本检索打破局部性约束。
- **可解释性**：门控权重可直观展示模型对实体类型和关系类型的关注度，有助于理解检索过程。
- **实验设计严谨**：包含消融、敏感性、案例、多种编码器、人类查询子集等分析，验证了鲁棒性和泛化性。
- **领域通用性**：在电商、学术、医学三个差异较大的数据集上均表现优异。

## 8. 不足与局限

- **多跳推理能力弱**：训练仅依赖最终答案监督，缺乏中间推理步骤的指导，难以处理复杂逻辑查询。作者承认这一局限，并建议未来引入LLM生成推理步骤或强化学习。
- **主题实体提取依赖规则**：使用Aho-Corasick和贪心匹配，可能遗漏或误识别实体，虽然可选LLM修剪，但仍可能成为性能瓶颈。
- **计算资源未详细报告**：未给出具体GPU数量和训练时长，复现成本不明确。
- **重排序器依赖闭源API**：使用GPT-4o-mini，成本较高且无法本地部署，可能影响实际应用。
- **未与最新大型模型对比**：仅对比了较小规模的基线（如DPR、QAGNN），未与GPT-4/Claude-3等强大模型直接比较重排序性能。
- **实验局限**：未在纯文本或纯图场景下单独验证CoRAG的适应性，也未评估对超过25个候选实体的扩展性。

（完）

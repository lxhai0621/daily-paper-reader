---
title: Mixture of Structural-and-Textual Retrieval over Text-rich Graph Knowledge Bases
title_zh: 文本丰富图知识库上的结构与文本检索混合方法
authors: "Yongjia Lei, Haoyu Han, Ryan A. Rossi, Franck Dernoncourt, Nedim Lipka, Mahantesh M Halappanavar, Jiliang Tang, Yu Wang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.941.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 文本丰富图知识库上的结构与文本检索混合
tldr: 现有方法通常孤立检索结构化与文本化知识，忽视其相互增强。本文提出MoR框架，通过规划-推理-组织流程交织结构遍历与文本匹配，从文本丰富图知识库中协同检索两类知识。实验表明该方法显著优于独立或混合基线，有效提升了查询应答的准确性。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.941/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 820, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.941/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.941/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 815, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.941/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 835, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.941/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.941/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 801, \"height\": 646, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1662, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 622, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 816, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 831, \"height\": 632, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 847, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 790, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 778, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 797, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.941/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 794, \"height\": 267, \"label\": \"Table\"}]"
motivation: 文本丰富图知识库中的结构和文本知识常被孤立检索，未利用其互补性。
method: 提出规划-推理-组织框架，交替进行结构遍历和文本匹配以获取互补知识。
result: 在多个基准上检索和问答准确率显著提升。
conclusion: 结构与文本检索的协同可大幅增强图知识库查询性能。
---

## Abstract
Text-rich Graph Knowledge Bases (TG-KBs) have become increasingly crucial for answering queries by providing textual and structural knowledge. However, current retrieval methods often retrieve these two types of knowledge in isolation without considering their mutual reinforcement and existing hybrid methods even bypass structural retrieval entirely. To fill this gap, we propose a Mixture of Structural-and-Textual Retrieval (MoR) to retrieve these two types of knowledge via a Planning-Reasoning-Organizing framework. In the Planning stage, MoR generates textual planning graphs delineating the logic for answering queries. Following planning graphs, in the Reasoning stage, MoR interweaves structural traversal and textual matching to obtain candidates from TG-KBs. In the Organizing stage, MoR further reranks fetched candidates based on their structural trajectory. Extensive experiments demonstrate the superiority of MoR in harmonizing structural and textual retrieval with inspiring insights, including imbalanced retrieving performance across different query logics and the benefits of integrating structural trajectories for candidate reranking.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

文本丰富图知识库（TG-KBs）同时包含文本化知识和结构化知识（如节点属性、边关系），在问答等任务中至关重要。然而，现有检索方法通常**孤立地**进行文本检索或结构检索，未能利用两者的相互增强。部分混合方法虽然融合了信息，但往往在邻居聚合后完全放弃结构检索，导致三个主要挑战：

- 频繁调用LLM聚合邻居导致资源开销过大；
- 聚合后丢弃结构信号，丢失逻辑规划信息；
- 不同查询和TG-KB对结构和文本知识的需求不同，刚性聚合无法自适应调整。

为此，论文提出**MoR（Mixture of Structural-and-Textual Retrieval）**，核心思想是**将混合专家（MoE）哲学引入检索设计**，通过**规划-推理-组织**三阶段框架，交替进行结构遍历和文本匹配，实现两类知识的协同检索。

## 2. 方法论：核心思想、关键技术细节

MoR框架包含三个模块，整体概率模型分解为三个条件分布：

### 2.1 规划阶段（Planning via Textual Graph Generation）
- **生成规划图**：将查询分解为多个推理路径（reasoning paths），每个路径由一系列实体节点（含类别和文本约束）构成，例如 `Institution → Author → Paper`。
- 采用**LLM（Llama 3.2-3B）** 生成规划图，通过一对一shot prompt合成训练数据，并微调模型。
- 避免逐步骤调用LLM，一次性生成整个规划图以提高效率。

### 2.2 推理阶段（Reasoning via Mixed Traversal）
- 沿规划图的推理路径，**交织进行结构遍历和文本匹配**：
  - **结构遍历**：按路径指定实体类别，逐层BFS遍历邻居节点，获取符合类别的候选。
  - **文本匹配**：对每个路径节点，用扩展查询（原查询 + 节点文本约束）进行BM25（或Contriever）检索，取Top-K。
- 每层候选集合 = 结构结果 ∪ 文本结果，作为下一层种子。
- 所有路径的最终候选取交集，确保满足所有逻辑约束。

### 2.3 组织阶段（Organizing via Structure-aware Rerank）
- 对中间候选，利用其**遍历轨迹**提取三种特征：
  - **Textual Fingerprint (TF)**：路径各节点的文本相似度序列。
  - **Structural Fingerprint (SF)**：节点类别序列。
  - **Traversal Identifier (TI)**：指示每步是结构还是文本检索的标志。
- 训练一个轻量级reranker（含线性层+Transformer），用交叉熵损失优化，对候选排序输出Top-K。

## 3. 实验设计

### 3.1 数据集
使用**STaRK基准**中的三个TG-KB：
- **Amazon**（电商产品，1M+实体，592M文本token）
- **MAG**（学术论文，1.87M实体，212M token）
- **Prime**（生物医学，129K实体，31.8M token）

### 3.2 对比方法
- **纯文本检索**：BM25, Ada-002, Multi-ada-002, DPR
- **纯结构检索**：QAGNN, ToG
- **混合检索**：AvaTaR, KAR, MFAR*, HYBGRAG

### 3.3 评价指标
Hit@1, Hit@5, Recall@20, MRR（全谱评估）

## 4. 资源与算力

论文**未明确说明使用的GPU型号、数量及训练时长**。仅提到：
- 规划图生成器使用**Llama 3.2-3B**微调，采用8-bit AdamW优化器，batch size=4，gradient accumulation=8，训练100 epoch或1000 steps。
- 推理阶段采用并行化优化，组织阶段使用batch计算。
- 未提供完整的硬件资源配置信息。

## 5. 实验数量与充分性

- **主实验**：在三个数据集上对比10+种基线，报告四项指标，结果充分。
- **消融实验**：
  - **模块消融**：逐步移除reranker、文本检索、结构检索，验证各部分贡献。
  - **特征消融**：对reranker的TF、SF、TI三种特征分别组合测试（2^3=8种组合）。
  - **路径vs节点特征**：比较使用完整轨迹与仅使用最后一节点。
- **进一步分析**：
  - 不同逻辑结构下的性能分布（图3）。
  - 检索源贡献比例（结构/文本）与信息占比（图5）。
  - 规划图生成准确率（表9）。
  - QA下游任务对比（表11）。
- **效率分析**：理论时间复杂度与实证时间（表4、5）。
- **公平性**：对比方法来自原基准文献和最新SOTA，消融实验严格控制变量，结论可靠。

## 6. 主要结论与发现

1. **MoR在三个数据集上平均达到最优**，在MAG上全面领先，Amazon和Prime上位居前二。
2. **混合检索优于单一文本或结构检索**，验证两类知识协同的必要性。
3. **结构感知reranker显著提升性能**，尤其对依赖结构信号的MAG增益明显。
4. **不同数据集对结构/文本偏好不同**：Amazon更依赖文本，MAG更依赖结构，Prime需要领域微调。
5. **规划图生成准确率较高**（MAG 88.85%，Amazon 70.03%，Prime 60.44%），但仍受限于LLM领域知识不足。
6. **轨迹特征（SF, TI）在MAG上贡献大**，在Amazon上作用有限，体现数据集特征差异。

## 7. 优点

- **创新性**：首次在TG-KB检索中系统引入MoE思想，规划-推理-组织框架新颖且合理。
- **自适应性**：通过混合遍历和reranker动态平衡结构/文本知识，无需手工规则。
- **可解释性**：清晰展示每个检索步骤的轨迹，便于分析决策过程。
- **效率优化**：采用并行化、批处理降低推理开销，理论复杂度可控。
- **实验全面**：涵盖多维度消融、特征分析、下游QA验证，结论可靠。

## 8. 不足与局限

1. **领域知识瓶颈**：在生物医学（Prime）上性能提升有限，通用LLM缺乏深度领域知识，规划图生成准确率低。
2. **仅最终层rerank**：未在中间层进行路由选择，可能错过更优子图探索。
3. **单轨迹利用**：实际多路径可达同一候选，但当前仅使用最长轨迹，信息利用不充分。
4. **计算复杂度指数增长**：随着路径深度增加，候选数量指数膨胀，虽可通过并行缓解，但大图上仍有压力。
5. **未公开完整算力细节**：无法复现资源消耗，影响可复现性。
6. **实验局限**：仅在三个英文TG-KB上测试，未验证跨语言或更大规模图的效果；未与动态检索等方法对比。

（完）

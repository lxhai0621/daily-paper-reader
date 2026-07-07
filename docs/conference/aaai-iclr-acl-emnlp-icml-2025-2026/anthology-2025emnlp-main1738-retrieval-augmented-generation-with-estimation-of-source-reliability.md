---
title: Retrieval-Augmented Generation with Estimation of Source Reliability
title_zh: 基于源可靠性估计的检索增强生成
authors: "Jeongyeon Hwang, Junyoung Park, Hyejin Park, Dongwoo Kim, Sangdon Park, Jungseul Ok"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1738.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 多源RAG结合源可靠性估计
tldr: 标准RAG仅依据查询与文档的相关性检索，忽略了不同来源的可靠性差异，可能引入错误信息。RA-RAG通过估计每个来源的可靠性，在检索时优先选择高可靠性和相关性的文档。实验证明该方法显著提升了RAG系统的准确性和鲁棒性。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 464, \"height\": 302, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 524, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1494, \"height\": 376, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1495, \"height\": 887, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1486, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1500, \"height\": 891, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 813, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 696, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1738/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1572, \"height\": 420, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1412, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 417, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1168, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 698, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 754, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 385, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1336, \"height\": 999, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1339, \"height\": 894, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 787, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 789, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1171, \"height\": 753, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1171, \"height\": 752, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1171, \"height\": 753, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1171, \"height\": 752, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1171, \"height\": 753, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1171, \"height\": 752, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1171, \"height\": 753, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1171, \"height\": 752, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1738/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1170, \"height\": 752, \"label\": \"Table\"}]"
motivation: 标准RAG忽略来源可靠性差异，可能检索到错误信息。
method: 估计来源可靠性，并据此优先选择可靠且相关的文档。
result: RA-RAG在多项任务中显著提升准确性和鲁棒性。
conclusion: 纳入源可靠性估计是增强RAG系统有效性的关键。
---

## Abstract
Retrieval-Augmented Generation (RAG) is an effective approach to enhance the factual accuracy of large language models (LLMs) by retrieving information from external databases, which are typically composed of diverse sources, to supplement the limited internal knowledge of LLMs. However, the standard RAG often risks retrieving incorrect information, as it relies solely on relevance between a query and a document, overlooking the heterogeneous reliability of these sources. To address this issue, we propose Reliability-Aware RAG (RA-RAG), a new multi-source RAG framework that estimates the reliability of sources and leverages this information to prioritize highly reliable and relevant documents, ensuring more robust and accurate response generation. Specifically, RA-RAG first estimates source reliability by cross-checking information across multiple sources. It then retrieves documents from the top- 𝜅 reliable and relevant sources and aggregates their information using weighted majority voting (WMV), where the selective retrieval ensures scalability while not compromising the performance. Comprehensive experiments show that RA-RAG consistently outperforms baselines in scenarios with heterogeneous source reliability while scaling efficiently as the number of sources increases. Furthermore, we demonstrate the ability of RA-RAG to estimate real-world sources’ reliability, highlighting its practical applicability. Our code and data are available at RA-RAG.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：标准RAG系统仅依赖查询与文档之间的相关性进行检索，忽略了不同信息源（如网站、社交媒体账号）的可靠性差异。这导致不可靠来源可能通过生成高相关但虚假的文档来污染检索结果，最终使LLM产生误导性输出。
- **整体含义**：本文提出一种能主动估计来源可靠性的多源RAG框架，将可靠性信息融入检索与答案聚合过程，从而提升系统对虚假信息的鲁棒性和准确性。

## 2. 方法论
- **核心思想**：将数据库按来源（source）划分，对每个来源单独检索并生成候选答案，然后利用估计出的来源可靠性进行加权多数投票（WMV）得到最终答案。
- **关键技术细节**：
  - **可靠性估计**：使用一组事实核查查询（fact-checking queries），对每个查询，从各个来源检索文档并生成答案。通过迭代的WMV算法（类似Li & Yu, 2014的加权多数投票）估计每个来源的可靠性权重 \(v_i\)。具体步骤：
    1. 初始化所有来源权重为1。
    2. 对每个事实核查查询，用当前权重进行WMV得到聚合答案。
    3. 根据每个来源的答案与聚合答案的一致性更新权重，并缩放到 \(v_i = N \hat{w}_i - 1\)。
  - **聚合阶段**：
    - 对每个来源的答案进行对齐过滤（使用AlignScore检测是否与检索文档一致，不一致则替换为“I don't know”）。
    - 使用语义聚类（基于NLI模型）合并等价答案。
    - 采用**κ-RRSS**（κ Reliable and Relevant Source Selection）：按可靠性降序遍历来源，选取前κ个包含相关文档（过滤后非IDK）的来源，仅对这些来源的答案进行WMV聚合。
- **公式与算法**（文字说明）：
  - 答案聚合：\(\hat{y} = \arg\max_{u \in C(M_{\text{filtered}})} \sum_i v_i \cdot \mathbb{1}(\text{align}(\hat{y}_i) = u)\)
  - κ-RRSS算法：对来源按可靠性排序，依次检查其答案是否非IDK，选中κ个后停止。
- **亮点**：无需人工事实核查，利用RAG自身能力自动生成查询和答案；κ-RRSS在保持性能的同时大幅降低计算开销。

## 3. 实验设计
- **数据集与场景**：
  - 使用三个问答数据集：Natural Questions (NQ)、TriviaQA (TQA)、HotpotQA（仅单跳）。
  - 构建多源异构可靠性基准：每个来源由参数 \(p_i\)（提供真实信息的概率）和 \(r_i\)（包含相关文档的概率）控制。采用两种先验：
    - Beta先验：连续可靠性分布，平均为0.6。
    - Adversary-hammer先验：极端情况，\(p_i\) 为0.1或0.9。
  - 每个数据集1600个查询（200用于可靠性估计，1400用于测试）。
- **基准方法**：
  - Oracle WMV（完美知道真实可靠性，上限）
  - MV（等权多数投票）
  - Vanilla RAG（标准RAG）
  - Robust RAG（认证鲁棒方法）
  - Self-RAG（自适应检索）
  - Vanilla LLM（无检索）
- **模型**：主要使用Llama3-8B-Instruct、Phi3-mini-Instruct、GPT-4o-mini、Llama2-7B。检索器使用Contriever。
- **评估指标**：准确性（答案包含黄金答案）。

## 4. 资源与算力
- 论文**未明确说明**GPU型号、数量、训练总时长等信息。仅在附录J中提到使用单块RTX 6000 Ada GPU进行推理时间测量，但未给出整体训练/估计的算力消耗。属于不足之一。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：在Beta先验下，对3个数据集×4种模型×6种来源数量（4~9）进行对比；在Adversary-hammer先验下，对3个数据集×Llama3-8B模型×7种对抗源数量进行对比。
  - 消融实验：包括κ的敏感性、κ-RRSS有无、过滤模块效果、可靠性估计准确性等。
  - 真实世界应用：使用PolitiFact收集的3个真实来源（两位政治家、一个X用户），评估可靠性估计的准确性（PCC、SRCC），并做增强实验。
- **充分性与公平性**：
  - 实验覆盖多个数据集、多种模型、多种可靠性分布，非常全面。
  - 对比了强基线（Oracle WMV、Self-RAG等），结果清晰表明RA-RAG优于其他方法。
  - 报告了多次随机实验的平均值，并分析了统计显著性（p值）。
  - 但缺乏对长文本、多跳QA等更复杂任务的评估，作者也承认这是未来工作。

## 6. 主要结论与发现
- RA-RAG在异构可靠性场景下**一致优于**所有基线，性能接近Oracle WMV（完美知识）。
- **κ-RRSS**能有效降低计算开销（如1000个来源时减少99.1%的token消耗），同时不牺牲准确率。
- **现实世界应用**：在Politician A、B和User A三个真实来源上，估计的可靠性高度相关（PCC>0.99），验证了方法的实用性。
- 过滤模块（AlignScore）能显著减少LLM在无关或虚假文档上的幻觉输出，改善聚合质量。

## 7. 优点
- **创新性**：首次显式地将来源可靠性估计嵌入RAG系统，解决标准RAG忽视来源差异的根本缺陷。
- **自监督性**：无需人工标注，利用RAG自身生成查询和答案进行可靠性估计。
- **可扩展性**：κ-RRSS使得在大量来源下计算可行。
- **鲁棒性**：在对抗性场景（adversary-hammer）中表现远超其他方法，MV和Robust RAG在多数对抗源下显著下降。
- **实验全面**：涵盖合成数据与真实世界数据，多种模型和设置。

## 8. 不足与局限
- **任务局限**：目前仅针对短文本问答，未验证长文本、多跳问答等复杂任务。作者虽提出分解思路，但无实验结果。
- **算力未明**：未提供完整的训练/估计算力消耗，复现成本不确定。
- **离线更新**：可靠性估计是离线进行的，无法动态适应来源可靠性变化（如账号被盗后突然传播虚假信息）。需要定期重估。
- **专业领域限制**：对于缺乏足够交叉验证来源的专门话题（如小众科技），可靠性估计可能不准确。
- **安全威胁**：即使可靠来源也可能突然大规模输出虚假信息（如被黑客攻击），离线估计无法即时响应。

（完）

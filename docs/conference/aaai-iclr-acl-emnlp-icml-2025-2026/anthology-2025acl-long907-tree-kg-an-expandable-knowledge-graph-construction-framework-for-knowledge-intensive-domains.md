---
title: "Tree-KG: An Expandable Knowledge Graph Construction Framework for Knowledge-intensive Domains"
title_zh: Tree-KG：面向知识密集型领域的可扩展知识图谱构建框架
authors: "Songjie Niu, Kaisen Yang, Rui Zhao, Yichao Liu, Zonglin Li, Hongning Wang, Wenguang Chen"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.907.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 可扩展知识图谱构建框架
tldr: 针对知识密集型领域构建知识图谱的复杂性高和更新慢的问题，Tree-KG提出一种可扩展的框架。它先利用LLM从教科书结构构建树状图，再通过预定义操作符迭代扩展，支持动态整合结构化与语义信息。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 766, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 1028, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 598, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 565, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 815, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1632, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.907/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1302, \"height\": 391, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.907/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1486, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.907/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.907/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 199, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.907/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 130, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.907/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 406, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.907/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1261, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.907/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1647, \"height\": 328, \"label\": \"Table\"}]"
motivation: 现有KG构建方法难以适应知识快速演化和高度复杂领域。
method: 结合LLM和领域实体构建初始树状图，再通过迭代操作符扩展。
result: 在多个知识密集型领域取得了高质量的KG构建效果。
conclusion: Tree-KG提供了一种灵活高效的知识图谱构建方案。
---

## Abstract
In knowledge-intensive domains like scientific research, effective decisions rely on organizing and retrieving intricate data. Knowledge graphs (KGs) help by structuring entities, relations, and contextual dependencies, but building KGs in such domains is challenging due to inherent complexity, manual effort, and rapid evolution. Inspired by how humans organize knowledge hierarchically, we propose Tree-KG, an expandable framework that combines structured domain texts with advanced semantic techniques. First, Tree-KG builds a tree-like graph from textbook structures using large language models (LLMs) and domain-specific entities, creating an explicit KG . Then, through iterative expansion with flexible, predefined operators, it uncovers hidden KG while preserving semantic coherence. Experiments demonstrate that Tree-KG consistently surpasses competing methods, achieving the highest F1 scores (12–16% above the second-best), with notable performance (F1 0.81) on the Text-Annotated dataset, highlighting its effectiveness in extracting high-quality information from source texts. Additionally, Tree-KG provides superior structural alignment, domain-specific extraction, and cost-efficiency, delivering robust results with reduced token usage and adaptable, resource-conscious deployment.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：知识密集型领域（如科学研究、医疗、金融）依赖大量专业知识进行决策，知识图谱（KG）能有效组织实体、关系及上下文依赖。然而，此类领域知识复杂度高、人工构建成本大、知识更新快，现有KG构建方法难以兼顾自动化、准确性、可扩展性和增量学习。
- **整体含义**：受人类层级化组织知识（如教科书结构）启发，作者提出Tree-KG——一个可扩展框架，利用大型语言模型（LLM）从结构化领域文本中构建初始显式KG，再通过预定义的算子迭代扩展，发现隐藏关系，保持语义一致性。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将教科书等结构化文档的层级关系作为骨架，构建树状层次KG；之后通过一系列算子（卷积、聚合、去重、边预测等）自动扩展隐藏知识，支持新文本源增量集成。
- **关键技术细节**：
  - **树状层次图定义**：
    - 节点分层：\( V = V_1 \cup V_2 \cup \cdots \cup V_k \)，每层不相交。
    - 边分两类：垂直边 \(E_1\) 仅连接相邻层节点，形成树；水平边 \(E_2\) 连接同层节点。
  - **KG Schema**：
    - 节点属性：name、description、relations。
    - 垂直边类型：`has_subsection`、`has_entity`、`has_subordinate`。
    - 水平边类型：`section_related` / `entity_related` 加上LLM预测的具体关系（如`obey`、`has`）。
  - **初始构建（Phase 1）**：
    - 文本分割：利用正则解析教科书章节/小节。
    - 自底向上摘要：对无子节点的叶子节点用LLM生成摘要，父节点聚合子节点摘要。
    - 实体与关系提取：LLM从摘要中提取实体、`has_entity`边以及`entity_related`水平边。
  - **迭代扩展（Phase 2）**：
    - **上下文卷积（conv）**：用LLM结合邻居信息更新实体描述，类似图卷积，通常一次即足够。
    - **实体聚合（aggr）**：根据LLM判定实体角色（core / non-core），将非核心实体作为核心实体的子节点（添加`has_subordinate`垂直边）。
    - **节点嵌入（embed）**：将描述嵌入为归一化向量（L2范数=1），用于后续检索和相似度计算。
    - **实体去重（dedup）**：基于嵌入相似度（阈值0.55）和LLM判断，合并相同实体（用并查集）。
    - **边预测（pred）**：基于打分函数 \( \text{score} = \alpha \cdot \cos(z_u, z_v) + \beta \cdot \text{AA} + \gamma \cdot \text{CA} \)，其中AA为Adamic-Adar分数，CA为共同祖先数。先通过第一阶段（\(\beta=0, \gamma=0.4\)）初始化连通性，再第二阶段（\(\beta=0.3, \gamma=0.1\)）补全边。
    - **结构集成（merge）**：将新文本源视为子图，通过嵌入相似度或唯一ID合并重叠实体，并采用图着色最小化跨章节边。

## 3. 实验设计：数据集、Benchmark、对比方法

- **数据集**：
  - 来自AI4EDU项目，约69,000份专业材料（教科书、讲义、论文），涵盖约100子领域、995万知识点。
  - 聚焦三个领域：物理（电磁、光学、量子）、数字电子、教育心理学。
  - 物理领域有三个ground truth：
    - Domain-Annotated KG：专家全领域标注。
    - Text-Annotated KG：专家从教材手工提取。
    - Appendix-List：教材附录知识点列表。
- **Benchmark方法**：GraphRAG、iText2KG、LangChain、AutoKG。SAC-KG因不可用未包含。
- **评估策略**：
  - **Ground truth评估**：计算ER、PC、F1、MEC、MED。
  - **互评估（5×5）**：各方法提取的实体集互为ground truth，计算ER。
  - **LLM评估**：用LLM生成实体特异性（ES）、完整性（EC）和关系强度（RS）。

## 4. 资源与算力

- **文中说明**：所有对比方法在SiliconFlow平台上使用DeepSeek-V3 API（2 RMB/M输入token，8 RMB/M输出）。Tree-KG的消融实验使用GLM-4-Air（1 RMB/M token）。**未明确提及GPU型号、数量或训练时长**。仅报告了token消耗和费用（见表3），Tree-KG总token约6.1M，费用18元，远低于LangChain（15M, 28元）等。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验（表1、表2）：物理领域对ground truth和LLM评估，以及三领域互评估（5×5表2和表7），共涉及多组指标。
  - 消融实验（4.3节）：4组（有无摘要、卷积步数、去重阈值、边预测超参数敏感度），均配有定量结果和图。
  - 附录更多实验：边预测额外边数影响（表6）、卷积PCA可视化、案例研究。
- **充分性评估**：实验设计全面，覆盖了多个数据集、多种指标、多个领域。消融验证了各组件贡献（摘要提升ES 9%、RS 8%；卷积提升EC 34%、RS 10%）。互评估避免了单一ground truth偏差。评估采用人工标注和LLM双重验证，公平性较好。但对比方法未包含SAC-KG等最新同类工作，且仅涉及三个知识密集型领域，泛化性需进一步验证。

## 6. 主要结论与发现

- Tree-KG在F1指标上超越所有对比方法12%-16%，在Text-Annotated上达到0.81 F1，表明其从原始文本中提取高质量信息的能力。
- 结构对齐最优：MEC最高（1.6x-20x），MED最低（0.8x-1.1x），更利于下游推理。
- 实体特异性（ES）和关系强度（RS）均领先，表明提取的实体和关系精准且关联紧密。
- 成本效率高：token消耗和费用低于LangChain和AutoKG，与iText2KG相当，远低于GraphRAG。
- 消融实验证实各算子有效：总结、上下文卷积、去重、边预测均显著提升KG质量。

## 7. 优点

- **可扩展性**：支持增量引入新文本源，并通过算子自动扩展KG，适合知识快速演化的领域。
- **结构清晰**：树状层次图模仿人类认知组织方式，便于导航和扩展。
- **算子驱动的灵活性**：预定义算子（conv、aggr、dedup、pred等）可组合调用，适应不同需求。
- **语义一致性**：利用LLM在上下文中生成描述和关系，并结合图结构信息，保持实体间逻辑连贯。
- **成本优势**：利用教科书结构减少LLM调用，总体token消耗较低，且可选仅初始构建阶段，适应低资源场景。
- **实验验证充分**：多维度评估（ground truth、互评估、LLM评估）和系统性消融，验证了方法有效性。

## 8. 不足与局限

- **依赖LLM质量**：实体/关系提取、摘要、卷积等均依赖LLM，模型性能直接影响KG质量。论文未讨论LLM在低资源语言或小模型下的适应性。
- **下游任务验证缺失**：论文仅评估KG本身质量，未在具体下游任务（如问答、推理）上测试效果。作者在Limitations中承认该方法可能不适用于推理等任务。
- **实验覆盖有限**：仅涉及三个领域（物理、数字电子、教育心理学），且主要基于教科书数据，对于非结构化、多源异构数据的泛化性未充分测试。
- **对比方法选择性缺失**：未与SAC-KG等同类最新框架比较，可能高估自身优势。
- **阈值与超参数依赖**：去重阈值（0.55）、边预测权重（α=0.6, β=0.3, γ=0.1）等需手动设定，且对结果敏感，可能影响鲁棒性。
- **处理噪声文本的能力**：论文假设输入为结构良好的教科书，对于格式混乱或噪音多的文本，文本分割和摘要可能失效。

（完）

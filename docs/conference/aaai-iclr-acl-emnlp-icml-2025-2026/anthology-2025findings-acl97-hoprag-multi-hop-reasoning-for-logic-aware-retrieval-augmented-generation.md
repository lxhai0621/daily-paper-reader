---
title: "HopRAG: Multi-Hop Reasoning for Logic-Aware Retrieval-Augmented Generation"
title_zh: HopRAG：用于逻辑感知检索增强生成的多跳推理
authors: "Hao Liu, Zhengren Wang, Xi Chen, Zhiyu Li, Feiyu Xiong, Qinhan Yu, Wentao Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.97.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 提出HopRAG，一种多跳推理的逻辑感知检索增强生成框架
tldr: 传统RAG检索器只关注词汇或语义相似性，忽略了逻辑相关性。HopRAG在索引阶段构建片段图，通过LLM生成的伪查询建立逻辑边；检索时采用检索-推理-剪枝机制，从初始相似片段出发，沿多跳邻居探索真正相关的片段。实验证明逻辑感知检索能显著提升多跳推理任务效果。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 743, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1594, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1624, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1243, \"height\": 1227, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1245, \"height\": 1242, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1255, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.97/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1153, \"height\": 296, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 726, \"height\": 1043, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1153, \"height\": 545, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1156, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1483, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1487, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1485, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1319, \"height\": 886, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1523, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1630, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.97/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1607, \"height\": 2314, \"label\": \"Table\"}]"
motivation: RAG检索缺乏逻辑相关性考量，导致多跳推理任务检索不准确。
method: 构建片段图并利用LLM生成伪查询建立逻辑边，采用检索-推理-剪枝的多跳机制。
result: 在多个基准上优于传统RAG方法。
conclusion: 逻辑感知的多跳推理检索能有效提升RAG系统准确性。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems often struggle with imperfect retrieval, as traditional retrievers focus on lexical or semantic similarity rather than logical relevance. To address this, we propose HopRAG , a novel RAG framework that augments retrieval with logical reasoning through graph-structured knowledge exploration. During indexing, HopRAG constructs a passage graph, with text chunks as vertices and logical connections established via LLM-generated pseudo-queries as edges. During retrieval, it employs a retrieve-reason-prune mechanism: starting with lexically or semantically similar passages, the system explores multi-hop neighbors guided by pseudo-queries and LLM reasoning to identify truly relevant ones. Experiments on multiple multi-hop benchmarks demonstrate that HopRAG’s retrieve-reason-prune mechanism can expand the retrieval scope based on logical connections and improve final answer quality.

---

## 论文详细总结（自动生成）

### 论文结构化总结

#### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：传统 RAG 系统的检索器（如稀疏检索 BM25、稠密检索 BGE）仅基于词汇或语义相似性，无法捕捉**逻辑相关性**。在需要多个片段联合推理的多跳 QA 任务中，检索结果往往包含大量“间接相关”或“不相关”的片段，导致回答不准确或不完整。
- **背景**：研究表明，即使使用先进搜索引擎，约 70% 的检索片段并不直接包含正确答案。作者受“六度分隔理论”启发，认为这些间接相关片段可作为“跳板”，通过逻辑关系跳跃到真正相关的片段。因此，自然的研究问题是：能否将推理能力引入检索模块？

#### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：构建一个**逻辑感知的图结构索引**，并在检索时通过**推理增强的图遍历**从间接相关片段跳到真正相关片段。
- **关键技术细节**：
  - **索引阶段**：
    - 顶点：每个文本片段作为一个顶点。
    - 边：利用 LLM 为每个片段生成两组**伪查询**：
      - 出向问题（out-coming）：该片段不能回答但能引出其他片段的问题。
      - 入向问题（in-coming）：该片段能回答的问题。
    - 通过混合检索（稀疏关键词 Jaccard + 稠密向量余弦相似度）匹配出向和入向问题，在对应片段之间建立**有向边**，边上存储匹配的问题、关键词和向量。
  - **检索阶段（检索-推理-剪枝）**：
    - **检索**：对用户查询提取关键词和向量，通过混合检索找到 top k 条边，将边指向的顶点加入队列。
    - **推理**：对于队列中的每个顶点，让 LLM 选择其出边中最有助于回答用户查询的边，跳转到目标顶点，重复多轮（`nhop` 次）。用计数器 `Ccount` 记录每个顶点被访问的次数，衡量其逻辑重要性。
    - **剪枝**：定义新指标 **Helpfulness**，综合顶点与查询的文本相似度（`SIM`）和逻辑重要性（`IMP`，归一化的访问次数），保留 top k 个顶点作为最终上下文。
  - **公式**：
    - `SIM(r⁺, r⁻)` = (关键词 Jaccard + 向量余弦相似度) / 2
    - `Hᵢ = SIM(vᵢ, q) + IMP(vᵢ, Ccount) / 2`
    - `IMP(vᵢ, Ccount) = Ccount[vᵢ] / sum(Ccount)`s

#### 3. 实验设计：数据集、基准、对比方法
- **数据集**：三个多跳 QA 基准
  - **HotpotQA**（1000 问题，验证集）
  - **2WikiMultiHopQA**（1000 问题）
  - **MuSiQue**（1000 问题）
- **对比方法**：
  - 非结构化 RAG：BM25、BGE、BGE + 查询分解、BGE + 重排序
  - 树结构 RAG：RAPTOR、SiReRAG
  - 图结构 RAG：GraphRAG、HippoRAG
- **评估指标**：
  - 答案质量：Exact Match (EM) 和 F1 分数（使用 GPT-4o 和 GPT-3.5-turbo 作为推理模型）
  - 检索质量（部分消融实验）：检索 F1 分数

#### 4. 资源与算力
- 论文**未明确说明**具体 GPU 型号、数量或训练时长。所有 LLM 调用（生成伪查询、推理遍历、最终回答）均使用闭源 API（GPT-4o-mini、GPT-4o、GPT-3.5-turbo），无训练过程。仅提到使用 BGE-base 嵌入模型（推理）和 Neo4j 图数据库。算力消耗主要体现在 LLM API 调用次数和延迟上。

#### 5. 实验数量与充分性
- **实验组数**：
  - 主实验结果（表1、2）：在两个推理模型、三个数据集上对比八种基线，共计约 2×3×8 ≈ 48 组结果。
  - top k 鲁棒性实验（表3）：在三种数据集上变化 top k (2~20)，报告答案和检索指标。
  - nhop 影响实验（表4）：变化 nhop (1~4)，报告检索 F1 和 LLM 调用次数。
  - 遍历模型消融（表5）：对比非 LLM、Qwen2.5-1.5B、GPT-4o-mini 作为遍历模型的性能。
  - 另外提供了案例研究（附录A.6）和效率分析（附录A.7）。
- **充分性评价**：实验设计较为全面，覆盖了主流基线、关键超参数和不同能力等级的遍历模型。但**仅针对多跳 QA 任务**，未推广到其他类型任务（如单跳 QA、摘要生成等），公平性方面所有基线均采用相同数据划分和 chunk 方式，具有可比性。

#### 6. 论文的主要结论与发现
- HopRAG 在几乎所有设置下取得最佳或次佳答案质量，**平均 EM/F1 比 BGE 提升 76.78%，比 SiReRAG 提升约 1.11%**。
- 通过图遍历，即使使用较少上下文（top 12），答案质量也能与使用 20 个片段的强基线持平，体现了**高效检索**。
- 将间接相关片段作为跳板确实能提高检索召回率（检索 F1 平均提升 20.97%）。
- 随着 `nhop` 增加，检索性能提升，但 LLM 调用成本线性增加，存在 trade-off；4 轮跳转足以覆盖大多数局部区域。
- 使用小型 LLM（Qwen2.5-1.5B）作为遍历模型也能取得有竞争力的结果，降低计算成本。

#### 7. 优点：方法或实验设计上的亮点
- **逻辑感知的图结构**：区别于传统图谱的预定义 schema，HopRAG 通过 LLM 生成的伪查询灵活建模片段间逻辑关系，无需实体提取或文本化，**下游任务友好**。
- **检索-推理-剪枝机制**：首次将 LLM 推理直接用于指导检索的跳跃方向，与纯相似性检索相比，显著提升了多跳任务的精准度和完整性。
- **高效更新与构建**：每个片段独立生成伪查询，边匹配可并行，支持增量更新；图度数较低（平均每顶点约 5.87 边），遍历高效。
- **实验设计公平**：与基线共享相同的 chunk 方式和检索引擎（Neo4j），消融实验全面，包括非 LLM 版本，证明了推理引入的必要性。

#### 8. 不足与局限
- **任务覆盖有限**：仅在多跳 QA 上评估，未验证在单跳 QA、开放域问答、摘要生成等任务上的泛化能力。
- **依赖 LLM 推理**：遍历阶段需要多次调用 LLM（如 `nhop=4` 时平均 38.53 次），增加了响应延迟和 API 费用，虽然可用小型模型缓解但仍有开销。
- **图结构特性未充分利用**：论文指出当前图顶点度分布未呈现幂律特征（小世界网络特性），未来可探索更优的度分布策略。
- **边构建策略简单**：仅匹配最相似的出向/入向问题，未考虑更复杂的多对多匹配或加权策略。
- **超参数敏感**：`top k` 和 `nhop` 对结果有影响，虽通过实验给出了推荐值，但未提供自适应调整机制。
- **未讨论检索失败场景**：当初始检索完全无相关片段时，HopRAG 可能失效，论文未分析这类极端情况。

（完）

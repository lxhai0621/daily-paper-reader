---
title: "TRACE: Traversal Retrieval-Augmented Chain of Evidence for Document Understanding"
title_zh: TRACE：面向文档理解的遍历式检索增强证据链
authors: "Liqi He, Zuchao Li, Hao Huang, Ping Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.445.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 遍历式检索增强证据链构建
tldr: 早期长上下文文档视觉问答难以兼顾视觉语义与有限上下文窗口，而现有RAG方法因被动检索忽略逻辑依赖，存在语义鸿沟与结构断裂。本文提出TRACE，通过在同时编码物理邻接与语义相关性的双层图上导航，将静态匹配检索转变为自适应证据链构建，并提出M5BookVQA基准评估书籍多跳推理，提升了文档理解能力。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-003.webp\", \"caption\": \"\", \"page\": 1, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-004.webp\", \"caption\": \"\", \"page\": 1, \"index\": 4, \"width\": 491, \"height\": 433}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-005.webp\", \"caption\": \"\", \"page\": 1, \"index\": 5, \"width\": 594, \"height\": 433}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-006.webp\", \"caption\": \"\", \"page\": 1, \"index\": 6, \"width\": 508, \"height\": 441}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-007.webp\", \"caption\": \"\", \"page\": 3, \"index\": 7, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-008.webp\", \"caption\": \"\", \"page\": 3, \"index\": 8, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-009.webp\", \"caption\": \"\", \"page\": 3, \"index\": 9, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-010.webp\", \"caption\": \"\", \"page\": 3, \"index\": 10, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-011.webp\", \"caption\": \"\", \"page\": 3, \"index\": 11, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-012.webp\", \"caption\": \"\", \"page\": 3, \"index\": 12, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-013.webp\", \"caption\": \"\", \"page\": 3, \"index\": 13, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-014.webp\", \"caption\": \"\", \"page\": 3, \"index\": 14, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-015.webp\", \"caption\": \"\", \"page\": 3, \"index\": 15, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-016.webp\", \"caption\": \"\", \"page\": 3, \"index\": 16, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-017.webp\", \"caption\": \"\", \"page\": 3, \"index\": 17, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-018.webp\", \"caption\": \"\", \"page\": 3, \"index\": 18, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-019.webp\", \"caption\": \"\", \"page\": 3, \"index\": 19, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-020.webp\", \"caption\": \"\", \"page\": 3, \"index\": 20, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-021.webp\", \"caption\": \"\", \"page\": 3, \"index\": 21, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-022.webp\", \"caption\": \"\", \"page\": 5, \"index\": 22, \"width\": 841, \"height\": 841}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-023.webp\", \"caption\": \"\", \"page\": 5, \"index\": 23, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-024.webp\", \"caption\": \"\", \"page\": 5, \"index\": 24, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-025.webp\", \"caption\": \"\", \"page\": 5, \"index\": 25, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-026.webp\", \"caption\": \"\", \"page\": 5, \"index\": 26, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-027.webp\", \"caption\": \"\", \"page\": 5, \"index\": 27, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-028.webp\", \"caption\": \"\", \"page\": 5, \"index\": 28, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-029.webp\", \"caption\": \"\", \"page\": 5, \"index\": 29, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-030.webp\", \"caption\": \"\", \"page\": 5, \"index\": 30, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-031.webp\", \"caption\": \"\", \"page\": 13, \"index\": 31, \"width\": 994, \"height\": 732}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-032.webp\", \"caption\": \"\", \"page\": 13, \"index\": 32, \"width\": 980, \"height\": 733}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-033.webp\", \"caption\": \"\", \"page\": 13, \"index\": 33, \"width\": 852, \"height\": 449}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-034.webp\", \"caption\": \"\", \"page\": 13, \"index\": 34, \"width\": 715, \"height\": 444}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-035.webp\", \"caption\": \"\", \"page\": 13, \"index\": 35, \"width\": 393, \"height\": 341}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-036.webp\", \"caption\": \"\", \"page\": 13, \"index\": 36, \"width\": 852, \"height\": 449}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-037.webp\", \"caption\": \"\", \"page\": 13, \"index\": 37, \"width\": 715, \"height\": 444}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-038.webp\", \"caption\": \"\", \"page\": 13, \"index\": 38, \"width\": 393, \"height\": 341}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-039.webp\", \"caption\": \"\", \"page\": 14, \"index\": 39, \"width\": 1969, \"height\": 1830}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-040.webp\", \"caption\": \"\", \"page\": 18, \"index\": 40, \"width\": 1391, \"height\": 1809}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-041.webp\", \"caption\": \"\", \"page\": 18, \"index\": 41, \"width\": 1394, \"height\": 1811}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-042.webp\", \"caption\": \"\", \"page\": 19, \"index\": 42, \"width\": 789, \"height\": 1108}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-043.webp\", \"caption\": \"\", \"page\": 19, \"index\": 43, \"width\": 789, \"height\": 1109}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long445/fig-044.webp\", \"caption\": \"\", \"page\": 19, \"index\": 44, \"width\": 790, \"height\": 1109}]"
motivation: 长文档VQA受限于有限上下文窗口，RAG被动检索存在语义鸿沟与结构断裂。
method: 提出TRACE，在编码物理邻接与语义相关性的双层图上构建自适应证据链。
result: 提出M5BookVQA基准，评估书籍多跳推理并提升文档理解。
conclusion: 将静态匹配检索转变为自适应证据链构建。
---

## Abstract
Early Long-context Document Visual Question Answering (DocVQA) methods struggle with preserving visual semantics or handling finite context windows. Conversely, recent RAG-based approaches suffer from "semantic gaps" and "structural disconnections" due to passive retrieval mechanisms that ignore logical dependencies. To address these challenges, we introduce TRACE (Traversal Retrieval-Augmented Chain of Evidence). By navigating a Bi-Layered Graph that encodes both physical adjacency and semantic relevance, TRACE transforms retrieval from static matching into adaptive evidence chain construction. Furthermore, we propose M5BookVQA, a benchmark designed to assess deep, multi-hop reasoning in books, addressing the limitations of existing datasets. Extensive experiments show that TRACE achieves an average accuracy improvement of 14.07% on M5BookVQA and exhibits robust generalization with a 13.38% gain across four established benchmarks. Our source code is available at https://github.com/shimurenhlq/TRACE.

---

## 论文详细总结（自动生成）

# TRACE 论文中文总结

## 1. 核心问题与整体含义

- **研究背景**：长上下文文档视觉问答（Long-context DocVQA）是文档智能的核心任务，要求模型跨多页、多模态（文本、图表、图像、复杂版式）整合证据并推理。
- **现有方法瓶颈**：
  - 早期 LLM+OCR 方法会丢失视觉语义，难以处理图表、版式等视觉信息。
  - VLM 端到端方法虽保留视觉信息，但受有限上下文窗口限制，无法一次处理整本书或长报告。
  - 近期 RAG 方法多采用被动匹配机制，存在两类关键失败：
    - **语义鸿沟（Semantic Gaps）**：检索内容词汇相关但语义误导。
    - **结构断裂（Structural Disconnections）**：忽略页面间逻辑依赖，割裂证据链。
- **论文整体含义**：提出 **TRACE（Traversal Retrieval-Augmented Chain of Evidence）**，将检索从静态匹配转变为在双层图上的自适应证据链构建；同时发布 **M5BookVQA** 基准，用于评估书籍场景中的深度多跳推理。

## 2. 方法论

### 2.1 核心思想
- 将文档建模为同时编码**物理邻接**与**语义相关性**的**双层图**。
- 通过查询分解与自适应图导航，逐步构造有序的**证据链（Chain of Evidence）**，再基于证据链生成答案。
- 目标不是一次性 Top-k 检索，而是模拟人类浏览：定位、验证、回溯、跳跃、串联证据。

### 2.2 双层图构建
- **节点**：每个页面 \(p_i\) 为一个节点，使用 ColPali 映射为多向量嵌入 \(E_i \in \mathbb{R}^{n_v \times d}\)。
- **物理邻接层 \(E_{phy}\)**：在逻辑连续页面间建立有向边 \((v_i, v_{i+1})\)，支持“翻页”式顺序阅读。
- **语义相关层 \(E_{sem}\)**：用 MaxSim 计算页面间 token 级相似度：
  - 对 \(E_i\) 中每个 token，在 \(E_j\) 中取最大内积并求和；
  - 若相似度超过阈值 \(\tau\)，则建立语义边。文中默认 \(\tau=0.7\)。
- **作用**：物理边支持局部顺序阅读，语义边支持跨页“逻辑跳跃”。

### 2.3 查询分解与对齐
- 使用 **Query Decomposition Engine（QDE）**，由 LLM 将复杂问题 \(Q\) 分解为原子语义查询 \(Q^*=\{q_1,\dots,q_K\}\)。
- 每个原子查询对应证据链的一个片段，缓解单一粗粒度查询向量与多跳证据之间的粒度不匹配。

### 2.4 自适应拓扑追踪器
- 维护全局：
  - **Whitelist \(W\)**：已接受证据页；
  - **Memory \(M\)**：推理轨迹与页面分析。
- 每个原子查询维护：
  - **候选栈 \(S_k\)**：初始为与 \(q_k\) 最相似的 top-m 页面；
  - **黑名单 \(B_k\)**：剪枝无关路径。
- 迭代流程：
  1. 从栈中弹出当前页 \(p_{curr}\)；
  2. 若已在 \(W\) 或 \(B_k\) 中，跳过；
  3. 用 VLM judge 判断其相对 \(q_k\) 的状态与推理分析；
  4. 若 **Relevant**，加入 \(W\) 和 \(M\)，并扩展物理邻居与语义邻居 TopK 入栈；
  5. 若 **Irrelevant**，加入 \(B_k\) 并回溯。
- 每轮接受页面数上限约为 \(\lfloor N_{total}/N_{sub} \rfloor\)，其中 \(N_{total}\) 为总页预算，\(N_{sub}\) 为原子查询数。

### 2.5 基于证据链的推理
- 所有查询处理完后，全局记忆 \(M\) 形成“Trace Trajectory”。
- 将该轨迹与 \(W\) 中页面的视觉内容输入推理 VLM（如 Qwen-VL-Max），生成最终答案。
- 通过显式条件化于证据链，减少幻觉并提升答案可溯源性。

### 2.6 可扩展图构建策略
- **章内微范围**：全 Token-wise MaxSim，保留细粒度语义。
- **书级/全局大范围**：粗到细两阶段：
  1. 页面均值池化后稠密检索，定位候选章节；
  2. 在候选章节内再做 Token-wise MaxSim 精确定位。
- 目的是将复杂度从 \(O(N^2T^2)\) 降到近似 \(O(N^2)\)。

## 3. 实验设计

### 3.1 数据集与基准
- **主基准：M5BookVQA**
  - 首个面向书籍的跨页、多跳 DocVQA 基准。
  - 包含 **2,054 个问题**，来自 **16,790 页非虚构书籍**。
  - 五个特点：多模态、多文档、多跳、多语言、多领域。
  - 覆盖 **6 种语言**：英语 50.2%、中文 36.4%、俄语 5.3%、日语 4.7%、法语 2.2%、德语 1.2%。
  - 覆盖 **19 个子领域**，四大类：人文艺术、自然科学、工程、社会科学。
  - 提供 **Hop Counts** 与 **Rationales** 标注；多数问题需 3–4 跳，最多 13 跳；证据页数最多 10 页。
- **泛化基准**：
  - MMLongBench-Doc
  - LongDocURL
  - PaperTab
  - FetaTab

### 3.2 对比方法
- **直接 VLM 推理**：InternVL-3.5-8B、Qwen3-VL-8B。
- **文本 RAG**：M3DocRAG（Text）、多种 LLM 文本 RAG。
- **视觉 RAG**：M3DocRAG（Image）、MDocAgent、MoLoRAG。
- **图式 RAG 对比**：Naive RAG、GraphRAG、MMGraphRAG、RAG-Anything。
- **多智能体方法**：MDocAgent。

### 3.3 评估指标与场景
- QA 指标：Accuracy。
- 检索指标：Recall@10、Precision@10、NDCG。
- 检索范围：Chapter、Book、Global 三种 scope。
- 泛化实验采用 Top-3 检索设置。
- PaperTab/FetaTab 使用 GPT-4o 作为语义正确性评估器。

## 4. 资源与算力

- **论文未明确说明**使用的 GPU 型号、数量、训练时长或总计算量。
- TRACE 主要是一个推理/检索导航框架，依赖现成 VLM/LLM 与 ColPali 等模型，未报告重新训练成本。
- 仅提供**相对成本分析**：
  - 以 MoLoRAG 为 1.0× 基准；
  - TRACE 平均延迟约 **4.0×**；
  - VLM API 调用约 **10.0×**。
- 因此，若需复现实验，算力资源信息不足。

## 5. 实验数量与充分性

- **实验组数概览**：
  - M5BookVQA 主实验：Chapter / Book / Global 三种 scope。
  - 四个 established benchmarks 的 QA 对比。
  - 两个数据集上的检索质量对比。
  - 导航轨迹分析：Ephy/Esem 依赖与切换频率。
  - 消融实验：组件消融 4 组 + backbone 替换 4 组。
  - 成本分析：延迟与 API 调用。
  - GraphRAG 方法对比。
  - 语言、领域、证据页数三类 breakdown。
  - 两个定性案例研究。
- **充分性**：
  - 实验覆盖面较广，涵盖主基准、泛化基准、检索指标、消融、轨迹、成本与细分分析。
  - 对核心组件均有消融，验证了 QDE、物理邻接、语义相关、证据链的必要性。
  - 提供了多语言、多领域、不同复杂度下的性能变化。
- **客观性与公平性**：
  - 论文声称 TRACE 与基线使用相同 backbone。
  - 泛化实验统一采用 Top-3 检索设置。
  - 但存在潜在偏差：
    - M5BookVQA 为作者自建，标注也由作者完成，可能对 TRACE 更有利。
    - 直接 VLM 推理只在 Chapter scope 评估，未在 Book/Global 比较。
    - TRACE 计算成本显著更高，未在所有比较中控制相同计算预算。
    - 部分评估依赖 GPT-4o 或规则，可能引入评估器偏差。
  - 总体而言，实验较充分，但公平性仍受自建基准与计算预算差异影响。

## 6. 主要结论与发现

- **被动匹配不足**：传统 RAG 的语义鸿沟与结构断裂会限制长文档多跳推理。
- **M5BookVQA 性能**：TRACE 平均准确率提升 **14.07%**；在 Chapter、Book、Global 三个 scope 均优于 M3DocRAG、MDocAgent、MoLoRAG。
- **泛化能力**：在四个 established benchmarks 上平均提升 **13.38%**，TRACE 平均 61.48%，优于 MoLoRAG 的 48.10%。
- **鲁棒性**：从 Chapter 到 Global，MoLoRAG 准确率下降约 17%，TRACE 仅下降约 7%。
- **轨迹规律**：
  - 随 scope 扩大，对语义层依赖从 53.59% 升至 63.51%。
  - 即使在 Global 设置下，仍保持约 36% 的物理邻接依赖。
  - Chapter scope 切换频率最高（60.96%）。
- **消融结论**：
  - 去掉 QDE：准确率下降 6.53%，Recall@10 下降 13.35%。
  - 去掉物理邻接：NDCG 从 76.01% 降至 48.07%，影响最大。
  - 去掉语义相关：准确率下降 10.91%，NDCG 下降 23.82%。
  - 去掉证据链：准确率下降 7.74%。
- **瓶颈判断**：长文档 VQA 的主要瓶颈在**证据获取**而非证据处理；检索失败会导致“Garbage In, Garbage Out”。
- **GraphRAG 对比**：TRACE 在 MMLongBench-Doc 上达 49.06%，

优于 GraphRAG、MMGraphRAG、RAG-Anything 等图式方法，表明通用知识图谱式检索并不天然适配长文档视觉问答，TRACE 的“证据链”结构更贴合文档多跳推理需求。
- **成本—性能权衡**：TRACE 以约 4× 延迟、10× API 调用换取约 13%–14% 的准确率提升，属于“高成本、高收益”的方案，适合对准确性要求高于实时性的场景。

## 7. 局限性与未来工作（论文自述与推断）

- **成本较高**：迭代式图导航与 VLM judge 调用导致延迟和 API 成本显著高于单轮 RAG，难以直接用于大规模在线服务。
- **依赖现成组件**：性能上限受 ColPali 检索质量与 VLM judge/推理模型能力制约，组件升级或替换可能带来较大波动。
- **超参数敏感**：语义边阈值 \(\tau\)、每轮接受页面预算、候选栈大小 \(m\) 等需针对不同文档规模调优。
- **基准自建偏差**：M5BookVQA 由作者构建与标注，虽覆盖多语言、多领域，但对 TRACE 的评测优势需第三方基准进一步验证。
- **可扩展性**：书级/全局范围采用粗到细两阶段近似，仍可能在大规模语料上遇到检索效率与内存瓶颈。
- **潜在方向**：更高效的图导航策略、自适应预算分配、与训练式检索器结合、扩展到更多模态（表格、公式、音频）与更细粒度的跨文档证据融合。

## 8. 总体评价与启示

- **问题定位准确**：论文清晰指出长文档 DocVQA 中“语义鸿沟”与“结构断裂”两类失败模式，并据此设计双层图与证据链机制，动机与方案高度对应。
- **方法设计有特色**：将检索从“一次性 Top-k”转为“自适应图遍历 + 证据链构建”，物理邻接与语义相关双通道互补，QDE 缓解查询粒度不匹配，整体思路接近人类浏览与推理过程。
- **基准贡献显著**：M5BookVQA 填补了书籍级、多跳、多语言、多模态 DocVQA 基准的空白，Hop Counts 与 Rationales 标注对后续研究有较高价值。
- **实验较扎实**：主基准、四个泛化基准、检索指标、消融、轨迹、成本、细分分析齐备，结论相互印证，尤其“瓶颈在证据获取而非处理”的判断具有方法论意义。
- **仍需改进之处**：计算成本、超参数敏感性、自建基准公平性、与训练式方法的结合等，是后续工作可重点突破的方向。
- **实践启示**：在长文档问答系统设计中，应重视页面间逻辑结构与证据链的可追溯性，而非仅依赖向量相似度；同时需在准确率与推理成本之间做显式权衡。

（完）

---
title: "LAD-RAG: Layout-aware Dynamic RAG for Visually-Rich Document Understanding"
title_zh: LAD-RAG：面向视觉丰富文档理解的布局感知动态RAG
authors: "Zhivar Sourati, Zheng Wang, Marianne Menglin Liu, Yazhe Hu, Mengqing Guo, Sujeeth Bharadwaj, Kyu J. Han, Tao Sheng, Sujith Ravi, Morteza Dehghani, Dan Roth"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.724.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 布局感知的动态RAG框架
tldr: 传统RAG在视觉丰富文档理解中按孤立分块编码内容，丢失结构与跨页依赖，且推理时固定检索页数，导致多页推理证据不全、答案质量下降。本文提出LAD-RAG布局感知动态RAG框架，在摄取阶段构建符号化文档图以捕获布局结构，并在推理阶段根据问题动态调整检索范围。实验表明该方法能更完整地检索证据，提升多页文档问答效果，为结构化文档的检索增强生成提供了新思路。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 4745, \"height\": 6240}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 8010, \"height\": 3270}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 16200, \"height\": 5400}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-004.webp\", \"caption\": \"\", \"page\": 8, \"index\": 4, \"width\": 7200, \"height\": 4500}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-005.webp\", \"caption\": \"\", \"page\": 15, \"index\": 5, \"width\": 5770, \"height\": 3980}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-006.webp\", \"caption\": \"\", \"page\": 16, \"index\": 6, \"width\": 5270, \"height\": 1855}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-007.webp\", \"caption\": \"\", \"page\": 16, \"index\": 7, \"width\": 10800, \"height\": 5400}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long724/fig-008.webp\", \"caption\": \"\", \"page\": 17, \"index\": 8, \"width\": 7200, \"height\": 4500}]"
motivation: 常规RAG按孤立分块编码并固定检索页数，丢失文档结构与跨页依赖，导致多页推理证据不全。
method: 提出LAD-RAG框架，摄取阶段构建符号化文档图捕获布局结构，推理阶段按问题动态调整检索范围。
result: 实验显示该方法能更完整检索证据，提升多页文档问答质量与答案可靠性。
conclusion: 为结构化文档的检索增强生成提供了布局感知与动态检索的新方案。
---

## Abstract
Question answering over visually rich documents (VRDs) requires reasoning not only over isolated content but also over documents’ structural organization and cross-page dependencies. However, conventional retrieval-augmented generation (RAG) methods encode content in isolated chunks during ingestion, losing structural and cross-page dependencies, and retrieve a fixed number of pages at inference, regardless of the specific demands of the question or context. This often results in incomplete evidence retrieval and degraded answer quality for multi-page reasoning tasks. To address these limitations, we propose LAD-RAG, a novel Layout-Aware Dynamic RAG framework. During ingestion, LAD-RAG constructs a symbolic document graph that captures layout structure and cross-page dependencies, adding it alongside standard neural embeddings to yield a more holistic representation of the document. During inference, an LLM agent dynamically interacts with the neural and symbolic indices to adaptively retrieve the necessary evidence based on the query. Experiments on MMLongBench-Doc, LongDocURL, DUDE, and MP-DocVQA demonstrate that LAD-RAG improves retrieval, achieving over 90% perfect recall on average without any top- k tuning, and outperforming baseline retrievers by up to 20% in recall at comparable noise levels, yielding higher QA accuracy with minimal latency.

---

## 论文详细总结（自动生成）

# LAD-RAG 论文中文总结

## 一、核心问题与整体含义（研究动机与背景）

- **任务背景**：视觉丰富文档（Visually Rich Documents, VRD）上的问答不仅需要理解孤立内容，还需推理文档的结构组织（阅读顺序、视觉分组、层级关系）与跨页依赖。现代多模态大模型（GPT-4o、InternVL、Qwen2.5VL 等）虽能处理此类输入，但当文档超出上下文窗口时效果受限；即便整体可放入上下文，性能也随长度增长而退化，相关信号被噪声稀释。
- **传统 RAG 的三大局限**：
  1. **丢失布局与结构上下文**：摄取时把文档视为孤立单元线性拼接，忽略布局层级与跨页连续性，导致证据检索不完整（如只返回标题页而漏掉后续列举示例的页面）。
  2. **过度依赖嵌入**：对依赖符号或结构线索的查询（如图表、页码、表格来源）表现差，难以聚合非连续但结构相关的图表与图注。
  3. **静态 top-k 检索**：检索深度与问题/文档复杂度无关，常导致检索过多或过少证据（不同问题所需页数可能从 3 页到 12 页不等）。
- **整体含义**：现有 RAG 缺乏整体性的文档表示，导致结构上分散的证据难以被完整检索。作者希望让 RAG 更接近人类阅读文档的方式——形成连贯的"心智图景"，并根据问题难度灵活回看不同部分、拉取不同量的证据。

## 二、方法论

### 核心思想
LAD-RAG 是一个**布局感知的动态 RAG 框架**，在摄取阶段同时构建**神经索引**与**符号化文档图**，在推理阶段由 LLM 智能体动态交互两种索引，按查询需求自适应检索完整证据集。

### 摄取阶段（Ingestion）
- **逐页解析**：使用 GPT-4o 逐页处理文档，提取所有可见元素（段落、图、表、节标题、脚注等），为每个元素生成**自包含描述**。
- **运行记忆（M）**：模拟人类阅读，跨页累积高层信息（章节结构、实体提及、主题进展、未解引用），用于消歧跨页关系。
- **文档图节点**：每个节点对应页面上的局部元素，包含布局位置、元素类型、显示内容、自包含摘要、视觉属性等字段，保证元素可独立检索与解释。
- **文档图边**：编码**引用关系**（段落引用图表、脚注引用章节）与**布局/结构关系**（同章节元素、跨页延续），借助运行记忆消歧仅凭当前页无法判断的关系。
- **双索引存储**：
  - **符号（图）索引 G**：含结构化节点/边属性，支持图检索与社区划分。
  - **神经索引 E**：对所有节点自包含摘要做向量索引，支持语义相似度搜索。
- 双表示既保留神经模型的语义丰富性，又保留显式布局结构，弥补纯嵌入会"抽象掉"细节的缺陷。

### 推理阶段（Inference）
- 采用 **LLM 智能体（GPT-4o）** 迭代与两种索引交互，先制定高层计划（语义/符号/混合检索模式），再发出工具调用，通过对话循环逐步精炼证据集。
- **终止条件**（任一满足）：接近上下文窗口、达到最大步数、智能体判断证据已足够。
- **三种工具接口**：
  1. `NeuroSemanticSearch(query)`：基于嵌入相似度从神经索引检索证据。
  2. `SymbolicGraphQuery(query_statement)`：对符号图做结构化查询（按元素类型、章节、页码过滤等）。
  3. `Contextualize(node)`：依据图的局部邻域与高阶关系（Louvain 社区检测）将节点扩展为连贯的证据簇。
- 相比固定 top-k，该机制支持完全上下文化、自适应的证据选择。

## 三、实验设计

### 数据集 / Benchmark（4 个 VRD 基准）
| 数据集 | 特点 |
|---|---|
| **MMLongBench-Doc** | 135 篇长 PDF（均 47.5 页，~21k token），1082 问，33% 需跨页证据 |
| **LongDocURL** | 396 篇文档（~33k 页），2325 QA 对，均 86 页，多页问题占比 52.9%，跨元素 37.1% |
| **DUDE** | ~5k 多页文档，覆盖医疗/法律/技术/金融，均 5.7 页 |
| **MP-DocVQA** | 46k 问，5928 篇文档，均 ~8 页，证据通常限于单页 |

### 对比方法
- **检索基线**：
  - 文本类：E5-large-v2、BGE-large-en、BM25
  - 图像类：ColPali（M3DocRAG 的检索骨干）
  - 层次化：RAPTOR（语义聚合的层级 RAG）
  - 基线按标准 RAG 设置，在 k 值升到完美召回点之间评估。
- **QA 对比**：
  - 使用 4 个 LVLM：Phi-3.5-Vision-4B、Pixtral-12B-2409、InternVL2-8B、GPT-4o
  - 检索设置：LAD-RAG 证据 / 最佳基线固定 k=5、k=10 / top-k 对齐（与 LAD-RAG 检索相同页数）/ 真值证据（oracle 上界）
  - 另对比全文档输入模型：mPLUG-DocOwl v1.5-8B、Idefics2-8B、MiniCPM-Llama3-V2.5-8B
- **评估指标**：
  - 检索：**Perfect Recall（PR）**（是否覆盖全部真值页）与 **Irrelevant Pages Ratio（IPR）**（噪声比例）
  - QA：用 GPT-4o 抽取答案 + 规则匹配判对错，并做人工评估验证（100 例，2 位标注者，Cohen's κ 达 0.86–0.92）

## 四、资源与算力

- **硬件**：4 块 NVIDIA A100 GPU。
- **软件环境**：Python 3.10.12、PyTorch 2.7.0+cu126、vLLM 0.9.2（推理服务）、networkx（图构建）。
- **超参**：所有 LVLM 提示步骤 temperature=0；图构建阶段最大 token 8192，QA 阶段 2048；检索智能体最大交互轮数 20；PDF 以 300 DPI 渲染。
- **说明**：论文**未明确报告训练时长**。LAD-RAG 属于检索/推理框架，图构建在离线摄取阶段一次性完成，主要计算发生在离线摄取，而非模型训练；论文亦未给出各阶段的墙钟耗时，仅报告了推理时的 LLM 调用次数与 token 量。

## 五、实验数量与充分性

- **实验规模**：
  - 4 个数据集上的检索对比（含多个 k 值扫描）。
  - 4 个 LVLM 上的端到端 QA 对比（含 single/multi 页细分）。
  - 消融实验：完整 LAD-RAG vs. w/o Contextualize (C)、w/o GraphQuery (G)、w/o C & G，并与 RAPTOR、ColPali、BM25、E5、BGE 对比。
  - 细分分析：按证据来源（layout/text/table/figure/chart）、问题类型（理解/推理/定位）、文档类型（指南、工作坊、手册、学术论文、财务报告等）拆解。
  - 延迟分析（LLM 调用次数分布、token 分布）。
  - 人工评估（100 样本，双标注者）。
- **充分性与公平性**：
  - 实验覆盖多数据集、多模型、多问题类型，消融设计清晰，能定位各组件贡献。
  - 与基线做 **top-k 对齐（topk-adjusted）** 控制检索预算，避免"靠多检索页数取胜"的不公平比较，设计较严谨。
  - QA 用自动化评判 + 人工验证，报告了 κ 一致性，评估流程可信。
  - **潜在不足**：LAD-RAG 使用 GPT-4o 做摄取与智能体，而部分基线可能使用不同骨干，存在骨干能力不对等的隐忧（论文用 topk-adjusted 部分缓解，但摄取端 LVLM 的差异未完全隔离）。

## 六、主要结论与发现

- **检索效果显著提升**：LAD-RAG 在 4 个基准上平均达到 **>90% perfect recall**，且无需任何 top-k 调参；在可比噪声水平下比基线召回率高最多 **20%**（MMLongBench ~20%、LongDocURL ~15%、DUDE/MP-DocVQA ~10%）。
- **基线需大 k 才能追平**：平均需 k=22（MMLongBench）、k=27（LongDocURL）、k=10（DUDE）、k=5（MP-DocVQA）才能匹配 LAD-RAG 召回，揭示常用低 k 实践与多页问题真实证据量之间的错配。
- **消融结论**：去掉上下文扩展（C）平均降 4%，去掉图查询（G）降 10%；仅用神经索引的变体（w/o C & G）仍优于传统基线，说明符号图与图检索带来额外增益。RAPTOR 表现接近 w/o G，说明语义层级无法替代布局结构。
- **QA 提升**：LAD-RAG 在所有模型与数据集上优于固定 top-k 与 topk-adjusted，多页问题平均提升 4 个百分点（最高 18），相对 topk-adjusted 平均 3 个百分点（最高 11）；端到端性能逼近 oracle（差距 5–8 分以内），个别情况甚至超过真值证据（因额外上下文有助于推理）。
- **延迟开销小**：图构建离线完成，推理时通常仅 2–5 次 LLM 调用，>97% 调用生成 <100 token，开销远低于需逐页扫描的方案（MoLoRAG、FRAG）。
- **重要观察**：即使给出近乎完美的证据，当前 LVLM 仍可能无法充分利用，说明下游推理能力是正交的瓶颈。

## 七、优点

- **神经 + 符号双索引设计**：同时保留语义丰富性与显式布局结构，弥补纯嵌入"抽象掉细节"的缺陷。
- **动态、查询自适应检索**：用 LLM 智能体替代固定 top-k，能按问题复杂度灵活决定检索范围与模式（语义/符号/混合）。
- **图结构设计细致**：节点含自包含摘要、布局与视觉属性；边编码引用、布局连续与跨页依赖；借助运行记忆消歧。
- **社区检测辅助上下文扩展**：用 Louvain 把节点扩展为连贯证据簇，兼顾局部邻域与高阶关系。
- **计算效率高**：重计算放在离线摄取，推理轻量（少量短 LLM 调用），对比逐页扫描方案优势明显。
- **实验严谨**：引入 topk-adjusted 控制预算、人工评估验证自动评判、按多维拆解分析。
- **动机叙事清晰**：以人类阅读的"心智图景"类比，直观解释方法合理性。

## 八、不足与局限

- **不改进推理能力**：论文明确限定贡献在检索，不涉及生成推理或答案合成；即使近乎完美证据，LVLM 仍可能失败。
- **依赖强 LVLM 摄取**：框架依赖 GPT-4o 做元素抽取与结构化，对噪声输入、复杂布局、低质量视觉内容（扫描件）存在抽取错误风险；DUDE 与 MP-DocVQA 含扫描文档，鲁棒性仍待进一步验证。
- **成本与工程权衡**：虽然作者称可用更小模型或传统 OCR 替代部分抽取，但跨页语义-布局链接仍依赖 LVLM；统一模型 vs. 模块化工具之间存在复杂度与鲁棒性的权衡。
- **代码未公开**：实现仍在机构审查与法律审查中，暂未释放，影响可复现性（虽提供了完整提示模板与超参）。
- **实验覆盖的潜在偏差**：部分数据集（如 MP-DocVQA）证据本限于单页，对多页聚合能力的评估有限；DUDE 中多页问题占比仅约 1%。不同数据集的跨页挑战程度不均。
- **对等性隐忧**：摄取端与智能体端均用 GPT-4o，而部分基线可能基于不同骨干，绝对性能对比的公平性需谨慎解读。
- **未报告训练/摄取耗时**：仅报告推理延迟与调用次数，缺少图构建阶段的成本量化，难以全面评估部署开销。

（完）

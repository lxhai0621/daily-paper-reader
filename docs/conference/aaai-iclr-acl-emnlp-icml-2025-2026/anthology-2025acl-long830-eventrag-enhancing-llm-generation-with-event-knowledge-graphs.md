---
title: "EventRAG: Enhancing LLM Generation with Event Knowledge Graphs"
title_zh: EventRAG：利用事件知识图谱增强大语言模型生成
authors: "Zairun Yang, Yilin Wang, Zhengyan Shi, Yuan Yao, Lei Liang, Keyan Ding, Emine Yilmaz, Huajun Chen, Qiang Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.830.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 提出EventRAG框架，利用事件知识图谱增强RAG
tldr: 现有RAG系统在叙事丰富文档和多源信息合成中存在不足。EventRAG通过构建事件知识图谱，合并语义等价事件节点并扩展弱连接，采用迭代检索与推理策略捕捉事件间时间与逻辑依赖。在UltraDomain和MultiHopRAG基准上显著优于基线系统，证明了事件结构化表示对提升生成质量的有效性。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.830/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1615, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.830/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1611, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.830/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1574, \"height\": 1406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.830/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 681, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.830/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 763, \"height\": 1103, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.830/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1329, \"height\": 920, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.830/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1501, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.830/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 816, \"height\": 366, \"label\": \"Table\"}]"
motivation: 针对RAG系统在处理叙事丰富文档和事件推理时的不足，提出利用结构化事件表征提升生成效果。
method: 构建事件知识图谱，合并等价事件节点并扩展连接；采用迭代检索与推理策略捕捉事件间依赖。
result: 在UltraDomain和MultiHopRAG基准上显著优于基线RAG系统。
conclusion: 事件知识图谱和迭代推理策略能有效提升RAG系统在事件密集型场景下的表现。
---

## Abstract
Retrieval-augmented generation (RAG) systems often struggle with narrative-rich documents and event-centric reasoning, particularly when synthesizing information across multiple sources. We present EventRAG, a novel framework that enhances text generation through structured event representations. We first construct an Event Knowledge Graph by extracting events and merging semantically equivalent nodes across documents, while expanding under-connected relationships. We then employ an iterative retrieval and inference strategy that explicitly captures temporal dependencies and logical relationships across events. Experiments on UltraDomain and MultiHopRAG benchmarks show EventRAG’s superiority over baseline RAG systems, with substantial gains in generation effectiveness, logical consistency, and multi-hop reasoning accuracy. Our work advances RAG systems by integrating structured event semantics with iterative inference, particularly benefiting scenarios requiring temporal and logical reasoning across documents.

---

## 论文详细总结（自动生成）

# 论文总结：EventRAG：利用事件知识图谱增强大语言模型生成

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现有检索增强生成（RAG）系统通常以文档、段落或句子为单位处理文本，忽略了底层的事件结构，导致在叙事丰富文档（如新闻报道、历史文献）中难以准确理解事件的时间演变、逻辑依赖和跨文档的事件交互。传统RAG在单次检索或浅层拼接中缺乏多事件推理能力，容易产生不一致的叙述和幻觉。
- **整体含义**：为了解决上述问题，本文提出 **EventRAG**——一个以事件为中心的RAG框架，通过构建结构化事件知识图谱（Event Knowledge Graph, EKG）并采用迭代推理策略，显式捕获事件间的时间关系和逻辑关联，从而提升生成内容的事实一致性、逻辑连贯性和多跳推理准确性。

## 2. 方法论

### 2.1 核心思想
- 将文本拆解为互连的事件，以事件节点（包含参与者、时间等属性）和关系边（如因果、时序）构建EKG；然后利用智能体（Agent）在EKG上进行自主、迭代的检索与推理，支持多步链路回溯和自我修正。

### 2.2 关键技术细节
- **阶段一：事件知识图谱构建**
  1. **事件提取**：使用LLM从文档中抽取事件、实体及其关系，并将它们通过嵌入模型转换为向量存入向量数据库。
  2. **实体融合**（Fuse Entities）：通过余弦相似度（阈值θ）合并语义等价或跨文档重复的实体/事件，建立“相似”关系，减少冗余并保持语义一致性。公式：若 similarity(V_i, V_j) > θ，则 V_i ∪ V_j → V_f。
  3. **知识扩展**（Expand Knowledge）：识别图中欠连接节点，利用文档线索或LLM固有知识补充缺失的关系和上下文，增强图的连通性。
- **阶段二：基于事件的检索与生成**
  1. **自主EKG查询**：Agent将输入问题q分解为与事件元素相关的子查询，从EKG中检索最相似事件 e_j（公式：e_j = argmax similarity(q, e_k)）。
  2. **时间感知推理**（Temporal-Aware Inference）：利用事件节点中的时间属性（如日期）和事件间先后关系（T(e_j) ⪯ T(e_k)）进行推理，捕获事件演化过程。
  3. **多事件推理**（Multi-Event Reasoning）：Agent迭代式地检索逻辑或时序相连的事件，构建中间推理路径并验证一致性，动态调整推理焦点。
  4. **反思与自校正**（Reflection & Self-Correction）：Agent定期评估自身推理结果的连贯性和准确性，发现不一致时重新访问相关事件节点，修正理解。

## 3. 实验设计

### 3.1 数据集与场景
- **生成有效性评估**：使用 UltraDomain 基准中的四个领域数据集——agriculture（12篇，224万字）、cooking（14篇，237万字）、history（26篇，557万字）以及 bioprotocol（100篇，6.1万字）。每个数据集由LLM生成125个高层次理解问题（共500个问题）。
- **推理能力评估**：使用 MultiHopRAG 基准（138篇，约42万字），包含四种问题类型：推理查询（33%）、比较查询（35%）、空查询（9%）、时间查询（23%），选取前100个问题。

### 3.2 对比方法
- NaiveRAG（基础检索+拼接）
- GraphRAG（Edge et al., 2024）
- LightRAG（Guo et al., 2024）
- 以及 EventRAG（本文）

### 3.3 评估指标
- **生成有效性**：六维度LLM评估（全面性、多样性、赋能、逻辑、直接性、总体胜率），以成对胜率（win rate）报告。
- **推理能力**：使用RAGAS定义的答案相关性、答案正确性、语义相似度。

## 4. 资源与算力
- **未明确说明**：论文中未提及使用的GPU型号、数量、训练时长等具体算力资源。实验均基于API调用（gpt-4o-2024-08-06、text-embedding-3-small）和向量数据库（milvus），推理阶段也依赖LLM，因此无法直接估计本地训练/推理的算力开销。

## 5. 实验数量与充分性
- **实验数量**：
  - 生成有效性：4个数据集 × 3个基线 → 12组主要对比（每个维度均报告胜率，共6维度）。
  - 推理能力：1个基准（MultiHopRAG）上4种查询类型 × 3个指标 → 12组数据。
  - 消融实验：2个消融变体（w/o知识扩展、w/o多事件推理）在4个数据集上对比NaiveRAG → 8组对比（每个维度均有）。
- **充分性与公平性**：
  - 实验覆盖了不同领域、文档长度和推理难度，具有较好代表性。
  - 所有方法使用相同LLM（gpt-4o）、相同嵌入模型、相同分块大小（1200 token）和 gleaning 参数（1），控制变量到位。
  - 生成有效性指标采用LLM评估（可能引入主观偏差），但基于篇幅约束和主流实践可接受。
  - 推理能力指标自动计算，客观性较好。
  - 消融实验验证了关键组件的作用，但缺少对实体融合单独消融（文中只强调其在总体中的贡献）。

## 6. 主要结论与发现
- EventRAG 在几乎所有评估维度上显著优于 NaiveRAG、GraphRAG、LightRAG。
  - 生成有效性：在逻辑性、全面性上提升最为突出（例如history数据集逻辑胜率84.8% vs 基线15.2%）。
  - 推理能力：答案正确率平均提升14%以上（相对于最强基线LightRAG），尤其在时间查询上正确率达87.86%（LightRAG 61.70%），比较查询正确率达81.64%（LightRAG 55.92%）。
- 消融实验表明：
  - **知识扩展**对全面性和多样性贡献大；
  - **多事件推理**对逻辑性和总体胜率至关重要。
- 案例研究显示 EventRAG 能生成结构清晰、细节丰富、时序连贯的叙述，优于GraphRAG。

## 7. 优点
- **创新性**：首个将事件知识图谱与迭代推理机制系统性地集成到RAG中的框架，弥补了传统RAG在事件层面的缺失。
- **实体融合与知识扩展**：有效减少多文档信息冗余，增强图连通性，提升检索精度。
- **时间感知推理**：显式建模事件的时间顺序和演化，适合新闻、历史、协议流程等时序敏感场景。
- **多事件自校正**：Agent的反思维度降低幻觉，提高推理的一致性。
- **实验全面**：覆盖生成质量和推理能力双重评价，消融分析验证组件必要性。

## 8. 不足与局限
- **计算效率低**：知识图谱构建阶段需要多次LLM调用（事件提取、关系识别、实体融合、知识扩展），导致处理大型文档集合时开销大，不适合实时性要求高的应用。
- **评估偏差风险**：生成有效性采用LLM（同一gpt-4o）作为评判者，可能存在自我偏好或评估偏差。
- **应用限制**：仅测试英文数据集，对其他语言和跨领域泛化能力未知；在动态变化的事件（如实时新闻）中，静态构建的EKG可能过时。
- **伦理风险**：用户可能过度依赖系统的时间推理进行未来预测或决策，论文建议将其作为辅助工具而非决策系统。
- **未与其他事件抽取专用模型对比**：论文使用通用LLM抽取事件，未与专用事件抽取器（如OneKE、CollabKG）的性能进行比较，可能低估事件抽取质量的影响。

（完）

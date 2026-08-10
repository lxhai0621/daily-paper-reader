---
title: "FRAG: Filtering Noise Using Snippet-Level Query Relevance"
title_zh: FRAG：基于片段级查询相关性过滤噪音
authors: "Yeming Jian, Yonggang Zhang, Shanzhi Gu, Long Lan, Tongliang Liu, Yiu-ming Cheung, Bo Han"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wIflv5cQiU"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过片段级噪声过滤提升RAG准确性
tldr: RAG通常通过扩大检索窗口提升召回，但也会引入更多噪声，分散模型注意力并降低准确率。本文提出细粒度RAG（FRAG），从查询中识别关键片段，并利用片段级查询相关性过滤检索噪声。针对多跳复杂查询，FRAG还结合对隐式推理关系的识别，避免过滤掉蕴含推理链的关键知识。实验显示FRAG在扩展检索窗口的同时能有效抑制噪声，提升RAG的准确性与可解释性，为改进RAG系统提供了实用技术。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 扩大RAG检索窗口虽可增加相关内容，但噪声增多会损害模型注意力与准确性。
method: FRAG基于片段级查询相关性识别关键查询片段并过滤检索噪声，同时保留多跳推理关系。
result: FRAG在增大检索窗口的同时抑制噪声，提高了RAG的准确率。
conclusion: 片段级查询相关性过滤是提升RAG精度和鲁棒性的有效途径。
---

## Abstract
Retrieval-Augmented Generation (RAG) augments large language models (LLMs) with external retrievals. Typically, expanding the retrieval window can improve RAG performance by retrieving more relevant content. However, it risks increased noise, which distracts the model’s attention and degrades accuracy. To mitigate this, we propose Fine-Grained RAG (FRAG), which identifies key snippets from query and extracts relevant information while filtering noise from retrievals using snippet-level query relevance. Yet, a new challenge arises in addressing complex RAG queries, which require knowledge pieces with implicit multi-hop logical relationships. Failure to identify these relationships may lead to loss of inference-based knowledge during filtering, degrading performance. To address this, we propose Self-Recognition, which extracts inference-based knowledge by leveraging historically extracted knowledge as contextual references. While FRAG notably improves performance, it incurs high computational cost. To alleviate this, we present FRAG-ip, a fine-tuned framework which markedly accelerates FRAG by an order of magnitude. Extensive experiments show that FRAG significantly boosts RAG, yielding average accuracy gains of 4.94%/13.44% on simple/complex tasks.

---

## 论文详细总结（自动生成）

# FRAG：基于片段级查询相关性过滤噪音——论文总结

## 1. 核心问题与整体含义

- **研究动机**：检索增强生成（RAG）通过引入外部检索内容增强大语言模型（LLM）的生成能力。通常，扩大检索窗口（如增加检索文档数量）会提高召回率，进而提升性能；但检索范围过大会引入更多**噪声**，这些无关内容会**分散模型注意力**、降低生成准确率。
- **核心问题**：如何在享受更大检索窗口收益的同时，有效过滤噪声？特别地，复杂多跳查询需要知识片段之间具有**隐式的逻辑推理关系**，若简单过滤则可能丢失关键推理链，导致性能下降。
- **整体含义**：论文提出细粒度 RAG 框架（FRAG），通过**片段级查询相关性**过滤检索噪声，并对复杂查询进行“自识别”以保留推理性知识，从而提升 RAG 的准确性、可解释性与实用性。

## 2. 方法论

- **核心思想**：从查询中识别关键片段（snippet），计算每个检索片段与查询关键片段的**相关性**，据此过滤无关噪声，而非在整篇文档层面进行粗糙筛选。
- **关键技术细节**：
  - **片段级相关性评估**：将查询分解为关键片段，在检索结果中逐片段计算与这些关键片段的语义相关性，保留高相关片段、丢弃低相关片段。
  - **复杂查询的隐式关系处理**：针对多跳逻辑关系，提出 **Self-Recognition** 机制——利用历史上已提取的知识片段作为上下文参考，帮助识别当前片段是否属于推理链的一部分，避免因过滤而丢失蕴含推理关系的知识。
  - **加速方案**：由于 FRAG 计算成本较高，论文提出 **FRAG-ip**——一个经过微调的框架，可将 FRAG 的计算速度提高**一个数量级**（order of magnitude）。
- **公式/算法流程**：摘要未给出具体数学公式，但其算法本质可描述为：  
  输入检索文档 → 查询片段识别 → 片段相关性打分 → 阈值过滤 → 结合 Self-Recognition 保留推理链 → 生成答案；FRAG-ip 则通过微调学生模型压缩推理步骤。

## 3. 实验设计

- **数据集与场景**：摘要仅提及任务类型分为**简单任务（simple tasks）** 和**复杂任务（complex tasks）**，未明确给出数据集名称（如 NaturalQuestions、HotpotQA 等均未在摘要中出现）。
- **Benchmark**：未说明具体基准测试集，无法确认采用了哪些标准评测语料。
- **对比方法**：未列出具体基线模型，推测与标准 RAG 或扩大检索窗口的朴素 RAG 对比。
- **实验结果概况**：FRAG 在简单/复杂任务上的平均准确率增益分别为 **4.94%** 和 **13.44%**，显示对复杂任务改进更明显。

## 4. 资源与算力

- 摘要中**未提及任何算力信息**，包括 GPU 型号、数量、训练时长、推理开销等。
- 仅提及 FRAG 本身计算成本较高，且 FRAG-ip 可实现约 10 倍加速，但具体硬件配置与运行时间一概未给出。

## 5. 实验数量与充分性

- **实验数量**：从摘要看，至少包含简单/复杂两类任务上的效果对比，以及 FRAG-ip 的加速效果验证（但未给数字）。未提及消融实验、参数敏感性、不同噪声水平、不同检索窗口规模等。
- **充分性评估**：
  - **不足**：缺乏数据集规模、基线数量、统计显著性等信息；没有展示过滤错误率、失败案例或可解释性分析。
  - **公平性存疑**：由于未公开基准和基线，无法判断比较是否全面、是否采用相同检索器/生成器设置。
  - **客观性受限**：摘要信息过少，实验结论主要依赖数值增益，但没有配套详尽实验支撑，审稿人可能因此质疑实验完整性。

## 6. 主要结论

- 扩大检索窗口与过滤噪声并非不可兼得：FRAG 在增大检索窗口的同时，通过片段级相关性过滤有效抑制噪声，进而提升 RAG 准确率。
- 对简单任务提升 4.94%，对复杂任务提升 13.44%，后者表明 Self-Recognition 在保留多跳推理链方面具有显著价值。
- FRAG-ip 大幅降低计算成本，使方法具备实际应用潜力。

## 7. 优点

- **问题切入务实**：直面“检索窗口越大噪声越多”的常见矛盾，而非一味追求召回。
- **细粒度过滤**：在片段级而非文档级做相关性判别，更加精准，便于定位和删除噪声片段。
- **关注推理链**：Self-Recognition 机制考虑了复杂查询中知识片段之间的隐式逻辑关系，避免机械过滤造成信息断层。
- **效率优化**：提供 FRAG-ip 加速方案，说明作者不仅关注效果，也重视部署可行性。

## 8. 不足与局限

- **实验信息不透明**：未给出具体数据集、基准、基线方法，无法验证比较的公平性与普适性。
- **资源开销未披露**：未说明训练或推理所需的算力，复现门槛未知，加速效果也缺乏量化数据。
- **实验规模不足**：缺少消融研究、超参数影响分析、鲁棒性测试等，使方法论的可解释性不充分。
- **适用范围存疑**：片段切分方式、相关性阈值选择均可能影响效果，但对这些变量未做讨论。
- **论文状态提示**：该文在 ICLR-2026 中被拒，说明审稿人可能对实验充分性或方法新颖性存在质疑。

（完）

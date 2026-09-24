---
title: "Concept rather than Document: Context Compression via AMR-based Conceptual Entropy"
title_zh: 概念而非文档：基于AMR概念熵的上下文压缩
authors: "Kaize Shi, Xueyao Sun, Xiaohui Tao, Lin Li, Qika Lin, Guandong Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.590.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 面向RAG的长上下文语义压缩
tldr: 大模型在处理长上下文尤其是检索增强生成时，大量支撑文档带来冗余信息，干扰推理。本文提出一种无监督上下文压缩框架，利用抽象语义表示（AMR）图，通过节点级熵量化概念重要性，从而保留语义关键内容并过滤无关文本。该方法在语义单元层面而非词元层面压缩上下文，有助于缓解长上下文的信息过载问题。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl590/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 2649, \"height\": 1755}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl590/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 4143, \"height\": 1540}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl590/fig-003.webp\", \"caption\": \"\", \"page\": 8, \"index\": 3, \"width\": 1000, \"height\": 600}]"
motivation: 长上下文与RAG中冗余文档造成信息过载，干扰推理且现有方法割裂语义单元。
method: 提出无监督上下文压缩框架，用AMR图节点熵衡量概念重要性。
result: 在保留语义核心信息的同时过滤无关文本，降低上下文冗余。
conclusion: 为长上下文RAG提供了语义级压缩方法。
---

## Abstract
Large Language Models (LLMs) face information overload when handling long contexts, particularly in Retrieval-Augmented Generation (RAG) where extensive supporting documents introduce redundant content that interferes with reasoning. Context engineering has emerged to address these challenges, yet existing methods rely on lexical or token-level features that fragment semantic units and fail to capture conceptually essential content. We propose an unsupervised context compression framework leveraging Abstract Meaning Representation (AMR) to preserve semantically essential information while filtering irrelevant text. By quantifying node-level entropy within AMR graphs, our method estimates the conceptual importance of each node, enabling retention of core semantics. Specifically, we construct AMR graphs from retrieved contexts, compute the conceptual entropy of each node, and identify statistically significant concepts to form a condensed, semantically focused context. Experiments on the PopQA and EntityQuestions datasets demonstrate that our method outperforms vanilla RAG and existing baselines, achieving superior accuracy while substantially reducing context length. To the best of our knowledge, this is the first work introducing AMR-based conceptual entropy for context compression, demonstrating the potential of structured linguistic representations in context engineering.

---

## 论文详细总结（自动生成）

## 论文总结：Concept rather than Document: Context Compression via AMR-based Conceptual Entropy

### 1. 核心问题与整体含义
- **研究动机**：LLM 处理长上下文时存在信息过载，RAG 中检索大量文档虽提高召回，却引入冗余和噪声，干扰推理并增加延迟。
- **现有不足**：已有上下文压缩方法多依赖词法、TF-IDF、token 级困惑度或生成式摘要，容易割裂语义单元，无法稳定保留“概念上必要”的内容。
- **核心主张**：应压缩到“概念”而非“文档/词元”。论文首次提出利用 AMR（Abstract Meaning Representation）图的节点级概念熵进行无监督上下文压缩，在保留语义核心的同时过滤无关文本。

### 2. 方法论
- **核心思想**：将检索文档解析为 AMR 图，以概念节点为单位估计信息量；高熵节点代表更具区分度和信息量的概念，保留显著高熵概念并还原为原文表达，形成压缩上下文。
- **问题形式化**：给定查询 \(Q\)、检索文档集 \(D\)、答案集 \(A\)，学习压缩函数 \(f(D)\to C'\)，使 \(Acc(Q,C')\ge Acc(Q,D)\) 且 \(|C'|\ll |D|\)。实验受控地只保留包含正确答案的文档。
- **AMR 图构建**：
  - 使用基于 mBART、在 AMR 3.0 上训练的解析器，将文档解析为句级 AMR 图 \(G_i=(V_i,E_i)\)。
  - 保留概念节点 \(V_i\)，丢弃显式关系边 \(E_i\)，假设人类和 LLM 可根据离散概念重建语义场景，避免人工关系符号干扰预训练语言理解。
- **概念熵计算**：
  - 用 AMR 生成模型对概念 token 序列的预测不确定性衡量信息量。
  - 对子词 token 计算困惑度式熵：\(E(s_j)=\exp(-\log P_\theta(s_j|s_{<j},G_i))\)。
  - 通过特殊前缀识别概念边界，聚合为概念级熵：\(H(v)=\frac1m\sum_{j=1}^m E(s_j)\)。
- **概念蒸馏**：
  - 对每篇文档内概念熵做单样本 t 检验：\(t_{stat}(v_j)=\frac{H(v_j)-\bar H}{s/\sqrt n}\)。
  - 计算双尾 p 值，保留 \(p(v_j)<\alpha\) 的显著高熵概念；论文设 \(\alpha=0.3\)，以平衡剪枝与保留上下文信号。
- **压缩与重建**：
  - 聚合所有文档中的显著概念形成 \(C'\)。
  - 后处理包括时间表达式重建、连续重复概念删除、表面实现还原到原文表达，降低 AMR 抽象带来的失真。

### 3. 实验设计
- **数据集/场景**：PopQA 与 EntityQuestions，均为知识密集型开放域问答，适合长上下文 RAG 推理。
- **检索设置**：PopQA 使用 Contriever，EntityQuestions 使用 BM25；只保留 `hasanswer=True` 的文档，并按 \(K=1\) 到 10 个含答案文档构造上下文。
- **Backbone LLM**：GPT-Neo-1.3B/2.7B、OPT-1.3B/2.7B、BLOOM-560m/7b1、Llama-2-chat-13B、Llama-3.1-Instruct-8B、DeepSeek-V2-Lite-16B、Qwen3-32B。
- **对比方法**：
  - Vanilla：原始检索文档。
  - 统计方法：TF-IDF。
  - LLM 驱动方法：关键词提取、摘要生成，均使用 LLaMA-3.1-8B-Instruct。
  - 专用压缩方法：Selective Context（SelCon）、LLMLingua。
  - 本文方法：AMR 概念熵压缩。
- **评价指标**：Accuracy（exact match）、AUC；AUC 分为标准区间 \(I_s=[1,10]\) 和长上下文区间 \(I_l=[6,10]\)；跨 backbone 的 AUC 标准差 \(\sigma\) 衡量稳定性。
- **补充实验**：压缩率对比、推理时间（ms/instance）、\(\alpha\) 消融（0.01、0.05、0.1、0.5 与 0.3 对比）。

### 4. 资源与算力
- 论文**未明确报告**使用的 GPU 型号、数量、训练时长或总计算量。
- 方法本身主要涉及 AMR 解析、熵计算和 LLM 推理；论文只报告了推理时间表，未说明硬件环境。
- 作者在 Limitations 中指出，AMR 图构建与熵计算会带来额外预处理成本，但属于离线阶段，未给出具体资源开销。

### 5. 实验数量与充分性
- **实验规模较大**：2 个数据集 × 10 个 backbone LLM × \(K=1\) 到 10 × 多种压缩方法，并报告 AUC、Accuracy、压缩率、推理时间和 \(\alpha\) 消融。
- **覆盖较广**：涵盖小模型到 32B 模型、统计/生成/专用压缩三类基线、标准与长上下文两个区间。
- **客观性较好之处**：统一提示模板，将压缩上下文标为 “facts”；受控设置只保留含答案文档，以隔离压缩效果。
- **仍有限制**：
  - 未报告多次随机种子或统计显著性检验，主要依赖跨模型 \(\sigma\)。
  - 受控设置不反映真实 RAG 中无关或冲突文档的干扰。
  - 两个检索器不同，可能影响跨数据集可比性。
  - 基线提示敏感，生成式摘要/关键词可能受 prompt 和幻觉影响。

### 6. 主要结论与发现
- 在 PopQA 和 EntityQuestions 上，AMR 概念熵压缩在多数配置中优于 Vanilla 和已有压缩基线，尤其在大模型上提升明显，如 Qwen3-32B、Llama-2-chat-13B、Llama-3.1-8

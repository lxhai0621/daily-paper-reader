---
title: "InfoFlow KV: Information-Flow-Aware KV Recomputation for Long Context"
title_zh: InfoFlow KV：面向长上下文的信息流感知KV重计算
authors: "Xin Teng, Canyu Zhang, Shaoyi Zheng, Danyang Zhuo, Tianyi Zhou, Shenji Wan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/e05eb28fd1d96c5ac66e5ccaa55708f11a699523.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向长上下文RAG的KV缓存重计算
tldr: 长上下文问答中的检索增强生成受制于在大量检索上下文上的推理期预填充开销，现有选择性KV重计算方法依赖启发式或表示差异，未建模所选词元能否真正影响生成。本文将其建模为信息流问题，发现查询的注意力范数信号可稳定识别既语义相关又结构上利于传播信息的词元。实验表明该方法在维持生成质量的同时降低长上下文RAG的计算开销，为长检索窗口的高效推理提供支撑。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 长上下文RAG的推理期预填充开销巨大，现有选择性KV重计算依赖启发式而缺乏理论建模。
method: 将选择性KV重计算建模为信息流问题，用查询的注意力范数信号筛选语义相关且结构利于传播的词元。
result: 该方法在保证生成质量的同时降低长上下文RAG的推理开销。
conclusion: 为长检索窗口下高效且一致的KV缓存复用提供了信息流视角的新方法。
---

## Abstract
Retrieval-augmented generation (RAG) for long-context question answering is bottlenecked by inference-time prefilling over large retrieved contexts. A common strategy is to precompute key–value (KV) caches for individual documents and selectively recompute a small subset of tokens to restore global causal dependencies, but existing methods rely on heuristics or representation discrepancies without modeling whether selected tokens can effectively influence generation. We cast selective KV recomputation as an information flow problem and show that a simple attention-norm signal from the query reliably identifies tokens that are both semantically relevant and structurally positioned to propagate information, when computed under an inference-consistent RoPE geometry. We therefore reconstruct global positional assignments for retrieved chunks and introduce an information-flow–guided chunk reordering strategy. Experiments on Large Language Model and Vision-Language Model benchmarks demonstrate consistent gains over prior methods under comparable latency.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向长上下文RAG的KV缓存重计算。

### 2. 核心内容
长上下文问答中的检索增强生成受制于在大量检索上下文上的推理期预填充开销，现有选择性KV重计算方法依赖启发式或表示差异，未建模所选词元能否真正影响生成。本文将其建模为信息流问题，发现查询的注意力范数信号可稳定识别既语义相关又结构上利于传播信息的词元。实验表明该方法在维持生成质量的同时降低长上下文RAG的计算开销，为长检索窗口的高效推理提供支撑。

### 3. 对应检索需求
Managing long context and retrieval window size。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=o8y6CoJsWA](https://openreview.net/forum?id=o8y6CoJsWA)

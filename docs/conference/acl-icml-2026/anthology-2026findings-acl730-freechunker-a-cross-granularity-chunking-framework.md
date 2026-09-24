---
title: "FreeChunker: A Cross-Granularity Chunking Framework"
title_zh: FreeChunker：跨粒度分块框架
authors: "Zhang Wenxuan, Yuan-Hao Jiang, Yang Cao, Yonghe Wu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.730.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 跨粒度分块提升RAG检索
tldr: 现有RAG分块方法大多基于固定粒度与静态边界，难以适应多样化的查询需求。本文提出FreeChunker跨粒度编码框架，将句子视为原子单元，从静态分块转向支持任意句子组合的灵活检索，从而避免语义边界检测的开销。在LongBench V2上的实验表明该框架能更好地适应复杂查询，为分块策略提供了新范式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl730/fig-001.webp\", \"caption\": \"\", \"page\": 5, \"index\": 1, \"width\": 10594, \"height\": 3526}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl730/fig-002.webp\", \"caption\": \"\", \"page\": 8, \"index\": 2, \"width\": 7200, \"height\": 2100}]"
motivation: 现有分块方法局限于固定粒度与静态边界，难以适应多样查询需求。
method: 提出跨粒度编码框架，以句子为原子单元，支持任意句子组合的灵活检索。
result: 在LongBench V2上验证了其适应复杂查询的能力。
conclusion: 以灵活检索范式替代静态分块，提升RAG适应性。
---

## Abstract
Chunking strategies significantly impact the effectiveness of Retrieval-Augmented Generation (RAG) systems. Existing methods operate within fixed-granularity paradigms that rely on static boundary identification, limiting their adaptability to diverse query requirements. This paper presents FreeChunker, a Cross-Granularity Encoding Framework that fundamentally transforms the traditional chunking paradigm: the framework treats sentences as atomic units and shifts from static chunk segmentation to flexible retrieval supporting arbitrary sentence combinations. This paradigm shift not only significantly avoids the computational overhead required for semantic boundary detection, but also enhances adaptability to complex queries. Experimental evaluation on LongBench V2 demonstrates that FreeChunker possesses significant advantages in both retrieval performance and time efficiency compared to existing chunking methods. The pre-trained models and codes are available at https://github.com/mazehart/FreeChunker.

---

## 论文详细总结（自动生成）

# FreeChunker 论文中文总结

## 1. 核心问题与整体含义
- **研究背景**：RAG 系统效果高度依赖文档分块策略；分块粒度影响块内连贯性、语义覆盖与下游生成质量。
- **核心问题**：现有方法大多基于固定粒度与静态边界识别，难以同时适配同一文档集合中不同查询对“细粒度细节”和“粗粒度上下文”的需求。
- **现有方法局限**：
  - 固定分块简单但易割裂语义或造成冗余；
  - SemanticChunker、Meta-Chunking、LumberChunker 等语义分块仍属单粒度范式，且边界检测计算开销大；
  - MoC、MoG 等自适应方法本质仍是聚合已有 chunker 专家，粒度控制受底层专家能力限制。
- **整体含义**：论文提出 FreeChunker，将句子视为原子单元，从“静态分块+重新编码”转向“句子编码+可配置连续多粒度组合检索”，以提升复杂查询适应性和效率。

## 2. 方法论
- **核心思想**：不物理切分并单独编码每个 chunk，而是在句子嵌入上通过可配置 mask 与跨粒度注意力，一次前向生成多个连续粒度 chunk 的嵌入。
- **流程**：
  - **Sentenizer**：将文档 \(D\) 拆为句子 \(S=\{s_1,\dots,s_n\}\)，用 token-level embedding 模型编码为句子嵌入矩阵 \(E=[\vec e_1,\dots,\vec e_n]\in\mathbb R^{n\times d}\)。
  - **Cross-Granularity Chunk Pattern**：构造 Chunk Pattern Mask \(P\in\{0,-\infty\}^{m\times n}\)。对粒度 \(g\) 和起始位置 \(s\)：
    \[
    P_{g,s}[i,j]=
    \begin{cases}
    0, & s\le j<s+g\\
    -\infty, & \text{otherwise}
    \end{cases}
    \]
    可叠加多种粒度，形成带状 mask。
  - **Cross-Granularity Encoder**：引入可学习 chunk embedding \(h_{chk}\)，复制为 \(H\)；以 \(H\) 为 Query，句子嵌入 \(E\) 为 Key/Value：
    \[
    Q=W_QH,\quad K=W_KE,\quad V=W_VE
    \]
    \[
    \mathrm{Attn}(H,E)=\mathrm{softmax}\left(\frac{QK^\top}{\sqrt d}+P\right)V
    \]
    再接 LayerNorm、FFN，单次前向并行生成所有 chunk 嵌入。
  - **去重与拼接**：为句子分配全局索引，存储为 `[Begin-t] St [End-t]`。检索后按索引合并重叠候选，同一索引保留最高分候选中的实例，排序拼接；不连续处插入“...”，保证重建确定、可复现。
- **训练**

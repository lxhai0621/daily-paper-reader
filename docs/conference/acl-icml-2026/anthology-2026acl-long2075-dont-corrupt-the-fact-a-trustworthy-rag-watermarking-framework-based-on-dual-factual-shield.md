---
title: "Don’t Corrupt the Fact: A Trustworthy RAG Watermarking Framework based on Dual Factual Shield"
title_zh: "勿篡改事实:基于双事实盾牌的可信RAG水印框架"
authors: "Hao Huang, JiaTang Luo, Ruihua Zhou, Yunpeng Li, Yuling Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.2075.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: "面向可信RAG的水印框架,缓解忠实性幻觉"
tldr: "检索增强生成旨在通过外部证据提升事实忠实性,但现有水印技术本质上与事实无关,迫使模型偏离其应遵循的源文档,导致输出与自身依据相矛盾的忠实性幻觉,削弱了RAG的核心价值。本文提出双事实盾牌DFS框架,针对RAG特有的水印与事实冲突问题,在保证水印安全性的同时维持事实忠实性,为高风险场景下可信RAG提供新方案。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2075/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 520, \"height\": 599}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2075/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 316, \"height\": 383}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2075/fig-003.webp\", \"caption\": \"\", \"page\": 8, \"index\": 3, \"width\": 3000, \"height\": 1200}]"
motivation: "现有RAG水印技术忽视事实,迫使模型偏离源文档,引发忠实性幻觉,削弱RAG可信度。"
method: "提出双事实盾牌DFS框架,针对RAG水印与事实保真的冲突设计新型架构。"
result: "该框架在保持水印安全性的同时维持输出对源文档的事实忠实,缓解忠实性幻觉。"
conclusion: 兼顾水印与事实的框架为高风险场景下的可信RAG提供可行方案。
---

## Abstract
While Retrieval-Augmented Generation (RAG) systems are designed to enhance factual fidelity by grounding LLMs in provided sources, the application of current watermarking techniques creates a paradoxical failure mode. These methods, being inherently fact-agnostic, force the model to deviate from the very source documents it is supposed to follow. This leads to “faithfulness hallucinations"—a critical flaw where the generated output contradicts its own grounding context. Consequently, these watermarks undermine the core value of RAG, rendering even the most secure schemes untrustworthy for high-stakes applications. To resolve this RAG-specific conflict, we introduce the Dual Factual Shield (DFS) framework, a novel architecture designed to enforce knowledge loyalty. The DFS framework employs a defense-in-depth strategy through two synergistic layers: a source-anchored algorithmic safeguard that shields critical terms from the retrieved context, and prompt-based semantic guidance that protects against factual corruption. To demonstrate its effectiveness, we enhance a state-of-the-art, spoofing-aware contrastive watermarking baseline with our framework. Experiments show that our framework drastically reduces the Knowledge Corruption Rate (KCR)—a new metric we introduce—while preserving its original high security and robustness. This work establishes a new paradigm for watermarking, evolving it from merely secure to truly trustworthy. We demonstrate that traceability and truth can, and must, coexist, paving the way for the responsible deployment of traceable AI in knowledge-critical domains.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：RAG 通过将 LLM 生成锚定在检索到的外部文档上，提升事实性与可信度；与此同时，水印技术被用于追踪机器生成内容的来源，防止滥用。
- **核心冲突**：现有 LLM 水印方法本质上是“事实无关”的，通常通过随机划分 green/red 词表并偏向 green token 来嵌入水印。这会把年份、数字、人名、地点等关键事实 token 随机分到 red list，迫使模型偏离其本应遵循的源文档。
- **关键问题**：论文将其称为 **“faithfulness hallucination”**，即水印导致生成文本与自身检索依据相矛盾。这不仅损害 RAG 的核心价值，也使即使安全性很高的水印方案在高风险场景中不可信。
- **整体含义**：论文主张水印不应只追求可检测性、鲁棒性和防伪安全，还必须具备“知识忠诚”。作者提出 **Dual Factual Shield（DFS）**，试图证明可追溯性与事实忠实性可以且必须共存。

## 2. 方法论

### 2.1 核心思想

- DFS 是一个 **三阶段 post-hoc 水印流水线**：先对未加水印的草稿答案进行改写，再构造受事实保护的 greenlist，最后进行受事实保护的采样。
- 总体采用 **防御纵深** 设计：
  - “软”约束：通过 prompt 语义引导，提示模型保留关键事实。
  - “硬”约束：通过算法手段把源文档中的关键事实 token 强制加入 greenlist，降低其被替换的概率。

### 2.2 三阶段流程

- **Stage I：Fact-Preserving Generation（软约束）**
  - 使用 spaCy 进行命名实体识别，并用规则匹配抽取数字型事实，如日期、百分比、金额等。
  - 将抽取的事实集合 \(E=\{e_1,e_2,\dots,e_n\}\) 序列化后加入改写 prompt，显式要求 LLM 不得改动这些关键事实。
  - 该阶段是“软”引导，目的是在不严重稀释水印信号的前提下，降低事实被意外篡改的概率。

- **Stage II：Semantic Mapping & Fact-Guarded Greenlist Construction**
  - 采用一个防 spoofing 的语义映射水印 backbone，通过对比学习编码器把词表划分为初始 greenlist \(G_{base}\) 和 red list \(R\)。
  - 但该语义映射本身仍是事实无关的，因此作者加入 **源文档锚定的事实约束**：
    - 对检索文档集合 \(D\) 做 NER，抽取人物、地点、组织等实体。
    - 统计实体 token 在检索证据中的出现情况；只要在源文档中出现至少一次的唯一实体 token，都纳入保护集合 \(S_{fact}\)。
    - 停用词和功能词因不属于命名实体而自然排除。
  - 构造最终受保护 greenlist：
    \[
    G_{final}=G_{base}\cup S_{fact}
    \]
  - 该操作相当于“Do-Not-Alter”策略：强制关键事实 token 进入 greenlist，提高其采样概率，减少被 red-list token 替换的风险。
  - 论文指出，由于 tokenizer 会把实体字符串拆成有限 token，该策略不会导致 greenlist 过度膨胀而严重稀释水印信号。

- **Stage III：Fact-Guarded Sampling**
  - 使用 \(G_{final}\) 对 LLM 输出 logits 进行偏置，提高从受保护 greenlist 中采样的概率，生成最终水印文本 \(X_w\)。
  - 检测仍遵循底层语义编码器的统计检测框架，即通过测量文本中 greenlist token 的比例来验证水印。

### 2.3 关键公式与指标

- 受保护 greenlist：
  \[
  G_{final}=G_{base}\cup S_{fact}
  \]
- 知识腐化率 KCR：
  \[
  KCR=\frac{TF-PF}{TF}
  \]
  - \(TF\)：标准答案中抽取的事实实体总数。
  - \(PF\)：标准答案与响应文本之间保持一致的事实实体数。
  - KCR 越低越好，0 表示事实完全保留。
- Faithfulness：
  \[
  Faithfulness=\frac{VS}{TS}
  \]
  - \(VS\)：被验证为有上下文支持的原子陈述数。
  - \(TS\)：抽取出的原子陈述总数。

## 3. 实验设计

- **数据集 / 场景**
  - **WikiEval**：标准 RAG 基准，由英文 Wikipedia 的 question-context-answer 三元组构成，主实验使用 50 个查询。
  - **Wiki-Big**：作者自建的大规模多领域 Wikipedia 基准，包含 300 个查询，覆盖历史、科学、流行文化、金融、医疗等领域，包含较多实体和数字型事实。
- **Backbone LLM**
  - 主要使用 **Llama-3.1-8B**。
  - 部分实验使用 **Qwen2.5-0.5B** 和 **Qwen2.5-7B** 做对比分析。
- **对比方法**
  - KGW、Unigram、SWEET、Unbiased、DiP、Contrastive WM。
  - 其中 Contrastive WM 是 SOTA 安全水印方法，也是 DFS 在 Stage II 采用的语义编码 backbone。
- **评价指标**
  - 水印性能：AUC，用于可检测性和防 spoofing 安全性。
  - 事实保真：KCR、Faithfulness。
  - 生成质量：ROUGE-1、ROUGE-L、PPL。
  - 安全场景：spoofing 攻击下的

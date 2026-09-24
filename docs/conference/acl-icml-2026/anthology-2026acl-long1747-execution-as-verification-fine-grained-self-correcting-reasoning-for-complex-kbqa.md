---
title: "Execution as Verification: Fine-Grained Self-Correcting Reasoning for Complex KBQA"
title_zh: 以执行为验证：面向复杂KBQA的细粒度自校正推理
authors: "Minghan Zhang, Zhen Yang, Haodong Zou, Jie Chen, Zhen Duan, Shu Zhao"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1747.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 结构化知识库问答与自校正语义解析
tldr: 针对基于LLM的先生成后执行语义解析受严格语法约束、易产生结构偏差与语义偏差而导致查询不可执行或结果错误的问题，本文提出Execution as Verification框架EVER。该方法将语义解析重构为由执行反馈驱动的迭代自校正推理过程。通过执行反馈迭代修正，显著缓解不可执行查询与错误执行结果问题，提升结构化知识库问答的准确率与可解释性，为知识推理的语义解析提供了自校正方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 3067, \"height\": 1253}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 3067, \"height\": 1253}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 534, \"height\": 433}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 2263, \"height\": 924}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-006.webp\", \"caption\": \"\", \"page\": 4, \"index\": 6, \"width\": 764, \"height\": 713}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-007.webp\", \"caption\": \"\", \"page\": 4, \"index\": 7, \"width\": 765, \"height\": 481}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-008.webp\", \"caption\": \"\", \"page\": 4, \"index\": 8, \"width\": 963, \"height\": 675}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1747/fig-009.webp\", \"caption\": \"\", \"page\": 4, \"index\": 9, \"width\": 2251, \"height\": 758}]"
motivation: 基于LLM的先生成后执行语义解析受严格语法约束，易产生结构偏差与语义偏差导致查询失败或错误。
method: 提出EVER框架，将语义解析重构为由执行反馈驱动的迭代自校正推理过程。
result: 通过执行反馈迭代修正，显著缓解不可执行查询与错误执行结果问题，提升KBQA准确率。
conclusion: 表明执行反馈可作为验证信号，为结构化知识问答的语义解析提供自校正方案。
---

## Abstract
Knowledge Base Question Answering (KBQA) leverages structured knowledge bases to offer superior interpretability and hallucination resistance, making it a critical technology for precise knowledge reasoning. However, the prevailing LLM-based generate-then-execute formulation of semantic parsing is limited by strict syntactic constraints, making it primarily prone to structural deviations that render queries unexecutable, while suffering from semantic deviations that yield incorrect execution results. To address these challenges, we propose the Execution as Verification (EVER) framework, reframing semantic parsing as an iterative, self-correcting reasoning process driven by execution feedback. First, motivated by the insight that query executability serves as a strong proxy for answer correctness, we introduce Fine-Grained Execution-Aware Planning. This mechanism decomposes complex semantic parsing into a sequence of stepwise reasoning processes oriented by executability verification, ensuring high query executability. We further design a Self-Guided Semantic Correction mechanism based on execution result verification, utilizing execution feedback to verify and calibrate semantic deviations, thereby ensuring the semantic correctness of executable queries. Experimental results on the WebQSP and CWQ datasets demonstrate that our method achieves significant improvements in both query executability and answer accuracy, achieving state-of-the-art performance, particularly in complex multi-hop scenarios. Our code is available at https://github.com/ahu-zmh/EVER.

---

## 论文详细总结（自动生成）

# 论文总结：Execution as Verification: Fine-Grained Self-Correcting Reasoning for Complex KBQA

## 1. 核心问题与研究动机
- KBQA 利用结构化知识库提升可解释性与抗幻觉能力，是精确知识推理的重要技术。
- 当前基于 LLM 的语义解析（SP）多采用“先生成后执行”范式，但逻辑形式语法约束严格，存在两类核心问题：
  - **结构偏差**：微小语法/结构错误导致查询完全不可执行，长逻辑链下尤为严重。
  - **语义偏差**：查询可执行但语义错配，返回错误结果。
- 论文的关键洞察：**查询可执行性是答案正确性的强代理信号**。对 ChatKBQA 等的经验分析显示，成功执行与答案准确率相关性约 90%，原因在于知识库结构稀疏，错误逻辑通常无法匹配有效图路径。
- 因此，仅最大化可执行性不够，还需保证语义一致性。论文提出将语义解析重构为**由执行反馈驱动的迭代自校正推理过程**。

## 2. 方法论：EVER 框架
### 核心思想
- 将执行反馈同时用作两类验证信号：
  - 执行成功/失败 → 验证结构有效性；
  - 执行结果 → 验证语义一致性。
- 把复杂 KBQA 语义解析拆解为逐步推理，并在每一步动态校正。

### 关键技术细节
- **Fine-Grained Execution-Aware Planning（细粒度执行感知规划）**
  - 将生成过程分解为 \(T\) 个离散步骤。历史状态 \(H_{t-1}=\{(l_0,r_0),...,(l_{t-1},r_{t-1})\}\)。
  - \(l_t\)：当前累积逻辑形式；\(r_t=\text{Execute}(l_t|K)\)：在知识库 \(K\) 上的执行结果。
  - 采用混合解码：
    - **Phase 1 意图锚定**：用贪心搜索生成自然语言推理意图 \(I_t=\text{LLM}_{greedy}(Q,H_{t-1})\)，防止语义漂移。
    - **Phase 2 骨架生成**：基于意图 \(I_t\) 用束搜索生成 \(K\) 个候选逻辑骨架 \(S_t=\text{LLM}_{beam}(Q,H_{t-1},I_t)\)，提供结构容错与后续回退空间。
- **Self-Guided Semantic Correction（自引导语义校正）**
  - **Phase 3 对齐**：将骨架中的实体/关系表面名映射到 KB UID。
    - 实体：先精确匹配，

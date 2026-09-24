---
title: "Q2EI: Query-to-Entity Inference for Semantic Condensation in Domain-Specific Retrieval"
title_zh: Q2EI：面向领域检索语义凝练的查询到实体推断
authors: "Yixuan Sun, Zhenqin Xu, HanFeng Zhai, Zishu Yu, Xiaohui Peng"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1791.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 将查询改写为语义凝练，对齐通俗查询与专业术语
tldr: 在专业领域，RAG 因通俗查询与专业术语之间的语义和词汇错配而不够可靠，生成式查询扩展又常引入冗余或幻觉，导致语义漂移。为此提出生成式查询凝练 GQC，把改写重新定义为语义凝练而非扩展，并以查询到实体推断 Q2EI 通过显式推断目标实体实现。该方法把语义对齐前移到改写阶段，生成信息密度更高的查询，提升了领域检索的准确性与稳定性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-003.webp\", \"caption\": \"\", \"page\": 2, \"index\": 3, \"width\": 895, \"height\": 603}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-004.webp\", \"caption\": \"\", \"page\": 2, \"index\": 4, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-005.webp\", \"caption\": \"\", \"page\": 2, \"index\": 5, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-006.webp\", \"caption\": \"\", \"page\": 2, \"index\": 6, \"width\": 765, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-007.webp\", \"caption\": \"\", \"page\": 2, \"index\": 7, \"width\": 450, \"height\": 445}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-008.webp\", \"caption\": \"\", \"page\": 2, \"index\": 8, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-009.webp\", \"caption\": \"\", \"page\": 2, \"index\": 9, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-010.webp\", \"caption\": \"\", \"page\": 5, \"index\": 10, \"width\": 615, \"height\": 764}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-011.webp\", \"caption\": \"\", \"page\": 5, \"index\": 11, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-012.webp\", \"caption\": \"\", \"page\": 5, \"index\": 12, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1791/fig-013.webp\", \"caption\": \"\", \"page\": 5, \"index\": 13, \"width\": 744, \"height\": 1042}]"
motivation: 专业领域 RAG 受通俗查询与专业术语错配影响，生成式扩展易带来冗余与语义漂移。
method: 提出生成式查询凝练，并以查询到实体推断 Q2EI 通过显式推断目标实体实现语义凝练。
result: 将语义对齐前移至改写阶段，生成信息密度更高的查询，改善领域检索。
conclusion: 为提升领域 RAG 的检索准确性提供了实体中心的改写策略。
---

## Abstract
Retrieval-Augmented Generation (RAG) remains unreliable in specialized domains due to semantic and lexical mismatch between lay queries and professional terminology, and existing generative expansion often introduces redundancy or hallucinations that cause semantic drift. We propose Generative Query Condensation (GQC), a query rewriting strategy that reframes rewriting as semantic condensation rather than expansion. To operationalize GQC, we introduce Query-to-Entity Inference (Q2EI), an entity-centric rewriting method that realizes semantic condensation through explicit inference of the underlying target entity. By moving semantic alignment from retrieval-time vector matching to the rewriting stage, Q2EI produces information-dense query representations. Experimental results on medical and legal benchmarks show that Q2EI consistently outperforms strong baselines across retrievers, improving retrieval effectiveness while substantially reducing rewriting token consumption compared to generative expansion methods. Further analysis confirms that these gains primarily arise from accurate entity inference, and that Q2EI’s semantic condensation design limits error amplification when inference is imperfect, leading to more stable and interpretable retrieval behavior.

---

## 论文详细总结（自动生成）

# Q2EI 论文中文总结

## 1. 核心问题与整体含义
- **研究背景**：RAG 在通用开放域任务中有效，但在医学、法律等专业领域中仍不可靠。核心困难是用户查询通常处于“非专业/现象级”语义空间，而专业文档使用规范化、领域术语化的表达，二者存在显著词汇错配与语义鸿沟。
- **现有方法问题**：传统稀疏检索依赖词面重叠，稠密检索依赖向量相似度，均难以可靠推断通俗描述背后的专业概念。生成式查询扩展（GQE，如 HyDE、Query2Doc）虽能补充语义，但在专业领域容易引入冗余、幻觉和语义漂移；知识图谱方法虽可显式对齐，但构图成本高、覆盖受限。
- **论文核心含义**：论文提出一种“减法式”改写思路——**生成式查询凝练（GQC）**，把查询改写从“扩展”转为“语义压缩”，并以**查询到实体推断（Q2EI）**具体实现。其目标是把语义对齐从检索时的向量匹配前移到改写阶段，生成信息密度更高的实体中心查询。

## 2. 方法论
- **核心思想**：不生成冗长伪文档，而是利用 LLM 的参数化知识，从现象级查询中显式推断核心领域实体，并重写为实体中心查询，以缩小通俗查询与专业文档之间的语义和词汇差距。
- **问题形式化**：
  - 查询空间 \(Q_{lay}\) 包含现象级通俗查询 \(q_{lay}\)，文档空间 \(D_{expert}\) 包含专业术语文档 \(d\)。
  - 目标是学习映射 \(f: Q_{lay} \rightarrow Q\)，使重写后的查询与目标文档的编码相似度最大化：
    \[
    \max_f \text{Sim}(\text{Enc}(f(q_{lay})), \text{Enc}(d_{target}))
    \]
- **GQE 与 GQC 对比**：
  - GQE 通过补充上下文近似目标文档分布：\(f_{GQE}(q_{lay}) = T(q_{lay}, c_{gen})\)，其中 \(c_{gen}\) 由 LLM 生成。
  - GQC 直接对查询进行语义凝练：\(f_{GQC}(q_{lay}) = q_{GQC}\)，输出高信息密度、低冗余的重写查询。
- **Q2EI 三步流程**：
  1. **指令构建与约束**：使用 persona prompting 让 LLM 扮演领域专家；要求“实体优先推断”，先推断规范化核心实体 \(e_{core}\)，再生成实体中心查询 \(q_{ent}\)；支持 zero-shot 与 few-shot 示例。
  2. **模型推理与实体中心重写**：给定通俗查询和指令，LLM 推断核心实体并归一化为专业问题形式。
  3. **实体中心检索**：用 \(q_{ent}\) 替代原始查询检索，将匹配从“现象描述→专业文档”转为“实体中心查询→专业文档”。
- **关键特点**：无需微调、不依赖人工构建知识库，把 LLM 参数化知识当作“软知识库”；通过语义凝练提高信噪比，降低语义漂移风险。

## 3. 实验设计
- **数据集/场景**：
  - 医学领域：MedQuAD

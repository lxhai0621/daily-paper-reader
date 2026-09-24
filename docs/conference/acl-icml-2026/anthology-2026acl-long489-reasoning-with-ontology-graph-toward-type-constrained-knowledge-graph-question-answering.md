---
title: "Reasoning with Ontology Graph: Toward Type-Constrained Knowledge Graph Question Answering"
title_zh: "基于本体图推理:面向类型约束的知识图问答"
authors: "Yongxue Shan, Jie Peng, Zixuan Dong, Fei Hu, Xiaodong Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.489.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 基于本体知识图的类型约束推理问答
tldr: "大模型推动知识图问答发展,但现有方法多依赖粒度不一致的LLM诱导类型系统,或在缺乏显式目标类型约束下进行多跳推理。本文提出OntGQA类型约束框架,在以关系为中心的本体图上推理,每条关系标注头尾实体类型以提供稳定模式骨架,并采用规划者-判断者架构与生成式回退。该方法融合结构化知识约束与检索推理,提升问答准确性。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long489/fig-001.webp\", \"caption\": \"\", \"page\": 7, \"index\": 1, \"width\": 2934, \"height\": 1956}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long489/fig-002.webp\", \"caption\": \"\", \"page\": 7, \"index\": 2, \"width\": 2934, \"height\": 1956}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long489/fig-003.webp\", \"caption\": \"\", \"page\": 12, \"index\": 3, \"width\": 999, \"height\": 608}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long489/fig-004.webp\", \"caption\": \"\", \"page\": 12, \"index\": 4, \"width\": 999, \"height\": 608}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long489/fig-005.webp\", \"caption\": \"\", \"page\": 14, \"index\": 5, \"width\": 1650, \"height\": 990}]"
motivation: "现有知识图问答依赖粒度不一致的LLM诱导类型系统,或在缺乏目标类型约束下多跳推理。"
method: "提出OntGQA,在以关系为中心的本体图上推理,采用规划者-判断者架构与生成式回退约束类型。"
result: "该方法通过稳定的类型模式骨架约束多跳推理,提升知识图问答的准确性与一致性。"
conclusion: 融合结构化本体约束与生成式推理可有效改进知识图问答系统。
---

## Abstract
Large language models (LLMs) have recently advanced knowledge graph question answering (KGQA), but current methods tend to rely on LLM-induced type systems with inconsistent granularity, or perform multi-hop reasoning without explicit target-type constraints. We introduce OntGQA, a type-constrained KGQA framework that reasons over a relation-centric ontology graph, where each relation is labeled with its head and tail entity types to provide a stable schema backbone. Built on this graph, OntGQA adopts a planner–judge architecture with generative backoff: a type planner proposes plausible head–tail type pairs, a judge verifies retrieved candidates and their paths, and a generator is invoked only when all candidates are rejected. By constraining both endpoints of reasoning in type space, OntGQA achieves state-of-the-art performance and produces ontology-grounded reasoning chains, with substantial Hit@1 gains (87.7%→91.5% on WebQSP and 67.6%→74.6% on CWQ).

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：知识图问答（KGQA）旨在基于结构化知识图回答自然语言问题，已在医疗、农业、多媒体等领域得到应用。随着大语言模型（LLM）发展，KG+LLM 成为重要方向，尤其是多跳路径推理。
- **核心问题**：现有方法主要存在两类缺陷：
  - **本体不稳定**：依赖 LLM 诱导类型系统，类型粒度不一致，例如 Lionel Messi 可被标为 Person、Footballer、Athlete，导致本体难以对齐。
  - **路径爆炸**：基于子图扩展的方法从问题实体出发扩展大邻域，容易引入大量目标类型错误的候选路径，造成路径爆炸和噪声。
- **整体含义**：论文提出 **OntGQA**，一个类型约束的 KGQA 框架。其核心是构建以关系为中心的本体图，每条关系标注头实体类型和尾实体类型，形成稳定模式骨架；再通过规划者—判断者架构与生成式回退，在类型空间中约束多跳推理两端，从而缩小搜索空间、提升准确率与可解释性。

## 2. 方法论

- **核心思想**：
  - 用 **关系中心本体图** 作为稳定 schema backbone，避免 LLM 诱导本体的粒度不一致。
  - 在推理中同时约束 **头类型** 和 **尾类型**，即预测 plausible head–tail type pairs。
  - 采用 **planner–judge architecture with generative backoff**：规划者提出类型计划，检索候选与路径，判断者验证，全部拒绝时才调用生成器回退。

- **本体图构建**：
  - 数据源为 Freebase RDF dump，处理 canonical namespace 下的三元组。
  - 使用 `type.property.schema` 作为头类型，`type.property.expected_type` 作为尾类型。
  - 过滤非语义/行政类型，如 `common.topic`；保留具有完整头尾签名的关系。
  - 对少量缺失或欠指定关系做 **dataset-aware completion**，仅使用训练集推断头尾类型，避免测试泄漏。
  - 最终本体图含约 **32,195 个关系、12,369 个实体类型**；单机构建约 **1.93 小时**，提取 **71,210 条 property–schema 条目**。

- **Step I：Ontology-Guided Planner**：
  - 规划器为问题 \(q\) 输出头尾类型对 \(\tau=(\tau_h,\tau_t)\)，作为多跳检索的端点约束。
  - 约束诱导后验：从问题实体到金答案的最短事实路径对齐到本体图，得到有效类型对集合 \(\mathcal{T}\)，并定义均匀目标分布 \(Q(\tau)\)。
  - LLM 先验：用指令提示 LLM 自回归生成类型对列表，形式如 `<PAIR> τ_h <SEP> τ_t </PAIR>`，记为 \(P_\phi(\tau|q)\)。

- **Step II：Plan-Conditioned Path Retrieval**：
  - 给定预测类型计划 \(\hat{\mathcal{T}}\) 和问题实体集 \(E_q\)，先在本体图中枚举与端点类型相容的关系路径，再在 KG 中实例化。
  - **1-hop**：枚举头类型 \(\tau_h\) 允许的出边关系 \(R^+(\tau_h)\)，实例化得到 1 跳推理路径。
  - **2-hop with boundary gates**：第一跳限制在 \(R^+(\tau_h)\)，第二跳限制在尾类型 \(\tau_t\) 允许的入边关系 \(R^-(\tau_t)\)。
  - **Backoff 到更长路径**：若 1–2 跳为空，则回退到 \(K=3\) 或 \(K=4\)，仍施加边界门控。
  - 检索后去重并将路径文本化为证据串，聚合得到候选—证据集合 \(C(\tau,O,G)\)。

- **Step III：Judge with Generative Backoff**：
  - 判断者接收问题、候选答案、少量最短文本化证据路径，输出 `YES` 或 `NO`。
  - 定义标签 log 概率质量 \(\ell_c(q,a',w_{a'})\)，以及带符号 margin：
    \[
    m(q,a',w_{a'})=\ell_{yes}-\ell_{no}
    \]
  - 若 \(m>0\) 且 \(|m|\ge \lambda_{margin}\)，则接受该候选；文中默认 \(\lambda_{margin}=1.0\)。
  - **生成式回退**：若所有候选被拒绝或没有候选，则调用生成器 \(Gen(q)\) 生成最终答案。
  - 最终答案：
    \[
    A(q)=Judge(q) \text{ if } Judge(q)\neq\emptyset,\text{ else } Gen(q)
    \]

- **优化框架**：
  - 规划器：最小化后验 \(Q(\tau)\) 与先验 \(P_\phi(\tau|q)\) 的 KL 散度，等价于对有效类型对做负对数似然。
  - 判断者：使用 listwise InfoNCE，对比正例 `YES` 与负例 `NO`。
  - 生成器：最大似然训练 \(L_{gen}=-\log P_\omega(a|q)\)。
  - 总损失：\(L_{total}=L_{plan}+L_{judge}+L_{gen}\)。

## 3. 实验设计

- **数据集与场景**：
  - 基于 **Freebase** 知识图，约 88M 实体、20K 关系、126M 事实三元组。
  - **WebQSP**：4,737 个问题，训练 2,826、测试 1,628，主要为 1–2 跳较简单推理。
  - **CWQ**：34,689 个问题，训练 27,639、测试 3,531，更复杂，最多 4 跳；约 20.75% 问题涉及 3 跳及以上。
- **评估指标**：
  - 主指标：**Hit@1** 与 **F1**。
  - 消融中额外报告 Precision、Recall。
  - 使用 95% 置信区间，单种子 bootstrap，10,000 次重采样。
- **对比方法**：
  - 图推理方法：GraftNet、NSM、SR+NSM、UniKGQA。
  - 纯 LLM 方法：Llama-2-7B、Llama-3.1-8B、ChatGPT、GPT-4o、DeepSeek-v3。
  - KG+LLM 方法：ToG(GPT-4)、RoG(Llama-2-7B)、SymAgent(Llama-2-7B)、GNN

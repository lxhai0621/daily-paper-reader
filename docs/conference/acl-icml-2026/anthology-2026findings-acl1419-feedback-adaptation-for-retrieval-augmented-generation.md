---
title: Feedback Adaptation for Retrieval-Augmented Generation
title_zh: 面向检索增强生成的反馈自适应
authors: "Jihwan Bang, Seunghan Yang, Kyuhong Shim, Simyung Chang, Juntae Lee, Sungha Choi"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1419.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 通过反馈自适应提升 RAG 可靠性
tldr: 检索增强生成系统在部署中常被用户或专家反馈纠正，但现有评估多基于静态假设，只关注总体准确率，无法刻画系统在反馈后的适应行为。作者将反馈自适应定义为一个新的问题设定，并提出校正时延与反馈后性能两个评估维度，用以衡量反馈传播到后续查询的速度与可靠性。实验揭示不同训练式方法的适应差异，为构建可纠错、持续改进的 RAG 系统提供了评估框架。
source: ACL-2026-Findings
selection_source: conference_retrieval
motivation: RAG 系统部署中常被反馈纠正，但现有静态评估无法衡量反馈如何影响后续查询的可靠性与适应速度。
method: 提出反馈自适应问题设定，并设计校正时延与反馈后性能两个评估维度来量化反馈传播效果。
result: 基于新指标发现训练式方法在反馈后适应速度与语义相关查询可靠性上存在明显差异。
conclusion: 该工作为可纠错、持续改进的 RAG 系统提供了可测量的评估框架与改进方向。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems are typically evaluated under static assumptions, despite being frequently corrected through user or expert feedback in deployment. Existing evaluation protocols focus on overall accuracy and fail to capture how systems adapt after feedback is introduced. We introduce feedback adaptation as a problem setting for RAG systems, which asks how effectively and how quickly corrective feedback propagates to future queries. To make this behavior measurable, we propose two evaluation axes: correction lag, which captures the delay between feedback provision and behavioral change, and post-feedback performance, which measures reliability on semantically related queries after feedback. Using these metrics, we show that training-based approaches exhibit a trade-off between delayed correction and reliable adaptation. We further propose PatchRAG, a minimal inference-time instantiation that incorporates feedback without retraining, demonstrating immediate correction and strong post-feedback generalization under the proposed evaluation. Our results highlight feedback adaptation as a previously overlooked dimension of RAG system behavior in interactive settings.

---

## 论文详细总结（自动生成）

# 论文总结：面向检索增强生成的反馈自适应

## 1. 核心问题与整体含义

- **研究动机**：检索增强生成（RAG）系统在部署中经常被用户或专家反馈纠正，但现有评估大多基于静态假设，只关注平均准确率（如 EM/F1），无法刻画系统在收到反馈后是否、以及多快、多可靠地改变后续行为。
- **核心问题**：论文提出“反馈自适应”（feedback adaptation）作为 RAG 的新问题设定，核心研究问题是：**系统一旦被纠正，该纠正如何有效且快速地传播到未来语义相关的查询上？**
- **整体含义**：
  - 反馈自适应不同于监督学习、持续学习或模型编辑：后者关注总体性能、旧知识保留或定向参数更新，而本文关注**交互过程中系统行为的时间动态**。
  - 现有 RAG 基准将“正确性”与“可适应性”混为一谈，掩盖了部署场景中反馈传播速度与泛化可靠性这一关键维度。
  - 论文的主要贡献是：提出反馈自适应问题设定；形式化两个评估指标——校正时延与反馈后性能；给出最小推理时实例 PatchRAG，并进行实证研究。

## 2. 方法论

### 2.1 核心思想

- 论文提出 **PatchRAG**，一种最小化的推理时反馈自适应实例。
- 其核心是：**不重新训练、不修改模型参数**，而是将反馈作为“补丁”存储到外部记忆中，并在推理时检索、拼接到提示中，通过上下文学习即时影响生成。
- 目标是同时满足两点：
  - 即时纳入反馈，降低校正时延；
  - 泛化到语义相关但词面不同的查询，提升反馈后性能。

### 2.2 关键技术细节

- 每个反馈项表示为三元组：  
  \[
  f_i = (q_i, a_i, c_i)
  \]  
  其中 \(q_i\) 是原始查询，\(a_i\) 是修正答案，\(c_i\) 是支持证据。
- 给定新查询 \(q\)，PatchRAG 为每个反馈项计算相关性得分：  
  \[
  S_i(q) = \lambda \cdot \text{sim}(q, q_i) + (1-\lambda)\cdot \text{sim}(q, c_i)
  \]  
  其中 \(\text{sim}\) 为嵌入余弦相似度，\(\lambda \in [0,1]\) 平衡“意图匹配”和“上下文 grounding”。实验中将 \(\lambda\) 固定为 0.5。
- **意图匹配**：\(\text{sim}(q, q_i)\) 捕捉用户意图层面的相似性，即使查询与证据表面重叠少，也能检索到相关反馈。
- **上下文 grounding**：\(\text{sim}(q, c_i)\) 保持内容级相关性，防止仅由意图相似导致的虚假匹配。
- 按得分选取 top-k 反馈项，作为纠正示例，通过 in-context learning 构造增强提示，让生成器立即基于反馈条件化输出。
- 论文强调 PatchRAG 是“最小参考实现”，不是最终方案，目的是隔离反馈纳入本身的影响。

### 2.3 反馈准备与评估协议

- **pre-t 反馈**：在时间步 \(t\) 之前，用 Llama-3 8B 从文档块生成合成问答对，存入反馈记忆，用于稳定检索与记忆行为，不提供评估查询的任务监督。
- **专家反馈**：在时间步 \(t\)，用 GPT-4 对评估查询进行改写，并结合对应证据生成修正答案，构造语义一致但词面差异较大的反馈项。原始测试查询不直接存入反馈记忆，以避免数据泄漏。
- **Snapshot 评估**：虽然反馈自适应本质是在线过程，论文采用快照式评估，比较反馈注入前后系统行为，以隔离反馈注入的边际效应，控制记忆漂移和查询分布变化等混淆因素。

## 3. 实验设计

### 3.1 数据集与指标

- 数据集：
  - Natural Questions (NQ)
  - TriviaQA
  - HotpotQA
- 指标：
  - NQ 和 TriviaQA 使用 Exact Match (EM)
  - HotpotQA 使用 F1
  - **校正时延**：从反馈提供到系统准备好用更新状态处理后续评估查询的墙钟时间。
  - **反馈后性能**：在时间步 \(t\) 更新后，系统在与反馈所需修正相同的语义相关查询上的 EM/F1。

### 3.2 对比方法

- 非反馈型 RAG 增强方法：
  - Standard RAG
  - Self-RAG
  - Auto-RAG
  - ChatQA-1.5
- 反馈驱动的训练式适应基线：
  - Golden-only
  - RAFT
- 本文方法：
  - PatchRAG
- 公平设置：
  - 所有系统使用相同生成器 Llama-3 8B。
  - 检索器使用 bge-m3。
  - 反馈记忆扩展到完整检索语料规模，如 TriviaQA 约 150K。
  - \(\lambda=0.5\)。

### 3.3 额外实验

- 校正时延 vs 反馈后性能：在 TriviaQA 上比较 PatchRAG、RAFT、Golden-only，并通过减少 RAFT 更新步数观察训练预算影响。
- 不完美反馈压力测试：
  - 用检索 top-1 证据替代金标证据
  - Noise 25%/50%/75%
  - Blank：省略答案
  - Vague：仅

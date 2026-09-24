---
title: "Reasoning with Memory: Adaptive Information Management for Retrieval-Augmented Generation"
title_zh: 用记忆推理：面向检索增强生成的自适应信息管理
authors: "Hieu Man, Ro-ee Tal, Abhishek Kumar, Jaejin Cho, Benjamin Hsu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1834.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 带显式工作记忆的状态感知RAG
tldr: 多跳推理是检索增强生成的核心难题，随着推理链增长，自适应检索与智能体流水线难以维持连贯的中间推理状态。本文提出 State-Aware RAG，引入显式工作记忆作为动态认知工作区，并用可训练抽取器通过路径-结果双重奖励主动过滤、整合与更新记忆。检索器与生成器保持冻结，具备即插即用灵活性。该框架在提升多跳推理一致性的同时改善了 RAG 准确性与相关性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1834/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1834/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 512, \"height\": 512}]"
motivation: 多跳RAG在推理链变长时难以维持连贯的中间推理状态，导致准确性下降。
method: 提出State-Aware RAG，引入显式工作记忆与可训练抽取器，通过路径-结果双重奖励过滤和更新记忆。
result: 检索器与生成器保持冻结仍能即插即用提升多跳推理的一致性，兼顾局部与全局策略。
conclusion: 该框架通过自适应信息管理增强了RAG推理的准确性与连贯性，具有良好通用性。
---

## Abstract
Multi-hop reasoning remains a fundamental challenge for Retrieval-Augmented Generation (RAG) systems. Recent approaches—from adaptive retrieval to agentic pipelines—struggle to maintain coherent intermediate reasoning states as chains grow longer. We introduce State-Aware RAG, a framework that addresses this limitation through an explicit working memory that serves as a dynamic cognitive workspace for reasoning. Our modular architecture features a lightweight, trainable extractor that learns to actively filter, consolidate, and update this working memory via a novel Path-Outcome Dual Reward paradigm, which balances local coherence with global strategy. The retriever and generator remain frozen, enabling plug-and-play flexibility. Experiments on eight QA benchmarks demonstrate state-of-the-art results, on average achieving +8.6% over the best memory-augmented baseline and +9.3% over the best RL-enhanced baseline. Our architecture generalizes seamlessly to stronger generators and retrievers without retraining, establishing dynamic memory management as a critical yet underexplored dimension for advancing RAG systems.

---

## 论文详细总结（自动生成）

# 《Reasoning with Memory: Adaptive Information Management for Retrieval-Augmented Generation》论文总结

## 1. 核心问题与研究动机

- **核心问题**：多跳推理是 RAG 系统的关键难题。随着推理链变长，已有方法难以维持连贯的中间推理状态。
- **背景痛点**：
  - 标准 RAG 将检索到的信息静态追加到上下文中，导致无关、冗余、冲突信息在多步推理中不断累积，造成上下文污染与推理漂移。
  - 现有研究主要关注“信息获取”，如查询改写、迭代检索、查询分解、组件微调，却忽视了“信息管理”，即如何主动筛选、整合和维护已检索内容。
  - 静态重排序、一次性上下文压缩对多步推理中的上下文噪声和膨胀不够鲁棒。
  - 已有记忆增强 RAG 存在局限：HippoRAG 使用静态知识图谱，MemoRAG 使用一次性全局压缩，Memory-R1 主要面向对话式情节记忆，缺乏多跳推理轨迹内的细粒度、持续记忆整理。
- **整体含义**：论文主张将 RAG 从“无状态检索 + 被动上下文累积”推进为“目标导向的知识遍历”，通过显式、动态、全局共享的工作记忆来提升多跳推理的一致性与准确性。

## 2. 方法论：State-Aware RAG

### 2.1 核心思想

- 引入**显式工作记忆**作为动态认知工作区，在推理过程中持续更新，而非被动累积文档。
- 将策略分解为三个模块：
  - **Retriever R**：根据当前查询检索候选文档。
  - **Generator G**：生成中间回答与下一子问题。
  - **Extractor E**：核心控制模块，负责过滤、整合、更新工作记忆。
- **只训练 Extractor**，Retriever 与 Generator 保持冻结，实现即插即用与低训练开销。

### 2.2 状态表示与推理循环

- 每个推理状态表示为 \(S_i = (q_i, r_i, M_i)\)：
  - \(q_i\)：当前子问题。
  - \(r_i\)：中间回答。
  - \(M_i\)：全局工作记忆。
- 初始状态 \(S_0 = (x, \varnothing, \varnothing)\)，最终目标是生成正确答案 \(y\)。
- 动作空间不是固定“检索-生成”流水线，而是组合式信息管理操作，包括：问题生成、检索、信息整理、回答生成、记忆更新。

### 2.3 工作记忆管理

Extractor 通过两个阶段维护记忆：

1. **Consolidation 整合**：
   - \(I_i = E_{\text{consolidate}}(q_i, D_i, M_{i-1})\)
   - 从检索文档 \(D_i\) 和旧记忆 \(M_{i-1}\) 中提取与当前子问题相关的信息。
   - 功能包括：相关性过滤、矛盾消解、冗余消除。

2. **Memory Update 记忆更新**：
   - \(M_i = E_{\text{update}}(x, M_{i-1}, I_i, (q_i, r_i))\)
   - 将新的“问题-回答对”和提炼知识整合进全局工作记忆。

### 2.4 Path-Outcome Dual Reward 训练

- 使用 LLM-as-a-Judge 计算两类奖励：
  - **Path Reward 路径奖励**：\(R_p(r_i, q_i) = \text{JUDGE}_{\text{PATH}}(r_i, q_i)\)，评估每步局部推理质量，包括相关性、充分性、逻辑连贯性和事实准确性。
  - **Outcome Reward 结果奖励**：\(R_o(y, x, y^*) = \text{JUDGE}_{\text{OUTCOME}}(y, x, y^*)\)，评估最终答案是否正确。
- 训练目标：
  - 最大化 \(\frac{1}{n-1}\sum_{i=1}^{n-1} R_p(q_i, r_i) + \lambda R_o(y, x, y^*)\)
  - 论文中设置 \(\lambda = 2\)，强调结果奖励，同时保留路径级监督。
- 训练流程：
  - 先用 DeepSeek-R1 作为 oracle extractor 合成约 10K 条推理路径。
  - 对 Qwen3-4B extractor 进行 SFT，再用 GRPO 强化学习。

### 2.5 推理模式

- **Socratic Planning**：
  - 仅使用 A1（Decompose & Answer）和 A5（Conclude）。
  - 生成单一推理链，计算效率高。
  - 适合推理复杂度较低的任务。
- **MCTS Planning**：
  - 使用 Monte Carlo Tree Search，节点为推理状态，边为五类动作：
    - A1 Decompose & Answer
    - A2 Consolidate
    - A3 Refine
    - A4 Redirect
    - A5 Conclude
  - 使用 UCT 进行树搜索。
  - 关键特点：**全局共享记忆**，一个分支发现的信息可更新 \(M_i\) 并供其他分支使用，而不是各分支独立。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- 共评估 **8 个 QA benchmark**：
  - **多跳 QA**：2WikiMultihopQA、HotpotQA、MuSiQue、Bamboogle。
  - **单跳 QA**：SimpleQA、Natural Questions、TriviaQA、PopQA。
- 采样设置：
  - 每个数据集随机采样 1,000 条样本。
  - Bamboogle 使用全部 125 条开发集样本。
- 指标：
  - **Sub-EM**：子串精确匹配，严格词面匹配。
  - **Acc.**：使用 Claude 3.7 Sonnet 作为 LLM-as-a-Judge 判断语义等价。

### 3.2 对比方法

论文对比了七类基线：

- **Direct Generation**：Qwen3-8B、CoT。
- **Standard RAG**：RAG、RAG + Rerank。
- **Iterative Retrieval**：IR-CoT、FLARE、Search-o1。
- **Query Reformulation**：Self-RAG、RaFe。
- **Planning-Enhanced RAG**：MCTS-RAG、RAG-Star。
- **RL-Enhanced RAG**：Search-R1、S3。
- **Memory-Augmented RAG**：MemoRAG、HippoRAG、HippoRAG 2。
- 公平性考虑：尽量选择 7–14B 参数规模的生成器，并在可能时使用与 State-Aware RAG 相同的 embedding 和 generator 复现结果。

### 3.3 主要结果

- **多跳 QA**：
  - MCTS 版本平均准确率 **58.0%**。
  - 比最佳记忆增强基线 HippoRAG 2 高 **+8.6%**。
  - 比最佳 RL 增强基线 S3 高 **+9.3%**。
- **单跳 QA**：
  - Socratic 版本平均准确率 **72.7%**。
  - 比 S3 高 **+9.3%**。
- 具体表现：
  - Bamboogle：Socratic 62.8 Acc，MCTS 65.7 Acc。
  - MuSiQue：Socratic 42.2 Acc，MCTS 45.5 Acc。
  - SimpleQA：Socratic/MCTS 均为 62.9 Acc。
  - TriviaQA：Socratic 84.8 Acc，MCTS 82.9 Acc。
  - PopQA：Socratic 68.5 Acc，MCTS 68.3 Acc。

### 3.4 消融实验

- **记忆管理组件消融**（Bamboogle）：
  - 去掉 Extractor：性能崩溃，Socratic −28.1%，MCTS −26.6%。
  - 去掉 Consolidation：Socratic −7.6%，MCTS −9.4%。
  - 去掉 Memory Update：Socratic −3.9%，MCTS −6.2%。
  - 说明主动筛选与持久记忆更新都关键，且 MCTS 更依赖全局连贯记忆。
- **训练策略消融**：
  - Prompt-Only、SFT-Only、RL w/ Outcome Reward、RL w/ Path Reward、RL Dual Reward。
  - 完整 Dual Reward 最优。
  - Path-only 能提供密集局部信号，Outcome-only 提供稀疏全局信号。
  - Claude 3.7 作为 Extractor 仍显著更强，说明 Extractor 规模/能力有提升空间。

### 3.5 组件分析与推理分析

- **Generator Scaling**：
  - Qwen3-8B → Qwen3-30B-A3B：+7.4% Acc。
  - 替换为 Claude 3.7 Sonnet：+16.5% Acc。
  - 无需重新训练 Extractor，体现即插即用。
- **Retriever Scaling**：
  - E5-base → Qwen3-Embedding-4B：+1.4%。
  - 静态 Wikipedia → Google Search：+22.2%，说明知识源覆盖与排序是主要瓶颈。
- **推理步数**：
  - 3 到 5 步快速提升，之后趋于平台。
  - MCTS 在不同步数预算下平均优于 Socratic 约 +2.9%。
- **Rollout 数量**：
  - Socratic 基本持平，符合确定性单轨迹预期。
  - MCTS 随 rollout 增加持续提升，从 3 到 15 增加 +3.3%。
- **成本**：
  - 2WikiMultihopQA 上 MCTS 需要约 **6.8 倍** Generator 调用（85.9 vs 12.7），但仅带来 **2.6 点**准确率提升（62.5 vs 59.9）。

## 4. 资源与算力

- 论文**未明确说明 GPU 型号、GPU 数量、训练总时长或总能耗**。
- 已给出的训练资源与配置：
  - SFT 框架：Axolotl。
  - RL 框架：verl + vLLM。
  - 推理服务：SGLang + LiteLLM。
  - 检索：FAISS + Wikipedia 2023 dump + Qwen3-Embedding-4B。
  - Extractor：Qwen3-4B-Thinking，LoRA 微调。
  - SFT：学习率 2e-4，batch size 128，2 epochs，LoRA rank 32，alpha 64，dropout 0.05，序列长度 8192。
  - RL：GRPO，学习率 5e-7，train batch 64，mini batch 32，KL 系数 0.001，每 prompt 4 个响应，5 epochs，max prompt 2048，max response 4096。
  - 训练数据：从 HotpotQA 和 2WikiMultihopQA 选 871 个种子问题，合成约 10K 条推理路径，约 70K state-action pairs。
- 结论：论文提供了较详细的训练超参数，但算力硬件信息缺失，无法判断实际计算开销。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验：8 个 QA benchmark × 多种基线，覆盖单跳与多跳。
  - 消融实验：记忆管理组件消融、训练策略消融。
  - 组件分析：Generator 替换、Retriever/知识源替换。
  - 推理分析：推理步数、rollout 数量、成本比较。
  - 总体实验规模较大，覆盖较全面。
- **充分性**：
  - 多跳与单跳任务均有覆盖。
  - 既有主结果，也有消融、组件替换和超参分析。
  - 对成本做了专门比较，较有实践参考价值。
- **客观性与公平性**：
  - 作者尽量选择 7–14B 参数范围内的基线，并在可能时统一 embedding 与 generator。
  - 但部分基线使用不同检索源或不同模型，例如 Search-o1、MCTS-RAG 使用 Bing/Web，而本方法默认使用 Wikipedia。
  - 组件分析显示 Google Search 相比 Wikipedia 可带来 +22.2%，说明检索源差异可能影响公平性。
  - 指标同时使用 Sub-EM 和 LLM-as-a-Judge 准确率，后者更宽容，但依赖 Claude 3.7，存在评估模型偏差风险。

## 6. 主要结论与发现

- 动态工作记忆管理是 RAG 中关键但此前未被充分探索的维度。
- State-Aware RAG 在 8 个 QA benchmark 上取得 SOTA：
  - 多跳 QA 平均 58.0% Acc，超过最佳记忆增强基线 +8.6%，超过最佳 RL 增强基线 +9.3%。
  - 单跳 QA 平均 72.7% Acc，超过 S3 +9.3%。
- 仅训练

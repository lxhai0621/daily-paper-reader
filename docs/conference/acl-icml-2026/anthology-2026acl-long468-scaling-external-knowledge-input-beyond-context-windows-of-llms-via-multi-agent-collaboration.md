---
title: Scaling External Knowledge Input Beyond Context Windows of LLMs via Multi-Agent Collaboration
title_zh: 通过多智能体协作将外部知识输入扩展至超出LLM上下文窗口
authors: "Zijun Liu, Zhennan Wan, Peng Li, Ming Yan, Fei Huang, Yang Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.468.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 多智能体协作扩展外部知识突破上下文窗口
tldr: 针对大模型有限上下文窗口限制外部检索知识规模、而现有上下文扩展方法会造成信息损失的问题，本文提出多智能体框架ExtAgents。该方法以分布式方式处理海量输入，并针对现有智能体编排设计中的两大瓶颈进行改进。实验表明该框架突破了上下文窗口限制，在推理时实现了对超长外部知识输入的更好扩展性，为长上下文管理与大规模检索知识整合提供了多智能体协作新范式。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 521, \"height\": 364}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-002.webp\", \"caption\": \"\", \"page\": 6, \"index\": 2, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-004.webp\", \"caption\": \"\", \"page\": 7, \"index\": 4, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-005.webp\", \"caption\": \"\", \"page\": 7, \"index\": 5, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-006.webp\", \"caption\": \"\", \"page\": 7, \"index\": 6, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-007.webp\", \"caption\": \"\", \"page\": 7, \"index\": 7, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-008.webp\", \"caption\": \"\", \"page\": 7, \"index\": 8, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-009.webp\", \"caption\": \"\", \"page\": 7, \"index\": 9, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-010.webp\", \"caption\": \"\", \"page\": 7, \"index\": 10, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-011.webp\", \"caption\": \"\", \"page\": 7, \"index\": 11, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-012.webp\", \"caption\": \"\", \"page\": 7, \"index\": 12, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-013.webp\", \"caption\": \"\", \"page\": 7, \"index\": 13, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-014.webp\", \"caption\": \"\", \"page\": 7, \"index\": 14, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-015.webp\", \"caption\": \"\", \"page\": 8, \"index\": 15, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-016.webp\", \"caption\": \"\", \"page\": 27, \"index\": 16, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-017.webp\", \"caption\": \"\", \"page\": 27, \"index\": 17, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-018.webp\", \"caption\": \"\", \"page\": 27, \"index\": 18, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-019.webp\", \"caption\": \"\", \"page\": 27, \"index\": 19, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-020.webp\", \"caption\": \"\", \"page\": 27, \"index\": 20, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-021.webp\", \"caption\": \"\", \"page\": 27, \"index\": 21, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-022.webp\", \"caption\": \"\", \"page\": 27, \"index\": 22, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-023.webp\", \"caption\": \"\", \"page\": 27, \"index\": 23, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-024.webp\", \"caption\": \"\", \"page\": 27, \"index\": 24, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-025.webp\", \"caption\": \"\", \"page\": 27, \"index\": 25, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-026.webp\", \"caption\": \"\", \"page\": 28, \"index\": 26, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-027.webp\", \"caption\": \"\", \"page\": 28, \"index\": 27, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-028.webp\", \"caption\": \"\", \"page\": 28, \"index\": 28, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-029.webp\", \"caption\": \"\", \"page\": 28, \"index\": 29, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-030.webp\", \"caption\": \"\", \"page\": 28, \"index\": 30, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-031.webp\", \"caption\": \"\", \"page\": 28, \"index\": 31, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-032.webp\", \"caption\": \"\", \"page\": 28, \"index\": 32, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-033.webp\", \"caption\": \"\", \"page\": 28, \"index\": 33, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-034.webp\", \"caption\": \"\", \"page\": 28, \"index\": 34, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-035.webp\", \"caption\": \"\", \"page\": 28, \"index\": 35, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-036.webp\", \"caption\": \"\", \"page\": 28, \"index\": 36, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-037.webp\", \"caption\": \"\", \"page\": 28, \"index\": 37, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-038.webp\", \"caption\": \"\", \"page\": 28, \"index\": 38, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-039.webp\", \"caption\": \"\", \"page\": 28, \"index\": 39, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-040.webp\", \"caption\": \"\", \"page\": 28, \"index\": 40, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-041.webp\", \"caption\": \"\", \"page\": 28, \"index\": 41, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-042.webp\", \"caption\": \"\", \"page\": 28, \"index\": 42, \"width\": 2400, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long468/fig-043.webp\", \"caption\": \"\", \"page\": 28, \"index\": 43, \"width\": 2400, \"height\": 3000}]"
motivation: 大模型有限上下文窗口限制了外部检索知识的规模，现有上下文扩展方法会造成信息损失。
method: 提出多智能体框架ExtAgents，以分布式方式处理海量输入，并针对智能体编排的两大瓶颈进行改进。
result: 该框架突破上下文窗口限制，在推理时实现对超长外部知识输入的更好扩展性。
conclusion: 为长上下文与大规模检索知识管理提供了多智能体协作新范式。
---

## Abstract
With the rapid advancement of post-training techniques for reasoning and information seeking, large language models (LLMs) can incorporate a large quantity of retrieved knowledge to solve complex tasks. However, the limited context window of LLMs obstructs scaling the amount of external knowledge input, prohibiting further improvement. Existing context window extension methods inevitably cause information loss. LLM-based multi-agent methods emerge as a new paradigm to handle massive input in a distributional manner, where we identify two core bottlenecks in existing agent orchestration designs. In this work, we develop a multi-agent framework, **ExtAgents**, to overcome the bottlenecks and enable better scalability in inference-time knowledge integration without longer-context training. Benchmarked with our enhanced multi-hop question answering test, ** ∞ Bench+**, and other public test sets including long survey generation, ExtAgents significantly enhances the performance over existing non-training methods with the same amount of external knowledge input, regardless of whether it falls *within or exceeds the context window*. Moreover, the method maintains efficiency due to high parallelism. We believe further study in the coordination of LLM agents on increasing external knowledge input could benefit real-world applications.

---

## 论文详细总结（自动生成）

# 论文总结：通过多智能体协作将外部知识输入扩展至超出LLM上下文窗口

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：随着推理与信息检索后训练技术（如长链思维、搜索增强推理）的快速发展，LLM 已能利用大量检索知识解决复杂任务；同时模型上下文窗口不断扩展，已超过一本书的长度。
- **核心矛盾**：对多跳问答、企业知识库推理、长篇综述写作等真实任务而言，**更多外部知识输入通常带来更好效果**，但 LLM 有限的上下文窗口阻碍了外部知识规模的进一步扩展。
- **现有方案的缺陷**：
  - **长上下文训练**（位置插值、YaRN、LongRoPE2 等）：经济成本高、注意力二次复杂度不可行、长上下文训练数据稀缺。
  - **RAG（检索增强生成）**：受排序误差限制，可能排除关键证据。
  - **上下文压缩**：压缩器可能丢弃只在推理链展开后才有用的细粒度线索。
  - 二者**都不可避免地造成信息损失**。
- **研究切入点**：LLM 多智能体协作以分布式方式处理海量输入是新兴范式，但现有智能体编排设计存在两个核心瓶颈。本文提出核心问题：**LLM 能否通过扩展超出上下文窗口的外部知识输入，持续提升任务表现？**
- **两项要求**：（i）可扩展的上下文扩展方法能接受海量输入；（ii）知识应在 LLM 与智能体的编排中被有效整合。本文聚焦于**无需长上下文训练的推理时知识整合可扩展性**。
- **识别出的两大瓶颈**（现有编排设计的共性）：
  - **知识同步（Knowledge Synchronization）**：瓶颈是每个智能体可访问智能体的"带宽"（bandwidth）。
  - **知识整合推理（Knowledge-Integrated Reasoning）**：瓶颈是推理过程中冗余信息的比例。

## 2. 方法论：ExtAgents 框架

### 核心思想
- 沿用分布式范式，将完整输入切分为适配小窗口的智能体专属上下文块（chunk）。
- 将智能体角色简化为两类，可处理任意规模输入：
  - **Seeking Agents（搜寻智能体）**：数量等于块数 N，理解分到的知识块并对查询做相关性打分，可选地剔除冗余块。
  - **Reasoning Agent（推理智能体）**：整合累积知识生成最终答案，判断可回答性，信息不足时可拒答，兼容多跳 QA 与长文生成。

### 关键组件一：全局知识同步（Global Knowledge Synchronization, GKS）
- 与以往仅限局部邻域交互的方法（LongAgent、LLM×MapReduce）不同，本文让**每个智能体具备全局可见性**，通过排序消息再组装上下文，最大化同步带宽。
- 形式化：第 t 步，每个 Seeking Agent 依据查询 q、本地块 d_i 与上一步全局消息集 M_{t-1} 更新消息 m_{i,t}。
- 每个消息对查询打分 h_{i,t}∈R⁺，用 Topk 选择相关性最高的 k 条消息，k 尽可能大但满足 `|q| + |d_i| + |Topk(M_{t-1})| < L`（L 为上下文长度）。
- 打分可附加 prompt 或使用独立度量工具（如检索分数），**分布式并行执行**，所有 Seeking Agents 可在同一时间步并行运行。

### 关键组件二：知识累积推理（Knowledge-Accumulating Reasoning, KAR）
- 每次同步步后启动推理；Reasoning Agent **增量整合**最相关消息，避免冗余信息过载。
- 第 s 次推理迭代（1≤s≤S）选择 top-2^s 条消息构成累积上下文 `M_r^(s) = Top2s({m_{i,t⋆}})`。
- 推理智能体先判断可回答性，仅在可回答时输出答案并终止流程；否则达到最大迭代数 S 后开启新一轮知识同步。
- 长综述生成采用草稿法：先生成提纲，再逐节填充；每节完成后新流程将上一节纳入查询以保持连贯。

### 并行与异步流水线
- 当打分用独立工具时，每次推理迭代可独立选取同步消息，实现并行；例如 top (2^(s-1)+1)~2^s 消息可与 top 2^(s-1) 消息的推理**交错异步**同步，形成流水线。

### 瓶颈对比（Table 1）
| 方法 | 同步带宽 | 推理上下文 | 可并行组件 |
|---|---|---|---|
| Chain of Agents | 2 | {m_{N,N}} | 无 |
| LongAgent | 2 | {m_{i,t}} 全部 | 同步 |
| LLM×MapReduce | O(L/\|m\|) | {m_{i,T}} | 同步 |
| **ExtAgents** | **N** | **Top2s(...)** | **同步 & 推理** |

## 3. 实验设计

### 数据集 / 场景
- **∞Bench+**（本文构建）：增强版多跳 QA 基准。用 gpt-4o-mini-2024-07-18 过滤掉任何 8k token 块即可回答的样本，并补充原 ∞Bench 中超过 128k token 的样本。含 En.QA（294 样本）与 Zh.QA（184 样本）两个子集。
- **HotpotQA**：开放域多跳问答（基于 Wikipedia），用 BM25 检索器。
- **AutoSurvey**：长篇综述生成（真实应用场景），使用预检索论文。

### Benchmark 构建依据
- 发现现有长上下文基准存在偏差：大量查询可用小窗口扫描文档回答。
- 敏感性检查表明 8k 扫描窗口稳健（相比 16k、32k 更有效剔除"捷径"查询而不激进削减数据）。
- 补充 Helmet correctness 分数、引用数、引用密度、重复率等辅助指标。

### 对比方法
- **Direct Input**：直接输入截断上下文。
- **LLM×MapReduce**：SOTA 长上下文多智能体方法。
- **Chain of Agents**：线性拓扑、带宽为 2。
- **DRAG / IterDRAG**：推理时可扩展检索方法（多跳 QA）。
- **AutoSurvey**：综述生成基线（仅替换生成过程）。

### 实验设置
- 输入长度控制为 {8k, 16k, 32k, 64k, 128k, 256k, 512k, 1024k} token，最大上下文窗口 128k。
- 使用的模型：DeepSeek-R1-Distill-Llama-8B、gpt-4o-mini-2024-07-18、Llama-3.1-8B-Instruct、gpt-4o-2024-08-06、Llama-3.2-3B-Instruct。
- 采样温度：闭源模型 0，开源模型 0.1；最大输入长度闭源 128k、开源 131,092 token。
- 报告 3 次运行的中位数以保证稳定复现。
- 默认超参数：最大同步步数 T=5，仅在 t=1 采用知识累积（S=5，序列 1→2→4→8→全部）。

## 4. 资源与算力

- **GPU**：4 张 NVIDIA A100 80GB GPU（用于开源模型部署与延迟测量）。
- **闭源模型**：通过 API 访问。
- **训练时长**：本文为**推理时方法，无需额外训练**，故未报告训练时长；实验均为推理评测。
- **延迟分析**：固定 16k token 块、在 4 张 A100 上测量不同输入长度下的延迟（Figure 6）。
- **异构实验**：两种 LLM 各部署在 2 张 GPU 上。
- **成本分析**：基于 token 数估算平均花费（Table 9，1M 输入 $0.15、1M 输出 $0.60），ExtAgents 因全局同步带宽较大而成本略高于部分基线（HotpotQA 上 ExtAgents $0.021 vs LLM×MapReduce $0.022）。

## 5. 实验数量与充分性

- **主实验**：3 个多跳 QA 基准（HotpotQA、En.QA、Zh.QA）+ 1 个长综述生成任务，覆盖多个输入长度与块大小。
- **消融实验**：
  - GKS 与 KAR 的消融（Figure 5）。
  - 同步步数 T 的敏感性（T=1,2,5,10，Table 12）。
  - 推理迭代调度策略 S 的消融（base-2 对数、base-4 对数、比例分数、穷举累积、小窗口约束，Table 13）。
- **泛化实验**：跨 5 个 LLM 家族（兼容性），含更弱（Llama-3.2-3B）与更强（gpt-4o）模型。
- **效率实验**：延迟分析、成本分析、异构模型协作（Table 6）。
- **鲁棒性分析**：可回答性检查的假阳性/假阴性分析（371 样本，Table 11）。
- **补充结果**：Helmet 分数、原始 ∞Bench 结果、Chain of Agents 缩放表现（Table 10）。
- **充分性与公平性**：
  - 实验覆盖较全面，含跨任务、跨模型、消融、效率与鲁棒性分析。
  - 基线在相同输入长度与块大小下对比，且重新实现以对齐设置；报告 3 次中位数。
  - **客观性亮点**：指出 LLM×MapReduce 在超出上下文窗口时无优势，且通过 ∞Bench+ 消除基准偏差。
  - **潜在不足**：∞Bench+ 过滤后样本数有限（En.QA 294、Zh.QA 184），可能影响评测稳定性；部分消融仅在小规模样本（如 371 样本）上进行。

## 6. 主要结论与发现

- **可扩展性**：ExtAgents 随外部知识输入增加持续提升性能，在 HotpotQA、∞Bench+ 上均显著优于所有基线，且在**输入超出上下文窗口时仍保持增益**（对比 LLM×MapReduce 无优势甚至下降）。
- **性能表现**（Table 4，最优设置）：gpt-4o-mini 下 HotpotQA F1=.534、En.QA=.382、Zh.QA=.482（均用 1024k 输入）；gpt-4o-2024-08-06 下 HotpotQA F1 从 N=1 的 .553 提升至 .597。
- **长综述生成**：相比 AutoSurvey，LLM-as-a-Judge 分数 7.63 vs 6.75，引用数 191 vs 113，重复率更低（1.80 vs 2.41）。
- **效率**：延迟随输入线性增长（直接输入为二次增长）；无限并行下甚至可降低延迟。
- **消融结论**：移除 KAR 性能显著下降（尤其知识量大时），说明 KAR 有效突破信息过载瓶颈；移除 GKS 也导致下降，说明带宽对捕捉相关信息有帮助。
- **模型兼容性**：更强 LLM 从 ExtAgents 获益更多；Llama 存在语言偏差

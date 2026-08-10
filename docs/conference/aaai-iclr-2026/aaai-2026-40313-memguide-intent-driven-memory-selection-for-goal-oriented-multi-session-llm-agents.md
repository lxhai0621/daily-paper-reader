---
title: "MemGuide: Intent-Driven Memory Selection for Goal-Oriented Multi-Session LLM Agents"
title_zh: MemGuide：面向目标导向多会话LLM代理的意图驱动记忆选择
authors: "Yiming Du, Bingbing Wang, Yang He, Bin Liang, Baojun Wang, Zhongyang Li, Lin Gui, Jeff Z. Pan, Ruifeng Xu, Kam-Fai Wong"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40313/44274"
tags: ["query:agent"]
score: 9.0
evidence: 面向目标导向多会话LLM代理的意图驱动记忆选择，利用RAG与长上下文记忆
tldr: 现有的多会话任务型对话系统依赖RAG和长上下文做长期记忆，但只按语义相似度检索，忽略任务意图，导致多会话连贯性下降。为此提出MemGuide两阶段意图驱动记忆选择框架：先检索目标一致的QA式记忆单元，再通过缺槽引导的过滤按槽补全增益重排。还发布了首个多会话TOD基准MS-TOD，验证了相比语义相似度基线在连贯性上的提升。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40313/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 840, \"height\": 790, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40313/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 707, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40313/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1568, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40313/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 749, \"height\": 449, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40313/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 429, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40313/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 671, \"height\": 518, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40313/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1321, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40313/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 679, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40313/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 823, \"height\": 604, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40313/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 860, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40313/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 846, \"height\": 564, \"label\": \"Table\"}]"
motivation: 现有长期记忆利用多基于语义相似度检索，忽略任务意图，损害多会话连贯性。
method: 提出两阶段意图驱动记忆选择框架：意图对齐检索召回目标一致的QA记忆单元，缺槽引导过滤用思维链推理和微调LLaMA-8B按槽补全增益重排。
result: 引入MS-TOD基准并实验，证明该方法在多会话连贯性上优于语义相似度基线。
conclusion: MemGuide表明以任务意图指导记忆选择可显著提升多会话LLM代理的长期记忆利用效果。
---

## Abstract
Modern task-oriented dialogue (TOD) systems increasingly rely on large language model (LLM) agents, leveraging Retrieval-Augmented Generation (RAG) and long-context capabilities for long-term memory utilization. However, these methods prioritise semantic similarity over task intent, degrading multi-session coherence. We propose MemGuide, a two-stage intent-driven memory selection framework: (1) Intent‑Aligned Retrieval retrieves goal-consistent QA‑formatted memory units; (2) Missing‑Slot Guided Filtering reranks units by slot-completion gain via a chain‑of‑thought reasoner and fine‑tuned LLaMA‑8B filter. We also introduce the MS-TOD, the first multi-session TOD benchmark with 132 diverse personas, 956 task goals, and annotated intent-aligned memory targets. Evaluations on MS-TOD show that MemGuide boosts task success rate by 11% (88%→99%) and reduces dialogue length by 2.84 turns, and matches single‑session performance.

---

## 论文详细总结（自动生成）

# MemGuide：面向目标导向多会话LLM代理的意图驱动记忆选择——论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：现代任务型对话（TOD）系统越来越多地依赖大语言模型（LLM）代理，利用检索增强生成（RAG）和长上下文能力进行长期记忆利用。已有方法主要基于语义相似度检索历史对话或直接将全部历史拼入上下文。
- **核心问题**：这些方法优先考虑表面语义相似性，而忽略任务意图和槽位级连续性，导致多会话对话的连贯性下降，难以支持跨会话的目标追踪、意图演化和槽位状态维护。
- **现实差距**：真实用户常跨多个会话完成复杂目标，但现有TOD数据集和模型（如MultiWOZ、SGD等）大多局限于单会话设置，造成系统能力与实际需求之间的根本性鸿沟。
- **整体意义**：论文提出**MemGuide**框架与**MS-TOD**基准，旨在将长期用户历史转化为可操作的目标一致上下文，实现跨会话、少轮次、任务连贯的对话生成，弥补多会话TOD研究的空白。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
MemGuide是一个**两阶段意图驱动记忆选择**框架，不依赖纯语义相似度，而是结合任务意图与槽位级信息需求来筛选长期记忆。

### 方法流程（文字说明）

1. **意图对齐检索（Intent-Aligned Retrieval）**
   - 给定当前对话上下文 `c`，使用GPT-4o-mini生成用户当前高层意图描述 `d_int`（如“预订去旧金山的酒店”）。
   - 将该意图描述作为检索键，与记忆库中存储的每条历史意图键 `k_i` 进行语义相似度计算（使用text-embedding-3-small等嵌入模型）。
   - 选取Top-K个意图主题一致的历史记忆条目（每个条目包含一组QA格式的记忆单元）作为候选集合 `M_cand`。

2. **缺失槽位引导过滤（Missing-Slot Guided Filtering）**
   - 先通过**CoT槽位推理器**分析当前对话上下文与意图，枚举所有必要槽位，检查已填充槽位，输出尚未确认/填充的缺失槽位列表 `L_miss`。
   - 再使用**微调后的LLaMA-8B过滤器**，对候选集合中的每个QA对 `(q_ij, a_ij)` 估计其填补缺失槽位的概率：
     ```
     s_ij = P(y=1 | c, L_miss, q_ij, a_ij)
     ```
     其中 y=1 表示该答案能填充某个缺失槽位。
   - 使用二分类交叉熵损失训练该过滤器：
     ```
     L = -Σ_ij [y_ij log s_ij + (1 - y_ij) log(1 - s_ij)]
     ```
   - 最终综合分数为语义相关分数与槽位补全分数的加权和：
     ```
     s_final,ij = α · s_pre,ij + (1 - α) · s_ij
     ```
   - 按最终分数选取Top-K个QA对的答案作为核心记忆 `A_core`。

3. **响应生成（Response Generation）**
   - 将对话上下文、核心事实 `A_core` 和缺失槽位列表 `L_miss` 输入LLM Reader，生成自然且主动的回复。
   - 例如根据历史偏好主动确认“上次您乘坐的是加拿大航空，这次是否仍选择该航班？”，减少冗余交互，加快任务完成。

## 3. 实验设计：数据集 / 场景 / 基准 / 对比方法

### 数据集与基准
- **MS-TOD**（提出的新基准）：首个多会话TOD基准，包含16个领域、19个意图、956个任务目标、2861个对话、18,530个话语；132个模拟用户，每人平均21.67个会话、5.45个意图；平均每任务4.24个槽位。
- 数据构建流程：基于SGD生成三阶段会话（不完整→更新→最终确认）；人工标注确认型响应；构建QA式记忆库；经过多人验证与一致性评估。
- 另使用**SGD**和**MultiWOZ 2.2**单会话基准验证DST泛化能力。

### 对比方法
- **通用LLM**：LLaMA3-8B、Qwen2.5-7B、Mistral-7B、GPT-4o-mini，比较全上下文提示（FCP）与MemGuide。
- **传统TOD系统**：BERT-DST、LDST、AutoTOD。
- **长文本摘要方法**：基于ChatCite的摘要式记忆方法。
- **检索基线**：BM25、密集检索、混合检索、Oracle上界。

### 评估指标
自动指标：GPT-4分数、联合目标准确率（JGA）、对话轮次效率（DTE）、任务成功率（S.R.）；人工评估：准确性（A）、信息量（I）、连贯性（C）及其平均（A.I.C.）。

## 4. 资源与算力

- 论文**未明确说明**具体GPU型号、数量、训练时长等算力资源。
- 仅提及使用GPT-4o-mini作为意图提取和CoT推理器，以及微调一个LLaMA-8B过滤器，但未给出训练该过滤器的计算成本细节。
- 推测实验在常规学术GPU集群上完成，但无法从文中确认。

## 5. 实验数量与充分性

实验较为充分，主要包括：
- **主实验**：在4种不同LLM下对比FCP与MemGuide（表3），覆盖自动与人工指标。
- **传统TOD与摘要基线对比**（表4）：对比BERT-DST、LDST、AutoTOD、ChatCite。
- **单会话DST泛化**（表5）：在SGD和MultiWOZ 2.2上与多种DST模型对比。
- **消融实验**：分别验证意图对齐检索（表6）和缺失槽位引导过滤（图4）的有效性。
- **案例研究**（表7）：对比FCP、Hybrid RAG、ChatCite、MemGuide的实际生成效果。
- **人工评估**：盲审方式，多维度评分。

**充分性评价**：
- 优点：覆盖多种模型类型、多个数据集、多项指标，并有消融与案例，结论可信度较高。
- 客观性/公平性：统一使用相同LLM作为生成器进行对比，减少了变量干扰；但MS-TOD数据集由论文作者构建，可能存在一定偏向性；人工评估样本量和标注者数量未详细披露。

## 6. 论文的主要结论与发现

- MemGuide在两个阶段分别对齐意图和利用缺失槽位过滤，显著优于纯语义相似度检索和全上下文提示。
- 在MS-TOD上，MemGuide将任务成功率从88%提升至99%（+11%），平均减少2.84轮对话，达到甚至超过单会话系统表现。
- 在不同底层LLM上均稳定提升：例如Mistral-7B下JGA从0.73升至0.80，DTE从2.52降低至1.21（降52%）；GPT-4o-mini下DTE从6.03降至3.19（降47%）。
- 与传统TOD系统和摘要方法相比，MemGuide全面领先，JGA提升至0.70，SR达0.99。
- 在单会话DST基准上，MemGuide*在SGD上达到0.846 JGA，在MultiWOZ 2.2上达到0.879 JGA，刷新或接近SOTA。
- 消融验证了意图对齐检索（GPT-4分数提升最多1.29分）和缺失槽位过滤（Recall@5平均提升7.7%）均起关键作用。

## 7. 优点

- **问题定位精准**：指出多会话TOD中“语义相似≠任务相关”的痛点，提出意图+槽位双重引导的记忆选择，思路新颖。
- **方法设计可解释**：两阶段流程清晰，意图对齐保证主题一致，缺失槽位过滤保证信息增益，最终响应生成有明确依据。
- **基准贡献**：MS-TOD是首个带有人物设定、多会话任务目标、意图对齐记忆标注的TOD基准，填补领域空白。
- **实验全面**：覆盖多LLM、传统TOD、摘要方法、单会话泛化、消融与案例，验证了方法的鲁棒性。
- **工程实践价值**：使用较小的LLaMA-8B做过滤器，结合LLM推理，兼顾效果与效率。

## 8. 不足与局限

- **算力信息缺失**：未报告GPU型号、数量、训练时间，不利于复现和公平比较成本。
- **基准构建偏差风险**：MS-TOD由作者使用GPT-4合成，模拟用户可能缺乏真实对话的自然性与噪声；人工验证规模未详细报告，可能存在标注偏差。
- **评估场景局限**：主要评估“确认型响应”生成，对更复杂的多轮任务规划、用户情绪、纠错场景覆盖不足。
- **过滤器依赖训练数据**：LLaMA-8B过滤器的训练数据由同一流程生成，与测试分布相似，可能导致性能高估。
- **记忆格式限制**：QA式记忆适用于结构化槽位任务，对非结构化长期偏好或叙事性记忆支持有限。
- **跨语言/跨文化泛化**：未讨论非英语场景，实际部署时可能受限于语言和领域适配。

（完）

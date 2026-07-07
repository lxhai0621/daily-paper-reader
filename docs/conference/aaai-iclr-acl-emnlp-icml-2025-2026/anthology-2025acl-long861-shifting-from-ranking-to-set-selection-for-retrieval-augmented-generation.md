---
title: Shifting from Ranking to Set Selection for Retrieval Augmented Generation
title_zh: 从排序到集合选择：检索增强生成的转变
authors: "Dahyun Lee, Yongrae Jo, Haeju Park, Moontae Lee"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.861.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 集合式段落选择方法提升RAG
tldr: SetR针对现有RAG检索只考虑段落个体相关性而导致复杂查询信息不足的问题，引入集合式选择方法。通过思维链推理明确查询的信息需求，并选择最优段落集合共同满足这些需求。实验表明，SetR在多跳QA基准上超越现有模型，提升了检索的综合覆盖度。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1642, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1608, \"height\": 750, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 714, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 741, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 978, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1647, \"height\": 394, \"label\": \"Table\"}]"
motivation: 现有RAG检索注重个体相关而忽略集合完整性，不适用于多跳问题。
method: 使用思维链推理解析信息需求，并基于集合选择最优段落群。
result: 在多跳QA基准上性能超越强基线，包括基于LLM的重排序器。
conclusion: 集合式选择是提升RAG检索质量的有效策略。
---

## Abstract
Retrieval in Retrieval-Augmented Generation (RAG) must ensure that retrieved passages are not only individually relevant but also collectively form a comprehensive set.Existing approaches primarily rerank top- k passages based on their individual relevance, often failing to meet the information needs of complex queries in multi-hop question answering.In this work, we propose a set-wise passage selection approach and introduce SetR, which explicitly identifies the information requirements of a query through Chain-of-Thought reasoning and selects an optimal set of passages that collectively satisfy those requirements.Experiments on multi-hop RAG benchmarks show that SetR outperforms both proprietary LLM-based rerankers and open-source baselines in terms of answer correctness and retrieval quality, providing an effective and efficient alternative to traditional rerankers in RAG systems.The code is available at https://github.com/LGAI-Research/SetR

---

## 论文详细总结（自动生成）

# 论文总结：Shifting from Ranking to Set Selection for Retrieval Augmented Generation

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：现有的检索增强生成（RAG）系统通常采用“重排序 + top-k 选择”策略，仅根据每个段落的个体相关性打分并选取前k个。这种方法忽略了段落间的多样性、完整性和综合性，尤其对于多跳问答等复杂查询，往往无法提供足够的信息覆盖，导致生成答案不完整或不准确。
- **研究动机**：RAG系统的信息需求与搜索引擎不同——搜索引擎只需返回相关结果，而RAG需要一组能共同覆盖查询所有必要线索的段落。作者提出应转向“集合式段落选择”，从整体优化所选集合的质量。
- **核心思路**：通过思维链（Chain-of-Thought, CoT）推理明确查询的信息需求（Information Requirement Identification, IRI），然后选择一组最能共同满足这些需求的段落，不再依赖传统的排序分数。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 核心思想
- **集合式选择（Set Selection）**：将检索建模为从候选段落池中选择一个最优子集的问题，优化目标是集合的集体相关性、覆盖度和精简性，而非个体排序。
- **信息需求识别（IRI）**：通过零样本CoT提示，让模型先列举回答查询所需的关键信息，再为每个需求找到包含该信息的段落，最后综合选出一组覆盖最广、最少冗余的段落。

### 关键技术细节
- **模型架构**：基于 Llama-3.1-8B-Instruct 微调得到 SetR，支持三种变体：
  - `SetR-Selection only`：直接输出所选段落，无推理过程。
  - `SetR-CoT`：使用通用CoT（“Let's think step by step”），但未显式分解信息需求。
  - `SetR-CoT & IRI`（完整模型）：采用专门设计的CoT提示，先列需求、再匹配、再选择。
- **数据构建**：使用 MS MARCO v1 的 40K 训练问题，每组搭配 top-20 候选段落。教师模型 GPT-4o 根据零样本提示生成推理和选择结果，作为蒸馏目标。
- **训练细节**：
  - 基于 Llama-3.1-8B-Instruct，使用 AdamW 优化器，学习率 5×10⁻⁶，有效 batch size 512，训练 5 个 epoch。
  - 使用 Axolotl 框架，在 16×A100 GPU 上训练。
- **推理流程**：
  1. 第一级检索（如 bge-large-en-v1.5）获取 top-20 段落。
  2. SetR 接收查询和候选段落，输出 CoT 推理和选中的段落（数量不限，通常 2-4 个）。
  3. 将所选段落作为上下文输入生成器（Llama-3.1-8B-Instruct 或 GPT-4o）生成最终答案。

## 3. 实验设计

### 数据集
- **端到端 QA**：HotpotQA、2WikiMultiHopQA、MuSiQue、MultiHopRAG（均为多跳问答基准）。
- **检索评估**：MultiHopRAG（提供金证据列表，可精确计算覆盖度）。

### 对比方法
- 无监督：BM25
- 监督稠密检索：bge-large-en-v1.5
- 基于交叉编码器的重排序：bge-reranker-large
- LLM 重排序器：RankLlama、RankVicuna、RankZephyr、FirstMistral、RankGPT（gpt-4o）

### 实验设置
- 第一级检索固定为 top-20，生成器固定为 Llama-3.1-8B-Instruct（对于 MultiHopRAG 使用 GPT-4o 以保证公平）。
- 所有基线通过 Rankify 工具包实现。
- 评估指标：
  - 端到端 QA：Exact Match (EM)、F1、Accuracy
  - 检索：MRR、NDCG、Precision、Recall、信息覆盖率 (IC@k)

## 4. 资源与算力

- **训练**：使用 16×A100 GPU，每个变体训练 5 个 epoch，batch size 512。论文未明确给出具体训练时长，但基于常见经验，估计在数小时至一天内完成（8B 模型 + 40K 数据）。
- **推理**：SetR 使用 Llama-3.1-8B-Instruct，计算开销适中；教师模型 GPT-4o 仅用于数据标注，推理时无需使用。

## 5. 实验数量与充分性

- **数量**：共包含
  - 主实验（表1）：4 个数据集，对比 11 种方法（含变体），每个方法报告 EM、F1、Accuracy。
  - 检索评估（表2）：MultiHopRAG 上的 6 种指标。
  - 消融实验（表3、表4）：在教师模型统一设置下对比排序与选择，及在统一训练框架下公平对比。
  - 效率分析（表5）：输出 token、输入 token 统计。
  - 信息覆盖与鲁棒性分析（图3）：Hit@k 分布、信息覆盖率曲线、不同 k 值下的 QA 性能。
- **充分性**：实验覆盖多个多跳数据集、多种基线、多个消融变体、方法级对比和公平设置。结论有充分数据支持，且性能提升统计显著（如 SetR 使用更少段落但 F1 更高）。实验设计客观公平。

## 6. 主要结论与发现

1. **SetR 在端到端 QA 上全面超越所有基线**，尤其在 F1 和 Accuracy 上提升显著（如 HotpotQA 上 EM 提升 2.8 点，F1 提升 3.7 点）。
2. **集合式选择比排序更有效**：即使使用相同的教师模型（GPT-4o），集合选择也优于排序（表3），证明方法本身的优势。
3. **信息需求识别（IRI）是关键**：在消融中，`SetR-CoT & IRI` 优于 `SetR-CoT` 和 `SetR-Selection only`，说明显式分解需求能提升覆盖度和精确度。
4. **使用更少段落获得更好性能**：SetR 平均只选择 2.91 个段落（基线为 5 个），却取得更高准确率，表明其抗噪声能力强，能有效去冗余。
5. **检索质量提升**：在 MultiHopRAG 上，Precision 和 Recall 分别提升 3.8%–4.6% 和 0.7%–2.7%，信息覆盖率从 19.33% 提升至 36.49%。
6. **效率优势**：生成器接受的输入 token 数大幅减少（如 MultiHopRAG 上从 2672 降至 1240），同时输出质量更高。

## 7. 优点

- **创新性**：首次明确提出 RAG 中“集合覆盖”问题，并设计端到端的集合选择框架，区别于传统排序。
- **实用性**：通过蒸馏得到轻量模型（8B），可在实际系统中替代重排序器，无需多步迭代，单步完成。
- **实验严谨**：不仅评估端到端生成，还单独评估检索性能，并提供方法级控制实验（统一教师、统一训练框架），确保结论归因于方法而非模型或数据差异。
- **开源贡献**：完整代码、训练配方和模型均已开源，便于复现和扩展。
- **效率分析**：提供了 token 级别的计算开销对比，证明方法在降低输入冗余的同时保持高性能。

## 8. 不足与局限

- **依赖初始检索质量**：SetR 在 top-20 候选上选择，若第一级检索遗漏关键信息，则无法补偿。
- **领域覆盖有限**：仅测试了多跳问答场景，未验证在代码生成、对话等其他 RAG 任务中的表现。
- **推理能力依赖基础模型**：SetR 的 CoT 推理质量受限于 Llama-3.1-8B 的能力，若基础模型推理弱，可能影响选择效果。
- **额外推理开销**：虽然输出 token 少，但 SetR 推理本身仍需生成 CoT 文本，相比纯排序模型有一定额外延迟（但比多步迭代方法轻量）。
- **缺乏对更大候选池（如 top-100）的验证**：论文提及这是未来方向，当前仅验证 top-20。

（完）

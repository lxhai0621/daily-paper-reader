---
title: "Correcting on Graph: Faithful Semantic Parsing over Knowledge Graphs with Large Language Models"
title_zh: 图上修正：利用大语言模型在知识图谱上进行可信语义解析
authors: "Ruilin Zhao, Feng Zhao, Hong Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.280.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 知识图谱上的语义解析框架，实现可信推理
tldr: 复杂多跳问答需要有效连接大语言模型与知识图谱。本文提出Correcting on Graph（CoG）框架，通过结构化知识解码让LLM生成事实感知的逻辑查询，并利用知识路径修正来纠正错误。实验表明CoG在多个KGQA数据集上取得高准确率，为结构化知识集成RAG提供了新范式。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.280/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1623, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.280/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 784, \"height\": 300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.280/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 728, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.280/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 745, \"height\": 821, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1648, \"height\": 879, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 781, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 782, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.280/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1664, \"height\": 830, \"label\": \"Table\"}]"
motivation: 大语言模型与知识图谱的有效交互对复杂推理至关重要。
method: 提出CoG框架，包括结构化知识解码和知识路径修正两个阶段。
result: 在多个KGQA基准上，CoG显著提升了多跳问答的准确性。
conclusion: 将语义解析与知识图谱结合能够构建更可靠的问答系统。
---

## Abstract
Complex multi-hop questions often require comprehensive retrieval and reasoning. As a result, effectively parsing such questions and establishing an efficient interaction channel between large language models (LLMs) and knowledge graphs (KGs) is essential for ensuring reliable reasoning. In this paper, we present a novel semantic parsing framework Correcting on Graph (CoG), aiming to establish faithful logical queries that connect LLMs and KGs. We first propose a structured knowledge decoding that enables the LLM to generate fact-aware logical queries during inference, while leveraging its parametric knowledge to fill in the blank intermediate entities. Then, we introduce a knowledge path correction that combines the logical query with KGs to correct hallucination entities and path deficiencies in the generated content, ensuring the reliability and comprehensiveness of the retrieved knowledge. Extensive experiments demonstrate that CoG outperforms the state-of-the-art KGQA methods on two knowledge-intensive question answering benchmarks. CoG achieves a high answer hit rate and exhibits competitive F1 performance for complex multi-hop questions.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：大型语言模型（LLM）在处理复杂多跳问题时面临事实知识缺乏和幻觉问题，而知识图谱（KG）可作为外部知识源。现有语义解析方法（如RoG）生成的关系路径（仅包含关系序列）缺乏中间实体的约束，导致37.2%的查询无效——即生成看似合理但无法从KG检索到任何信息的逻辑查询。
- **整体含义**：本文提出Correcting on Graph（CoG）框架，旨在通过结构化知识解码和知识路径修正，建立LLM与KG之间可信的、可执行的逻辑查询，从而提升多跳问题回答的准确率和覆盖率。

## 2. 方法论

### 核心思想
- 将KG中的知识路径视为**连续实体与关系的序列**（例如：话题实体→关系1→中间实体→关系2→答案实体），强制LLM生成包含中间实体的完整知识路径，并利用KG对路径中的幻觉实体和路径缺失进行修正。

### 关键技术细节
- **结构化知识解码**：
  - 知识背诵（Knowledge Reciting）：利用训练集中的问题-路径对（最短路径，≤2跳）微调LLM（Llama 3.1-8B-Instruct），使其能够根据问题生成从话题实体到答案实体的完整知识路径，形式为：`eq → r1 → e1 → r2 → ... → rn → ea`。
  - 知识解码（Knowledge Decoding）：推理时，使用微调后的LLM和束搜索（beam width=2）生成多条可能的知识路径。将路径中的中间实体替换为占位符，提取逻辑查询`eq → r1 → ? → r2 → ... → ?`。
- **知识路径修正**：
  - 幻觉实体修正：执行逻辑查询，从KG中检索真实路径，替换生成路径中不存在的中间实体。
  - 路径缺陷修正：通过广度优先搜索（BFS）从话题实体出发，沿逻辑查询中的关系路径扩展，补充缺失的答案路径，确保覆盖所有可能的答案实体。
- 最后，用修正后的知识路径帮助LLM（ChatGPT或GPT-4）进行联合答案预测。

### 公式或算法流程（文字说明）
1. 构建训练数据：对每个问题q，在KG中从话题实体eq到答案实体ea进行BFS，提取最短路径。
2. 微调LLM：最大化条件概率Pθ(Pk | q, eq)，使其学会生成知识路径Pk。
3. 推理时生成路径：Ppred = LLM_ft(q, eq)，束搜索保留多个路径。
4. 提取逻辑查询：LQ = eq → r1 → ? → r2 → ... → rn → ?。
5. 在KG上执行LQ，得到修正后的路径集合P_correction。
6. 将修正路径输入LLM进行答案预测（每条答案一行）。

## 3. 实验设计

### 数据集
- **WebQSP**：4037个问题，30.0%多跳，95.3%可解（存在路径）；训练2826，测试1628。
- **CWQ**（Complex WebQuestions）：34672个问题，42.1%多跳，80.1%可解；训练27639，测试3531。
- **知识图谱**：Freebase（两数据集共用）。实验中为每个问题提取局部知识子图。

### Benchmark与对比方法
- **传统KGQA方法**：GRAFT-NET、NSM、SR+NSM、NSM+h、UniKGQA。
- **LLM-based KGQA方法**：KD-CoT、StructGPT、KB-BINDER、ToG（+ChatGPT/+GPT-4）、KG-CoT、GoG、Interactive-KBQA、EffiQA、RoG（最相关语义解析方法）、GNN-RAG。
- 对比指标：Hit（正确回答是否在输出中）、Hit@1（最高候选是否正确）、F1综合评估。

## 4. 资源与算力

- **微调**：使用2张NVIDIA A100（80GB）GPU，微调Llama 3.1-8B-Instruct。
- **超参数**：batch size=4，学习率2e-5，warmup ratio=0.03，余弦学习率调度器，训练3个epoch。
- **推理**：调用OpenAI API使用ChatGPT和GPT-4进行答案预测。
- **论文未明确提及总训练时长**，但给出了GPU型号与数量。

## 5. 实验数量与充分性

- **主实验**：在两个数据集（WebQSP, CWQ）上的对比，覆盖Hit、Hit@1、F1指标，共报告了15种以上基线方法的结果。
- **消融实验**：
  - CoG vs. w/o decoding（直接检索2跳路径）、w/o correction（不进行路径修正）。结果显示两个组件均至关重要。
  - 将CoG作为知识检索器与其他检索器对比（ToG、RoG、GNN-RAG），统一用ChatGPT预测答案，突出路径质量提升。
- **进一步分析**：
  - 在WebQSP上计算Hit_question和Hit_answer，评估修正前后路径的答案覆盖率。
  - 改变束宽度（2~10），观察性能变化趋势。
  - 案例研究：展示幻觉实体和路径缺陷的具体示例及修正效果。
- **充分性评价**：实验设计较为充分，从整体性能、组件贡献、路径质量、超参数影响等多个角度验证，对比基线全面，消融实验合理，结论具有说服力。但未进行跨KG的泛化实验（仅使用Freebase），也未测试不同LLM基座（仅使用Llama 3.1-8B）。

## 6. 主要结论与发现

- CoG在WebQSP和CWQ上均取得**最优性能**，Hit分别达90.5%（GPT-4版）和70.3%，F1达78.0和60.8。
- 结构化知识解码（背诵任务+含中间实体生成）显著减少无效查询，优于仅生成关系路径的方法。
- 知识路径修正有效消除幻觉实体（提升Hit_question 2.8%）和弥补路径缺陷（提升Hit_answer 26.0%），是提高召回率和F1的关键。
- 作为检索器，CoG提供的知识路径质量优于ToG、RoG、GNN-RAG，且仅需一次KG交互，推理延迟低。

## 7. 优点

- **方法创新**：首次在语义解析中显式引入中间实体约束，结合“语言模型作为知识库”范式，让LLM在生成路径时“填空”，降低幻觉。
- **有效性**：消融实验清晰证明各组件贡献，知识修正可纠正两种典型错误（幻觉实体、路径缺陷）。
- **效率**：相比迭代式LLM agent方法，CoG只需一次KG查询，推理更快。
- **可解释性**：生成的知识路径可追溯，便于分析错误原因。
- **实用性强**：在复杂多跳问答上达到SOTA，且F1性能领先，说明在答案召回和噪声控制上均有优势。

## 8. 不足与局限

- **需要微调**：LLM必须针对特定KG模式（如Freebase的实体中间节点）进行微调，无法零样本迁移到其他KG（如Wikidata）。
- **知识图谱依赖**：假设KG提供了可用的局部子图；对于不可解问题（4.7%~19.8%）无法处理。
- **计算资源**：微调需8B参数模型及2×A100，对资源要求较高；推理依赖商业API（GPT-4），成本较高。
- **泛化性有限**：仅在Freebase上评估，未测试其他领域或更复杂的KG（如Wikidata中长路径、负采样等）。
- **束搜索代价**：增大束宽度可能引入噪声，需谨慎调参。
- **可解性问题**：实验保留了不可解问题，但对超出KG范围的问题，框架无法提供答案，这在实际应用中可能是个限制。

（完）

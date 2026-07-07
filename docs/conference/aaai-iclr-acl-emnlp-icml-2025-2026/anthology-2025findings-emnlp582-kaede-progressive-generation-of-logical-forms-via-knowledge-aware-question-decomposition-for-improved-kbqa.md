---
title: "KaeDe: Progressive Generation of Logical Forms via Knowledge-Aware Question Decomposition for Improved KBQA"
title_zh: KaeDe：通过知识感知问题分解逐步生成逻辑形式以改进KBQA
authors: "Ranran Bu, Jian Cao, Jianqi Gao, Shiyou Qian, Hongming Cai"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.582.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 基于问题分解的知识库问答
tldr: KaeDe针对基于语义解析的KBQA方法难以直接生成复杂图结构逻辑形式的问题，提出了一种先生成后检索的方法。该方法通过知识感知的问题分解逐步生成逻辑形式，提高了逻辑形式的可执行性和KBQA性能。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.582/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.582/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 742, \"height\": 829, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.582/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 406, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 925, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 1017, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 805, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 802, \"height\": 859, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 759, \"height\": 175, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 797, \"height\": 340, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 798, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 795, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1654, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.582/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 803, \"height\": 371, \"label\": \"Table\"}]"
motivation: 复杂图结构的逻辑形式直接生成困难且易失败。
method: 集成知识感知的问题分解和逐步逻辑形式生成，再检索候选。
result: 在标准KBQA基准上提升了准确率，尤其是复杂问题。
conclusion: 问题分解策略有效提升了KBQA对复杂结构的处理能力。
---

## Abstract
Knowledge base question answering (KBQA) refers to the task of answering natural language questions using large-scale structured knowledge bases (KBs). Existing semantic parsing-based (SP-based) methods achieve superior performance by directly converting questions into structured logical form (LF) queries using fine-tuned large language models (LLMs). However, these methods face the key challenge of difficulty in directly generating LFs for complex graph structures, which often leads to non-executable LFs that negatively impact overall KBQA performance. To address this challenge, we propose KaeDe, a novel generate-then-retrieve method for KBQA. This approach integrates knowledge-aware question decomposition and subsequent progressive LF generation within the generation phase, followed by an unsupervised retrieval phase. Specifically, the original question is decomposed into simplified, topic entity-centric sub-questions and explanations within the KB context. Path-level LFs are derived from these intermediate expressions and then combined into a comprehensive graph-level LF. Finally, the LF is refined through unsupervised entity and relation retrieval. Experimental results demonstrate that our method achieves state-of-the-art (SOTA) performance on WebQuestionSP (WebQSP) and ComplexWebQuestions (CWQ) benchmarks, particularly with fewer model parameters.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

*   **任务背景**：知识库问答（KBQA）旨在利用大规模结构化知识库回答自然语言问题。基于语义解析（SP）的方法通过微调大语言模型（LLM）直接将问题转换为结构化逻辑形式（LF），再执行查询获得答案。
*   **核心问题**：
    *   现有SP方法在生成复杂图结构的LF时存在困难，容易产生不可执行的LF，导致性能下降。
    *   当前主流方法分为“检索-生成”和“生成-检索”两类。前者依赖复杂的检索过程，引入额外计算开销和噪声；后者虽然减少了检索负担，但LLM在处理复杂问题时难以关注所有细节，尤其在小参数模型上更为明显。
    *   现有问题分解方法更关注原问题本身，缺乏知识库对齐，可能导致后续过程语义偏差。
*   **研究目标**：提出一种结合知识感知问题分解与逐步LF生成的“生成-检索”框架，降低复杂LF的生成难度，提高可执行性和整体性能，尤其在小参数模型上实现SOTA。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 核心思想
KaeDe（Knowledge-aware question Decomposition and progressive LF generation）将生成阶段分解为两个任务，再辅以无监督检索：
1. **知识感知问题分解**：基于KB上下文，将原问题分解为主题实体为中心的简单子问题和解释。
2. **逐步逻辑形式生成**：根据中间表达式生成路径级LF，再组装成完整的图级LF。
3. **无监督检索**：对生成的LF进行实体和关系检索，校正并执行。

### 关键技术细节
*   **数据准备**：对每个训练样本，从原始SPARQL查询中提取实体为中心的推理路径，将路径转换为路径级LF，并进一步组合为图级LF。同时，利用三元组语义规则将路径线性化为自然语言表达（子问题或解释），如“The r of e0 is e1”形式。
*   **指令微调**：使用LoRA（低秩适应）对LLM进行参数高效微调，使同一模型依次完成分解、路径生成和组装三个子任务。训练数据分为`Dd`（分解）、`Dg`（生成）、`Da`（组装）三部分。优化目标为最大化序列概率。
*   **逻辑形式生成**：微调后的LLM通过束搜索（beam search）依次生成候选分解表达式、候选路径级LF和候选图级LF。每个步骤的束搜索结果传递给下一步。
*   **无监督检索与执行**：
    *   实体检索：使用SimCSE计算预测实体与FACC1标注实体集的相似度，取top-k候选替换回LF，转换回SPARQL执行。
    *   关系检索：若实体检索后无可执行LF，则对关系进行类似检索，基于主题实体的邻接关系集。
    *   阈值和top-k限制候选数量。

### 算法流程（文字说明）
1. 给定原问题q，LLM生成一组候选分解表达式集合ˆX（每个ˆX包含对每个候选主题实体的子问题/解释）。
2. 对每个ˆX，LLM生成对应的路径级LF集合ˆℓ′。
3. 对每个ˆℓ，LLM组装成候选图级LF ˆL。
4. 对每个ˆL，先进行实体检索，将匹配实体替换后执行获取答案Ae；若Ae为空，再进行关系检索，替换关系后执行获取答案Ar。
5. 返回所有答案的并集。

## 3. 实验设计

### 数据集
*   **WebQSP（简单问题）**：4737个问题，稀疏跳数，单跳为主。
*   **ComplexWebQuestions (CWQ)（复杂问题）**：34,689个问题，多跳、多实体，包含合取、比较、最高级等类型。
*   两者均基于Freebase知识库。

### 基准方法
*   **IR-based**：NSM、Rigel、UniK-QA、UniKGQA（非LLM）；RoG、ToG、FiDeLis（LLM）。
*   **SP-based**：HGNet、TIARA、FC-KBQA（非LLM）；DecAF、ARG-KBQA、TFS-KBQA、ChatKBQA（LLM）。

### 评估指标
*   F1分数（答案覆盖度）、Hits@1（top-1准确率）。
*   Beam Match (BM)（检查生成束中是否包含标准LF）。

## 4. 资源与算力

*   **GPU**：单张NVIDIA A40 GPU。
*   **LLM主干**：Llama 2 7B（主要）、Llama 2 13B、DeepSeek 7B、DeepSeek R1 8B（对比验证）。
*   **训练时间**：
    *   WebQSP：约17小时（7B），31小时（13B）。
    *   CWQ：约18小时（7B），33小时（13B）。
*   **显存**：未明确说明，但LoRA有效降低了显存占用。

## 5. 实验数量与充分性

### 实验组数
1. **整体性能对比**：在WebQSP和CWQ上对比了10+种基线方法（包括非LLM和LLM变体）。
2. **模型与参数分析**：改变模型大小（7B vs 13B）、PEFT目标模块（仅q_proj,v_proj vs 所有线性层）、不同主干（Llama vs DeepSeek）。
3. **消融实验**：
    *   生成阶段：去掉分解、去掉分解+逐步生成（直接LF生成）。
    *   检索阶段：去掉oracle实体链接、去掉关系检索、去掉全部检索。
    *   综合：去掉全部生成+检索。
4. **超参数分析**：束大小（3,5,8）对Hits@1和F1的影响。
5. **案例分析**：给出了多个实体情况下的分解实例。
6. **效率分析**：对比直接LF生成与KaeDe的平均每问题运行时间。
7. **失败分析**：统计不同类型错误（实体、关系、跳数、约束、图结构、执行）的占比。

### 充分性评价
*   **覆盖度**：涵盖了主流水准、模型变体、关键组件、超参数敏感性、效率、错误类型，比较全面。
*   **公平性**：所有基线结果引用原作者或使用相同设备复现（ChatKBQA标注了复现），超参数设置合理（束大小、学习率等）。
*   **客观性**：消融实验清晰展示了各组件的贡献，失败分析揭示了主要瓶颈（关系错误71.18%，不可执行率42.61%）。

## 6. 主要结论与发现

1. **性能提升**：KaeDe在WebQSP上Hits@1达91.09%（超越ChatKBQA 5.73%），F1略低（-0.26%）；在CWQ上Hits@1 88.28%（+6.91%），F1 80.15%（+3.33%）。证明了方法在复杂问题上的优势。
2. **参数效率**：7B模型即可超过或媲美更大模型（13B）的性能，且在小模型上对复杂问题（多跳）提升更明显。
3. **分解与逐步生成的有效性**：消融实验表明，移除分解后Hits@1下降0.53%，BM下降0.64%；完全移除分解和逐步生成后Hits@1下降3.05%，BM下降5.05%。
4. **检索的贡献**：去掉检索后Hits@1和F1大幅下降（-8.13%和-7.29%），表明KB对LF的校准至关重要。
5. **束大小影响**：增大束大小提高Hits@1但可能降低F1（引入噪声），需平衡。
6. **错误分布**：关系错误（71.18%）是主要问题，但检索能有效修复，非可执行率降至42.61%。

## 7. 优点

*   **创新性**：首次将知识感知的问题分解与逐步LF生成结合，在生成阶段融入KB上下文，缩小语义鸿沟。
*   **方法设计**：分解任务使复杂LF生成简化为多个简单子任务，LLM可更专注，尤其适合小参数模型。
*   **效率与性能平衡**：先生成后检索策略避免了复杂检索开销，在7B模型上达到SOTA，降低了推理成本。
*   **实验全面**：包含充分消融、模型变体、超参数分析、效率和错误分析，结论可靠。
*   **代码开源**：提供GitHub代码，促进复现。

## 8. 不足与局限

*   **额外计算开销**：三次束搜索（分解、路径生成、组装）带来O(n³)复杂度，相比直接生成（O(n)）显著增加时间（约2-3倍），在束大小8时尤为明显。
*   **噪声问题**：束搜索和检索可能将非可执行LF错误校准为可执行但错误的LF，影响F1分数。
*   **数据集覆盖**：只测试了Freebase上的两个数据集（WebQSP、CWQ），未涉及其他知识库（如Wikidata）或领域，泛化性待验证。
*   **错误分析局限**：失败分析揭示关系错误为主，但未深入探究关系预测的具体原因（如长尾关系、语义歧义）。
*   **可解释性**：虽然分解提供了中间步骤，但最终回答的可解释性仍有限（类似黑盒生成）。
*   **实际部署成本**：尽管参数少，但三次束搜索的耗时可能不适用于实时场景。

（完）

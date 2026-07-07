---
title: "From Phrases to Subgraphs: Fine-Grained Semantic Parsing for Knowledge Graph Question Answering"
title_zh: 从短语到子图：知识图谱问答中的细粒度语义解析
authors: "Yurun Song, Xiangqing Shen, Rui Xia"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.272.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 细粒度语义解析用于知识图谱问答
tldr: 大语言模型给知识图谱问答带来机遇但存在语义偏离和推理噪声。本文提出细粒度语义解析框架FGSP，通过对历史问答对进行短语级分割构建映射库，实现更精确的图谱模式匹配。在复杂多跳推理任务上，FGSP显著提升了可扩展性和泛化能力，为结构化知识集成提供新思路。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.272/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 1078, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.272/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 794, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.272/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 665, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.272/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.272/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 741, \"height\": 429, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1254, \"height\": 829, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 611, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 613, \"height\": 639, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 733, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 660, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 159, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 688, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.272/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1652, \"height\": 377, \"label\": \"Table\"}]"
motivation: 现有语义解析在大规模复杂KGQA中缺乏泛化性。
method: 构建FGSP框架，利用短语级分割构建细粒度映射库以匹配子图模式。
result: 在多个KGQA基准上，FGSP实现更高的准确率和召回率。
conclusion: 短语级细粒度解析增强了语义解析在知识图谱问答中的实用性和鲁棒性。
---

## Abstract
The recent emergence of large language models (LLMs) has brought new opportunities to knowledge graph question answering (KGQA), but also introduces challenges such as semantic misalignment and reasoning noise. Semantic parsing (SP), previously a mainstream approach for KGQA, enables precise graph pattern matching by mapping natural language queries to executable logical forms. However, it faces limitations in scalability and generalization, especially when dealing with complex, multi-hop reasoning tasks.In this work, we propose a Fine-Grained Semantic Parsing (FGSP) framework for KGQA. Our framework constructs a fine-grained mapping library via phrase-level segmentation of historical question-logical form pairs, and performs online retrieval and fusion of relevant subgraph fragments to answer complex queries. This fine-grained, compositional approach ensures tighter semantic alignment between questions and knowledge graph structures, enhancing both interpretability and adaptability to diverse query types. Experimental results on two KGQA benchmarks demonstrate the effectiveness of FGSP, with a notable 18.5% relative F1 performance improvement over the SOTA on the complex multi-hop CWQ dataset. Our code is available at https://github.com/NUSTM/From-Phrases-to-Subgraphs.

---

## 论文详细总结（自动生成）

# 论文总结：From Phrases to Subgraphs: Fine-Grained Semantic Parsing for Knowledge Graph Question Answering

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：大语言模型（LLM）在知识图谱问答（KGQA）中面临两大挑战：一是LLM非结构化训练数据与KG结构化数据之间的**语义错位**，导致幻觉；二是LLM顺序推理范式在处理多跳问题时产生**冗余路径**，引入噪声积累。传统语义解析（SP）虽能精准匹配图模式，但在可扩展性和泛化性上受限，尤其面对复杂多跳问题时容易因未见模式而错误映射关系。
- **整体含义**：论文提出细粒度语义解析框架FGSP，通过将历史问答对分解为短语级映射，实现问题与KG结构的细粒度对齐，从而在保持精确性的同时增强对复杂查询的适应能力，为结构化知识集成提供新思路。

## 2. 方法论：核心思想与关键技术细节

- **核心思想**：将KGQA中的语义解析从“整个问题→整个逻辑形式”的粗粒度映射，降级为“子问题/短语→子图片段”的细粒度组合式匹配。采用两阶段架构：
  - **离线阶段**：
    1. **规则预处理SPARQL**：提取基本图模式（BGP），合并端点非实体的BGP成分，形成语义完整的推理片段。
    2. **LLM驱动的短语级分割**：利用GPT-4o等模型，基于预处理片段和原始问答对，通过双向对齐生成自然语言短语与SPARQL片段的配对。解决“过度聚合”（一个短语包含多步推理）和“过度碎片化”（语义不完整）问题。
  - **在线阶段**：
    1. **问题分解**：使用LLM（如GPT-4o）将复杂问题分解为无嵌套的子问题（例如“What currencies do countries bordering Germany use?” → “What countries border Germany?” + “What are the currencies used in a country?”）。
    2. **短语检索**：对每个子问题，通过稠密检索（如BGE-m3）从离线映射库中召回top-k最匹配的自然语言短语及其对应的SPARQL片段。
    3. **子图实例化与融合**：将检索到的SPARQL片段中的实体替换为当前问题的实体，实例化为子图；然后通过两种规则进行融合：
       - **顺序融合**（A→B→C）：前一个子图的结果作为后续子图的输入，形成推理路径。
       - **组合融合**（A+B→C）：多个子图同时施加约束，得到满足所有条件的子图。
- **关键技术细节**：SPARQL作为逻辑形式；LLM在分解和检索阶段不接触KG，仅在离线构建期间参与语义映射；融合过程基于规则，保证可解释性和确定性。

## 3. 实验设计

- **数据集**：
  - **WebQSP**：2,826训练/1,628测试，最多2跳；基于Freebase。
  - **CWQ**（Complex WebQuestions）：27,639训练/3,531测试，最多4跳；基于Freebase。
- **基准对比**：共14个基线，分为三类：
  - **LLM-only**：Llama3.1-8b、Qwen2-7B、ChatGPT、GPT-4。
  - **推理型（Inference-based）**：StructGPT、Readi、ToG、KG-CoT（均与KG交互）。
  - **训练型（Training-based）**：NSM、TransferNet、SR+NSM、UniKGQA、DECAF、RoG。
- **评估指标**：F1（整体覆盖率）和Hit（至少一个正确答案出现）。
- **实现细节**：GPT-4o作为基础和分割模型（温度0.4），BGE-m3作为检索嵌入模型，检索top-k=5；基线结果直接引用原论文。

## 4. 资源与算力

- 论文**未明确说明使用的GPU型号、数量及训练时长**。仅提及：
  - 离线构建和在线分解使用GPT4o（API调用，非本地训练）。
  - 稠密检索使用BGE-m3（可能是预训练模型）。
  - 框架本身不涉及大规模模型训练（仅需少量推理调用），因此算力需求较低。局限性部分提到依赖Freebase，但未提及训练硬件。

## 5. 实验数量与充分性

- **主要实验**：表1展示了FGSP与14个基线在WebQSP和CWQ上的F1/Hit对比，充分覆盖各类方法。
- **消融与分析实验**（Q1-Q6共六组）：
  - Top-k对性能的影响（图4左/右）。
  - 细粒度检索 vs 完整问题检索（图4）。
  - 短语库规模的影响（5%-100%曲线，图5）。
  - 不同LLM作为短语分割模型（GPT-4o vs 开源模型，表2）。
  - 不同LLM进行问题分解（表3）。
  - 不同检索方法（BM25 vs 多种稠密模型，表4）。
- **充分性评估**：
  - 实验设计较为全面，覆盖了框架各个组件的贡献。
  - 对比基线包含最强SOTA（RoG），且使用统一评估指标。
  - 但仅使用Freebase单一KG，未在Wikidata/DBpedia上验证泛化性（作者在局限中提及）。
  - 未提供统计显著性检验，部分差异可能来自随机性（但多次实验验证趋势）。

## 6. 主要结论与发现

- **性能提升显著**：在CWQ上F1达到66.6%，相对RoG提升18.5%；Hit达91.6%。WebQSP上F1 73.3%，Hit 88.4%。
- **细粒度检索优于完整问题检索**：在所有top-k设置下，短语级检索比整句检索F1平均高49.1%（CWQ），证明分解的必要性。
- **短语库规模效应**：性能随短语数量增加而提升，但在30%-100%区间增速放缓，出现饱和；即使仅有5%短语，F1仍维持58.2%，体现鲁棒性。
- **模型兼容性**：开源模型（Qwen-14B、LLaMA-8B）在短语分割上达到GPT-4o的95%以上性能；但参数<1.5B时因过度聚合/碎片化导致性能骤降。
- **问题分解关键**：去除分解模块后，CWQ上F1下降9.1%，Hit下降9.2%。
- **检索方法影响**：稠密检索（BGE-m3）远优于BM25；不同稠密模型间差异较小（6-7%）。

## 7. 优点

- **方法创新性**：首次将语义解析从“问题级”降为“短语级”，实现组合式细粒度对齐，兼具可解释性和灵活性。
- **解耦设计**：LLM在在线阶段不直接接触KG，避免语义错位；离线构建仅需少量LLM调用，成本低。
- **融合范式简洁有效**：基于规则（顺序+组合）的融合方式避免了LLM生成噪声，确保推理可靠性。
- **鲁棒性强**：在短语库稀疏、模型参数较小、不同检索方式下均保持相对稳定的性能，适合实际低资源场景。
- **实验分析深入**：六组消融实验细粒度探讨了各个组件的影响，结论具有说服力。

## 8. 不足与局限

- **依赖特定KG**：仅基于Freebase验证，未评估在Wikidata、DBpedia等其他KG上的迁移性，可能受实体分布和schema差异影响。
- **规则替换粗糙**：子图实例化采用规则性实体替换，可能引入不准确匹配（如实体歧义），作者承认可通过生成式模型改进。
- **逻辑形式单一**：仅使用SPARQL，未探索S-expression、lambda-DCS等其他LF格式，通用性有待验证。
- **缺少完整训练开销说明**：未报告GPU资源、训练时间等，复现成本不透明。
- **未进行跨场景验证**：仅限KGQA任务，是否能推广到表格QA、文本到SQL等仍需探索。
- **分割依赖LLM能力**：当分解模型参数极低时（<1.5B），短语质量严重下降，说明存在模型能力瓶颈。

（完）

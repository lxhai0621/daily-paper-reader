---
title: Automated Knowledge Graph Construction for CAR T Cell Receptor Design via Hybrid Text Mining
title_zh: 基于混合文本挖掘的 CAR T 细胞受体设计自动化知识图谱构建
authors: "Luo, H., Tang, D., Zivanov, A., Miskov-Zivanov, N."
date: 2026-04-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.06.716719v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 从文献中自动构建知识图谱的工作流
tldr: 本研究针对CAR T细胞受体设计中缺乏系统性信号转导知识的问题，开发了一种结合REACH、INDRA和Llama 3的大模型自动化工作流。通过对PubMed文献进行混合文本挖掘，构建了一个包含约7500条相互作用和1800个实体的知识图谱。该工具为预测T细胞表型和筛选CAR胞内结构域提供了结构化基础，助力免疫治疗研究。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-001.webp\", \"caption\": \"Table 2. The top 10 cell types most often found in interactions extracted from the retrieved paper corpora and the number of interactions that include them for each corpus.\", \"page\": 6, \"index\": 1, \"width\": 760, \"height\": 350}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-002.webp\", \"caption\": \"Figure 1. Pipeline for automatically extracting interaction from published literature for the biomolecular interaction knowledge base.\", \"page\": 2, \"index\": 2, \"width\": 979, \"height\": 298}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-003.webp\", \"caption\": \"Figure 5. The workflow of collecting interactions for the knowledge graph from all 15 paper corpora, by combining outputs from INDRA, REACH and Llama 3, and filtering with FLUTE, with the number of interactions in each step.\", \"page\": 7, \"index\": 3, \"width\": 1031, \"height\": 336}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-004.webp\", \"caption\": \"Table 3. Top 10 DCs found in the generated knowledge graph.\", \"page\": 7, \"index\": 4, \"width\": 466, \"height\": 408}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-005.webp\", \"caption\": \"Figure 2. All terms used for creating queries(left) and an outline of the process for creating final 15 queries (right). Terms within the same group are combined with operator “or” and different groups are connected with operator “and”. DCs are the candidates considered for intracellular receptor domains. Process markers (PMs) are biomarkers of the biological process (BPs) of interest for CAR T cells.\", \"page\": 3, \"index\": 5, \"width\": 1038, \"height\": 363}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-006.webp\", \"caption\": \"Figure 6. Principal Component Analysis of the Node2Vec embedding of the created CAR T cell literature-based knowledge graph. The grey dots are all graph nodes, while the colored and labeled nodes are DCs.\", \"page\": 8, \"index\": 6, \"width\": 727, \"height\": 438}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-007.webp\", \"caption\": \"Figure 3. The prompt for the few-shot learning approach used for Llama 3.\", \"page\": 4, \"index\": 7, \"width\": 1031, \"height\": 427}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-008.webp\", \"caption\": \"Figure 4. Papers retrieved with the 15 search queries, for the three contexts, CAR T cell, T cell, and None, and the five combinations of terms, CD only, CD+PM, CD+PM+BP, PM only, PM+BP. a) Total papers retrieved from PubMed and the cutoff for machine reader processing (line); b) % papers from the top 2000 retrieved from PubMed in which REACH (left) and INDRA (right) found at least one interaction.\", \"page\": 5, \"index\": 8, \"width\": 1029, \"height\": 236}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-06-716719-v1/fig-009.webp\", \"caption\": \"Table 1. Summary of found interactions for each query.\", \"page\": 5, \"index\": 9, \"width\": 704, \"height\": 460}]"
motivation: 现有的CAR T细胞设计缺乏对胞内信号转导结构域及其生物学效应的系统性知识资源支持。
method: 整合REACH、INDRA和Llama 3等工具，通过15个针对性查询从PubMed文献中提取生物分子相互作用并构建知识图谱。
result: 构建了包含约7500个相互作用和1800个实体的多关系图谱，并证明引入生物过程本体术语可显著提升文献检索效率。
conclusion: 该自动化工作流为CAR T细胞表型预测和胞内结构域筛选提供了结构化基础，具有广泛的免疫治疗研究应用前景。
---

## 摘要
设计下一代嵌合抗原受体（CARs）需要对胞内信号转导结构域及其下游生物学效应有系统的理解，但目前尚不存在用于此目的的全面知识资源。在此，我们提出了一种自动化工作流，该工作流集成了多种自然语言处理和大型语言模型工具，从 PubMed 文献中提取生物分子相互作用，并将其组装成 CAR T 细胞信号转导知识图谱。我们的流水线在 15 个针对性搜索查询中结合了 REACH、INDRA 和 Llama 3，生成了一个包含约 1,800 个实体（包括蛋白质、生物过程和化学物质）之间约 7,500 种独特相互作用的有向多关系图。我们进一步证明，包含生物过程本体术语的查询比仅包含蛋白质名称的搜索能检索到更多包含丰富相互作用的论文，为未来的文献挖掘工作提供了实践指导。由此产生的知识库为预测 T 细胞表型和优先筛选用于 CAR 设计的胞内结构域候选物提供了结构化基础，在免疫治疗研究的知识驱动推理中具有更广泛的适用性。

## Abstract
Designing next-generation Chimeric Antigen Receptors (CARs) requires a systematic understanding of intracellular signaling domains and their downstream biological effects, yet no comprehensive knowledge resource currently exists for this purpose. Here, we present an automated workflow that integrates multiple natural language processing and large language model tools to extract biomolecular interactions from PubMed literature and assemble them into a CAR T cell signaling knowledge graph. Our pipeline combines REACH, INDRA, and Llama 3 across 15 targeted search queries, yielding a directed multi-relational graph of ~7,500 unique interactions among ~1,800 entities, including proteins, biological processes, and chemicals. We further demonstrate that queries incorporating biological process ontology terms retrieve more interaction-rich papers than protein-name-only searches, offering practical guidance for future literature mining efforts. The resulting knowledge base provides a structured foundation for predicting T cell phenotypes and prioritizing intracellular domain candidates for CAR design, with broader applicability to knowledge-driven inference in immunotherapy research.

---

## 论文详细总结（自动生成）

这篇论文介绍了一种名为“基于混合文本挖掘的 CAR T 细胞受体设计自动化知识图谱构建”的研究。以下是对该论文的详细总结：

### 1. 核心问题与背景（研究动机）
*   **核心问题**：嵌合抗原受体（CAR）T 细胞疗法在癌症治疗中表现出色，但设计高效的 CAR 分子（尤其是胞内信号转导结构域）面临巨大挑战。目前缺乏一个系统性的、结构化的知识库来描述不同信号结构域如何影响下游生物学效应（如细胞耗竭、记忆表型等）。
*   **研究动机**：生物医学文献海量且增长迅速，人工提取相关信号通路信息效率极低。因此，需要一种自动化的工具，从现有文献中提取生物分子相互作用，构建专门针对 CAR T 细胞设计的知识图谱（Knowledge Graph, KG），以支持数据驱动的受体设计和表型预测。

### 2. 方法论：核心思想与技术细节
该研究提出了一套整合传统自然语言处理（NLP）工具与大语言模型（LLM）的自动化工作流：
*   **混合提取策略**：
    *   **REACH & INDRA**：使用传统的生物医学自然语言处理工具（REACH）和集成平台（INDRA）来提取具有高置信度的标准化生物分子相互作用。
    *   **Llama 3 (LLM)**：利用 Llama 3 模型通过 Few-shot（少样本）提示词工程，提取传统工具可能遗漏的复杂上下文关系或非标准描述。
*   **查询策略设计**：设计了 15 种不同的 PubMed 搜索查询组合，涵盖了胞内结构域（CD）、过程标记物（PM）和生物过程（BP）术语，并设置了三种上下文（CAR T 细胞、T 细胞、无特定上下文）。
*   **自动化流水线**：
    1.  **文献检索**：根据 15 个查询从 PubMed 获取相关论文。
    2.  **文本挖掘**：并行运行 REACH、INDRA 和 Llama 3 提取实体间的相互作用（如“A 激活 B”）。
    3.  **过滤与整合**：使用 FLUTE 等工具对提取结果进行过滤，去除冗余和低质量信息。
    4.  **图谱构建**：将提取的实体（蛋白质、化学物质、生物过程）和关系组装成有向多关系图。

### 3. 实验设计
*   **数据集**：直接使用 PubMed 数据库作为原始语料来源。
*   **实验场景**：通过 15 组不同的查询策略（如“CD 仅限”、“CD+PM”、“CD+PM+BP”等）来测试文献检索的效率和提取相互作用的丰富度。
*   **评估方法**：
    *   对比了不同查询策略下检索到的论文数量及包含相互作用的论文比例。
    *   使用 **Node2Vec** 算法对构建的知识图谱进行嵌入（Embedding），并通过主成分分析（PCA）可视化，验证图谱中实体的聚类特征和生物学合理性。

### 4. 资源与算力
*   **模型使用**：明确提到了使用 **Llama 3** 作为 LLM 提取器。
*   **算力说明**：论文**未明确说明**具体的 GPU 型号、数量或训练/推理的总时长。通常此类工作涉及对数千篇论文摘要或全文的推理，需要中大型 GPU 集群支持。

### 5. 实验数量与充分性
*   **实验规模**：研究分析了 15 个不同的文献语料库，涵盖了从数百到数千篇不等的论文。
*   **充分性评价**：实验设计较为充分。作者不仅对比了不同工具（REACH vs INDRA vs Llama 3）的提取效果，还深入探讨了搜索词组合（如加入本体术语 BP）对结果质量的影响。通过 PCA 可视化证明了图谱在捕捉生物学相关性方面的有效性。

### 6. 主要结论与发现
*   **图谱规模**：成功构建了一个包含约 **7,500 条独特相互作用**和 **1,800 个实体**（蛋白质、生物过程、化学物质）的 CAR T 信号转导知识图谱。
*   **查询优化**：发现包含“生物过程（BP）”本体术语的查询比仅使用蛋白质名称的查询能检索到更多高质量、富含相互作用的论文。
*   **混合优势**：LLM（Llama 3）能够补充传统 NLP 工具无法识别的复杂关系，显著提高了知识图谱的完整性。
*   **生物学发现**：图谱能够清晰地展示不同胞内结构域（如 CD28, 4-1BB）与特定信号通路及 T 细胞表型之间的关联。

### 7. 优点
*   **自动化程度高**：实现了从文献检索到图谱构建的全流程自动化，极大降低了人工成本。
*   **混合架构**：结合了传统 NLP 的严谨性和 LLM 的灵活性，平衡了提取的准确率与召回率。
*   **实用性强**：直接针对 CAR T 细胞设计这一前沿领域，生成的知识图谱可直接用于下游的计算建模和实验指导。

### 8. 不足与局限
*   **幻觉风险**：尽管使用了过滤机制，但 LLM（Llama 3）仍可能产生错误的相互作用提取（幻觉问题），需要更严格的验证。
*   **数据源限制**：主要依赖 PubMed，可能遗漏了专利、会议论文或其他非公开的实验数据。
*   **动态更新**：论文未详细讨论图谱如何随新文献的发布进行实时动态更新。
*   **偏差风险**：文献本身存在发表偏倚（Positive Bias），图谱可能会过度强化已知的热门研究路径，而忽略新兴或负面的实验结果。

（完）

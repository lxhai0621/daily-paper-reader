---
title: "CROssBARv2: A Unified Computational Framework for Heterogeneous Biomedical Data Representation and LLM-Driven Exploration"
title_zh: CROssBARv2：一种用于异构生物医学数据表示和 LLM 驱动探索的统一计算框架
authors: "Sen, B., Ulusoy, E., Darcan, M., Ergun, M., Lobentanzer, S., Rifaioglu, A. S., Turei, D., Saez-Rodriguez, J., Dogan, T."
date: 2026-04-15
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.12.718028v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 自动化知识发现与集成平台
tldr: CROssBARv2是一个统一的生物医学数据集成平台，旨在解决数据碎片化问题。它通过构建包含本体、元数据和向量嵌入的大规模知识图谱，整合了异构生物医学资源。该平台集成了CROssBAR-LLM，利用知识图谱增强大模型，提供准确的问答和语义搜索。它支持药物重定位和蛋白质功能预测等任务，为生物医学发现和转化研究提供了可扩展、AI就绪且用户友好的基础框架。
source: biorxiv
selection_source: fresh_fetch
motivation: 针对生物医学数据存储分散、模态单一且元数据不均导致的集成分析与重现性难题。
method: 构建一个富含来源信息的知识图谱，结合标准化本体、向量嵌入及基于知识图谱增强的LLM问答系统。
result: 通过多案例分析、生物医学问答基准测试及蛋白质功能预测实验，验证了系统的生物学一致性和预测效能。
conclusion: CROssBARv2为假设生成和知识发现提供了可扩展的AI驱动基础，有效提升了生物医学研究的效率。
---

## 摘要
生物医学发现受到碎片化、特定模态的存储库和不均匀元数据的阻碍，限制了综合分析、可访问性和可重复性。为了应对这些挑战，我们提出了 CROssBARv2，这是一个具有丰富溯源信息的生物医学数据与知识集成平台，它将异构来源统一到一个可维护、可扩展的系统中。通过将多种数据类型整合到广泛的知识图谱中，并辅以标准化的本体、丰富的元数据和基于深度学习的向量嵌入，CROssBARv2 减轻了研究人员在多个孤立数据库中检索的需求，并能促进包括预测建模和机制推理在内的下游任务，从而支持药物重定位和蛋白质功能预测等应用。该平台通过 CROssBAR-LLM 提供交互式图谱探索和基于嵌入的语义搜索，CROssBAR-LLM 是一个直观的自然语言问答系统，它将大语言模型（LLM）的输出锚定在底层知识图谱中，以减轻幻觉。我们通过以下方式评估了 CROssBARv2：(i) 多个用例分析以测试生物学一致性和关系有效性；(ii) 知识增强的生物医学问答基准测试，将 CROssBAR-LLM 与通用 LLM 进行比较；以及 (iii) 利用 CROssBARv2 的异构结构进行蛋白质功能预测的深度学习预测建模实验。总之，CROssBARv2 提供了一个可扩展、AI 就绪且用户友好的基础，促进了假设生成、知识发现和转化研究。

## Abstract
Biomedical discovery is hindered by fragmented, modality-specific repositories and uneven metadata, limiting integrative analysis, accessibility, and reproducibility. To address these challenges, we present CROssBARv2, a provenance-rich biomedical data-and-knowledge integration platform that unifies heterogeneous sources into a maintainable, scalable system. By consolidating diverse data types into an extensive knowledge graph enriched with standardised ontologies, rich metadata, and deep learning-based vector embeddings, CROssBARv2 alleviates the need for researchers to navigate multiple siloed databases and can facilitate downstream tasks, including predictive modelling and mechanistic reasoning, enabling applications such as drug repurposing and protein function prediction. The platform offers interactive graph exploration and embedding-based semantic search with CROssBAR-LLM, an intuitive natural language question-answering system that grounds large language model (LLM) outputs in the underlying knowledge graph to mitigate hallucinations. We assess CROssBARv2 through (i) multiple use-case analyses to test biological coherence and relational validity; (ii) knowledge-augmented biomedical question-answering benchmarks comparing CROssBAR-LLM against generalist LLMs; and (iii) a deep learning-based predictive modelling experiment for protein function prediction leveraging the heterogeneous structure of CROssBARv2. Collectively, CROssBARv2 provides a scalable, AI-ready, and user-friendly foundation that facilitates hypothesis generation, knowledge discovery, and translational research.

---

## 论文详细总结（自动生成）

这篇论文介绍了 **CROssBARv2**，一个旨在解决生物医学数据碎片化、提高数据可解释性并利用大语言模型（LLM）驱动知识探索的统一计算框架。以下是对该论文的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：生物医学数据散落在各个孤立的存储库中，缺乏统一的元数据标准，导致集成分析困难。此外，现有的知识图谱（KG）通常缺乏溯源信息，且对非编程背景的研究人员不友好。
*   **研究动机**：通用大语言模型（LLM）在处理专业生物医学问题时容易产生“幻觉”。研究团队希望通过构建一个富含元数据、可自动更新的异构知识图谱，并将其与 LLM 结合，实现准确、可追溯的生物医学知识发现。

### 2. 方法论：核心思想与关键技术
*   **核心思想**：构建一个“AI 就绪”的异构知识图谱，通过混合搜索（图遍历 + 向量相似度）和自然语言接口（Text-to-Cypher）连接结构化知识与生成式 AI。
*   **关键技术细节**：
    *   **数据集成**：利用 `BioCypher` 框架和自定义适配器脚本，整合了 34 个数据源，涵盖 14 种节点类型（如蛋白质、药物、疾病、基因等）和 51 种边缘类型。
    *   **知识表示**：引入了丰富的元数据（证据代码、置信度分数、来源），并为节点集成了多种深度学习嵌入（如蛋白质的 ESM2/ProtT5、化合物的 SELFormer、基因的 Nucleotide Transformer）。
    *   **CROssBAR-LLM**：采用 Text-to-Cypher 技术，将用户的自然语言问题转化为 Neo4j 数据库查询语句，执行后将结构化结果反馈给 LLM 生成最终回答。
    *   **混合搜索**：结合了基于图结构的路径查询和基于向量索引的语义相似度搜索，能够发现图中未直接连接但功能相似的实体。

### 3. 实验设计
*   **实验场景与数据集**：
    1.  **生物学有效性验证**：使用 `metapath2vec` 算法在蛋白质家族、药物-疾病关联和通路同义性上进行聚类分析。
    2.  **LLM 基准测试**：
        *   **Cypher 生成**：50 个手动构建的复杂查询。
        *   **生物医学问答**：100 个内部真假题和 50 个来自 `GeneTuring` 的外部基准题。
    3.  **预测建模**：在 `DeepHGAT` 人类数据集上进行蛋白质功能预测（GO 条目预测）。
*   **对比方法**：
    *   **LLM 对比**：GPT-4o, Claude 3.5 Sonnet, Llama 3.1, DeepSeek R1, Gemini 1.5 Pro 等。
    *   **预测模型对比**：与 DeepHGAT, PSPGO 等 SOTA（当前最佳）模型对比。

### 4. 资源与算力
*   **算力说明**：论文中**未明确说明**构建整个知识图谱和训练 ProtHGT 模型所使用的具体 GPU 型号、数量或总训练时长。
*   **部署环境**：提到系统部署在基于 Docker 容器化的虚拟专用服务器（VPS）上，使用 Traefik 进行反向代理和负载均衡。

### 5. 实验数量与充分性
*   **实验规模**：
    *   涵盖了从基础的图结构验证到复杂的 LLM 问答，再到下游的深度学习预测任务。
    *   使用了 34 个主流生物医学数据库，数据量达 270 万节点和 1260 万条边。
*   **充分性与公平性**：实验设计较为全面，既有定量的指标（Fmax, HR@K, 准确率），也有定性的案例分析（如 *de novo* 分子机制推导）。通过引入外部基准（GeneTuring）和时间切片验证（蛋白质功能预测），保证了评估的客观性。

### 6. 主要结论与发现
*   **知识增强显著**：将 LLM 与 CROssBARv2 结合后，在生物医学问答上的表现远超通用 LLM（如 Gemini 1.5 Pro 的准确率从随机水平提升至 98%）。
*   **预测性能领先**：基于该图谱训练的 `ProtHGT` 模型在蛋白质功能预测任务中达到了 SOTA 水平，证明了异构图结构对特征学习的价值。
*   **混合搜索的威力**：通过向量相似度，系统能够成功识别出数据库中不存在的新型（*de novo*）小分子的潜在治疗机制。

### 7. 优点（亮点）
*   **溯源性强**：每个节点和边缘都带有详细的来源和置信度元数据，有效解决了生物医学数据质量参差不齐的问题。
*   **用户友好**：提供了 GraphQL API、Neo4j 浏览器和 LLM 问答三种交互方式，兼顾了开发者和实验生物学家的需求。
*   **自动化维护**：通过适配器脚本实现了数据的定期更新和可扩展性。

### 8. 不足与局限
*   **标识符映射挑战**：不同数据库间的标识符（ID）交叉引用不完整或不一致，可能导致部分数据在集成时丢失。
*   **疾病粒度问题**：不同疾病本体（如 Mondo, KEGG Disease）的分类粒度差异较大，影响了跨数据库的推理精度。
*   **LLM 依赖性**：Text-to-Cypher 的准确性高度依赖于底层 LLM 的逻辑推理能力，对于极其复杂的嵌套查询，小型模型仍可能失败。
*   **算力细节缺失**：缺乏模型训练的资源消耗说明，不利于其他研究者评估复现成本。

（完）

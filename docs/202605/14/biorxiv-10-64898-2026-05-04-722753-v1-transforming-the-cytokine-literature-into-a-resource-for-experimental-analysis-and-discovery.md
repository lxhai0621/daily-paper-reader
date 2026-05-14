---
title: Transforming the cytokine literature into a resource for experimental analysis and discovery
title_zh: 将细胞因子文献转化为实验分析与发现的资源
authors: "Oesinghaus, L., Park, M., Shao, R., Koh, P. W., Seelig, G."
date: 2026-05-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.04.722753v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 从细胞因子文献中自动发现知识
tldr: 针对细胞因子生物学文献分散、难以系统利用的问题，本研究开发了CytED框架。该框架利用大语言模型从11万篇全文中提取了超过100万条“细胞因子-细胞类型-效应”三元组，实现了实验数据与文献知识的大规模对接。CytED能定量比较实验观测与既往研究，揭示了IL-10刺激下的新特征，为细胞因子研究提供了强大的分析工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 细胞因子生物学知识分散在海量文献中，导致在解释新实验结果时难以进行系统性的文献比对和利用。
method: 开发了CytED框架，利用多步LLM流水线从11万篇全文文献中提取并标注了超过百万条结构化的细胞因子效应三元组。
result: 成功识别了IL-10刺激下单核细胞的促炎特征及CD8+ T细胞在体内外的细胞毒性差异，并能区分原发与继发效应。
conclusion: CytED建立了一种将非结构化领域文献转化为分析工具的新范式，有效桥接了文献知识与实验发现。
---

## 摘要
细胞因子生物学知识分散在数十万篇出版物中，这使得在解释新实验时难以进行系统性利用。大语言模型（LLMs）可以辅助针对性的文献解读，但随机检索仍不完整且不可靠。我们提出了细胞因子效应数据库（CytED），这是一个用于大规模连接用户提供的实验数据集与文献知识的框架。CytED 利用多步 LLM 流水线从 11 万篇全文出版物中生成了超过一百万个“细胞因子-细胞类型-效应”三元组，并附带实验背景以及基因、通路和细胞过程方向性变化的注释。这种结构实现了观察到的扰动响应与跨细胞因子、细胞类型和实验背景的既有文献之间的定量比较。应用于外周血单核细胞（PBMCs）的体外 IL-10 刺激时，CytED 识别出单核细胞中意想不到的促炎特征，以及 CD8+ T 细胞细胞毒性反应中系统的体内-体外差异。CytED 能够推断细胞因子信号传导，区分原发性与继发性细胞因子效应，并指导组合扰动筛选的设计。总之，CytED 建立了一种将非结构化领域文献转化为连接文献与实验的分析工具的通用范式。

## Abstract
Cytokine biology is dispersed across hundreds of thousands of publications, making it difficult to use systematically when interpreting new experiments. Large language models (LLMs) can assist with focused literature interpretation, but ad hoc retrieval remains incomplete and unreliable. We present the Cytokine Effect Database (CytED), a framework for interfacing user-supplied experimental datasets with literature knowledge at scale. CytED uses a multi-step LLM pipeline to generate over a million cytokine-cell type-effect triples from 110,000 full-text publications, with annotations for experimental context and directional changes in genes, pathways, and cellular processes. This structure enables quantitative comparison between observed perturbation responses and prior literature across cytokines, cell types, and experimental contexts. Applied to in vitro IL-10 stimulation of PBMCs, CytED identifies unexpected pro-inflammatory features in monocytes and systematic in vivo-in vitro differences in cytotoxicity responses in CD8+ T cells. CytED infers cytokine signaling, distinguishes primary from secondary cytokine effects, and guides the design of combinatorial perturbation screens. Together, CytED establishes a general paradigm for converting unstructured domain literature into analytical tools that bridge literature and experiment.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **CytED（Cytokine Effect Database，细胞因子效应数据库）** 的框架，旨在解决免疫学领域中细胞因子研究知识碎片化的问题。以下是对该论文的深度结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：细胞因子生物学知识海量且分散在数十万篇学术论文中。研究人员在面对新的实验数据（如单细胞测序结果）时，很难系统性地将其与既往文献进行对比，导致解释新发现的过程效率低下且容易产生偏差。
*   **整体含义**：该研究试图打破“非结构化文献”与“结构化实验数据”之间的壁垒。通过构建 CytED，研究者可以将海量文本转化为可计算的知识库，从而实现实验观测结果与全球文献知识的定量对齐。

### 2. 论文提出的方法论
*   **核心思想**：利用大语言模型（LLM）构建多步自动化流水线，从海量全文文献中提取结构化知识，并将其转化为可用于统计分析的“三元组”形式。
*   **关键技术细节**：
    *   **多步 LLM 流水线**：从 11 万篇全文文献中识别并提取信息。
    *   **结构化三元组**：提取“细胞因子-细胞类型-效应（Cytokine-Cell Type-Effect）”三元组。
    *   **多维度标注**：不仅提取基因变化，还标注了实验背景（如物种、组织）、通路方向性变化以及细胞过程。
    *   **定量比较框架**：开发了一套算法，允许用户输入自己的实验扰动响应数据，并与 CytED 中的文献记录进行统计学上的定量比对。

### 3. 实验设计
*   **数据集与场景**：
    *   **文献数据集**：涵盖 11 万篇生物医学全文。
    *   **实验验证场景**：对外周血单核细胞（PBMCs）进行体外 IL-10 刺激实验。
*   **Benchmark 与对比**：
    *   对比了 CytED 提取的知识与传统的人工检索/随机检索结果。
    *   对比了 IL-10 在不同细胞类型（单核细胞 vs CD8+ T 细胞）中的表现。
    *   对比了体内（in vivo）与体外（in vitro）实验环境下细胞因子效应的差异。

### 4. 资源与算力
*   **算力说明**：论文摘要和元数据中**未明确说明**具体的 GPU 型号、数量或训练时长。但考虑到处理 11 万篇全文并运行多步 LLM 流水线，该项目通常需要大规模的云计算资源或高性能计算集群支持。

### 5. 实验数量与充分性
*   **实验规模**：
    *   **数据规模**：提取了超过 100 万条结构化三元组，规模巨大。
    *   **验证案例**：通过 IL-10 刺激实验、CD8+ T 细胞毒性分析、原发/继发效应区分以及组合扰动筛选设计等多个案例进行了验证。
*   **充分性评价**：实验设计较为充分，不仅涵盖了大规模的数据提取，还通过具体的生物学实验验证了工具的实用性，能够揭示传统方法难以发现的细微生物学特征（如 IL-10 的促炎特性）。

### 6. 论文的主要结论与发现
*   **IL-10 的新特征**：CytED 识别出 IL-10 在单核细胞中具有意想不到的促炎特征，挑战了其作为纯抗炎因子的传统认知。
*   **环境差异性**：揭示了 CD8+ T 细胞在体内和体外环境下对细胞因子反应的系统性差异。
*   **功能扩展**：CytED 能够有效区分细胞因子的直接（原发）效应和间接（继发）效应，并能辅助设计复杂的组合药物/因子筛选实验。

### 7. 优点
*   **规模化与结构化**：将极度分散的非结构化文本转化为百万量级的结构化数据库，实现了知识的“量化”。
*   **桥接能力强**：直接打通了“文献检索”与“实验数据分析”两个原本孤立的环节。
*   **发现能力**：通过大规模数据对比，能够纠正或补充人类研究者对特定细胞因子（如 IL-10）的片面认知。

### 8. 不足与局限
*   **LLM 幻觉风险**：尽管采用了多步流水线，但 LLM 在提取复杂生物学逻辑时仍可能存在误读或幻觉。
*   **文献覆盖偏差**：系统依赖于全文获取权限，可能存在出版物偏倚（Publication Bias），即研究较少的细胞因子在数据库中信息匮乏。
*   **动态更新挑战**：生物医学文献增长极快，如何保持数据库的实时更新并确保存量数据的准确性是一个长期挑战。

（完）

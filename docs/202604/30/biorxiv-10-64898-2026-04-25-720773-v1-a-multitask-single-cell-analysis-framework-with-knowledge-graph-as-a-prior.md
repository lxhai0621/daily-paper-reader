---
title: A multitask single-cell analysis framework with knowledge graph as a prior
title_zh: 以知识图谱为先验的多任务单细胞分析框架
authors: "Mathew, B., Ganguly, R., Maity, A., Halder, A., Sabu, J. T., Gupta, N., Peela, S. C. M., Samanta, S., Kumari, S., Bhattacharjee, N., Joshi, S., Gupta, S., Ahuja, G., Farooq, M., Majumdar, A., Hasan, S., Sengupta, D."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.25.720773v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.5
evidence: 将异构知识图谱直接嵌入到分解框架中
tldr: 本研究针对单细胞RNA测序分析中各项任务相互孤立的问题，提出了scKNIFE框架。该框架利用图正则化非负矩阵分解，将包含超过50万条边的异构知识图谱作为先验知识嵌入模型，实现了对单细胞表达谱重建与多种生物实体活性的联合推断。在癌症数据集上的实验证明，scKNIFE在细胞聚类、注释及代谢程序识别方面表现优异，为癌症转录组学提供了一个模块化且可扩展的端到端解释工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的单细胞分析流程通常将聚类、注释和代谢推断等任务视为独立过程，缺乏统一的生物学先验整合。
method: 提出scKNIFE框架，通过将大规模异构知识图谱嵌入图正则化非负矩阵分解模型，实现多任务联合推断。
result: 在多个癌症数据集中，该方法在细胞聚类和注释上达到领先水平，并能准确识别与治疗反应相关的代谢程序。
conclusion: scKNIFE是一个功能强大且可扩展的单细胞分析工具，能够通过统一的潜在表示实现对复杂生物学功能的深度解读。
---

## 摘要
单细胞RNA测序通过揭示肿瘤微环境的细胞和分子多样性重塑了癌症生物学，但大多数分析流程仍将聚类、注释、通路评分、代谢推断和细胞间通讯视为独立的任务。在此，我们提出了scKNIFE（基于知识图谱的非负矩阵分解用于功能实体推断），这是一个统一的图正则化非负矩阵分解框架，可联合重建单细胞表达谱并推断多种生物实体的活性，包括通路、细胞类型标志物、代谢反应和任务、配体-受体相互作用以及细胞状态程序。通过将异构知识图谱直接嵌入到分解目标中，scKNIFE通过拉普拉斯正则化在生物相关实体之间传播信息，同时稀疏性约束保留了可解释性。集成的先验图包含47,274个节点和506,620条边，由Gene Ontology、Reactome、Hallmark基因集、Human-GEM、CellChat、PanglaoDB、Cytopus和源自Tabula Muris的注释等互补资源组装而成。在多个以癌症为重点的单细胞数据集中，scKNIFE在聚类和细胞类型注释方面表现出具有竞争力甚至领先的性能，同时还能恢复与专门的代谢研究方法一致并能捕捉治疗反应相关状态的生物学一致代谢程序。此外，该框架支持从单一潜在表示中进行下游细胞类型特异性生物活性的推断。总之，这些结果确立了scKNIFE作为一个模块化且可扩展的框架，用于单细胞癌症转录组学的端到端生物学解释。

## Abstract
Single-cell RNA sequencing has reshaped cancer biology by revealing the cellular and molecular diversity of the tumor microenvironment, yet most analysis pipelines still treat clustering, annotation, pathway scoring, metabolic inference, and cell-cell communication as separate tasks. Here, we present scKNIFE (Knowledge graph-based NMF for Inference of Functional Entities), a unified graph-regularized non-negative matrix factorization framework that jointly reconstructs single cell expression profiles and infers activities of diverse biological entities, including pathways, cell-type markers, metabolic reactions and tasks, ligand-receptor interactions, and cell-state programs. By embedding a heterogeneous knowledge graph directly into the factorization objective, scKNIFE propagates information between biologically related entities through Laplacian regularization while sparsity constraints preserve interpretability. The integrated prior graph spans 47,274 nodes and 506,620 edges, assembled from complementary resources including Gene Ontology, Reactome, Hallmark gene sets, Human-GEM, CellChat, PanglaoDB, Cytopus, and Tabula Muris-derived annotations. Across multiple cancer-focused single-cell datasets, scKNIFE yields competitive to leading performance for clustering and cell-type annotation, while also recovering biologically coherent metabolic programs that agree with dedicated metabolism-focused methods and capture therapy-response-associated states. In addition, the framework supports downstream inference of cell-type-specific biological activities from a single latent representation. Together, these results establish scKNIFE as a modular and extensible framework for end-to-end biological interpretation of single-cell cancer transcriptomics.
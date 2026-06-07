---
title: "Ignet 2.0 and Vignet: An Ontology-Driven Web Platform for Biomedical Gene Interaction Discovery and Visualization"
title_zh: Ignet 2.0与Vignet：用于生物医学基因相互作用发现与可视化的本体驱动Web平台
authors: "Asaduzzaman, S., Bansal, B., Combs, P., Zhang, J., Rehana, H., McGregor, B., He, Y., Hur, J."
date: 2026-06-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.02.729682v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 本体驱动的知识发现平台
tldr: 面对日益增长的生物医学文献，现有平台如STRING等在统一本体语义分类和疫苗网络构建方面存在不足。Ignet 2.0与Vignet作为双平台系统，通过PubMed文献挖掘和BioBERT评分引擎处理百万级基因共现对，并整合Interaction Network Ontology、Vaccine Ontology、Human Disease Ontology和DrugBank。平台提供基因相互作用发现、基因集富集检索、AI摘要及疫苗探索功能，并通过REST API和MCP实现实时集成。该工作为证据驱动的基因交互分析和疫苗语义探索提供了可扩展、本体引导的解决方案。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有生物医学平台缺乏统合本体驱动的基因相互作用发现、疫苗网络构建及AI辅助证据检索的一站式系统。
method: 融合PubMed文献挖掘、BioBERT评分、多种本体和药物库，构建基因相互作用评分和疫苗交互网络。
result: 实现百万级基因对评分、基因集富集检索、AI摘要及疫苗探索功能，并提供REST API和MCP接口。
conclusion: 平台为本体引导的基因交互分析和疫苗语义探索提供了可扩展、实时数据集成的基础设施。
---

## 摘要
背景：生物医学文献的扩展要求系统的本体引导发现基因相互作用、疫苗机制、药物关联和不良事件。现有平台如STRING、DisGeNET和PubTator未能提供统一的、可自由访问的系统，该系统整合了基于本体的语义相互作用分类、以疫苗为中心的异质网络构建以及人工智能辅助的证据检索。结果：Ignet 2.0和Vignet是可自由访问的双平台系统，它们结合了PubMed文献挖掘、基于BioBERT的数百万基因-基因共现对的相互作用评分，并整合了三个生物医学本体和一个精选药物资源：相互作用网络本体（INO）、疫苗本体（VO）、人类疾病本体（HDO）和DrugBank。Ignet 2.0支持基因相互作用发现、经BioBERT评分的基因对证据的基因集富集检索，以及通过BioSummarAI进行的AI辅助总结。Vignet通过VO引导的疫苗探索、VacPair相互作用评分以及VacNet中疫苗、基因、药物和疾病网络的创建扩展了这些功能。公共的表述性状态转移应用程序编程接口（REST API）和模型上下文协议（MCP）端点实现了实时集成，促进了对生物医学知识发现的信任。结论：Ignet 2.0和Vignet是可扩展的、本体引导的生物医学知识平台，它们促进基于证据的基因相互作用分析、以疫苗为中心的语义探索和AI辅助的知识发现。其实时PubMed数据集成确保了最新的见解；然而，用户应考虑验证过程以及纳入最新实验数据的潜在延迟，这可能影响即时数据的可靠性。可用性：Ignet 2.0：https://ignet.org/ignet；Vignet：https://ignet.org/vignet/

## Abstract
Background: The expansion of biomedical literature demands systematic ontology-guided discovery of gene interactions, vaccine mechanisms, drug associations, and adverse events. Existing platforms such as STRING, DisGeNET, and PubTator fall short of providing a unified, freely accessible system that integrates ontology-based semantic interaction classification, vaccine-focused heterogeneous network construction, and Artificial Intelligence-assisted evidence retrieval. Results: Ignet 2.0 and Vignet are freely accessible dual-platform systems that combine PubMed literature mining, BioBERT-based interaction scoring for millions of gene-gene co-occurrence pairs and integrate three biomedical ontologies and one curated drug resource, Interaction Network Ontology (INO), Vaccine Ontology (VO), Human Disease Ontology (HDO), and DrugBank. Ignet 2.0 supports gene interaction discovery, gene set enrichment retrieval of BioBERT-scored GenePair evidence, and AI-assisted summarization through BioSummarAI. Vignet extends these features with VO-guided Vaccine Exploration, VacPair interaction scoring, and the creation of vaccine, gene, drug, and disease networks in VacNet. A public Representational State Transfer Application Programming Interface (REST API) and Model Context Protocol (MCP) endpoint enable real-time integration, fostering trust in biomedical knowledge discovery. Conclusion: Ignet 2.0 and Vignet are scalable, ontology-guided biomedical knowledge platforms that facilitate evidence-based gene interaction analysis, vaccine-focused semantic exploration, and AI-assisted knowledge discovery. Their real-time PubMed data integration ensures up-to-date insights; however, users should consider validation processes and potential lags in incorporating the latest experimental data, which may affect the reliability of immediate data. Availability: Ignet 2.0: https://ignet.org/ignet; Vignet: https://ignet.org/vignet/
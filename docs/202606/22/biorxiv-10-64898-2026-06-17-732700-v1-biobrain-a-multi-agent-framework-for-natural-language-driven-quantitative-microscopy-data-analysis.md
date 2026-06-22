---
title: "BioBrain: A Multi-Agent Framework for Natural Language Driven Quantitative Microscopy Data Analysis"
title_zh: BioBrain：自然语言驱动的定量显微镜数据分析的多智能体框架
authors: "Tsolakidis, K., Breuer, A., Bender, S. W. B., Margaritaki, S., Dreisler, M. W., Oikonomou, A., Hatzakis, N. S."
date: 2026-06-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.17.732700v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 用于自然语言驱动显微镜数据分析的多智能体框架
tldr: 荧光显微镜数据日益复杂，分析门槛高。现有方法依赖专业软件和技能，制约生物学家使用。BioBrain多智能体框架将自然语言分析目标转换为可复现流程，集成已验证方法并透明报告参数。在双通道TIRF和三维晶格光片基准测试中，指定参数时精确复现专家结果，未指定时退化可预测。该框架弥合了数据获取与生物学发现之间的鸿沟，让生物学家用生物语言而非软件语言进行分析。
source: biorxiv
selection_source: fresh_fetch
motivation: 荧光显微镜数据量激增，但分析依赖专门软件和专业知识，阻碍了生物学家直接获取定量见解。
method: 提出多智能体框架BioBrain，将自然语言目标映射到可执行分析流程，集成已验证方法并透明报告每一步参数。
result: 在TIRF和晶格光片基准上，指定参数时精确复现专家结果，未指定时退化可预测，优于直接使用语言模型。
conclusion: 弥合数据获取与生物学发现之间的差距，使生物学家能用自然语言进行定量分析。
---

## 摘要
荧光显微镜的进步极大地扩展了可解决的生物学问题范围，能够以前所未有的时空分辨率定量观察分子相互作用和细胞动态。然而，成像数据日益增长的复杂性已超过了我们分析它们的能力。尽管存在众多计算方法，但它们通常依赖专门的软件环境、异构数据格式和技术专业知识，限制了采用并扩大了数据采集与定量生物学解释之间的鸿沟。在此，我们介绍BioBrain，一个将自然语言分析目标转化为可执行且可复现的显微镜分析流程的多智能体框架。BioBrain并非生成分析代码，而是组装经过验证的分析方法，并通过将现有实验室脚本集成到一个统一的对话框架中来扩展其分析能力。每个选定的方法和推断的参数都会被透明地报告，确保分析的可追溯性和可复现性。在双通道全内反射荧光和三维晶格光片基准测试中，当参数指定时，BioBrain精确重现了专家得出的结果；当参数未指定时，其性能可预测且可追溯地下降，而前沿语言模型虽然无警告地完成分析，却产生了依赖于模型的大幅定量误差。BioBrain为弥合数据采集与生物学发现之间日益扩大的鸿沟提供了一条实用路径，使实验科学家能够以生物学的语言而非软件的语言与计算分析进行沟通。

## Abstract
Advances in fluorescence microscopy have dramatically expanded the range of biological questions that can be addressed, enabling quantitative observations of molecular interactions and cellular dynamics with unprecedented spatial and temporal resolution. However, the growing complexity of imaging data has outpaced our ability to analyze them. Despite numerous computational methods exist, they often rely on specialized software environments, heterogeneous data formats, and technical expertise, limiting adoption and widening the gap between data acquisition and quantitative biological interpretation. Here we introduce BioBrain, a multi-agent framework that translates natural-language analytical goals into executable and reproducible microscopy analysis pipelines. Instead of generating analysis code, BioBrain assembles validated analytical methods and can expands its analytical capabilities by integrating existing laboratory scripts into a unified conversational framework. Every selected method and inferred parameter is transparently reported, ensuring traceable and reproducible analyses. On two-channel total internal reflection fluorescence and three-dimensional lattice light-sheet benchmarks, BioBrain exactly reproduces expert-derived results when parameters are specified and degrades predictably and traceably when they are not, while frontier language models generated large, model-dependent quantitative errors despite completing without warning. BioBrain offers a practical path for closing the widening gap between data acquisition and biological discovery, enabling experimental scientists to communicate with computational analysis in the language of biology rather than the language of software.
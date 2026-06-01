---
title: Ontology-driven software engineering using LLMs for knowledge graphs in engineering biology
title_zh: 使用大语言模型的基于本体的软件工程：面向工程生物学中的知识图谱
authors: "Medeni, I. T., Ünal, M., Galizi, R., Bartley, B., Beal, J., Myers, C. J., Vaidyanathan, P., Mısırlı, G."
date: 2026-06-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.29.728869v2.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 基于本体驱动的LLM知识图谱生成框架
tldr: 工程生物学领域对标准化和集成工具的需求日益增长，但大语言模型生成的软件常难以满足复杂需求且不够直观。为此，我们提出一种基于本体的软件工程方法，利用大语言模型将领域术语和图结构系统映射为面向用户的软件库。该方法通过为合成生物学开放语言SBOL创建本体并生成sbol-script库得到验证，该库支持浏览器内使用或原生Web应用开发。这一框架和资源为社区提供了可持续软件工程解决方案，有助于推动工程生物学软件项目的长期发展。
source: biorxiv
selection_source: fresh_fetch
motivation: 工程生物学标准化和工具开发需求增加，现有LLM生成软件不够直观和可持续。
method: 提出本体到语言框架，利用LLM将本体结构化映射为面向用户的软件库。
result: 创建SBOL3本体并生成sbol-script库，可在浏览器中使用或开发Web应用。
conclusion: 基于本体的方法与资源有助于社区开发可持续的软件项目。
---

## 摘要
大语言模型已经改变了软件工程实践。然而，生成的工件并不总是开发者友好的，并且可能部分满足复杂需求。随着工程生物学中对工具进行标准化、集成和开发的需求增加，需要新颖的方法来可持续地创建和维护直观的软件。在这里，我们提出了一种使用大语言模型的基于本体的方法，用于创建面向用户的知识图谱软件库。我们引入了一个本体到语言的框架，以系统地映射领域术语和图结构。然后，我们通过为最新的合成生物学开放语言标准创建本体，并生成sbol-script软件库来演示这种方法，该库可以在浏览器中使用或用于开发具有原生Web支持的应用程序。这种基于本体的软件工程方法和这些资源对于社区以及促进可持续软件项目的开发至关重要。SBOL3本体和sbol-script库可从https://github.com/SynBioDex/sbol-owl3和https://github.com/SynBioDex/sbol-script获取。

## Abstract
Large language models have transformed software engineering practices. However, generated artefacts are not always developer-friendly and may partially meet complex requirements. As the need to standardise, integrate, and develop tools in engineering biology increases, novel approaches are needed to create and maintain intuitive software sustainably. Here, we present an ontology-driven approach using large language models to create user-facing software libraries for knowledge graphs. We introduce an ontology-to-language framework to systematically map domain terms and graph structures. We then demonstrate this approach by creating an ontology for the latest Synthetic Biology Open Language standard and generating the sbol-script software library, which can be used within browsers or to develop applications with native web support. This ontology-driven software engineering approach and these resources are essential for the community and to facilitate the development of sustainable software projects. The SBOL3 Ontology and the sbol-script library are available from https://github.com/SynBioDex/sbol-owl3 and https://github.com/SynBioDex/sbol-script.
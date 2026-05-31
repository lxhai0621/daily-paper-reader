---
title: Ontology-driven software engineering using LLMs for knowledge graphs in engineering biology
title_zh: 使用大语言模型的本体驱动软件工程方法在工程生物学知识图谱中的应用
authors: "Medeni, I. T., Ünal, M., Galizi, R., Bartley, B., Beal, J., Myers, C. J., Vaidyanathan, P., Mısırlı, G."
date: 2026-05-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.29.728869v1.full.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 使用LLM和本体驱动生成知识图谱库以集成结构化知识库
tldr: 工程生物学对标准化和集成工具的需求日益增长，但大型语言模型生成的软件工件对开发者不够友好，难以满足复杂需求。本文提出一种本体驱动方法，利用大型语言模型为知识图谱创建面向用户的软件库。通过引入本体到语言框架，系统映射领域术语和图结构，并构建了合成生物学开放语言（SBOL）的本体，生成了sbol-script库。该库可在浏览器中使用或用于开发原生Web应用，为社区提供了可持续软件工程资源，促进了工程生物学工具的发展。
source: biorxiv
selection_source: fresh_fetch
motivation: 工程生物学需要标准化和集成工具，但LLM生成的软件库对开发者不友好，难以满足复杂需求。
method: 提出本体驱动方法，引入本体到语言框架，系统映射领域术语和图结构，结合LLM生成软件库。
result: 创建SBOL3本体并生成sbol-script库，可在浏览器或Web应用中使用。
conclusion: 该方法为社区提供可持续软件工程资源，促进工程生物学工具发展。
---

## 摘要
大语言模型已经改变了软件工程实践。然而，生成的工件并不总是对开发者友好，并且可能部分满足复杂的需求。随着工程生物学中工具标准化、集成和开发需求的增加，需要新的方法来可持续地创建和维护直观的软件。在这里，我们提出了一种使用大语言模型的本体驱动方法，用于创建面向用户的知识图谱软件库。我们引入了一个本体到语言的框架，系统地映射领域术语和图结构。然后，我们通过为最新的合成生物学开放语言标准创建本体并生成sbol-script软件库来演示这种方法，该库可以在浏览器中使用或用于开发支持本机Web的应用程序。这种本体驱动的软件工程方法以及这些资源对于社区以及促进可持续软件项目的开发至关重要。SBOL3本体和sbol-script库可在https://github.com/SynBioDex/sbol-owl3和https://github.com/SynBioDex/sbol-script获得。

## Abstract
Large language models have transformed software engineering practices. However, generated artefacts are not always developer-friendly and may partially meet complex requirements. As the need to standardise, integrate, and develop tools in engineering biology increases, novel approaches are needed to create and maintain intuitive software sustainably. Here, we present an ontology-driven approach using large language models to create user-facing software libraries for knowledge graphs. We introduce an ontology-to-language framework to systematically map domain terms and graph structures. We then demonstrate this approach by creating an ontology for the latest Synthetic Biology Open Language standard and generating the sbol-script software library, which can be used within browsers or to develop applications with native web support. This ontology-driven software engineering approach and these resources are essential for the community and to facilitate the development of sustainable software projects. The SBOL3 Ontology and the sbol-script library are available from https://github.com/SynBioDex/sbol-owl3 and https://github.com/SynBioDex/sbol-script.
---
title: "VFB-MCP: Natural-Language Access to Drosophila Neuroscience Grounded by an Expert-Curated Ontology-Led Knowledgebase"
title_zh: VFB-MCP：基于专家策展本体知识库的果蝇神经科学自然语言访问
authors: "McLachlan, A. D., Court, R., Pilgrim, C., Longden, K., Brown, N. H. D., Osumi-Sutherland, D., Jefferis, G. S. X. E., Armstrong, D. J."
date: 2026-06-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.16.732577v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 通过MCP将LLM与专家知识库集成
tldr: 传统生物数据库访问依赖领域专业知识，对新用户形成障碍。本文通过Model Context Protocol (MCP)将专家策划的本体知识库Virtual Fly Brain (VFB)暴露给大语言模型，实现自然语言查询。在果蝇神经科学30项任务中，VFB-MCP-equipped LLM在25项上产生精确可验证答案，显著优于裸LLM和网络搜索辅助LLM。该方法为神经科学和连接组学数据提供有效的大语言模型访问途径。
source: biorxiv
selection_source: fresh_fetch
motivation: 生物数据库访问需领域专业知识，新用户难以构建查询，需要降低访问门槛。
method: 通过Model Context Protocol将专家策划的本体知识库VFB暴露给LLM，实现自然语言精准查询。
result: 在30项神经科学任务中，VFB-MCP-equipped LLM在25项上给出精确可验证答案，优于裸LLM和网络搜索辅助LLM。
conclusion: MCP结合本体知识图谱可有效提升LLM在神经科学和连接组学数据查询中的回答质量。
---

## 摘要
生物数据库存储着经过策展的知识，研究人员传统上通过Web界面或API访问这些知识。要超越随意浏览，需要领域特定的知识和专长来构建探索这些数据所需的查询。这给正在经历范式转变的科学领域的新用户带来了障碍。通过模型上下文协议（MCP）将这些数据库暴露给大型语言模型（LLM），可以实现自然语言访问，这是一种潜在的可用性解决方案。我们针对Virtual Fly Brain（VFB）实现了这一点，VFB是一个由专家策展、基于本体的果蝇神经科学知识库，提供了使最近整合的联结组变得可访问所需的精确性。在30项神经科学任务上，与裸LLM和网络搜索辅助LLM进行基准测试，配备VFB-MCP的LLM在25/30任务上产生了精确、可验证且适当量化的答案，而网络搜索辅助LLM为14/30，裸LLM为2/30（Wilcoxon p<0.01，Holm校正，所有成对比较）。对于需要数据量化的任务，MCP的优势最大（89%对比网络的11%）。这项工作确立了基于本体的知识图谱上的MCP作为提高LLM在神经科学和联结组学数据响应质量的有效方法。

## Abstract
Biological databases store curated knowledge that researchers traditionally access through web interfaces or APIs. To move beyond casual browsing requires domain-specific knowledge and expertise to frame the queries necessary to explore this data. This generates a barrier for new users in scientific fields undergoing paradigm shifts. Exposing these databases to large language models (LLMs) via the Model Context Protocol (MCP) enables natural-language access, a potential accessibility solution. We implement this for Virtual Fly Brain (VFB), an expert-curated and ontology-backed knowledgebase of Drosophila neuroscience, providing the precision needed to make recently-integrated connectomes accessible. Benchmarked on 30 neuroscience tasks against a bare LLM and a web-search-assisted LLM, the VFB-MCP-equipped LLM produces precise, verifiable and appropriately quantified answers on 25/30 tasks vs 14/30 for web and 2/30 for bare (Wilcoxon p<0.01, Holm-corrected, all pairwise comparisons). The MCP advantage is largest for tasks where data quantification is required (89% vs 11% web). This work establishes MCP over ontology-backed knowledge graphs as an effective method to improve LLM response quality for neuroscience and connectomics data.
---
title: "BIFO: A Biological Information Flow Ontology for Directed Propagation in Heterogeneous Biomedical Knowledge Graphs"
title_zh: BIFO：用于异构生物医学知识图谱中定向传播的生物信息流本体
authors: "Taylor, D. M., Mohseni Ahooyi, T., Stear, B., Zhang, Y., Lahiri, A. M., Simmons, J. A., Chinwalla, A., Nemarich, C., Callahan, T. J., Silverstein, J. C."
date: 2026-05-28
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.25.727605v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 异构生物医学知识图谱中的定向传播本体
tldr: "生物医学知识图谱中并非所有边都能传递生物学信号，直接传播会引入噪声。提出BIFO本体，定义14个实体类和流分类学主干，制定可接受有向变换规则，通过四步条件化协议将原始图转化为仅保留可传播边的条件化传播图。在DDKG上验证，3360万条边中保留2370万（70.7%），分离出1330万可传播机制边和1050万保留但不传播的观察关联边。BIFO为生物知识图谱提供方向感知、可解释的信号传播规范，可作为重用基板。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有知识图谱分析忽略边类型差异，导致信号沿生物学无意义路径传播，影响结果解释性。
method: 构建BIFO本体，定义14个实体类和流分类学主干G+CH→RNA→P→PW→C→PH→DS，设定可接受有向变换约束，通过四步条件化协议过滤原始图。
result: "在DDKG上处理3360万边，保留2370万（70.7%），其中1330万可传播机制边与1050万保留非传播观察边清晰分离。"
conclusion: BIFO为异构知识图谱提供通用可传播性规范，支持方向感知、生物学可解释的信号传播分析。
---

## 摘要
生物医学知识图谱通过多种关系类型连接多种实体类型，从而整合异构数据。基于这些图谱进行信号传播的计算分析（随机游走、扩散和消息传递）隐含地假设每条可遍历的边都能携带生物信号。在异构知识图谱中，这很少成立：层次性、词法性和纯统计性的边本身并不定义可接受的定向状态转换，遍历这些边会沿着不具有生物学意义的路径传播信号。我们提出了生物信息流本体（BIFO），这是一种与图无关的规范，明确了哪些定向变换在生物学上可接受以实现可计算的信息流。BIFO定义了十四个实体类、一组围绕主干G+CH[-&gt;]RNA[-&gt;]P[-&gt;]PW[-&gt;]C[-&gt;]PH[-&gt;]DS组织的流类分类体系、一组可接受性约束以及一个两级CURIE映射，无需特定于模式的代码即可应用于任何其标识符和谓词可通过BIFO映射表解析或扩展的图。一个四步条件化协议将原始属性图转换为条件化传播图，其中仅保留可接受的、考虑方向的边。我们在Data Distillery知识图谱（DDKG）上提供了参考实现；将一个独立于队列、以基因为中心的子图条件化为包含3360万条边的BIFO基质，保留了2370万条（70.7%）作为BIFO分类的关系，清晰地将1330万条可传播的机制性边与1050万条保留但不传播的观察性关联区分开来，并确认通路概念被配置为BIFO-PPR通路评分的累积端点。BIFO是知识图谱上信号可计算传播的可接受性规范。它作为开放规范发布，附带版本化的映射表和工具，为生物医学知识图谱的可解释、方向感知分析提供了可重用的基质。

## Abstract
Biomedical knowledge graphs integrate heterogeneous data by connecting many entity types through many relationship types. Computational analyses that propagate signal across these graphs (random walks, diffusion, and message passing) implicitly assume that every traversable edge can carry a biological signal. In a heterogeneous KG this is rarely true: hierarchical, lexical, and purely statistical edges do not, by themselves, define an admissible directed state transformation, and traversing them propagates signal along paths that are not biologically meaningful. We present the Biological Information Flow Ontology (BIFO), a graph-agnostic specification of which directed transformations are biologically admissible for computable information flow. BIFO defines fourteen entity classes, a taxonomy of flow classes organized around the backbone G+CH [-&gt;]RNA [-&gt;]P [-&gt;]PW [-&gt;]C [-&gt;]PH [-&gt;]DS, a set of admissibility constraints, and a two-level CURIE mapping that can be applied without schema-specific code to any graph whose identifiers and predicates are resolvable through, or extendable to, the BIFO mapping tables. A four-step conditioning protocol converts a raw property graph into a conditioned propagation graph in which only admissible, direction-aware edges remain. We provide a reference implementation on the Data Distillery Knowledge Graph (DDKG); conditioning a cohort-independent, gene-anchored subgraph as a BIFO substrate of 33.6 million edges retained 23.7 million (70.7%) as BIFO-classified relationships, cleanly separating 13.3 million propagating mechanistic edges from 10.5 million retained-but-non-propagating observational associations, and confirming that pathway concepts are configured as scoring accumulation endpoints for BIFO-PPR pathway scoring. BIFO is an admissibility specification for computable propagation of signal over knowledge graphs. It is released as an open specification with versioned mapping tables and tooling, providing a reusable substrate for biologically interpretable, direction-aware analysis of biomedical knowledge graphs.
---
title: "VaxjoOnto: A Vaccine Ontology-driven Framework for Adjuvant Selection"
title_zh: VaxjoOnto：一种基于疫苗本体论的佐剂选择框架
authors: "He, Y., Zheng, Y."
date: 2026-05-27
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.27.690985v2.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 知识图谱集成用于佐剂选择
tldr: "疫苗佐剂选择是开发瓶颈，现有计算工具多聚焦抗原发现。VaxjoOnto将疾病-佐剂匹配建模为知识图谱上的top-k推荐任务，使用图神经网络和列表级排序目标训练。在基准上，已知疾病NDCG@10达0.59，未见疾病达0.27（比随机基线提升5.4倍）。该本体驱动框架有效补充了现有抗原发现工具，为佐剂优先级排序提供新思路。"
source: biorxiv
selection_source: fresh_fetch
motivation: 佐剂选择是疫苗开发瓶颈，但缺乏计算优先级排序工具，现有工作多聚焦抗原发现。
method: 构建生物医学本体异构知识图，使用图神经网络结合列表级排序目标进行疾病-佐剂匹配推荐。
result: "公共基准上已知疾病NDCG@10=0.59，未见疾病0.27，较随机基线提升5.4倍。"
conclusion: VaxjoOnto提供本体驱动的佐剂优先级排序框架，可有效补充现有抗原聚焦工具。
---

## 摘要
选择有效的佐剂仍然是疫苗开发中的瓶颈，但大多数计算工作针对的是抗原发现而非佐剂优先排序。我们将疾病-佐剂匹配视为一个基于生物医学本体的异构知识图上的top-k推荐任务，整合了经过整理的事实、机制通路和文本证据。我们引入了VaxjoOnto，这是一个使用列表排序目标训练的图神经网络。在一个公开基准测试中，VaxjoOnto在已知疾病上达到了0.59的NDCG@10，在先前未见疾病上达到了0.27（比随机基线提高了5.4倍）。该框架提供了一种基于本体的佐剂优先排序方法，补充了现有的以抗原为中心的工具。

## Abstract
Selecting an effective adjuvant remains a bottleneck in vaccine development, but most computational efforts have targeted antigen discovery rather than adjuvant prioritization. We frame disease-adjuvant matching as a top-k recommendation task on a heterogeneous knowledge graph grounded in biomedical ontologies, integrating curated facts, mechanistic pathways, and textual evidence. We introduce VaxjoOnto, a graph neural network trained with a listwise ranking objective. On a public benchmark, VaxjoOnto achieves NDCG@10 of 0.59 on seen diseases and 0.27 on previously unseen diseases (a 5.4 times improvement over a random baseline). The framework provides an ontology-anchored approach to adjuvant prioritization that complements existing antigen-focused tools.
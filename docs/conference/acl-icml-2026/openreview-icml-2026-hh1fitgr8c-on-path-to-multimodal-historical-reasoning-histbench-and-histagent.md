---
title: "On Path to Multimodal Historical Reasoning: HistBench and HistAgent"
title_zh: 迈向多模态历史推理：HistBench与HistAgent
authors: "Jiahao Qiu, Fulian Xiao, Yimin Wang, Yuchen Mao, Yijia Chen, Xinzhe Juan, Siran Wang, Xuan Qi, Tongcheng Zhang, Zixin Yao, Jiacheng Guo, Yifu Lu, Charles Argon, Jundi Cui, Daixin Chen, Junran Zhou, Shuyao Zhou, Zhanpeng Zhou, Ling Yang, Shilong Liu, Hongru WANG, Kaixuan Huang, xun jiang, Xi Gao, Mengdi Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/44aece1478419c978a8126227e9ac00c08524608.pdf"
tags: ["query:ancient-text"]
score: 6.0
evidence: 面向人文学科的多模态历史推理基准与领域智能体
tldr: 大模型在历史等人文学科的能力仍待探索，历史推理涉及多模态史料解读、时间推断与跨语言分析，通用智能体虽在现有基准表现良好却缺乏领域专业知识。本文构建HistBench历史推理基准，并设计领域智能体HistAgent。该基准包含按难度分层的四百余道经审核题目，覆盖史实检索等多种问题类型，为古籍与史料的多模态语义推理及数字人文研究提供了评测与智能体方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型在历史等人文学科的能力不足，缺乏领域专业推理能力。
method: 构建HistBench历史推理基准并设计领域智能体HistAgent。
result: 基准覆盖多类历史问题并评估提升多模态史料推理能力。
conclusion: 为史料多模态语义推理与数字人文提供评测与智能体方案。
---

## Abstract
Recent advances in large language models (LLMs) have led to remarkable progress across various domains, yet their capabilities in the humanities, particularly history, remain underexplored. Historical reasoning poses unique challenges for LLMs, involving multimodal source interpretation, temporal inference, and cross-linguistic analysis. Existing general-purpose agents perform well on many current benchmarks but lack the domain expertise needed to address complex historical questions.
To address this gap, we introduce HistBench, a new benchmark of 414 high-quality and carefully-reviewed questions stratified by difficulty and designed to evaluate LLM's capacity for historical reasoning. The tasks span a wide range of historical problems—from factual retrieval based on primary sources to interpretive analysis of manuscripts and images, to interdisciplinary challenges involving archaeology, linguistics, or cultural history. Furthermore, the benchmark dataset spans 29 ancient and modern languages and covers a wide range of historical periods and world regions. Finding the poor performance of LLMs and other agents on HistBench, we further present HistAgent, a history-specific agent equipped with carefully designed tools for OCR, translation, archival search, and image understanding in history. On HistBench, HistAgent based on GPT-4o achieves an accuracy of 28.50\% pass@1 and 36.47\% pass@2, significantly outperforming LLMs with online search and generalist agents, including GPT-4o (18.60\%), DeepSeek-R1 (14.98\%), Grok 3 (17.63\%) and Open Deep Research by smolagents (19.57\% pass@1 and 25.12\% pass@2). These results highlight the limitations of existing LLMs and generalist agents and demonstrate the advantages of HistAgent for historical reasoning. Notably, HistAgent also achieves 60.00\% pass@1 accuracy on the GAIA benchmark, showing that domain-specific customization doesn't hinder HistAgent's competitive performance on real-world general tasks. Code is available at https://github.com/CharlesQ9/HistAgent.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向人文学科的多模态历史推理基准与领域智能体。

### 2. 核心内容
大模型在历史等人文学科的能力仍待探索，历史推理涉及多模态史料解读、时间推断与跨语言分析，通用智能体虽在现有基准表现良好却缺乏领域专业知识。本文构建HistBench历史推理基准，并设计领域智能体HistAgent。该基准包含按难度分层的四百余道经审核题目，覆盖史实检索等多种问题类型，为古籍与史料的多模态语义推理及数字人文研究提供了评测与智能体方案。

### 3. 对应检索需求
digital humanities research on semantic parsing of ancient texts。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=hh1FITGR8C](https://openreview.net/forum?id=hh1FITGR8C)

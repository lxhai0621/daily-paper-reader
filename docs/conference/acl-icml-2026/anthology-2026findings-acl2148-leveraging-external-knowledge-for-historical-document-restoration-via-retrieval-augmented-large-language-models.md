---
title: Leveraging External Knowledge for Historical Document Restoration via Retrieval-Augmented Large Language Models
title_zh: 利用外部知识通过检索增强大模型修复历史文献
authors: "Gabeen Kim, Kyeongpil Kang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.2148.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 利用外部知识的检索增强历史文献修复
tldr: 历史文献是珍贵知识档案，却常因物理损坏而难以辨识。现有基于掩码语言模型的修复方法能利用局部上下文，却难以恢复需要外部历史知识的命名实体。本文提出结合检索增强生成的修复框架，将预训练大模型的内隐知识与显式检索的外部上下文相融合。实验表明该方法有效缓解了上下文相关专有名词的推断难题，为古籍文献的语义分析与知识提取提供支持。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2148/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 759, \"height\": 1007}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2148/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 1152, \"height\": 1152}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2148/fig-003.webp\", \"caption\": \"\", \"page\": 14, \"index\": 3, \"width\": 1230, \"height\": 635}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2148/fig-004.webp\", \"caption\": \"\", \"page\": 14, \"index\": 4, \"width\": 1227, \"height\": 670}]"
motivation: 历史文献因损坏难以辨识，现有掩码语言模型修复方法缺乏外部知识，难以恢复命名实体。
method: 提出结合检索增强生成的框架，融合大模型内隐知识与显式检索的外部上下文来修复文献。
result: 实验表明该方法有效缓解了上下文相关专有名词的推断难题，提升历史文献修复质量。
conclusion: 该工作将RAG用于历史文献修复，为古籍语义分析与知识提取提供了新途径。
---

## Abstract
Historical documents act as invaluable knowledge archives but often suffer from illegibility due to physical deterioration and damage. While existing restoration methods based on masked language modeling effectively utilize local context, they struggle to restore named entities that require external historical knowledge. To address this limitation, we introduce a novel framework for historical document restoration that leverages large language models with retrieval-augmented generation (RAG). By combining the implicit knowledge of pre-trained LLMs with explicitly retrieved external context, our model ARI effectively mitigates the challenge of inferring context-dependent proper nouns. Extensive experiments on Korean historical documents demonstrate that our approach significantly outperforms baselines, achieving substantial gains in restoring both general characters and named entities. Furthermore, comprehensive evaluations including expert assessments confirm that ARI serves as a practical tool for domain experts, promising to accelerate the analysis of historical records.

---

## 论文详细总结（自动生成）

# 论文总结：利用外部知识通过检索增强大模型修复历史文献

## 1. 核心问题与整体含义
- **研究背景**：历史文献是重要知识档案，但常因物理退化、光照、温湿度、手写转录等因素导致不可读。韩国《朝鲜王朝实录》（AJD）与《承政院日记》（JRS）等 Hanja 文献中，JRS 约有 11.1K 篇文档、41.9K 个字符损坏或不可识别。
- **核心问题**：现有基于掩码语言模型（MLM）的修复方法主要依赖单篇文档的局部上下文，难以恢复需要外部历史知识的命名实体，如人名、地名、书名、官职等。
- **统计动机**：论文统计约 42,064 个损坏字符中，约 44.8% 为命名实体；其中 PER 占 26.7%、LOC 占 6.9%、ETC 占 6.8%、DAT 占 3.4%、POH 占 1.0%，非命名实体占 55.2%。说明命名实体修复是关键难点。
- **整体含义**：论文提出结合大语言模型与检索增强生成（RAG）的历史文献修复框架，将 LLM 的内隐知识与显式检索到的外部上下文结合，提升一般字符与命名实体的修复效果，并面向领域专家提供实用协作工具。

## 2. 方法论
- **核心思想**：使用预训练 LLM 作为生成式修复器，通过 RAG 显式注入外部历史知识，并通过微调让模型更好利用检索文档；模型命名为 **ARI**（Archive Restoration Intelligence）。
- **输入输出形式**：损坏字符用 `[Dn]` 标记，模型输出 JSON，如 `{"[D1]": "南", "[D2]": "延"}`，每个 `[Dn]` 对应一个 Hanja 字符。
- **外部知识注入**：
  - **元数据**：加入朝代/王、年、月、日等时间信息。
  -

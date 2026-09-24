---
title: "Ranking Free RAG: Replacing Re-ranking with Selection in RAG for Sensitive Domains"
title_zh: 无排序的RAG：在敏感领域用选择替代重排序
authors: "Yash Saxena, Ankur Padia, Mandar Chaudhary, Kalpa Gunaratna, srinivasan parthasarathy, Manas Gaur"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/89249f95a20c7f640700b1838d6277110fd3ab32.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向敏感领域的可解释证据选择RAG
tldr: 在敏感领域部署的检索增强生成系统需要可解释的证据选择与抗数据投毒能力，而现有方法依赖不透明的相似度检索与任意 top-k 截断，既无解释也易受攻击。本文提出 METEORA，通过偏好微调让通用大模型生成显式理由，指导自适应证据选择。该框架提升了检索的准确性与可解释性，为敏感域 RAG 的可靠性提供保障。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 敏感领域RAG依赖不透明相似度检索与任意top-k截断，缺乏解释且易受数据投毒攻击。
method: 提出METEORA，偏好微调通用LLM生成显式理由，引导可解释的自适应证据选择。
result: 该框架实现可解释的证据选择，增强对对抗操纵的鲁棒性并提升检索质量。
conclusion: METEORA为敏感域RAG提供了可解释、抗投毒的证据选择方案，提升系统可信度。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems deployed in sensitive domains must provide interpretable evidence selection and robust safeguards against data poisoning, yet current approaches rely on opaque similarity-based retrieval with arbitrary top-k cutoffs that offer no explanation for their selections and remain vulnerable to adversarial manipulation. We propose METEORA, a rationale-driven RAG framework that addresses these fundamental limitations through interpretable, adaptive evidence retrieval. Our framework introduces three synergistic contributions. First, we preference-tune a general-purpose LLM to generate explicit rationales that articulate why specific evidence is needed for a given query. These rationales then guide adaptive evidence selection through a two-step process: rationale-chunk pairing for query-specific relevance assessment, followed by dynamic cutoff detection that eliminates the need for arbitrary k heuristics. Finally, the same rationales enable a verification stage that filters poisoned or misleading evidence before generation. Evaluation across six datasets demonstrates substantial improvements on three critical dimensions. For retrieval quality, METEORA achieves **21.05\%** higher precision than the best-performing baseline, while its variant with context expansion achieves **13.41\%** higher recall. In terms of efficiency, the framework reduces the volume of evidence required to reach comparable recall by **80\%**, which directly translates to a **33.34\%** improvement in downstream answer generation accuracy. Most notably for adversarial robustness, METEORA increases the F1 score from **0.10 to 0.44** under poisoning attacks, a 4.4$\times$ improvement that makes RAG systems substantially more resilient to adversarial manipulation. Human evaluation with four experienced annotators confirms genuine interpretability, achieving a mean confidence score of **3.64/5** and demonstrating that humans can reliably reconstruct evidence-level decisions with **86\% accuracy**. These results demonstrate that rationale-driven retrieval can simultaneously enhance interpretability, efficiency, and safety in RAG systems for sensitive domains. The code is available in the anonymous GitHub repository \url{https://anonymous.4open.science/r/METEORA-DC46/README.md}

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向敏感领域的可解释证据选择RAG。

### 2. 核心内容
在敏感领域部署的检索增强生成系统需要可解释的证据选择与抗数据投毒能力，而现有方法依赖不透明的相似度检索与任意 top-k 截断，既无解释也易受攻击。本文提出 METEORA，通过偏好微调让通用大模型生成显式理由，指导自适应证据选择。该框架提升了检索的准确性与可解释性，为敏感域 RAG 的可靠性提供保障。

### 3. 对应检索需求
Techniques to improve RAG accuracy and relevance。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=O88FCPAPAj](https://openreview.net/forum?id=O88FCPAPAj)

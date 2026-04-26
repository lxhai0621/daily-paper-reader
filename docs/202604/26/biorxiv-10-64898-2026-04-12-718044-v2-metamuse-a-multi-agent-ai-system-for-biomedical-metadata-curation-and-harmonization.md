---
title: "MetaMuse: A Multi-Agent AI System for Biomedical Metadata Curation and Harmonization"
authors: "Mittal, E., Litman, E., Myers, T., Agarwal, V., Gopinath, A., Kassis, T."
date: 2026-04-20
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.12.718044v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自主元数据提取和协调的多智能体系统
tldr: MetaMuse是一个多智能体框架，用于自动化知识发现和非结构化元数据标准化。
source: biorxiv
selection_source: fresh_fetch
motivation: 用于自主元数据提取和协调的多智能体系统。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Inconsistent and unstructured metadata in public biomedical repositories, such as the Gene Expression Omnibus (GEO), severely limits data discoverability and research reproducibility. To address this, we introduce MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW, a modular, multi-agent artificial intelligence framework designed to autonomously extract, validate, and standardize unstructured biomedical metadata. Operating through a three-stage architecture utilizing large language model agents, specialized CO_SCPLOWURATORC_SCPLOWAO_SCPLOWGENTSC_SCPLOW contextually extract candidate values for specific target metadata fields. A centralized AO_SCPLOWRBITRATORC_SCPLOWAO_SCPLOWGENTC_SCPLOW enforces cross-field logical consistency to prevent contradictory annotations. Finally, a NO_SCPLOWORMALIZERC_SCPLOWAO_SCPLOWGENTC_SCPLOW leveraging a domain-specific semantic search model (SapBERT) maps these free-text candidates to formal ontological terms. We evaluated MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW on a gold-standard dataset of manually curated GEO samples, achieving over 95% curation accuracy across key target metadata fields, and demonstrated robust scalability on a broader dataset of 400 samples. Notably, MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW avoids data hallucination by defaulting to conservative false negatives when evidence is ambiguous, thereby preserving strict data integrity. By providing a fully auditable and context-aware curation pipeline, MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW offers a scalable solution for enriching public data repositories and accelerating reproducible, data-driven scientific discovery.
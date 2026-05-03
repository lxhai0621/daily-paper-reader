---
title: "All Models are Wrong, Some are Annotated: Automating Metadata in Biomedical Repositories"
title_zh: 所有模型都是错的，但有些是有标注的：生物医学库中元数据的自动化
authors: "Cohen, I., Yu, H., McDougal, R. A."
date: 2026-04-27
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.23.720371v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.5
evidence: 使用大语言模型自动提取元数据和知识发现
tldr: "高质量元数据对科学发现至关重要，但生物医学库中常存在标注稀疏问题。本研究评估了大语言模型（LLM）从神经科学库ModelDB的源代码中自动推断离子通道和受体亚型元数据的能力。通过对比GPT系列模型与传统XGBoost模型，发现结合启发式增强提示的LLM在类型和亚型识别上表现卓越，准确率分别达到96%和88.1%。该方法为生物医学库的大规模元数据自动化标注提供了高效且可扩展的解决方案。"
source: biorxiv
selection_source: fresh_fetch
motivation: 针对生物医学库中手动标注元数据稀疏且效率低下的问题，探索利用大语言模型从源代码中自动提取关键生物学元数据的可行性。
method: "提取ModelDB中5,133个模型文件，对比了GPT-5.2、GPT-mini（零样本及启发式增强提示）与基于特征工程的XGBoost模型在元数据分类上的表现。"
result: "启发式增强的GPT模型在类型识别上达到96%的准确率，在亚型识别上达到88.1%，显著优于传统的XGBoost基准模型。"
conclusion: 大语言模型能够直接从源代码中高效生成高质量元数据，是提升生物医学库可发现性和自动化标注水平的实用工具。
---

## 摘要
目的：高质量的元数据对于科学发现至关重要，然而在快速增长的存储库中，稀疏的标注导致许多生物学相关的细节未能被捕获。我们评估了大语言模型（LLMs）是否能从神经科学存储库的源代码中准确推断出离子通道和受体亚型的元数据。材料与方法：我们从 ModelDB 中提取了 5,133 个模型文件。其中 1,100 个子集经过人工标注；253 个用于测试，其余分为训练集（80%）和验证集（20%）。在零样本（zero-shot）和启发式增强提示下评估了基于 LLM 的方法（GPT-5.2 和 GPT-mini）。使用准确率、精确率、召回率和 F1 分数在类型和亚型级别评估性能。使用文本和模拟衍生特征的特征工程 XGBoost 模型作为基准。结果：LLMs 的表现优于 XGBoost 基准。在类型级别，带有启发式增强的 GPT-mini 实现了最高性能（准确率 96.0%，F1 0.962）。在亚型级别，GPT-5.2+启发式和 GPT-mini+启发式均达到了相同的准确率（88.1%），其中 GPT-5.2+启发式实现了最高的 F1（0.878）。模型输出在多次运行中保持一致，且错误局限于相关的机制家族。讨论与结论：LLMs 展示了直接从源代码进行元数据标注的强大潜力，在极少调优的情况下优于特征工程方法。然而，不同亚型的性能存在差异，错误通常反映了歧义或对更常见标签的偏见。这些发现表明，LLMs 可作为生物医学库中可扩展元数据生成的实用工具，尽管仔细的评估和特定领域的验证仍然很重要。虽然在计算神经科学中得到了证明，但这种方法可能推广到其他科学代码库中与库无关的元数据标注。

## Abstract
ObjectiveHigh-quality metadata is essential for scientific discovery, yet sparse annotations in rapidly growing repositories leave many biologically relevant details uncaptured. We evaluated whether large language models (LLMs) can accurately infer ion channel and receptor subtype metadata from source code in a neuroscience repository.

Materials and MethodsWe extracted 5,133 model files from ModelDB. A subset of 1,100 was manually annotated; 253 were held out for testing, and the remainder split into training (80%) and validation (20%) sets. LLM-based approaches (GPT-5.2 and GPT-mini) were evaluated under zero-shot and heuristic-augmented prompting. Performance was assessed at type and subtype levels using accuracy, precision, recall, and F1 score. A feature-engineered XGBoost model using text- and simulation-derived features served as a baseline.

ResultsLLMs outperformed the XGBoost baseline. At the type level, GPT-mini with heuristic augmentation achieved the highest performance (accuracy 96.0%, F1 0.962). At the subtype level, both GPT-5.2+heuristics and GPT-mini+heuristics achieved identical accuracy (88.1%), with GPT-5.2+heuristics achieving the highest F1(0.878). Model outputs were consistent across runs and errors confined to related mechanistic families.

Discussion and ConclusionLLMs demonstrate strong potential for metadata annotation directly from source code, outperforming feature-engineering approaches with minimal tuning. However, performance varied across subtypes, and errors often reflected ambiguity or bias toward more common labels. These findings suggest LLMs may serve as practical tools for scalable metadata generation in biomedical repositories, although careful evaluation and domain-specific validation remain important. While demonstrated in computational neuroscience, this approach may generalize to repository-agnostic metadata annotation in other scientific code repositories.
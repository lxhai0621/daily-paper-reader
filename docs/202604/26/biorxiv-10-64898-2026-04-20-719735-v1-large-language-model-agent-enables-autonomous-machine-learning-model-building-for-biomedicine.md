---
title: Large Language Model Agent Enables Autonomous Machine Learning Model Building for Biomedicine
authors: "Guo, H., Liang, Y., Cheng, X., Ellington, C., Xie, P., Song, L., Xing, E."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719735v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自动机器学习模型开发的自主智能体系统
tldr: AIDO.Harness利用智能体AI系统自动化生物医学模型开发的整个生命周期。
source: biorxiv
selection_source: fresh_fetch
motivation: 用于自动机器学习模型开发的自主智能体系统。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Machine learning accelerates biomedical discovery, but creating effective predictive models requires specialized human expertise and demanding manual effort. Researchers must iteratively design pipelines, select architectures, and debug code. This challenge is particularly severe in biomedicine because of the heterogeneous datasets, sparse annotations, and complex evaluation protocols one must deal with. We present AIDO.Harness, an agentic artificial intelligence system that fully automates the entire life-cycle of biomedical model development. Provided only with a natural language task description and a target metric, AIDO.Harness autonomously constructs executable training and evaluation pipelines. The system selects optimal modeling strategies, executes experiments, and uses automated feedback-loop to iteratively revise its own code, configurations, and training procedures. It flexibly adapts to new tasks by training specialized models de novo or refining pretrained foundation models. We show that across diverse biomedical benchmarks, AIDO.Harness produces highly competitive solutions against human alternatives, while eliminating the manual iteration previously required for robust model development. By automating the translation of raw data into reliable AI models, AIDO.Harness demonstrates how AI itself can be used to accelerate AI for biomedical research.
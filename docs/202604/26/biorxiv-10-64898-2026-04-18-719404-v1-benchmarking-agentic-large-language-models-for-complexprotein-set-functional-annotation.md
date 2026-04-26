---
title: Benchmarking Agentic Large Language Models for ComplexProtein-Set Functional Annotation
authors: "Zhang, X."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.18.719404v1.full.pdf"
tags: ["query:agent"]
score: 9.0
evidence: 针对复杂生物注释任务的智能体大模型基准测试
tldr: 评估了LLM智能体在合成异构生物信息学证据进行功能注释时的可靠性。
source: biorxiv
selection_source: fresh_fetch
motivation: 针对复杂生物注释任务的智能体大模型基准测试。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Large language model (LLM) agents are increasingly used to synthesize heterogeneous bioinformatics evidence, but their reliability for high-volume biological annotation remains poorly characterized. We evaluated three agent configurations on a controlled protein annotation task: Claude App with Claude Opus 4.7, Claude Code CLI with Claude Opus 4.7 and Claude Scientific Skills, and Codex App with GPT-5.4 and Claude Scientific Skills. Each configuration was run three times on the same verbatim prompt, the same 73 selected orthogroup FASTA files (1,705 protein sequences), and the same local evidence: Swiss-Prot BLASTP output, Pfam/HMMER domain hits, DeepTMHMM topology predictions, and SignalP secretion predictions. We audited the nine outputs for coverage, biological correctness, missing evidence, hallucinated or over-specific annotations, and within-method consistency, then merged the best-supported evidence into a final orthogroup annotation table. All nine runs covered all 73 orthogroups, indicating that the agents could retrieve and organize the complete input set. However, normalized calcification-relevance calls were only moderately reproducible: within-method exact tier agreement ranged from 0.397 to 0.685 for Claude App (mean 0.562), 0.342 to 0.740 for Claude Code (mean 0.516), and 0.411 to 0.630 for Codex App (mean 0.539), and the per-run number of high-confidence calls varied from 0 to 12 across the nine runs. The final curated table retained 3 high-confidence, 9 moderate, 18 watchlist, and 43 low-relevance orthogroups. The most robust direct candidates were sulfatase (OG0017138) and sulfotransferase (OG0020703) families and an FG-GAP/integrin-like surface protein family (OG0018986), whereas common error modes included elevating pentapeptide-repeat orthogroups on motif evidence alone, treating weakly secreted housekeeping enzymes as matrix proteins, and taking low-complexity BLAST labels at face value. Skill-enabled agents improved file handling, evidence traceability, and reproducibility of computational checking, but they did not eliminate biological overinterpretation. These results support a best-practice workflow in which LLM agents draft annotations only after deterministic evidence tables are generated, with explicit scoring rules, provenance columns, run-to-run replication, and expert review of high-impact claims.
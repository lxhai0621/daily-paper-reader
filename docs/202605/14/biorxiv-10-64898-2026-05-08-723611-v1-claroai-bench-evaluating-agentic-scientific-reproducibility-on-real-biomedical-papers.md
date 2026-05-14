---
title: "ClaroAI-Bench: Evaluating Agentic Scientific Reproducibility on Real Biomedical Papers"
authors: "O'Connell, K. A."
date: 2026-05-12
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.08.723611v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 评估AI智能体复现计算发现的能力
tldr: "ClaroAI-Bench是一个评估AI智能体在生物医学领域科学复现能力的基准测试。它包含35篇NIH资助的论文，涵盖基因组学、影像学等五大领域。通过五维评估指标（数据发现、获取、代码可用性、环境重建及结果复现），研究发现全功能智能体能复现约60.6%的计算论文，揭示了环境重建是复现过程中的主要瓶颈，为科学AI评估提供了新工具。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有的代码生成基准测试无法充分评估AI智能体在处理具有复杂环境和缺失元数据的真实科学复现任务中的能力。
method: 提出了包含35篇真实论文的ClaroAI-Bench，并采用涵盖数据、代码、环境和结果五个维度的评分标准来评估智能体的端到端复现表现。
result: "全功能智能体成功复现了60.6%的计算论文，且研究发现元数据评分与复现成功率强相关，而环境重建是分歧最大的评估维度。"
conclusion: ClaroAI-Bench填补了科学AI评估的空白，证明了AI智能体在处理长程、真实的科学复现任务中具有潜力，但也面临环境配置等挑战。
---

## Abstract
We introduce ClaroAI-Bench, an evaluation suite for measuring AI agents' ability to reproduce computational findings from published biomedical research. The benchmark comprises 35 real NIH-funded papers spanning five modalities (genomics, imaging, clinical/EHR, epidemiology, wet-lab) scored on a five-dimension rubric: data findability (D1), data accessibility (D2), code availability (D3), environment reconstructability (D4), and results reproducibility (D5). Each task requires an agent to locate data, obtain code, reconstruct the compute environment, execute the analysis, and verify results against published claims, mirroring the full scientific reproduction pipeline. In a three-condition ablation, an audit-only baseline (D1-D4 metadata scoring) and a bash-only agent (API + bash tool) both achieve 0% D5 reproduction, while a full-capability agent (Claude Code, all tools) reproduces 20 of 33 computational papers (60.6%; 95% CI [42.4, 75.8]). D1-D4 metadata scores strongly predict D5 outcomes (Spearman r=0.68, p<0.0001), and papers with accessible data and code achieve 2.9 times higher D5 scores than restricted papers (p=0.0013). Multi-model scoring with three frontier models (Claude Opus 4.6, GPT-5.4, Gemini 2.5 Pro) yields inter-model agreement of r=0.85-0.97 on D3 but only r=0.51-0.81 on D4, identifying environment reconstruction as the dimension with highest evaluator disagreement. ClaroAI-Bench fills a gap between code-generation benchmarks (SWE-bench) and end-to-end scientific AI evaluations by testing long-horizon, real-world reproduction tasks with brittle environments, missing metadata, and access constraints. The benchmark, scoring rubric, agent logs, and pip-installable auditor are archived at https://doi.org/10.5281/zenodo.20071236 and on HuggingFace Datasets at https://huggingface.co/datasets/kyleaoconnell22/claroai-bench.

---

## 论文详细总结（自动生成）

这是一份关于论文《ClaroAI-Bench: Evaluating Agentic Scientific Reproducibility on Real Biomedical Papers》的结构化深入分析报告：

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：评估AI智能体（AI Agents）是否能够端到端地复现已发表的真实科学研究结果。
*   **研究背景**：虽然AI在代码生成、文献综述和实验设计方面表现出色，但现有的基准测试（如SWE-bench）多关注孤立的代码修复或合成任务。科学复现是一个复杂的长程任务，涉及在异构仓库中寻找数据、修复缺失或损坏的代码、重建计算环境以及验证定量结果。
*   **整体含义**：论文提出了**ClaroAI-Bench**，这是首个针对真实生物医学论文（受NIH资助）的计算复现能力评估基准，旨在衡量AI在处理真实世界科学“脆弱性”（如元数据缺失、环境配置困难）时的表现。

### 2. 论文提出的方法论
*   **核心思想**：将科学复现过程标准化为五个连续阶段，并对应五维评分量表（D1-D5）。
*   **五维评分标准（0-2分制）**：
    1.  **D1 (Data Findable)**：数据是否可发现（是否有声明、链接或访问号）。
    2.  **D2 (Data Accessible)**：数据是否可获取（是否可直接下载或需授权）。
    3.  **D3 (Code Available)**：代码是否可用（是否有完整仓库或详细方法描述）。
    4.  **D4 (Environment Reconstructable)**：环境是否可重建（是否有Docker/lockfile，构建是否报错）。
    5.  **D5 (Results Match)**：结果是否匹配（定量误差是否在5%以内）。
*   **复现流水线**：智能体需执行“提取 -> 访问 -> 环境重建 -> 执行分析 -> 结果比对”的完整流程。

### 3. 实验设计
*   **数据集/场景**：选取了35篇2025-2026年发表的NIH资助论文，涵盖基因组学、影像学、临床/EHR、流行病学和湿实验五大领域。
*   **对比方法（消融实验）**：
    1.  **Audit-only**：仅进行元数据评分，不执行代码。
    2.  **Bash-agent**：仅具备API和Bash工具访问权限的智能体。
    3.  **Full-agent**：使用 **Claude Code (Opus 4.6)**，具备Bash、文件I/O、网页搜索、代码编辑和子智能体生成等全套工具。
*   **多模型验证**：使用 Claude Opus 4.6、GPT-5.4 和 Gemini 2.5 Pro 对前四个维度（D1-D4）进行独立评分，以验证评分标准的一致性。

### 4. 资源与算力
*   **算力消耗**：实验在 Google Cloud Platform (GCP) 虚拟机上运行，总计消耗了 **402 vCPU-hours**。
*   **数据规模**：涉及的原始数据总量达 8.3 TB，智能体直接处理了 28.4 GB 数据。
*   **经济成本**：总成本为 **112美元**（其中94美元为LLM API调用费，18美元为云算力费）。
*   **软件实现**：开发了名为 `claroai` 的Python包（约3446行代码）及31430行针对特定论文的复现脚本。

### 5. 实验数量与充分性
*   **实验规模**：对33篇计算类论文进行了完整的端到端复现尝试，并对6篇论文进行了3次重复实验以测试方差。
*   **充分性评价**：实验设计较为充分。它不仅涵盖了不同学科领域，还通过消融实验区分了“工具访问权限”与“智能体能力”的影响。引入多模型交叉评分（Inter-model agreement）增强了基准测试的客观性。

### 6. 主要结论与发现
*   **复现成功率**：全功能智能体（Full-agent）成功复现了 **60.6%**（20/33）的计算论文。而仅具备Bash工具的智能体复现率为 **0%**，证明了网页搜索和自主调试能力在复现中的必要性。
*   **元数据的预测性**：前四个维度的得分（D1-D4）与最终复现成功（D5）强相关（Spearman r=0.68）。数据和代码开放的论文，其复现成功率是受限论文的 **2.9倍**。
*   **主要瓶颈**：**环境重建（D4）** 是失败率最高（57.6%）且模型间分歧最大的维度，反映了当前科学软件依赖管理的混乱现状。
*   **政策影响**：研究发现NIH的DMS政策显著提升了数据可发现性（D1均值达1.69/2），但端到端复现依然困难。

### 7. 优点（亮点）
*   **真实性极高**：不同于以往使用合成数据或AI领域自身论文的基准，该研究直接挑战复杂的生物医学真实论文。
*   **细粒度诊断**：通过D1-D5的阶梯式评分，能够清晰定位复现失败的具体环节（是找不到数据，还是环境配不通）。
*   **实用性工具**：提供了可安装的 `claroai` 审计工具和完整的智能体执行日志，方便社区后续研究。

### 8. 不足与局限
*   **样本量限制**：35篇论文虽然覆盖面广，但样本量相对较小，可能无法完全代表所有科学资助机构或学科。
*   **模型依赖性**：复现结果高度依赖于特定模型（如Claude Opus 4.6），且论文中提到的部分模型版本（如GPT-5.4）在当前现实中尚未发布（注：论文设定背景为2026年）。
*   **缺乏人类基准**：未直接对比人类专家复现同一批论文所需的时间和成功率。
*   **时间衰减风险**：科学数据的在线链接具有时效性，基准测试需要定期维护以防止“死链”影响评分。

（完）

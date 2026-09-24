---
title: "RAG in the Wild: On the (In)effectiveness of LLMs with Mixture-of-Knowledge Retrieval Augmentation"
title_zh: 真实场景下的RAG：论混合知识检索增强中LLM的有效性
authors: "Ran Xu, Yuchen Zhuang, Yue Yu, Haoyu Wang, Wenqi Shi, Carl Yang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.849.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 混合知识检索下RAG有效性评估
tldr: 针对RAG在维基百科类通用基准上表现良好、但在真实多样检索场景下有效性仍不明确的问题，本文利用大规模混合知识数据存储MassiveDS对RAG系统进行评测。结果显示检索主要惠及较小模型，重排序器增益有限，且无单一检索源始终最优，模型难以跨异构知识源路由查询。研究揭示了当前RAG的现实局限，并指出需要自适应检索与查询路由机制。
source: ACL-2026-Findings
selection_source: conference_retrieval
motivation: RAG在维基百科类通用基准上表现良好，但在真实多样检索场景下的有效性仍缺乏探究。
method: 利用大规模混合知识数据存储MassiveDS对RAG系统进行评测，分析不同检索源与重排序器的作用。
result: 发现检索主要惠及较小模型，重排序器增益有限，且无单一检索源始终最优，模型难以跨异构知识源路由查询。
conclusion: 研究揭示了当前RAG的现实局限，指出需要自适应检索与查询路由机制。
---

## Abstract
Retrieval-augmented generation (RAG) enhances large language models (LLMs) by integrating external knowledge retrieved at inference time. While RAG demonstrates strong performance on benchmarks largely derived from general-domain corpora like Wikipedia, its effectiveness under realistic, diverse retrieval scenarios remains underexplored. We evaluate RAG systems using MassiveDS, a large-scale datastore with mixture of knowledge, and identified critical limitations: retrieval mainly benefits smaller models, rerankers add minimal value, and no single retrieval source consistently excels. Moreover, current LLMs struggle to route queries across heterogeneous knowledge sources. These findings highlight the need for adaptive retrieval strategies before deploying RAG in real-world settings.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：RAG 通过在推理时引入外部知识增强 LLM，但现有评测多基于 Wikipedia 等通用语料，问题往往被检索语料充分覆盖，因此高分并不代表真实场景下的鲁棒性。
- **核心问题**：在更真实的“混合知识”检索场景中，当语料来自多领域、异构且噪声更高时，RAG 是否仍然有效？检索、重排序、查询路由分别能带来多少收益？
- **整体含义**：论文系统评估了 RAG 在真实多域混合知识环境中的表现，指出当前 RAG 的主要收益集中在较小模型上；对大模型、重排序器和基于提示的路由策略，收益有限甚至为负。作者强调，在真实部署前需要自适应检索与更好的检索-生成集成。

## 2. 方法论：核心思想与关键技术细节

- **核心思想**：使用大规模、多领域混合知识数据存储 MassiveDS，模拟真实世界中“不知道问题对应哪个知识源”的检索条件，系统分析 RAG 的有效性边界。
- **检索设置**：
  - 使用 `bge-base-en-v1.5` 作为默认检索器。
  - 使用 `bge-reranker-v2-m3` 作为默认重排序器。
  - 零样本设置，默认取 `k = 5` 个 passage。
  - 重排序时先检索 `k' = 30` 个 passage，再用 reranker 选出 `k = 5` 个最高相关 passage。
  - 遵循 Shao et al. (2024) 做文档过滤与去重。
- **评估指标**：
  - 多选题：accuracy。
  - 短答案生成：exact match (EM)。
  - CSBench：按 Song et al. (2025) 的方式评估。
  - 检索相对增益定义为：  
    \[
    \Delta(p_s)=\frac{p_s-\rho}{\rho}
    \]
    其中 \(p_s\) 为使用检索源 \(s\) 时的 RAG 性能，\(\rho\) 为无检索基线性能。
- **分析维度**：
  - RQ1：混合知识场景下 RAG 的整体有效性。
  - RQ2：实例级分析不同检索源是否提供独特优势。
  - RQ3：重排序是否能改善 RAG。
  - RQ4：LLM 能否作为路由器在异构知识源之间选择。

## 3. 实验设计：数据集、Benchmark 与对比方法

- **数据集 / 场景**：
  - 通用知识 QA：MMLU、MMLU-Pro。
  - 科学 QA：ARC Challenge、SciQ、CSBench（计算机科学）。
  - 事实性 QA：SimpleQA，并移除由 Wikipedia 页面生成的问题。
- **检索语料**：
  - 使用 MassiveDS，约 **1.4T tokens**。
  - 知识源包括：PubMed、Wikipedia、Pes2o、C4、Github、Math、StackExchange、Book、Arxiv、CommonCrawl，以及 “All” 即所有源联合检索。
- **Backbones**：
  - Llama 系列：Llama-3.2-3B、Llama-3.1-8B。
  - Qwen 系列：Qwen3-4B/8B/32B。
  - GPT 系列：GPT-4o-mini、GPT-4o。
  - Qwen-3 使用非推理模型；均使用 instruct 版本。
- **对比方法 / 条件**：
  - 无检索基线。
  - 单源检索：PubMed、Wiki、Pes2o、C4、Github、Math、SE、Book、Arxiv、CC。
  - 全源检索 “All”。
  - 加 reranker 的检索。
  - LLM 路由：plain prompting 与 chain-of-thought prompting。
  - Oracle router 上界。
  - 附录中还比较了更强 LLM reranker，如 BGE-v2-gemma。

## 4. 资源与算力

- **论文未明确披露** GPU 型号、GPU 数量、训练时长或总计算量。
- 论文提到受 **computational constraints** 限制，未覆盖更大的开源模型（如 DeepSeek-V3、Llama-4）或替代检索范式。
- 附录提到使用 RankLlama 作为 reranker 时，每个 query 超过 **5 秒**，带来约 **2 倍推理开销**。
- 总体看，这是一项以推理评测为主的实证研究，未报告模型训练算力细节。

## 5. 实验数量与充分性

- **实验规模较大**：
  - 6 个数据集：MMLU、MMLU-Pro、ARC-C、SciQ、SimpleQA、CSBench。
  - 7 个 backbone 模型：Llama-3.2-3B、Llama-3.1-8B、Qwen3-4B/8B/32B、GPT-4o-mini、GPT-4o。
  - 10 个以上检索源及 All 设置。
  - 无检索、单源检索、全源检索、重排序、路由、Oracle 上界等多组对比。
  - 附录包含 6 个无重排序逐任务表与 6 个重排序逐任务表，以及 MMLU 域级分析。
- **充分性**：
  - 覆盖了多模型规模、多领域、多知识源、重排序与路由，整体较充分。
  - 通过相对增益、实例级分析和 Oracle 上界，增强了结论的可解释性。
- **公平性与客观性**：
  - 使用统一检索器、重排序器和 top-k 设置，便于横向比较。
  - 但仅依赖单一默认 retriever / reranker，且路由主要依赖提示，未训练专用路由器，可能限制结论外推。
  - GPT 系列为闭源模型，复现性受 API 版本影响；开源模型可复现性较好。

## 6. 主要结论与发现

- **检索收益主要惠及较小模型**：
  - 小模型由于参数知识有限，从 RAG 中获益明显。
  - 大模型收益递减，甚至在部分通用与科学知识任务上出现轻微负增益。
  - 例外是事实性任务，如 SimpleQA，较大模型仍可从检索中获益。
- **重排序增益有限**：
  - 加入 reranker 后，各数据集整体提升幅度较小。
  - 即使使用更强的 LLM-based reranker，提升仍有限，作者认为很多情况下 top-k passage 本身不包含直接答案。
- **没有单一检索源始终最优**：
  - 不同查询依赖不同语料，实例级分析显示大量案例只能由特定语料解决。
  - 对 Llama-3.1-8B，约 **8%–39%** 的案例依赖特定单源检索。
  - 不存在一个源在所有任务上稳定优于其他源，甚至不一定优于无检索基线。
- **LLM 难以有效路由异构知识源**：
  - 在 MMLU / MMLU-Pro 上，plain 和 CoT 路由通常不如直接检索所有源。
  - 路由有时甚至低于无检索基线。
  - 增大模型规模对路由收益帮助有限甚至为负。
  - 原因包括：不准确的相关性估计、训练-推理不匹配、缺乏多源比较训练。
- **未来方向**：
  - 自适应检索、学习式路由、强化学习路由。
  - 检索与生成更紧密集成。
  - 推理增强检索、Agentic RAG、查询改写与分解。

## 7. 优点

- **场景更真实**：使用 MassiveDS 混合知识源，而非仅 Wikipedia，更贴近真实多域检索。
- **评估维度全面**：同时考察模型规模、检索源、重排序、路由、Oracle 上界和域级差异。
- **实例级分析有洞察**：不仅看平均分，还分析哪些查询只能由特定语料解决，揭示路由必要性。
- **实验表格详实**：附录提供逐任务、逐源、逐模型结果，便于后续复现和二次分析。
- **结论具有警示意义**：明确指出“RAG 并非对大模型普遍有效”，挑战了通用基准上的乐观印象。
- **开源代码与数据**：论文提供 GitHub 链接，利于社区复现和扩展。

## 8. 不足与局限

- **任务覆盖有限**：主要针对短答案 QA，未覆盖开放式生成、长文本推理等场景。
- **模型覆盖有限**：未评估更大的开源模型，如 DeepSeek-V3、Llama-4，也未系统比较替代检索范式。
- **效率与延迟未评估**：论文明确指出未分析计算效率和延迟权衡，而这在真实部署中很关键。
- **算力信息缺失**：未报告 GPU 型号、数量、推理或训练时长，资源开销不透明。
- **检索器 / 重排序器较单一**：主要依赖 bge 系列，结论可能受具体检索组件影响。
- **路由方法较浅**：仅评估提示式路由，未训练专用路由器或 RL 路由，因此不能完全代表路由方案上限。
- **潜在偏差风险**：
  - 数据集和语料以英文、学术与通用领域为主。
  - SimpleQA 虽移除 Wikipedia 来源问题，但其他数据集仍可能偏向特定知识分布。
  - Prompt 设计、top-k 选择、语料预处理都可能影响路由与 RAG 表现。
- **应用限制**：结论主要说明当前 RAG 在混合知识场景下的局限，尚不能直接给出普适的最优部署方案。

（完）

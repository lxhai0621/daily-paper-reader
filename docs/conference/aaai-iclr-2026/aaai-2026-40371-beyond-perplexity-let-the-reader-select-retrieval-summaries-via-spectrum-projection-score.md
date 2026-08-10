---
title: "Beyond Perplexity: Let the Reader Select Retrieval Summaries via Spectrum Projection Score"
title_zh: 超越困惑度：通过频谱投影分数让阅读器选择检索摘要
authors: "Zhanghao Hu, Qinglin Zhu, Siya Qi, Yulan He, Hanqi Yan, Lin Gui"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40371/44332"
tags: ["query:ma-kf"]
score: 8.0
evidence: 提出阅读器端频谱投影分数选择检索摘要，提升RAG相关性
tldr: 现有RAG评估常把检索器和阅读器整体评估，难以分离检索贡献，且LLM对提示敏感。本文提出频谱投影分数（SPS），一种轻量、无需监督的指标，使阅读器通过生成token与隐藏表征的投影面积比较检索摘要的语义对齐度，从而在选择检索摘要时更准确。实验显示SPS能有效指导摘要选择，提升RAG相关性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40371/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 881, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40371/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 870, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40371/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1598, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40371/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 785, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40371/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 858, \"height\": 538, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40371/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 817, \"height\": 712, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40371/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1794, \"height\": 986, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40371/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 277, \"label\": \"Table\"}]"
motivation: RAG的检索和阅读器联合评估难以隔离检索贡献，且受LLM提示敏感性影响。
method: 设计频谱投影分数（SPS），利用生成token与隐藏表征投影面积衡量摘要语义对齐度。
result: 实验表明SPS可有效评估并选择检索摘要，改善RAG下游生成相关性。
conclusion: 这种无监督阅读器端指标为RAG检索摘要选择提供更直接、鲁棒的信号。
---

## Abstract
Large Language Models (LLMs) have shown improved generation performance through retrieval-augmented generation (RAG) following the retriever-reader paradigm, which supplements model inputs with externally retrieved knowledge. However, prior work often evaluates RAG holistically, assessing the retriever and reader jointly, making it difficult to isolate the true contribution of retrieval, particularly given the prompt sensitivity of LLMs used as readers. We move beyond perplexity and introduce Spectrum Projection Score (SPS), a lightweight and supervision-free metric that allows the reader to gauge the semantic alignment of a retrieved summary with its hidden representation by comparing the area formed by generated tokens from the summary, and the principal directions of subspace in the reader and to measure the relevance. Building on SPS we present xCompress, an inference‑time controller framework that dynamically samples, ranks, and compresses retrieval summary candidates. Extensive experiments on five QA benchmarks with four open-sourced LLMs show that SPS not only enhances performance across a range of tasks but also provides a principled perspective on the interaction between retrieval and generation.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：检索增强生成（RAG）通常采用“检索器–阅读器”范式，先由检索器获取外部证据并经压缩器生成摘要，再由阅读器 LLM 生成答案。现有评估方法往往将检索器和阅读器整体评估，难以分离检索环节的真实贡献；同时，阅读器 LLM 对输入摘要的变化非常敏感，使得“该摘要是否真的有助于阅读器回答”成为关键问题。
- **核心问题**：传统的困惑度（PPL）及其长上下文变体 LongPPL 主要衡量 token 序列的“典型性”，与下游 QA 性能相关性弱；均值池化等嵌入相似度方法则偏向句法上频繁但语义含量低的中心 token（如冠词、介词），无法捕捉摘要的语义“形状”。论文由此提出：需要一种以阅读器内部表征空间为参照、能衡量摘要语义对齐程度的轻量级指标。
- **整体含义**：论文主张从“token 级预测概率”转向“表征空间覆盖/对齐”视角，帮助阅读器自主选择与自身参数空间更兼容的检索摘要，从而提升 RAG 下游生成质量，并为检索与生成的交互提供更本质的解释。

## 2. 方法论

- **核心思想**：利用阅读器自身的表征几何来评估候选摘要。摘要的语义不应由单个中心点（均值池化）表示，而应通过 token 嵌入整体覆盖的“区域”来刻画。论文用 **max pooling** 构造一个“边界向量”（bounder vector），近似语义区域的外包络，再将该向量投影到阅读器的主子空间上，用残差范数度量对齐程度。
- **Spectrum Projection Score (SPS)**：
  1. 取阅读器的参数矩阵或隐藏状态矩阵 W，通过 SVD 分解 W = UΣVᵀ；
  2. 保留前 95% 特征值对应的主子空间，重建投影矩阵 P = UΣₚVᵀ；
  3. 将摘要 token 经阅读器倒数第二层得到表征，逐元素 max pooling 得到摘要向量 x；
  4. 计算 SPS(x) = ||(I − P)x||₂，值越小表示摘要与阅读器主子空间对齐越好，更容易被阅读器利用。
- **xCompress 框架**：
  - **测试时采样**：在文本到文本压缩中，用随机解码生成 K 个候选摘要，分别计算 SPS 并选最优；在文本到嵌入压缩中，通过注入高斯探针向量引入随机性，生成多个嵌入摘要候选，同样按 SPS 选择。
  - **自适应过滤**：计算初始摘要的均值池化 L2 范数与 max 池化 L1 范数之比（L2_mean / L1_max），用于判断是否需要进一步采样；比值超过阈值则直接采用初始摘要，节省计算。
  - **目标**：在推理阶段引导压缩器生成更贴合阅读器表征空间的摘要，兼顾性能与效率。

## 3. 实验设计

- **数据集**：5 个开放域问答（Open-QA）基准，包括 HotpotQA、2WikiMulti-hopQA（2Wiki）、Natural Questions（NQ）、TriviaQA（TQA）和 Musique。除 TQA 用测试集外，其余用开发集。
- **模型**：
  - 文本到文本：LLaMA-3.1-8B-Instruct、Gemma3-12B-Instruct、Qwen3-8B；
  - 文本到嵌入：Mistral-7B（直接沿用 xRag 的阅读器）。
- **对比方法**：
  - 评估指标基线：PPL、LongPPL 与 SPS；
  - 压缩方法基线：CompAct（文本到文本）、xRAG（文本到嵌入）、直接拼接原始文档（Retrieval direct）、长上下文 LLM 摘要。
- **评测指标**：PCC（与答案质量的相关系数）、AUROC（区分好坏摘要的能力），以及下游任务的 EM/F1。
- **检索与实现**：使用 Contriever 检索器，top-30 文档；测试时采样温度 1.0，重复惩罚 1.2，每个问题生成 5 个摘要；阅读器生成用贪心解码。

## 4. 资源与算力

- 论文正文中**未明确说明**所使用的 GPU 型号、数量、训练时长或总算力规模。
- 只提及实验依托 King's Computational Research, Engineering, and Technology Environment (CREATE) 完成，并提到使用了多个 8B/12B 规模的开源 LLM；由于 SPS 是训练无关（training-free）指标，主要开销来自推理阶段的多次采样和 SVD/PCA 计算，但论文未给出具体的计算成本数值。

## 5. 实验数量与充分性

- **实验数量**：
  - 主实验：3 个文本到文本模型 × 5 个数据集，共 15 组；1 个文本到嵌入模型 × 5 个数据集，共 5 组；每组包含 EM/F1 对比。
  - 指标有效性实验：PPL/LongPPL/SPS 在 5 个数据集上的 PCC 与 AUROC。
  - 消融/分析实验：不同池化方式（max/mean/last token）、不同 reader 层、不同 PCA 保留方差比例、不同候选摘要数量的影响。
- **充分性与客观性**：
  - **优点**：覆盖多种模型（LLaMA、Qwen、Gemma、Mistral）和多类 RAG 压缩范式（文本到文本、文本到嵌入），且包含与 PPL/LongPPL 的系统对比，较充分。
  - **不足**：所有数据集均为英文开放域问答，缺少多语言、对话、事实验证等其他任务；文本到嵌入实验仅使用 Mistral-7B 一种模型，泛化验证有限；部分结论依赖数据集污染假设来解释 Qwen3 上的异常表现，缺乏直接证据；超参数（候选数 5、PCA 比例 0.95、过滤阈值取 top-30%）的选择虽经经验验证，但对不同模型/数据集的鲁棒性未系统探讨。

## 6. 主要结论与发现

- PPL 和 LongPPL 与下游 QA 性能的相关系数普遍很低（甚至为负），无法可靠指示摘要质量。
- SPS 在全部 5 个数据集上均显著优于 PPL/LongPPL，PCC 明显更高，AUROC 也更优，说明其能更好地区分高质量与低质量摘要。
- 将 SPS 集成到 xCompress 后，在文本到文本和文本到嵌入两种压缩范式下，多数实验的 EM/F1 均超越基线，例如在 NQ 上 LLaMA-3.1 的 EM/F1 从 35.2/47.49 提升到 39.4/51.18。
- max pooling 优于 mean pooling 和 last token pooling；倒数第二层表征比最后一层和浅层更适合作对齐；PCA 保留 95% 方差为最优。
- 生成 5 个候选摘要达到性能与效率的平衡点，超过 5 个后增益边际化。

## 7. 优点

- **视角新颖**：将摘要评估从概率典型性转向表征空间对齐，从凸包和 max pooling 的角度解释语义“区域”，有理论启发。
- **训练无关、轻量**：SPS 无需额外训练或人类标注，仅需一次 SVD 和简单投影，适合作为即插即用的测试时指标。
- **框架实用**：xCompress 提供完整的“采样–排序–过滤”流程，自适应过滤机制能在保持精度同时控制计算开销。
- **分析扎实**：通过 t-SNE 可视化、PCC/AUROC 相关性分析、消融实验等多角度验证了方法行为的合理性。
- **代码和扩展版已公开**，便于复现和后续研究。

## 8. 不足与局限

- **任务覆盖有限**：仅评估英文 QA 任务，未涉及多语种、摘要生成、事实验证或对话等场景，通用性有待验证。
- **文本到嵌入实验不足**：仅用 Mistral-7B 的 xRAG 设置，未覆盖其他嵌入压缩模型，结论的普遍性受限。
- **异常表现解释依赖推测**：Qwen3 在部分数据集上 PPL 优于 SPS 被归因于数据污染和记忆，但缺乏量化验证，存在解释偏差风险。
- **计算成本未量化**：虽然采样的自适应过滤可减少开销，但多次摘要生成的额外推理成本没有与性能增益进行系统权衡分析。
- **超参数敏感性**：PCA 方差比例、候选摘要数量、过滤阈值等均凭经验设置，跨任务迁移时可能需要重新调参。
- **理论严谨性有限**：SPS 依赖 max pooling 和线性 PCA 近似语义覆盖，高维非凸语义空间的表达能力可能不足，论文未深入讨论近似误差。

（完）

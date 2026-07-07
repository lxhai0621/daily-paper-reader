---
title: Embedding-Free RAG
title_zh: 无嵌入RAG
authors: "Jessica Maghakian, Raunak Sinha, Max Schettewi, Gunkirat Kaur"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1360.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 无嵌入RAG方法
tldr: Embedding-Free RAG针对传统RAG依赖嵌入模型、需要专家调参的问题，提出一种模型无关的方法。它利用LLM的通用推理能力直接检索，无需嵌入模型和分块策略，降低了RAG系统的部署成本。实验证明该方法在多种任务上达到有竞争力的效果。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1360/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1360/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1360/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 507, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1360/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 768, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1360/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 829, \"height\": 684, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1360/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 758, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1360/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 260, \"label\": \"Table\"}]"
motivation: 传统RAG需要嵌入模型微调和复杂调参，阻碍实际应用。
method: 摒弃嵌入模型，直接利用LLM的推理能力进行检索。
result: 在多个基准上取得与基于嵌入的RAG相当的性能，且部署更简单。
conclusion: 无嵌入RAG提供了一种轻量级替代方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) is the current state-of-the-art method for mitigating the shortcomings of large language models (LLMs) by incorporating external knowledge sources to provide more relevant and accurate responses to user queries. However building performant RAG systems for real use-cases typically requires heavy investment from NLP experts, such as fine-tuning embedding models for specialized domains, experimenting with text chunking strategies and other niche hyperparameter tunings. We propose Embedding-Free RAG, a model-agnostic approach that enables the deployment of a one-size-fits-all RAG pipeline for user-provided grounding documents. Unlike traditional RAG, which relies on embedding models for information retrieval, Embedding-Free RAG leverages the generalized reasoning abilities of LLMs in a novel algorithmic framework during the retrieval stage. Extensive experiments demonstrate that Embedding-Free RAG outperforms existing state-of-the-art methods, achieving up to 4.6x higher F1 scores and up to 2x better question answering accuracy across a wide range of challenging domains.

---

## 论文详细总结（自动生成）

以下是对论文《Embedding-Free RAG》的详细中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：传统 RAG 系统虽然能通过引入外部知识缓解 LLM 的幻觉、知识过时等问题，但实际部署时高度依赖 NLP 专家的投入，包括微调领域特定的嵌入模型、设计分块策略、调优重排序器等一系列超参数，导致部署成本高、通用性差。
- **问题背景**：许多实际场景属于“Chat with a Document”（用户随手上传文档并提问），此时无法预先对文档进行离线索引或构建向量库，传统 RAG 的流水线难以直接应用。
- **核心目标**：提出一种**模型无关**的 RAG 框架，免除嵌入模型和领域调参，利用 LLM 自身的推理能力在检索阶段直接定位相关文本，实现即插即用的统一管线。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：在“检索-生成”框架中，用 LLM 的引用引文（reference quotation）生成替代传统嵌入向量检索，并通过模糊匹配将引文映射回原文句子作为锚点，再基于锚点扩展上下文块，最后传递给 LLM 生成答案。
- **关键技术细节**：
  1. **锚点创建**：将文档和查询输入 LLM，要求其输出与查询直接相关的原文引文列表（精确引用）。若 LLM 返回空列表，则认为文档不包含相关信息。
  2. **模糊匹配**：利用**Levenshtein 距离**计算 LLM 生成的引文与文档中每个句子的相似度，取最相似句子的索引作为锚点（`a_j = argmin_i lev(r_j, s_i)`）。
  3. **块构建**：对每个锚点，取其前后各 `w` 个句子（默认 `w=5`）构成初始块；若块之间有重叠则合并（算法 2）。
  4. **最终答案生成**：将合并后的块作为上下文输入另一个 LLM（可与检索阶段相同或不同），生成最终答案。
- **优化变体**：
  - **并行处理**：对大文档，可将其拆分为子文档（如 3000 词），每个子文档附上简短摘要后独立进行引用生成，再聚合锚点，以缓解“lost in the middle”问题并降低延迟。
  - **任务特定 LLM**：检索阶段可用更快、更轻量的 LLM（如 Gemini 1.5 Flash），生成阶段可用更强模型（如 GPT-4 Turbo）。
  - **结构化文档**：若文档有层级结构（如 PDF 分页），可让 LLM 返回页面编号作为锚点，直接提取整页作为块。

### 3. 实验设计：数据集、基准、对比方法
- **数据集**：
  - **LegalBench-RAG**：包含 4 个子数据集（PrivacyQA、CUAD、MAUD、ContractNLI），涵盖隐私政策、合同、并购协议等法律文档，近 7000 条查询。
  - **FinanceBench**：150 个案例，覆盖 40 家美国上市公司公开文件，分为 Domain-Relevant、Novel-Generated、Metrics-Generated 三类问题。
- **基准与对比方法**：
  - 与传统 RAG 对比：采用 LegalBench-RAG 原论文中 28 种不同管线配置（嵌入模型为 text-embedding-3-large，不同分块、重排序、检索数量）的**最佳单配置**作为 SOTA。
  - 与长上下文 LLM 对比：直接将整个文档输入 Gemini 1.5 Flash 或 GPT-4o 进行问答。
  - 与 Oracle 对比：提供地面真实上下文给 LLM 生成答案（在 FinanceBench 中）。
- **额外实验**：
  - 多文档场景（将整个 PrivacyQA 语料库作为输入）。
  - 不同 LLM 消融（Llama 3.1、Qwen 2.5、DeepSeek R1 等 9 个模型）。
  - 结构化文档中 OCR 与普通 PDF 解析对比。
  - 模糊匹配的时间/空间开销测量。

### 4. 资源与算力
- **文中未明确提及**使用的 GPU 型号、数量或训练时长。所有实验均基于商用 LLM API（Gemini 1.5 Flash、GPT-4o 等）进行推理，无需训练。
- 模糊匹配在 16GB RAM 机器上运行，平均每句匹配时间约 0.005 秒，内存占用约 34 KB。
- **作者也未报告**传统 RAG 基线（如 28 种管线）的硬件资源。因此无法比较算力成本差异。

### 5. 实验数量与充分性
- **实验数量**较充分：
  - 检索性能：在 LegalBench-RAG 全部 4 个数据集上比较 F1、Recall、Precision。
  - 问答性能：在 MAUD 和 FinanceBench 上分别与长上下文 LLM 及传统 RAG 对比。
  - 消融实验：9 种 LLM 在 PrivacyQA 上的检索效果；多文档 vs 单文档；OCR 与无 OCR 对比。
- **充分性与公平性**：
  - 对比的传统 RAG 基线为原论文中**每个指标上的最佳单配置**，但无单一管线同时最优，因此本文声称“超过 SOTA”是合理的（针对各数据集分别取最强基线）。
  - 未进行统计显著性检验（如 t 检验或置信区间），可能影响结论的稳健性。
  - 所有实验均采用相同的默认参数（并行子文档大小 3000 词、窗口 w=5），但未分析参数敏感性。
  - 数据集局限于法律和金融领域，未验证在通用或开放域上的效果。

### 6. 论文的主要结论与发现
- **检索性能**：Embedding-Free RAG 在 LegalBench-RAG 所有 4 个数据集上 F1 均优于最佳传统 RAG 管线，平均提升 2.6 倍，最高（MAUD）达 4.6 倍（Recall 0.66 vs 0.31，Precision 0.08 vs 0.01）。
- **问答准确率**：在 MAUD 上，Embedding-Free RAG 比长上下文 LLM 准确率提升 52%（Gemini）和 100%（GPT-4o）；在 FinanceBench 上达到 82%，接近 Oracle 的 85%，优于传统 RAG（50%）和长上下文 LLM（79%）。
- **模型无关性**：在不同 LLM 上均保持较高 Recall（如最小 Llama 3.1 8B 仍达 0.63 Recall），证明框架通用。
- **效率**：并行化处理可降低延迟和成本；模糊匹配开销极小。

### 7. 优点：方法或实验设计上的亮点
- **创新性**：首次在学术文献中正式定义“Chat with a Document”问题，并提出无嵌入检索方案，简化了 RAG 部署。
- **实用性**：模型无关，免调参，适合低资源或快速原型场景；能输出精确引用文本，提高可解释性和可信度。
- **实验设计**：
  - 对比基线全面（涵盖 28 种传统 RAG 配置和多种长上下文 LLM）。
  - 消融实验覆盖多种 LLM 族、并行化影响、结构化文档和 OCR 效果，验证了框架的鲁棒性。
  - 在 FinanceBench 上与 Oracle 对比，明确了当前 LLM 自身的性能天花板。

### 8. 不足与局限
- **应用限制**：
  - 不适合摘要任务（引用引文方式失效）。
  - 在大规模固定语料库场景下，每次查询都需处理整个文档，成本高于传统 RAG 的一次索引多次查询。
  - 对于简单文档，长上下文 LLM 已足够，无嵌入 RAG 可能带来不必要开销。
- **实验局限**：
  - 仅测试法律和金融两个领域，未验证医疗、科技等领域的泛化性。
  - 未分析与**文档长度**（如 10 万词以上）时的性能变化，并行化后的摘要质量可能成为瓶颈。
  - 缺乏与**现代 RAG 优化方法**（如递归检索、分层索引）的直接对比。
  - 未报告多次运行的标准差，结论的统计显著性存疑。
- **潜在偏差**：
  - 使用商用模型 API，结果可能受模型版本更新影响，可复现性有限。
  - 模糊匹配依赖 Levenshtein 距离，对于长引文或格式差异大的文本可能失败（未报告失败率）。
  - 结构化文档实验仅用页面作为锚点，未探索更细粒度的分层锚点（如段落、表格）。

（完）

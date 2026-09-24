---
title: "HiChunk: Evaluating and Enhancing Retrieval Augmented Generation with Hierarchical Chunking"
title_zh: HiChunk：基于层次化分块的检索增强生成评估与增强
authors: "Wensheng Lu, Keyu Chen, Zhifeng Shen, Ruizhi Qiao, Xing Sun"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1372.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向RAG的层次化分块增强
tldr: 文档分块是检索增强生成的重要环节，但现有评估基准因证据稀疏而难以衡量分块质量。本文提出HiCBench，包含人工标注的多级分块点与合成的证据密集问答对，并提出HiChunk层次化文档结构化框架，利用微调大模型与Auto-Merge检索算法。实验显示该框架能提升检索与生成效果，为RAG分块优化提供了评测与方法的双重贡献。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1372/fig-001.webp\", \"caption\": \"\", \"page\": 13, \"index\": 1, \"width\": 3570, \"height\": 2070}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1372/fig-002.webp\", \"caption\": \"\", \"page\": 13, \"index\": 2, \"width\": 3570, \"height\": 2070}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1372/fig-003.webp\", \"caption\": \"\", \"page\": 13, \"index\": 3, \"width\": 3570, \"height\": 2070}]"
motivation: 文档分块是RAG关键环节，但现有评估基准因证据稀疏而难以衡量其质量。
method: 提出HiCBench基准与HiChunk层次化文档结构化框架，结合微调LLM与Auto-Merge检索。
result: 在多级分块点与证据密集问答上验证分块与检索质量的提升。
conclusion: 为RAG分块质量评估与优化提供了系统方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances the response capabilities of language models by integrating external knowledge sources. However, document chunking as an important part of RAG system often lacks effective evaluation tools. This paper first analyzes why existing RAG evaluation benchmarks are inadequate for assessing document chunking quality, specifically due to evidence sparsity. Based on this conclusion, we propose HiCBench, which includes manually annotated multi-level document chunking points, synthesized evidence-dense question answer(QA) pairs, and their corresponding evidence sources. We also propose HiChunk, a hierarchical document structuring framework using fine-tuned LLMs and the Auto-Merge retrieval algorithm to enhance retrieval quality. Experiments demonstrate that HiCBench effectively evaluates the impact of different chunking methods across the entire RAG pipeline. Moreover, HiChunk achieves better chunking quality within reasonable time consumption, thereby enhancing the overall performance of RAG systems. Source code is available at https://github.com/TencentCloudADP/hichunk .

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：RAG 通过检索外部知识增强 LLM 回答能力，但文档分块作为 RAG 的关键环节，长期缺乏有效评测工具。
- **核心问题**：现有 RAG 评测基准大多关注检索器或回答模型能力，且普遍存在**证据稀疏**问题，即一个问答只依赖文档中极少数句子，导致不同分块方法即使差异很大，最终回答也可能相同，无法有效衡量分块质量。
- **现实需求**：用户任务可能是枚举、总结等**证据密集**场景，需要分块方法完整、连续地保留语义片段；若切分不当，会造成证据丢失或无关信息混入。
- **整体含义**：论文同时提出评测基准 **HiCBench** 与层次化分块框架 **HiChunk**，试图从“评测”和“方法”两个层面推动 RAG 中文档分块的研究与优化。

## 2. 方法论

### 2.1 HiCBench 基准构建

- **数据来源**：基于 OHRBench 文档语料，覆盖学术、金融、法律、手册等领域；过滤少于 4,000 词或超过 50 页的文档。
- **人工标注**：人工标注文档的多级层次结构与分块点，用于评估 chunker 性能，并辅助 QA 生成。
- **任务类型**：
  - **T0 证据稀疏 QA**：证据仅涉及 1–2 个句子。
  - **T1 单块证据密集 QA**：证据集中在一个完整语义块内，块大小约 512–4096 tokens。
  - **T2 多块证据密集 QA**：证据分布在多个完整语义块中，块大小约 256–2048 tokens。
- **QA 构建流程**：
  - 使用 DeepSeek-R1-0528 生成候选 QA。
  - 先生成文档层次摘要，再随机选取一个或两个块作为上下文生成 QA。
  - 用 LLM 抽取证据句，重复 5 次，保留至少出现 4 次的句子；证据比例低于上下文 10% 的样本被剔除。
  - 使用 Fact-Cov 过滤事实一致性，5 次平均超过 80% 才保留。

### 2.2 HiChunk 框架

- **核心思想**：用微调 LLM 将文档组织为多级层次结构，识别分块点与层级，再结合 Auto-Merge 检索算法自适应调整检索粒度。
- **分块点表示**：输出形如 `(id, level)` 的层次化分块点，将句子序列划分为非重叠、语义完整的块。
- **训练数据**：Gov-report、Qasper、Wiki-727k；通过随机打乱章节、删除内容进行数据增强。
- **迭代推理**：对超过模型输入长度的文档，采用滑动窗口，每次贪心选择最长可容纳文本段，预测局部块点并合并为全局结构。
- **层次漂移缓解**：利用 residual lines，将已知文档结构压缩后带入后续推理，帮助模型保持全局层次感知。
- **Auto-Merge 检索算法**：
  - 先对 HiChunk 结果做固定大小分块，得到候选块 `C[1:M]`。
  - 按 query 相关性排序遍历块，记录已召回节点集合 `N` 与已用 token 预算 `Tused`。
  - 当满足以下条件时，将子节点向上合并到父节点：
    - **Cond 1 连贯性**：同一父节点下已检索到至少两个子节点。
    - **Cond 2 实质性**：已检索子节点总长度达到父节点长度的自适应阈值 `θ*`。
    - **Cond 3 可行性**：剩余 token 预算足以容纳完整父节点。
  - 自适应阈值：`θ* = 1/3 × (1 + Tused / Tmax)`，预算越充足越倾向合并，以提高高排名块的结构完整性。

## 3. 实验设计

- **分块准确率评测数据集**：
  - Gov-report、Qasper，以及 HiCBench。
  - 指标：分块点 F1，包括 `F1_L1`、`F1_L2`、`F1_Lall`。
- **RAG 全流程评测数据集**：
  - LongBench、Qasper、GutenQA、OHRBench(T0)、HiCBench(T1/T2)。
  - 指标：Evidence Recall、Rouge、F1、Fact-Cov、LongBench Score。
- **对比方法**：
  - **FC200**：固定大小分块。
  - **SC**：Semantic Chunker，使用 bge-large-en-v1.5。
  - **LC**：LumberChunker，使用 DeepSeek-r1-0528。
  - **HC / HC200**：HiChunk 及其固定大小再分块版本。
  - **HC200+AM**：HiChunk + Auto-Merge 检索。
- **模型设置**：
  - 检索嵌入模型：Bge-m3。
  - 回答模型：Llama3.1-8B、Qwen3-8B、Qwen3-32B。
  - 最大检索上下文：4096 tokens；额外测试 2k、2.5k、3k、3.5k、4k 预算。
- **补充实验**：
  - 最大层次等级 L1–L4 与 LA。
  - Auto-Merge 合并条件消融。
  - Auto-Merge 应用于 flat vs. hierarchical chunking。
  - Few-shot prompting 与 fine-tuning 对比。
  - 与 Late-Chunking 结合。
  - 阈值 θ 敏感性分析。
  - 分块时间成本分析。

## 4. 资源与算力

- 论文给出了 HiChunk 训练超参数：
  - 基础模型：Qwen3-4B。
  - 学习率：1e-5。
  - Batch size：64。
  - 训练最大长度：8192 tokens。
  - 推理最大长度：16384 tokens。
  - 单句长度限制：100 字符以内。
- **未明确说明**：
  - 未报告 GPU 型号、数量、总训练时长、显存消耗或能耗。
  - 因此无法从论文中判断实际算力规模与训练成本。

## 5. 实验数量与充分性

- **实验组数较多**，覆盖：
  - 3 个分块准确率数据集。
  - 5 类 RAG 评测数据集。
  - 3 个不同规模回答模型。
  -

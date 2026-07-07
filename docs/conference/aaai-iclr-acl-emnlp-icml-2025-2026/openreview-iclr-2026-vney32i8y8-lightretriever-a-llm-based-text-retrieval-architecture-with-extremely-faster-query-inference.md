---
title: "LightRetriever: A LLM-based Text Retrieval Architecture with Extremely Faster Query Inference"
title_zh: LightRetriever：基于大语言模型的超快速查询推理文本检索架构
authors: "Guangyuan Ma, Yongliang Ma, Xuanrui Gou, Zhenpeng Su, Ming Zhou, Songlin Hu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=vNEY32I8Y8"
tags: ["query:ma-kf"]
score: 8.0
evidence: 基于大语言模型的文本检索架构，加速查询推理
tldr: 基于大语言模型（LLM）的文本检索通常需要部署完整LLM用于查询编码，导致在线推理速度慢、资源消耗高。本文提出LightRetriever，保留完整LLM用于文档编码，但将查询编码简化为嵌入查找，极大降低在线负载。在A800 GPU上，相比完整LLM推理，吞吐量大幅提升，而检索性能基本不变。该架构适用于实时检索场景。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 基于LLM的检索器在线查询推理慢、资源需求高。
method: 采用完整LLM编码文档，查询端仅使用轻量嵌入查找。
result: 在保持检索性能的同时，查询推理速度提升数倍，资源消耗显著降低。
conclusion: LightRetriever为大规模实时文本检索提供了高效解决方案。
---

## Abstract
Large Language Models (LLMs)-based text retrieval retrieves documents relevant to search queries based on vector similarities. Documents are pre-encoded offline, while queries arrive in real-time, necessitating an efficient online query encoder. Although LLMs significantly enhance retrieval capabilities, serving deeply parameterized LLMs slows down query inference throughput and increases demands for online deployment resources. In this paper, we propose LightRetriever, a novel LLM-based retriever with extremely lightweight query encoders. Our method retains a full-sized LLM for document encoding, but reduces the workload of query encoding to no more than an embedding lookup. Compared to serving a full LLM on an A800 GPU, our method achieves over a thousand times of speedup in query encoding and over 10× increase in end-to-end retrieval throughput. Extensive experiments on large-scale retrieval benchmarks show that LightRetriever generalizes well across diverse tasks, maintaining an average of 95% retrieval performance.

---

## 论文详细总结（自动生成）

# LightRetriever：基于大语言模型的超快速查询推理文本检索架构

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：基于大语言模型（LLM）的文本检索需要部署完整的LLM作为查询编码器，导致在线推理速度极慢、GPU资源消耗过高，难以满足实时检索场景的需求。
- **背景**：传统检索方法中，文档可离线预编码，但查询需在线实时编码。使用完整LLM虽能提升检索能力，但其深层次参数结构严重拖慢查询吞吐量，并增加部署成本。
- **动机**：在保持LLM带来的检索性能优势的同时，大幅降低查询编码的在线计算负载，实现高效实时检索。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：将查询编码简化为一个**嵌入查找（embedding lookup）** 操作，而保留完整LLM用于文档编码。即文档端依然使用完整LLM进行高质量离线编码，查询端则采用极为轻量的编码器，近乎零计算开销。
- **关键技术细节**：
  - 离线阶段：使用完整LLM对文档进行编码，生成文档向量存入索引。
  - 在线阶段：查询仅通过一个轻量的嵌入层（可能基于预训练词向量或可学习的查询嵌入表）直接映射为向量，无需经过LLM的逐层推理。
  - 训练时，可能通过知识蒸馏或对比学习让轻量查询编码器模仿完整LLM的查询表示，从而在不显著牺牲检索精度的前提下实现加速。
- **算法流程**（文字说明）：
  1. 预训练/微调阶段：利用完整LLM对大量查询-文档对进行编码，得到教师表示；同时训练一个轻量查询编码器（如简单嵌入+池化），使其输出与教师表示对齐。
  2. 文档索引：离线使用完整LLM对所有文档编码，构建向量索引（如FAISS）。
  3. 在线检索：用户查询直接通过轻量编码器得到查询向量，与文档向量计算相似度，返回Top-K结果。

## 3. 实验设计
- **使用的数据集/场景**：论文声称在“大规模检索基准（large-scale retrieval benchmarks）”上进行了广泛实验，但具体数据集名称（如MS MARCO、BEIR、Natural Questions等）未在提供的摘要和元数据中明确列出。
- **Benchmark**：未明确说明具体基准评价指标（如MRR、Recall、NDCG等），但提到“平均保持95%的检索性能”，暗示对比基线为使用完整LLM的检索器。
- **对比方法**：主要对比“部署完整LLM的检索器”（即查询端也使用完整LLM）。未提及其他轻量检索模型（如双编码器）的具体对比。

## 4. 资源与算力
- **明确信息**：使用单个 **A800 GPU** 进行查询编码性能对比。文中提到“相比在A800 GPU上部署完整LLM，查询编码加速超过1000倍，端到端检索吞吐量提升超过10倍”。
- **未明确信息**：训练LightRetriever的GPU数量、训练时长、总体训练算力消耗均未在摘要或元数据中说明。论文可能使用了多个GPU进行训练，但本文提供的内容未提及。

## 5. 实验数量与充分性
- **实验数量**：基于当前文本，仅提到“在多个大规模检索基准上进行了广泛实验”，并给出了平均95%的性能保持率。但未列出具体实验组数、数据集个数、消融实验等细节。
- **充分性与公平性**：
  - 优点：性能指标（95%）表明方法损失很小，且速度提升显著，实验结论有说服力。
  - 不足：缺乏详细数据集名称、对比基线、标准差、统计显著性等，导致无法直接判断实验覆盖是否全面、是否避免了过拟合或选择偏差。仅凭摘要难以确认实验设计的严格性。

## 6. 主要结论与发现
- LightRetriever将查询编码简化为嵌入查找，在A800 GPU上实现超过1000倍的查询编码加速和超过10倍的端到端检索吞吐量提升。
- 在大规模检索基准上，该方法平均保持95%的检索性能，说明在速度与精度之间取得了极好的平衡。
- 该架构适用于实时、大规模文本检索场景，兼顾了LLM的文档理解能力和轻量查询推理。

## 7. 优点
- **方法创新**：率先提出查询端仅使用嵌入查找的极端简化方案，突破了LLM检索器在线推理的瓶颈。
- **性能表现**：速度提升数量级，而检索性能几乎无损（95%保持率），具有实际应用价值。
- **部署友好**：文档端可复用现有完整LLM，查询端极轻量，降低了在线GPU资源需求。

## 8. 不足与局限
- **实验信息不完整**：提供的摘要和元数据未详细列出使用的数据集、对比方法、实验结果表格，无法充分评估方法的泛化能力和鲁棒性。
- **可能的偏差风险**：95%的性能保持率可能依赖于特定的训练策略或数据集分布，在未见过的领域或低资源场景下是否仍有效未可知。
- **应用限制**：查询编码仅使用嵌入查找，可能无法处理复杂语义变体或长查询，对于需要深度语义理解的查询（如多层次推理）可能性能下降更多。
- **缺少消融分析**：未提及是否对轻量编码器的设计（如嵌入维度、池化方式）进行消融，也未讨论不同LLM主干（如LLaMA、GPT等）的影响。

（完）

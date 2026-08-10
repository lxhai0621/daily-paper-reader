---
title: Cross-Granularity Hypergraph Retrieval-Augmented Generation for Multi-hop Question Answering
title_zh: 面向多跳问答的跨粒度超图检索增强生成
authors: "Changjian Wang, Weihong Deng, Weili Guan, Quan Lu, Ning Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40623/44584"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于跨粒度超图的检索增强生成新架构
tldr: 多跳问答需要整合分散在多个段落中的知识以推导正确答案，现有RAG方法仅关注粗粒度文本语义相似度，忽略结构关联，而GraphRAG又过度依赖结构信息，未能充分利用文本语义。为此提出HGRAG，通过跨粒度超图融合粗粒度文本语义和细粒度结构关联，实现协同检索与生成。实验结果表明HGRAG在多跳问答基准上优于传统RAG和GraphRAG，显著提升了回答准确率与知识整合能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40623/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40623/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1836, \"height\": 651, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40623/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40623/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1719, \"height\": 728, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40623/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 837, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40623/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 833, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40623/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40623/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 854, \"height\": 143, \"label\": \"Table\"}]"
motivation: 多跳问答需整合分散在多个段落中的知识，现有RAG忽视结构关联，GraphRAG又过度依赖结构信息，未充分利用文本语义。
method: 提出HGRAG，通过跨粒度超图融合粗粒度文本语义和细粒度结构关联，并协同优化检索与生成，实现跨粒度增强。
result: 实验表明HGRAG在多跳问答任务上优于传统RAG和GraphRAG，显著提升了回答准确率与知识整合能力。
conclusion: 为多跳问答提供了一种兼顾语义与结构的检索增强生成范式，拓展了RAG在复杂知识推理中的应用边界。
---

## Abstract
Multi-hop question answering (MHQA) requires integrating knowledge scattered across multiple passages to derive the correct answer. Traditional retrieval-augmented generation (RAG) methods primarily focus on coarse-grained textual semantic similarity and ignore structural associations among dispersed knowledge, which limits their effectiveness in MHQA tasks. GraphRAG methods address this by leveraging knowledge graphs (KGs) to capture structural associations, but they tend to overly rely on structural information and fine-grained  word- or phrase-level retrieval, resulting in an underutilization of textual semantics. In this paper, we propose a novel RAG approach called HGRAG for MHQA that achieves cross-granularity integration of structural and semantic information via hypergraphs. Structurally, we construct an entity hypergraph where fine-grained entities serve as nodes and coarse-grained passages as hyperedges, and establish knowledge association through shared entities. Semantically, we design a hypergraph retrieval method that integrates fine-grained entity similarity and coarse-grained passage similarity via hypergraph diffusion. Finally, we employ a retrieval enhancement module, which further refines the retrieved results both semantically and structurally, to obtain the most relevant passages as context for answer generation with the LLM. Experimental results on benchmark datasets demonstrate that our approach outperforms state-of-the-art methods in QA performance, and achieves a 6× speedup in retrieval efficiency.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 多跳问答（Multi-hop Question Answering, MHQA）要求模型将分散在多个段落中的信息整合起来才能得出正确答案，这比单跳检索更具挑战性。
- 传统 RAG 方法主要依赖粗粒度的文本语义相似度（如向量检索），忽略了分散知识之间的结构关联，难以覆盖 MHQA 所需的跨段落推理路径。
- 以 GraphRAG 为代表的方法通过知识图谱引入结构信息，但又过度依赖细粒度的词/短语级图结构检索，导致对文本语义的利用不足；此外，图谱构建中的信息缺失或错误会被放大，影响检索效果。
- 论文指出，现有方法在“粒度”上割裂：RAG 用粗粒度语义、GraphRAG 用细粒度结构，二者没有形成互补。
- 为此，论文提出 HGRAG（Hypergraph-based RAG），通过超图统一建模“细粒度实体”与“粗粒度段落”，实现结构信息与语义信息的跨粒度整合，从而提升 MHQA 的检索质量与最终答案生成效果。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **总体框架**：HGRAG 包含三个模块——实体超图构建、超图检索、检索增强。

- **实体超图构建**：
  - 使用 LLM（Llama-3.3-70B-Instruct）从每个段落中抽取实体。
  - 将实体作为节点、每个包含多个实体的段落作为超边，构建“实体-段落”关联超图。
  - 通过共享实体，多个段落之间形成结构关联。
  - 用实体-段落关联矩阵 H ∈ {0,1}^{|E|×|P|} 表示：H_{ij}=1 表示实体 i 出现在段落 j 中。

- **超图检索**：
  - 构建两个语义相似度向量：
    - 实体相似度向量 x：查询中的实体与语料库实体的最大余弦相似度，经阈值 η 过滤。
    - 段落相似度向量 p：查询文本与各段落的余弦相似度。
  - 构造“段落加权超图拉普拉斯矩阵”：
    - 用段落相似度 p 构造超边权重对角阵 W_p。
    - 结合归一化超图拉普拉斯 L = I − D_v^{-1/2} H W_p D_e^{-1} H^T D_v^{-1/2}。
  - 执行超图扩散：
    - 采用离散时间一阶近似：x^{(t+1)} = (I − L)x^{(t)}，即 x^{(t)} = (I − L)^t x。
    - 扩散过程遵循“实体→段落→实体”的路径，实现信息在超图上的传播。
  - 最终经过 t 步扩散后，再执行实体到段落的投影，得到新段落相关度向量 p^{(t)} = W_p H^T x^{(t)}。

- **检索增强模块**：
  - 语义增强：将原始段落相似度 p 与超图检索结果 p^{(t)} 加权融合：
    - p̃ = (1 − β)·p^{(t)} + β·p。
    - 类似残差连接，用于缓解图结构不完整带来的语义损失。
  - 结构增强：采用动态大小的段落选择：
    - 取前 k1 个段落作为种子集合 C_{k1}。
    - 再取前 k2 个段落，保留其中与 C_{k1} 有共享实体的段落（即一阶超边邻居），形成最终上下文 C_q。
    - 相比固定 top-k，动态选择可减少冗余、降低噪声。

## 3. 实验设计：数据集、基准与对比方法

- **数据集**（三个常用 MHQA 基准）：
  - HotpotQA
  - 2WikiMultiHopQA
  - MuSiQue
- 实验设置：参照 HippoRAG 2，每个数据集随机抽取 1000 个问题，并收集相关语料（支持段落+干扰段落）。
- **对比方法（Baselines）**：
  - 经典检索器：BM25、Contriever、GTR。
  - 大型嵌入模型：GTE-Qwen2-7B-Instruct、GritLM-7B、NV-Embed-v2（7B）。
  - 结构增强 RAG：RAPTOR、Graph RAG、HippoRAG、HippoRAG 2。
- **评估指标**：
  - 检索：Recall@5。
  - QA：Exact Match（EM）和 F1 分数。

## 4. 资源与算力

- 论文中未明确报告训练时长、GPU 数量等算力信息。
- 提及使用的硬件/模型配置：
  - 密集编码器：NV-Embed-v2（7B）。
  - LLM：Llama-3.3-70B-Instruct（用于实体抽取和答案生成，temperature=0）。
  - 检索时间对比实验：CPU 为 Intel Xeon Platinum 8558；GPU 为 NVIDIA H200。
  - 未说明训练/推理的总耗时、显存占用等具体资源消耗细节。

## 5. 实验数量与充分性

- **实验组数较多，覆盖较全面**：
  - 3 个数据集上的检索效果对比（表 1）。
  - 3 个数据集上的 QA 效果对比（表 2，涉及 EM 和 F1）。
  - 语义消融实验（HotpotQA，表 3）：移除 W_p、移除语义增强。
  - 结构消融实验（HotpotQA，表 4）：对比 top-5/top-10 固定大小与动态结构增强。
  - 图规模对比（表 5）：HGRAG vs HippoRAG 2 的节点/边/超边数量。
  - 检索时间对比（表 6）：CPU/GPU 时间对比。
- **充分性评价**：
  - 实验设计较为客观：与多种类型基线对比，包含经典、大模型、结构增强三类；消融实验验证了各模块的作用；效率分析补充了实用价值。
  - 但消融实验仅在 HotpotQA 上进行，未在其他两个数据集上验证，泛化性证据稍弱。
  - 与 HippoRAG 2 的效率比较仅基于 MuSiQue 数据集，覆盖面有限。

## 6. 论文的主要结论与发现

- HGRAG 在三个 MHQA 基准上均取得领先效果：
  - 检索 Recall@5 平均值最高（87.5），比 HippoRAG 2（87.1）略高，且在 2Wiki 上提升 2.6%。
  - QA 性能（EM/F1）全面优于所有基线，平均 F1 达 69.6%，比 HippoRAG 2 高 4.6 个百分点；在 MuSiQue 上 F1 相对提升 10.7%。
- HGRAG 检索到的段落质量更高：虽然在某些数据集上 Recall@5 略低于 HippoRAG 2，但 QA 结果更好。
- 图规模更小：HGRAG 仅需 57,684 个节点和 11,656 条超边，远少于 HippoRAG 2 的 96,944 个节点和 1,399,367 条边；共同节点数量仅为 HippoRAG 2 的 59.5%。
- 检索效率显著提升：CPU 上比 HippoRAG 2 快约 6.3 倍；在 GPU 上可再加速 43.2 倍（相对于 HippoRAG 2 的 CPU 实现）。
- 消融实验证明：超图权重矩阵（W_p）、语义增强、结构增强均对最终性能有贡献，说明跨粒度整合的有效性。

## 7. 优点

- **创新性**：提出用超图自然建模“实体-段落”跨粒度关系，将结构关联与语义相似度统一到一种检索框架中。
- **方法设计合理**：
  - 超图扩散能够传播多跳信息，无需迭代式检索，避免高延迟。
  - 语义增强的残差式融合缓解了图结构错误带来的负面影响。
  - 动态大小选择机制比固定 top-k 更灵活、更省 token。
- **效率突出**：通过减少冗余节点/边和使用矩阵运算，实现了显著的检索加速。
- **实验对比规范**：与论文 HippoRAG 2 使用相同的编码器、LLM 和 prompt，保证公平性；覆盖三种类型基线，对比全面。

## 8. 不足与局限

- 消融实验仅在一个数据集（HotpotQA）上报告，其他两个数据集（MuSiQue、2Wiki）上各模块的贡献未验证，可能降低结论的普适性。
- 检索效率对比仅使用 MuSiQue 数据集，且只对比了 HippoRAG 2，未与其他 GraphRAG 方法进行效率比较。
- 实体抽取依赖 LLM，存在抽取错误或遗漏的风险，可能影响超图结构质量；论文未对这种噪声鲁棒性做专门分析。
- 超参数（η、β、t）通过在小规模验证集上选取，未说明在不同数据集上的敏感性，泛化性有待进一步分析。
- 未报告计算资源细节（如训练时长、GPU 数量、内存占用等），复现成本不透明。
- 方法仍然依赖稠密编码器（NV-Embed-v2）的初始相似度，若语义编码本身偏差较大，整体表现可能受限。

（完）

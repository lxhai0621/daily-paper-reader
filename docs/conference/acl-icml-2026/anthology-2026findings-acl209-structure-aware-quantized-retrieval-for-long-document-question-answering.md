---
title: Structure-Aware Quantized Retrieval for Long-Document Question Answering
title_zh: 面向长文档问答的结构感知量化检索
authors: "Hui Huang, Julien Velcin, Yacine Kessaci"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.209.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 面向长文档问答的结构感知检索
tldr: 长文档问答中相关证据常分散于相距较远的章节，传统长文档QA/RAG流程易出现上下文碎片化，检索到局部合理却结构错位的段落。本文提出层次量化文档检索器HQDR，将层次图表示与统一词元词表对齐，把显式结构融入检索，并以混合打分机制解耦语义匹配与结构对齐。实验表明该方法能更准确地定位跨章节证据，提升长文档问答的检索质量与下游表现。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl209/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 2701, \"height\": 1309}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl209/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 1900, \"height\": 915}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl209/fig-003.webp\", \"caption\": \"\", \"page\": 14, \"index\": 3, \"width\": 1397, \"height\": 478}]"
motivation: 长文档问答证据分散，传统QA/RAG检索易出现上下文碎片化与结构错位的段落。
method: 提出HQDR，将层次图表示对齐统一词元词表，并以混合打分解耦语义匹配与结构对齐。
result: 该方法更准确地定位跨章节证据，改善长文档问答的检索与回答效果。
conclusion: 将显式文档结构引入检索，为长文档RAG缓解上下文碎片化提供了有效方案。
---

## Abstract
Long-document question answering is challenging because relevant evidence is often scattered across distant sections. Traditional long-document QA/RAG pipelines often suffer from context fragmentation, retrieving locally plausible but structurally misaligned passages. We present the Hierarchical Quantized Document R etriever (HQDR), a framework that aligns hierarchical graph representations with a universal token vocabulary and integrates explicit structure into retrieval. By grounding continuous structural features in a fixed, discrete semantic space, HQDR captures universal hierarchical patterns rather than overfitting to specific layouts. We further propose a hybrid scoring mechanism that decouples semantic matching from structural alignment. Extensive experiments on QASPER and Natural Questions demonstrate that HQDR achieves consistent gains over strong baselines and exhibits superior robustness when transferring between datasets with distinct structural characteristics.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：长文档问答中，回答所需证据常分散在相距较远的章节或段落中。传统长文档 QA/RAG 流程通常把文档扁平化为独立 chunk，丢失了标题、章节、段落之间的层次与顺序关系。
- **核心痛点**：扁平化检索容易召回“语义相似但结构错位”的段落，即局部看似相关、但并非查询真正指向的章节上下文，导致上下文碎片化。
- **背景约束**：虽然 LLM 支持长上下文，但整篇文档输入存在“lost-in-the-middle”现象，且推理成本高，不适合大规模企业部署。
- **已有方法不足**：GNN 可编码层次结构，但连续 GNN 表示与 PLM 语义融合困难，深层 GNN 还容易过平滑，模糊不同结构角色；RAPTOR 等层次化 RAG 方法虽有效，但常依赖递归 LLM 摘要，架构复杂、成本较高。
- **整体含义**：论文提出 **HQDR（Hierarchical Quantized Document Retriever，层次量化文档检索器）**，将层次图表示对齐到统一 token 词表，把显式文档结构引入检索，并用混合打分解耦语义匹配与结构对齐，以提升长文档检索的准确性、跨数据集迁移性和效率。

## 2. 论文提出的方法论

### 2.1 核心思想

- 将每篇文档建模为 **文档—章节—段落** 的层次图。
- 用冻结 PLM 提供语义特征，用 GNN 注入结构特征，再融合为结构感知表示。
- 将连续结构特征量化到由 LLM 词表锚定的固定离散语义空间，增强鲁棒性与迁移性。
- 检索阶段使用 **文档专属章节元码本（section meta-codebook）**，显式计算查询与段落的结构轮廓，并与稠密语义相似度混合打分。

### 2.2 文档图构建与特征融合

- 文档 \(D\) 表示为图 \(G=(V,E)\)，节点包括：文档节点、章节节点、段落节点；边包括层次边（文档—章节、章节—段落）和顺序边（相邻段落等）。
- 对每个节点文本 \(R_i\)，用冻结 PLM 得到语义特征 \(x_i\)。
- 用 3 层 GAT 聚合邻居，得到结构嵌入 \(Z_e\)。
- 融合表示：
  \[
  z_{f,i}=\phi \cdot \frac{W_f z_{e,i}}{\|W_f z_{e,i}\|_2}+(1-\phi)\cdot \frac{x_i}{\|x_i\|_2}
  \]
  其中 \(\phi\) 为可学习标量，用于平衡结构信息与原始语义方向。

### 2.3 自监督结构量化

- 构造固定码本 \(E=\{e_k\}_{k=1}^K\)：使用 LLaMA-2 tokenizer 词表，经同一冻结 PLM 编码 token 得到；论文中码本大小 \(K=15562\)，维度 \(d=768\)。
- 对融合表示 \(z_{f,i}\)，用温度缩放余弦相似度计算软分配概率：
  \[
  p_k(z_{f,i})=\frac{\exp(\cos(z_{f,i},e_k)/\tau)}{\sum_j \exp(\cos(z_{f,i},e_j)/\tau)}
  \]
- 量化表示为码本条目的期望：
  \[
  z_{q,i}=\sum_k p_k(z_{f,i})e_k
  \]
- 总损失：
  \[
  L=L_{Rec}+L_{Doc}+L_{Commit}+\lambda L_{KL}
  \]
  - \(L_{Rec}\)：重建损失，保证量化后仍能恢复 PLM 语义。
  - \(L_{Commit}\)：承诺损失，约束融合表示与量化表示接近。
  - \(L_{KL}\)：KL 对齐损失，使融合表示与原始语义的软分配一致。
  - \(L_{Doc}\)：论文新增的父子节点 InfoNCE 对比损失，正样本为文档—章节、章节—段落等父子对，负样本主要取同文档兄弟节点，以增强层次感知。

### 2.4 IR 微调与混合检索

- 预训练后冻结主干，仅微调轻量结构投影头 \(g(\cdot)\) 和打分权重 \(\alpha\)。
- 对每篇文档构建章节元码本：
  \[
  C_D=\{c_s=z_{f,v_s}\mid s\in S\}
  \]
  即各章节的结构感知融合表示。
- 对段落 \(p\) 和查询 \(q\)，分别投影为 \(h_p=g(z_{f,p})\)、\(h_q=g(x_q)\)。
- 用 Top-k Softmax 在章节元码本上生成稀疏结构轮廓：
  \[
  a_p=\text{softmax}(\text{Top-}k(\{\cos(h_p,c_s)\}_{s\in S}))
  \]
  查询侧同理得到 \(a_q\)。论文设 \(k=4\)，以增强结构信号稀疏性和判别力。
- 最终混合打分：
  \[
  S(q,p)=\alpha\cdot \cos(x_q,z_{f,p})+(1-\alpha)\cdot \langle a_q,a_p\rangle
  \]
  第一项为稠密语义相似度，第二项为查询与段落在章节结构上的对齐分数。
- 检索微调使用 InfoNCE 损失，正样本为真实证据段落，负样本包括同章节结构负例和语义 hard negatives。
- 推理时支持离线索引：预先计算章节码本、段落结构轮廓；在线仅计算查询编码和高效向量打分。

## 3. 实验设计

- **数据集 / 场景**：
  - **QASPER**：5,049 个问题，1,585 篇 NLP 论文，具有清晰章节层次，用于科学长文检索。
  - **Natural Questions 结构化子集**：从 NQ-dev 构造，清洗 HTML 并转为 QASPER 类似格式，丢弃少于 6 个章节的文档，最终 3,211 篇文档；使用随机 70/20/10 划分。
  - **NQ-Hard 子集**：来自 DAPR，再按论文过滤标准保留长文档复杂 QA 对，用于测试困难结构推理。
- **评价指标**：Hit@1、Hit@5、Hit@10、MRR@10、NDCG@

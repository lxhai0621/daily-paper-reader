---
title: "RAGFort: Dual-Path Defense Against Proprietary Knowledge Base Extraction in Retrieval-Augmented Generation"
title_zh: RAGFort：面向专有知识库抽取的检索增强生成双路径防御
authors: "Qinfeng Li, Miao Pan, Ke Xiong, Ge Su, Zhiqiang Shen, Yan Liu, Sun Bing, Hao Peng, Xuhong Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40432/44393"
tags: ["query:ma-kf"]
score: 8.0
evidence: RAG系统防御知识库抽取攻击
tldr: 该论文针对检索增强生成（RAG）系统面临的知识库重构攻击，提出了一种双路径防御方法RAGFort。现有防御仅覆盖类内或类间单一路径，而该工作通过系统实验证明联合保护的必要性。RAGFort同时阻断两种攻击路径，显著降低了攻击成功率，同时保持RAG系统正常性能。该工作增强了专用RAG系统的安全性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: RAG系统面临重构攻击威胁，现有防御仅针对单一路径，联合保护缺失。
method: 提出RAGFort双路径防御框架，同时保护类内和类间知识抽取路径。
result: 实验表明双路径防御大幅降低攻击成功率，且不影响正常RAG性能。
conclusion: 联合保护是RAG防御的关键，RAGFort提供了有效方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems deployed over proprietary knowledge bases face growing threats from reconstruction attacks that aggregate model responses to replicate knowledge bases. Such attacks exploit both intra-class and inter-class paths—progressively extracting fine-grained knowledge within topics and diffusing it across semantically related ones, thereby enabling comprehensive extraction of the original knowledge base. However, existing defenses target only one path, leaving the other unprotected. We conduct a systematic exploration to assess the impact of protecting each path independently and find that joint protection is essential for effective defense. Based on this, we propose RAGFort, a structure-aware dual-module defense combining contrastive reindexing for inter-class isolation and constrained cascade generation for intra-class protection. Experiments across security, performance, and robustness confirm that RAGFort significantly reduces reconstruction success while preserving answer quality, offering the first comprehensive defense against knowledge base extraction attacks.

---

## 论文详细总结（自动生成）

# RAGFort：面向专有知识库抽取的检索增强生成双路径防御——论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：检索增强生成（RAG）系统在部署于专有知识库时，面临来自攻击者的**知识库重构攻击**。攻击者通过黑盒API查询，利用类内（intra-class）和类间（inter-class）两条路径逐步提取知识库中的细粒度内容，最终近乎完整地复制原始知识库。现有防御策略仅针对其中一条路径（如仅限制跨主题扩散或仅模糊单块内容），无法有效抵御双向协同攻击。
- **研究动机**：商业RAG系统（如医疗、金融领域）的知识库是核心知识产权，重构攻击会导致功能等价系统的非法复制，造成直接经济损失。作者首次系统性地比较了单路径保护与双路径保护的效果，证明**联合保护是有效防御的必要条件**，并据此提出RAGFort框架。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：采用**结构感知的双模块防御**，分别阻断类间和类内攻击路径。
  - **类间保护（Inter-class Isolation）**：通过**对比重索引（Contrastive Reindexing）** 增强不同主题类别间的语义分离度，使攻击者难以从已知主题扩散到相邻主题。
  - **类内保护（Intra-class Protection）**：通过**约束级联生成（Constrained Cascade Generation）** 抑制模型在生成时输出敏感或高风险的细粒度内容。
- **关键技术细节**：
  - **类间保护流程**：
    1. 无监督聚类（HDBSCAN）为知识库块分配伪标签（latent topic structures）。
    2. 基于伪标签进行**监督对比学习（SupCon）**，训练一个结构感知的编码器，使同类嵌入更紧凑、异类嵌入更分离。
    3. 用该编码器重建检索器的密集索引，但生成阶段仍使用原始块内容（仅改变检索排序，不改生成输入）。
  - **类内保护流程**：
    1. 采用**两阶段级联生成**：轻量级草稿模型（draft model）先提议候选令牌，强参考模型（reference model）根据拒绝规则选择性验证或替换高风险令牌。
    2. 拒绝规则优化目标：在受预算约束下最小化生成损失，同时降低敏感内容出现概率。近似规则为：当草稿模型的最大置信度显著低于参考模型时触发回退。
    3. 通过伯努利采样调整生成分布，确保最终分布不偏离参考模型。
- **公式与算法**：文中给出了SupCon损失函数、拉格朗日松弛后的拒绝规则优化形式、以及近似规则，并证明了其与最优规则的后悔界（regret bound）较小。算法1描述了级联生成流程。

## 3. 实验设计：数据集、场景、基准与对比方法

- **数据集**（三个领域）：
  - **HealthCareMagic**：医疗问答（症状、诊断、治疗）
  - **Enron Email**：公司邮件（商业场景）
  - **MathQA**：数学应用题（数值推理）
- **基准与对比方法**：
  - **无防御（Without protection）**：原始RAG系统。
  - **已有的单路径防御**：
    - **Re-ranking Protection**（类间防御）：设置语义相似度阈值，只返回高度相关的块。
    - **Summarization Protection**（类内防御）：用摘要替代原始块内容。
  - **本文方法**：
    - **RAGFort（完整双路径）**；
    - **RAGFort InterOnly**（仅类间模块）；
    - **RAGFort IntraOnly**（仅类内模块）。
- **攻击策略**：
  - **Worm-Attack**：使用自复制对抗提示触发级联提取。
  - **RAG-Thief**：基于智能体维护已提取块内存，迭代生成新查询。
- **评估指标**：
  - **安全指标**：块恢复率（Chunk Recovery Rate, CRR），同时满足ROUGE-L≥0.5和语义余弦相似度≥0.85。
  - **性能指标**：回答准确率（Accuracy, ACC）和计算开销（FLOPs）。

## 4. 资源与算力

- 论文中**没有明确说明使用的GPU型号、数量或训练时长**。仅在实验中提到使用了Qwen-14B、DeepSeek-R1-8B、Gemma-3-27B等模型，但未提供训练/推理的具体硬件配置。因此无法定量总结算力消耗。

## 5. 实验数量与充分性

- **实验数量**：
  - 主安全实验（表1）：3个数据集 × 3种生成模型 × 2种攻击 × 3种防御方法（无防御、RAGFort、Re-ranking、Summarization） = 至少108组数据（含多次重复）。
  - 消融实验（表2）：3个数据集 × 3种模型 × 2种攻击 × 4种变体（无防御、完整、仅类间、仅类内） = 至少72组数据。
  - 系统性能实验（表3）：3个数据集 × 3种模型 × 2种状态（保护前后） = 18组数据。
  - 此外还有图1的双路径保护对比实验（3个数据集 × 多种保护比例）。
- **充分性与公平性**：
  - 覆盖了三个不同领域、三种规模（8B~27B）的生成模型、两种主流攻击方法，对比了现有最相关的两种单路径防御。
  - 安全指标同时包含词法和语义相似度，避免单一指标偏差。
  - 系统性能同时评估准确率和计算开销。
  - 消融实验清晰验证了每个模块的必要性及协同效果。
  - **但存在局限**：未评估对合法用户查询的影响（如是否过度拒绝），也未对比更多防御基线（如差分隐私、数据过滤等）；攻击仅考虑了黑盒设置，未测试白盒或更高级攻击。

## 6. 论文的主要结论与发现

1. **单路径保护不足以抵御知识库重构攻击**：无论仅保护类间还是仅保护类内，攻击者仍能恢复大量内容（CRR仅从基线降低约17%~25%）。
2. **双路径联合保护效果显著优于单路径**：完整RAGFort将平均CRR降低至无防御时的**0.51倍**，而单路径变体分别为0.75倍和0.83倍。
3. **RAGFort几乎不损害RAG系统性能**：准确率下降小于2个百分点，FLOPs甚至因轻量级草稿模型使用而有所降低。
4. **级联生成中的拒绝规则可有效抑制敏感内容生成**，且理论保证其性能接近最优。

## 7. 优点：方法或实验设计上的亮点

- **首次系统性研究双路径防御**：明确指出了现有单路径防御的不足，并通过实验量化证明联合保护的必要性。
- **创新的技术设计**：
  - 对比重索引结合无监督聚类和监督对比学习，巧妙利用知识库内在话题结构，不依赖人工标注。
  - 级联生成中的拒绝规则设计兼顾安全性和效率，且理论上证明了近似最优。
- **实验全面**：覆盖多数据集、多模型、多种攻击，并进行了详细的消融和性能分析，结论可靠。
- **实用性**：RAGFort可直接集成到现有RAG流水线，无需修改生成模型本身，部署成本低。

## 8. 不足与局限

- **实验覆盖有限**：
  - 攻击类型仅考虑两种黑盒攻击，未测试更高级的（如白盒、主动推理、多轮对话型）攻击。
  - 防御基线仅对比了Re-ranking和Summarization，未与差分隐私、知识编辑、动态检索扰动等方法对比。
  - 未评估对**合法用户查询的误拒率**（安全性提升是否会错误拒绝正常请求）。
- **方法局限**：
  - 类间保护依赖无监督聚类质量，若知识库话题重叠严重或存在噪音，聚类效果可能下降。
  - 类内保护中的拒绝规则基于置信度比较，可能对校准不良的模型不稳定。
  - 级联生成引入额外计算（参考模型仍需要部分参与），虽FLOPs下降但延迟可能增加（论文未报告延迟指标）。
- **应用场景限制**：主要针对知识库重构攻击，不直接防御其他隐私攻击（如成员推理、属性推断）或恶意提示注入。
- **可复现性**：代码已开源，但硬件和训练细节缺失，可能增加复现难度。

（完）

---
title: "immuneKG: An Immune-Cell-Aware Knowledge Graph Framework for Target Discovery in Immune-Mediated Diseases"
title_zh: immuneKG：一种用于免疫介导疾病靶点发现的免疫细胞感知知识图谱框架
authors: "Ye, Y., PB-IDD Department, Pharmablock Sciences Inc.,"
date: 2026-05-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.30.721823v2.full.pdf"
tags: ["query:mmkqa"]
score: 9.0
evidence: 用于靶点发现的多模态知识图谱
tldr: 本研究提出immuneKG，一个专注于自身免疫性疾病的多模态知识图谱框架。它引入了免疫细胞节点及相关关系，并通过自身抗体、细胞因子等特征重构疾病节点。结合HeteroPNA-Attn图神经网络和新颖性评分机制，该框架在IBD靶点发现中表现卓越，为药物研发提供了具有生物学解释性的决策支持。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有生物医学知识图谱在免疫介导疾病的靶点识别中缺乏深度免疫机制建模。
method: 构建包含免疫细胞实体和多模态疾病特征的知识图谱，并利用HeteroPNA-Attn网络进行推理。
result: "在IBD靶点预测中达到0.99的Hits@100，并能有效识别具有潜力的新型靶点。"
conclusion: immuneKG通过整合免疫细胞机制，实现了从简单筛选到深度决策支持的药物发现范式转变。
---

## 摘要
生物医学知识图谱已成为AI驱动药物研发的基础设施，但其在免疫介导疾病新靶点识别方面的转化影响仍然有限。在此，我们提出了immuneKG，这是一个以自身免疫性疾病为中心的多模态知识图谱，通过对疾病节点进行具有生物学意义的特征重编程构建而成，旨在实现对免疫相关疾病的深度机制建模。immuneKG引入了一个新的实体类别immune_cell和四种原始的有向关系类型，共增加了9,105个现有生物医学知识图谱模式中缺失的新三元组。疾病节点被赋予了三组量化免疫稳态失衡的新模态特征集：自身抗体谱、细胞因子特征和HLA基因型，并辅以系统受累评分和遗传特征。该图谱包含分布在7,287个实体和32种关系类型中的超过407,000个训练三元组。应用于炎症性肠病（IBD）时，immuneKG结合HeteroPNA-Attn图神经网络，在针对Clarivate II期及以上临床管线的测试中实现了0.99的Hits@100，同时一种新颖性惩罚评分函数挖掘出了具有高潜力的“暗靶点”。该框架从传统的候选空间筛选转向以开发为导向的决策支持范式，为下游药物研发提供可操作且可解释的指导。immuneKG项目已在GitHub上公开。研究亮点：1. 我们提出了ImmuneKG，引入了新的immune_cell节点类型、四种原始的免疫细胞关系类型以及自身免疫性疾病节点的黄金特征集，同时修剪冗余节点以增强特征深度和分布平衡。2. 我们开发了HeteroPNA-Attn，这是一种专门的异构图注意力网络，可缓解跨节点模态的特征分布密度不均问题。多头相互注意力机制平衡了跨模态权重，随着模态的增加，下游性能稳步提升。3. 我们驱动新颖性的评分模块优先考虑从头靶点发现，而非回顾性数据拟合。通过优化Hits@1而非报告大型候选池中的成功案例，消除了选择偏差，并展示了在真实研发场景中的真实预测能力。4. 可解释性分析证实，免疫细胞节点在复杂的多跳图推理中起着关键作用；路径级注意力权重的可视化显示，immuneKG通过具有生物学一致性的免疫细胞中间体引导预测。

## Abstract
Biomedical knowledge graphs have emerged as foundational infrastructure for AI-driven drug discovery, yet their translational impact on novel target identification in immune-mediated diseases remains limited. Here we present immuneKG, a multimodal knowledge graph centred on autoimmune diseases, constructed through biologically meaningful feature reprogramming of disease nodes to enable deep mechanistic modelling of immune-related disorders. immuneKG introduces a new entity class immune_cell and four original directed relation types, together adding 9,105 novel triples absent from all existing biomedical KG schemas. Disease nodes are endowed with three novel modal feature sets quantifying immune homeostatic imbalance: autoantibody profiles, cytokine signatures, and HLA genotypes, complemented by systemic involvement scores and genetic features. The graph encompasses over 407,000 training triples across 7,287 entities and 32 relation types. Applied to inflammatory bowel disease (IBD), immuneKG combined with a HeteroPNA-Attn graph neural network achieves a Hits@100 of 0.99 against a Clarivate Phase II+ clinical pipeline, while a novelty-penalised scoring function surfaces high-potential dark targets. The framework shifts from conventional candidate-space screening to a development-oriented decision-support paradigm, providing actionable and interpretable guidance for downstream drug discovery. The immuneKG project is publicly available on GitHub at https://github.com/YaowenYe/immuneKG.

HighlightsO_LIWe propose ImmuneKG, introducing novel immune_cell node types, four original immune-cell relation types, and a gold feature set for autoimmune disease nodes, while pruning redundant nodes to enhance feature depth and distribution balance.
C_LIO_LIWe develop HeteroPNA-Attn, a dedicated heterogeneous graph attention network that mitigates uneven feature distribution density across node modalities. Multi-head mutual attention balances cross-modal weights, yielding steady downstream performance gains as modalities are added.
C_LIO_LIOur novelty-driven scoring module prioritises de novo target discovery over retrospective data fitting. Optimising Hits@1 rather than reporting successes from large candidate pools eliminates selection bias and demonstrates authentic predictive power in real-world R&D scenarios.
C_LIO_LIInterpretability analysis confirms that immune cell nodes play a pivotal role in complex multi-hop graph reasoning; visualisation of path-level attention weights reveals that immuneKG routes predictions through biologically coherent immune-cell intermediaries.
C_LI

---

## 论文详细总结（自动生成）

这是一份关于论文《immuneKG: An Immune-Cell-Aware Knowledge Graph Framework for Target Discovery in Immune-Mediated Diseases》的结构化总结：

### 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：传统的生物医学知识图谱（BKG）在自身免疫性疾病（ADs）的靶点发现中存在局限性。它们通常采用通用的疾病定义，缺乏对“免疫自稳失衡”这一核心病理过程（如细胞因子风暴、免疫耐受丧失、自身反应性T/B细胞浸润）的显式建模。
*   **研究背景**：自身免疫性疾病具有高度的异质性和复杂的免疫调节机制，导致临床试验失败率高。现有的模型往往只能识别出已知的“明星靶点”，难以挖掘具有潜力的“暗靶点”（Dark Targets）。

### 2. 方法论：核心思想与关键技术
*   **immuneKG 构建**：
    *   **实体与关系**：包含7,287个实体和32种关系。创新性地引入了**28种免疫细胞子类**（如Th17、Treg、M1巨噬细胞等）作为一级实体。
    *   **原创关系**：新增了4种有向关系（IcE：表达标志基因；IcDv：驱动分化；IcIm：涉及疾病；DrIc：药物调节），填补了现有图谱在免疫细胞层面的空白。
*   **疾病节点特征重构（黄金特征集）**：
    *   整合了**GWAS遗传关联**（含HLA基因型）、**HPO表型特征**、**IEDB自身抗体与细胞因子谱**。
*   **模型架构（HeteroPNA-Attn）**：
    *   **KGE层**：使用 **ComplEx** 模型在复数空间处理有向生物学关系。
    *   **GNN层**：采用双分支架构。**PNA分支**通过度数感知缩放处理全局拓扑；**HGT分支**处理异构语义。
    *   **融合层**：通过多源注意力门控网络动态平衡知识图谱嵌入、GNN嵌入和多模态疾病特征。
*   **新颖性惩罚评分**：
    *   设计了基于节点度数的对数惩罚函数，降低过度研究的“枢纽基因”排名，优先推荐生物学合理但研究较少的新靶点。

### 3. 实验设计
*   **数据集与场景**：整合了GNBR、DrugBank、CTD、DisGeNET等12个公共数据库，并手动策展了免疫细胞相关三元组。
*   **Benchmark**：
    *   **链接预测**：对比了TransE、DistMult、ComplEx、ConvKB等7种主流KGE模型。
    *   **图谱对比**：与目前最全面的开源图谱 **PrimeKG** 进行性能对比。
*   **案例研究**：以炎症性肠病（IBD）为核心场景进行靶点预测。
*   **临床验证**：使用 Clarivate Cortellis 数据库中处于 II 期及以上临床阶段的靶点作为金标准进行富集分析。

### 4. 资源与算力
*   **软件框架**：基于 PyTorch、PyKEEN 和 PyTorch Geometric 构建。
*   **训练细节**：
    *   KGE 阶段：300 轮（Epochs）。
    *   GNN 阶段：200 轮。
    *   融合网络：100 轮。
*   **算力说明**：文中未明确标注具体的 GPU 型号和数量，但提到使用了 Adam 优化器和标准的深度学习训练流程，属于中等规模的图神经网络训练需求。

### 5. 实验数量与充分性
*   **实验规模**：进行了链接预测基准测试、消融实验（验证不同模态特征的贡献）、跨图谱对比实验以及针对 IBD 的深度案例分析。
*   **充分性**：实验设计较为全面，不仅涵盖了算法指标（MRR, Hits@k），还通过**多跳推理路径可视化**和**免疫细胞结构贡献分析**（如 Th17/Treg 的双桥特征）验证了模型的生物学解释性。

### 6. 主要结论与发现
*   **性能提升**：在链接预测任务中，immuneKG 的表现显著优于 PrimeKG（MRR 提升 83.3%，Hits@1 提升 135.3%）。
*   **IBD 预测**：在 IBD 靶点预测中，Hits@100 达到 0.99，成功识别出 TNF、IL6 等已知靶点，并将 **CAMP**（组织蛋白酶抗微生物肽）识别为高潜力的新型靶点。
*   **解释性**：证实了免疫细胞节点在推理路径中起到了关键的中介作用，模型预测的逻辑与已知的免疫病理学（如髓系激活和 Th17/Treg 失衡）高度一致。

### 7. 优点与亮点
*   **免疫感知**：首次将免疫细胞及其分化/表达关系系统性地整合进靶点发现图谱。
*   **多模态融合**：不仅利用图拓扑，还引入了自身抗体和细胞因子等深度生物学特征。
*   **抗偏见设计**：通过新颖性惩罚机制解决了 AI 模型倾向于预测“明星靶点”的顽疾。
*   **可解释性**：提供了从药物到免疫细胞再到疾病的完整推理链条。

### 8. 不足与局限
*   **数据稀疏性**：药物-免疫细胞（DrIc）和免疫细胞-疾病（IcIm）的关系密度仍较低，依赖于未来的手动策展或单细胞数据集成。
*   **冷启动问题**：对于完全没有预训练嵌入的新实体，模型表现会受到影响。
*   **验证局限**：虽然临床富集率高，但预测的“暗靶点”仍需进一步的湿实验（In vitro/In vivo）验证。
*   **地域偏差**：部分遗传特征（如 GWAS）可能存在人群分布不均的问题。

（完）

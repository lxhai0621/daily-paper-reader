---
title: Reconstructing living materials as a computable design space with multi-agent reasoning
title_zh: 利用多智能体推理将活体材料重构为可计算的设计空间
authors: "Xiao, Y., Zeng, X., Yang, Z., Gu, J., Lu, Y., Wang, Y., Wen, H., Chen, M., Huang, Z., Hu, J., Liu, J., Sha, C., Xie, J., Li, H., Zhu, X., Zheng, S., Zhang, J., Zong, W., He, Z., Xu, Y., Zhou, X., Li, F., Liu, H., He, Q., Liu, L., Yu, Z."
date: 2026-06-09
pdf: "https://www.biorxiv.org/content/10.64898/2026.02.15.705954v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 多智能体推理框架从文献中发现知识
tldr: 活体材料的设计因细胞、基质、工艺和环境的复杂耦合而难以计算化。本文提出LiveMat多智能体推理框架，将3.4万余条非结构化文献标准化为知识图谱，整合微生物、聚合物、功能输出与评估上下文。基准测试表明跨域特征整合是主要瓶颈，LiveMat通过约束分解与专家锚定排名克服之。在伤口愈合任务中，该框架优先出一个四组件设计，实现了最先进的体内性能，为可解释、证据驱动的活体材料发现提供了可扩展基础设施。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有AI加速科学发现的方法难以应对活体材料中上下文依赖的跨域耦合问题。
method: 构建多智能体推理框架LiveMat，通过约束分解、来源感知提取和一致性检查，将非结构化文献转化为可计算知识图谱。
result: 在伤口愈合任务中，LiveMat优先出一个四组件设计，实现了最先进的体内性能。
conclusion: LiveMat建立了可扩展的、可解释与证据驱动的活体材料发现基础设施。
---

## 摘要
人工智能正越来越多地用于加速科学发现，但大多数成功的框架都是在定义明确的分子、蛋白质或材料空间中运作。活体材料提出了一个更严峻的计算问题，因为其功能源于细胞、基质、制造过程和评估条件之间的上下文相关耦合。在此，我们介绍LiveMat，一个多智能体推理框架，它将非结构化文献转化为活体材料的可计算设计空间。LiveMat标准化了34,215条活体材料记录，将16,769种微生物和17,446种聚合物条目整合到一个知识图谱中，该图谱连接了活体组分、非生物基质、功能输出、评估环境和性能指标。在五个大型语言模型上的基准测试表明，活体材料推理主要受限于跨领域特征整合，而非粗粒度分类。LiveMat通过约束分解、来源感知提取、一致性检查和专家锚定排序克服了这一限制。在一项前瞻性伤口愈合任务中，它优先选择了具有最先进体内性能的四组分设计，为可解释、基于证据的活体材料发现建立了可扩展的基础设施。

## Abstract
Artificial intelligence is increasingly used to accelerate scientific discovery, but most successful frameworks operate within well-defined molecular, protein or materials spaces. Living materials present a more formidable computational problem because functions emerge from context dependent coupling among cells, matrices, fabrication processes and evaluation conditions. Here we introduce LiveMat, a multi-agent reasoning framework that transforms unstructured literature into a computable design space for living materials. LiveMat standardizes 34,215 living material records, integrating 16,769 microorganism and 17,446 polymer entries into a knowledge graph linking living components, abiotic matrices, functional outputs, evaluation contexts and performance metrics. Benchmarking across five large language models shows that living material reasoning is limited mainly by cross-domain feature integration rather than coarse classification. LiveMat overcomes this limitation through constraint decomposition, provenance-aware extraction, consistency checking and expert-anchored ranking. In a prospective wound-healing task, it prioritizes a four-component design with state-of-the-art in vivo performance, establishing a scalable infrastructure for interpretable, evidence-grounded living material discovery.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：活体材料（living materials）的设计面临严峻的计算挑战，其功能源于细胞、基质（非生物基质）、制造工艺和评估条件之间的**上下文相关耦合**，远超传统分子、蛋白质或材料空间中的定义明确问题。
- **研究动机**：现有AI加速科学发现的框架大多适用于离散、低维度或明确特征空间，难以处理活体材料中**跨领域、上下文依赖**的复杂耦合关系。
- **整体含义**：通过将非结构化文献转化为可计算的知识图谱，为活体材料发现建立可解释、证据驱动且可扩展的基础设施，以加速设计周期并降低试错成本。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：构建多智能体推理框架 **LiveMat**，将非结构化文献（摘要、全文等）标准化为活体材料的可计算设计空间。
- **关键技术细节**：
  - **知识图谱构建**：整合 34,215 条活体材料记录，集成 16,769 种微生物和 17,446 种聚合物条目，形成连接活体组分、非生物基质、功能输出、评估环境和性能指标的图谱。
  - **多智能体推理**：包含四个核心模块：
    - **约束分解**：将复合设计问题拆解为子约束（如细胞类型、基质材料、制造条件、评估指标）。
    - **来源感知提取**：从文献中提取信息时保留出处（来源文献），确保可追溯性。
    - **一致性检查**：跨文献交叉验证矛盾信息，消除噪声。
    - **专家锚定排序**：利用领域专家知识（如偏好、权衡规则）对候选设计方案进行优先级排序。
  - **基准测试**：在五个大型语言模型（LLM）上评估，发现活体材料推理的主要瓶颈是**跨领域特征整合**，而非粗粒度分类能力不足。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：从非结构化文献中提取的 **34,215 条活体材料记录**，覆盖 16,769 种微生物与 17,446 种聚合物。
- **基准（Benchmark）**：未明确指定标准化benchmark，但通过**五个LLM**（未列出具体模型名称）进行跨模型对比，评估推理瓶颈。
- **对比方法**：未详细列出其他方法，但隐含对比了单一LLM直接推理 vs LiveMat多智能体推理，并通过消融实验验证跨域特征整合是关键瓶颈。
- **前瞻性验证任务**：**伤口愈合**任务，LiveMat优先选择一个四组分设计，并在体内实验中实现最先进（state-of-the-art）性能。

### 4. 资源与算力

- **文中未明确说明**使用的具体GPU型号、数量、训练时长等算力信息。仅提及使用了多个LLM进行推理，但未提供计算资源细节。

### 5. 实验数量与充分性

- **实验数量**：
  - 基准测试：在5个LLM上进行推理瓶颈分析（可视为一组对照实验）。
  - 前瞻性伤口愈合任务：1个实际应用场景，包含体内验证。
  - 未提及更多的消融实验（如去约束分解、去一致性检查等）或额外的数据集测试。
- **充分性评估**：
  - **优点**：验证了跨域特征整合瓶颈，并通过实际体内实验证明了框架的有效性。
  - **不足**：仅在单一任务（伤口愈合）上进行了前瞻性验证，缺乏多任务、多领域（如生物膜、生物传感器等）的泛化测试；未系统报告知识图谱构建的准确率、召回率等质量指标。

### 6. 论文的主要结论与发现

- **主要结论**：LiveMat能够有效将非结构化文献转化为可计算设计空间，并通过多智能体推理克服跨域特征整合瓶颈。
- **关键发现**：
  - 活体材料推理的主要瓶颈在于**跨领域特征的整合**，而非粗粒度分类能力。
  - 在伤口愈合任务中，LiveMat优先选择的四组分设计实现了**最先进的体内性能**。
  - 该方法为可解释、证据驱动的活体材料发现建立了**可扩展的基础设施**。

### 7. 优点：方法或实验设计上的亮点

- **方法论创新**：提出**多智能体推理框架**，将文献挖掘、知识图谱构建与专家知识结合，专门针对活体材料的跨域耦合问题。
- **可解释性与证据驱动**：保留文献来源，支持因果溯源；通过专家锚定排序增强物理可解释性。
- **规模化能力**：处理数万条记录，整合微生物与聚合物两类核心组分，具备扩展至其他活体材料领域的潜力。
- **实际验证**：通过前瞻性体内实验（伤口愈合）证明了方法的实际效用，而非仅停留在计算基准。

### 8. 不足与局限

- **实验覆盖有限**：仅在一个任务（伤口愈合）上进行了前瞻性验证，未评估在其他活体材料应用（如生物修复、智能材料）中的表现。
- **偏差风险**：依赖文献数据质量（如发表偏倚、实验条件差异），知识图谱中可能存在噪声或缺失信息。
- **通用性待考**：方法中“专家锚定排序”需要领域专家参与，可能导致主观性；对不同学科领域的适应能力未知。
- **资源与可重复性**：未公开具体算力需求、代码或数据集，难以独立复现实验结果。
- **计算瓶颈未量化**：仅指出跨域整合是瓶颈，但未深入分析多智能体框架的计算开销与扩展性。

（完）

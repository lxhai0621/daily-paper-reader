---
title: "MetaMuse: A Multi-Agent AI System for Biomedical Metadata Curation and Harmonization"
title_zh: MetaMuse：一种用于生物医学元数据整理与协调的多智能体人工智能系统
authors: "Mittal, E., Litman, E., Myers, T., Agarwal, V., Gopinath, A., Kassis, T."
date: 2026-04-15
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.12.718044v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自主元数据提取和整理的多智能体框架
tldr: 针对生物医学数据库中元数据不一致且非结构化的问题，本文提出了MetaMuse框架。该系统采用多智能体架构，通过提取、逻辑验证和本体映射三个阶段，实现了对非结构化元数据的自动化、高精度标准化处理，显著提升了数据的可发现性和研究复现性。
source: biorxiv
selection_source: fresh_fetch
motivation: 公共生物医学库中元数据格式混乱且缺乏结构化，严重阻碍了数据的有效利用和科学研究的复现。
method: 采用由提取智能体、逻辑仲裁智能体和基于SapBERT的标准化智能体组成的三阶段多智能体AI架构。
result: "在GEO金标准数据集上实现了超过95%的元数据提取准确率，并展现出良好的扩展性和严谨的防幻觉机制。"
conclusion: MetaMuse为大规模生物医学元数据清洗提供了可审计且高效的解决方案，有助于加速数据驱动的科学发现。
---

## 摘要
公共生物医学数据库（如 Gene Expression Omnibus, GEO）中不一致且非结构化的元数据严重限制了数据的可发现性和研究的可重复性。为解决这一问题，我们推出了 MetaMuse，这是一个模块化的多智能体人工智能框架，旨在自主提取、验证和标准化非结构化的生物医学元数据。该框架采用基于大语言模型智能体的三阶段架构：专门的 CuratorAgents 根据上下文为特定的目标元数据字段提取候选值；中央 ArbitratorAgent 执行跨字段的逻辑一致性检查，以防止出现矛盾的注释；最后，NormalizerAgent 利用领域特定的语义搜索模型（SapBERT）将这些自由文本候选值映射到正式的本体术语。我们在人工整理的 GEO 样本金标准数据集上对 MetaMuse 进行了评估，在关键目标元数据字段上实现了超过 95% 的整理准确率，并在包含 400 个样本的更广泛数据集上展示了强大的可扩展性。值得注意的是，MetaMuse 通过在证据模糊时默认采取保守的假阴性策略来避免数据幻觉，从而保持了严格的数据完整性。通过提供完全可审计且具备上下文感知能力的整理流水线，MetaMuse 为丰富公共数据库和加速可重复的数据驱动型科学发现提供了一种可扩展的解决方案。

## Abstract
Inconsistent and unstructured metadata in public biomedical repositories, such as the Gene Expression Omnibus (GEO), severely limits data discoverability and research reproducibility. To address this, we introduce MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW, a modular, multi-agent artificial intelligence framework designed to autonomously extract, validate, and standardize unstructured biomedical metadata. Operating through a three-stage architecture utilizing large language model agents, specialized CO_SCPLOWURATORC_SCPLOWAO_SCPLOWGENTSC_SCPLOW contextually extract candidate values for specific target metadata fields. A centralized AO_SCPLOWRBITRATORC_SCPLOWAO_SCPLOWGENTC_SCPLOW enforces cross-field logical consistency to prevent contradictory annotations. Finally, a NO_SCPLOWORMALIZERC_SCPLOWAO_SCPLOWGENTC_SCPLOW leveraging a domain-specific semantic search model (SapBERT) maps these free-text candidates to formal ontological terms. We evaluated MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW on a gold-standard dataset of manually curated GEO samples, achieving over 95% curation accuracy across key target metadata fields, and demonstrated robust scalability on a broader dataset of 400 samples. Notably, MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW avoids data hallucination by defaulting to conservative false negatives when evidence is ambiguous, thereby preserving strict data integrity. By providing a fully auditable and context-aware curation pipeline, MO_SCPLOWETAC_SCPLOWMO_SCPLOWUSEC_SCPLOW offers a scalable solution for enriching public data repositories and accelerating reproducible, data-driven scientific discovery.

---

## 论文详细总结（自动生成）

以下是对论文《MetaMuse: A Multi-Agent AI System for Biomedical Metadata Curation and Harmonization》的结构化深入总结：

### 1. 核心问题与研究动机
*   **核心问题**：公共生物医学数据库（如 GEO）中的元数据长期存在**非结构化、不一致且质量参差不齐**的问题。关键实验信息（如组织来源、疾病状态、性别等）往往埋藏在自由文本中，导致数据难以被检索、复现或用于大规模机器学习。
*   **研究动机**：现有的手动整理（准确但不可扩展）与传统启发式算法（可扩展但准确度低且缺乏上下文）之间存在权衡。MetaMuse 旨在利用大语言模型（LLM）的多智能体协作，实现高精度、可扩展且可审计的元数据标准化处理。

### 2. 方法论：核心思想与技术细节
MetaMuse 采用模块化的**三阶段多智能体架构**：
*   **第一阶段：数据摄取（Data Intake）**：从 GEO 和 PubMed 提取原始元数据，丢弃无关字段（如联系方式），并将相关信息打包为 JSON 格式。
*   **第二阶段：预处理（Preprocessing）**：使用 **CuratorAgent** 确定样本类型（原代样本 vs. 细胞系），这决定了后续需要提取哪些特定字段（如原代样本关注年龄/种族，细胞系关注细胞系 ID）。
*   **第三阶段：条件处理（Conditional Processing）**：
    *   **CuratorAgent（提取者）**：为每个目标字段分配独立智能体，从原始文本中提取候选值。该智能体具备上下文感知能力，能区分“研究背景中提到的疾病”与“样本实际患有的疾病”。
    *   **ArbitratorAgent（仲裁者）**：核心创新点。它审查所有字段的逻辑一致性（例如：如果细胞系是乳腺癌细胞，则疾病字段不能是肝癌），并提供反馈让 CuratorAgent 进行迭代修正（最多 3 次）。
    *   **NormalizerAgent（标准化者）**：利用 **SapBERT** 模型进行语义搜索，将自由文本映射到正式本体（如 MONDO, UBERON, ChEMBL）。

### 3. 实验设计
*   **数据集**：
    *   **金标准验证集**：随机抽取 100 个 GEO 样本进行人工标注，作为性能基准。
    *   **扩展数据集**：包含 400 个样本，用于评估系统的可扩展性和在大规模数据下的表现。
*   **对比基准（Benchmark）**：以专家人工整理的结果为金标准。
*   **评估指标**：每字段的提取准确率、标准化准确率、错误类型分布（假阳性 vs. 假阴性）。

### 4. 资源与算力
*   **模型使用**：主要使用 Google 的 **Gemini-2.5-pro**（用于复杂推理的提取和仲裁）和 **Gemini-2.5-flash**（用于预处理和标准化）。
*   **算力细节**：文中提到 SapBERT 的向量索引使用了 **FAISS** 库，并在具备硬件支持时进行 **GPU 加速**。
*   **未明确说明的部分**：论文未具体列出推理过程消耗的总 GPU 小时数或具体的 GPU 型号（如 A100 数量），这在基于 API 的 LLM 研究中较为常见。

### 5. 实验数量与充分性
*   **实验规模**：共处理了 500 个样本（100 个深度人工审计 + 400 个自动化评估）。
*   **充分性评价**：
    *   **优点**：实验覆盖了多种生物医学字段（疾病、组织、药物、性别等），并对错误类型进行了细致的分解（如区分幻觉与漏报）。
    *   **局限**：100 个样本的金标准规模相对较小；虽然展示了高准确率，但缺乏与其他自动化工具（如 MetaSRA 或特定 NLP 管道）的直接头对头（Head-to-Head）对比实验。

### 6. 主要结论与发现
*   **高提取精度**：在金标准数据集上，关键字段的提取准确率超过 **95%**。
*   **防幻觉机制**：系统表现出“保守”特性，错误多为假阴性（未检出），极少出现假阳性（幻觉），这对于维护科学数据的完整性至关重要。
*   **标准化瓶颈**：虽然提取很准，但将文本映射到本体 ID（Normalization）仍是挑战。例如，疾病字段的准确率从提取时的 95% 降至标准化后的 80%，组织字段从 97% 降至 66%。
*   **仲裁的重要性**：跨字段逻辑检查显著提升了最终数据的生物学合理性。

### 7. 优点与亮点
*   **多智能体协作**：通过“提取-仲裁-修正”循环模拟了人类专家的共识过程。
*   **可审计性**：系统为每个决策提供推理链（Rationale）和证据日志，方便人工回溯。
*   **上下文感知**：能够识别复杂的实验设计（如对照组的正确映射），优于简单的关键词匹配。

### 8. 不足与局限
*   **本体映射难题**：对于高度专业化、复合型或细粒度的术语（如复杂的细胞亚型），现有的语义搜索模型（SapBERT）仍存在匹配偏差。
*   **源数据依赖**：如果原始 GEO 记录极其简略或缺乏关联论文，系统性能会受限。
*   **成本与延迟**：使用高性能 LLM（如 Gemini Pro）进行多轮迭代，在大规模处理数百万个样本时，成本和 API 调用延迟可能是潜在障碍。

（完）

---
title: "HARVEST: Unlocking the Dark Bioactivity Data of Pharmaceutical Patents via Agentic AI"
title_zh: HARVEST：通过智能体 AI 揭示制药专利中隐藏的生物活性数据
authors: "Shepard, V., Musin, A., Chebykina, K., Zeninskaya, N. A., Mistryukova, L., Avchaciov, K., Fedichev, P. O."
date: 2026-04-17
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.15.711910v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于自主提取结构化生物活性记录的多智能体流水线
tldr: 医药专利中蕴含海量生物活性数据，但因格式复杂难以被现有数据库系统捕获。本研究开发了基于智能体AI的流水线HARVEST，以极低成本（每份文件0.11美元）从16.5万份专利中自动提取了315万条活性记录，填补了BindingDB等数据库的空白。该工具仅用一周便完成了需55年人工才能完成的任务，并揭示了现有预测模型在处理新颖支架和靶点时的局限性。
source: biorxiv
selection_source: fresh_fetch
motivation: 医药专利中海量的结构-活性关系（SAR）数据因缺乏高效提取手段而处于“黑暗”状态，无法被计算模型利用。
method: 开发了名为HARVEST的多智能体大语言模型流水线，能够自主从USPTO专利档案中提取结构化的生物活性记录。
result: 成功提取315万条记录，包含BindingDB中缺失的32.6万个独特支架和967个蛋白靶点，且成本极低、速度极快。
conclusion: HARVEST有效解锁了专利中的海量数据，并通过新基准H-Bench证明了现有开源模型在处理新颖化学空间和靶点时存在显著的泛化差距。
---

## 摘要
医药专利包含大量记录蛋白质-配体结合数据的构效关系（SAR）表。尽管这些信息在技术上是公开的，但在计算上仍难以获取，实际上处于“暗处”，被困在庞大的文档中，且目前尚无数据库对其进行系统性捕获。我们提出了 HARVEST，这是一个多智能体大语言模型流水线，能够以每份文档 0.11 美元的成本，从美国专利商标局（USPTO）专利档案中自动提取结构化的生物活性记录。在对 164,877 份专利的应用中，HARVEST 生成了 315 万条活性记录，恢复了 BindingDB 中缺失的 326,342 个独特骨架和 967 个蛋白质靶点。该流水线在不到一周的时间内完成了一项原本需要专家持续工作 55 年以上的任务。自动提取结果与 BindingDB 中人工策划的美国专利语料库的一致性达到 80%，考虑到参考数据中已发现的错误，这只是一个保守的下限。我们进一步介绍了 H-Bench，这是一个基于这些恢复数据构建的、具有结构保证的留出（held-out）基准测试集。在 H-Bench 上对领先的开源模型 Boltz-2 进行的评估揭示了一个二维泛化差距：模型在新型骨架和未表征的蛋白质靶点上的性能均有所下降，暴露了在现有公共仓库上训练的模型的根本局限性。

## Abstract
Pharmaceutical patents contain vast Structure-Activity Relationship tables documenting protein- ligand binding data. While technically public, this information remains computationally inaccessible and effectively dark, trapped in bulky documents that no existing database has systematically captured. We present HARVEST, a multi-agent large language model pipeline that autonomously extracts structured bioactivity records from USPTO patent archives at $0.11 per document. Applied to 164,877 patents, HARVEST produced 3.15 million activity records, recovering 326,342 unique scaffolds and 967 protein targets absent from BindingDB. This pipeline completed in under a week a task that would otherwise require over 55 years of continuous expert labor. Automated extraction achieves 80% agreement with human curated corpus of US patents from BindingDB, a conservative lower bound given identified errors within the reference data. We further introduce H-Bench, a structurally guaranteed held-out benchmark built from this recovered data. Evaluation of the leading open-source model Boltz-2 on H-Bench reveals a two-dimensional generalization gap: performance degrades both on novel scaffolds and on uncharacterized protein targets, exposing fundamental limitations of models trained on existing public repositories.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **HARVEST** 的多智能体 AI 系统，旨在从海量的医药专利中自动提取“黑暗”生物活性数据（即公开但难以计算利用的数据），并基于此构建了新的基准测试集 **H-Bench**。

以下是对该论文的结构化总结：

### 1. 核心问题与研究动机
*   **核心问题**：医药专利中蕴含着全球最大规模的蛋白质-配体相互作用（PLI）实验数据，但这些数据被“困”在非结构化的专利文档（如复杂的表格、化学图表和长文本）中。
*   **研究动机**：
    *   **数据缺口**：现有的公共数据库（如 BindingDB）主要依赖人工策划，覆盖面有限且更新缓慢。
    *   **泛化危机**：当前的 AI 药物研发模型（如 AlphaFold 3, Boltz-2）在处理新颖化学空间或未表征靶点时表现不佳，原因在于训练数据和基准测试集存在严重的重叠和稀疏性。
    *   **成本瓶颈**：传统人工提取 16 万份专利的数据需要超过 55 年的专家劳动，成本极高。

### 2. 方法论
HARVEST 采用了一种**多智能体大语言模型（LLM）流水线**架构，将复杂的提取任务分解为五个专门的顺序智能体：
*   **核心思想**：通过任务分解减少幻觉，利用长文本上下文（1M+ tokens）维持化合物与靶点的关联。
*   **关键技术流程**：
    1.  **智能体 1（靶点提取）**：识别生物靶点（蛋白、酶等）及实验条件。
    2.  **智能体 2（活性提取）**：提取定量测量值（IC50, Ki, Kd, EC50）及其单位。
    3.  **智能体 3（化合物映射）**：将专利内部别名（如“化合物 42”）映射到 IUPAC 名称或标识符。
    4.  **智能体 4（化学结构解析）**：直接解析专利 XML 中的 **CDX（ChemDraw 二进制）** 文件转化为 SMILES，避免了传统 MOL 文件转换中的常见错误。
    5.  **智能体 5（蛋白靶点解析）**：利用高性能 LLM（如 GPT-5 级别模型）将非标准蛋白名称映射到规范的 UniProt ID。
*   **数据标准化**：所有数值统一归一化为纳摩尔（nM）单位。

### 3. 实验设计
*   **数据集**：处理了 **164,877 份 USPTO 专利档案**。
*   **Benchmark（基准）**：
    *   **验证基准**：与 BindingDB (BDB) 中人工策划的美国专利子集进行对比。
    *   **H-Bench**：论文贡献了一个全新的、具有结构保证的留出基准测试集，包含 BindingDB 中不存在的 48 个蛋白靶点和 6 万多个新颖化合物。
*   **对比方法**：
    *   **提取精度对比**：与人工策划的 BindingDB 记录进行残差分析。
    *   **模型评估**：在 H-Bench 上评估了领先的开源结构模型 **Boltz-2**。

### 4. 资源与算力
*   **成本**：每份文档的提取成本仅为 **0.11 美元**。
*   **效率**：在不到一周的时间内完成了 16.5 万份专利的处理（相当于 55 年人工）。
*   **模型使用**：使用了 `google/gemini-2.5-flash`（用于大规模语义提取，利用其长上下文和提示词缓存）和 `openai/gpt-5-2025-08-07`（用于复杂的蛋白名称推理）。
*   **算力说明**：文中未详细列出具体的 GPU 硬件配置，但强调了利用云端 LLM API 的并行处理能力（50 个文档并行处理）。

### 5. 实验数量与充分性
*   **实验规模**：从 40,902 份专利中提取了 **315 万条活性记录**，最终获得 214 万个独特的 PLI。
*   **充分性**：
    *   **交叉验证**：对 5,668 份共有专利进行了详细对比，一致性达 80.3%。
    *   **手动校验**：对差异最大的记录进行了人工回溯原始专利文本，证明 HARVEST 在单位换算等错误率上低于人工。
    *   **消融实验**：验证了 CDX 解析对提高化学结构准确性的必要性。
*   **客观性**：实验设计考虑了专利家族去重和活性崖（Activity Cliffs）密度分析，评估较为全面客观。

### 6. 主要结论与发现
*   **数据增量**：HARVEST 发现了 32.6 万个独特骨架和 967 个 BindingDB 缺失的蛋白靶点。
*   **提取质量**：自动提取与人工策划的一致性极高（相关系数 r=0.925），且在处理单位换算错误方面优于人类。
*   **二维泛化差距**：通过 H-Bench 发现，Boltz-2 等模型在“新化学空间”和“新蛋白靶点”两个维度上性能均显著下降，证明现有模型尚未真正掌握可迁移的结合物理规律，更多是依赖结构相似性记忆。

### 7. 优点
*   **高性价比与高通量**：将专利挖掘的成本和时间降低了几个数量级，使大规模专利数据利用成为可能。
*   **技术创新**：采用 CDX 二进制解析解决了化学结构提取中的长期顽疾；多智能体协作有效处理了超长文档的上下文关联。
*   **开源贡献**：不仅提供了工具，还发布了高质量的 H-Bench 基准集，解决了 AI 药研领域数据污染（Data Leakage）的问题。

### 8. 不足与局限
*   **Markush 结构处理**：目前无法处理专利中常见的马库什（Markush）通式结构（占排除数据的 8%）。
*   **多模态限制**：无法从剂量反应曲线等图形数据中提取信息。
*   **安全过滤偏差**：由于 LLM 的安全策略，系统会拒绝处理涉及高风险病原体（如埃博拉病毒）的专利，导致相关领域数据缺失。
*   **靶点解析局限**：对于复杂的蛋白复合物（如整合素），规范映射仍存在挑战。

（完）

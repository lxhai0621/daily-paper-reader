---
title: "Benchmarking Agentic Bioinformatics Systems for Complex Protein-Set Retrieval: A Coccolithophore Calcification Case Study"
title_zh: 针对复杂蛋白质集检索的智能体生物信息学系统基准测试：以颗石藻钙化为例的研究
authors: "Zhang, X."
date: 2026-04-02
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.28.715041v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 对复杂多步检索工作流的智能体系统进行基准测试
tldr: 本研究针对生物信息学中复杂的蛋白质集检索任务，评估了Codex、Biomni Lab和DeerFlow 2三种大模型智能体系统。以定石藻钙化相关蛋白质检索为案例，通过对UniProt数据的多维度分析，对比了各系统在检索准确性、覆盖范围及重复运行稳定性方面的表现。结果显示，Codex在灵敏度与特异性之间达到了最佳平衡，且稳定性最高，而其他系统虽产出量大但相关性较低，为未来开发高质量生物信息智能体提供了参考。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-28-715041-v1/fig-001.webp\", \"caption\": \"Figure 2: Overall retrieval trade-off across the six shared categories. Higher y-values indicate broader sensitivity; farther right indicates tighter alignment to the benchmark prompt under the subset relevance heuristic. Codex delivered the best balance, DeerFlow was the broadest useful expansion, and Biomni showed the largest but least specific output.\", \"page\": 6, \"index\": 1, \"width\": 945, \"height\": 572}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-28-715041-v1/fig-002.webp\", \"caption\": \"Table 1: System-level comparison of the three agent outputs as observed from the saved run folders.\", \"page\": 7, \"index\": 2, \"width\": 977, \"height\": 615}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-28-715041-v1/fig-003.webp\", \"caption\": \"Figure 4: Three-way accession overlap for the six shared benchmark categories in the run 2 crossagent comparison. Interior numbers report the seven Venn regions for each category, and the panel headers report total proteins retrieved by each agent in that category. Circle areas are schematic and are not proportional to set size.\", \"page\": 14, \"index\": 3, \"width\": 923, \"height\": 524}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-28-715041-v1/fig-004.webp\", \"caption\": \"Figure 3: Within-system run-to-run stability across the six shared prompt categories. C1–C6 follow the prompt order from inorganic-carbon acquisition through signaling and gene control. Codex was nearly invariant, DeerFlow was stable in the tighter transport categories but much less stable in signaling, and Biomni showed the largest run-to-run swings in the broadest bins.\", \"page\": 8, \"index\": 4, \"width\": 885, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-28-715041-v1/fig-005.webp\", \"caption\": \"Table 2: Category-level comparison across the six shared benchmark categories. Triple overlap is reported as a fraction of the union of all three systems for that category.\", \"page\": 9, \"index\": 5, \"width\": 977, \"height\": 590}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-28-715041-v1/fig-006.webp\", \"caption\": \"Figure 1: Benchmark workflow used in this study. Saved outputs from the three agent systems were normalized to UniProt accessions, reduced to the six shared prompt categories, and compared using overlap analysis plus a literature-informed relevance heuristic.\", \"page\": 5, \"index\": 6, \"width\": 840, \"height\": 818}]"
motivation: 旨在评估大语言模型智能体在处理需要外部数据库和多步工作流的复杂生物信息检索任务时的实际效能与可靠性。
method: 对比三个智能体系统在六个钙化相关类别下的蛋白质检索表现，通过重叠分析、维恩分解和启发式相关性评估进行量化分析。
result: Codex在保持高相关性的同时具有极高的运行稳定性，而DeerFlow和Biomni虽然检索数量更多，但包含大量低相关性蛋白且重复性较差。
conclusion: 智能体在复杂生物信息任务中的质量取决于提示词分解、查询生成精度及运行稳定性，而非单纯的输出数量。
---

## 摘要
大语言模型智能体越来越多地被用于需要外部数据库、工具使用和长多步检索工作流的生物信息学任务。然而，对这些系统的实际评估仍然有限，特别是对于目标集既庞大又具有生物异质性的提示词。在本研究中，我对三个智能体系统在同一项困难的检索任务上进行了基准测试：从 UniProt 下载六个机制各异类别的颗石藻钙化相关蛋白质，同时生成按类别分类的 FASTA 文件和支持证据。比较的系统包括扩展了 Claude 科学技能的 Codex 应用智能体、Biomni Lab 在线版以及仅具备默认技能的 DeerFlow 2。输出结果在 UniProt 登录号级别进行了标准化，并使用重叠分析、维恩分解以及针对基准提示词的每个子集启发式相关性评估，按类别进行了逐一比较。在六个共有类别中，单次运行中 Codex 检索到 2,118 个蛋白质，DeerFlow 检索到 6,255 个，Biomni 检索到 8,752 个。Codex 在灵敏度和特异性之间表现出最佳平衡：其 92.4% 的蛋白质属于高相关性子集，其余 7.6% 属于中等相关性。DeerFlow 的检索结果更为详尽，但其 43.8% 的蛋白质属于低或中低相关性子集。Biomni 生成的集合最大，但其 69.5% 的蛋白质属于低或中低相关性子集，这主要是由于其广泛扩展到了通用的钙传感器、激酶、转录因子和特异性较差的结构域家族。类别特定分析显示，Codex 是无机碳运输、钙和 pH 调节、囊泡运输及信号传导最强的主要来源，而 DeerFlow 则贡献了有价值的补充性基质和多糖候选蛋白质。每个系统的第二次运行在可重复性方面也表现出显著差异：Codex 的系统内稳定性最高（平均类别 Jaccard 系数为 0.982；微 Jaccard 系数为 0.974），DeerFlow 居中（0.795；0.571），Biomni 稳定性最低（0.412；0.319）。这些结果表明，对于复杂的蛋白质家族检索任务，智能体的质量与其说取决于原始输出量，不如说取决于提示词分解、分类范围界定、精确查询生成、富含溯源信息的导出产物以及多次运行的稳定性。

## Abstract
Large language model agents are increasingly used for bioinformatics tasks that require external databases, tool use, and long multi-step retrieval workflows. However, practical evaluation of these systems remains limited, especially for prompts whose target set is both large and biologically heterogeneous. Here, I benchmarked three agent systems on the same difficult retrieval task: downloading coccolithophore calcification-related proteins from UniProt across six mechanistically distinct categories, while producing category-separated FASTA files and supporting evidence. The compared systems were Codex app agents extended with Claude Scientific Skills, Biomni Lab online, and DeerFlow 2 with default skills only. Outputs were normalized at the UniProt accession level and compared category by category using overlap analysis, Venn decomposition, and a heuristic relevance assessment of each subset relative to the benchmark prompt. Across the six shared categories, Codex retrieved 2,118 proteins, DeerFlow 6,255, and Biomni 8,752 in a run. Codex showed the best balance between sensitivity and specificity: 92.4% of its proteins fell into subsets labeled high relevance and the remaining 7.6% into medium relevance. DeerFlow was substantially more exhaustive, but 43.8% of its proteins fell into low or low-medium relevance subsets. Biomni produced the largest sets, yet 69.5% of its proteins fell into low or low-medium relevance subsets, mainly due to broad expansion into generic calcium sensors, kinases, transcription factors, and poorly specific domain families. Category-specific analysis showed that Codex was the strongest primary source for inorganic carbon transport, calcium and pH regulation, vesicle trafficking, and signaling, whereas DeerFlow contributed valuable complementary matrix and polysaccharide candidates. A second run for each system also separated them strongly by repeatability: Codex had the highest within-system stability (mean category Jaccard 0.982; micro-Jaccard 0.974), DeerFlow was intermediate (0.795; 0.571), and Biomni was least stable (0.412; 0.319). These results suggest that for complex protein-family retrieval tasks, agent quality depends less on raw output volume than on prompt decomposition, taxonomic scoping, exact query generation, provenance-rich export artifacts, and repeated-run stability.

---

## 论文详细总结（自动生成）

以下是对论文《Benchmarking Agentic Bioinformatics Systems for Complex Protein-Set Retrieval: A Coccolithophore Calcification Case Study》的结构化深入总结：

### 1. 论文的核心问题与整体含义
*   **研究动机**：在生物信息学中，检索特定生物过程（如颗石藻钙化）相关的蛋白质集非常困难，因为这些过程往往跨越多个代谢路径和功能类别，在 UniProt 等数据库中的注释零散且不均。
*   **核心问题**：大语言模型（LLM）智能体虽然被用于此类多步检索任务，但缺乏针对“大规模且生物学异质性”目标集的系统性评估。
*   **研究意义**：通过颗石藻钙化这一复杂案例，测试不同设计哲学的智能体系统在处理高难度生物信息检索任务时的准确性、全面性和稳定性。

### 2. 论文提出的方法论
*   **核心思想**：采用“提示词分解 + 结果标准化 + 多维重叠分析 + 启发式相关性评估”的框架。
*   **技术流程**：
    1.  **任务分解**：将钙化过程分解为 6 个机制类别（无机碳获取、钙/pH 调节、有机基质、多糖重塑、囊泡运输、信号控制）。
    2.  **标准化处理**：将各智能体输出的 FASTA 或表格数据统一提取为 UniProt 登录号（Accession）。
    3.  **重叠分析**：对三个系统的输出进行三方维恩图（Venn）分解，识别共有核心与特有扩展。
    4.  **相关性评分**：基于文献（如 *Nature Communications* 等）建立启发式标准，将检索到的蛋白质子集标注为高、中、中低、低四个相关性等级。
    5.  **稳定性评估**：通过重复运行（Run 1 vs Run 2），计算 Jaccard 相似度来衡量系统内的一致性。

### 3. 实验设计
*   **场景/数据集**：以颗石藻（Coccolithophore）为目标分类群，从 UniProt 数据库检索钙化相关蛋白。
*   **对比方法（三个智能体系统）**：
    *   **Codex + Claude Scientific Skills**：基于 OpenAI Codex 应用并扩展了专门的科学技能库。
    *   **Biomni Lab**：斯坦福开发的通用生物医学 AI 智能体。
    *   **DeerFlow 2**：字节跳动开发的开源超级智能体框架（使用默认技能）。
*   **Benchmark 标准**：基于 6 个预设的生物学类别，要求输出 FASTA 文件及支持证据。

### 4. 资源与算力
*   **算力说明**：论文**未明确说明**具体的硬件算力（如 GPU 型号或数量）。
*   **原因分析**：该研究属于应用层基准测试，主要评估智能体系统的逻辑编排和工具调用能力。实验是基于已有的智能体平台（Codex App, Biomni Online, DeerFlow 2）运行，重点在于输出产物的质量分析而非模型训练过程。

### 5. 实验数量与充分性
*   **实验规模**：针对 3 个系统，每个系统进行了 2 次独立运行（Run 1 和 Run 2），覆盖了 6 个核心生物学类别。
*   **充分性评价**：
    *   **优点**：实验设计较为深入，不仅对比了系统间的差异，还通过重复运行评估了随机性。使用了 accession 级别的硬比对，避免了自然语言描述的模糊性。
    *   **局限**：样本量（运行次数）较小（仅 2 次），不足以进行复杂的统计推断，但对于揭示系统行为模式（如 Biomni 的高召回/低精度倾向）已具备足够的说服力。

### 6. 论文的主要结论与发现
*   **性能权衡**：存在明显的“灵敏度-特异性”权衡。**Codex** 表现最平衡，92.4% 的结果为高相关；**DeerFlow** 扩展性最强，适合作为补充；**Biomni** 产出量最大但特异性最差（近 70% 为低相关蛋白）。
*   **稳定性差异**：**Codex** 几乎是确定性的（Jaccard 0.982）；**DeerFlow** 居中（0.795）；**Biomni** 极不稳定（0.412），在不同运行间结果差异巨大。
*   **类别敏感性**：定义明确的运输蛋白类别（如无机碳运输）各系统达成高度共识；而信号传导和基质蛋白等模糊类别极易导致智能体检索漂移。

### 7. 优点
*   **实战导向**：直接针对生物学家在构建新研究方向蛋白质集时的真实痛点。
*   **溯源性强**：强调了“溯源产物”（如检索脚本、证据表、查询词 JSON）在生物信息学任务中的重要性，而非仅仅看 FASTA 结果。
*   **混合策略建议**：提出了实用的建议，即以高特异性智能体（Codex）为骨干，结合高扩展性智能体（DeerFlow）进行补充。

### 8. 不足与局限
*   **评估主观性**：相关性评分虽然参考了文献，但仍带有一定的启发式（Heuristic）主观判断，非完全的实验验证。
*   **数据库依赖**：智能体的表现受限于 UniProt 本身的注释质量，对于颗石藻这类非模式生物，许多蛋白仍是未表征的 TrEMBL 条目。
*   **任务局限**：仅测试了蛋白质检索任务，未涉及结构预测、转录组分析或湿实验设计等其他生物信息学领域。

（完）

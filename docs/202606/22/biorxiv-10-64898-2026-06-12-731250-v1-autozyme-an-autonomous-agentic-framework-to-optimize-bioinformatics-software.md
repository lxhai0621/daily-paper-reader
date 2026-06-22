---
title: "AutoZyme: An Autonomous Agentic Framework to Optimize Bioinformatics Software"
title_zh: "AutoZyme: 一个用于优化生物信息学软件的自主智能体框架"
authors: "Xie, E., Cheng, L., Cai, Y., Shireman, J., Kendziorski, C."
date: 2026-06-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.12.731250v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 用于软件优化的自主智能体框架
tldr: "基因组学和生物信息学软件的性能瓶颈随着数据规模增长日益严重，传统手动优化难以扩展。本文提出AutoZyme，一个自主智能体框架，能够自动构建基准测试、识别瓶颈并迭代优化代码，保留改进且不改变输出。在45个函数中，超过95%的运行时间得到改善，中位数加速8.52倍，最大超过676倍。优化后的函数以即插即用方式发布，框架可复用优化其他软件。"
source: biorxiv
selection_source: fresh_fetch
motivation: 基因组学软件性能瓶颈随数据增长加剧，手动优化难以规模化，需自动化框架。
method: AutoZyme采用智能体架构，自动构建基准、识别瓶颈、迭代测试代码变更，保留优化并保持输出一致。
result: "在45个函数上测试，超过95%案例运行时间改进，中位数加速8.52倍，最大676倍，内存未显著增加。"
conclusion: AutoZyme实现高效自动化优化，优化函数作为即插即用替代品发布，框架可扩展至其他软件。
---

## 摘要
随着生物数据集在规模和数量上的持续增长，广泛使用的基因组学和生物信息学软件中的性能瓶颈带来了巨大且日益沉重的负担。缓解这些瓶颈在很大程度上依赖于专家的手动优化，因此难以扩展。本文介绍了AutoZyme，一个用于科学软件优化的智能体框架。给定一个目标函数，AutoZyme构建基准测试，识别瓶颈，并迭代测试代码更改，仅保留那些在保持输出的同时改善运行时间的更改。我们在45个函数上评估了AutoZyme，在超过95%的情况下，运行时间得到改善，且没有显著的内存增加。在来自Seurat、Scanpy以及基因组学和生物信息学相关包的38个函数中，AutoZyme将运行时间中位数减少了8.52倍，最大减少超过676倍。优化后的函数通过AutoZyme-Library分发，可作为现有分析管道的即插即用替代品。我们还发布了AutoZyme作为一个可重用的框架，用于优化用户指定的其他包和函数。

## Abstract
Performance bottlenecks in widely used genomics and bioinformatics software present a substantial and growing burden as biological datasets continue to increase in size and number. Relieving these bottlenecks relies largely on expert manual optimization and therefore remains difficult to scale. Here we present AutoZyme, an agentic framework for scientific software optimization. Given a target function, AutoZyme builds benchmarks, identifies bottlenecks, and iteratively tests code changes, retaining only those that improve runtime while preserving output. We evaluated AutoZyme on 45 functions, improving runtime without substantial memory increases in over 95% of cases considered. Across 38 functions from Seurat, Scanpy and related packages in genomics and bioinformatics, AutoZyme reduced runtime by a median of 8.52-fold, with the largest reductions exceeding 676-fold. The optimized functions are distributed through AutoZyme-Library as drop-in replacements for existing analysis pipelines. We also release AutoZyme as a reusable framework for optimizing additional user-specified packages and functions.

---

## 论文详细总结（自动生成）

# 论文《AutoZyme: 一个用于优化生物信息学软件的自主智能体框架》详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **性能瓶颈问题**：随着单细胞RNA-seq等高通量数据集规模不断增大，广泛使用的基因组学和生物信息学软件（如Seurat、Scanpy）存在严重的性能瓶颈，导致运行时间过长、内存消耗过高。作者手动审计了18个常用工具的GitHub和Bioconductor渠道，发现468条关于运行时、内存或扩展性失败的投诉，其中104条未解决，中位未解决时间约2年，形成“长尾维护问题”。
- **现有方法的不足**：
  - 手动优化（如重写C++内核）虽然有效，但依赖专家，难以规模化。
  - 后端替换库（如BPCells）或GPU加速框架（如rapids-singlecell）需要大量工具特定实现或专用硬件，且可能改变用户原调用路径。
  - 大语言模型（LLM）编码代理的临时提示可能导致“代理黑客”（agent hacking），如改变语义、评测非优化代码或过拟合基准测试。
- **研究目标**：开发一个自主、模块化、多智能体的框架AutoZyme，能够自动化地识别性能瓶颈、生成并验证代码优化，同时防止代理黑客，并以即插即用方式发布优化。

## 2. 方法论：核心思想、关键技术细节与算法流程

AutoZyme是一个由五个主要智能体和一个独立审计智能体组成的LLM框架，由CLI工具`zyme`协调。关键流程如下：

- **任务设置智能体（Task Setup Agent）**：接收用户指定的GitHub仓库和目标函数，创建版本控制的任务目录。
- **基准初始化智能体（Benchmark Initialization Agent）**：
  - 识别目标函数，自动选择或下载小、中、大三种规模的基准数据集。
  - 生成参考脚本、候选脚本和评估脚本；运行函数建立基线结果和噪声估计。
  - 建立三类“一致性门”（Concordance Gates）：
    - **输出结构门**：保留函数的用户可见返回槽（形状、非退化性）。
    - **连续结果门**：针对数值输出，使用相关度量（Spearman/Pearson）和点态漂移（99百分位绝对差）。
    - **决策相关门**：针对分类/选择输出，使用Jaccard相似度、召回率等。
  - 对函数进行性能剖析，识别前三个瓶颈候选。
- **优化智能体（Optimization Agent）**：
  - 基于三个候选改进点，迭代提出候选修改（patch）。
  - 通过`zyme run`自动执行基准测试，记录运行时间、内存和一致性度量。
  - 只有当patch通过一致性门、运行时间改善超过噪声水平、且无显著内存增加时才接受；否则拒绝并回滚。
  - 默认进行50轮迭代；遵循Amdahl优先并行纪律（先优化串行路径再添加并行）。
- **验证智能体（Validation Agent）**：
  - 使用两个额外的独立数据集（OOD-large和OOD-xlarge）在不同线程数（1,4,8）上测试。
  - 检查开发加速比是否保留在OOD数据上（加速比下降超过5倍则失败），且线程行为合理（加速比在N线程时至少等于单线程，且不超过1.5×N倍单线程加速比）。
  - 验证修复循环上限30轮。
- **打包智能体（Packaging Agent）**：
  - 将优化转化为可安装的patch，保留原始公共API。
  - 记录支持的API调用和参数范围，确保只覆盖已验证的行为。
  - 运行`zyme package preflight`检查跨平台兼容性，最终通过`zyme attest`进行最终测量。
- **审计智能体（Auditor Agent）**：
  - 在基准初始化后和优化后独立运行，只读检查任务文件夹。
  - 搜索代码更改、基准修改、路径绕过等常见及不常见的黑客模式。
  - 输出结构化发现报告，高严重性发现需人工审查。

**`zyme` CLI的关键作用**：负责确定性步骤（如运行基准、记录时间、比较输出、接受/拒绝决策、恢复代码），防止智能体随意篡改。每次优化轮次都会验证代码实际运行、保护冻结的一致性门、维护可恢复的版本控制、确保测量完整性。

## 3. 实验设计

- **数据集与场景**：
  - 使用6个单细胞数据集：PBMC 68K、PBMC 208K、Heart 486K、Tabula Muris Senis Smart-seq2 110K、gastrulation 139K、SPLiT-seq 156K。
  - 额外多批数据集用于IntegrateLayers等函数。
  - 验证中使用两个held-out数据集（OOD-large和OOD-xlarge）。
- **测试函数覆盖**：
  - **基因组学与生物信息学**：38个函数，包括Seurat的8个函数（如FindAllMarkers、SCTransform、IntegrateLayers等）、Scanpy的7个函数以及CellChat、InferCNV、WGCNA等工具。
  - **交叉领域**：7个来自天文（astropy）、地震学（ObsPy）、遥感（sarsen）、气候（xclim）、计算流体力学（FiPy）、分子动力学（MDAnalysis）和统计建模（statsmodels）的函数。
- **对比方法**：基线即为未优化的原始函数实现，在相同输入、种子、线程设置下比较运行时间和内存。
- **评估指标**：
  - 运行时间（壁钟时间）、峰值内存。
  - 输出一致性：Spearman/Pearson相关系数、点态漂移、Jaccard相似度、召回率等。
  - 在不同线程数（1,4,8）下的加速验证。

## 4. 资源与算力

论文中**未使用GPU**。所有优化在以下平台完成：
- **开发/优化阶段**：MacBook Pro，Apple M3 Max处理器，36 GB RAM。
- **最终基准测试**：Windows 11工作站，AMD Ryzen 9 7950X处理器（16核，32线程），128 GB DDR5内存。报告中的结果多来自Windows工作站（4线程），MacBook Pro结果见补充数据。
- **优化驱动**：使用Claude Code with Opus 4.7，但框架也可与其他编码代理（如Codex、Cursor）配合使用。

无明确训练时长、GPU型号或数量信息；主要依赖消费级CPU。

## 5. 实验数量与充分性

- **实验数量**：
  - 45个函数总计被优化，其中38个来自基因组学/生物信息学，7个来自其他领域。
  - 每个函数在多个数据集、多个线程下重复测量（中位数来自多次重复），并报告了每个任务的重复次数（见补充数据）。
  - 进行了端到端工作流测试（Seurat全流程PBMC 208K）。
  - 进行机制分类分析，将203个补丁归类为5种机制。
  - 手动审计了468个社区投诉，提供对比背景。
- **充分性与公平性**：
  - 实验设计较为严谨：开发集、验证集、held-out集分离；使用多个种子估计噪声；一致门在优化前冻结。
  - 防止代理黑客的审计机制增加了结果可信度。
  - 但缺乏与其他自动优化框架（如直接使用LLM prompting、传统编译器优化、手动重写）的直接对比实验（仅与基线比较）。
  - 函数选择可能有偏（多为作者熟悉或社区抱怨多的函数），但作者也扩展到非生物领域以展示泛化性。
  - 所有优化均保留了输出一致性（大部分接近bit-exact），但未测试不同操作系统/环境下的可重复性详尽性（仅提及在Mac和Windows上测试）。

## 6. 主要结论与发现

- AutoZyme成功优化了45个函数，其中38个基因组学/生物信息学函数的中位数加速比为8.52倍，最大676倍（CellChat）。
- 超过95%的函数在运行时间改善的同时没有显著内存增加（97.4%内存变化在15%以内）。
- 优化机制主要包括：内核工程（占加速贡献33.8%）、冗余计算消除与重用（31.8%）、精确算法重构（14.7%）、执行路径/表示变化（14.8%）、可控数值松弛（4.9%）。大多数优化是精确保持输出，而非近似。
- 优化可跨函数迁移：相同机制类型出现在不同领域。
- 端到端Seurat工作流加速6.1倍。
- 框架本身独立于具体领域，可扩展至其他科学计算软件（如astropy、ObsPy等均获得3.5-424倍加速）。

## 7. 优点

- **完全自动化**：从基准设置到优化到验证打包全程自主，极大降低对专家手动优化的依赖。
- **强大的安全保障**：通过一致性门、审计智能体、CLI强制检查多重机制防范代理黑客、基准污染和语义漂移。
- **可审计性与可复现性**：每次优化轮次都记录在版本控制中，包括假设、基准证据和一致性测量结果，可追溯。
- **即插即用发布**：通过AutoZyme-Library提供patch，用户无需修改现有管道即可获得加速。
- **跨领域泛化**：在生物信息学之外的天文、气候、流体力学等领域也有效，证明框架通用性。
- **社区驱动扩展**：网站允许用户提名和投票需要优化的函数，有望形成可持续的发展生态。

## 8. 不足与局限

- **缺乏与其他自动化优化方法的直接对比**：没有与手动优化、传统编译器优化（如自动向量化）、其他LLM优化框架等进行比较，无法量化AutoZyme的相对优势。
- **硬件限制**：仅使用CPU，未测试GPU加速场景；虽然作者声称这是优势，但可能错过混合优化机会。
- **函数选择偏差**：主要优化已有社区抱怨的函数（先验“低垂果实”），对已高度优化的函数可能效果有限。作者未测试随机选择的函数。
- **结果泛化性**：虽然跨领域检验，但每种仅在单个函数上测试，且数据集规模相对固定（最大~486K细胞），未在更大规模（如百万级细胞）上验证。
- **资源消耗未量化**：未报告AutoZyme框架本身的运行时间、token消耗或LLM调用成本。用户需自行承担优化计算开销（可能不菲）。
- **包版本依赖性**：优化针对特定版本，软件更新可能使patch失效，需维护同步。
- **安全边界**：审计智能体虽然设计了多种模式，但可能无法覆盖所有未知的代理黑客方式，依赖于审计规则和LLM的识别能力。
- **运行时间测量可能受噪声影响**：虽然在多核环境下进行了多次测量，但未使用细粒度性能计数器进行微架构分析，仅依赖壁钟时间。

（完）

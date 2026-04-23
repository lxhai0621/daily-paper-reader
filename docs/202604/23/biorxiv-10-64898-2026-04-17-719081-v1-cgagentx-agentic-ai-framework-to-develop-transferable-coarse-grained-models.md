---
title: "CGAgentX: Agentic AI Framework to Develop Transferable Coarse-Grained Models"
title_zh: CGAgentX：用于开发可迁移粗粒化模型的智能体 AI 框架
authors: "Deshmukh, S. A., Seth, S."
date: 2026-04-18
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.17.719081v1.full.pdf"
tags: ["query:ma-kf"]
score: 10.0
evidence: 协调专业 LLM 智能体的自主多智能体框架
tldr: CGAgentX是一个基于大语言模型的多智能体框架，旨在自动化开发可迁移的粗粒度（CG）分子模型。该框架通过六个专业智能体在主智能体协调下，利用闭环迭代和多叉并行模拟策略，自主优化参数以匹配原子模拟和实验数据。在DMSO和DMA案例中，它实现了高精度的属性预测，为分子建模提供了一种无需人工干预的通用AI平台。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统的粗粒度模型开发过程复杂且高度依赖人工经验，难以高效平衡多种物理属性之间的参数优化权衡。
method: 构建了一个由主智能体协调的六智能体系统，通过多叉并行模拟策略自主生成物理假设、调用MD工具并进行闭环迭代优化。
result: "在DMSO和DMA的测试中，该框架在无人工干预下实现了关键实验属性误差小于5%，并保持了与原子参考模型的一致性。"
conclusion: CGAgentX证明了多智能体AI在复杂科学建模任务中的有效性，为开发高精度、可迁移的粗粒度模型提供了可扩展的自动化方案。
---

## 摘要
我们提出了 CGAgentX，这是一个通用的自主多智能体框架，其中基于大语言模型（LLM）的专业化智能体协同优化粗粒化（CG）模型参数，以重现目标性质。通过以极性溶剂二甲基亚砜（DMSO）和 N,N-二甲基乙酰胺（DMA）作为代表性案例研究，我们展示了该框架开发 CG 模型的能力，这些模型能够准确重现原子模拟和实验文献中的关键性质。六个专业化智能体——映射（Mapping）、拓扑（Topology）、边界（Boundary）、假设（Hypothesis）、诊断（Diagnostic）和优化（Optimization）——在主智能体（Master Agent）的领导下运行，通过自主调用外部工具（包括分子动力学（MD）模拟和分析工作流）并利用适应度函数评估输出来协调闭环、迭代的参数细化。该框架的核心是假设智能体，它通过协调并行多叉模拟（同时评估多个候选参数集）来生成并验证具有物理动机的参数假设。这种多叉策略扩展了参数空间的探索，产生了更丰富的数据集，从而在迭代过程中实现更准确的假设细化。智能体根据中间模拟结果自适应地提出参数更新建议，从而在结构、热力学和输运性质之间的复杂权衡中实现高效导航。该框架在保持与原子参考行为一致的同时，以 5% 以内的准确度重现了关键实验性质，且无需人工干预即可实现收敛。其模块化架构易于扩展到其他分子系统，并可容纳额外的目标、约束或模拟引擎，为可迁移 CG 模型的开发提供了一个通用的智能体 AI 平台。

## Abstract
We present CGAgentX, a general autonomous multi-agent framework in which specialized LLM-based agents coordinate the optimization of coarse-grained (CG) model parameters to reproduce target properties. Using polar solvents dimethyl sulfoxide (DMSO) and N,N-dimethylacetamide (DMA) as representative case studies, we demonstrate the framework's capability to develop CG models that accurately reproduce key properties from atomistic simulations and experimental literature. Six specialized agents - Mapping, Topology, Boundary, Hypothesis, Diagnostic, and Optimization - operate under a Master Agent that orchestrates closed-loop, iterative parameter refinement by autonomously invoking external tools, including molecular dynamics (MD) simulations and analysis workflows, and evaluating outputs through a fitness function. Central to the framework is a Hypothesis Agent that generates and verifies physically motivated parameter hypotheses by coordinating parallel multi-fork simulations, wherein multiple candidate parameter sets are evaluated simultaneously. This multi-fork strategy expands parameter space exploration, yielding richer datasets that enable more accurate hypothesis refinement across iterations. Agents adaptively propose parameter updates based on intermediate simulation outcomes, enabling efficient navigation of complex trade-offs among structural, thermodynamic, and transport properties. The framework reproduces key experimental properties within 5% accuracy while maintaining consistency with atomistic reference behavior, achieving convergence without manual intervention. The modular architecture is readily extensible to other molecular systems and can accommodate additional targets, constraints, or simulation engines, providing a general agentic-AI platform for transferable CG model development.

---

## 论文详细总结（自动生成）

这是一份关于论文《CGAgentX: Agentic AI Framework to Develop Transferable Coarse-Grained Models》的结构化总结：

### 1. 核心问题与整体含义
*   **研究动机**：粗粒化（CG）分子动力学模拟是研究大规模分子系统的关键，但其开发过程存在两大挑战：一是**映射方案（Mapping）**与**力场参数化（Parameterization）**高度耦合且互为因果；二是传统优化算法（如PSO、玻尔兹曼反演）属于“黑盒”搜索，缺乏物理直觉，难以在复杂的结构、热力学和输运性质之间取得平衡。
*   **核心目标**：开发一个名为 **CGAgentX** 的自主多智能体 AI 框架，利用大语言模型（LLM）的物理推理能力，实现从分子结构到高精度、可迁移 CG 模型的全自动化开发。

### 2. 方法论
*   **核心思想**：将 CG 模型开发视为一个“假设驱动”的迭代决策问题，而非单纯的数值优化。通过多个专业化智能体协作，模拟人类专家的逻辑进行闭环优化。
*   **关键技术细节**：
    *   **六大专业智能体**：
        1.  **Mapping Agent (MA)**：解析分子结构（SMILES），自主提出原子分组方案。
        2.  **Topology Agent (TA)**：准备系统拓扑，生成初始坐标和模拟文件。
        3.  **Boundary Agent (BA)**：基于原子参考数据或几何估算，设定参数的物理边界。
        4.  **Hypothesis Agent (HA)**：核心组件，根据诊断报告提出具有物理动机的假设（如“增加电荷以提高内聚能”）。
        5.  **Optimizer Agent (OA)**：将抽象假设转化为具体的参数集。
        6.  **Diagnostic Agent (DA)**：分析模拟结果，评估相态稳定性及属性误差。
    *   **多叉并行策略（Multi-fork Strategy）**：在每个迭代周期，HA 提出一个假设，OA 将其转化为 $n$ 个不同的参数分支（Forks）并行模拟。这不仅加速了收敛，还为 HA 提供了更丰富的反馈数据。
    *   **闭环流程**：主智能体（Master Agent）协调数据流，通过适应度函数（Fitness Function）评估密度、汽化热、表面张力和偶极矩。

### 3. 实验设计
*   **研究对象**：两种典型的极性溶剂——**二甲基亚砜 (DMSO)** 和 **N,N-二甲基乙酰胺 (DMA)**。
*   **Benchmark（基准）**：
    *   **实验数据**：密度、汽化热 ($H_{vap}$)、表面张力 (ST) 和偶极矩。
    *   **原子模拟 (AA)**：作为结构分布（键长、键角、RDF）的参考。
*   **对比维度**：
    *   不同映射方案（含/不含显式静电虚拟位点）。
    *   不同并行分支数（2, 4, 8 Forks）对收敛速度的影响。
    *   温度迁移性测试（DMSO: 298K/323K; DMA: 298K/313K）。

### 4. 资源与算力
*   **LLM 模型**：使用了 Moonshot AI 的 **Kimi K2.5** 模型（部署于弗吉尼亚理工大学 ARC 集群）。
*   **计算硬件**：
    *   **优化阶段**：使用 AMD EPYC 7702 CPU 核心，每个并行分支分配 16 个核心。
    *   **验证阶段**：100 ns 的生产模拟在 **NVIDIA A30 GPU** 上执行。
*   **时长**：文中未明确给出总耗时，但提到 Fork 8 方案在第 8 个 Epoch 即可将误差降至 10% 以下。

### 5. 实验数量与充分性
*   **实验规模**：共进行了 **54 组独立优化实验**（3 次重复 × 3 种分支设置 × 3 种映射方案 × 2 种溶剂）。
*   **数据深度**：分析了超过 **3073 条物理假设** 的文本逻辑，验证了 AI 是否真的在进行物理推理。
*   **充分性评价**：实验设计非常充分。不仅涵盖了数值上的准确性验证，还通过消融实验展示了分支数量对效率的提升，并进行了长达 100 ns 的独立验证模拟，确保了结果的稳健性。

### 6. 主要结论与发现
*   **高精度**：最终开发的 CG 模型在关键实验属性上的误差均在 **5% 以内**（部分低至 0.2%）。
*   **物理推理能力**：73% 的 AI 假设包含明确的物理机制推理（如利用 $\mu = q \times d$ 关系平衡电荷与键长）。
*   **加速效应**：增加并行分支（Fork 8）比基础方案（Fork 2）的收敛速度快 **2.6 倍**，且生成的假设更具定量化。
*   **迁移性**：模型在不同温度下均保持了良好的准确性，证明参数捕捉到了物理本质而非过拟合。

### 7. 优点与亮点
*   **自主性**：实现了从映射到参数化的全流程“无人值守”开发。
*   **可解释性**：HA 提供的推理过程使参数选择不再是黑盒，人类研究员可以理解 AI 的优化逻辑。
*   **模块化**：框架易于扩展，可以轻松更换模拟引擎（如从 NAMD 换成 Gromacs）或添加新的目标属性。
*   **多属性平衡**：成功解决了表面张力与汽化热之间难以同时优化的传统难题。

### 8. 不足与局限
*   **结构与热力学的权衡**：实验发现，为了追求热力学属性（如密度、汽化热）的极高精度，某些结构分布（如 DMA 的键角分布）会出现约 30% 的偏差。
*   **系统复杂性限制**：目前仅在小分子极性溶剂上验证，尚未在蛋白质、聚合物等具有复杂构象空间的生物大分子上进行测试。
*   **计算成本**：虽然减少了人工，但大规模并行 MD 模拟和频繁调用 LLM API 仍需要显著的计算资源支持。

（完）

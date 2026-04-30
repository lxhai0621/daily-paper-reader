---
title: "Using AI to Build AI: AIDO.Builder Enables Autonomous Machine Learning Model Building for Biomedicine"
title_zh: 用AI构建AI：AIDO.Builder实现生物医学领域的自主机器学习模型构建
authors: "Guo, H., Liang, Y., Cheng, X., Ellington, C., Xie, P., Song, L., Xing, E."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719735v2.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 全自动生物医学模型开发的智能体AI系统
tldr: AIDO.Builder是一个旨在自动化生物医学机器学习模型构建的智能体系统。针对生物医学数据异构、标注稀疏等挑战，该系统仅需自然语言描述即可自主完成从策略选择、代码编写到迭代优化的全生命周期开发。它能灵活运用从头训练或微调基础模型的方法，在多个基准测试中达到与人类专家相当的水平，显著降低了AI在生物医学研究中的应用门槛。
source: biorxiv
selection_source: fresh_fetch
motivation: 生物医学领域模型开发过程复杂且高度依赖人工经验，亟需自动化工具来降低技术门槛并提高效率。
method: 开发了名为AIDO.Builder的智能体系统，通过自然语言任务描述驱动，利用自动化反馈循环自主设计、执行并迭代优化模型训练与评估流水线。
result: 在多种生物医学基准测试中，AIDO.Builder生成的模型表现出与人类专家开发的方案极具竞争力的性能。
conclusion: AIDO.Builder证明了利用AI自动化构建AI模型的可行性，为加速生物医学研究中的AI应用提供了强有力的技术支撑。
---

## 摘要
机器学习加速了生物医学发现，但创建有效的预测模型需要专门的人类专业知识和繁重的手动工作。研究人员必须迭代地设计流水线、选择架构并调试代码。由于该领域常见的异构数据集、稀疏标注和复杂的评估协议，这一挑战在生物医学中尤为严峻。我们提出了AIDO.Builder，这是一个智能体人工智能系统，能够完全自动化生物医学模型开发的整个生命周期。仅需提供自然语言任务描述和目标指标，AIDO.Builder即可自主构建可执行的训练和评估流水线。该系统选择合适的建模策略，执行实验，并利用自动反馈循环迭代地修改其自身的代码、配置和训练程序。它通过从头训练专用模型或利用预训练基础模型进行任务适配，灵活地适应新任务。我们展示了在多种生物医学基准测试中，AIDO.Builder产生了与人类方案相比极具竞争力的解决方案，同时消除了以往稳健模型开发所需的手动迭代。通过自动化将原始数据转化为可靠的AI模型，AIDO.Builder展示了AI本身如何被用于加速生物医学研究中的AI发展。

## Abstract
Machine learning accelerates biomedical discovery, but creating effective predictive models requires specialized human expertise and demanding manual effort. Researchers must iteratively design pipelines, select architectures, and debug code. This challenge is particularly severe in biomedicine because of the heterogeneous datasets, sparse annotations, and complex evaluation protocols that are common in the domain. We present AIDO.Builder, an agentic artificial intelligence system that fully automates the entire life-cycle of biomedical model development. Provided only with a natural language task description and a target metric, AIDO.Builder autonomously constructs executable training and evaluation pipelines. The system selects suitable modeling strategies, executes experiments, and uses automated feedback-loop to iteratively revise its own code, configurations, and training procedures. It flexibly adapts to new tasks by training specialized models de novo or by using pretrained foundation models to build predictive models through task-appropriate adaptation. We show that across diverse biomedical benchmarks, AIDO.Builder produces highly competitive solutions against human alternatives, while eliminating the manual iteration previously required for robust model development. By automating the translation of raw data into reliable AI models,AIDO.Builder demonstrates how AI itself can be used to accelerate AI for biomedical research.

---

## 论文详细总结（自动生成）

### 论文总结：AIDO.Builder —— 生物医学领域的自主机器学习构建智能体

#### 1. 核心问题与整体含义（研究动机和背景）
在生物医学领域，利用机器学习（ML）加速科学发现已成为趋势，但构建高效的预测模型仍高度依赖人类专家的手动干预。研究人员需要耗费大量时间进行任务解析、数据表示选择、架构设计、代码编写、错误调试以及超参数优化。
*   **领域挑战**：生物医学数据具有高度异构性（如基因序列、分子结构、病理图像）、标注稀疏、评估协议复杂且软件依赖冲突频发。
*   **研究目标**：开发一个名为 **AIDO.Builder** 的自主智能体系统，旨在实现生物医学模型开发全生命周期的自动化，将研究人员从繁重的工程负担中解放出来，使其专注于高层的实验设计和生物学解释。

#### 2. 方法论：核心思想与关键技术
AIDO.Builder 被建模为一个在**部分可观测马尔可夫决策过程（POMDP）**中运行的决策实体。其核心思想是通过 LLM 驱动的反馈循环，自主完成“计划-执行-观察-修正”的迭代。
*   **分层规划（Planning）**：将自然语言目标分解为结构化的子任务图（如数据探索、模型实现、训练、分析）。
*   **模块化架构**：
    *   **实现模块（Implementation）**：生成简洁的 Python 代码。
    *   **调试模块（Debugging）**：通过分析 Traceback 自动修复语法错误、维度不匹配或库兼容性问题。
    *   **精炼模块（Refinement）**：基于实验反馈（如过拟合、收敛慢）进行架构变异或超参数调整。
*   **经验记忆系统（Memory System）**：
    *   **反射创建**：任务完成后，LLM 总结成功经验和失败教训，并将其向量化存储。
    *   **相似性检索**：在新任务中检索相似的子任务模式（如“如何处理不平衡分类”），实现跨任务的知识迁移。
*   **基础模型适配**：系统不仅能从头构建模型，还能自主选择并微调生物医学基础模型（如 AIDO.RNA, AIDO.DNA, ESM2），设计复杂的融合机制（如双向交叉注意力）。

#### 3. 实验设计：数据集、Benchmark 与对比方法
论文在多个具有代表性的生物医学基准上验证了系统性能：
*   **任务类型与数据集**：
    *   **图像分类**：组织病理学癌症检测（Histopathologic Cancer Detection）。
    *   **蛋白质适应性预测**：ProteinGym CSN4（回归任务）。
    *   **分子属性预测**：PolarisHub CYP2D6 底物识别。
    *   **空间转录组学**：OpenProblems 空间变量基因（SVG）排名。
    *   **序列交互预测**：DNA-RNA 相互作用（基于 AIDO 家族基础模型）。
    *   **肽类活性预测**：DPP-IV 抑制肽预测（基于 ESM2 微调）。
    *   **迭代基因发现**：BioDiscoveryBench（CRISPR 筛选）。
*   **对比基准（Baseline）**：主要对比了 **Biomni**（通用生物医学 AI 智能体）和 **BioDiscovery Agent**，以及特定任务的启发式方法。

#### 4. 资源与算力
*   **算力说明**：论文**未明确给出**具体的 GPU 型号、数量或总训练时长。
*   **环境描述**：提到系统在受控的虚拟环境中运行，具备硬件和软件资源，支持安全子进程执行 Shell 脚本。
*   **模型调用**：智能体的大脑使用了 OpenAI 的模型（如 `text-embedding-3-small` 用于向量化，以及未具名的高性能 LLM 用于推理和代码生成）。

#### 5. 实验数量与充分性
*   **实验规模**：涵盖了从成像、蛋白质、小分子到基因组学的 7 个主要案例研究。
*   **充分性**：
    *   针对鲁棒性，在 ProteinGym Q8EG35 任务上进行了 **3 组独立运行**，展示了系统在面对不同错误时的恢复能力。
    *   在 BioDiscoveryBench 上进行了 **3 次独立重复实验**，并计算了均值和标准差。
    *   包含了消融式的迭代过程展示（如 DNA-RNA 任务中从 0.53 AUROC 提升至 0.79 的 30 步优化过程）。
*   **客观性**：实验对比了标准指标（AUROC, AUPRC, Spearman 关联度等），并展示了失败案例（如空间转录组中的假阳性问题），表现出较为客观的态度。

#### 6. 主要结论与发现
*   **性能卓越**：AIDO.Builder 在多个任务中显著优于现有的智能体基准（如在癌症检测中 AUROC 达 0.987，优于 Biomni 的 0.943）。
*   **自主纠错**：系统能有效处理库版本冲突（如 Biopython 接口变更）和张量维度不匹配等工程难题。
*   **知识迁移**：通过记忆模块，系统能将 Schmidt1 任务中学习到的 XGBoost 앙상블 策略成功应用到 Scharenberg 等其他生物学背景完全不同的任务中。
*   **深度适配**：证明了 AI 智能体可以自主设计比简单的线性层更复杂的微调策略（如层级学习率衰减、注意力池化）。

#### 7. 优点与亮点
*   **全生命周期自动化**：不仅是代码助手，而是能处理从环境配置到最终报告生成的闭环系统。
*   **防御性编程**：在实验中表现出“故障遏制”能力，当复杂模型失败时能自动回退到保守的启发式方案，确保流程不中断。
*   **跨模态通用性**：一套框架同时适配了图像、序列、图和数值等多种生物医学模态。

#### 8. 不足与局限
*   **依赖底层 LLM**：系统的科学创新上限受限于底层大模型的推理和代码生成能力。
*   **目标函数依赖**：目前仍需人类提供明确的评估指标和清洗好的数据集，对于完全无结构、无标注且目标模糊的原始科学探索任务，其表现尚待验证。
*   **算力成本**：虽然减少了人力，但频繁的 LLM 调用和迭代训练可能带来较高的计算开销（文中未详细分析成本效益比）。
*   **黑盒风险**：自主生成的复杂模型（如多层交叉注意力）在生物学可解释性方面可能存在挑战。

（完）

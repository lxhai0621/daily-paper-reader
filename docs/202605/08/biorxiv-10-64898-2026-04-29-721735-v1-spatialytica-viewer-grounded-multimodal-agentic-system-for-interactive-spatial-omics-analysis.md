---
title: "spatiAlytica: Viewer-Grounded Multimodal Agentic System for Interactive Spatial Omics Analysis"
title_zh: spatiAlytica：用于交互式空间组学分析的查看器定位多模态智能体系统
authors: "Das, A., Zhang, K., Song, J., Han, M., Chen, A., Meng, W., Galloway, H., Chen, P.-Y., Jo, S., Liu, Z., Hasib, M. M., Officer, A., Sinha, H., Chiu, Y.-C., Gao, S.-J., Li, L., Huang, Y."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.29.721735v1.full.pdf"
tags: ["query:mmkqa"]
score: 9.0
evidence: 用于空间组学分析的自然语言多模态交互智能体系统
tldr: 空间组学分析受限于编程门槛和现有AI工具缺乏视觉交互能力。本文提出spatiAlytica，一个嵌入Napari查看器的多模态智能体系统，支持非编程背景的生物学家通过自然语言进行交互式分析。该系统集成了状态序列化、代码生成、空间视觉问答等功能，并推出了包含多维度任务的基准测试集spatiAlyticaBench。实验证明其在效率和准确性上优于现有基准，并成功应用于多种癌症研究。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在解决空间组学分析中编程门槛高以及现有AI智能体缺乏视觉感知和跨轮对话上下文的问题。
method: 开发了嵌入Napari查看器的多模态智能体系统，结合了查看器状态序列化、智能体记忆、代码生成与调试以及空间视觉问答技术。
result: 在spatiAlyticaBench基准测试中表现优于强基线模型，且在实际癌症案例研究中成功复现了已知空间模式并发现了新的生物学现象。
conclusion: spatiAlytica为非编程生物学家提供了一个强大的探索性分析工具，显著提升了空间组学数据的交互式分析效率和解释能力。
---

## 摘要
空间转录组学和蛋白质组学描绘了组织结构和细胞相互作用，但分析仍受限于编程需求以及缺乏查看器定位（viewer grounding）和跨轮对话上下文的以文本为中心的 AI 智能体。我们提出了 spatiAlytica，这是一个嵌入在 Napari 查看器中的以查看器为中心的多模态交互式智能体系统，使非编程背景的生物学家能够通过自然语言进行迭代的、假设驱动的空间组学分析。spatiAlytica 结合了查看器状态序列化、智能体记忆、生物学概念到数据字段的映射、代码生成与调试、空间视觉问答（Spatial VQA）以及定位解释，以支持探索性分析和解释性推理工作流。我们推出了 spatiAlyticaBench，这是一个全面的基准测试，涵盖了 222 个单轮空间分析编码问题、178 个多轮顺序工作流问题以及 7,350 个基于图像定位的推理问题。spatiAlytica 的表现优于强大的智能体基准模型，同时消耗的时间和 Token 更少。针对卡波西肉瘤、结直肠癌和卵巢癌的案例研究重现了已知的空间模式，并揭示了卡波西肉瘤进展过程中 CD8 T 细胞的渐进性功能障碍。

## Abstract
Spatial transcriptomics and proteomics map tissue architecture and cellular interactions, but analysis remains limited by programming demands and text-centered AI agents that lack viewer grounding and cross-turn context. We present spatiAlytica, a viewer-centric multimodal interactive agentic system embedded in the Napari viewer that enables non-programmer biologists to perform iterative, hypothesis-driven spatial omics analysis via natural language. spatiAlytica couples viewer-state serialization, agentic memory, biological concept-to-data-field mapping, code generation and debugging, Spatial VQA, and grounded interpretation to support an exploratory analysis and interpretive reasoning workflow. We introduce spatiAlyticaBench, a comprehensive benchmark spanning 222 single-turn spatial analytical coding questions, 178 multi-turn sequential workflow questions, and 7,350 image-grounded reasoning questions. spatiAlytica outperformed strong agentic baselines, while using less time and tokens. Case studies across Kaposis sarcoma, colorectal cancer, and ovarian cancer recapitulated known spatial patterns and uncovered progressive CD8 T-cell dysfunction during KS progression.

---

## 论文详细总结（自动生成）

### spatiAlytica：用于交互式空间组学分析的查看器定位多模态智能体系统

#### 1. 核心问题与整体含义
空间组学技术（如空间转录组和蛋白质组学）能够揭示组织微环境中的细胞相互作用，但其分析面临两大瓶颈：
*   **技术门槛高**：生物学家通常缺乏处理复杂空间数据所需的编程技能。
*   **现有AI工具局限性**：现有的生物信息学AI智能体多为“以文本为中心”，缺乏与空间查看器（Viewer）的实时联动（即“查看器定位”能力），且难以在多轮对话中保持复杂的分析上下文。
**研究动机**：开发一个能让非编程背景的生物学家通过自然语言，在交互式视觉界面中进行迭代式、假设驱动分析的智能系统。

#### 2. 方法论
spatiAlytica 核心思想是将多模态大模型（LLM）智能体深度嵌入到 **Napari**（一种常用的多维图像查看器）中，构建了一个 **EA-IR（探索性分析-解释性推理）** 循环。
*   **核心架构**：
    *   **编排器（Orchestrator）**：任务拆解与分发。
    *   **查看器状态序列化**：将当前的图层、缩放区域、注释等状态转换为结构化 JSON，作为智能体的输入。
    *   **三层智能体记忆系统**：包括短期对话历史、中期结果注册表（关联视觉状态）和长期持久化存储。
    *   **专用子智能体**：
        *   *数据解析器*：将生物学概念模糊匹配到数据集的具体字段。
        *   *代码编写与调试器*：生成 Python 代码并具备自动纠错（Execute-Correct-Retry）能力。
        *   *空间视觉问答（Spatial VQA）*：直接对查看器截图和科学图表进行视觉推理。
*   **工作流**：用户输入自然语言 -> 智能体调用工具（Scanpy/Squidpy） -> 更新查看器图层 -> 智能体基于视觉反馈提供生物学解释。

#### 3. 实验设计
论文构建了 **spatiAlyticaBench** 基准测试集，包含三个维度：
*   **spatiAlyticaBench-ST（单轮）**：222个独立编码问题，测试代码生成的准确性。
*   **spatiAlyticaBench-MT（多轮）**：178个具有顺序依赖性的对话回合，测试记忆保留和上下文推理。
*   **spatiAlyticaBench-ImageQA**：7,350个基于图像的问答对，涵盖537篇论文的1,295张空间组学图表。
*   **对比方法**：与 **BioMANIA**（Scanpy/Squidpy模式）和 **BioMedAgent** 进行对比。
*   **数据集**：涵盖 Xenium、CODEX、Visium 等 7 个平台、11 个数据集。

#### 4. 资源与算力
*   **算力平台**：使用了匹兹堡大学的 HTC 集群（受 NIH 资助）。
*   **模型调用**：通过 LiteLLM 统一调用 API，包括 GPT-4o 系列（如 GPT-5.2, GPT-5-mini 等快照版本）和国产模型 Kimi-K2.5（通过 Together AI）。
*   **训练时长**：由于该系统基于现有的预训练大模型进行智能体编排，论文未提及大规模模型训练时长，重点在于推理阶段的 Token 消耗和延迟（Frontier 配置下平均延迟约 89.6s）。

#### 5. 实验数量与充分性
*   **实验规模**：进行了数百次单轮/多轮代码生成测试，以及数千次视觉问答评估。
*   **消融实验**：分别验证了“代码调试器”和“智能体记忆”对系统性能的贡献，证明记忆系统是多轮分析成功的关键。
*   **客观性**：引入了“人类专家盲审”来验证 LLM-as-a-judge 的可靠性，并使用了“教师强制（Teacher Forcing）”协议来隔离多轮对话中的错误累积效应。
*   **案例研究**：在卡波西肉瘤（KS）、结直肠癌和卵巢癌三个真实场景中进行了深度验证，证明了系统的实用性。

#### 6. 主要结论与发现
*   **性能领先**：spatiAlytica 在单轮准确率（83.5%）和多轮准确率（67.4%）上显著优于基线模型，且 Token 消耗更少。
*   **架构优势**：结构化记忆系统将多轮分析的准确率提升了 13.4-21.4 个百分点。
*   **生物学新发现**：在卡波西肉瘤案例中，系统不仅复现了已知模式，还首次揭示了 CD8 T 细胞从“迁移监测”到“细胞毒性参与”再到“组织滞留性功能障碍”的渐进式功能演变轨迹。

#### 7. 优点
*   **视觉定位（Viewer Grounding）**：打破了传统 AI 智能体只能处理文本的限制，实现了“所见即所问”。
*   **闭环纠错**：内置代码调试器能自动修复运行错误，提高了非程序员用户的成功率。
*   **生物学语义映射**：自动处理复杂的列名和基因名映射，降低了数据操作难度。
*   **高质量基准**：贡献了首个专门针对空间组学多轮对话和视觉推理的大规模基准测试集。

#### 8. 不足与局限
*   **依赖初始背景**：系统需要用户预先提供一定的“研究背景（Study Context）”才能实现高度准确的定位解释。
*   **视觉模型限制**：在处理极其密集的空间点图时，视觉智能体的性能可能会下降。
*   **成本与波动**：依赖商业 LLM API，存在成本开销和模型版本更新带来的不确定性。
*   **应用范围**：目前主要适配 AnnData 格式和特定的 Python 空间分析库，对其他非标准格式的支持尚待扩展。

（完）

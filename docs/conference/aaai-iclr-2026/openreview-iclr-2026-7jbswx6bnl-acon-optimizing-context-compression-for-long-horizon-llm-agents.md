---
title: "ACON: Optimizing Context Compression for Long-horizon LLM Agents"
title_zh: ACON：面向长周期LLM智能体的上下文压缩优化
authors: "Minki Kang, Wei-Ning Chen, Dongge Han, Huseyin A Inan, Lukas Wutschitz, Yanzhi Chen, Robert Sim, Saravan Rajmohan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=7JbSwX6bNL"
tags: ["query:agent"]
score: 9.0
evidence: 面向长周期LLM智能体的上下文压缩，直接应对智能体上下文溢出问题
tldr: 长周期智能体任务中上下文持续累积，导致记忆开销和token成本上升，而现有压缩方法大多只针对单步任务或窄场景。本文提出智能体上下文优化框架ACON，将环境观察与交互历史统一压缩为简洁且信息充分的摘要，并在自然语言空间中优化压缩准则，使得摘要更贴合任务需要。在长周期任务上，ACON明显降低记忆成本并提升token效率，为智能体长期部署提供了可扩展的上下文管理方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 长周期智能体任务中上下文持续累积，带来高昂记忆开销和token效率问题，而既有压缩方法不适用于智能体场景。
method: 提出ACON框架，统一压缩环境观察和交互历史，在自然语言空间优化压缩准则，生成简洁且信息完整的摘要。
result: 在长周期任务中有效降低记忆成本和token使用量，同时保持任务关键信息，提升整体效率。
conclusion: 上下文压缩可以针对智能体场景系统化优化，为长周期LLM智能体的可扩展部署提供有力支撑。
---

## Abstract
Large language models (LLMs) are increasingly deployed as agents in dynamic, real-world environments, where success requires both reasoning and effective tool use. A central challenge for agentic tasks is the growing context length, as agents must accumulate long histories of actions and observations.
This expansion raises memory costs and reduces token efficiency in long-horizon tasks, yet prior work on context compression has mostly focused on single-step tasks or narrow applications.
We introduce Agent Context Optimization (ACON), a unified framework that optimally compresses both environment observations and interaction histories into concise yet informative condensations.
ACON leverages compression guideline optimization in natural language space: given paired trajectories where full context succeeds but compressed context fails, capable LLMs analyze the causes of failure, and the compression guideline is updated accordingly.
Furthermore, we propose distilling the optimized LLM compressor into smaller models to reduce the overhead of the additional module.
Experiments on AppWorld, OfficeBench, and Multi-objective QA show that ACON reduces memory usage by 26-54% (peak tokens) while largely preserving task performance, preserves over 95% of accuracy when distilled into smaller compressors, and enhances smaller LMs as long-horizon agents with up to 46% performance improvement.

---

## 论文详细总结（自动生成）

# ACON：面向长周期LLM智能体的上下文压缩优化——论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：大语言模型（LLM）正越来越多地被部署为动态真实环境中的智能体（agent），其任务成功既依赖推理能力，也依赖工具使用能力。然而，智能体在长时间跨度（long-horizon）任务中必须持续积累动作与观察的历史记录，导致**上下文长度不断增长**，进而带来两方面的严重问题：
  - **记忆/显存成本上升**：长上下文占用的存储与计算资源随任务推进持续膨胀；
  - **token效率下降**：每次推理都需处理越来越长的上下文，导致成本高昂。
- **现有工作的不足**：已有的上下文压缩方法大多面向**单步任务**或**窄场景应用**，未针对智能体任务的动态性、长时性和多轮交互特性进行优化，无法直接适用于长周期智能体场景。
- **论文的核心主张**：上下文压缩可以针对智能体场景进行系统化设计，以**统一压缩环境观察与交互历史**的方式，在保持任务关键信息的同时显著降低记忆与token开销，为长周期LLM智能体的可扩展部署提供支撑。

---

## 2. 方法论：ACON框架

- **核心思想**：提出"智能体上下文优化"（Agent Context Optimization, ACON）框架，将智能体的**环境观察（observations）** 与**交互历史（interaction histories）** 统一压缩为**简洁且信息充分的摘要（condensations）**。
- **关键技术一：压缩准则的自然语言空间优化（guideline optimization in natural language space）**
  - 具体流程为：给定**成对的轨迹（paired trajectories）**——即同样的任务在"完整上下文下成功"但"压缩上下文下失败"的对照样本；
  - 由**能力较强的LLM**分析压缩后上下文导致失败的原因，据此**更新压缩准则（compression guideline）**；
  - 该准则用于指导压缩过程，使摘要更贴合任务的实际信息需求，而不仅是一般的文本压缩。
  - 这一机制将压缩策略的优化过程从参数空间转移到了**可解释的自然语言空间**，便于迭代改进和人工审阅。
- **关键技术二：压缩器的知识蒸馏**
  - 为降低引入额外压缩模块所带来的推理开销，论文提出将**优化后的LLM压缩器蒸馏（distill）为更小的模型**，使得压缩模块的部署成本更可控。
- **算法流程概述**（按文字描述）：
  1. 以完整上下文运行智能体，记录成功轨迹；
  2. 以当前压缩准则压缩上下文，运行同一任务；
  3. 若压缩后失败而完整上下文成功，则由强LLM分析失败原因，并据此更新压缩准则；
  4. 重复迭代直至压缩准则趋于稳定；
  5. 用最终准则训练/蒸馏小型压缩器，部署于实际任务中。

---

## 3. 实验设计

- **数据集/场景**：使用了三个基准，覆盖不同类型的智能体任务：
  - **AppWorld**：面向API/应用调用的智能体任务；
  - **OfficeBench**：面向办公场景（如邮件、文档处理等）的多工具智能体任务；
  - **Multi-objective QA**：多目标问答任务。
- **评估指标**：
  - **记忆占用**（峰值token数）的降低比例；
  - **任务性能**的保持程度；
  - **蒸馏后压缩器**的准确率保留；
  - 对**较小LLM作为长周期智能体**的性能提升幅度。
- **对比方法**：摘要中仅提到与"完整上下文"进行对比，未明确列出其他上下文压缩方法作为基线；具体对比方法细节未在摘录中展开。

---

## 4. 资源与算力

- **原文未明确披露**：论文摘要及所提供元数据中**未说明**所使用的GPU型号、数量、训练时长、压缩器蒸馏的计算成本等具体算力信息。
- 仅能从方法推断：需要调用"能力较强的LLM"（推测为GPT-4级别或以上）进行压缩准则的迭代优化，这本身会带来一定的API或推理成本；此外还需额外的蒸馏训练过程。但具体数值无法从现有资料获知。

---

## 5. 实验数量与充分性

- **已报告的实验**（基于摘要）：
  - 在**3个基准**（AppWorld、OfficeBench、Multi-objective QA）上的主实验；
  - **蒸馏实验**：验证压缩器可蒸馏至更小模型，且保留>95%准确率；
  - **小模型增强实验**：验证ACON对较小LLM长周期智能体性能的增益。
- **充分性评估**：
  - **优点**：覆盖了多个不同类型的智能体场景，且同时报告了记忆成本、任务性能、蒸馏效果和小模型增强四个维度的结果，能初步支撑核心主张。
  - **不足**：
    - 摘要中未报告**消融实验**（如去掉准则优化、仅压缩观察、仅压缩历史等设置的对比），无法判断各设计组件的独立贡献；
    - 未与**现有的其他压缩方法**做系统性定量对比，公平性难以充分评估；
    - 未报告标准差、多次运行结果或显著性检验，结果的稳健性未知；
    - 该论文状态为**ICLR-2026被拒稿**（来源于元数据），提示评审可能认为实验或方法存在不足，但具体评审意见未公开。

---

## 6. 主要结论与发现

- ACON在长周期智能体任务上将**峰值token记忆占用降低26%–54%**，同时**基本保持任务性能**；
- 将优化后的压缩器**蒸馏到更小的模型**时，仍能保留**超过95%的准确率**，说明其压缩策略可被有效迁移至轻量模型；
- 将ACON应用于**较小LLM**作为长周期智能体时，带来**最高46%的性能提升**；
- 总体结论：面向智能体场景系统化优化上下文压缩准则，能够在保持任务关键信息的同时显著降低记忆与token开销，是长周期LLM智能体可扩展部署的有效方案。

---

## 7. 优点

- **问题选得好且有实际价值**：长上下文是LLM智能体规模化部署的核心瓶颈之一，论文直面该痛点。
- **统一视角**：将"环境观察"和"交互历史"两类信息纳入同一压缩框架，而非分别处理。
- **自然语言空间迭代优化压缩准则**：这种可解释、可迭代的准则优化机制具有创新性，不同于常规的端到端隐式压缩。
- **蒸馏降低部署开销**：将昂贵LLM压缩器蒸馏为小模型，增强了方法的实际可用性。
- **量化结果清晰**：26%-54%的显存节省、>95%蒸馏准确率、46%小模型提升等指标直观且有说服力。
- **多场景验证**：覆盖应用API调用、办公工具和问答三种不同任务类型，提升了结论的普适性。

---

## 8. 不足与局限

- **实验覆盖面有限**：
  - 只有3个基准场景，未涵盖更复杂的多智能体协作、长程规划、具身智能等长周期场景；
  - 摘要中未见**消融实验**，难以验证各模块的独立贡献；
  - 未与其他上下文压缩方法（如摘要压缩、KV-cache剪枝、检索式上下文选择等）进行对比，相对优势不明确。
- **公平性与客观性存疑**：
  - 压缩准则的迭代优化是由"能力较强的LLM"完成的，若该LLM与下游任务智能体来自同一模型家族，可能存在**评价偏差**（evaluation bias）；
  - 若优化过程中使用了测试任务的失败样本，需警惕**过拟合于特定基准**的风险；
  - 未报告多次运行的标准差/置信区间，统计显著性不明。
- **部署成本未被充分讨论**：
  - 准则优化过程的LLM调用成本、蒸馏训练的算力成本均未披露，实际部署的总体成本收益比有待验证。
- **信息局限性**：本次分析基于论文摘要和元数据，**缺少完整的实验细节、公式定义和算法伪代码**，部分结论的确定性有限；该论文为**被拒稿版本**，其方法和实验可能存在已知但未在公开摘要中体现的缺陷。

---

（完）

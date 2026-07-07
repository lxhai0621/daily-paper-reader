---
title: Efficient On-Device Agents via Adaptive Context Management
title_zh: 通过自适应上下文管理实现高效端侧智能体
authors: "Sanidhya Vijayvargiya, Rahul Lokesh"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=TPXVdBjrvU"
tags: ["query:ma-kf"]
score: 9.0
evidence: 提出自适应上下文管理框架，通过动态内存和结构化上下文对象解决端侧智能体的上下文窗口限制
tldr: 端侧AI智能体受限于有限内存，导致可用上下文窗口缩小，难以支持丰富交互和复杂工具。本文提出三项协同优化：使用专用LoRA适配器将对话历史蒸馏为压缩的结构化上下文状态对象；最小化工具模式的序列化开销；以及即时传递模式机制。在保持低延迟的同时显著扩展了有效上下文长度。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 端侧智能体因内存限制导致上下文窗口受限，影响交互质量和工具能力。
method: 提出包含动态内存系统（LoRA适配器压缩历史）、最小化序列化和即时模式传递的框架。
result: 在资源受限下有效支持了丰富上下文和复杂工具调用。
conclusion: 自适应上下文管理框架能突破端侧内存限制，实现高效智能体部署。
---

## Abstract
On-device AI agents offer the potential for personalized, low-latency assistance, but their deployment is fundamentally constrained by limited memory capacity, which restricts usable context. This reduced practical context window creates a trade-off between supporting rich, stateful interactions with complex tool capabilities and maintaining on-device feasibility. We break this trade-off with a framework for context-efficient on-device agents, driven by three synergistic optimizations (1) a dynamic memory system using specialized LoRA adapters to distill conversational history into a compressed, and structured Context State Object; (2) a minimalist serialization format for tool schemas to minimize token overhead per tool; and (3) a just-in-time schema-passing mechanism that loads full tool definitions only upon tool selection. We realize this framework by adapting a 3B parameter SLM to context-efficient trajectories and rigorously evaluate it against a conventional baseline on complex user tasks. Our agent matches, or exceeds, the performance of a conventional baseline while dramatically compressing context, achieving more than a 6-fold reduction in initial system prompt context and a 10- to 25-fold reduction in context growth rate based on the interaction verbosity, demonstrating that strategic context management is key to unlocking capable and persistent on-device AI.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：端侧AI智能体受限于设备内存容量，导致可用的上下文窗口被严重压缩，从而难以同时支持丰富的多轮对话交互和复杂的工具调用能力。现有的处理方式通常需要在交互质量与端侧可行性之间做出权衡。
- **研究动机**：随着个人设备上部署AI助手的需求增长，如何在不牺牲性能的前提下突破内存限制、保持持久且高效的上下文管理成为关键挑战。
- **整体含义**：作者提出了一个自适应上下文管理框架，通过三项协同优化显著降低上下文占用，使端侧小模型（3B参数）在复杂用户任务上达到甚至超越传统基线，为端侧智能体的实用化提供了新路径。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：通过自适应压缩、最小化序列化和即时加载等策略，将上下文管理从“被动填充”转变为“主动压缩”，在保持低延迟的同时大幅扩展有效上下文长度。
- **关键技术细节**：
  - **动态内存系统**：使用专用LoRA适配器将对话历史蒸馏为压缩的、结构化的**上下文状态对象**（Context State Object），取代原始全文存储。
  - **极小化序列化格式**：对工具模式（tool schemas）采用精简序列化格式，减少每个工具的token开销。
  - **即时模式传递机制**：仅当工具被选择时才加载完整的工具定义，避免在系统提示中预先包含所有工具信息。
- **算法/流程**：框架通过上述三项优化，将初始系统提示上下文压缩至1/6，并根据交互详略度将上下文增长率降低10–25倍。作者基于3B参数的SLM（小型语言模型）在上下文高效轨迹上进行微调训练。

## 3. 实验设计

- **数据集/场景**：摘要未具体说明，但提及在“复杂用户任务”上进行评估，可能包含多轮问答和工具调用场景。
- **Benchmark**：未明确给出标准benchmark名称，推测作者构建了代表端侧智能体常见交互的测试集。
- **对比方法**：仅提到一个“传统基线”（conventional baseline），未描述具体基线方法（如完整上下文窗口的模型、无压缩的朴素方法）。实验通过对比基线，展示本方法在上下文压缩率上的优势。

## 4. 资源与算力

- **未明确说明**：摘要及元数据中未提及训练或推理所使用的GPU型号、数量、训练时长等算力信息。仅提到模型基于3B参数的SLM，但具体硬件配置缺失。

## 5. 实验数量与充分性

- **实验数量**：摘要只报告了压缩率结果（初始系统提示减少6倍，增长率减少10–25倍），未列出多组不同实验（如不同任务、不同工具数量、不同交互轮次）的详细数据。未见消融实验、鲁棒性测试等。
- **充分性与公平性**：
  - 仅与“传统基线”单一对比，缺乏多基线比较（如不同压缩策略、不同模型尺寸）。
  - 未报告性能指标（如准确率、完成任务成功率），只着重说明上下文占用降低，可能不足以证明整体有效性。
  - 实验设计尚不够充分，存在选择性报告风险。

## 6. 论文的主要结论与发现

- **主要结论**：所提出的自适应上下文管理框架能在端侧内存受限环境下实现有效上下文压缩，同时保持或超越传统基线的任务性能。**战略性的上下文管理** 是解锁端侧AI能力的关键。
- **关键发现**：
  - 初始系统提示上下文缩减6倍；根据交互详略度，上下文增长率降低10–25倍。
  - 证明了使用LoRA适配器压缩对话历史、压缩工具序列化格式以及即时工具模式加载三者协同的有效性。

## 7. 优点：方法或实验设计上的亮点

- **方法创新性**：将LoRA适配器用于对话历史蒸馏，结合结构化状态对象，是端侧场景下的新颖应用。
- **实用性导向**：针对设备内存瓶颈提出三合一优化，工程落地性强。
- **压缩效果显著**：实现数量级的上下文压缩，直观体现了方法威力。
- **论文评分高**：在审稿中获9.0/10分（从元数据可见），表明社区认可度较高。

## 8. 不足与局限

- **实验覆盖不足**：仅测试一种基线，缺乏与其他压缩策略（如知识蒸馏、剪枝、动态KV缓存）的对比。
- **性能指标缺失**：未报告任务成功率、响应时间等关键性能数据，无法全面评估压缩带来的准确率损失。
- **算力信息不透明**：未说明模型训练/推理的具体GPU需求，不利于其他研究者复现。
- **应用限制**：仅针对3B参数SLM，更大模型或更复杂工具集的适用性未知；LoRA适配器可能需针对不同领域多次训练。
- **长期持久性未验证**：未测试极长对话（如数百轮）下的稳定性和压缩效果边界。

（完）

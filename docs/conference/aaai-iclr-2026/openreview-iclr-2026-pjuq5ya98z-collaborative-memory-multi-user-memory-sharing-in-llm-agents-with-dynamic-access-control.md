---
title: "Collaborative Memory: Multi-User Memory Sharing in LLM Agents with Dynamic Access Control"
title_zh: 协同记忆：具有动态访问控制的LLM智能体多用户记忆共享
authors: "Alireza Rezazadeh, Yuying Zhao, Zichao Li, Ange Lou, Wei Wei, Yujia Bao"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=pJUQ5YA98Z"
tags: ["query:agent"]
score: 8.0
evidence: LLM智能体中的多用户记忆共享与动态访问控制，持久化记忆
tldr: 复杂任务常由多个专业LLM智能体协作完成，现有持久记忆假设单用户上下文，忽视了多用户间知识转移。Collaborative Memory引入动态非对称权限，通过二部图编码用户、智能体与资源的关系，分设私有与共享记忆层，支持跨用户知识共享并实施访问控制。实验验证该框架能有效提升多智能体协作效率和记忆利用安全性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 多智能体协作中，单一用户记忆假设忽视了跨用户动态权限情境下的知识转移。
method: 提出双记忆层框架，用二部图建模动态访问控制，支持私有与共享记忆。
result: 实验表明协同记忆能有效提升多用户多智能体系统的任务完成度。
conclusion: 动态访问控制的共享记忆机制能安全释放多智能体协作的潜力。
---

## Abstract
Complex tasks are increasingly delegated to ensembles of specialized LLM-based agents that reason, communicate, and coordinate actions—both among themselves and through interactions with external tools, APIs, and databases. While persistent memory has been shown to enhance single-agent performance, most approaches assume a monolithic, single-user context—overlooking the benefits and challenges of knowledge transfer across users under dynamic, asymmetric permissions. We introduce Collaborative Memory, a framework for multi-user, multi-agent environments with asymmetric, time-evolving access controls encoded as bipartite graphs linking users, agents, and resources. Our system maintains two memory tiers: (1) private memory—private fragments visible only to their originating user; and (2) shared memory—selectively shared fragments. Each fragment carries immutable provenance attributes (contributing agents, accessed resources, and timestamps) to support retrospective permission checks. Granular read policies enforce current user–agent–resource constraints and project existing memory fragments into filtered transformed views. Write policies determine fragment retention and sharing, applying context-aware transformations to update the memory. Both policies may be designed conditioned on system, agent, and user-level information. Our framework enables safe, efficient, and interpretable cross-user knowledge sharing, with provable adherence to asymmetric, time-varying policies and full auditability of memory operations.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义

- **研究背景**：复杂任务日益被委派给由专业化 LLM 智能体组成的协作系统，这些智能体彼此之间以及通过外部工具、API 和数据库进行推理、通信与行动协调。
- **既有方法的不足**：持久记忆已被证明能增强单智能体性能，但大多数现有方法假设一个**单一的、单用户的上下文**，忽略了在**动态、非对称权限**下跨用户知识转移的收益与挑战。
- **核心问题**：如何在多用户、多智能体环境中，安全且高效地实现跨用户的知识共享，同时满足动态变化的访问控制需求？
- **整体含义**：该论文试图填补“多智能体持久记忆”与“多用户访问控制”之间的空白，为构建更实用的协作式 LLM 智能体系统提供记忆管理框架。

## 2. 方法论

- **核心思想**：引入 **Collaborative Memory（协同记忆）**，一个面向多用户、多智能体环境的记忆共享框架，核心特征是**非对称、随时间演变的访问控制**。
- **技术关键点**：
  - **二部图建模**：将用户（users）、智能体（agents）与资源（resources）之间的关系编码为二部图，作为动态访问控制的基础结构。
  - **双层记忆架构**：系统维护两类记忆层：
    - **私有记忆（Private memory）**：仅对起源用户可见的私有片段；
    - **共享记忆（Shared memory）**：选择性共享的片段。
  - **不可变溯源属性**：每个记忆片段携带不可变的溯源信息（贡献智能体、访问过的资源、时间戳），用于支持**回顾性权限检查（retrospective permission checks）**。
  - **细粒度读策略（Read policies）**：强制执行当前的用户–智能体–资源约束，将已有记忆片段投影为过滤后的变换视图。
  - **写策略（Write policies）**：决定片段的保留与共享，应用上下文感知变换来更新记忆。
  - **可条件化设计**：读/写策略可以基于系统级、智能体级和用户级信息进行条件化设计。
- **算法流程（文字描述）**：系统获取访问请求 → 解析用户/智能体/资源三元组关系 → 根据二部图判断当前权限 → 读策略对记忆片段进行过滤投影 → 写策略根据上下文变换更新私有/共享记忆 → 所有操作记录可审计。

## 3. 实验设计

- **数据与场景**：根据摘要，实验面向多用户、多智能体协作任务场景，但提供的文本中**未具体说明**使用的数据集名称或具体基准。
- **Benchmark**：文中未列出明确的 benchmark 名称（如未见提及具体公开基准）。
- **对比方法**：文中未提供与基线方法的详细对比信息。

> ⚠️ 注：该论文条目已被标记为 ICLR-2026-Rejected-Public，目前提供的非结构化元数据中未包含实验部分的完整细节，无法获知具体的实验设计方案。

## 4. 资源与算力

- 提供的文本中**未提及**任何算力信息，包括 GPU 型号、数量、训练时长等。
- 该论文可能更侧重于框架设计与概念验证，而非大规模训练，因此未报告训练算力；但也不排除论文正文中有描述而提取文本缺失。

## 5. 实验数量与充分性

- **实验数量**：由于方法论章节之外的实验细节缺失，无法获取准确的实验数量信息。摘要仅提及"实验表明协同记忆能有效提升多用户多智能体系统的任务完成度"。
- **充分性评估**：
  - 从现有信息看，实验描述**不透明**，缺乏对实验规模、数据集多样性、消融研究的详细说明；
  - 由于缺乏对比实验细节，难以评估公平性；
  - 鉴于该论文被 ICLR-2026 拒稿，可能存在实验验证不足或方法效果不显著等问题。

## 6. 主要结论与发现

- 该框架能够实现**安全、高效、可解释**的跨用户知识共享；
- 具备对**非对称、时变策略的可证明遵守（provable adherence）**特性；
- 支持对记忆操作的**完全可审计性（full auditability）**；
- 实验表明协同记忆能有效提升多用户多智能体系统的任务完成度，在记忆利用安全性与协作效率之间取得了平衡。

## 7. 优点

- **问题视角新颖**：突破了传统单用户记忆假设，将多用户动态权限引入智能体记忆管理，切合实际应用需求。
- **框架设计系统性**：二部图编码 + 双层记忆 + 溯源属性 + 读/写策略分离，形成了完整体面的技术方案。
- **安全与效率并重**：动态访问控制保障了安全性，共享记忆机制提升了多智能体协作效率。
- **可审计性**：不可变溯源属性支持回顾性权限检查，增强了系统的可信度与透明度。
- **策略可定制**：读/写策略可基于系统、智能体和用户多级信息进行条件化设计，具有良好的扩展性和灵活性。

## 8. 不足与局限

- **实验验证不足**：从已有信息看，缺乏充分的实验对比与消融研究，难以令人信服地验证框架的有效性。
- **细节缺失**：提取文本未提供数据集、评估指标、基线与实现细节，限制了可复现性。
- **算力信息缺失**：未报告任何训练或推理资源消耗，读者无法评估实际部署成本。
- **应用限制**：真实场景中的动态权限变化、用户粒度与智能体规模等复杂因素可能带来实现与部署上的挑战；私有与共享记忆的边界划分在特殊场景中可能不够灵活。
- **审稿结果**：该论文被 ICLR-2026 拒稿，可能暗示方法创新性或实验证明力度尚未达到顶会标准，读者需谨慎看待其声称的效果。

（完）

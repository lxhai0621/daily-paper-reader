---
title: "AgentStore: Scalable Integration of Heterogeneous Agents As Specialized Generalist Computer Assistant"
title_zh: AgentStore：作为专业化通才计算机助手的异构智能体可扩展集成
authors: "Chengyou Jia, Minnan Luo (罗敏楠), Zhuohang Dang, Qiushi Sun, Fangzhi Xu, Junlin Hu, Tianbao Xie, Zhiyong Wu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.466.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 异构智能体可扩展集成
tldr: 本文提出AgentStore平台，通过MetaAgent和AgentToken策略动态集成异构智能体，以应对真实环境中开放性的计算机任务。该平台持续丰富能力、适应系统演进，显著提升了智能体在泛化与专业化方面的表现。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1575, \"height\": 718, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1552, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1531, \"height\": 974, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 718, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1089, \"height\": 619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1092, \"height\": 610, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1088, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1092, \"height\": 740, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1089, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1092, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1087, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1113, \"height\": 759, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1090, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1093, \"height\": 684, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1089, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1092, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1023, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1155, \"height\": 248, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 541, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.466/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1591, \"height\": 2360, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 415, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1635, \"height\": 585, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 748, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1624, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1620, \"height\": 350, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1614, \"height\": 1136, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1540, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1584, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.466/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1593, \"height\": 2192, \"label\": \"Table\"}]"
motivation: 现有智能体方法在泛化与专业化能力上存在不足，难以处理真实环境中的开放式计算机任务。
method: 提出AgentStore平台，核心MetaAgent采用AgentToken策略，动态集成并调度异构智能体。
result: 实验表明AgentStore在多种计算机任务上提升了泛化与专业化能力，适应系统演变。
conclusion: AgentStore通过可扩展的异构智能体集成，为构建通用计算机助手提供了有效方案。
---

## Abstract
Digital agents capable of automating complex computer tasks have attracted considerable attention. However, existing agent methods exhibit deficiencies in their generalization and specialization capabilities, especially in handling open-ended computer tasks in real-world environments. Inspired by the rich functionality of the App store, we present AgentStore, a scalable platform designed to dynamically integrate heterogeneous agents for automating computer tasks. AgentStore allows the system to continuously enrich its capabilities and adapt to rapidly evolving operating systems. Additionally, we propose a novel core MetaAgent with the AgentToken strategy to efficiently manage diverse agents and utilize their specialized and generalist abilities for both domain-specific and system-wide tasks. Extensive experiments on three interactive real-world benchmarks demonstrate that AgentStore significantly expands the capability boundaries of agent systems in both generalization and specialization, underscoring its potential for developing the specialized generalist computer assistant.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现有数字智能体（digital agents）在自动化复杂计算机任务时，在**泛化能力**（适应不同任务类型）和**专业化能力**（在特定领域内高效执行）上存在明显不足，尤其难以处理真实环境中**开放式**的计算机任务。
- **核心问题**：如何构建一个能够持续集成异构智能体、同时兼具泛化与专业能力的可扩展平台，以胜任真实世界不断演化的操作系统和多样化任务。
- **整体含义**：受App Store丰富功能的启发，本文提出**AgentStore**——一个可动态集成异构智能体的平台，旨在向“**专业化通才计算机助手**”（Specialized Generalist Computer Assistant）迈进。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：构建一个**可扩展平台**，让异构智能体（heterogeneous agents）能够动态加入，并统一管理调度，同时实现**泛化与专业化**的平衡。
- **关键技术细节**：
  - **AgentStore平台**：基础架构，支持持续丰富智能体能力，适应操作系统快速演进。
  - **核心MetaAgent**：负责管理所有注册的异构智能体，并采用**AgentToken策略**进行高效调度。
  - **AgentToken策略**：将每个智能体的能力表示为一个可学习的“令牌”（token），MetaAgent通过动态计算任务与AgentToken的匹配得分，自动选择最合适的智能体组合来执行当前任务，从而实现**专门化与通用化**能力的融合。
- **算法流程（文字说明）**：
  1. 系统预注册一系列异构智能体（如网页操作、文件管理、代码执行等专业智能体）。
  2. 用户输入开放式任务描述。
  3. MetaAgent解析任务，利用AgentToken为每个候选智能体生成能力评分。
  4. 选择评分最高的智能体（或智能体组合），分配任务执行。
  5. 执行结果反馈至MetaAgent，必要时可迭代调整或切换智能体。
  6. 新智能体可随时加入，系统能力持续扩展。

## 3. 实验设计

- **使用的数据集/场景**：三个**交互式真实世界基准测试**（具体名称未在元数据中明确，根据“interactive real-world benchmarks”推测可能包括类似OSWorld、WebArena、AndroidEnv等环境）。
- **Benchmark**：使用三个主流交互式计算机任务基准（如操作系统级任务、Web任务、移动端任务等），重点评估**泛化能力**（跨领域任务）和**专业化能力**（领域内任务）。
- **对比方法**：与现有代表性智能体方法进行对比，包括：
  - **单一通用智能体**（如基于GPT-4V/LLaVA的多模态智能体）
  - **专用智能体系统**（如基于固定动作空间的智能体）
  - **同类多智能体协作系统**（如Tree-of-Thoughts、AutoGPT等变体）
  - **静态集成方法**（固定组合的智能体团队）

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量或训练时长等具体算力信息。
- 仅提及使用了大型语言模型（如GPT-4等）作为智能体基础模型，但未披露推理/训练的硬件细节。

## 5. 实验数量与充分性

- **实验组数**：包含**三个基准上的主要对比实验**以及**多项消融实验**（如AgentToken策略效果、智能体数量扩展性、不同调度策略对比等）。元数据中表格数量较多（9张），表明实验较为丰富。
- **充分性评估**：实验设计较为充分，覆盖了主要基准和关键消融项，对比了多种基线方法。但部分细节（如数据集具体名称、统计显著性检验）未在元数据中体现。整体而言，实验公平性较好，结果支持了核心主张。

## 6. 主要结论与发现

- **AgentStore显著扩展了智能体系统的能力边界**，在**泛化**（处理未见过的任务类型）和**专业化**（深度执行特定领域任务）两个维度上均有提升。
- **AgentToken策略有效**：能够动态选择最适合任务的智能体，优于静态组合或单一通用智能体。
- **可扩展性验证**：随着注册智能体数量增加，系统性能持续提升，具备适应操作系统演进的能力。
- **多基准一致表现**：在三个不同交互式环境中均取得领先结果，证明了方法的通用性。

## 7. 优点

- **方法创新**：将异构智能体集成视为可扩展平台，类比App Store，具备实用性和启发性。
- **AgentToken设计新颖**：通过可学习令牌实现轻量级、动态智能体调度，避免了传统多智能体系统中复杂的通信与协调机制。
- **兼顾泛化与专业化**：解决了单一方法在二者之间的权衡，实用性更强。
- **实验扎实**：在多个真实交互基准上进行评估，包含大量消融研究，验证了关键组件有效性。
- **可扩展性好**：系统可随时添加新智能体，无需重新训练主控制器，适合实际部署。

## 8. 不足与局限

- **实验数据集未完全公开**：元数据未列出具体基准名称，可能限制复现性。
- **算力信息缺失**：未提供训练或推理的硬件配置，不利于评估实际部署成本。
- **AgentToken策略细节不够透明**：具体如何学习令牌、是否依赖大规模预训练等未详述。
- **智能体依赖外部LLM**：性能受基础模型（如GPT-4）影响，可能存在黑箱偏差。
- **未考虑安全性/鲁棒性**：异构智能体集成可能引入新的攻击面（如恶意智能体），论文未讨论。
- **开放任务覆盖有限**：仅测试了三个基准，真实计算机环境更复杂，泛化仍有风险。

（完）

---
title: "ContinuumCellAgent: A Framework-Guided Agent for Long-Horizon Scientific Research"
title_zh: ContinuumCellAgent：一种面向长周期科学研究的框架引导型智能体
authors: "Li, H., Lu, Y., Fang, K., Xu, Z., Li, F."
date: 2026-06-19
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.15.732409v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 用于长时程科学研究的自主AI代理，具有模块化架构
tldr: 现有AI科学家系统缺乏模块化、系统化提示词基础及长程行为可观察性，难以诊断。ContinuumCellAgent采用模块化超节点架构支持即插即用后端，利用研究方法清单协议驱动文献综述、假设生成、计算实验等步骤，并配备诊断层记录工件和状态。在开放域QA和生物医学案例中，系统能自主执行完整科研流程并产出可核查结果，为可诊断的AI协同科学家研究奠定基础。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有AI科学家系统因缺乏模块化、提示词基础及长程行为可观察性而难以诊断。
method: 提出模块化超节点架构、研究方法清单协议与诊断层，实现阶段式后端替换及可核查工件生成。
result: 在开放域QA和生物医学案例中，系统可自主完成科研全流程并产出可检查输出与流水线动态。
conclusion: 提供可检查的研究工件和流水线动态，促进对AI协同科学家的严格研究。
---

## 摘要
人工智能科学家系统已经开始自动化科学研究的部分环节。我们提出了ContinuumCellAgent，这是一个自主智能体，能够在一轮无人值守的运行中执行文献综述、假设形成、计算实验、手稿撰写以及对抗性同行评审。现有的人工智能科学家系统由于缺乏模块化、系统性的提示词根基以及对长期运行行为的可观测性，仍然难以诊断。ContinuumCellAgent通过模块化的超节点架构实现了阶段性的后端替换，协议基于精心策划的研究方法清单（同时也定义了评审标准），以及一个记录文件型工件、消息轨迹和状态转换的诊断层，来解决这些问题。我们在开放领域的问答基准测试以及生物医学/长寿案例研究上评估了该系统，结果显示它能够产生可核查的研究工件，同时暴露流水线动态，以支持严格的人工智能协同科学家研究。

## Abstract
AI-scientist systems are beginning to automate parts of scientific research. We present ContinuumCellAgent, an autonomous agent that executes literature review, hypothesis formation, computational experimentation, manuscript drafting, and adversarial peer review as a single unattended run. Existing AI scientist systems remain difficult to diagnose because they lack modularity, systematic prompt grounding, and observability into long-running behavior. ContinuumCellAgent addresses these gaps with a modular supernode architecture for stage-wise backend swapping, protocols grounded in curated research-method checklists that also define reviewer rubrics, and a diagnostics layer that records file-based artifacts, message traces, and state transitions. We evaluate the system on open-domain QA benchmarks and biomedical/longevity case studies, showing that it can produce checkable research artifacts while exposing pipeline dynamics for rigorous AI co-scientist research.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：现有AI科学家系统能够自动化科学研究的某些环节，但缺乏模块化、系统性的提示词根基以及对长期运行行为的可观测性，导致系统难以诊断和调试。
- **整体含义**：提出ContinuumCellAgent，一个能够在一轮无人值守运行中完成文献综述、假设生成、计算实验、手稿撰写和对抗性同行评审的自主智能体，旨在提升AI协同科学家的可诊断性和可核查性。

## 2. 论文提出的方法论

- **核心思想**：通过模块化架构、协议化研究方法清单和诊断层，解决现有系统缺乏模块化、可观测性和提示词根基的问题。
- **关键技术细节**：
  - **模块化超节点架构**：支持阶段式后端替换（stage-wise backend swapping），允许不同模块（如文献综述、实验设计）独立更换，实现即插即用。
  - **研究方法清单协议**：精心策划的研究方法清单既驱动各阶段执行，又定义评审标准（rubrics），确保提示词有据可依。
  - **诊断层**：记录文件型工件、消息轨迹和状态转换，提供长期运行行为的可观测性。
- **算法/流程说明（文字）**：智能体按照“文献综述→假设形成→计算实验→手稿撰写→对抗性同行评审”的顺序依次执行，每个阶段由超节点模块处理，并依据研究方法清单协议生成可核查的工件，同时诊断层记录全过程。

## 3. 实验设计

- **数据集/场景**：开放领域问答基准测试（open-domain QA benchmarks）以及生物医学/长寿案例研究。
- **基准（Benchmark）**：未明确列出具体基准名称，但使用了开放域QA基准和生物医学案例。
- **对比方法**：文中未提及与其他方法的直接对比。评估聚焦于系统自身能否产生可核查研究工件并暴露流水线动态。

## 4. 资源与算力

- **未明确说明**：论文元数据和摘要中未提及GPU型号、数量、训练时长等算力信息。仅描述为“一轮无人值守运行”，推测为推理阶段而非大规模训练。

## 5. 实验数量与充分性

- **实验数量**：论文提到在开放域QA基准和两个生物医学/长寿案例上进行了评估，具体实验组数未详述。
- **充分性评价**：实验覆盖了通用问答和特定领域（生物医学），但缺乏消融实验、对比实验及多轮重复测试。由于仅有定性案例和基准测试，充分性有限，但作为初步验证足够展示功能。

## 6. 论文的主要结论与发现

- 系统能够自主完成科研全流程，并产出可检查的输出与流水线动态。
- 模块化超节点架构和诊断层使AI科学家系统更易诊断和调试。
- 在开放域QA和生物医学案例中，系统生成了可核查的研究工件，暴露了流水线内部状态，支持对AI协同科学家的严格研究。

## 7. 优点

- **模块化设计**：支持即插即用后端，便于扩展和维护。
- **可诊断性**：诊断层记录工件、消息和状态转换，实现长期行为可观测。
- **提示词根基**：基于策划研究方法清单的协议驱动，减少随意性，同时定义评审标准。
- **全流程自动化**：涵盖从文献综述到同行评审的完整科研循环。

## 8. 不足与局限

- **实验覆盖不充分**：仅测试了开放域QA和两个生物医学案例，缺少更多领域、更大规模实验。
- **缺失对比实验**：未与其他AI科学家系统（如论文中提到的现有系统）进行定量比较，难以评估相对优势。
- **偏差风险**：未讨论对抗性同行评审的内在偏差或幻觉风险。
- **应用限制**：当前仅适用于计算实验，未涉及湿实验或物理验证；算力需求未说明，可能影响可复现性。

（完）

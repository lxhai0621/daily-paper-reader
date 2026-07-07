---
title: "Turning Conversations into Workflows: A Framework to Extract and Evaluate Dialog Workflows for Service AI Agents"
title_zh: 将对话转化为工作流：面向服务AI代理的对话工作流提取与评估框架
authors: "Prafulla Kumar Choubey, Xiangyu Peng, Shilpa Bhagavath, Caiming Xiong, Shiva Kumar Pentyala, Chien-Sheng Wu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.203.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 基于问答链式推理提示的工作流提取方法
tldr: 该论文提出从历史对话中自动提取服务AI代理工作流的框架。方法包括两步：首先检索相关对话，然后使用基于问答的链式推理（QA-CoT）提示生成结构化工作流。引入自动化模拟评估方法验证工作流质量。该工作直接优化了智能体工作流的提示设计，提升了自主代理的对话响应一致性。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1612, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1648, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1653, \"height\": 670, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1641, \"height\": 1132, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 789, \"height\": 654, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1631, \"height\": 1170, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1652, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1640, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1629, \"height\": 865, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1654, \"height\": 399, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1632, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1626, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1624, \"height\": 771, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1635, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1623, \"height\": 290, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.203/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1625, \"height\": 528, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 744, \"height\": 104, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1665, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1618, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 640, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1659, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1283, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1178, \"height\": 1603, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 821, \"height\": 136, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.203/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 579, \"height\": 248, \"label\": \"Table\"}]"
motivation: 服务AI代理需要结构化工作流来保证响应一致性，但工作流通常未文档化，自动提取方法尚属空白。
method: 采用检索阶段选择相关对话，再通过QA-CoT提示生成结构化工作流，并设计自动化模拟评估。
result: 实验表明该方法能有效从对话中提取高质量工作流，提升代理响应准确性和任务完成率。
conclusion: 该框架为智能体工作流的自动化构建提供了可行方案，可迁移至多种服务代理场景。
---

## Abstract
Automated service agents require well-structured workflows to deliver consistent and accurate responses to customer queries. However, such workflows are often undocumented, and their automatic extraction from conversations remains largely unexplored. In this work, we present a novel framework for extracting and evaluating dialog workflows from historical interactions. Our extraction process involves two key stages: (1) a retrieval step to select relevant conversations based on key procedural elements, and (2) a structured workflow generation step using question-answer-based chain-of-thought (QA-CoT) prompting. To comprehensively evaluate the quality of the extracted workflows, we introduce an automated simulation framework with agent and customer bots that measures their effectiveness in resolving customer issues. Extensive experiments on the ABCD and SynthABCD datasets show that our QA-CoT technique improves workflow extraction by 12.16% in average macro accuracy over the baseline. Moreover, our evaluation method closely aligns with human assessments, offering a reliable and scalable framework for future research.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：服务AI代理依赖结构化工作流（dialog workflows）来保证对客户查询的一致、准确响应。然而，这些工作流通常未被文档化，且从历史对话中自动提取工作流的方法几乎未被探索。现有工作流创建主要依赖人工，耗时、易过时、难以覆盖真实交互的复杂性。
- **研究动机**：过去客户-代理对话中隐含了大量程序性知识，自动提取并结构化这些知识，可以为人类代理和AI系统提供可复用的指南。
- **整体含义**：该工作填补了从对话自动提取工作流的空白，提出了一个端到端的框架，包括检索、生成和评估，显著提升了工作流提取的准确性和可靠性。

### 2. 论文提出的方法论：核心思想与关键技术细节

#### 核心思想
提出两阶段流水线：**检索阶段** + **生成阶段**；并配套一个自动化的**端到端模拟评估框架**。

#### 关键技术细节

- **检索阶段（Procedural Element-based Retrieval, Proc-Sim）**
  1. 从每条对话中提取关键程序化元素（意图、槽值、解决步骤），使用GPT-4o-mini。
  2. 将这些元素用OpenAI text-embedding-3-small嵌入，计算每个意图的质心。
  3. 选取与质心余弦相似度最高的top-K条对话，确保所选对话代表最常见的解决步骤，同时过滤噪声。

- **生成阶段（QA-CoT prompting）**
  - 模拟一个**Guide**（提问者）和**Implementer**（回答者）之间的问答过程（单次生成整个问答链）。
  - Guide聚焦先决条件、决策点、步骤逻辑；Implementer基于历史对话提供详细回答。
  - 将问答链与检索到的对话一起输入LLM，生成最终结构化工作流（步骤列表，含条件分支）。

- **评估框架（E2E Evaluation）**
  1. **分解工作流**为所有可能的子流（路径）。
  2. 为每个子流生成用户/系统信息及成功标准。
  3. 使用**客户机器人**和**代理机器人**模拟对话，代理机器人遵循预测的工作流。
  4. 对话结束后，判断是否达成成功标准。

### 3. 实验设计

#### 数据集
- **ABCD**：人类标注的对话数据集，包含噪声（代理可能跳过或打乱步骤）。
- **SynthABCD**：利用相同工作流由LLM生成的干净对话数据集，去除人为错误，用于理想化评估。

#### 基准与对比方法
- **检索策略对比**：Random（随机选择）、Conv-Sim（全对话嵌入相似度）、Proc-Div（程序化元素多样性选择）、Proc-Sim（本文方法）。
- **工作流生成方法对比**：
  - Basic：直接提示。
  - Reflection：初始生成后反思补全。
  - Plan：先规划再生成。
  - Ensemble：生成多个工作流后一致性合并。
  - QA-CoT（本文方法）。
  - QA-CoT+Reflect：在QA链上再反思。

#### 使用的LLM
- 闭源：GPT-4o, Gemini-1.5-Pro, Opus-3, Sonnet-3.5
- 推理LLM：OpenAI o1, o1-mini, o3-mini, DeepSeek-R1
- 开放LLM：Llama-3.1-405B-Instruct, Qwen2.5-72B-Instruct, Qwen2.5-7B-Instruct

#### 评估指标
- Macro Accuracy（每个意图正确子流百分比的平均值）
- Micro Accuracy（所有意图总体正确子流百分比）
- #utt（平均对话话语数）

### 4. 资源与算力

- 论文**未明确说明**使用的GPU型号、数量或训练时长。仅提及使用了多个LLM（GPT-4o, Gemini, Opus, Sonnet等）进行推断，以及GPT-4o-mini用于提取程序化元素。所有实验均为推断（inference），未涉及模型训练。因此无法提供具体算力信息。

### 5. 实验数量与充分性

- **实验数量**：包括大量实验：
  - 检索策略消融：4种检索方法 × 5种对话数量（25/50/75/100/all） × 4个LLM。
  - 生成方法对比：8种提示策略 × 2个数据集 × 8个闭源LLM（含推理LLM） + 3个开放LLM。
  - 消融研究：QA-CoT有无检索、多轮vs单轮问答。
  - 人工评估：验证E2E框架准确性（94.81%场景正确）和与人类评分的一致性（Kappa=0.92）。
- **充分性与公平性**：实验设计较全面，涵盖了不同噪声程度的数据集、多种LLM、多种检索和生成策略。对比基线包括反射、规划、集成等常见增强方法。消融实验有效隔离了各组件的贡献。人工评估验证了自动评估的可靠性。总体实验充分、客观。

### 6. 论文的主要结论与发现

1. **QA-CoT提示显著优于所有基线**：在ABCD上平均macro accuracy提升8.73%（最高GPT-4o提升11.81%），在SynthABCD上提升15.59%。
2. **检索策略至关重要**：Proc-Sim（基于程序化元素相似度）在大部分LLM上优于直接使用全对话嵌入（Conv-Sim）或随机选择。选择75条对话通常最佳。
3. **E2E评估与人类判断高度一致**：Kappa=0.922，自动选择场景准确率94.81%。
4. **推理LLM（如o3-mini）也能从QA-CoT获益**：单独使用推理模型不一定好于非推理模型，但加入QA-CoT后性能普遍提高。
5. **错误分析**：常见错误包括混淆系统可用信息与需从用户获取的信息、忽略替代选项、未正确跟随条件分支。

### 7. 优点

- **方法创新**：QA-CoT通过Guide/Implementer交互捕捉细粒度程序知识，突破了简单提示的局限；检索策略基于程序化元素而非表面对话，更具鲁棒性。
- **评估框架可靠**：端到端模拟评估避免了人工评估的一致性问题，且与人类判断高度吻合，可扩展。
- **实验设计全面**：覆盖噪声/干净数据、多种LLM、多种提示策略、消融验证，分析深入（含错误分析）。
- **开源实用**：提供了完整提示和框架细节，可复现。

### 8. 不足与局限

- **领域限制**：方法针对服务AI代理，对于更复杂领域（如医疗、法律）可能需要调整。
- **依赖意图标签**：检索阶段按意图分组，若意图标签不可用需额外分类步骤。
- **合成数据局限**：SynthABCD是理想化数据，不能完全代表真实世界噪声，尽管论文同时使用了ABCD。
- **评估局限**：E2E评估假设工作流路径可以完全枚举，对于极复杂工作流可能不适用；且仅评估任务是否成功，未充分量化效率（尽管给出了话语数）。
- **人工验证规模**：人工评估仅涉及18个意图、231个场景、105次模拟对话，规模有限。
- **资源消耗**：使用多个大型LLM进行推断，成本高，但论文未详细讨论计算开销。

（完）

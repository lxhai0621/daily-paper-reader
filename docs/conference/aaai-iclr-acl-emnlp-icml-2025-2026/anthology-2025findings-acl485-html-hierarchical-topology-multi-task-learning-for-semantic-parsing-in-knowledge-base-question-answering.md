---
title: "HTML: Hierarchical Topology Multi-task Learning for Semantic Parsing in Knowledge Base Question Answering"
title_zh: HTML：面向知识库问答语义解析的层次拓扑多任务学习
authors: "Aziguli Wulamu, Lyu Zhengyu, Kaiyuan Gong, Yu Han, Zewen Wang, Zhihong Zhu, Bowen Xing"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.485.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 知识库问答的语义解析
tldr: 该论文针对知识库问答中从自然语言问题生成精确逻辑形式的挑战，提出了层次拓扑多任务学习框架HTML。该框架将主任务（逻辑形式生成）与实体预测、关系预测和基础逻辑形式生成三个辅助任务结合，通过层次结构共享表示。实验表明HTML在多个KBQA基准上优于现有方法，尤其增强了模型对复杂问题的处理能力。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.485/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.485/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1622, \"height\": 967, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.485/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1638, \"height\": 1008, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.485/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1620, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.485/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 649, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.485/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1643, \"height\": 859, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 608, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1460, \"height\": 772, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 783, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 685, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 810, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 702, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1393, \"height\": 889, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1392, \"height\": 832, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.485/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1416, \"height\": 496, \"label\": \"Table\"}]"
motivation: KBQA中从问题到逻辑形式的映射复杂，尤其涉及多样实体和关系时。
method: 提出层次多任务学习框架，联合主任务和三个辅助任务进行共享表示学习。
result: 在多个KBQA基准上取得最优性能，复杂问题处理能力显著提升。
conclusion: 层次多任务学习是增强KBQA语义解析的有效范式。
---

## Abstract
Knowledge base question answering (KBQA) aims to answer natural language questions by reasoning over structured knowledge bases. Existing approaches often struggle with the complexity of mapping questions to precise logical forms, particularly when dealing with diverse entities and relations. In this paper, we propose Hierarchical Topology Multi-task Learning (HTML), a novel framework that leverages a hierarchical multi-task learning paradigm to enhance the performance of logical form generation. Our framework consists of a main task: generating logical forms from questions, and three auxiliary tasks: entity prediction from the input question, relation prediction for the given entities, and logical form generation based on the given entities and relations. Through joint instruction-tuning, HTML allows mutual guidance and knowledge transfer among the hierarchical tasks, capturing the subtle dependencies between entities, relations, and logical forms. Extensive experiments on public benchmarks show that HTML markedly outperforms both supervised fine-tuning methods and training-free ones based on powerful large language models (e.g., GPT-4), demonstrating its superiority in question understanding and structural knowledge reasoning.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：知识库问答（KBQA）旨在利用结构化知识库回答自然语言问题。核心挑战在于将问题精确映射为逻辑形式（如S-expression、SPARQL），尤其当涉及多样实体和关系、需要多跳推理时。
- **现有问题**：当前方法存在三大缺陷：  
  - **元知识缺失**：不提取候选实体和关系，直接生成逻辑形式易出错。  
  - **错误传播**：先提取参考知识再生成逻辑形式，但提取结果中的噪声会误导后续步骤。  
  - **对齐不足与高成本**：训练无关方法（如基于GPT-4的In-Context Learning）无法充分对齐问题与结构化知识，且需大量API调用，成本高。
- **研究动机**：通过任务分解与层次多任务学习，让模型协同学习实体识别、关系抽取和逻辑形式骨架生成，从而提升语义解析的准确性和鲁棒性。

### 2. 方法论：核心思想与关键技术

- **核心思想**：将主任务（语义解析，SP）分解为三个层次辅助子任务，并通过统一指令微调（Instruction Tuning）实现知识迁移与相互指导。
- **层次任务拓扑**（Fig. 1）：
  1. **EntRA**（实体识别与对齐）：从问题中提取实体并在知识库中映射。
  2. **EARE**（实体感知关系抽取）：在给定实体下，预测它们之间的关系。
  3. **SkelGen**（逻辑形式骨架生成）：基于实体和关系生成完整的逻辑形式。
- **指令设计**：为每个任务设计特定指令模板（详见论文§2.2），例如：
  - SP指令：直接要求将问题转换为逻辑形式。
  - EntRA指令：要求输出对齐到知识库的实体名。
  - EARE指令：要求输出实体间关系。
  - SkelGen指令：要求基于实体和关系生成逻辑形式。
- **训练流程**（Fig. 2）：
  - 构建所有指令数据，随机选取比例α（如50%~70%）的子任务指令，与全部主任务指令混合。
  - 使用LoRA高效微调LLaMA2-7B/13B。
  - 目标函数为负对数似然：\( \mathcal{L} = -\sum_{n=1}^{N} \log p(y_n | y_{<n}, I) \)。
- **推理阶段**：仅使用SP指令进行推理，无需额外子任务调用，因为子任务能力已融入主任务。

### 3. 实验设计

- **数据集**：  
  - **WebQuestionsSP (WebQSP)**：3098训练/1639测试样本。  
  - **ComplexWebQuestions 1.1 (CWQ)**：27639训练/3531测试/3519验证样本。  
- **基准方法**：对比两类共9种SOTA方法：  
  - 训练无关方法：ChatGPT+CoT、ToG（GPT-4）、GoG（GPT-4）、Interactive-KBQA等。  
  - 监督微调方法：KD-CoT、RoG、ChatKBQA、CoQ等。  
- **评估指标**：F1、Hits@1、Accuracy（Acc）。
- **对比设置**：  
  - 主要对比表1（使用检索实体）。  
  - 额外对比表2（使用黄金实体）。  
  - 消融实验：移除每个子任务（表3）。  
  - 指令混合比例α分析（Fig. 4）。  
  - 任务拓扑对比（表4）：Only E、Only R、E&R、CoT、Mix等6种设置。  
  - 子任务准确性评估（表5）：实体Acc、关系Acc、骨架Acc、逻辑形式精确匹配(LF-EM) Acc。  
  - 错误类型分布分析（Fig. 5）。  
  - 案例研究（Fig. 6）。

### 4. 资源与算力

- **硬件**：单块NVIDIA A40 GPU（48GB显存）。
- **微调方法**：LoRA（参数高效微调）。
- **超参数**：学习率5e-5，batch size 4，梯度累积步数4。
- **训练轮次**：WebQSP训练100 epochs，CWQ训练10 epochs（因CWQ数据量约为WebQSP的十倍）。
- **备注**：文中未明确说明训练总时长、GPU数量（仅一块）或具体波数，但指出这些参数与基线ChatKBQA保持一致以确保公平。

### 5. 实验数量与充分性

- **实验组数**：至少涵盖以下8组实验：  
  1. 主结果（表1）  
  2. 黄金实体结果（表2）  
  3. 子任务消融（表3）  
  4. 指令混合比例α探索（Fig. 4，含4子图×5比例）  
  5. 任务拓扑比较（表4，含4种方法×2模型×2数据集设置）  
  6. 子任务准确性（表5）  
  7. 错误类型分布（Fig. 5）  
  8. 案例研究（Fig. 6）  
  此外还有附录中不同实现策略探索（表7）等。
- **充分性与公平性**：  
  - 对多个数据集、多种基线和设置进行了全面对比。  
  - 消融实验各子任务移除后均有显著下降，验证了每个组件的必要性。  
  - 与ChatKBQA共享相同超参数和训练策略，确保公平。  
  - 但在不同α和任务拓扑上的调优可能存在过拟合风险（尤其在小数据集WebQSP上），且未报告多次运行的方差。

### 6. 主要结论与发现

- HTML在WebQSP和CWQ上均取得新SOTA：  
  - 使用LLaMA2-13B，在WebQSP上Acc达75.3%（+1.5% vs ChatKBQA），CWQ上Acc达75.1%（+1.8% vs ChatKBQA）。  
  - 相比最佳训练无关方法GoG，在CWQ Hits@1上提升7.7%。
- 子任务贡献：移除任何子任务都会导致性能下降，其中SkelGen影响最大。
- 错误分析：关系错误占比最高（WebQSP 49.8%，CWQ 45.7%），未来需重点改进关系抽取。
- 案例研究表明，HTML能避免关系错误和幻觉问题。

### 7. 优点

- **方法创新**：提出层次任务拓扑，将复杂语义解析分解为可学习的子任务，并通过多任务指令微调实现协同增强。
- **高效推理**：推理时只用一个指令，无额外成本，避免训练无关方法的高API开销。
- **实验全面**：覆盖两个标准数据集、多种基线、消融、比例调优、拓扑对比、错误分析、案例展示，论证充分。
- **可复现性**：使用开源模型LLaMA2和LoRA，超参数公开。

### 8. 不足与局限

- **执行阶段未关注**：论文仅聚焦语义解析（逻辑形式生成），未处理逻辑形式到SPARQL的执行错误（如格式错误、实体映射失败），作者也承认这是未来方向。
- **关系抽取仍是瓶颈**：错误分析显示关系错误占比最高，但HTML未专门优化该子任务（如引入关系类型的结构化约束）。
- **比例调优依赖数据**：最佳指令混合比例α在不同数据集和模型规模上变化（如WebQSP需70%~100%，CWQ需50%~70%），可能需要针对每个新场景重新调优。
- **计算资源有限**：仅用单块A40 GPU，未探索更大模型或更优训练策略（如全参数微调）的潜力。
- **重复性未报告方差**：未提供多次运行的标准差，结果可能有一定随机性。
- **应用限制**：仅验证于Freebase知识库，对其他KB（如Wikidata、DBpedia）的迁移性未测试。

（完）

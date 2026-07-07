---
title: Memory-augmented Query Reconstruction for LLM-based Knowledge Graph Reasoning
title_zh: "记忆增强的查询重建:面向LLM知识图谱推理"
authors: "Mufan Xu, Gewen Liang, Kehai Chen (陈科海), Wei Wang, Xun Zhou, Muyun Yang (杨沐昀), Tiejun Zhao (赵铁军), Min Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1234.pdf"
tags: ["query:agent"]
score: 8.0
evidence: 记忆增强的查询重建用于知识图谱推理
tldr: LLM在知识图谱问答中常混淆工具调用与知识推理，导致幻觉。MemQ构建查询语句的记忆模块，显式描述查询语义，使LLM通过自然语言推理和记忆增强查询重建，避免错误工具调用。实验表明该方法有效降低幻觉，提升KGQA的准确性和可解释性，为智能体记忆管理提供了范例。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1234/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1234/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1390, \"height\": 760, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1234/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1484, \"height\": 581, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1234/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1234/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 758, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1234/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1234/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1330, \"height\": 893, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1266, \"height\": 887, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1273, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 786, \"height\": 172, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 780, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 792, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 780, \"height\": 114, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 136, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1584, \"height\": 2341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1486, \"height\": 1528, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1577, \"height\": 1739, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1234/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1360, \"height\": 574, \"label\": \"Table\"}]"
motivation: LLM在KGQA中工具调用与推理混淆，引发幻觉。
method: 建立查询记忆模块，通过记忆增强重建查询语句。
result: 降低工具调用幻觉，提升KGQA准确性和可读性。
conclusion: 记忆模块分离推理与调用，增强智能体可靠性。
---

## Abstract
Large language models (LLMs) have achieved remarkable performance on knowledge graph question answering (KGQA) tasks by planning and interacting with knowledge graphs. However, existing methods often confuse tool utilization with knowledge reasoning, harming readability of model outputs and giving rise to hallucinatory tool invocations, which hinder the advancement of KGQA. To address this issue, we propose Memory-augmented Query Reconstruction for LLM-based Knowledge Graph Reasoning (MemQ) to decouple LLM from tool invocation tasks using LLM-built query memory. By establishing a memory module with explicit descriptions of query statements, the proposed MemQ facilitates the KGQA process with natural language reasoning and memory-augmented query reconstruction. Meanwhile, we design an effective and readable reasoning to enhance the LLM’s reasoning capability in KGQA. Experimental results that MemQ achieves state-of-the-art performance on widely used benchmarks WebQSP and CWQ.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在基于大型语言模型（LLM）的知识图谱问答（KGQA）任务中，现有方法往往将工具调用（如SPARQL查询的生成）与知识推理过程混为一谈。这种混淆导致两方面问题：①推理步骤可读性差（通常以抽象的SPARQL关系表示）；②易引发工具调用幻觉（hallucinatory tool invocations），即LLM生成不合理的查询语句或错误地调用工具，从而降低结果的可靠性和可分析性。
- **研究动机**：解决工具调用与推理过程耦合带来的可读性差和幻觉问题，使LLM能够专注于生成可读的自然语言推理步骤，再通过外部记忆模块辅助查询重建，最终与知识图谱交互。
- **整体含义**：提出一种“记忆增强的查询重建”框架（MemQ），将KGQA过程解耦为三个独立任务：记忆构建、知识推理、查询重建。通过建立显式存储查询语句及其自然语言描述的记忆模块，让LLM仅需进行自然语言推理，而无需直接生成工具调用，从而提升KGQA的准确性和可解释性。

## 2. 论文提出的方法论

- **核心思想**：利用LLM构建一个“查询记忆”模块，该模块将训练集中已有的SPARQL查询语句分解为可描述的片段（statement），并为每个片段生成自然语言描述。在推理阶段，LLM先生成自然语言推理步骤（以“查找”、“确保”、“排序”等形式），然后通过语义相似度从记忆中检索对应的查询语句片段，最后通过规则拼接重建完整的SPARQL查询，执行并获取答案。

- **关键技术细节**：
  - **记忆构建**：采用基于规则的分解策略，利用Freebase中的CVT节点（复合值类型）特性，将SPARQL查询分为三类结构，并使用通用LLM（如GLM-4）为每个片段生成自然语言描述，存储为 `<描述, 查询语句>` 对。
  - **知识推理**：对LLM进行微调（以Llama2-7b为基模型），使其生成格式化的推理计划 `P = {p_i}`，每个步骤 `p_i` 以自然语言描述，如“Find the spouse of richard nixon, assign it to ?x”。推理步骤限制为每次只搜索或检查一个实体。
  - **查询重建**：基于语义相似性（Sentence-BERT编码）自适应召回记忆，采用双阈值策略：若top-1相似度≥γ1则召回1条；否则召回所有不低于γ2的片段。然后通过规则将召回语句按推理顺序拼接，并用推理步骤中的实体ID填充变量，生成最终SPARQL查询。

- **公式/算法流程（文字说明）**：
  1. 记忆构建阶段：对训练集中每个SPARQL，分解为类型1/2/3的语句片段；用LLM生成每个片段的自然语言描述；存储为 `M(n_i) → s_i`。
  2. 知识推理阶段：微调LLM，输入问题Q和主题实体E，输出n步推理计划P。
  3. 查询重建阶段：对每个推理步骤p_i，从记忆中检索最匹配的语句s_i；将检索到的所有语句按步骤顺序拼接；用实体ID替换占位符；执行最终查询得到答案。

## 3. 实验设计

- **数据集与场景**：使用两个广泛使用的KGQA基准：
  - **WebQSP**：基于Freebase的问答数据集。
  - **CWQ**（Complex WebQuestions）：更复杂的多跳问答数据集。

- **Benchmark**：以Hits@1和F1（Macro-F1）作为主要评估指标，遵循前人工作惯例。

- **对比方法**：
  - 零样本基线：Llama2-7b、Llama3-8b、Qwen2.5-7b。
  - 经典非LLM方法：KV-Mem、GraftNet、QGG、NSM等。
  - 基于LLM的规划/交互方法：RoG、ToG、KG-Agent、KD-CoT、ChatKBQA等。
  - 自建消融基线：无查询记忆直接微调（-w/o QRM）、无规划专家和记忆直接微调（-w/o PE, QRM）。

- **实验设置**：基模型为Llama2-7b（主要对比）；也使用Llama3-8b、Vicuna-7b、Qwen2.5-7b进行通用性分析。微调数据来自训练集的记忆描述。

## 4. 资源与算力

- 文中仅在附录F的“时间效率”实验中明确说明硬件配置：**单张 NVIDIA H20 96GB GPU，Intel(R) Xeon(R) Platinum 8468V CPU**，用于测量推理和查询重建的平均时间成本（见表8）。该实验表明MemQ的额外时间开销较低。
- **未明确说明**：完整实验（如LLM微调、大规模推理测试）所使用的GPU数量、训练时长、显存消耗等具体算力信息。论文在Acknowledgement中提到受国家自然科学基金等项目支持，但未提供详细的算力资源描述。

## 5. 实验数量与充分性

- **实验数量**：论文进行了大量实验，包括：
  - 主实验结果（表1）：在WebQSP和CWQ上与多个基线对比。
  - 推理能力增强分析（表2）：比较重建子图与黄金子图的边命中率（EHR）和图编辑距离（GoldGED）。
  - 消融实验（表3）：验证记忆模块和规划专家的有效性。
  - 幻觉缓解人工评估（表4）：对推理计划的正确性、完整性、冗余性进行人工检查（随机采样100例）。
  - 鲁棒性实验（图4）：在扰动数据（删除/替换语句）下测试Hits@1变化。
  - 错误分析（图5）：分类主路径错误和过滤错误。
  - 数据效率分析（图6）：使用不同比例训练数据（10%~100%）微调后的性能。
  - 模型通用性测试（表5）：在四个不同LLM上的表现。
  - 案例分析（图7及附录中表13、表14）：展示实际推理和重建结果。
  - OOD性能测试（附录表7）：测试训练集中未出现过的查询语句。
  - 时间效率（附录表8）：不同跳数下的推理和重建时间。

- **充分性与公平性**：
  - 实验设计较为全面，覆盖了性能、鲁棒性、可解释性、数据效率、模型泛化等多个维度。
  - 对比基线包括多种主流方法，且复现了部分基线结果（标注*）。
  - 消融实验直接针对核心贡献（记忆模块、解耦策略）进行验证。
  - 人工评估随机采样100例，评估标准明确（正确性、完整性、冗余性），但样本量相对较小，可能存在标注偏差。
  - 总体而言，实验比较充分，结论有较强的实证支持，但在大规模多数据集或跨知识图谱的验证上尚有不足。

## 6. 论文的主要结论与发现

- MemQ在WebQSP和CWQ上均达到**SOTA性能**（WebQSP: Hits@1=0.841, F1=0.858；CWQ: Hits@1=0.803, F1=0.830），显著优于所有基线。
- 推理能力增强分析表明，MemQ重建的子图在边命中率和图编辑距离上远优于RoG，尤其在多跳场景下保持高准确性。
- 消融实验证实，记忆模块和规划专家对性能提升至关重要，直接微调将推理和工具调用混合会导致性能下降。
- 人工评估显示，MemQ显著减少了正确性和完整性错误（幻觉减少），但冗余性错误略有增加（由于语义相似边的召回）。
- 鲁棒性实验表明，即使训练数据中有20%的扰动，MemQ仍保持较高性能。
- 数据效率实验显示，仅用10%训练数据即可达到约0.7的F1，表明方法对有限数据利用高效。
- 模型通用性测试表明，MemQ可适配不同LLM（Llama2、Llama3、Vicuna、Qwen）并保持优势。
- OOD测试表明，对未见过的查询语句，MemQ利用自适应召回仍能取得相对较好的结果（Hit=0.587），优于RoG和ChatKBQA。

## 7. 优点

- **创新性**：首次提出将工具调用与知识推理显式解耦，通过构建查询记忆模块实现，思路新颖，有效缓解工具调用幻觉。
- **可解释性**：推理步骤以自然语言呈现，便于人类理解和检查，相比SPARQL路径更直观。
- **有效性**：在多个基准上达到SOTA，且消融和鲁棒性实验充分验证了各模块贡献。
- **通用性**：框架可基于不同LLM实现，不依赖于特定基模型；记忆模块具有便携性，可与其他工具/推理策略结合。
- **数据效率**：仅需少量训练数据即可获得不错性能，降低了标注成本。
- **鲁棒性**：对数据噪声和OOD情况有一定容忍度，实际部署更可靠。

## 8. 不足与局限

- **对标注查询的依赖**：记忆构建基于训练集已有的黄金SPARQL查询，假设具有真值查询。论文在Limitation中指出未来可通过建模整个Freebase来摆脱这种依赖，但当前版本仍需要标注数据。
- **CVT节点处理依赖规则**：分解策略依赖手工规则处理CVT节点，可能无法覆盖所有复杂查询结构，灵活性有限。
- **冗余检索问题**：自适应召回策略可能引入语义相似但无关的边，导致重建查询包含冗余条件（如附录案例所示）。虽然作者认为这在Freebase中合理，但可能降低精确性。
- **未验证即插即用能力**：论文声称具有良好插拔能力，但未进行与其他工具（如不同KG接口）或跨任务迁移的正式实验。
- **有限的人工评估规模**：幻觉评估仅随机采样100例，样本量偏小，且评估可能受主观影响。缺乏更大规模或第三方评估。
- **资源信息不完整**：未提供完整微调和推理所需的算力细节（如GPU数量、训练时长），影响可复现性评估。
- **领域局限性**：仅在Freebase的WebQSP和CWQ上验证，未在更现代或开放域的知识图谱（如Wikidata）上测试，泛化性有待进一步证实。

（完）

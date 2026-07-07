---
title: Discovering Latent Facts from Context to Construct Richer Open Knowledge Graphs
title_zh: 从上下文中发现潜在事实以构建更丰富的开放知识图谱
authors: "Jinpeng Li, Hang Yu, Ziqi Ma, Peng Qi"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38998/42960"
tags: ["query:ma-kf"]
score: 8.0
evidence: 提出KG-DLF方法，从上下文中发现潜在事实以构建开放知识图谱
tldr: 现有知识图谱构建方法受限于大模型输入长度，只能提取单文本内知识，无法跨文本发现潜在知识。本文提出KG-DLF方法，通过发现与上下文逻辑一致的新事实来增强开放知识图谱构建。该方法利用LLM的生成能力，但突破了单文本局限，能更丰富地组织知识。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有知识图谱构建受限于输入长度，无法发现跨文本的潜在知识。
method: 提出KG-DLF方法，利用上下文逻辑发现新事实以增强开放知识图谱构建。
result: 能够发现跨文本的潜在事实，生成更丰富的知识图谱。
conclusion: 通过上下文中潜在事实的发现，可显著提升开放知识图谱的覆盖率和质量。
---

## Abstract
Knowledge graph construction (KGC) aims to extract valuable information from text and organize it into structured knowledge graphs (KGs). Recent methods have leveraged the strong generative capabilities of large language models (LLMs) to improve the generalization and reduce the labor costs. However, constrained by the input length of LLMs, existing methods mainly focus on extracting knowledge within individual texts and lack the capability to discover latent knowledge across texts. To fill this gap, we propose a novel method for open knowledge graph construction, termed KG-DLF. The core idea of this method is to enhance the knowledge graph construction process by discovering new facts that are consistent with the underlying contextual logic. Specifically, we first design a knowledge extractor to extract knowledge from the text. Then, a knowledge normalizer performs schema alignment on the extracted knowledge. Next, we explore a knowledge discoverer based on a clue search strategy, which leverages the logical consistency of context to mine latent facts. Finally, we design a counterfactual-based knowledge corrector, enabling the model to purify knowledge and reduce factual errors. Experimental results show that KG-DLF is capable of extracting comprehensive knowledge in open-world scenarios across three KGC benchmarks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义
- **研究动机**：现有基于大语言模型（LLM）的知识图谱构建（KGC）方法受限于LLM的输入长度，通常采用文本分段策略，只关注单文本内知识提取，忽略了跨文本间的语义关联，导致构建的知识图谱碎片化、缺乏连贯性。
- **研究问题**：如何突破输入长度限制，发现跨文本的潜在事实（latent facts），从而生成更丰富、更连贯的开放知识图谱。
- **整体含义**：提出KG-DLF方法，通过增强知识图谱构建过程中的上下文逻辑一致性发现新事实，以提升知识图谱的完整性和质量。这是首次尝试通过发现潜在知识来增强KGC的工作。

## 2. 方法论
- **核心思想**：利用LLM的生成能力，结合语义线索检索和反事实比较，从上下文中挖掘跨文本的潜在事实，并自动纠正错误知识。
- **关键技术细节**：
  - **知识提取器（Knowledge Extractor）**：通过上下文学习（ICL）示例提示LLM从文本中提取三元组形式的事实，并自动为每个元素生成schema描述。
  - **知识规范化器（Knowledge Normalizer）**：使用BERT-based嵌入模型计算新提取schema与预定义schema集合的余弦相似度，设定阈值λ进行对齐，并通过对比学习优化嵌入模型。
  - **知识发现器（Knowledge Discoverer）**：首先让LLM判断实体对是否在现实世界中相关；对于相关实体对，采用线索检索策略：计算主体实体在客体实体2跳邻域内各节点的相关性得分（LLM评分），选择Top-k路径作为上下文线索，引导LLM生成与现有图逻辑一致的潜在关系。
  - **知识纠正器（Knowledge Corrector）**：基于反事实思维，为每个事实生成一组反事实（替换关系），让LLM基于上下文选择最合理的事实，从而纠正错误或噪声知识。
- **公式与算法流程**（文字说明）：
  - Schema对齐：\( s^* = \arg\max_{s_i \in S} \text{sim}(\hat{s}, s_i) \)，若 \(\text{sim} > \lambda\) 则对齐。
  - 线索路径置信度：\( \text{conf}_X(p_i) = \frac{1}{l} \sum_{j=1}^l \psi(X, e_j) \)，其中 \(\psi\) 为LLM相关性评分函数，选择Top-k路径作为线索。
  - 反事实纠正：原事实 \( f_i = (s, r, o) \) 与反事实集 \(\hat{F}\) 比较，若原事实合理性最高则保留，否则替换。

## 3. 实验设计
- **数据集**：
  - **WebNLG***：单文本场景，1165条文本-事实对，4001个事实，345个实体，159个关系。
  - **REBEL***：长距离依赖复杂关系，从105516条测试数据中随机采样1000条长文本-事实对，4000个事实，3643个实体，196个关系。
  - **Wiki-NRE***：跨文本场景，包含长尾关系，从29619条测试数据中随机采样1000条跨文本实例（超过两段文本），2335个实体，45个关系。
- **基准（Benchmark）**：采用WebNLG官方评估脚本，计算F1、精确匹配（Exact）、部分匹配（Partial）、严格匹配（Strict）分数。
- **对比方法**：
  - **通用大模型（GLMs）**：Mistral-7B-Instruct、LLaMA3-8B-Instruct、ChatGPT-3.5、ChatGPT-4.0。
  - **生成式构建方法（GCMs）**：REGEN、GenIE、SAC-KG、EDC+R、AutoSchemaKG。

## 4. 资源与算力
- **文中明确说明**：实验使用PyTorch和HuggingFace框架，基于22核CPU（AMD EPYC 7T83）和两块RTX-4090 GPU（每块24GB显存）。所有实验结果取三次运行平均值。未提训练时长或总计算量，但提出KG-DLF无需微调LLM，仅需提示调用，因此计算开销主要来自多次LLM推理。

## 5. 实验数量与充分性
- **实验组数**：
  - 主实验：在三个数据集上对比KG-DLF与所有基线（表1），共12行模型×3数据集。
  - 消融实验：6种组件组合（表2），分别评估知识提取器（KE）、知识规范化器（KN）、知识发现器（KD）、知识纠正器（KC）的贡献。
  - 超参数分析：ICL示例数量h（图3a）、线索数k（图3b）、实体阈值λE和关系阈值λR在REBEL*和Wiki-NRE*上的联合影响（图3c-d）。
  - 案例研究：两个真实世界案例（图4）展示知识发现与纠正效果。
- **充分性与公平性**：实验覆盖不同场景（单文本、长距依赖、跨文本），消融设计合理，基线涵盖多种主流方法。超参数调优过程详细，且在不同数据集上统一最佳设置（h=5, k=3, λE=0.80, λR=0.75）。未报告统计显著性检验，但三次平均结果降低了随机性。总体实验较充分、客观。

## 6. 主要结论与发现
- KG-DLF在三数据集上均达到最优F1，分别超过最佳基线1.9%（WebNLG*）、4.6%（REBEL*）、8.6%（Wiki-NRE*），尤其在跨文本场景提升最大。
- 消融实验表明各组件均有贡献：知识规范化器提升一致性，知识发现器恢复遗漏关系，知识纠正器减少错误。
- 超参数分析显示：ICL示例5个足够；线索数k=3平衡性能与存储；最优阈值λE=0.80，λR=0.75适用于不同数据集。
- 案例证明模型能成功发现跨文本潜在关系（如“合作”）并纠正误标关系（如“朋友”改为“合作”），增强知识图谱结构。

## 7. 优点
- **方法创新**：首次提出通过发现跨文本潜在事实来增强KGC，突破了LLM输入长度限制导致的碎片化问题。
- **无需微调**：基于提示调用LLM，可灵活适配不同基础模型，降低训练成本。
- **反事实纠正机制**：模仿人类反思行为，自动净化知识，减少事实错误，无需额外标注。
- **线索检索策略**：利用现有知识图谱结构提供上下文约束，引导LLM生成逻辑一致的关系，缓解幻觉。
- **实验全面**：从多个维度（消融、超参数、案例）验证方法有效性，结论可靠。

## 8. 不足与局限
- **依赖LLM能力**：性能受基础LLM质量影响，若LLM本身缺乏相关领域知识或易产生幻觉，可能导致不准确结果（如Mistral-7B表现差）。
- **超参数手动调节**：阈值λ、线索数k等需要人工调优，不同领域可能需要重新调整，泛化性有限。
- **计算成本**：多次调用LLM（提取、规范化、发现、纠正）可能带来较高延迟和API费用，未提供效率对比。
- **反事实生成噪声**：随机替换关系可能产生不合理反事实，影响纠正准确性，文中未分析反事实质量。
- **评估限制**：仅使用三个英文数据集，未涵盖多语言、垂直领域（如医疗、金融）或大规模场景；未评估对下游任务（如问答、推荐）的影响。
- **缺失统计检验**：未报告置信区间或显著性水平，削弱了结论的统计可靠性。

（完）

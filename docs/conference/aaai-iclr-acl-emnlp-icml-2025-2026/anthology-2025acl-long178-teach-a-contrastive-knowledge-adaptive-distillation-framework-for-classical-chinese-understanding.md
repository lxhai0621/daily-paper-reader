---
title: "TEACH: A Contrastive Knowledge Adaptive Distillation Framework for Classical Chinese Understanding"
title_zh: TEACH：面向文言文理解的对比知识自适应蒸馏框架
authors: "Yuting Wei, Qi Meng, Yuanxing Xu, Bin Wu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.178.pdf"
tags: ["query:ancient-text"]
score: 9.0
evidence: 文言文理解，结合词义消歧与句子翻译
tldr: 传统文言文处理将语言理解分割为独立任务，忽略了背景信息且用户参与度低。大语言模型虽能统一解决但计算成本高且易产生历史错误。本文提出TEACH框架，融合词义消歧与句子翻译，利用置信度标注的知识库和链式思维提示，在保持高效的同时提升了文言文理解的可解释性和准确性。实验表明该方法显著优于现有基线。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.178/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1465, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.178/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 786, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.178/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 729, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.178/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 790, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.178/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1385, \"height\": 745, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.178/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 404, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 733, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 783, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 783, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 612, \"height\": 115, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 740, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 704, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 810, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.178/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 670, \"height\": 899, \"label\": \"Table\"}]"
motivation: 传统文言文处理方法割裂任务且缺乏背景信息，大语言模型成本高且易出错。
method: 提出TEACH框架，融合词义消歧与句子翻译，结合置信度知识库和链式思维提示。
result: 在文言文理解任务上取得显著改进，降低了计算开销并提高了历史准确性。
conclusion: TEACH为古典中文数字化处理提供了高效准确的统一解决方案。
---

## Abstract
Traditional methods for processing classical Chinese typically segment language understanding into discrete tasks, which overlook crucial background information and reduce user engagement. Large language models (LLMs) provide integrated solutions, yet they entail high computational costs and risks of generating inaccurate historical information. To tackle these challenges, we propose a novel framework, TEACH (conTrastive knowlEdge Adaptive distillation with enhanCed Historical interpretability), which focuses on classical Chinese understanding by integrating word sense disambiguation with sentence translation. This integration leverages a confidence-annotated knowledge base and a step-by-step Chain-of-Thought prompting mechanism to minimize hallucinations and improve semantic analysis. Moreover, TEACH employs contrastive distillation learning to efficiently transfer capabilities from larger models to smaller ones (e.g., Qwen2-1.5B), addressing overly liberal translations. Additionally, we introduce an innovative generation evaluation metric using iterative word alignment, enhancing LLM performance assessments by distinguishing additional information and addressing excessive translation issues. Experiments conducted on real-world datasets validate TEACH’s efficacy in classical Chinese educational scenarios.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：传统文言文处理方法将词义消歧（WSD）和句子翻译视为独立任务，忽略了历史背景信息，且缺乏可解释性，用户参与度低。大语言模型（LLMs）虽能提供集成方案，但计算成本高昂，且容易产生历史幻觉（hallucinations）或过度意译。
- **意义**：本文旨在开发一个统一框架，既能同时完成WSD和翻译，又能提供历史背景的可解释输出，并通过知识蒸馏将大模型能力迁移至小模型，降低部署成本，适用于文言文教育场景。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：提出TEACH框架（conTrastive knowlEdge Adaptive distillation with enhanCed Historical interpretability），结合检索增强生成（RAG）、链式思维（CoT）提示、对比蒸馏学习，将教师模型（ERNIE-Bot4）的推理能力迁移到学生模型（如Qwen2-1.5B）。
- **关键技术细节**：
  - **可解释知识构建**：
    - 构建历史信息知识库（基于《二十四史》等，使用Milvus向量数据库），检索时加入置信度评分（基于长度惩罚和欧氏距离）。
    - 收集169,742个文言词义注释（来自汉典网），用于词义选择。
  - **对比知识自适应蒸馏**：
    - **教师生成**：设计三步零样本CoT提示：（1）分析历史背景；（2）从注释中选择合适词义；（3）结合前两步进行直译。
    - **学生训练**：对3,000条高质量数据微调，采用两项损失：
      - 蒸馏损失（`Ldis`）：负对数似然，以标准直译`es`为标签。
      - 对比损失（`Lcon`）：以教师生成的自由翻译`os`为负样本，`es`为正样本，对翻译部分进行token级对比学习，抑制过度意译。
      - 总损失 `L = -(Ldis + Lcon)`，使用LoRA参数高效微调。
  - **改进的评估指标**：
    - 针对LLMs常有的过度解释和额外信息问题，提出**迭代自标注词对齐（WAS）**方法，通过最优传输求解对齐矩阵，并采用迭代更新和合并策略，生成对齐后的序列`C'`和`R'`。
    - 定义 **BLEU_WAS** 和 **ROUGE-WAS**，分别对候选和参考进行对齐并计算n-gram重叠，惩罚过长/过短翻译。

## 3. 实验设计
- **数据集**：使用Erya数据集（最大文言文翻译数据集），覆盖不同历史时期和文体。训练集随机选取3,000条生成高质量推理数据（经专家校正），测试集10,000条（从验证集抽取）。
- **基准方法**：
  - 经典模型：Erya（最先进文言文翻译模型）。
  - LLMs：Yi1.5-6B、ChatGLM3-6B、GLM-4-9B、Qwen2-1.5B/7B、Xunzi-Qwen2（在Qwen2上用文言文语料微调），均使用Base和Chat版本。
  - 对比方法：Normal prompt（简单翻译指令） vs TEACH prompt（三步CoT+知识库）。
- **评估指标**：传统指标（BLEU、ROUGE、BERTScore、METEOR）及改进指标（BLEU_WAS、ROUGE_WAS）。还进行了人工评估（5名专家，6个维度：历史完整性、准确性、词义准确性、翻译流畅度、翻译准确性、风格一致性）。

## 4. 资源与算力
- **教师模型**：使用百度的ERNIE-Bot4 API（闭源）。
- **学生模型微调**：在1块NVIDIA A100 GPU（40GB显存）上进行，batch size=64，epochs=10，学习率5e-5，使用LoRA。具体训练时间未明确说明。
- **评估**：词对齐计算在NVIDIA 3090 GPU上执行，每10,000句约2-3分钟。
- **推理**：TEACH训练的Qwen2-1.5B可在一张3090 GPU上部署，推理时间约0.87秒/句；7B模型约2.59秒。

## 5. 实验数量与充分性
- **实验组数**：
  - 主表1：对比9种LLM的Base/Chat版本在Normal和TEACH下的8项指标，共约18组+Erya。
  - 表2：消融提示与训练策略（6种配置）。
  - 表3：组件消融（历史H、注释A、对比损失Lcon，5种配置）。
  - 表4：人工评估（4种模型输出）。
  - 图6：训练数据规模影响（1000-3000条）。
- **充分性与公平性**：
  - 覆盖多种规模（1.5B-7B）和训练方式（Base vs Chat）的LLMs。
  - 消融实验验证各组件贡献（H、A、Lcon），控变量合理。
  - 人工评估采用5名专家，Cronbach's Alpha=0.89，信度高。
  - 对比基线包括传统专用模型和多种LLM，公平性较好。但未与更大型LLM（如GPT-4）直接对比。

## 6. 主要结论与发现
- TEACH框架在所有骨干模型上均显著优于Normal prompt，平均提升4-11%（表1）。
- 即使是小模型（Qwen2-1.5B Base）经TEACH训练后，性能接近甚至超过大模型（如7B）的Normal版本。
- 改进指标（BLEU_WAS/ROUGE_WAS）能更准确评估LLMs的额外信息和过度翻译问题。
- 历史上下文（H）和词义注释（A）共同作用时效果最佳；对比损失（Lcon）有助于保持直译风格，但可能略微降低语义丰富度（表3）。
- 人工评估显示，TEACH训练的Qwen2-7B在翻译风格一致性上甚至优于教师模型ERNIE-Bot4（表4）。

## 7. 优点
- **任务统一与可解释性**：首次将WSD与翻译融合，并提供历史背景分析，适合教育场景。
- **蒸馏效率高**：仅用3,000条数据即可将大模型推理能力迁移到小模型（参数仅0.8-4%），资源开销小。
- **针对LLM特点的评估改进**：提出的WAS指标有效处理了过度翻译和额外信息，更贴合人类判断。
- **实验设计全面**：从自动指标、消融、人工评估多维度验证。

## 8. 不足与局限
- **跨语言适应性弱**：扩展到其他语言需重新构建领域知识库和调整CoT提示，依赖专家资源。
- **知识库构建尚未自动化**：历史信息检索依赖人工标注的置信度，词义注释需从特定网站爬取，可能无法覆盖所有文言词汇。
- **实验局限**：
  - 仅使用Erya一个数据集，未在多个文言文理解任务（如阅读理解、问答）上验证。
  - 未与GPT-4、Claude等更强LLM对比（受限于API成本）。
  - 对比损失中对负样本的定义依赖教师输出，可能引入教师偏差。
- **应用限制**：小模型在翻译流畅性上仍与教师有差距，需进一步优化。

（完）

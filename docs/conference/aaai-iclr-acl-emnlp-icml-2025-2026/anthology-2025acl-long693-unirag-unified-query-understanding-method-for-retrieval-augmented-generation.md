---
title: "UniRAG: Unified Query Understanding Method for Retrieval Augmented Generation"
title_zh: UniRAG：面向检索增强生成的统一查询理解方法
authors: "Rui Li, Liyang He, Qi Liu, Zheng Zhang, Heng Yu, Yuyang Ye, Linbo Zhu, Yu Su"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.693.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: RAG统一查询理解
tldr: 该论文针对RAG中查询增强与编码分离导致的错误累积和策略选择困难问题，提出统一框架UniRAG。采用仅解码器LLM联合进行查询增强和编码，消除任务分离，并通过可学习路由自动选择最优增强策略。实验表明UniRAG在多种复杂查询类型上显著提升了RAG的准确性和效率，确保了鲁棒性。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1644, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.693/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 786, \"height\": 376, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1600, \"height\": 794, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 827, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 759, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.693/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 366, \"label\": \"Table\"}]"
motivation: 现有查询增强方法任务分离，信息共享不足且策略选择困难。
method: 设计统一解码器架构，联合执行查询增强与编码，并引入可学习路由。
result: 在多个RAG基准上，UniRAG在准确性和效率上均优于现有方法。
conclusion: 统一查询处理是提升RAG系统性能的关键。
---

## Abstract
Retrieval-Augmented Generation (RAG) technology effectively addresses the issues of knowledge update lag and hallucinations in large language models (LLMs) by integrating internal and external knowledge. Existing query augmentation methods improve RAG’s performance in handling complex queries but face two key challenges: (1) the separation of query augmentation and encoding tasks, which hinders information sharing and introduces cumulative errors, and (2) the difficulty of selecting the optimal augmentation strategy for different scenarios. In this work, we propose UniRAG, a unified framework for query understanding in RAG. UniRAG employs a decoder-only LLM to jointly perform query augmentation and encoding, eliminating task separation. To facilitate adaptive query augmentation, we categorize existing techniques into query paraphrasing, query expansion, and query abstraction. Our model learns to select the optimal augmentation strategy based on user queries, leveraging retrieval and generation outputs as feedback. Experimental results show that UniRAG significantly outperforms traditional query augmentation methods in five knowledge-intensive benchmark tasks in both closed and open domain question answering.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **背景**：检索增强生成（RAG）通过结合内部与外部知识，有效缓解了大语言模型（LLM）的知识更新滞后和幻觉问题。现有查询增强方法（如改写、扩展、抽象）虽提升了复杂查询的处理能力，但面临两大挑战：
  1. **任务分离**：查询增强与编码任务作为独立模型或阶段运行，限制了信息共享，易导致累积误差。
  2. **策略选择困难**：不同增强方法在不同场景下表现各异，难以针对特定查询选择最优策略。
- **整体含义**：为了克服上述问题，论文提出 **UniRAG**——一个统一的查询理解框架，旨在通过端到端模型联合执行查询增强与编码，并自适应选择增强策略，从而提升RAG系统的鲁棒性与性能。

## 2. 方法论
### 2.1 核心思想
- 使用一个 **decoder-only LLM**（基于Llama-3.1-8B）同时完成查询增强和查询编码，消除任务分离。
- 将现有增强技术归纳为三类：**查询改写（Paraphrase）**、**查询扩展（Expansion，如HyDE）**、**查询抽象（Abstraction，如Step-back Prompting）**，并增加“无需增强”选项。
- 利用**检索器反馈**（首位相关文档的倒数排名）和**生成器反馈**（生成答案的对数概率）作为选择增强策略的信号。

### 2.2 关键技术细节
- **两阶段训练**：
  - **阶段1：查询增强训练**  
    - 从多个知识密集型QA/检索数据集（如Natural Questions、MS MARCO、BoolQ等）中采样种子数据，使用GPT-4o-mini为每个查询生成三类增强查询。  
    - 收集检索器与生成器的反馈分数，过滤掉效果差于原始查询的实例。  
    - 训练目标包含两部分：  
      - **策略选择损失** \(L_{sel}\)：将反馈分数映射到动作token（如`<Paraphrase>`），用KL散度对齐模型预测分布与反馈概率分布。  
      - **增强查询生成损失** \(L_{gen}\)：标准的下一个token预测损失。  
    - 总损失：\(L_{enh} = L_{sel} + L_{gen}\)。
  - **阶段2：查询编码训练**  
    - 将原始查询、增强查询与指令模板拼接，附加`<EOS>` token提取嵌入。  
    - 使用InfoNCE对比损失 \(L_{ret}\) 训练查询与文档的相似度，同时融入硬负样本挖掘。

### 2.3 推理机制
- **默认解码**：选择概率最高的动作token并贪婪生成增强查询。
- **基于阈值的解码**：计算原始token概率与最大增强token概率的比值，低于阈值 \(\gamma\) 时才执行增强，可控制增强频率。
- **基于树的解码**：生成所有概率不低于原始token的动作，使用束搜索（beam size B）探索多种策略组合，并通过倒排秩融合（RRF）合并检索结果。

## 3. 实验设计
### 3.1 数据集与场景
- **闭集问答**：PubHealth（事实验证）、ARC-Challenge（科学推理选择题）。
- **开放域问答**：PopQA（长尾实体查询）、TriviaQA-unfiltered、TimeQA（时间敏感查询）。  
  共5个知识密集型基准，涵盖不同复杂度和领域。

### 3.2 基准与对比方法
- **基线**：
  - 无检索（Zero-shot Prompting）
  - 原始查询直接检索
  - 单独使用查询改写、HyDE、Step-back Prompting（基于GPT-4o-mini生成）
- **生成器**：Llama-3-8B-Instruct、Llama-3-70B-Instruct、GPT-4o-mini。
- **检索器**：Contriever-MS MARCO（统一固定）。

### 3.3 评价指标
- 准确率（基于生成答案是否包含标准答案，不要求严格文本匹配）。

## 4. 资源与算力
- **训练硬件**：4张 NVIDIA A100 80GB GPU。
- **训练框架**：DeepSpeed ZeRO-3、FlashAttention2、BFloat16精度。
- **训练细节**：
  - 增强阶段：3个epoch，batch size 256，峰值学习率2e-5，线性衰减+3%预热，最大序列长度512。
  - 编码阶段：1个epoch，LoRA秩16，梯度检查点，温度\(\tau=0.01\)。
- **未明确说明**：具体的训练总时长。

## 5. 实验数量与充分性
- **主要结果**（表1）：在5个数据集×3种生成器上，比较UniRAG与5种基线，共15组对比，全面验证一致性优势。
- **消融实验**（表2）：
  - 查询增强阶段：仅用检索反馈、仅用生成反馈、拒绝采样策略。
  - 查询编码阶段：使用Contriever、去除增强训练、去除额外数据。
- **解码策略分析**（图3a）：对比默认、阈值（多\(\gamma\)值）、树搜索的性能与延迟。
- **数据规模影响**（图3b）：在PopQA和PubHealth上测试5k~100k训练数据的效果。
- **策略准确率分析**（图4）：使用2.1K验证集比较UniRAG与其他方法的选择胜率。
- **充分性评价**：实验覆盖多任务、多模型、多维度消融，对比充分，结果客观。但未在多检索器（如BM25、其他稠密检索器）上验证，且未在更多领域（如代码、对话）测试。

## 6. 主要结论与发现
- UniRAG在所有5个基准数据集上**一致优于**所有独立查询增强方法，平均提升2~9个准确率百分点。
- **自适应策略选择有效**：UniRAG在90%以上案例中正确选择或优于单一策略，避免“一刀切”缺陷。
- **统一框架优势显著**：端到端联合训练比分离式（仅增强或仅编码）更优，验证了信息共享和误差减少的假设。
- **灵活解码平衡效率与精度**：基于树的搜索性能最高但延迟大；基于阈值的解码可通过\(\gamma\)调节，适应不同应用需求。
- **数据规模正相关**：更多合成数据带来持续性能提升，说明框架具有扩展潜力。

## 7. 优点（方法或实验设计亮点）
- **统一性**：首次将查询增强与编码融合到一个decoder-only LLM中，消除任务分离，减少误差累积。
- **自适应**：通过可学习的策略选择机制，动态为每个查询选择最优增强方法，而非固定规则。
- **可插拔性**：UniRAG可无缝集成到不同LLM（已验证8B/70B/GPT-4o-mini），且支持自定义解码策略。
- **反馈驱动**：同时利用检索器和生成器的反馈作为监督信号，兼顾检索相关性与生成质量。
- **实验严谨**：覆盖多种任务类型、多种模型规模、全面消融及超参数分析，结果可信。

## 8. 不足与局限
- **策略预设局限**：仅基于三类预定义增强策略，可能无法泛化到所有领域或用户意图（如需要多跳推理、结构查询等）。
- **依赖检索文档质量**：性能仍受限于检索器检索到的文档质量，在低资源或高度专业化领域可能引入噪声。
- **合成数据依赖**：增强查询由GPT-4o-mini生成，可能引入固有偏差，且影响模型在非英语场景的泛化性。
- **实验覆盖有限**：未在更多样化的检索器（如BM25、ColBERT）或任务（如代码生成、对话）上验证，也未分析不同LLM作为检索器时的表现。
- **计算开销**：树搜索解码虽性能高但延迟较大，实际部署可能需要权衡；训练阶段使用4×A100对部分团队仍属较高成本。

（完）

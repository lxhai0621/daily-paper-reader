---
title: "LongRecipe: Recipe for Efficient Long Context Generalization in Large Language Models"
title_zh: LongRecipe：高效扩展大语言模型长上下文泛化的方法
authors: "Zhiyuan Hu, Yuliang Liu, Jinman Zhao, Suyuchen Wang, Yan Wang, Wei Shen, Qing Gu, Luu Anh Tuan, See Kiong Ng, Zhiwei Jiang, Bryan Hooi"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.581.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 高效扩展大语言模型长上下文窗口
tldr: 大语言模型在预训练阶段上下文窗口有限，且扩展窗口的资源消耗极大。本文提出LongRecipe策略，通过影响性令牌分析、位置索引变换和训练优化，模拟长序列输入并显著提升模型对长距离依赖的理解。实验在三种不同类型的大语言模型上验证了有效性，实现了资源高效的上下文扩展，支持更长的检索窗口。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.581/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1630, \"height\": 847, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.581/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 771, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.581/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 504, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.581/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1568, \"height\": 1516, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.581/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1517, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.581/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.581/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 534, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.581/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 646, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.581/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1413, \"height\": 643, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.581/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1413, \"height\": 534, \"label\": \"Table\"}]"
motivation: 大语言模型上下文窗口有限且扩展成本高昂。
method: 提出LongRecipe策略，包括影响性令牌分析、位置索引变换和训练优化。
result: 在三种大语言模型上验证了方法有效性，显著提升长上下文理解能力。
conclusion: LongRecipe为长上下文泛化提供了高效训练方案。
---

## Abstract
Large language models (LLMs) face significant challenges in handling long-context tasks because of their limited effective context window size during pretraining, which restricts their ability to generalize over extended sequences. Meanwhile, extending the context window in LLMs through post-pretraining is highly resource-intensive.To address this, we introduce LongRecipe, an efficient training strategy for extending the context window of LLMs, including impactful token analysis, position index transformation, and training optimization strategies. It simulates long-sequence inputs while maintaining training efficiency and significantly improves the model’s understanding of long-range dependencies. Experiments on three types of LLMs show that LongRecipe can utilize long sequences while requiring only 30% of the target context window size, and reduces computational training resource over 85% compared to full sequence training. Furthermore, LongRecipe also preserves the original LLM’s capabilities in general tasks. Ultimately, we can extend effective context window of open-source LLMs from 8k to 128k, achieving performance close to GPT-4 with just one day of dedicated training using a single GPU with 80G memory. Our code is released at https://github.com/zhiyuanhubj/LongRecipe.

---

## 论文详细总结（自动生成）

# 论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLMs）在预训练阶段的有效上下文窗口有限（通常为4k–8k），导致其在长上下文任务（如长文档摘要、长程问答、上下文中学习）中泛化能力不足。直接通过后训练扩展上下文窗口面临计算和内存成本呈二次增长的问题，资源消耗巨大。
- **研究动机**：现有高效扩展方法（如PoSE、RPES）存在局限性：PoSE只考虑两个片段来模拟位置索引，遗漏了长距离依赖；RPES随机选择位置编码会破坏局部句子结构，导致泛化差距。因此，需要一种既能高效训练又能保留长距离依赖、同时保持模型通用能力的方法。
- **整体含义**：提出LongRecipe，一种高效的训练策略，通过模拟长序列输入、减少资源消耗，显著提升LLM的长上下文泛化能力，并保持原有通用能力。

## 2. 方法论

### 核心思想
通过**影响性令牌分析**识别对长文本训练至关重要的令牌，从中提取短片段；再通过**位置索引变换**模拟长序列的位置索引；最后使用**预训练数据重放**和**模型合并**优化训练，保持模型通用能力。

### 关键技术细节
- **影响性令牌分析**：比较基础模型（短上下文）和扩展模型（长上下文）在相同输入上的logit变化，计算每个令牌类型的显著性分数Δ(t)，选择变化最大的20%令牌类型（如数字、代词等）作为锚点。基于这些锚点筛选和上采样包含这些令牌的句子，构建紧凑的训练样本。
- **位置索引变换**：将原始长序列分割成句子/段落（segment），在训练时随机跳过一定范围的位置索引（0到M），使片段间的距离增大，模拟更长序列的位置关系。公式：pos(s_i) = pos(s_{i-1}) + |s_{i-1}| + g(s_i) + 1，其中g(s_i)是随机跳跃步长。这样可以在短片段上模拟远距离依赖。
- **训练优化策略**：
  - **预训练数据重放**：在长上下文训练后，使用与原预训练数据同分布的重放数据集进行额外训练，恢复模型通用能力。
  - **模型合并**：将原始模型（短上下文）与训练后的模型（长上下文+重放）按权重λ1、λ2（实验中均取0.5）合并，兼顾通用能力和长上下文能力。

## 3. 实验设计

### 使用的数据集和Benchmark
- **训练数据**：基于SlimPajama的80k样本（每样本128k tokens），来源于Fu et al. (2024)，包含领域平衡和长度上采样。实验中使用10k样本。
- **长上下文泛化评估**：
  - **Multi-Needle In A Haystack (NIAH(M))**：多针检索任务，评估模型检索隐藏信息的能力。
  - **RULER**：包含13个子任务的综合基准，覆盖检索、问答等。
  - **LongBench**：双语长上下文理解基准（21个子集）。
- **通用能力评估**：
  - **MMLU**（57个学科）、**GSM8K**（小学算术推理）、**HumanEval**（代码生成）。

### 对比方法
- **Full-length Text Training (FLT)**：使用完整目标长度语料训练。
- **Randomized Positional Encoding Scheme (RPES)**：随机选择位置索引模拟长序列。
- **Positional Skip-wisE (PoSE)**：固定上下文窗口分块并添加跳跃偏置。
- **其他开源/闭源模型**：Llama3-8B、Mistral-7B、Qwen2-7B及其指令版本，以及GPT-4、Gemini-1.5-Pro等。

## 4. 资源与算力

- **训练配置**：以Llama3-8B为例，扩展至80k上下文使用1×A800/H100 GPU（80G内存），训练时长26/16小时（A800/H100）；扩展至128k使用2×A800/H100 GPU，约30/20小时。总训练tokens约240M（80k）或384M（128k）。
- **效率**：仅使用目标上下文窗口的30% tokens（如24k/80k），计算资源减少超过85%，对比FLT（需完整序列训练）。
- **最终结果**：单张H100 GPU一天内可将8k模型扩展至128k，性能接近GPT-4。

## 5. 实验数量与充分性

- **实验数量**：在三种不同架构的LLM（Llama3-8B、Mistral-7B、Qwen2-7B）上进行实验，覆盖80k和128k两种目标长度。每个模型都对比了FLT、RPES、PoSE和LongRecipe。报告了NIAH(M)、RULER、LongBench以及通用能力指标（MMLU、GSM8K、HumanEval）。还包含了消融实验（表2-4）和与众多开源/闭源模型的比较（表1）。
- **充分性**：实验设计较为全面，覆盖了主流基准和多种模型，消融实验验证了每个组件的效果（如影响性令牌分析、位置索引变换、重放和合并）。但未在更大模型（如70B）上进行消融，也未包含监督微调（SFT）阶段的实验，作者在局限中已提及。整体上实验客观公平，对比方法均使用相同设置。

## 6. 主要结论与发现

- **长上下文泛化**：LongRecipe在NIAH(M)上平均比RPES高6.6%、比PoSE高7.8%；在RULER上比RPES高2.9%、比PoSE高4.7%。在Llama3-8B的80k设置下，NIAH(M)提升10.1%。
- **效率优势**：仅需30%的token即可达到接近全量训练的性能，训练成本降低85%以上。增加token比例至100%仅有约1%的提升。
- **通用能力保持**：通过重放和模型合并，模型在MMLU、GSM8K、HumanEval上的下降幅度极小（如MMLU从65.7%降至63.0%），恢复了约75%的数学和65%的编程能力。
- **性能对标**：LongRecipe训练的Llama3-8B在128k窗口下性能超过Yi-9B、Llama3.1-8B等基础模型，接近GPT-4水平。

## 7. 优点

- **方法创新**：结合影响性令牌分析和位置索引变换，在短序列上模拟长距离依赖，兼顾效率和有效性。
- **资源高效**：极大降低计算和内存需求（单GPU即可完成扩展），具有实际应用价值。
- **通用性**：适用于多种LLM架构（Llama、Mistral、Qwen），无需架构修改。
- **保持通用能力**：通过重放和模型合并策略，有效缓解了长上下文训练对基础能力的负面影响。
- **分析深入**：对令牌类型、距离、连续段长度等进行了详细分析，解释了方法有效性的原因。

## 8. 不足与局限

- **缺乏监督微调（SFT）**：当前工作仅限于持续预训练/后训练，未结合长上下文SFT（如LongWriter），导致与顶级指令模型仍有差距（如与Llama3.1-8B-Instruct对比）。
- **实验覆盖有限**：未在更大规模模型（如70B、130B）上进行实验，也未在更长上下文（如512k、1M）上验证。作者计划在后续工作中扩展。
- **语义连贯性影响**：方法丢弃了部分不包含关键令牌的句子，可能影响文本的语义连贯性。但作者通过长依赖分数分析认为影响不大。
- **可解释性不足**：对“影响性令牌”的选择标准（top 20%基于logit变化）缺乏深入理论解释，可能依赖经验阈值。
- **应用限制**：方法依赖两阶段（原始模型和扩展模型）的比较，需要先有一个经过长上下文训练的参考模型，这在实际部署中可能增加成本。

（完）

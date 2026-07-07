---
title: "CNNSum: Exploring Long-Context Summarization with Large Language Models in Chinese Novels"
title_zh: CNNSum：基于大语言模型的中文小说长上下文摘要探索
authors: "Lingxiao Wei, He Yan, Lu Xiangju, Junmin Zhu, Jun Wang, Wei Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.421.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 中文小说长上下文摘要数据集
tldr: CNNSum针对长上下文摘要缺乏标注数据的问题，构建了基于中文小说的多尺度摘要基准（16k-128k）。通过评测多种LLM并进行人工分析，发现高级模型会产生主观评论导致摘要模糊，且目前长上下文摘要主要依赖于检索窗口的大小设置。该工作为长上下文管理提供了重要参考。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.421/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 795, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.421/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.421/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.421/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1650, \"height\": 859, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.421/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 780, \"height\": 610, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1618, \"height\": 1545, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1633, \"height\": 382, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 661, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 809, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 792, \"height\": 585, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1650, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1091, \"height\": 2404, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1648, \"height\": 1272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1631, \"height\": 1039, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.421/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1634, \"height\": 1027, \"label\": \"Table\"}]"
motivation: 长上下文摘要数据集匮乏，阻碍了该领域的研究进展。
method: 构建包含695个样本、长度从16k到128k的多尺度中文小说摘要基准。
result: 发现当前LLM在长上下文摘要中易产生主观评论，且依赖窗口大小。
conclusion: 为长上下文摘要研究提供了基准和深入分析。
---

## Abstract
Large language models (LLMs) have been well-researched in various long-context tasks. However, the scarcity of long-context summarization datasets hinders progress in this area. To address this, we introduce CNNSum, a multi-scale long-context summarization benchmark based on Chinese novels, featuring human-driven annotations across four subsets totaling 695 samples, with lengths ranging from 16k to 128k. We benchmark numerous LLMs and conduct detailed human assessments to summarize abnormal output types. Furthermore, we extensively explore how to improve long-context summarization. In our study: (1) Advanced LLMs may generate much subjective commentary, leading to vague summaries. (2) Currently, long-context summarization mainly relies on memory ability. The advantages of Large LLMs are hard to utilize, thus small LLMs are more cost-effective. (3) Different prompt types paired with various version models may cause large performance gaps. In further fine-tuning, these can be mitigated, and the Base version models perform better. (4) LLMs with RoPE-base scaled exhibit strong extrapolation potential; using short-context data can significantly improve long-context summarization performance. However, further applying other interpolation methods requires careful selection. (5) CNNSum provides more reliable evaluation results than other benchmarks. We release CNNSum to advance future research.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与研究动机
- **问题**：长上下文摘要数据集严重匮乏，阻碍了大型语言模型（LLM）在该领域的研究进展。现有基准存在数据泄露风险、样本量小、长度不足（多低于16k）、缺乏多尺度子集、标注质量低（依赖网络收集或LLM合成）等问题。
- **动机**：构建一个高质量、多尺度、基于人工标注的中文小说长上下文摘要基准，系统评估并改进LLM在此任务上的表现。

## 2. 方法论：核心思想与技术细节
- **数据集构建（CNNSum）**：
  - **语料收集**：从中文互联网开源数据收集103本书，去除无主线故事或由短篇组成的书籍，并通过Qwen2-72B-Instruct检测泄露风险，过滤掉27本可能被模型广泛记忆的书籍。
  - **多尺度采样**：使用Yi分词器定义四个目标长度（16k、32k、64k、128k），每个子集有特定范围（如16k-4k~16k+2k）。对每本书采用滑动窗口采样，优先从样本少的书籍选取数据以保证多样性。最终获得695个样本。
  - **摘要标注**：采用“增量更新”方法，先用多种商业LLM（Qwen、Doubao、Kimi、Gemini）生成每章情节概要，然后由23名人工专家选择关键情节并用自己的话重写摘要，避免主观评论。每样本由一位专家标注，另一位审核一致性。
- **评估设置**：
  - 两种提示类型：指令在开头（Prompt-IB）和指令在结尾（Prompt-IE）。
  - 主要指标：ROUGE-L（中文分词用jieba）；辅助指标：BERTScore（用中文XLNet-Large）。
- **微调实验**：
  - 训练数据：约9000个独立于CNNSum语料的中文小说摘要样本（长度2k~4k），将短样本随机拼接成长序列（平均16k和32k），以激活模型的外推能力。
  - 微调方法：使用LoRA（rank=8），并解冻嵌入层和归一化层，基于Flash Attention 2和DeepSpeed。

## 3. 实验设计
- **数据集/场景**：
  - 主基准：CNNSum（四个子集L、XL、2XL、3XL）。
  - 对比基准：CLongEval-LStSum（含Small、Medium、Large三个子集）。
- **Baseline方法**：
  - **商业模型**：GPT-4o、GPT-4o-mini、Gemini-1.5-pro、Moonshot-v1、Qwen-plus、Doubao-pro。
  - **开源模型**：Yi系列（6B/34B/200K）、InternLM2.5系列（7B/20B/1M）、ChatGLM3-6B-128K、GLM4-9B-Chat-1M、Llama3.1系列（8B/70B、128k）、Qwen1.5/2/2.5系列（7B/32B/72B）、Ministral-8B-Instruct、LWM-Text-1M等。
- **对比方法**：主要对比不同模型、不同提示模板、不同模型版本（Base vs Chat/Instruction）、不同位置编码缩放方法（原始RoPE、PI、NTK、YaRN）。

## 4. 资源与算力
- 文中提及微调实验在 **NVIDIA A100（80GB）GPU** 上进行，但未明确说明使用的GPU数量。
- 训练步数：对于平均长度16k的数据，训练400~500步；对于32k数据，从16k检查点继续微调200~300步。
- 算力描述较为简略，未提供总GPU·小时数，仅说明了实验环境。

## 5. 实验数量与充分性
- **实验组数**：大量实验，包括：
  - 主基准表（Table 2）：涵盖20+个模型在四子集上的ROUGE-L结果。
  - BERTScore表（Table 3）：商业模型的额外评估。
  - 提示对比表（Table 4、10）：针对高MSE模型的详细Prompt-IB vs Prompt-IE结果。
  - 微调消融表（Table 5、11）：不同模型系列、不同位置编码缩放方法（PI、NTK、YaRN）及不同训练长度。
  - 外推可靠性分析（Figures 1-4）：对比CNNSum与CLongEval在不同缩放设置下的性能曲线。
- **充分性评估**：实验设计较为系统，覆盖了多种模型类型（商业/开源、大/小、Base/Chat）、多种提示策略、多种位置编码方法，并进行了人工案例分析。消融实验较为完整。但主要依赖单一自动指标ROUGE-L，且未做更复杂的自动评估（如GPT-4作为评判）。整体公平性较好，但部分商业模型因内容安全过滤导致样本排除，可能引入偏差。

## 6. 主要结论与发现
1. **高级LLM易产生主观评论**：GPT-4o等模型倾向于输出主观叙述，导致摘要模糊，而聚焦客观情节的模型（如Moonshot-v1）得分更高。
2. **小模型更具成本效益**：长上下文摘要主要依赖记忆能力，大模型的推理优势难以发挥；InternLM2.5-7B-1M表现接近20B版本，成本更低。
3. **提示类型与模型版本影响大**：Prompt-IB vs Prompt-IE可导致巨大性能差距，尤其对短上下文模型（如Qwen1.5-7B）。微调后差距可消除；Base版本模型比Chat/Instruction版本更适合微调和外推。
4. **RoPE-base缩放模型具有强外推潜力**：使用短上下文数据微调可显著提升长上下文摘要能力，但结合其他插值方法（如PI、NTK）需谨慎选择，过度插值可能损害外推表现。
5. **CNNSum提供更可靠评估**：相比CLongEval-LStSum，CNNSum的长子集样本长度更集中，避免了长短样本混排导致的误导性高平均分。

## 7. 优点
- **数据集质量高**：基于全新语料，避免泄露风险；多尺度设计（16k~128k），覆盖不同难度；人工+LLM协作标注，保证准确性和效率。
- **实验系统全面**：涵盖商业和开源模型、多种提示、模型版本、位置编码方法，并进行人工错误类型分析。
- **实用洞察**：指出小模型、Base版本、无插值微调的优越性，为实际应用提供了明确指导。
- **评估可靠性**：通过对比实验证明CNNSum在长外推评价上更稳定，避免CLongEval的误导。

## 8. 不足与局限
- **自动评估指标局限**：主要依赖ROUGE-L，未采用更先进的LLM-based评估（如GPT-4评分），人工分析仅用于案例而非全覆盖。
- **提示模板多样性不足**：仅使用了两种提示类型，更复杂的提示可能带来细微差异，未深入探索。
- **微调实验基于LoRA**：可能无法代表全参数微调的效果；拼接数据的潜在干扰（如短数据集间互相影响）未探究。
- **单语言、单领域**：仅中文小说，泛化性有限；未来需扩展到英文及其他领域。
- **算力细节缺失**：未报告具体GPU数量和训练耗时，不易复现资源需求。
- **商业模型样本排除**：部分样本因安全过滤或长度限制被排除，可能引入偏差。

（完）

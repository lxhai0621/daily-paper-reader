---
title: "ConvX: A Lightweight Converter to Bridge Indexed Dense Representations and Large Language Models for Retrieval-Augmented Generation"
title_zh: ConvX：桥接索引稠密表示与大模型以提升检索增强生成的轻量转换器
authors: "Bonggeun Choi, Keunha Kim, Junho Han, Youngjoong Ko"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1823.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 基于压缩的 RAG 缓解长检索上下文
tldr: 检索增强生成通过引入外部知识提升了开放域问答，但检索上下文会显著扩展输入提示，使 transformer 生成器面临随序列长度和维度平方级增长的计算开销与推理延迟。针对这一效率瓶颈，作者提出 ConvX，一种轻量转换器，将索引化稠密表示与大模型桥接，对检索内容进行压缩。实验表明该压缩式 RAG 方法能在维持效果的同时降低长上下文带来的延迟，为高效 RAG 的检索窗口管理提供思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1823/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 2705, \"height\": 1411}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1823/fig-002.webp\", \"caption\": \"\", \"page\": 7, \"index\": 2, \"width\": 1600, \"height\": 1000}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1823/fig-003.webp\", \"caption\": \"\", \"page\": 8, \"index\": 3, \"width\": 2809, \"height\": 577}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1823/fig-004.webp\", \"caption\": \"\", \"page\": 9, \"index\": 4, \"width\": 577, \"height\": 578}]"
motivation: RAG 中检索上下文大幅扩展输入提示，导致 transformer 生成器推理延迟随序列长度和维度急剧上升。
method: 提出轻量转换器 ConvX，将索引化稠密表示与大模型桥接，对检索上下文进行压缩以降低计算开销。
result: 实验显示该压缩式 RAG 方法在保持生成效果的同时有效降低长上下文带来的推理延迟。
conclusion: 该工作为缓解 RAG 长上下文瓶颈、提升检索增强生成效率提供了轻量可行的方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) has significantly advanced open-domain question answering systems by incorporating external knowledge into large language models. Despite its effectiveness, existing RAG pipelines suffer from critical efficiency limitations. In particular, modern transformer-based generators exhibit quadratic or higher computational complexity with respect to input sequence length and hidden dimensionality, leading to substantial inference latency as model scales and contextual inputs increase. This issue is exacerbated in RAG settings, where retrieved contexts substantially expand the input prompt. To alleviate this challenge, we propose an effective compression-based RAG framework, ConvX, that directly leverages indexed dense representations produced by a retriever, entirely substituting to long text contexts. Our approach expands a single dense representation into a fixed number of memory slots using a lightweight converter to provide rich lexical information. This design enables efficient knowledge integration while significantly reducing input length and computational overhead. Empirical evaluations demonstrate that the proposed model achieves competitive performances compared to the existing state-of-the-art model that uses a large ad-hoc context compressor, while offering substantially improved inference efficiency.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：检索增强生成（RAG）通过引入外部知识提升开放域问答的事实准确性和可更新性，但检索到的长上下文会显著扩展输入提示。
- **核心问题**：Transformer 生成器对输入序列长度和隐藏维度具有二次或更高计算复杂度，检索上下文越长，推理延迟和计算开销越大。现有压缩方案存在明显不足：
  - 文本压缩方法压缩率有限，难以彻底解决长上下文问题。
  - 基于嵌入的压缩方法通常依赖 ad-hoc 压缩器，容易过拟合训练数据，使 memory slots 退化为软提示而非忠实知识载体。
  - 存在“双重编码”问题：同一 passage 先被 retriever 编码，又被压缩器编码。
  - 预计算并索引 memory slots 会带来额外存储开销。
  - xRAG 等方法虽直接注入 retriever 嵌入，但用单个向量表示整个 passage，且常只用 top-1 结果，细粒度信息损失严重。
- **整体含义**：论文提出 ConvX，一个轻量转换器框架，直接复用检索器产生的索引化稠密表示，将其扩展为固定数量 memory slots，替代长文本上下文，从而在保持竞争力的同时显著提升 RAG 推理效率。

## 2. 方法论

- **核心思想**：不重新压缩原始文本，也不依赖大型 ad-hoc 压缩器；而是把 retriever 已产生的 passage embedding 切分并投影到 LLM 嵌入空间，扩展成多个 memory slots，显式保留 passage 级词汇信息。
- **整体流程**：三阶段训练。
  - **Stage 1：预训练 Converter**
    - 将 retriever passage embedding 分成 \(M\) 个 chunk，得到 \(H \in \mathbb{R}^{M \times D'_r}\)，其中 \(D'_r = D_r / M\)。
    - 通过三层 converter 投影到 LLM 隐藏维度：\(\tilde{Z} = \text{Converter}(H) \in \mathbb{R}^{M \times D_g}\)。
    - Converter 中间层对 \(M\) 个 memory slots 使用多头自注意力，促进 slot 间交互并防止梯度坍缩。
    - **词汇重构损失**：将每个 slot 经 LLM 的 LM Head 和 softmax 得到 token 分布，再用 max pooling 聚合成 passage 级分布；以原 passage 中出现的 token 作为监督，计算负对数似然损失。
    - **辅助对齐损失**：
      - MSE 对齐：让转换后 memory slots 的平均表示接近原 passage 经 LLM 编码后的平均隐藏状态。
      - KL 对齐：让转换表示的词汇分布接近 LLM 对原始 passage 诱导的词汇分布。
    - 总损失为词汇重构、MSE、KL 三项等权相加。Stage 1 后冻结 converter。
  - **Stage 2：预训练 LLM**
    - 让目标 LLM 学会消费 memory slots。设计四个语言建模任务：
      - **SPR**：单 passage 重建，给定 memory slots 重建原文。
      - **NCP**：下一块预测，只从前半块构造 memory slots，预测后半块。
      - **CCR**：连续块重建，两个 chunk 各自编码为 memory slots，重建完整 passage。
      - **MPR**：多 passage 重建，采样两个不同 passage，各自构造 memory slots，重建拼接文本。
    - 总损失为四个任务损失之和。训练中按比例采样任务，早期以单 passage 任务为主，后期逐渐增加多 passage 任务比例。
  - **Stage 3：自蒸馏**
    - 每个问题搭配 5 个检索 passage，其中可能包含噪声或无关内容。
    - 不直接使用短 gold answer 做 SFT，而是用 vanilla RAG 基于原始文本 passage 生成的伪答案作为监督。
    - 目的：恢复 LLM 原生生成能力，同时让 memory slots 作为知识载体而非软提示。

## 3. 实验设计

- **模型与检索设置**：
  - 目标 LLM：Mistral-7B-Instruct-v0.2，使用 LoRA 微调。
  - 检索器：SPLADE-v3 检索 passage，因配置未明确而省略 rerank。
  - 预先构建检索索引，并用 SFR retriever 重新编码检索 passage，与 xRAG 设置对齐。
- **数据**：
  - 预训练：Wikipedia-KILT 中 2.5M passages。
  - 微调：MultiQA，包含 NQ、MS-MARCO、AdversarialQA、HotpotQA、WikiQA、SCIc、ASQA、TriviaQA、FreebaseQA、SQuAD。
  - 过滤：剔除 vanilla RAG 生成答案不包含标注 gold answer 的训练样本。
  - 评估：NQ、TriviaQA、HotpotQA、ASQA、PopQA。
- **评估指标**：
  - span exact match（spanEM），采用包含式匹配：若 gold answer 字符串作为连续片段出现在生成输出中，则判为正确。
- **对比方法**：
  - 上界参考：未压缩 RAG。
  - 下界参考：无上下文 LLM。
  - 压缩基线：AutoCompressor、ICAE、xRAG、PCC-lite、PISCO。
- **主要实验场景**：
  - 主实验：5 个 QA 数据集，ConvX 使用 16× 和 128× 压缩率。
  - 单 passage 设置：NQ、AdversarialQA，比较 relevant-only 与 top-1 检索场景。
  - 消融实验：移除 Stage 2、自蒸馏、Stage 1、Stage 1&2、压缩、上下文等。
  - 效率分析：GFLOPs 与压缩延迟对比。
  - 生成行为分析：答案长度对比。
  - 注意力分析：生成答案对输入 prompt 和 memory slots 的注意力权重。
  - 词汇分析：附录展示 memory slots 恢复的词汇信息。

## 4. 资源与算力

- 论文明确报告了训练算力：
  - **Stage 1 预训练 Converter**：28 GPU 小时，1× A6000 Pro 96 GB。
  - **Stage 2 预训练 LLM**：60 GPU 小时，1× A6000 Pro 96 GB。
  - **Stage 3 自蒸馏**：9 GPU 小时，1× A6000 Pro 96 GB。
- 总计约 **97 GPU 小时**，使用单卡 A6000 Pro 96 GB。
- 论文还给出了各阶段超参数，包括训练步数、学习率、batch size、LoRA 配置、最大 passage 长度等。
- 训练数据规模为 2.5M passages，模型 checkpoint 和部分数据/索引已公开。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 主实验覆盖 5 个评估数据集、2 种压缩率、5 个基线方法，以及 RAG 上界和 LLM 下界。
  - 单 passage 实验覆盖 2 个数据集，并区分 relevant-only 与 top-1 检索。
  - 消融实验包含约 7 种设置：完整 ConvX、LLM-Finetuned、w/o Stage 1、w/o Stage 2、w/o Stage 1 & 2、w/o Self-Distil、w/o Compression、w/o Context。
  - 额外分析包括效率、答案长度、注意力可视化、memory slots 词汇分析。
- **充分性评价**：
  - 实验覆盖面较广，从主性能、鲁棒性、消融、效率、可解释性多个角度验证方法。
  - 对比了代表性压缩方法和 RAG 上下界，评估指标与 prior work 对齐。
  - 论文公开代码、checkpoint、passage collection 和带检索

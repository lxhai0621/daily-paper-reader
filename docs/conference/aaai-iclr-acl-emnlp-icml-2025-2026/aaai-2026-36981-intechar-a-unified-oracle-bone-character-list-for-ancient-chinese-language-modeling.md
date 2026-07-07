---
title: "InteChar: A Unified Oracle Bone Character List for Ancient Chinese Language Modeling"
title_zh: InteChar：面向古代中文语言建模的统一甲骨文字符列表
authors: "Xiaolei Diao, Zhihan Zhou, Lida Shi, Ting Wang, Ruihua Qi, Daqian Shi, Hao Xu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/36981/40943"
tags: ["query:ancient-text"]
score: 9.0
evidence: 统一的甲骨文字符列表，支持古代中文语言建模
tldr: 古代文字语言模型训练面临样本稀缺和字符编码缺失的挑战，尤其针对中国早期文字如甲骨文。本文提出InteChar，一个统一且扩展的甲骨文字符列表，包含规范化编码，解决了数字化处理中的字符集问题。该资源支持了更有效的预训练，提升了古文字下游任务的性能，推动了中国古代文字的数字化转型。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 古代文字缺乏统一编码，样本稀少，阻碍语言模型训练。
method: 构建了标准化的甲骨文字符列表和编码方案，支持数字化处理。
result: 提供了首个统一甲骨文字符集，提升了古代中文语言模型的下游任务性能。
conclusion: InteChar为古代文字的数字化和计算处理奠定了字符集基础。
---

## Abstract
Constructing historical language models (LMs) plays a crucial role in aiding archaeological provenance studies and understanding ancient cultures. However, existing resources present major challenges for training effective LMs on historical texts. First, the scarcity of historical language samples renders unsupervised learning approaches based on large text corpora highly inefficient, hindering effective pre-training. Moreover, due to the considerable temporal gap and complex evolution of ancient scripts, the absence of comprehensive character encoding schemes limits the digitization and computational processing of ancient texts, particularly in early Chinese writing. To address these challenges, we introduce InteChar, a unified and extensible character list that integrates unencoded oracle bone characters with traditional and modern Chinese. InteChar enables consistent digitization and representation of historical texts, providing a foundation for robust modeling of ancient scripts. To evaluate the effectiveness of InteChar, we construct the Oracle Corpus Set (OracleCS), an ancient Chinese corpus that combines expert-annotated samples with LLM-assisted data augmentation, centered on Chinese oracle bone inscriptions. Extensive experiments show that models trained with InteChar on OracleCS achieve substantial improvements across various historical language understanding tasks, confirming the effectiveness of our approach and establishing a solid foundation for future research in ancient Chinese NLP.

---

## 论文详细总结（自动生成）

# InteChar: 面向古代中文语言建模的统一甲骨文字符列表 — 详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：古代文字（尤其是甲骨文）语料极其稀缺，且大量字符缺乏统一编码，导致传统语言模型难以有效预训练和用于下游任务。
- **研究动机**：现有资源仅覆盖编码字符，忽略了出土文献中大量未编码的甲骨文字，造成信息丢失；低资源环境下无监督预训练效率低下。
- **整体含义**：通过构建统一、可扩展的字符列表 InteChar 和配套语料库 OracleCS，为古代中文 NLP 提供数字基础设施，使模型能够学习完整的字符语义，提升历史语言理解能力。

## 2. 论文提出的方法论：核心思想与关键技术细节
- **核心思想**：将未编码的甲骨文字符与现代汉字统一编码，形成标准化的字符集；基于该字符集构建专家标注+LLM增强的语料库，用于训练和评估历史语言模型。
- **关键技术细节**：
  - **InteChar 构建（四阶段流程）**：
    1. 初始化：加载官方 Unicode CJK 字符集（>90,000字符）。
    2. 集成已编码字符：从中坚图书馆的多个历史字体集中筛选与语料库共现的甲骨文形，去除重复。
    3. 构建新字符：对语料中未编码的甲骨文，使用基于目标检测的部首识别方法（Diao et al. 2023a）自动检测部首，经专家验证、矢量化、分配内部码点。
    4. 专家校对：使用孪生网络检测重复字形，人工审核。最终 InteChar 共含 11,288 个字符。
  - **OracleCS 语料库构建**：
    - 核心：专家从考古资料和甲骨拓片中挑选高质量样本，包括已释读和未释读字符（均用 InteChar 编码）。
    - 扩充：引入先秦经典（论语、春秋等）；采用指令微调式的数据增强（包括句子翻译、同义替换、字形结构分析、语义预测等）。
    - 每个字符包含部首分解、语义注释（未释读字符留空）。

## 3. 实验设计
- **使用的数据集**：OracleCS 共 173,459 个样本，含 11,288 个独立字符；另有专门的任务子集（如 cloze 15,416 实例、检索 896 查询与 12,141 候选、翻译 15,868 训练/10,578 测试等）。
- **Benchmark 组成**：
  - **嵌入评估**（零样本）：
    - Cloze Completion on OBI：基于甲骨文句子的完形填空，度量 NDCG@k 和 MRR@k（k=10,20）。
    - Commentary-to-Text Retrieval：现代注释与经典原文的句子级检索，度量 NDCG@k 和 MRR@k（k=400,500）。
  - **微调评估**（参数高效微调 LoRA）：
    - Ancient Chinese Translation（句子级翻译）
    - Polysemous Word Matching（二分类，判断上下文中的词义是否匹配）
    - Word Parsing（字符级释义选择）
    - 均报告准确率。
- **对比方法**：10 个模型：BERT、Llama-3-8B、GPT-2、MiniRBT、guwenBERT-base、sikuBERT、Qwen-7B-Chat、GLM-4-9B、XunziALLM、TongGu-LLM。每个模型分别使用原始字符列表和 InteChar 进行训练/微调。

## 4. 资源与算力
- 论文明确说明：实验在 **8 块华为 Ascend-D910b NPU** 上，基于 Ubuntu 环境，使用 PyTorch 实现。
- **具体训练时长未提及**。嵌入训练 10 个 epoch，微调 10 个 epoch，使用 AdamW 优化器。
- 从“高性价比”角度看，算力描述基本透明，但缺少训练时间或总 FLOPs 的量化，无法直接复现计算开销。

## 5. 实验数量与充分性
- **实验组数**：共 2 大类（嵌入评估 + 微调评估），每类包含多个子任务（共 5 个子任务），每个子任务上 10 个模型×2 种字符列表 = 约 100 个实验点，结果表格完整清晰。
- **充分性**：
  - 覆盖从经典小模型（BERT）到当代大语言模型（Qwen-7B-Chat、GLM-4-9B）及专为古中文设计的模型（XunziALLM、TongGu-LLM）。
  - 嵌入评估验证了字符/句子表征能力；微调验证了任务特定适应能力。
  - 对比条件一致（相同 backbone 冻结或 LoRA 设置），公平性较好。
- **缺乏消融实验**：未单独分析 InteChar 中哪个组件贡献最大（如新构建字符 vs. 集成编码字符），也未分析 OracleCS 中数据增强的效果。

## 6. 论文的主要结论与发现
- **InteChar 显著提升所有模型在古文字理解任务上的表现**：
  - 嵌入评估：例如 GPT-2 的 MRR@10 从 0.168→0.534；Qwen-7B-Chat 的 NDCG@10 从 0.302→0.842。
  - 微调评估：所有模型在三个下游任务上准确率均提高（如 TongGu-LLM 平均准确率从 92.21%→92.92%）。
- 结论：统一编码后，模型能更有效地学习未编码字符的语义，弥补信息缺失，在零样本和微调场景均受益。
- **InteChar 为古代 NLP 提供了标准化基础**，具有可扩展性。

## 7. 优点
- **创新性**：首次系统性地为甲骨文等未编码字符构建统一 Unicode 兼容字符列表，填补了古文字数字化处理中的关键空白。
- **方法实用性**：半自动新字符构建流水线（基于部首识别→专家验证→矢量→编码）兼顾效率和领域知识，易于迁移到其他古文字。
- **基准全面**：评估涵盖嵌入质量（完形填空、检索）和下游任务（翻译、词义消歧、解析），覆盖不同粒度。
- **数据多样性**：OracleCS 融合专家标注与 LLM 增强，缓解低资源问题。
- **开源友好**：明确提供了 TrueType 字体文件（.ttf），且字符列表设计为可扩展。

## 8. 不足与局限
- **构建过程的定量验证不足**：新字符构建中的部首识别准确率未报告，依赖专家手动校正，自动化程度和扩展性尚不确定。
- **数据增强风险**：LLM 辅助增强可能引入噪声或语料漂移，论文未评估数据增强的单独贡献或质量控制。
- **覆盖范围有限**：仅聚焦甲骨文，对其他早期汉字（如金文、简帛文字）的集成未验证；此外，仅包含先秦经典，未覆盖后期文献。
- **计算成本高**：使用 8 块 NPU 资源，但未分析不同规模模型下的性价比；小模型可能受益有限。
- **评估局限性**：
  - 微调任务使用 LoRA，未与其他适应方法（如全参数微调）对比。
  - 未在真实考古/历史研究场景中验证（如协助释读未知字符）。
  - 缺乏跨语言泛化实验（例如其他古代文字如楔形文字）。

（完）

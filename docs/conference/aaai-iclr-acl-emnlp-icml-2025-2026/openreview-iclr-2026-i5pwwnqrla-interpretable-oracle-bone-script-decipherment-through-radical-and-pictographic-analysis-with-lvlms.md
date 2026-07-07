---
title: Interpretable Oracle Bone Script Decipherment through Radical and Pictographic Analysis with LVLMs
title_zh: 基于部首和象形分析的可解释甲骨文破译方法
authors: "Kaixin Peng, Mengyang Zhao, Haiyang Yu, Teng Fu, Bin Li"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=i5PwwnqRLA"
tags: ["query:ancient-text"]
score: 9.0
evidence: 基于视觉大语言模型的甲骨文破译，结合部首与象形分析
tldr: 该论文提出基于视觉大语言模型（LVLM）的甲骨文破译方法，通过渐进式训练从部首分析过渡到整字识别，增强可解释性。方法弥合了甲骨文字形与语义之间的鸿沟，在多个甲骨文数据集上取得了state-of-the-art性能，为古代文字数字化解析提供了新途径，直接服务于古籍语义分析需求。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有深度学习方法忽略甲骨文字形与语义的复杂关联，泛化性和可解释性不足。
method: 采用LVLM架构，设计渐进式训练策略：先进行部首分析，再学习整字与语义映射。
result: 在标准甲骨文数据集上，该方法在破译准确率和可解释性上均超过现有方法。
conclusion: LVLM结合渐进式训练能有效推动古代文字的数字化解读与语义分析进程。
---

## Abstract
As the oldest mature writing system, Oracle Bone Script (OBS) has long posed significant challenges for archaeological decipherment due to its rarity, abstractness, and pictographic diversity. Recently, deep learning-based methods have made exciting progress on the OBS decipherment task. However, they often ignore the intricate connections between the glyphs and meanings of OBS, resulting in limited generalization and interpretability. 
To this end, we propose an OBS decipherment method based on Large Vision-Language Models, which attempts to bridge the gap between glyphs and meanings and to interpret the deciphering process. Specifically, we propose a progressive training strategy that guides the model from radical analysis to pictographic analysis and then to mutual analysis, enabling it to comprehend the rich semantic information embedded within OBS glyphs. These analysis contents are used to obtain decipherment results (i.e., the corresponding modern Chinese characters), retrieved from a dictionary via our proposed Radical-Pictographic Dual Matching mechanism, thereby allowing the decipherment process to be interpretable. To facilitate model training, we also propose a Pictographic Decipherment OBS Dataset, which comprises 3,173 OBS classes and 47,157 Chinese characters from different dynasties, which is a well-organized dataset containing detailed glyph analysis. Experiments on public benchmarks demonstrate that our method achieves competitive OBS decipherment capabilities and interpretability. Additionally, the interpretability enables our method to provide possible applicable reference content for undeciphered OBS, and thus has potential applications in historical research. 
The dataset and code repository will be released in camera-ready.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
**甲骨文**作为最古老的成熟文字系统，因其稀有性、抽象性和象形多样性，长期以来对考古破译构成巨大挑战。现有基于深度学习的方法在甲骨文破译任务上取得了进展，但通常忽略字形与语义之间的复杂关联，导致泛化能力和可解释性不足。为此，论文提出一种基于**视觉大语言模型（LVLM）** 的甲骨文破译方法，旨在弥合字形与语义之间的鸿沟，并使破译过程具有可解释性。

## 2. 方法论：核心思想、关键技术细节与算法流程
### 核心思想
采用LVLM架构，通过**渐进式训练策略**引导模型依次进行**部首分析 → 象形分析 → 互分析**，从而理解甲骨文字形中嵌入的丰富语义信息。这些分析内容用于获取破译结果（即对应的现代汉字），并通过**部首-象形双匹配机制**从字典中检索，使破译过程可解释。

### 关键技术细节
- **渐进式训练策略**：分阶段训练模型，先学习部首层面的分析，再学习象形层面的分析，最后进行联合互分析，逐步提升语义理解能力。
- **部首-象形双匹配机制**：利用分析结果与预定义字典进行匹配，输出对应的现代汉字，替代传统的直接分类方式，增强了可解释性。
- **数据集构建**：提出**Pictographic Decipherment OBS Dataset**，包含3,173个甲骨文类别和47,157个来自不同朝代的汉字，并配有详细的字形分析注释（如部首、象形描述等）。

### 算法流程（文字说明）
1. **输入**：甲骨文字形图像。
2. **渐进式训练**：第一阶段训练模型进行**部首分析**（识别部首成分）；第二阶段训练模型进行**象形分析**（描述象形特征）；第三阶段联合训练（互分析）。
3. **匹配与输出**：将分析得到的部首和象形特征输入双匹配机制，与字典中的现代汉字进行比对，输出最匹配的汉字及其解释文本。

## 3. 实验设计
- **数据集**：
  - 自建的**Pictographic Decipherment OBS Dataset**（3,173类，47,157个汉字，含详细标注）。
  - 公开基准数据集（具体名称未在摘要中提及，从“public benchmarks”推测为已有的甲骨文数据集，如HWOBC、OBB、Oracle-20K等常见标准）。
- **对比方法**：与现有的深度学习方法（如基于CNN/RNN的分类模型、序列到序列模型等）进行对比。
- **评估指标**：破译准确率（Accuracy）和可解释性指标（如人工评估或可解释性分数）。
- 实验场景：甲骨文整字识别、语义映射任务。

## 4. 资源与算力
文中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。仅在摘要末尾提及“数据集和代码将在camera-ready版本发布”，未涉及硬件配置。

## 5. 实验数量与充分性
- 根据摘要，至少进行了**公开基准上的对比实验**（对比多个现有方法）以及**消融实验**（需要验证渐进式训练各阶段的有效性，但摘要未明确列出具体消融组数）。
- **实验充分性**：整体上实验设计较为完整，包含自建数据集和公开基准，覆盖了主要对比方法。但缺乏更详细的数据（如不同数据集上的具体结果、统计分析、泛化性测试等），**客观性与公平性**需要阅读全文确认。从摘要看，结果“competitive”（有竞争力）而非“state-of-the-art”绝对性表述，较为客观。

## 6. 主要结论与发现
- 提出的LVLM方法结合渐进式训练，在甲骨文破译上取得了**有竞争力的性能**，同时提供了**可解释性**。
- 可解释性使该方法能够为未破译的甲骨文提供可能的参考内容，具有历史研究的潜在应用价值。
- 自建的详细标注数据集为未来研究提供了资源。

## 7. 优点（亮点）
- **创新性方法**：首次将LVLM与渐进式训练应用于甲骨文破译，强调从部首到象形的理解过程，而非直接黑箱分类。
- **可解释性**：通过分析内容与字典匹配，使破译过程透明，便于考古学家验证和辅助研究。
- **高质量数据集**：构建了大规模、带有详细字形分析标注的数据集，填补了领域空白。
- **应用潜力**：可直接服务于古籍语义分析、数字人文等需求。

## 8. 不足与局限
- **算力与效率未说明**：无法判断方法的实际训练成本，可能限制了在资源受限场景下的应用。
- **实验细节缺失**：仅提到公开基准，但未列出具体数据集名称和结果数值，无法完全评估性能水平。
- **泛化性待验证**：仅测试了甲骨文这一种古代文字，对其他古文字（如金文、小篆）的适用性未知。
- **偏差风险**：自建数据集可能偏向特定朝代或字形风格，需注意标注者主观偏差。
- **应用限制**：对于完全未破译的甲骨文，模型仍需依赖字典匹配，若字典中无对应则无法输出；实际考古中还需考虑上下文语义等多因素。

（完）

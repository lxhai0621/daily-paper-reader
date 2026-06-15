---
title: A multi-agent system for spine MRI report generation from multi-sequence imaging
title_zh: 基于多序列影像的脊柱MRI报告生成多智能体系统
authors: "Xiao, Z., Yang, J., Sun, G., Zhang, H., Xu, H., Yao, Y., Miller, Z. D., King, W. E., Kanani, M. M., Andre, J. B., Chu, S., Zhang, M., Kinahan, P. E., Cross, N. M., Wang, S."
date: 2026-06-11
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.07.730703v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 基于基础模型的多智能体系统用于脊柱MRI报告生成
tldr: "脊柱MRI报告生成面临多序列数据整合和解释复杂的挑战。本文提出SpineAgent多智能体框架，基于预训练的DINOv3编码器和持续训练策略，从32,047名患者的453,683个MRI序列中学习患者级嵌入。在17种脊柱病症预测中平均AUROC提升10.8%，并支持病理定位、图像报告检索和端到端报告生成，经放射科专家评估达到领先性能。该框架通过分解报告任务为临床子任务，实现了准确、可解释且泛化性强的多序列脊柱MRI报告生成。"
source: biorxiv
selection_source: fresh_fetch
motivation: 脊柱MRI解读需整合多序列信息，现有方法难以有效结合多序列数据且保留序列特异性诊断信息。
method: 基于DINOv3预训练T1/T2编码器，通过持续训练学习序列合成器获取患者级嵌入，并构建37个专门智能体进行条件诊断、定位和检索，最终由医疗报告智能体生成报告。
result: "在17种病症预测中平均AUROC提升10.8%，跨制造商和跨队列泛化性强，且在病理定位和报告生成上经放射科评估达到领先水平。"
conclusion: SpineAgent通过持续训练和多智能体分解策略，实现了准确、可解释且泛化的多序列脊柱MRI报告生成。
---

## 摘要
脊柱病变是全球范围内疼痛和残疾的主要原因之一。脊柱磁共振成像（MRI）是临床评估的核心，但其解读仍然复杂且耗时，需要整合多个成像序列和解剖区域的信息。尽管自动化MRI分析近期取得进展，但有效结合多序列数据同时保留序列特异性诊断信息仍是一个开放挑战。

本文提出SpineAgent，一种基于多序列基础模型构建的脊柱MRI报告生成多智能体框架，该模型使用来自32,047名患者和453,683个MRI序列的常规临床数据（总计13,441,191张MRI切片）进行训练。为适应不同序列模式，我们首先基于DINOv3分别预训练两个编码器，分别处理T1和T2加权序列。然后引入持续训练策略，学习一个合成器，利用T1和T2编码器嵌入其他序列的图像，生成整合MRI序列中各种信号的患者级嵌入。利用这些嵌入，SpineAgent实现了最先进的性能，在17项脊柱状态预测任务中，平均AUROC比最佳竞争方法提高10.8%，并在跨厂商和跨队列评估中表现出强泛化能力。除分类外，SpineAgent通过识别与发现相关的切片和分割病理区域实现病理定位。它还支持多模态图像-报告检索，为可扩展和可解释的MRI报告生成奠定坚实基础。

我们进一步将这些经过验证的SpineAgent能力集成到37个专门智能体中，用于疾病诊断、病理区域定位和临床相似病例检索。最后，我们将它们的输出作为结构化标记纳入端到端训练的医学报告智能体，用于报告生成。通过自动评估指标和五位放射科专家的评估，SpineAgent在脊柱MRI报告生成方面取得了领先性能。

总之，SpineAgent引入了一种用于多序列脊柱MRI理解的持续训练方法。通过将报告生成分解为由专门智能体处理的临床基础子任务，SpineAgent框架能够实现准确、可解释且泛化的脊柱MRI报告，适用于多样化的成像序列和解剖区域。

## Abstract
Spinal pathology is a leading cause of pain and disability worldwide. Spine magnetic resonance imaging (MRI) is central to clinical evaluation, yet its interpretation remains complex and time-consuming, requiring integration of information across multiple imaging sequences and anatomical regions. Despite recent advances in automated MRI analysis, effectively combining multi-sequence data while preserving sequence-specific diagnostic information remains an open challenge.

Here we present SpineAgent, a multi-agent framework for spine MRI report generation built upon a multi-sequence foundation model trained on routine clinical data from 32,047 patients and 453,683 MRI series, comprising a total of 13,441,191 MRI slices. To accommodate diverse modalities of sequences, we first pre-train two DINOv3-based encoders separately on T1- and T2-weighted sequences. We then introduce a continual training strategy that learns a synthesizer to embed images of other sequences using the T1 and T2 encoders, producing patient-level embedding that integrates various signals across MRI sequences. Using these embeddings, SpineAgent achieves state-of-the-art performance, with mean 10.8% AUROC improvement across 17 spinal condition-prediction tasks compared to the best competing method, and demonstrates strong generalizability under cross-manufacturer and cross-cohort evaluation. Beyond classification, SpineAgent enables pathology localization by identifying findings-relevant slices and segmenting pathological regions. It also supports multimodal image-report retrieval, providing a solid foundation for scalable and explainable MRI report generation.

We further integrate these validated capabilities of SpineAgent into 37 specialized agents for condition diagnosis, pathological-region localization, and clinically-similar-cases retrieval. Finally, we incorporate their outputs as structured tokens within a Medical Report Agent trained end-to-end for report generation. Through both automated metrics and expert evaluation by five radiologists, SpineAgent achieves leading performance in spine MRI report generation.

Together, SpineAgent introduces a continual training approach for multi-sequence spine MRI understanding. By decomposing report generation into clinically grounded subtasks addressed by specialized agents, the SpineAgent framework enables accurate, interpretable and generalizable spine MRI reporting across diverse imaging sequences and anatomical regions.
---
title: "DOMINO: Learning Domain Co-occurrence for Multidomain Protein Design"
title_zh: DOMINO：学习结构域共现以进行多结构域蛋白质设计
authors: "Dai, F., Su, J., Tan, Q., Yang, H., Zhou, X., Yuan, F."
date: 2026-05-05
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.01.721929v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.5
evidence: 多领域蛋白质设计的对比检索模型
tldr: DOMINO是一个用于多结构域蛋白质设计的两阶段框架。它通过DOMIN模型学习结构域的共现规律并检索潜在配对，再利用DOMO模型生成包含特定结构域及其连接序列的完整蛋白质。该方法不仅能重现自然界的结构域组合，还能探索全新的组合空间。实验表明，DOMINO生成的500万个蛋白质具有高结构置信度和序列多样性，为蛋白质工程提供了高效的设计工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在解决自然界多结构域蛋白质组合空间稀疏的问题，通过学习结构域共现规律来设计新型蛋白质。
method: 提出由对比检索模型DOMIN和条件自回归序列模型DOMO组成的DOMINO框架，实现结构域匹配与全长序列生成。
result: 成功生成了500万个具有高AlphaFold预测置信度、多样化CATH标注且相对于UniRef100具有序列新颖性的蛋白质。
conclusion: 证明了结构域共现规律可作为有效的预测设计先验，为通过现有结构模块的新组合来探索多结构域蛋白质空间提供了可扩展策略。
---

## 摘要
多结构域蛋白质通过结构域的重用和重组产生，但自然界的架构仅代表了可能的结构域组合空间中稀疏且结构化的样本。在这里，我们介绍了 DOMINO，这是一个两阶段框架，它从 TED 注释的多结构域蛋白质中学习结构域共现，并利用学习到的模式生成新的多结构域序列。DOMIN 是一个对比检索模型，它将结构域嵌入到潜在的兼容性空间中，并从 TED 衍生的结构域池中为查询结构域检索候选伙伴，包括在 TED 衍生共现集中未观察到的配对。DOMO 是一个条件自回归序列模型，它通过联合生成指定的结构域区域以及它们之间和周围的非结构域序列上下文，将每个检索到的结构域对转换为全长蛋白质序列。DOMIN 恢复了自然结构域共现的分层模式，并利用候选的新配对扩展了观察到的 CATH 同源超家族共现网络。DOMO 将留出的自然配对和 DOMIN 检索到的配对都实现为具有高结构域恢复率和高 AlphaFold 预测结构置信度的蛋白质。大规模应用下，DOMINO 生成了 500 万个检索衍生的多结构域蛋白质，采样设计显示出对指定结构域的恢复、多样化的 CATH 注释以及相对于 UniRef100 的序列新颖性。总之，这些结果支持将结构域共现作为一种预测性设计先验，并展示了一种通过现有结构模块的新组合来探索多结构域蛋白质架构的可扩展策略。

## Abstract
Multidomain proteins arise through the reuse and recombination of structural domains, yet natural architectures represent a sparse, structured sample of the possible domain-combination space. Here, we introduce DOMINO, a two-stage framework that learns domain co-occurrence from TED-annotated multidomain proteins and uses the learned patterns to generate new multidomain sequences. DOMIN, a contrastive retrieval model, embeds domains into a latent compatibility space and retrieves candidate partners for a query domain from a TED-derived domain pool, including pairings not observed in the TED-derived co-occurrence set. DOMO, a conditional autoregressive sequence model, converts each retrieved domain pair into a full-length protein sequence by jointly generating the specified domain regions and the non-domain sequence context between and around them. DOMIN recovers hierarchical patterns of natural domain co-occurrence and expands the observed CATH homologous-superfamily co-occurrence network with candidate novel pairings. DOMO realizes both held-out natural pairs and DOMIN-retrieved pairs as proteins with high domain recovery and high AlphaFold-predicted structural confidence. Applied at scale, DOMINO generated 5 million retrieval-derived multidomain proteins, with sampled designs showing recovery of the specified domains, diverse CATH annotations, and sequence novelty relative to UniRef100. Together, these results support domain co-occurrence as a predictive design prior and demonstrate a scalable strategy for exploring multidomain protein architectures through new combinations of existing structural modules.
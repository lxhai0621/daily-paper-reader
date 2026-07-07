---
title: Document Segmentation Matters for Retrieval-Augmented Generation
title_zh: 文档分段对检索增强生成至关重要
authors: "Zhitong Wang, Cheng Gao, Chaojun Xiao, Yufei Huang, Shuzheng Si, Kangyang Luo, Yuzhuo Bai, Wenhao Li, Tangjian Duan, Chuancheng Lv, Guoshan Lu, Gang Chen, Fanchao Qi, Maosong Sun"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.422.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: RAG文档分块方法
tldr: 针对检索增强生成（RAG）中文档分段这一关键但常被忽视的问题，现有规则或语义方法存在上下文不连贯或成本过高缺陷。本文提出PIC方法，利用文档摘要作为伪指令指导分块，通过计算句子与摘要的语义相似度实现自适应分组。实验表明PIC在多个RAG基准上提升检索和生成质量，为RAG系统提供了一种简单有效的预处理优化手段。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.422/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1627, \"height\": 728, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.422/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 776, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.422/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1649, \"height\": 509, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 763, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1645, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 457, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 588, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 497, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 775, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 774, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1668, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.422/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1666, \"height\": 623, \"label\": \"Table\"}]"
motivation: 现有RAG中文档分块方法导致上下文不连贯或信息冗余，影响生成质量。
method: 提出PIC方法，利用文档摘要作为伪指令，通过语义相似度自适应分组相关句子。
result: 在多个RAG基准上，PIC显著提升了检索准确性和生成质量。
conclusion: 文档分段是RAG的关键环节，PIC提供了一种低成本、高效的分块方案。
---

## Abstract
Retrieval-augmented generation (RAG) enhances large language models (LLMs) by integrating external knowledge. A critical yet underexplored challenge in RAG is document segmentation, also known as document chunking. Existing widely-used rule-based chunking methods usually lead to suboptimal splits, where overly large chunks introduce irrelevant information and small chunks lack semantic coherence. Existing semantic-based approaches either require costly LLM calls or fail to adaptively group contextually related sentences. To address these limitations, we propose PIC, Pseudo-Instruction for document Chunking), a simple yet effective method that leverages document summaries as pseudo-instructions to guide chunking. By computing semantic similarity between sentences and the summary, PIC dynamically groups sentences into chunks that align with the document’s key themes, ensuring semantic completeness and relevance to potential user instructions. Experiments on multiple open-domain question-answering benchmarks demonstrate that PIC can significantly improve retrieval accuracy (Hits@k) and end-to-end QA performance (Exact Match) without any additional training.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）
- 检索增强生成（RAG）通过整合外部知识提升大语言模型（LLM）的响应质量，但文档分割（chunking）这一基础环节长期被忽视。
- 现有方法存在明显缺陷：
  - 规则方法（固定长度、段落）导致语义不完整或引入无关信息。
  - 语义方法要么成本高昂（需多次调用大模型），要么无法自适应地将相关句子归组。
- 论文旨在设计一种无需训练、低成本且能保证语义连贯性的文档分块方法，从而提升RAG的检索精度和最终生成质量。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：利用文档摘要作为“伪指令”（Pseudo‑Instruction），通过计算每个句子与该摘要的语义相似度，动态地将相邻句子分组为块。摘要代表了文档的核心主题，与潜在用户指令分布相近。
- **关键技术细节**：
  1. **生成伪指令**：使用LLM（GPT‑4o‑mini）为每个文档生成简洁、信息丰富的摘要。
  2. **计算相似度**：用嵌入模型（bge‑large‑en‑v1.5）编码摘要和所有句子，计算每个句子与摘要的余弦相似度 $r_i$。
  3. **动态阈值**：以文档内所有句子相似度的均值 $\mu$ 作为阈值（实验证明最优）。
  4. **分块规则**：
     - 连续句子相似度均 $\geq \mu$ 的归为“相关块”（Crel）；
     - 连续句子相似度均 $< \mu$ 的归为“不相关块”（Cirr）；
     - 最终块集合 $C = C_{\text{rel}} + C_{\text{irr}}$。
- 该算法无需模型重训练，仅需一次摘要生成和一次嵌入相似度计算，计算开销远低于多次LLM调用的语义方法。

## 3. 实验设计
- **知识库**：最新英文Wikipedia dump（2024‑12‑01），约600万文档，经WikiExtractor提取清洗。
- **基准数据集（6个OpenQA）**：Natural Questions (NQ)、TriviaQA、WebQuestions (WebQ)、SQuAD、EntityQuestions (EQ)、PopQA。
- **对比方法**：
  - 规则方法：Sentence（逐句）、Paragraph（逐段）、Fixed‑size（固定100词，保留句子边界）。
  - 语义方法：Semantic（基于相邻句子相似度低点切分）。
  - 生成方法：Proposition（将文本重写为自包含的原子命题）。
- **评估指标**：
  - 检索性能：Hits@k（Top‑5和Top‑20）。
  - 端到端QA性能：Exact Match (EM)，分别使用Qwen2.5‑7B‑Instruct和Meta‑Llama‑3‑8B‑Instruct作为生成模型。
- **检索器**：bge‑large‑en‑v1.5，同时也是分块阶段的嵌入模型。

## 4. 资源与算力
- 论文未明确报告使用的GPU型号、数量或训练时长。
- 方法本身**无需训练**（zero‑shot），主要计算开销来自：
  - 摘要生成：调用GPT‑4o‑mini（云端API），需处理全部600万文档；
  - 嵌入计算：单次前向传播，可用CPU/GPU快速完成。
- 文中未提及摘要生成的具体时间或成本。

## 5. 实验数量与充分性
- **主要实验**：
  - 检索性能：6个数据集 × 2个k值（Top‑5/20）→ 12组结果（表1）。
  - QA性能：6个数据集 × 2个LLM × 2个k值 → 24组结果（表2）。
- **消融与深入分析**：
  - 伪指令类型影响（表3）：Random、Sent（随机句子）、Mean（句子嵌入均值）与完整PIC对比。
  - 阈值影响（图2）：5个阈值（μ±2σ区间）下的检索和QA性能。
  - 真实指令分块（RIC）对比（表4）：在NQ和Qasper上测试。
  - 块长度分布统计（图3、表6）。
  - 检索块中相关块比例分析（表5）。
- **充分性评价**：实验设计较为全面，覆盖了不同数据集、不同LLM、多个基线以及核心消融变体。结果客观（报告了多次重复? 未明确，但通常为单次或固定随机种子）。公平：检索器、生成模型、评估流程完全一致。

## 6. 主要结论与发现
- PIC在6个数据集的平均检索Hits@k和QA Exact Match上均**超越所有基线**。
- 检索性能：平均Top‑5 Hits@k为58.4%，Top‑20为69.5%，优于Proposition（57.7/68.9）和Semantic（56.0/67.4）。
- QA性能：以Qwen2.5‑7B为例，平均Top‑5 EM为49.9%，Top‑20为52.5%，相比Proposition提升约2个百分点；使用Llama‑3时也有类似提升。
- **伪指令的必要性**：使用文档摘要作为伪指令比随机摘要、随机句子或句子嵌入均值更有效（表3）。
- **动态阈值最优**：平均相似度μ作为阈值显著优于其他固定或偏移阈值（图2）。
- **相关块更易检索**：在PIC分块中，相关块占检索结果的大多数（>50%），尤其在实体密集数据集（EQ、PopQA）中几乎覆盖所有黄金块。
- 真实指令分块（RIC）可达到更高性能，但PIC在未知指令分布下已接近最优。

## 7. 优点
- **简单高效**：无需模型重训练，仅需一次摘要生成和一次相似度计算，计算成本低。
- **即插即用**：产生的PICWiki数据集可直接替换现有RAG知识库，提升性能。
- **新颖视角**：用文档摘要作为“伪指令”来模拟用户查询分布，将分块问题转化为与主题相关性的自适应聚类。
- **全面实验**：覆盖6个基准、2种LLM、多种基线，消融分析充分，结论可靠。
- **开源贡献**：公开PICWiki数据集和代码（论文中承诺）以促进社区研究。

## 8. 不足与局限
- **摘要生成开销**：虽低于多次LLM调用，但仍需为每个文档生成摘要，在处理超大规模语料时可能耗时。
- **依赖摘要质量**：若摘要不够准确或遗漏重要内容，分块效果会下降。
- **实验范围有限**：仅评估通用领域的开放域QA，未涉及专业领域（法律、医疗）或需要跨文档推理的场景。
- **未验证长文档处理**：Wikipedia文档长度中等，对于超长文档（如书籍）的效果未知。
- **偏差风险**：摘要生成使用GPT‑4o‑mini，可能引入模型固有偏见；仅用一种检索器（bge‑large‑en‑v1.5），未见对不同嵌入模型的鲁棒性分析。
- **可重复性**：未提供摘要生成的完整计算资源消耗（如API调用数、耗时），可能影响复现成本评估。

（完）

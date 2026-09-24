---
title: "Scaling Beyond Context: A Survey of Multimodal Retrieval-Augmented Generation for Document Understanding"
title_zh: 超越上下文扩展：面向文档理解的多模态检索增强生成综述
authors: "Sensen Gao, Shanshan Zhao, Xu Jiang, Lunhao Duan, Yong Xien Chng, Qing-Guo Chen, Weihua Luo, Kaifu Zhang, Jia-Wang Bian, Mingming Gong"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.204.pdf"
tags: ["query:mmkqa"]
score: 8.0
evidence: 面向文档理解的多模态RAG综述
tldr: 文档理解中的OCR管线与原生多模态大模型各有局限，前者丢失结构细节，后者难以建模长上下文，而文档的多模态特性需要更先进的检索范式。本文系统综述了面向文档理解的多模态检索增强生成，梳理文本、表格、图表与布局的联合检索与推理方法。综述为该领域提供了统一视角与分类框架，指出跨模态检索与上下文建模的关键挑战与未来方向。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 611, \"height\": 696}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 611, \"height\": 647}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-003.webp\", \"caption\": \"\", \"page\": 1, \"index\": 3, \"width\": 614, \"height\": 675}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-004.webp\", \"caption\": \"\", \"page\": 1, \"index\": 4, \"width\": 5433, \"height\": 2173}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-005.webp\", \"caption\": \"\", \"page\": 5, \"index\": 5, \"width\": 1207, \"height\": 769}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-006.webp\", \"caption\": \"\", \"page\": 5, \"index\": 6, \"width\": 1210, \"height\": 772}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-007.webp\", \"caption\": \"\", \"page\": 5, \"index\": 7, \"width\": 417, \"height\": 566}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-008.webp\", \"caption\": \"\", \"page\": 5, \"index\": 8, \"width\": 1035, \"height\": 657}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-009.webp\", \"caption\": \"\", \"page\": 5, \"index\": 9, \"width\": 1025, \"height\": 647}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-010.webp\", \"caption\": \"\", \"page\": 5, \"index\": 10, \"width\": 609, \"height\": 662}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-011.webp\", \"caption\": \"\", \"page\": 5, \"index\": 11, \"width\": 1270, \"height\": 1170}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-012.webp\", \"caption\": \"\", \"page\": 5, \"index\": 12, \"width\": 466, \"height\": 494}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-013.webp\", \"caption\": \"\", \"page\": 5, \"index\": 13, \"width\": 427, \"height\": 567}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-014.webp\", \"caption\": \"\", \"page\": 7, \"index\": 14, \"width\": 461, \"height\": 562}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-015.webp\", \"caption\": \"\", \"page\": 7, \"index\": 15, \"width\": 455, \"height\": 585}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-016.webp\", \"caption\": \"\", \"page\": 7, \"index\": 16, \"width\": 431, \"height\": 577}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-017.webp\", \"caption\": \"\", \"page\": 7, \"index\": 17, \"width\": 434, \"height\": 590}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-018.webp\", \"caption\": \"\", \"page\": 7, \"index\": 18, \"width\": 445, \"height\": 577}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long204/fig-019.webp\", \"caption\": \"\", \"page\": 7, \"index\": 19, \"width\": 447, \"height\": 571}]"
motivation: OCR管线丢结构、多模态大模型难建模上下文，文档多模态特性呼唤更先进的检索范式。
method: 系统综述面向文档理解的多模态RAG，梳理文本、表格、图表与布局的联合检索与推理。
result: 提出统一视角与分类框架，归纳跨模态检索与上下文建模的关键挑战。
conclusion: 为多模态检索增强生成的后续研究指明方向。
---

## Abstract
Document understanding is critical for applications from financial analysis to scientific discovery. Current approaches, whether OCR-based pipelines feeding Large Language Models (LLMs) or native Multimodal LLMs (MLLMs), face key limitations: the former loses structural detail, while the latter struggles with context modeling. Retrieval-Augmented Generation (RAG) helps ground models in external data, but documents’ multimodal nature, i.e., combining text, tables, charts, and layout, demands a more advanced paradigm: Multimodal RAG. This approach enables holistic retrieval and reasoning across all modalities, unlocking comprehensive document intelligence. Recognizing its importance, this paper presents a systematic survey of Multimodal RAG for document understanding. We propose a taxonomy based on domain, retrieval modality, and granularity, and review advances involving graph structures and agentic frameworks. We also summarize key datasets, benchmarks, and applications, and highlight open challenges in efficiency, fine-grained representation, and robustness, providing a roadmap for future progress in document AI.

---

## 论文详细总结（自动生成）

## 一、论文的核心问题与整体含义（研究动机与背景）

- **研究背景**：文档理解在金融分析、科学发现等场景中至关重要。当前主流方案存在两条路线：
  - **OCR 管线 + LLM**：依赖 OCR 提取文本再送入大语言模型，优点是文本精度较高，但会丢失版面结构、表格关系、图表语义等视觉信息。
  - **原生多模态大模型（MLLM）**：将文档作为图像序列统一建模，能保留视觉结构，但在数百至数千页的长文档场景下受限于上下文窗口，检索准确率下降且幻觉风险上升。
- **核心矛盾**：文档天然是多模态的，包含文本、表格、图表、版式布局等异构信息。单纯文本 RAG 或纯视觉 RAG 都难以同时兼顾结构保真与细粒度语义。
- **论文主张**：需要一种更先进的范式——**面向文档理解的多模态检索增强生成（Multimodal RAG）**，实现跨模态的整体检索与推理。
- **研究缺口**：
  - 已有 RAG 综述多聚焦文本 RAG，对多模态 RAG 覆盖有限。
  - 已有文档理解综述又很少系统讨论多模态 RAG。
  - 本文自称是**第一篇明确连接“多模态 RAG”与“文档理解”的系统性综述**。
- **整体含义**：论文试图为文档 AI 提供一个统一分类框架，梳理方法、数据集、评测指标、应用与工业部署，并指出未来方向。

## 二、论文提出的方法论

> 注意：本文是综述论文，不提出新的模型或算法，其“方法论”体现在**分类体系、问题形式化和方法归纳**上。

### 2.1 问题形式化

- 将 RAG 定义为：给定查询 \(q\)，从候选文档池 \(D=\{d_i\}_{i=1}^N\) 中检索相关页面，再以检索结果为条件生成答案。
- 每个文档 \(d_i\) 可包含页面图像和 OCR 文本 \(T_i\)。
- 使用模态特定编码器映射到共享嵌入空间：
  - 图像编码：\(z_i^{img}=Enc^{img}(d_i)\)
  - 文本编码：\(z_i^{text}=Enc^{text}(T_i)\)
  - 查询编码：\(e_q^{text}=Enc^{text}(q)\)
- 相似度用内积计算，可选单位归一化后等价于余弦相似度。

### 2.2 检索策略

- **纯视觉检索**：仅用图像通道打分 \(s^{img}(e_q,z_i)\)，按阈值或 Top-K 选择页面。
- **联合视觉—文本检索**，两种主流策略：
  - **置信度加权分数融合**：\(s^{conf}=\lambda_i s^{img}+(1-\lambda_i)s^{text}\)，其中 \(\lambda_i\) 表示图像置信度，\(\lambda_i=1\) 退化为纯视觉，\(\lambda_i=0\) 退化为纯文本。
  - **模态并集检索**：分别按图像和文本检索，再取并集，可选去重或 Borda、RRF 等排名融合。
- **生成阶段**：生成器 \(G\) 以原始查询和检索上下文 \(X\) 为条件生成最终回答：\(r=G(q,X)\)。

### 2.3 分类体系

论文从四个维度组织现有方法：

- **领域开放性**：
  - 开放域：从大规模文档库跨文档检索。
  - 闭域：仅针对单篇长文档检索最相关页面或片段。
- **检索模态**：
  - 图像模态：将页面作为图像编码，代表方法如 ColPali、VisRAG、DSE。
  - 图像+文本模态：结合 OCR 文本或 MLLM 生成摘要，代表方法如 VisDoMRAG、HM-RAG、ViDoRAG、PREMIR。
- **检索粒度**：
  - 页面级：整页作为原子检索单元。
  - 元素级：表格、图表、图像、文本块、区域等更细粒度。
  - 代表方法：VRAG-RL、MG-RAG、MMRAG-DocQA、mKG-RAG、RegionRAG、HKRAG、Snappy 等。
- **混合增强**：
  - 图结构增强：将多模态内容表示为图，节点为页面/文本片段/图像/表格/版面块，边表示语义、空间、上下文关系。
  - 智能体增强：用自主 agent 进行查询分解、检索策略选择、证据验证与融合。

### 2.4 训练损失归纳

- 多模态 RAG 常用 **ColBERT 式晚期交互 + 对比学习**。
- 查询和文档表示为多 token 嵌入 \(H_q\)、\(H_d\)，相似度为：
  - \(\text{Sim}(q,d)=\sum_{t=1}^{L_q}\max_{1\le m\le L_d}\langle h_{q,t},h_{d,m}\rangle\)
- 训练时对 batch 内查询—文档对使用对比损失：
  - \(\mathcal{L}=-\frac{1}{B}\sum_{i=1}^B \log\frac{\exp(p_i)}{\exp(p_i)+\exp(n_i)}\)
  - 其中 \(p_i\) 为正样本相似度，\(n_i\) 为最难负样本相似度。

### 2.5 评测指标归纳

- **检索评测**：Top-K Accuracy、Recall@K、Precision@K、F1@K、MRR@K、nDCG@K。
- **生成评测**：
  - 软匹配：BLEU、ROUGE、METEOR。
  - 严格匹配：EM、ANLS、PNLS、AccANLS。
  - 语义匹配：BERTScore、RoBERTa、G-Acc。

## 三、实验设计

> 本文为综述，不开展原创实验，而是汇总并对比已有方法在公开 benchmark 上的结果。

### 3.1 数据集与 Benchmark

- 论文汇总了 20 余个广泛使用的多模态文档理解数据集与基准，例如：
  - **DocVQA**：UCSF 行业文档集合上的 VQA。
  - **InfoVQA**：信息图问答。
  - **SlideVQA**：多页幻灯片问答。
  - **ChartQA**：图表逻辑与算术推理。
  - **TAT-DQA**：金融报告中的表格+文本数值推理。
  - **DUDE**：多行业、多领域视觉丰富文档。
  - **MMLongBench-Doc**：长上下文多模态文档基准。
  - **M3DocVQA**：开放域多页 PDF 多跳推理。
  - **VisDoMBench**：跨文档、多模态元素推理。
  - **OpenDocVQA**：开放域视觉丰富文档检索与 QA。
  - **ViDoSeek**：大规模视觉丰富文档 RAG 评测。
  - **UniDoc-Bench**：统一文档中心 MM-RAG 基准。
  - **BBox-DocVQA**：带边界框定位的 DocVQA。
- 论文指出当前多模态 RAG benchmark 规模可达 **20K–200K 页面、20M–200M 视觉 token**，远超现有 MLLM 的 128K–1M 上下文限制。

### 3.2 对比方法

- 论文在表 4 中汇总了多类方法在 DocVQA、SlideVQA、InfoVQA、MMLongBench-Doc 等基准上的结果。
- 涉及的代表方法包括：
  - **检索评测**：SV-RAG、DSE、VisRAG、CMRAG、RegionRAG、LILaC、ColPali、ColQwen2、VDocRAG、Light-ColPali、HKRAG 等。
  - **生成评测**：VisRAG、FRAG、LILaC、SV-RAG、CREAM、M3DocRAG、VisDoMRAG、VDocRAG、ReDocRAG、VRAG-RL、SimpleDoc、MMRAG-DocQA、CMRAG、MoLoRAG、RECON、LAD-RAG、DREAM、MARA、SLEUTH 等。
- 评测指标按方法实际采用指标标注，并尽量对齐可比较指标。

### 3.3 评测维度

- **检索评测**：关注页面或元素检索准确性，使用 Top-5、R@10、MRR@10、nDCG@5、nDCG@10 等。
- **生成评测**：关注在检索上下文条件下答案正确性，使用 EM、ANLS、PNLS、G-Acc 等。

## 四、资源与算力

- **论文未明确报告自身使用的 GPU 型号、数量、训练时长或总计算量**。
- 作为综述论文，本文不训练新模型，也不进行大规模实验，因此没有传统意义上的算力开销说明。
- 文中提到的效率问题主要针对被综述方法：
  - 当前多模态 RAG benchmark 需要 20–200M 视觉 token。
  - 现有 MLLM 上下文窗口通常为 128K–1M。
  - 工业部署中存储密集视觉嵌入会带来内存和检索延迟瓶颈。
- 但论文没有给出统一的算力统计表或能耗分析。

## 五、实验数量与充分性

- **实验数量**：
  - 本文不是实验型论文，没有自己的消融实验或训练实验。
  - 主要“实验性内容”是表 4 中汇总的多方法、多基准评测结果，覆盖 DocVQA、SlideVQA、InfoVQA、MMLongBench-Doc 四个主要基准。
  - 表 2 系统对比了约 40 余种方法，维度包括领域、模态、粒度、图结构、智能体、是否训练、是否使用 OCR 等。
  - 表 7 和表 8 总结了各方法的核心贡献。
- **充分性**：
  - 作为综述，覆盖范围较广，方法分类细致，数据集与指标梳理较完整。
  - 但汇总结果来自不同论文，实验设置、backbone、训练数据、评测协议不完全一致，**横向对比的公平性有限**。
  - 论文也承认不同方法采用不同指标，只能“尽量对齐可比指标”。
- **客观性**：
  - 优点：明确区分检索评测与生成评测，并标注指标差异。
  - 局限：未进行统一复现实验，未控制变量，因此不能视为严格公平的 benchmark 比较。
- **是否充分**：
  - 对综述目标而言，文献覆盖较充分。
  - 对“方法优劣的因果判断”而言，证据仍不充分。

## 六、论文的主要结论与发现

- 多模态 RAG 是文档理解从“文本中心”走向“视觉—文本联合”的关键范式。
- 当前研究呈现以下趋势：
  - 从 OCR 文本 RAG 转向图像或图像+文本混合检索。
  - 从页面级检索转向元素级、区域级、布局感知的细粒度检索。
  - 从单轮 retrieve-then-read 转向图结构索引和智能体协作。
- 主要挑战集中在：
  - **效率**：视觉 token 数量巨大，存储与检索成本高。
  - **细粒度表示**：页面级建模忽略表格、图表、脚注、版面语义。
  - **鲁棒性与安全**：跨模态攻击面、知识投毒、幻觉、数据泄露、来源验证不足。
  - **评测有效性**：现有 benchmark 易饱和、可能存在数据污染，且与真实大规模开放域 RAG 场景存在错位。
- 工业部署方面：
  - 开源框架如 RAGFlow、LlamaIndex、RAG-Anything、LightRAG、AutoRAG、RAGLite 降低了部署门槛。
  - 但检索质量与领域专家预期对齐、数据治理、访问控制、可审计性、错误归因仍是开放问题。
- 论文最终呼吁：
  - 发展更高效的视觉嵌入压缩与分层检索。
  - 设计层次化、可定位视觉证据的评测协议。
  - 引入隐私保护检索、可验证生成和风险感知信任校准。

## 七、优点

- **定位清晰**：首次系统连接“多模态 RAG”与“文档理解”，填补了两类综述之间的空白。
- **分类体系完整**：从领域开放性、检索模态、检索粒度、图结构、智能体五个维度组织文献，结构清晰。
- **问题形式化规范**：用统一符号定义检索、融合与生成流程，便于比较不同方法。
- **覆盖范围广**：汇总 40 余种方法、20 余个数据集与 benchmark，并整理核心贡献表。
- **指标梳理细致**：区分检索指标与生成指标，并给出 Top-K、Recall、MRR、nDCG、EM、ANLS、PNLS、G-Acc 等公式。
- **兼顾学术与工业**：不仅讨论模型方法，还分析工业部署、开源工具、效率权衡与数据治理。
- **批判性分析较强**：指出 OCR-free 与 OCR-based 的悖论、benchmark 饱和与污染风险、复杂度—性能权衡问题。

## 八、不足与局限

- **无原创实验**：作为综述，没有提出新方法，也没有统一复现或控制变量实验，无法直接验证各方法优劣。
- **横向比较公平性有限**：表 4 结果来自不同论文，backbone、训练数据、评测设置不一致，指标也不完全统一。
- **算力与成本分析缺失**：未系统统计各方法的训练/推理成本、GPU 资源、延迟和能耗。
- **工业部署讨论偏初步**：论文自述对用户中心评测、系统集成、部署可扩展性等分析仍较初步。
- **数据质量与跨域迁移分析不足**：虽汇总数据集，但对标注一致性、数据质量、跨域泛化、评测对齐缺乏深入量化。
- **领域快速变化**：多模态 RAG 发展迅速，新数据集、新模型和新评测协议可能迅速改变结论，综述存在时效性局限。
- **安全与伦理仅概括**：提到偏见、幻觉、跨模态攻击和知识投毒，但未展开系统性防御方案评估。
- **应用限制**：
  - 高资源消耗限制实时工业部署。
  - 长文档、多页、跨文档场景仍受上下文和检索精度约束。
  - 高风险领域需额外验证来源、权限与合规性。

（完）

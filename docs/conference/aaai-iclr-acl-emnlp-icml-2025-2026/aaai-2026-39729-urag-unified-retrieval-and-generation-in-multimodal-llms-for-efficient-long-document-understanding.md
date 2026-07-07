---
title: "URaG: Unified Retrieval and Generation in Multimodal LLMs for Efficient Long Document Understanding"
title_zh: URaG：多模态大语言模型中统一检索与生成的高效长文档理解
authors: "Yongxin Shi, Jiapeng Wang, Zeyu Shan, Dezhi Peng, Zening Lin, Lianwen Jin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39729/43690"
tags: ["query:ma-kf"]
score: 7.0
evidence: 长文档理解中的检索与生成
tldr: 该论文针对多模态大模型处理长文档时信息干扰和二次计算成本的问题，提出URaG框架。通过将检索和生成统一在端到端训练中，利用早期层粗略关注、深层聚焦相关的类人推理模式，实现高效长文档理解。实验表明URaG在减少计算开销的同时提升了长文档问答的准确性，避免了外部检索器带来的复杂性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多模态大模型处理长文档面临信息干扰和二次计算开销。
method: 设计统一检索与生成框架，利用注意力分布的类人粗细推理模式。
result: 在长文档基准上，URaG以更少计算量取得更优或相当的性能。
conclusion: 端到端的统一检索和生成是提升长文档理解效率的有效途径。
---

## Abstract
Recent multimodal large language models (MLLMs) still struggle with long document understanding due to two fundamental challenges: information interference from abundant irrelevant content, and the quadratic computational cost of Transformer-based architectures. Existing approaches primarily fall into two categories: token compression, which sacrifices fine-grained details; and introducing external retrievers, which increase system complexity and prevent end-to-end optimization. To address these issues, we conduct an in-depth analysis and observe that MLLMs exhibit a human-like coarse-to-fine reasoning pattern: early Transformer layers attend broadly across the document, while deeper layers focus on relevant evidence pages. Motivated by this insight, we posit that the inherent evidence localization capabilities of MLLMs can be explicitly leveraged to perform retrieval during the reasoning process, facilitating efficient long document understanding. To this end, we propose URaG, a simple-yet-effective framework that Unifies Retrieval and Generation within a single MLLM. URaG introduces a lightweight cross-modal retrieval module that converts the early Transformer layers into an efficient evidence selector, identifying and preserving the most relevant pages while discarding irrelevant content. This design enables the deeper layers to concentrate computational resources on pertinent information, improving both accuracy and efficiency. Extensive experiments demonstrate that URaG achieves state-of-the-art performance while reducing computational overhead by 44-56%.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：多模态大语言模型（MLLMs）在处理长文档时面临两大挑战：  
  - **信息干扰**：大量无关内容稀释了与问题相关的信息。  
  - **二次计算成本**：Transformer 架构对序列长度的二次复杂度导致计算开销过高。  
- **现有解决方案的不足**：  
  - **令牌压缩**（如 mPLUG-DocOwl2）会牺牲细粒度视觉细节。  
  - **引入外部检索器**（如 SV-RAG、M3DocRAG）增加了系统复杂度，且检索器与 MLLM 分离无法端到端优化，易导致次优协同和错误传播。  
- **论文动机**：通过对 MLLM 注意力分布的分析，发现其呈现“粗到细”的类人推理模式——早期层均匀关注所有页面，深层聚焦证据页面。据此提出将这种内在的证据定位能力显式用于检索，实现统一检索与生成。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：在单个 MLLM 内统一检索与生成，利用早期 Transformer 层的表征进行证据选择，过滤无关内容，让深层层专注于推理。  
- **关键组件**：  
  - **跨模态检索模块**：由两个线性层 + GELU 激活组成（参数量仅占模型总参数的 0.05%~0.07%）。  
  - 从 LLM 第 6 层的隐藏状态中提取每页的视觉特征序列 \(E_v^{(p)}\) 和查询文本特征序列 \(E_q\)。  
  - **上下文延迟交互**（late interaction）计算相似度：  
    \[
    s_{q,v}(p) = \sum_{i \in [|E_q|]} \max_{j \in [|E_v^{(p)}|]} (E_{q_i} \cdot E_{v_j}^{(p)T})
    \]  
  - 根据相似度保留 top-k（默认 k=5）页面，丢弃其余页面的视觉令牌。  
- **训练策略**（两阶段）：  
  1. **检索预训练**：仅训练检索模块，使用检索损失 \(L_{\text{retrieval}} = \log(1 + \exp(S_{\text{neg}} - S_{\text{pos}}))\)。  
  2. **联合微调**：引入 LoRA 适配器（rank=32, alpha=64, dropout=0.1），联合优化检索损失和生成损失（交叉熵）。  
- **实现细节**：基于 Qwen2.5-VL（3B 和 7B），检索模块输出维度 1024 → 512，L2 归一化。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：  
  - MPDocVQA、DUDE、SlideVQA、MMLongBench-Doc、LongDocURL。  
  - 训练集包含 MPDocVQA、DUDE、SlideVQA 的训练部分。  
- **评估指标**：  
  - 检索：Top1 / Top5 准确率。  
  - 生成：ANLS（MPDocVQA, DUDE）、EM（SlideVQA）、Generalized Accuracy 和 F1（MMLongBench-Doc）、Generalized Accuracy（LongDocURL）。  
- **对比方法**：  
  - **文本检索**：BM25、SBERT、BGE-M3、BGE-large、NV-Embed-v2。  
  - **视觉检索**：CLIP、SigLIP、ColPali、MM-Embed、SV-RAG。  
  - **MLLM 基线**：Qwen2-VL、Qwen2.5-VL、InternVL2.5/3、mPLUG-DocOwl2、CREAM、SV-RAG 等。  
- **主要实验**：  
  - 证据页面检索性能（Table 1）。  
  - 长文档理解主流基准结果（Table 2, Table 3）。  
  - 与基线（相同 Qwen2.5-VL）的公平对比（Table 4）。  
  - 消融实验：检索模块插入位置（Table 5）、两阶段训练策略（Table 6）。  
  - 计算效率对比（Table 7）。

### 4. 资源与算力

- **硬件**：4 块 NVIDIA A6000 GPU（未明确单卡显存大小，A6000 为 48GB）。  
- **训练时长**：检索预训练和联合微调各 1 个 epoch；未给出具体小时数。  
- **参数规模**：URaG-3B 和 URaG-7B，检索模块参数量极小。

### 5. 实验数量与充分性

- **实验组别**：  
  - 检索对比（1 张表，6 种方法 × 4 数据集）。  
  - 生成对比（2 张主表，覆盖 16+ 种方法）。  
  - 基线消融（1 张表，含有无微调对比）。  
  - 位置消融（1 张表，4 个层位置）。  
  - 训练策略消融（1 张表，3 种配置）。  
  - 效率分析（1 张表，3 种输入长度）。  
- **充分性评价**：  
  - 覆盖多种任务（VQA、多页 QA、细粒度证据分类）。  
  - 对比了文本/视觉检索、多种 MLLM 基线，训练数据与评估数据有重叠（MPDocVQA/DUDE/SlideVQA），但 LongDocURL 和 MMLongBench-Doc 为评估。  
  - 消融实验完整，验证了关键设计。  
  - 计算效率分析使用了 FLOPs 公平比较。  
  - 结论客观，承认了微调后 LongDocURL 下降的现象。

### 6. 论文的主要结论与发现

- URaG 在多个长文档理解基准上达到 **state-of-the-art** 性能。  
- **计算开销降低 44%~56%**（FLOPs 对比）。  
- 验证了 MLLM 具有内在的粗到细推理能力，且早期层（第 6 层）的嵌入足以用于高质量检索。  
- 检索模块极轻量（<0.1% 参数），无需外部检索器，实现端到端优化。  
- 对图表、图像等视觉密集型证据类型尤其有效。

### 7. 优点

- **统一框架**：检索与生成集成在同一 MLLM 内，降低系统复杂度，避免外部检索器的额外存储和推理延迟。  
- **端到端可优化**：检索模块与生成模块联合训练，避免错误传播。  
- **轻量高效**：仅增加两个线性层，参数量可忽略；通过早期过滤大幅减少后续计算。  
- **理论启发**：基于注意力分析的类人推理模式为设计提供依据，具有可解释性。  
- **结果强健**：在不微调 MLLM 骨干的情况下依然超越基准，泛化性良好。

### 8. 不足与局限

- **训练数据偏差**：训练集（MPDocVQA/DUDE/SlideVQA）中单页证据问题占主导，可能影响对多页问题（MUL）的性能（Table 3 中 MUL 指标相对较低）。  
- **域外性能下降**：在 LongDocURL 上微调后反而不如仅预训练检索模块，提示存在过拟合或域偏移风险。  
- **模型泛化**：仅基于 Qwen2.5-VL 验证，未在更多 MLLM 架构（如 LLaVA、InternVL）上测试。  
- **长上下文外推未深入**：虽然通过重复页面模拟了 100 页场景，但真实文档布局和长短分布与人工重复不同。  
- **检索 k 值固定**：默认 k=5 未针对不同文档长度自适应调整。  
- **缺乏训练时长/吞吐量**：未报告 GPU 训练小时数或推理速度（仅 FLOPs）。

（完）

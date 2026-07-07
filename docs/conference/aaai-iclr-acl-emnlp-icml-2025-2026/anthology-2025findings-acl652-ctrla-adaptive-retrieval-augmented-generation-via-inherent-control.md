---
title: "CtrlA: Adaptive Retrieval-Augmented Generation via Inherent Control"
title_zh: CtrlA：通过内在控制实现自适应检索增强生成
authors: "Liu Huanshuo, Hao Zhang, Zhijiang Guo, Jing Wang, Kuicai Dong, Xiangyang Li, Yi Quan Lee, Cong Zhang, Yong Liu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.652.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于内在控制的自适应RAG，减少幻觉
tldr: 自适应RAG通过动态检索缓解LLM幻觉，但现有方法仅依赖统计不确定性。CtrlA首次从表示角度出发，提取LLM的诚实度和置信度方向特征，用于控制检索时机。实验表明CtrlA能更准确地决定何时检索，有效提升生成准确性。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1570, \"height\": 755, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 505, \"height\": 322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1029, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 831, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1440, \"height\": 1057, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1628, \"height\": 1532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1645, \"height\": 874, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.652/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1663, \"height\": 485, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 547, \"height\": 546, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 739, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 488, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 704, \"height\": 546, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 483, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1437, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 764, \"height\": 740, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 728, \"height\": 745, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1476, \"height\": 1394, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.652/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 496, \"height\": 236, \"label\": \"Table\"}]"
motivation: 现有自适应RAG方法仅依赖统计不确定性，不够精确。
method: 利用LLM内部表示中的诚实度和置信度方向特征，控制检索时机。
result: CtrlA在多个基准上优于现有自适应RAG方法。
conclusion: CtrlA为自适应RAG提供了新的表示控制范式。
---

## Abstract
Retrieval-augmented generation (RAG) has emerged as a promising solution for mitigating hallucinations of large language models (LLMs) with retrieved external knowledge. Adaptive RAG enhances this approach by enabling dynamic retrieval during generation, activating retrieval only when the query exceeds LLM’s internal knowledge. Existing methods primarily focus on detecting LLM’s confidence via statistical uncertainty. Instead, we present the first attempts to solve adaptive RAG from a representation perspective and develop an inherent control-based framework, termed CtrlA. Specifically, we extract the features that represent the honesty and confidence directions of LLM and adopt them to control LLM behavior and guide retrieval timing decisions. We also design a simple yet effective query formulation strategy to support adaptive retrieval. Experiments show that CtrlA is superior to existing adaptive RAG methods on a diverse set of tasks. Honesty steering can effectively make LLMs more honest and confidence monitoring is a promising indicator of retrieval trigger.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：检索增强生成（RAG）能有效缓解大型语言模型（LLM）的幻觉问题，但传统RAG采用固定检索策略，导致过度依赖外部知识或检索不充分。自适应RAG（ARAG）通过动态决定“何时检索”来优化，其关键在于判断LLM内部知识是否足以回答当前问题。
- **现有方法的局限性**：当前ARAG主要依赖统计不确定性（如输出概率、熵、内部状态）作为检索触发信号。然而这些方法存在两个问题：① 假设LLM输出忠实反映内部知识（即诚实性），但LLM会在“诚实”与“有用”之间权衡，产生低诚实度输出；② 将不确定性与置信度等同，但LLM可能高置信度地输出“我不知道”或等效表达（此时仍需检索），也可能因语义等价表达的方式多样性导致高不确定性但无需检索。
- **论文核心思想**：首次从**表示学习角度**解决ARAG问题，提出框架**CtrlA**，通过提取LLM内部表示中对应**诚实度**和**置信度**的方向特征，同时用于**控制LLM行为（诚实引导）** 和**监控置信度（指导检索时机）**，从而更精准地决定何时检索。

### 2. 论文提出的方法论
- **核心思想**：基于线性表示假设和叠加假设，通过在LLM表示空间中定位诚实度和置信度的方向，利用这些方向向量在生成过程中逐层调整表示（诚实引导）和计算置信度分数（置信度监控）。
- **关键技术细节**：
  - **特征提取**：
    - 使用对比指令（honest/dishonest, confident/unconfident）搭配句子声明，在Teacher-forcing模式下收集各层token表示。
    - 计算正负指令下表示向量的差值获得对比向量，对该层所有对比向量进行PCA，取第一主成分作为该层的方向特征 \( v_h \)（诚实）和 \( v_c \)（置信度）。
  - **诚实引导（Honesty Steering）**：
    - 生成每个token时，对LLM第 \( l \) 层的表示 \( r_k^l \) 施加线性偏移：\( \hat{r}_k^l = r_k^l + \lambda \cdot v_h^l \)，\(\lambda\) 为强度系数（默认0.3）。
    - 逐token、逐层修改表示，使LLM更倾向于输出与内部知识一致的诚实答案。
  - **置信度监控（Confidence Monitoring）**：
    - 对每个生成token \( k \)，计算其表示与置信度方向 \( v_c^l \) 在每层的点积，再平均池化并经过缩放和阈值处理：\( \bar{m}_k = \text{scale}([\text{meanpool}(r_k^{l\top} \cdot v_c^l)]) - \tau \)，\(\tau\) 为灵敏度阈值（默认0.0）。
    - 若新信息token的置信度分数 \( \bar{m}_k < 0 \)，则认为LLM不自信，触发检索；同时检测拒绝表达（如“我不知道”）并单独处理。
  - **查询构建**：
    - **上下文增强查询（CAQ）**：将原问题与当前生成段落中未出现在前文的且不自信的token屏蔽后拼接。
    - **目标验证查询（TVQ）**：利用LLM将原问题与当前生成段落转化为格式良好的查询语句，用于验证当前输出。
- **算法流程**：
  - 输入query，LLM结合诚实引导逐句生成。
  - 每生成一个token，置信度监控实时计算分数，并判断检索触发条件。
  - 若不触发，则继续生成下一句；若触发，则使用CAQ或TVQ构建查询，检索相关文档，重新生成当前句子（必要时结合拒绝处理模块进行最多K次重试）。
  - 重复直至达到结束条件。

### 3. 实验设计
- **数据集与场景**：
  - **短问答**：PopQA、TriviaQA（准确率）。
  - **长问答**：ASQA（str-em、Rouge-L、EM、F1、MAUVE）、Biography Generation（FactScore）。
  - **多跳问答**：2WikiMultihopQA、HotpotQA（EM、F1）。
  - **时效性问答**：FreshQA（500条测试，含四种时间敏感类型，报告relaxed和strict准确率）。
- **对比方法**：
  - 无检索、单轮RAG、基于规则的固定长度/句子/查询分解RAG、自适应RAG方法（FLARE、Self-RAG、DRAGIN、SeaKR、RQ-RAG、QC-RAG等）。
  - 复现方法使用相同骨干模型（Mistral-7B）、相同检索源（2018英文Wikipedia，部分任务补充网页检索），并保持解码策略（greedy）一致。
- **评估指标**：根据任务选择准确率、ROUGE-L、MAUVE、EM、F1、FactScore等。

### 4. 资源与算力
- 论文附录B.4明确提到：使用**2块NVIDIA Tesla V100 32GB GPU**进行所有推理实验；诚实度和置信度特征提取使用scikit-learn的PCA实现。
- 由于CtrlA不需要微调，仅需提取特征和在线推理，因此**未报告额外训练时长或能耗**，算力需求相对较低。

### 5. 实验数量与充分性
- **实验组数**：
  - 主要评估在6个核心数据集 + FreshQA上进行，每个数据集对比多个基线。
  - 消融实验丰富：包括诚实引导强度（λ）、置信度阈值（τ）、引导层范围与步长、查询构建策略（CAQ vs TVQ）、拒绝处理模块、不同骨干LLM（LLaMA2、Vicuna等）。
  - 针对诚实/置信度特征有效性额外进行TruthfulQA评估和人工混淆矩阵分析。
- **充分性与公平性**：
  - 实验覆盖了短/长/多跳/时效性等多种任务类型，评估全面。
  - 严格控制变量：复现基线采用相同骨干、解码策略、检索源；对不可复现的方法（如Self-RAG）引用其公开结果进行对比。
  - 消融实验考虑多维度超参数和组件影响，验证了设计的必要性。
  - 不足：部分任务（如PopQA）因2018 Wikipedia缺失实体而补充网页检索，与基线（Self-RAG）的2020 corpus或Google API不完全一致，但论文已说明差异并尽量对齐。

### 6. 论文的主要结论与发现
- **CtrlA在所有任务上显著优于现有ARAG方法**，包括基于不确定性的FLARE、DRAGIN，基于微调的Self-RAG，以及各种规则方法。
- **诚实引导有效提升LLM诚实度**：在TruthfulQA上验证，适量引导（λ=0.3）能使准确率提升；过量引导则损害语义空间导致性能下降。在RAG场景下，诚实引导也优于简单的“诚实提示”。
- **置信度监控是可靠的检索触发信号**：通过对置信度分数设阈值，能有效识别LLM不自信的情况，且对未知问题、不可答问题敏感。
- **中间层（5~18层）引导效果最佳**，且步长为2~3时效果最好。
- **拒绝处理模块至关重要**，尤其在长尾问题（PopQA）上显著提升准确率（从38.0%到44.1%）。

### 7. 优点
- **创新性**：首次从表示学习视角解决ARAG问题，将诚实度和置信度方向进行分离并利用，打破了统计不确定性的依赖。
- **即插即用、无需微调**：特征提取仅需少量无标注数据，推理时只需对LLM表示做简单线性操作，计算开销小，易于集成。
- **方法论简洁有效**：诚实引导和置信度监控均基于线性操作；阈值τ和系数λ可调，便于任务适配。
- **查询构建策略考虑周全**：CAQ考虑了噪声过滤（屏蔽不自信+旧信息），TVQ提供格式友好的查询，两者互补。
- **实验全面且深入**：多任务、多骨干、多组消融，验证了框架的鲁棒性和可迁移性。

### 8. 不足与局限
- **特征提取质量**：使用简单的PCA和对比指令方法，作者承认更复杂的方法（如微调）可能产生更有效的特征，当前方法对数据分布和大小较敏感（小数据集时表现不稳定）。
- **未验证检索内容质量**：CtrlA不显式评估检索到的文档是否相关、有用或正确的，可能引入噪声或冲突信息（虽然后续生成可通过诚实引导部分缓解）。
- **未跨语言测试**：所有实验均基于英文，诚实/置信度方向的迁移性在其他语言中未验证。
- **诚实引导强度需谨慎调参**：λ过大可能破坏语义空间，不同任务最优λ不同，实际部署需调试。
- **置信度监控阈值τ固定为0**：虽然实验显示τ=0效果良好，但不同场景下可能需要调整，论文未提供自动化调整方法。
- **算力报告不完整**：仅提及推理使用2块V100，未给出总计算量或时间，对资源需求估计不够透明。

（完）

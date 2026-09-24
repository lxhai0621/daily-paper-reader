---
title: Agentic Verification for Ambiguous Query Disambiguation
title_zh: 面向歧义查询消解的智能体验证方法
authors: "Youngwon Lee, Seung-Won Hwang, Ruofan Wu, Feng Yan, Danmei Xu, Moutasem Akkad, Zhewei Yao, Yuxiong He"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1932.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: RAG查询消解的验证
tldr: "在RAG的歧义查询消解中，先多样化再验证的流程常生成无法从语料回答的查询，需要昂贵的事后剪枝与验证。本文提出VerDICT，将多样化与验证统一，在早期整合检索器相关性与生成器可回答性反馈。在ASQA数据集上，VerDICT相较最强基线将落地感知F1平均提升23%。该方法减少了级联错误并支持并行，为RAG的歧义查询处理提供了更高效的方案。"
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1932/fig-001.webp\", \"caption\": \"\", \"page\": 5, \"index\": 1, \"width\": 4005, \"height\": 1095}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1932/fig-002.webp\", \"caption\": \"\", \"page\": 9, \"index\": 2, \"width\": 3208, \"height\": 1576}]"
motivation: RAG中歧义查询消解的先多样化后验证流程会产生无法从语料回答的未落地查询，并需昂贵的事后剪枝与验证。
method: 提出VerDICT，将多样化与验证统一，早期整合检索器相关性与生成器可回答性反馈。
result: "在ASQA上，VerDICT相较最强基线将落地感知F1平均提升23%。"
conclusion: 统一多样化与验证可减少级联错误并支持并行，提升RAG歧义查询处理效果。
---

## Abstract
We study ambiguous-query disambiguation in retrieval-augmented generation (RAG). Prior Diversify-then-Verify (DtV) pipelines first generate interpretations and then retrieve evidence, often introducing ungrounded queries that cannot be answered from the corpus and requiring costly post-hoc pruning and verification. We propose VerDICT, a novel approach that unifies diversification with verification by integrating retriever relevance and generator answerability feedback early. This not only reduces cascading errors but also enables parallelism. On ASQA, VerDICT improves grounding-aware F1 by an average of 23% over the strongest baselines across multiple LLM backbones.

---

## 论文详细总结（自动生成）

# VERDICT：面向歧义查询消解的智能体验证方法（ACL 2026 Findings）论文总结

## 1. 核心问题与研究动机

- **背景**：检索增强生成（RAG）在企业场景中需要在领域特定、动态演化的语料上回答简短模糊的查询（如"What is HP?"），必须先进行**歧义消解**，将其分解为语料中可回答的具体解释（interpretation）。
- **既有方法的两条路线及其缺陷**：
  - **RAC（先检索后生成）**：用单一 top-k 检索定义可解释范围，受限于**有界召回**（bounded recall）；增大 k 又会引入噪声并让 LLM 难以产出干净的消解结果。
  - **DtV（Diversify-then-Verify，如 DIVA）**：先用 LLM 生成候选伪解释，再检索证据并事后验证。问题是**在见到证据前就完成多样化**，无法知道哪些解释在语料中真正可回答，从而产生大量**未落地（ungrounded）解释**（如企业内部语料中根本没有"Harry Potter"），这些解释仍会触发检索与下游处理，最终被丢弃，造成**级联错误**、昂贵的验证调用与串行延迟。
- **核心主张**：应当把**多样化与验证统一**起来，在解释生成的当下就用检索器与生成器反馈做落地约束，从而同时降低错误传播并实现并行化。

## 2. 方法论

### 2.1 问题形式化
- 给定歧义问题 $q$ 与段落语料 $C$，目标是识别有效解释集 $Q=\{q_1,\dots,q_N\}$ 及对应答案 $Y$。
- 在 RAG 设定下，模型输出为**三元组集合** $\hat{T}=\{(\hat q_j,\hat y_j,\hat p_j)\}_{j=1}^{M}$，其中 $\hat p_j\in C$ 为支撑段落；人类标注用波浪号表示（$\tilde Q$ 等）。

### 2.2 核心思想：Verified Diversification（验证式多样化）
与 DtV 相反，VERDICT **不先生成解释再看证据**，而是先构建高覆盖的检索宇宙，再逐段落判断其能否支撑一个具体的"消解后问答对"，把验证前移到生成点：

- **检索器相关性反馈（Relevance Feedback）**：
  - 先用 LLM 通过提示 $I_R$ 把 $q$ 改写为**松弛查询** $q'$（保留核心实体与概念，最大化开放性）；
  - 仅做**一次**检索 $U=\text{TopK}_k(C,q';s)$，论文经验性调优 $k=20$（在 GPT-4o 骨干下与 top-100 覆盖持平）。
  - 大 k + 松弛查询在保持计算效率的同时提升解释的多样性与覆盖度。
- **生成器可回答性反馈（Answerability Feedback）**：
  - 对每个 $p_i\in U$，生成器仅接收 $(q,p_i)$ 与提示 $I_E$，输出一对 $(\hat q_i,\hat y_i)$ 或**弃权（null）**；
  - 成功的输出构成候选三元组 $T_0=\{(\hat q_i,\hat y_i,p_i)\mid p_i\in U,\ \hat q_i\neq\text{null}\}$；
  - 该"逐段落抽取"可**完全并行**，每次调用输入极短，降低延迟与幻觉，且对小模型更友好。
  - 例如同时提到 HP 产品的段落 $p_2$ 因无法生成合法问答对被剪枝，而可回答"HP 是什么"的 $p_1$ 被保留。

### 2.3 Consolidated Feedback（反馈整合）
- 将生成器产出的"问题+答案"拼接后用检索器编码器 $f$ 投影到隐空间 $\mathbb{R}^d$；
- 使用 **HDBSCAN**（层次密度聚类）聚类，丢弃不属于任何稠密簇的**离群点**（通常来自不可回答解释或低忠实度改写）；
- 每个非离群簇选取 **medoid 三元组**作为最终输出 $\hat{T}$；
- 该步骤**不引入额外的检索或 LLM 调用**，同时天然完成**去重**（语料冗余导致同一解释被多段落支撑），而 RAC/DIVA 把去重完全交给 LLM。

### 2.4 复杂度对比
- DtV：检索器调用 $O(|R|)$（每个伪解释一次），LLM 调用 $O(|R|)\times O(|U_R|)$，单次输入上下文长；
- VERDICT：检索器调用 $O(1)$，LLM 调用 $O(|U|)\times O(1)$，单次输入仅一个段落。

### 2.5 落地评估协议（Grounded Metrics）
- 传统指标（BLEU 匹配、无落地 Recall）不检查生成是否被段落支撑，且参考集本身可能有界覆盖或包含未落地解释；
- 提出扩展的二值匹配 $V(\hat q,\hat p)\in\{0,1\}$（由 LLM 判定），据此定义：
  - **G-Precision** $=\frac{1}{|\hat Q|}\sum_{\hat q\in\hat Q}V(\hat q,\hat p)$；
  - **G-Recall** $=\frac{1}{|\bar Q|}\sum_{\bar q\in\bar Q}V(\bar q,\hat p)$，其中 $\bar Q$ 是人工解释 $\tilde Q$ 与已通过验证的模型预测的并集；
  - **G-F1** 为二者调和平均。

## 3. 实验设计

- **主要数据集 / Benchmark**：**ASQA**（基于 AmbigNQ，验证集 948 例，Wikipedia 语料），提供人工标注解释 $\tilde Q$、答案 $\tilde Y$ 与可选支撑段落。
- **对比方法**：
  - **RAC**（Kim et al., 2023）：单次 top-k 检索 + 长上下文生成；
  - **DIVA**（In et al., 2025）：DtV 的代表性 SOTA；
  - **DIVA−Verification**：仅使用 DIVA 的伪解释，作为轻量效率型基线。
- **骨干 LLM**：LLaMA 3.1 8B、LLaMA 3.3 70B、GPT-4o。
- **检索系统**：arctic-embed（第一阶段）+ gte-Qwen2（重排/嵌入）；聚类用 HDBSCAN；贪心解码。
- **评价指标**：多样性（$|\hat Q|$、Sufficient%、无落地 Recall）+ 落地指标（G-Precision、G-Recall、G-F1）。
- **附加场景**：
  - **AmbigDocs**（实体级歧义，指标为 answer recall）；
  - **私有企业基准**（215 份内部 IT 类 PDF，60 个人工标注问答对，查询被改写以注入歧义）；
  - **HotpotQA**（多跳扩展：松弛出两个子查询 $q'_1,q'_2$，取笛卡尔积 $U_{q_1}\times U_{q_2}$ 拼接为单上下文后复用原流程）；
  - **与 MADAM-RAG 式多智能体聚合的单轮变体对比**。

## 4. 资源与算力

- **论文未明确披露任何算力信息**：没有给出 GPU 型号、数量、训练时长、总调用量或成本估算。
- 从方法描述可推断：该方法**不涉及模型训练**（无微调），完全依赖推理/API 调用；实验中用到 GPT-4o（API）与 LLaMA 3.1 8B / 3.3 70B，以及 arctic-embed、gte-Qwen2 两个嵌入/重排模型。
- 唯一与"成本"相关的量化是**调用复杂度**（表 1）与**端到端延迟**（表 6、表 9），而非硬件资源。

## 5. 实验数量与充分性

大致包含以下实验组：

- **主实验**：ASQA × 3 个骨干 × 4 个方法（含人工标注参照），报告 6 类指标；
- **消融实验**：Retriever-only 与 Generator-only 两个削弱版本，验证两类反馈的协同必要性；
- **聚类策略敏感性**：Default / Conservative / $f(\hat q;\hat y)$ / $f(\hat q)$ 四组；
- **去重有效性**：冗余率对比（10.21% vs 21.94%）；
- **效率**：端到端延迟与分组件延迟分解；
- **泛化性**：AmbigDocs、私有企业语料、HotpotQA 三个额外场景；
- **替代聚合方案**：与 MADAM-RAG 式 LLM 聚合的单轮变体对比（精度略降、延迟约 10 倍）；
- **误差分析**：按"段落是否相关/可回答"划分四象限，统计答案正确率与解释错误率；
- **LLM 评判稳定性**：GPT-4o 重复评测 3 次，最大差异 0.4 个百分点。

**充分性与公平性评估**：

- 覆盖面较广（多骨干、多数据集、多任务、消融、延迟、误差分析、评判稳定性），整体较充分；
- 对比设置基本公平：DIVA 的验证器统一固定为 GPT-4o（因弱模型在长上下文验证上表现不可靠），并说明其遵循原论文的 top-5 设置；
- **存在若干可质疑之处**：私有企业基准规模较小（60 条）且不可复现；HotpotQA 扩展仅报告 $|\hat Q|$ 与 G-Precision（G-Recall 按构造恒为 1）；消融采用"削弱代理"而非真正移除反馈信号；G-Precision 的 LLM 判定存在主观性。

## 6. 主要结论与发现

- **多样性达到人类水平且跨模型稳定**：VERDICT 的 $|\hat Q|$、Sufficient% 与人工标注相当；而 DIVA/RAC 的多样性对模型规模高度敏感（8B 时 Sufficient% 掉到 <1%）。
- **落地质量显著提升**：G-Precision 达 92.82%（GPT-4o）、81.50%（LLaMA 70B）；人工标注解释仅 65.47% 落地，DtV 最多 53% 未落地。
- **G-F1 大幅领先**：8B 57.94 / 70B 67.80 / GPT-4o 70.82，相较各骨干下最强基线**平均提升 23%**。
- **两类反馈缺一不可**：仅检索器反馈使 G-Precision 从 93% 跌至 68%；仅生成器反馈使 $|\hat Q|$ 从 3.16 跌至 1.15、G-Recall 从 57% 跌至 24%。
- **效率更优**：端到端延迟 2.12s vs DIVA 5.34s，源于逐段落并行、单次检索、无长上下文串行验证。
- **泛化性良好**：AmbigDocs answer recall 35.8（DIVA 26.1、RAC 27.4）；私有企业语料 G-Precision 90.1；HotpotQA G-Precision 91.27（DtV 77.43）。
- **聚类整合优于 LLM 聚合**：精度更高、延迟约 0.2s vs 2s。
- **误差规律**：当段落既相关又可回答时，8B 正确率 92%、更强模型达 98–99%；主要错误集中在"不可回答段落未能正确弃权"，且随模型规模显著缓解。

## 7. 优点

- **架构层面的创新**：把"验证"从后置阶段内化为多样化过程的一部分，从源头阻断未

落地解释的产生，避免了 DtV 范式中"先生成、后验证"造成的级联错误与无效检索；这一改动虽小，但重新划分了检索器与生成器在歧义消解中的职责边界。
- **检索器与生成器的角色分工清晰**：检索器只负责"广度"（松弛查询 + 单次大 k 检索），生成器只负责"深度"（逐段落判断可回答性并抽取问答对），二者各司其职，避免了长上下文提示中让单一 LLM 同时兼顾开放性与落地性的困难。
- **工程友好**：单次检索、逐段落可并行、单次调用输入极短，使方法在小模型上也能工作（8B 的 Sufficient% 仍接近人类），并且对私有语料无需训练即可迁移。
- **评估协议上的贡献**：提出 G-Precision / G-Recall / G-F1，把"解释是否被语料支撑"显式纳入指标，并揭示了人工标注本身仅约 65% 落地这一被忽视的事实，对后续歧义消解研究具有方法论价值。
- **聚类式反馈整合**：用 HDBSCAN + medoid 在隐空间中同时完成去噪、去重与选代表，不额外消耗检索或 LLM 调用，且实证优于 LLM 聚合（精度更高、延迟约低一个数量级），是一个"零额外成本换质量"的设计。
- **可复现性较好**：核心超参（k=20、提示模板、聚类变体）均有说明，且提供了四组聚类策略与评判稳定性的对照。

## 8. 局限性

- **对检索宇宙的依赖**：松弛查询 + 固定 k=20 的检索宇宙是解释覆盖度的上限；若某解释在 top-20 中无任何段落命中，VERDICT 无法恢复该解释（尽管论文称 k=20 与 top-100 覆盖持平，但这是经验性结论，换语料/检索器是否成立未充分验证）。
- **LLM 弃权能力是瓶颈**：误差分析显示主要错误来自"不可回答段落未能正确弃权"，即生成器的可回答性判断不够可靠；小模型（8B）在此处的错误率明显高于大模型，说明方法的落地质量仍随骨干能力单调变化。
- **评估协议的循环性风险**：G-Precision/G-Recall 依赖 LLM 判定 $V(\hat q,\hat p)$，而同一族 LLM 也参与生成与验证；虽然做了重复评测稳定性检查（最大差异 0.4pp），但稳定性 ≠ 正确性，判定偏差方向未被独立人工评估校准。
- **参考集 $\bar Q$ 的构造**：G-Recall 的分母取"人工解释 ∪ 已通过验证的模型预测"，这一并集设计会使模型自产的有效解释也能计入召回，可能对 VERDICT 类方法有系统性偏向，削弱了与 DIVA/RAC 的可比性。
- **私有企业基准不可复现且规模小**：215 份 PDF、60 条问答对，仅能作为定性佐证，不足以支撑强统计结论；且查询歧义是人工注入的，与真实企业查询分布可能存在差距。
- **HotpotQA 扩展较浅**：仅验证了"松弛出两个子查询 + 笛卡尔积"这一种多跳形式，且只报告 $|\hat Q|$ 与 G-Precision（G-Recall 按构造恒为 1），多跳场景下的落地召回能力实际未被检验。
- **消融非严格移除**：Retriever-only / Generator-only 是"削弱代理"而非真正消融对应反馈信号，因此"两类反馈缺一不可"的因果强度有限。
- **聚类超参敏感性**：HDBSCAN 的最小簇规模、离群点判定阈值等未系统报告；论文承认需丢弃离群点，但未说明离群率随语料/模型的变化，过激的离群裁剪可能误删稀有但正确的解释。
- **延迟对比的公平性**：2.12s vs 5.34s 的端到端延迟优势部分来自并行化与单次检索的架构差异，而非纯粹的算法效率；在同等硬件/API 配额下（尤其 API 限流时）并行逐段落调用的实际吞吐表现未被讨论。
- **未覆盖多语言与非英语语料**：全部实验基于英语 Wikipedia 与英语企业内部文档，跨语言歧义消解（如中文缩写、日语同形词）未涉及。

## 9. 启发与展望

- **"验证前移"是可迁移的范式**：把后置验证信号内化为生成时的约束，这一思路可推广到其他"开放生成 + 落地约束"的任务，如多跳问答的子问题生成、对话式检索中的澄清提问、以及需要引用支撑的长文生成。
- **检索器/生成器职责解耦**：让检索器负责召回广度、生成器负责落地判断，避免单一长上下文 LLM 同时承担开放与约束的双重目标，这一分工对 RAG 系统的提示工程有直接指导意义。
- **评估应显式区分"多样性"与"落地性"**：论文揭示的人工标注仅 65% 落地，提示社区在构建歧义消解基准时应同步标注支撑段落，否则会奖励"看起来多样但无法回答"的输出。
- **后续可探索方向**：
  - 用**自适应 k** 或迭代检索替代固定 top-20，在覆盖度与噪声间动态平衡；
  - 用**更强的弃权/校准机制**（如置信度阈值、轻量判别器）改善不可回答段落的识别；
  - 将隐空间聚类整合推广到**跨查询、跨会话**的解释归并，构建可复用的解释库；
  - 在**多跳与多语言**场景中检验松弛查询与笛卡尔积扩展的伸缩性；
  - 引入**独立人工评估**校准 LLM 判定，缓解评估协议的循环性。
- **对工业 RAG 的启示**：在动态演化的私有语料上，与其让 LLM 先自由发散再昂贵验证，不如用一次松弛检索圈定"可能可回答的宇宙"，再让模型逐条落地判断——这既降低幻觉与无效调用，也天然契合并行化与成本控制。

（完）

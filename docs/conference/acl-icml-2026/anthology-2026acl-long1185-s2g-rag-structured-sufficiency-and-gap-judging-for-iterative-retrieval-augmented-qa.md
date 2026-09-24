---
title: "S2G-RAG: Structured Sufficiency and Gap Judging for Iterative Retrieval-Augmented QA"
title_zh: "S2G-RAG:面向迭代式检索增强问答的结构化充分性与缺口判断"
authors: "Minghan Li, Junjie Zou, Xinxuan Lv, Chao Zhang, Guodong Zhou (周国栋)"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1185.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: "迭代式RAG框架,通过充分性判断提升检索准确性"
tldr: "多跳问答中,迭代式检索增强生成常因证据链不完整或累积冗余干扰文本而失败。本文提出S2G-RAG框架,引入显式控制器S2G-Judge,每轮判断当前证据记忆是否足以作答,若不足则输出描述缺失信息的结构化缺口项,以此指导下一步检索。该方法通过结构化充分性判断控制检索进程,提升了检索准确性与答案可靠性,为迭代式RAG的可控性提供新思路。"
source: ACL-2026-Long
selection_source: conference_retrieval
motivation: "迭代式RAG在多跳问答中易从不完整证据作答或累积干扰文本,缺乏对检索充分性的显式控制。"
method: "提出S2G-RAG框架,引入S2G-Judge控制器,每轮判断证据是否充分并输出结构化缺口项指导下一轮检索。"
result: "该方法通过结构化充分性判断控制检索流程,减少冗余干扰,提升了多跳问答的证据链完整性与作答准确性。"
conclusion: 显式的结构化充分性与缺口判断能有效增强迭代式RAG的可控性与检索质量。
---

## Abstract
Retrieval-Augmented Generation (RAG) grounds language models in external evidence, but multi-hop question answering remains difficult because iterative pipelines must control what to retrieve next and when the available evidence is adequate. In practice, systems may answer from incomplete evidence chains, or they may accumulate redundant or distractor-heavy text that interferes with later retrieval and reasoning. We propose S2G-RAG (Structured Sufficiency and Gap-judging RAG), an iterative framework with an explicit controller, S2G-Judge. At each turn, S2G-Judge predicts whether the current evidence memory supports answering and, if not, outputs structured gap items that describe the missing information. We map these gap items into the next retrieval query, producing stable multi-turn retrieval trajectories. To reduce noise accumulation, we maintain a sentence-level Evidence Context by extracting a compact set of relevant sentences from retrieved documents. Experiments on TriviaQA, HotpotQA, and 2WikiMultiHopQA show that S2G-RAG improves multi-hop QA performance and robustness under multi-turn retrieval. Furthermore, S2G-RAG can be integrated into existing RAG pipelines with a lightweight component, without modifying the search engine or retraining the generator.

---

## 论文详细总结（自动生成）

# S2G-RAG 论文中文总结

## 1. 核心问题与整体含义

- **研究背景**：检索增强生成（RAG）已成为知识密集型问答的标准方案，但多跳问答仍困难，因为答案需要跨多个文档组合证据，后续检索依赖前几轮中间发现。
- **核心问题**：迭代式 RAG 存在“检索控制瓶颈”——每一轮必须判断当前累积证据是否足以作答，以及若不足，下一步应检索什么。
- **现实失败模式**：
  - 证据链不完整时仍强行作答；
  - 继续检索但目标不清，导致重复、冗余或干扰文本累积，反过来破坏后续检索与推理。
- **现有方法不足**：
  - 控制常与自由文本生成纠缠，难以审计，且在干扰下脆弱；
  - 下一跳信息需求表达不充分，易漂移、重复或过度泛化；
  - 过程监督昂贵，理想轨迹监督与实际多轮中间证据状态存在分布不匹配；
  - 多轮检索上下文膨胀，朴素拼接会进一步破坏控制。
- **整体含义**：论文主张把迭代 RAG 的控制显式化、结构化、模块化，提出 **S2G-RAG**，通过每轮“充分性判断 + 缺口项预测”来控制检索，并用句级证据上下文抑制噪声累积。

## 2. 方法论

- **核心思想**：将迭代 RAG 控制建模为每轮结构化预测：判断证据是否充分；若不足，输出描述缺失信息的结构化缺口项，用其构造下一轮检索查询。
- **S2G-RAG 推理循环**：
  - 给定问题 \(q\) 和外部语料 \(D\)，维护累积证据上下文 \(C_t\)，初始 \(C_0=\emptyset\)，最多运行 \(T\) 轮检索。
  - 每轮由四部分组成：**S2G-Judge、Retriever、Evidence Extractor、Reasoner**。
- **S2G-Judge**：
  - 输入仅为 \((q, C_t)\)，输出 \(y_t=(s_t,G_t)\)。
  - \(s_t\in\{\text{true},\text{false}\}\) 表示当前证据是否足以支持作答。
  - 若 \(s_t=\text{true}\)，则 \(G_t=\emptyset\)，进入作答。
  - 若 \(s_t=\text{false}\)，输出结构化缺口项集合 \(G_t\)。
  - 缺口项 schema 四字段：
    - `category`：`bridge_entity / attribute / relation / evidence_span / other`
    - `target`：被查询实体
    - `slot`：粗粒度属性或关系名
    - `description`：简短自然语言说明
  - 采用 **context-only constraint**：充分性判断必须严格基于 \(C_t\) 中已有证据，避免依赖参数化知识。
- **查询构造**：
  - 当 \(s_t=\text{false}\)，将缺口项映射为查询短语。
  - 优先拼接 `target + slot`；若二者不全，则回退到 `description`。
  - 取前 \(K\) 个有效短语追加到原问题；默认 \(K=1\)。若无有效短语，则 \(\tilde q_t=q\)。
- **句级证据抽取**：
  - 将新检索文档分句，形成全局索引候选池，每句附文档标题以保留来源。
  - LLM 抽取器基于 \((q,G_t,S_t)\) 只输出句子索引，不改写或生成证据文本。
  - 再确定性映射回原句，形成证据块 \(E_t\)，更新：
    \[
    C_t = C_{t-1} \oplus E_t
    \]
  - 缺口项 \(G_t\) 用于优先选择能填补当前信息缺口的句子，保持多跳进展。
- **Reasoner**：
  - 与检索控制解耦，仅在 \(s_t=\text{true}\) 或达到最大预算时调用，基于 \((q,C_t)\) 生成最终答案。
- **训练方式：轨迹蒸馏**：
  - 在训练问题上执行同一迭代检索与证据累积流程，记录每轮快照 \((q,C_t)\)。
  - 轨迹收集使用未微调 judge backbone，模拟真实多轮状态，包括冗余和干扰。
  - 强教师模型 GPT-4o-mini 在 context-only 约束下标注每轮充分性决策和结构化缺口项。
  - 进行格式检查与轻量冲突过滤，去除低置信监督。
  - 用 LoRA 做监督微调，使 S2G-Judge 直接预测结构化输出：
    \[
    L(\phi)=-\sum_{(x_t,y_t)}\sum_{i=1}^{|y_t|}\log p_\phi(y_{t,i}\mid y_{t,<i},x_t)
    \]

## 3. 实验设计

- **数据集/场景**：
  - **TriviaQA**：单跳开放域问答。
  - **HotpotQA**：多跳问答，需跨文档组合证据。
  - **2WikiMultiHopQA**：多跳问答，强调实体消歧和细粒度证据组合。
  - 使用各数据集提供的 Wikimedia dumps 作为检索语料，官方 development split 评估。
  - 指标：Exact Match（EM）和 F1。
- **实现配置**：
  - 答案 Reasoner：Llama-3-8B-Instruct。
  - Evidence Extractor：与 Reasoner 相同 backbone。
  - S2G-Judge：Llama-3.2-3B-Instruct + LoRA。
  - 教师：GPT-4o-mini。
  - 默认最多 \(T=4\) 轮检索，每轮 top-\(k=6\)，按标题跨轮去重。
  - 稀疏检索：BM25 / Pyserini；稠密检索：E5-base-v2。
- **对比基线**：
  - NaiveGen：无检索直接作答。
  - Standard RAG：单轮检索生成。
  - IR-CoT：检索与中间推理信号交错。
  - FLARE：基于生成不确定性触发检索。
  - ReSP：retrieve–summarize–plan 迭代。
  - Self-RAG：用反思 token 控制检索。
  - SIM-RAG：轻量 critic 判断是否接受答案或继续搜索。
  - RAG-Critic：错误感知 critic 触发修正工作流。
- **主要结果概览**：
  - BM25 下，S2G-RAG：
    - TriviaQA：72.0 EM / 77.9 F1
    - HotpotQA：43.3 EM / 56.5 F1
    - 2WikiMultiHopQA：41.7 EM / 48.6 F1
  - E5 下，S2G-RAG：
    - TriviaQA：71.1 EM / 78.0 F1
    - HotpotQA：42.0 EM / 53.5 F1
    - 2WikiMultiHopQA：39.0 EM / 45.3 F1
  - 相对 SIM-RAG，BM25 下 TriviaQA +1.3 EM / +2.3 F1；HotpotQA +10.6 EM / +13.2 F1；2Wiki +7.6 EM / +8.4 F1。
- **分析实验**：
  - 消融：w/o SFT、w/o S2G-Judge、w/o Extractor。
  - 充分性预测混淆矩阵。
  - 证据记忆压缩效率与延迟。
  - 与 LLM summarization、ReComp extractive/abstractive 压缩方法对比。
  - 教师–学生在不同检索预算 \(

- 教师–学生在不同检索预算 \(T\) 下的决策质量与最终性能对比：随着 \(T\) 从 1 增至 4，学生 S2G-Judge 的充分性判断准确率与缺口项匹配率逐步提升，在 \(T=4\) 时已接近教师 GPT-4o-mini 的水平；继续增加预算收益递减，且可能因累积噪声导致假阳性上升。学生模型在低预算下更保守，倾向于继续检索，而教师更早判定充分，表明轨迹蒸馏有效传递了“何时停止”的决策边界。

- **消融实验结论**：
  - **w/o SFT**：直接使用未微调的 judge backbone，充分性判断与缺口项格式错误率显著升高，多跳数据集 EM 下降最明显，证明轨迹蒸馏是结构化控制能力的关键来源。
  - **w/o S2G-Judge**：退化为固定轮次迭代检索，无法自适应停止，HotpotQA 与 2WikiMultiHopQA 上因冗余证据累积导致 F1 大幅下降。
  - **w/o Extractor**：以整文档拼接替代句级证据抽取，上下文长度急剧膨胀，检索控制与推理均受干扰，尤其在 2Wiki 上实体消歧能力退化明显。
  - 三者中，移除 S2G-Judge 的损害最大，说明显式充分性判断与缺口项预测是 S2G-RAG 的核心增益。

- **充分性预测混淆矩阵**：S2G-Judge 在“充分/不充分”二分类上保持较高精确率与召回率；假阳性（过早停止）多出现在需要隐式常识桥接的样本，假阴性（过度检索）多出现在问题表述模糊或首轮检索未命中关键实体时。context-only 约束有效抑制了参数化知识泄漏，使判断更依赖可审计证据。

- **证据记忆压缩效率**：句级证据抽取将每轮上下文从整文档级别压缩至数十句以内，token 消耗降低约一个数量级，同时下游 EM/F1 不降反升。与 LLM summarization、ReComp extractive/abstractive 压缩相比，S2G-RAG 的句级抽取在压缩率、来源可追溯性和延迟之间取得更优平衡；抽象压缩虽进一步缩短上下文，但易丢失细粒度实体与关系，导致多跳推理断裂。

- **错误分析**：剩余错误主要分为三类：① 检索未命中，即缺口项正确但检索器未能返回相关文档；② 实体链接/消歧错误，在 2Wiki 中尤为突出；③ 多跳链断裂，即中间证据被正确检索但 Reasoner 未能正确组合。这些错误表明，S2G-RAG 的控制层已较稳健，进一步提升需依赖更强检索器与推理器。

## 4. 结论与贡献

- **主要贡献**：
  1. 将迭代 RAG 的控制瓶颈显式建模为每轮“充分性判断 + 结构化缺口项预测”，使检索决策可审计、可干预。
  2. 提出 S2G-RAG 框架，通过句级证据抽取与缺口引导查询构造，缓解多轮上下文膨胀与检索漂移。
  3. 设计轨迹蒸馏训练范式，利用未微调 judge 收集真实多轮状态，由强教师标注结构化监督，避免理想轨迹与测试分布不匹配。
  4. 在单跳与多跳问答基准上取得一致提升，尤其在多跳场景下显著优于 Self-RAG、SIM-RAG、RAG-Critic 等强基线。

- **整体结论**：结构化、模块化的检索控制是提升迭代 RAG 鲁棒性与多跳推理能力的有效途径；S2G-RAG 在性能、可解释性和效率之间实现了良好折中。

## 5. 局限与未来工作

- **局限**：
  - 依赖 GPT-4o-mini 等强教师模型进行轨迹标注，训练成本较高，且教师偏差可能传递给学生。
  - 缺口项 schema 为人工预定义，对开放域中罕见信息需求类型的覆盖有限。
  - 检索质量仍是性能上限的重要约束，稀疏/稠密检索器未命中时控制层难以完全补偿。
  - 实验主要集中于英文 Wikipedia 语料，跨领域、多语言与多模态场景尚未验证。

- **未来工作**：
  - 探索更高效的弱监督或自监督轨迹标注，降低对强教师的依赖。
  - 扩展缺口项 schema 或引入动态 schema 生成，适应更复杂的信息需求。
  - 与更强检索器、工具调用及多模态证据源结合。
  - 研究自适应检索预算与在线学习，使 S2G-Judge 能在部署中持续改进。

（完）

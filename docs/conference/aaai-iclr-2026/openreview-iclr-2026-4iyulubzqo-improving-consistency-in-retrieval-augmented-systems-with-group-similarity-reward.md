---
title: Improving Consistency in Retrieval Augmented Systems with Group Similarity Reward
title_zh: 利用组相似度奖励提升检索增强系统的一致性
authors: "Faisal Hamman, Chenyang Zhu, Anoop Kumar, Xujun Peng, Sanghamitra Dutta, Daben Liu, Alfy Samuel"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=4IyULUbzQO"
tags: ["query:ma-kf"]
score: 9.0
evidence: 提出组相对奖励与一致性评估框架，减少RAG在语义等价查询上的不一致
tldr: RAG系统在语义等价输入上常存在答案不一致，影响可靠性与信任。本文将一致性拆解为检索器、生成器和端到端三个层面，并提出基于释义集合的组相对奖励方法，明确识别不一致来源并直接优化生成一致性。实验证明该方法能有效提升RAG系统在多个数据集上的一致性指标，为高可信RAG部署提供了系统化方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: RAG在语义等价查询下输出不一致，损害高价值领域中的可信度。
method: 提出一致性分解评估框架，并用组相对奖励对生成器进行优化。
result: 在多个基准上显著提升信息一致性，并定位到具体不一致来源。
conclusion: 通过显式优化一致性可增强RAG系统的可靠性和部署价值。
---

## Abstract
RAG systems are increasingly deployed in high-stakes domains where users expect outputs to be consistent across semantically equivalent queries. However, existing systems often exhibit significant inconsistencies due to variability in both the retriever and generator (LLM), undermining trust and reliability. In this work, we focus on \emph{information consistency}—the requirement that outputs convey the same core content and information across semantically equivalent inputs. We introduce a principled evaluation framework that decomposes RAG consistency into retriever-level, generator-level, and end-to-end components, helping identify inconsistency sources. To improve consistency, we propose  \textbf{P}araphrased \textbf{S}et Group Relative Policy Optimization (PS-GRPO), an RL approach that leverages multiple rollouts across paraphrased set to assign \emph{group similarity rewards}.   We leverage PS-GRPO to achieve Information \textbf{Con}sistent \textbf{RAG} (Con-RAG), training the generator to produce consistent outputs across paraphrased queries and remain robust to retrieval-induced variability. Because exact reward computation over paraphrase sets is computationally expensive, we also introduce a scalable approximation method that retains effectiveness while enabling efficient, large-scale training. Empirical evaluations across  short-form, multi-hop, and long-form QA benchmarks demonstrate that Con-RAG significantly improves both consistency and accuracy over strong baselines, even in the absence of explicit ground-truth supervision. Our work provides practical solutions for evaluating and building reliable RAG systems for safety-critical deployments.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：检索增强生成（RAG）系统已广泛应用于金融、医疗等高风险领域，用户期望系统对语义等价的查询能给出一致、可靠的答案。然而，由于检索器（retriever）与生成器（LLM）本身的随机性和变异性，现有 RAG 系统即使在语义完全相同的输入下也可能输出不一致的内容，严重削弱用户信任与系统可靠性。
- **核心问题**：论文聚焦于 **信息一致性（information consistency）**，即系统必须在语义等价的输入上传达相同的核心内容与信息。作者明确指出，一致性问题在现有 RAG 研究中被忽视，且缺乏系统化的评估与优化手段。
- **整体意义**：该工作旨在为 RAG 提供一套“可评估 + 可优化”的一致性方案，使其更适用于安全关键的部署场景，填补了从理论定义到工程实践之间的空白。

### 2. 论文提出的方法论

- **核心思想**：将一致性问题显式建模，并利用强化学习直接优化生成器在释义（paraphrase）集合上的一致性，而非依赖启发式规则或隐式的模型能力。
- **一致性分解评估框架**：将 RAG 一致性拆解为三个可独立量化的层级：
  - **检索器级一致性**：语义等价查询是否检索到相近文档集合；
  - **生成器级一致性**：给定相同或等效上下文时 LLM 是否输出一致答案；
  - **端到端一致性**：系统整体在语义等价输入下的最终输出一致性。
  - 该分解便于精确定位不一致的源头，是后续优化的基础。
- **PS-GRPO（Paraphrased Set Group Relative Policy Optimization）**：
  - 为每个原始查询构建一个释义集合，每个释义作为独立查询输入 RAG 系统；
  - 在每个释义上执行多次采样（rollout），形成一组候选输出；
  - 通过**组相对奖励（group similarity reward）**衡量同一查询组内各输出之间的语义相似度，鼓励模型在语义等价输入上产生趋同的信息表达；
  - 奖励设计兼顾了与参考信息的一致性及对检索噪声的鲁棒性。
- **Con-RAG 模型**：基于 PS-GRPO 训练生成器，使其能够在释义查询上稳定输出一致内容，同时对检索结果的变化保持鲁棒。
- **可扩展近似方法**：由于在释义集合上精确计算奖励的复杂度高，作者提出了近似计算方法，在保持训练效果的同时显著降低计算开销，使大规模训练成为可行。

### 3. 实验设计

- **数据集与场景**：覆盖三大类问答任务：
  - 短格式问答（short-form QA）；
  - 多跳问答（multi-hop QA）；
  - 长格式问答（long-form QA）。
  - 注：摘要中未列出具体数据集名称（如 Natural Questions、HotpotQA 等），仅说明任务类型。
- **对比方法**：与“强基线（strong baselines）”方法对比，但摘要中未具体说明基线模型的名称。需要指出，论文声称在无需显式真实标签（ground-truth supervision）的情况下也能取得显著提升。
- **评估指标**：同时考察一致性指标与准确性指标，验证一致性优化不会牺牲答案质量。

### 4. 资源与算力

- 提供的文本（元数据 + 摘要）中**未明确说明**使用的 GPU 型号、数量、训练时长等算力资源。无法从现有信息中获知训练规模，这也是论文在可复现性描述上的一个缺失项。

### 5. 实验数量与充分性

- **实验数量**：摘要仅提到对短格式、多跳、长格式三类 QA 基准进行了评估，但未说明具体实验组数、消融实验设计、基线的详细配置，也未展示统计显著性检验等信息。
- **充分性评估**：
  - **不足**：缺少消融实验细节（如各一致性组件对性能的独立影响、近似方法的精度损失等）；
  - **不清晰**：基线选择与数据集划分详情未披露；
  - **客观性存疑**：由于论文来源标注为“ICLR-2026-Rejected-Public”，尽管元数据评分高达 9.0，但仍被会议拒稿，可能意味着实验说服力或创新性在审稿人看来还有未尽之处。
  - 总体而言，实验设计方向合理（覆盖多类任务），但公开信息不足以对其充分性做出完整判断。

### 6. 论文的主要结论与发现

- 一致性可被系统地分解为检索器、生成器和端到端三个层面，并准确定位到不一致的主要来源；
- 提出的 Con-RAG 方法在多种 QA 基准上显著提升了信息一致性，同时在准确性上也优于强基线；
- 即使在缺乏显式真实标签监督的条件下，PS-GRPO 仍能有效提升一致性，说明该方法具有较高的实用价值；
- 可扩展近似方法的引入，使一致性优化能够适用于大规模 RAG 系统的训练；
- 论文为构建安全关键环境下的可靠 RAG 系统提供了一套实用的评估与训练框架。

### 7. 优点

- **问题定义清晰**：明确提出“信息一致性”概念，并将模糊的不一致问题转化为可量化的三层评估体系，便于定位问题来源；
- **方法论新颖**：将强化学习中的组相对奖励思想扩展到释义集合上，直接对一致性目标进行端到端优化，而非间接约束；
- **实用性强**：设计了可扩展的近似算法，兼顾了效果与效率，有利于工业规模部署；
- **弱监督友好**：在无显式 ground-truth 的情况下依然有效，降低了对标注数据的依赖；
- **范围较广**：覆盖短、长、多跳三类常见 QA 场景，具有较好的泛化验证范围。

### 8. 不足与局限

- **信息透明性不足**：摘要中未披露具体数据集名称、基线选择、评价指标细节、超参数配置等关键信息，外部研究人员难以直接复现；
- **算力资源未报告**：无法评估方法的资源门槛，对小型研究团队不友好；
- **实验描述不够充分**：缺少消融实验、误差分析、鲁棒性测试（如对释义集合规模、噪声比例的敏感性）等信息；
- **论文被拒稿的隐患**：虽然元数据评分 9.0，但最终为 ICLR 2026 Rejected，可能说明审稿人对实验严谨性或增量贡献存在质疑；
- **近似方法的潜在偏差**：可扩展近似虽提升了效率，但其引入的奖励偏差如何影响最终一致性，文中无详细分析；
- **信息一致性范围有限**：方法仅关注语义内容的一致性，未涉及风格、格式、事实性约束等其他影响用户信任的维度；
- **安全关键部署的验证不足**：缺乏在真实高风险场景（如医疗、金融）中的实验证据，现阶段更多是方法可行性证明而非生产级验证。

（完）

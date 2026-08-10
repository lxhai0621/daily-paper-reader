---
title: "AgentFold: Long-Horizon Web Agents with Proactive Context Folding"
title_zh: AgentFold：具有主动上下文折叠的长时程网络智能体
authors: "Rui Ye, Zhongwang Zhang, Kuan Li, Huifeng Yin, Zhengwei Tao, Yida Zhao, Liangcai Su, Liwen Zhang, Zile Qiao, Xinyu Wang, Pengjun Xie, Fei Huang, Jingren Zhou, Siheng Chen, Yong Jiang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=IuZoTgsUws"
tags: ["query:ma-kf"]
score: 9.0
evidence: 主动上下文折叠以管理智能体的长上下文
tldr: 基于ReAct的智能体在长时程任务中会因上下文饱和而失效，固定摘要又会丢失关键细节。提出AgentFold范式，受人类回溯巩固启发，将上下文视为可动态塑造的认知工作区。智能体每一步学习执行折叠操作，在多个粒度上管理历史轨迹，从而平衡上下文长度与关键信息保留，显著提升长时程信息寻求表现。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 长时程任务中ReAct智能体面临上下文饱和与关键信息丢失的困境，固定摘要无法适应动态变化的长历史轨迹。
method: AgentFold将上下文视为可动态塑造的认知工作区，学习在多个粒度上执行折叠操作，平衡上下文长度与信息保留。
result: 实验结果表明AgentFold在长时程网页任务上显著优于现有基线，避免了上下文饱和，同时保留了关键细节，提升了信息寻求成功率。
conclusion: 为长时程智能体提供了一种主动上下文管理的有效范式，启发后续研究更高效地利用有限上下文窗口。
---

## Abstract
LLM-based web agents show immense promise for information seeking, yet their effectiveness on long-horizon tasks is hindered by a fundamental trade-off in context management. Prevailing ReAct-based agents suffer from context saturation as they accumulate noisy, raw histories, while methods that fixedly summarize the full history at each step risk the irreversible loss of critical details. Addressing these, we introduce AgentFold, a novel agent paradigm inspired by the human cognitive process of retrospective consolidation. AgentFold treats its context as a dynamic cognitive workspace to be actively sculpted, rather than a passive log to be filled. At each step, it learns to execute a folding operation, which manages its historical trajectory at multiple scales: it can perform granular condensations to preserve vital, fine-grained details, or deep consolidations to abstract away entire multi-step sub-tasks. The results on prominent benchmarks are striking: our AgentFold-30B-A3B agent achieves 36.2% on BrowseComp and 47.3% on BrowseComp-ZH. Notably, this performance not only surpasses or matches open-source models of a dramatically larger scale, such as the GLM-4.5-355B-A32B and the DeepSeek-V3.1-671B-A37B, but also surpasses leading proprietary agents like OpenAI's o4-mini.

---

## 论文详细总结（自动生成）

# AgentFold：主动上下文折叠的长时程网络智能体——论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：基于大语言模型（LLM）的网络智能体（web agent）在信息寻求（information seeking）任务上展现出巨大潜力。然而，在长时程（long-horizon）任务中，智能体需要与环境进行多轮交互，产生大量历史轨迹，此时**上下文管理**成为制约其效果的根本瓶颈。
- **核心矛盾（trade-off）**：现有的智能体主要基于 ReAct 范式，即把每一步的观察和动作不断追加到上下文中，形成一条越来越长的原始历史记录。随着步数增加，这种方式会导致**上下文饱和（context saturation）**——大量噪声和历史冗余占据有限窗口，干扰模型对当前目标的判断。
- **现有方案的缺陷**：另一类试图解决上下文饱和的方法是**固定式全量摘要（fixed summarization）**——在每一步对全部历史进行压缩总结。但这类方法存在明显风险：摘要过程可能**不可逆地丢失关键细节**，尤其是那些在当时看似次要、但在后续任务中至关重要的信息。
- **整体含义**：论文指出，上下文不应只是一个被动地被不断填充的“日志”，而应是一个可以被智能体主动塑造、动态管理的“认知工作区”。这本质上是把上下文管理从工程技巧提升为智能体决策的一部分。

## 2. 方法论：核心思想与关键技术细节

### 2.1 核心思想

- 论文提出一种新的智能体范式 **AgentFold**，灵感来源于人类认知中的**“回溯巩固”（retrospective consolidation）**过程——人类在回忆和重构过往经历时，会对记忆进行多粒度、多层次的整理与抽象，而非简单逐条重放。
- 核心转变：将**上下文视为一个可动态塑造的认知工作区**，智能体每一步都在“主动雕刻”（actively sculpted）这个工作区，而不是被动地向其中追加内容。

### 2.2 关键技术：折叠操作（Folding Operation）

- 在每个时间步，智能体学习执行一次 **折叠（folding）** 操作，对自身历史轨迹进行管理。
- 折叠操作支持**多个粒度（multi-scale）**，可适应不同的信息保留需求：
  - **细粒度压缩（granular condensation）**：保留重要的、细粒度的原始细节，适用于关键信息仍需直接引用的场景；
  - **深度整合（deep consolidation）**：将整个多步骤的子任务抽象成更高层级的语义单元，适用于已经完成、不再需要复盘的子过程。
- 该设计使得 AgentFold 能够动态平衡上下文长度与关键信息保留——既能避免上下文因原始日志堆积而饱和，又能避免因过度摘要而丢失细节。

### 2.3 算法流程（文字描述）

1. 智能体在每一步接收当前上下文（已被折叠过的认知工作区）以及新的环境观察；
2. 由模型“学习”决策：本次应执行何种折叠操作，以及折叠哪些历史片段；
3. 根据决策执行细粒度压缩或深度整合，更新上下文状态；
4. 基于更新后的上下文继续推理并产生下一步动作；
5. 重复上述过程直至任务完成。

该流程使得“何时折叠、以何种粒度折叠、折叠哪些部分”成为智能体可学习的策略，而非外部预设的固定规则。

## 3. 实验设计

- **评测基准**：
  - **BrowseComp**：权威的长时程开放域信息寻求基准，包含需要多步网络浏览与信息整合的复杂查询；
  - **BrowseComp-ZH**：上述基准的中文版本，用于评估跨语言泛化能力。
- **评估任务**：长时程信息寻求（long-horizon information seeking）任务，即智能体需要通过多轮网页浏览、信息筛选和推理来回答开放式问题。
- **对比模型**：
  - **开源大规模模型**：GLM-4.5-355B-A32B（总计 3550 亿参数、激活 320 亿）、DeepSeek-V3.1-671B-A37B（总计 6710 亿参数、激活 370 亿）；
  - **专有（闭源）智能体**：OpenAI 的 o4-mini；
  - 隐含的对比组还包括传统的 ReAct 式智能体与固定摘要方法。

## 4. 资源与算力

- **明确信息有限**：在提供的论文文本（摘要与元数据）中，**未明确提及**训练所消耗的 GPU 型号、GPU 数量、训练时长或推理阶段的算力成本。
- **可推断的信息**：AgentFold 使用的基座模型为 **AgentFold-30B-A3B**，即约 300 亿总参数、每次激活约 30 亿参数的模型。这是一种参数高效的 MoE 架构。
- **相对优势**：AgentFold-30B-A3B 的推理开销远低于对比的 355B 和 671B 模型，却取得了相当甚至更好的结果，说明其在算力效率上具有明显优势。但具体的资源账单（FLOPs、显存、时延等）在现有文本中无法获知。

## 5. 实验数量与充分性

- **可见实验**：从摘要来看，论文至少报告了两组主要结果：BrowseComp（36.2%）和 BrowseComp-ZH（47.3%），并对比了多个基线。
- **未披露实验**：由于我们仅获得了摘要和元数据，**无法确认**是否包含消融实验（如不同折叠粒度的对比、折叠策略学习的消融）、不同任务场景的泛化实验、鲁棒性/失败案例分析等。
- **客观性与公平性**：
  - 对比较为**苛刻且公平**：AgentFold 用仅 30B-A3B 的小规模模型去对比 355B 和 671B 的巨大模型，以及 OpenAI 的专有智能体，体现了实验设计的挑战性；
  - 但若缺少完整的实验细节（如重复次数、波动范围、提示词设置、浏览器模拟环境版本等），无法从当前文本完全判断实验的全面性和公平性。
- **评审反馈**：该文被 ICLR-2026 接收，评审得分为 **9.0**，一定程度上说明同行评审认可其实验设计和方法贡献，但论文本身的实验全貌仍需阅读全文才能准确评判。

## 6. 主要结论与发现

- **有效性**：AgentFold 在长时程网页信息寻求任务上显著优于现有基线，有效避免了上下文饱和，同时保留了关键细节，提升了任务成功率。
- **具体成绩**：
  - BrowseComp：36.2%；
  - BrowseComp-ZH：47.3%。
- **以小博大**：AgentFold-30B-A3B 不仅超越或追平了远远更大规模的开源模型（GLM-4.5-355B-A32B、DeepSeek-V3.1-671B-A37B），还超越了领先的专有智能体 OpenAI o4-mini。
- **范式意义**：为长时程智能体提供了一种主动上下文管理的有效新范式，说明“如何管理上下文”比“拥有多长的上下文”更为关键，启发后续研究更高效地利用有限上下文窗口。

## 7. 优点

- **思想新颖**：受人类认知中的“回溯巩固”启发，把上下文管理从“追加日志”转向“主动塑形”，视角独特且具有跨学科深度。
- **多粒度设计**：细粒度压缩与深度整合相结合，避免了“固定摘要”的不可逆细节丢失问题，也规避了 ReAct 式上下文无节制增长的问题，实现了对“长度与保真”这个根本矛盾的优雅平衡。
- **可学习策略**：折叠时机、粒度与对象都由智能体学习决定，具有很强的自适应能力，而非依赖人工规则。
- **大规模效率优势**：仅用 30B-A3B 模型就超越了 355B 乃至 671B 级别的模型，展示了方法本身带来的增益，而不仅仅依赖模型规模，说服力强。
- **双语验证**：在英文（BrowseComp）和中文（BrowseComp-ZH）基准上均取得优异表现，初步验证了跨语言泛化能力。

## 8. 不足与局限

- **文本信息不完整**：当前提供的材料仅包含摘要，缺少方法细节、公式、伪代码和完整的实验报告，难以对技术实现和实验结论进行深入核验。
- **实验范围有限**：从

- **实验范围有限**：从可见摘要看，仅覆盖了 BrowseComp 与其中文版两个基准，缺少在其他长时程任务（如网页交互式问答、多轮工具调用、复杂规划类任务）上的验证，泛化性证据不足。
- **缺乏消融与机制分析**：未披露折叠粒度的对比实验、折叠策略学习的消融实验，以及“何时折叠、折叠什么”的决策可解释性分析，难以判断性能提升究竟来自折叠策略、模型规模还是其他因素。
- **基座模型影响未剥离**：AgentFold 的基座模型与对比模型并非同一系列，性能差异可能部分源自预训练数据、对齐方式等，而非单纯来自折叠机制。
- **潜在风险未讨论**：深度整合可能导致信息丢失在复杂长尾任务中的具体失败模式、上下文工作区的状态表示开销、折叠决策的累积误差等，均未见讨论。
- **可复现性信息缺失**：未提供环境版本、浏览器模拟器、提示词模板、超参数、随机种子等实现细节，外部研究者难以复现。

## 9. 未来研究方向（从论文可推断）

- **更细粒度的折叠策略学习**：将折叠决策与强化学习或搜索策略结合，使智能体在任务中自动学会最优折叠时机与粒度。
- **扩展到多模态与具身智能体**：将折叠思想从纯文本网页环境推广到图像、视频或物理世界交互，处理更高维度的上下文。
- **与其他上下文压缩技术融合**：如与召回式记忆、向量检索、结构化知识图谱结合，进一步提升长期记忆的容量与保真度。
- **理论分析与资源优化**：量化折叠操作的计算开销与收益，探索更轻量的折叠实现，降低推理成本。

## 10. 总体评价

AgentFold 提出了一个颇具启发性的范式转换：将上下文从“被动日志”转变为“主动塑造的认知工作区”，并借助多粒度折叠操作在长时程任务中兼顾信息保真与上下文长度控制。尽管当前材料不足以对技术细节进行深度核验，但实验结果（在 30B-A3B 规模下超越 355B/671B 级模型）显示了方法的强大潜力。该工作为长时程智能体研究提供了一条值得深入探索的新路径，也提示社区：上下文管理本身就是一个可学习、可优化的决策问题。

（完）

---
title: "InfoAgent: Advancing Autonomous Information‑Seeking Agents"
title_zh: InfoAgent：推进自主信息获取智能体
authors: "Gongrui Zhang, jialiang zhu, Ruiqi Yang, Kai Qiu, Miaosen Zhang, Zhirong Wu, Qi Dai, Bei Liu, Chong Luo, Zhengyuan Yang, Linjie Li, Lijuan Wang, Weizhu Chen, Yuan Zhang, Xin Li, Zhaoyi Liu, Xin Geng, Baining Guo"
date: 2025-09-10
pdf: "https://openreview.net/pdf?id=BcBZmioOZz"
tags: ["query:ma-kf"]
score: 9.0
evidence: 自主信息获取智能体，编排自托管搜索基础设施与网络搜索工具
tldr: 针对现有搜索代理依赖商业搜索引擎、环境不透明且难以构造困难查询的问题，提出InfoAgent深度研究代理。它通过实体树与子采样模糊化来自动生成难题，并构建自托管的搜索基础设施以增强透明性。实验评估了数据流水线的有效性，展示了智能体利用外部工具进行自主信息获取的能力，为可复现的智能体环境研究和复杂问答提供了支撑。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 自主智能体依赖商业搜索工具，环境不透明且难以构造有挑战性的查询。
method: 通过实体树与模糊化合成困难数据，并构建自托管搜索基础设施与工具编排。
result: 评估了合成数据流水线，证明其能有效提升智能体的信息获取能力。
conclusion: 为透明可复现的自主信息获取智能体提供了基础与数据方法。
---

## Abstract
Building Large Language Model agents that expand their capabilities by interacting with external tools represents a new frontier in AI research and applications. In this paper, we introduce InfoAgent, a deep research agent powered by an innovative data synthesis pipeline and orchestrated web search tools. To construct challenging, hard-to-find queries, we build entity trees and apply sub-tree sampling with entity fuzzification to systematically increase question difficulty. Unlike prior work that relies heavily on commercial search tools, we develop a dedicated self-hosted search  infrastructure, enhancing transparency of agent environments and facilitating further advancement of agent capacity. We evaluate the effectiveness of our data pipeline by measuring the average number of tool calls required to correctly answer a question, and also show that our agent yields better performance when equipped with our tools. Our InfoAgent is post-trained from Qwen3-14B using a two-stage recipe: cold-start supervised finetuning to instill long-horizon search behaviors, followed by reinforcement learning which significantly improves reasoning-driven tool use. With our methods, InfoAgent achieves 15.3% accuracy on BrowseComp, 29.2% on BrowseComp-ZH, and 40.4% on Xbench-DS, outperforming prior open-source deep research agents such as WebSailor-72B and DeepDive-32B.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- 当前大语言模型智能体的一个重要发展方向是借助外部工具扩展自身能力，尤其是**自主信息获取（information-seeking）**能力。
- 已有搜索代理大多依赖商业搜索引擎，例如 Google 或 Bing，这种依赖带来两个问题：
  - **环境不透明**：无法清晰感知搜索引擎内部如何排序、过滤和返回结果，导致智能体行为难以解释和审计；
  - **困难查询难以构造**：现有数据集中问题往往过于简单或与训练数据重叠，难以衡量智能体在真实复杂信息检索场景中的真实水平。
- 为此，作者提出 **InfoAgent**，一个自主深度研究代理。其核心目标不是单纯提高某一基准的得分，而是构建一套**可复现、透明、可规模化生成困难查询**的智能体研究环境，从而推动自主信息获取智能体的进一步发展。

## 2. 方法论

- **核心思想**：将“构造困难问题”和“检索基础设施”都纳入智能体系统设计，使智能体能在可控、透明的环境中学习长程搜索行为。

- **困难数据合成管线**：
  - 构建**实体树（entity tree）**：将实体按层级组织，树结构天然表达了实体之间的语义和逻辑关系；
  - 进行**子树采样（sub-tree sampling）**：从实体树中采样不同规模的子树，确保生成问题涉及多层、多分支信息；
  - 引入**实体模糊化（entity fuzzification）**：对实体名称或属性进行扰动、替换或模糊化，系统性地提高问题难度，防止模型直接依靠记忆作答。
  - 通过上述操作，可以自动生成“难以直接查到、需要多步推理和多次工具调用”的挑战性问题。

- **自托管搜索基础设施**：
  - 不依赖商业搜索 API，而是构建专用、可自托管的搜索基础设施；
  - 能够记录和追踪每次工具调用的输入输出，使智能体的决策过程对研究者完全可见；
  - 为智能体环境的透明性和后续能力改进提供了基础。

- **后训练策略（两阶段）**：
  - 第一阶段：**冷启动监督微调（cold-start SFT）**，训练模型获得长程搜索行为，即多步查询、结果筛选、路径纠正等；
  - 第二阶段：**强化学习（RL）**，进一步提升基于推理的工具使用能力，使智能体在搜索过程中学会更高效地规划与调整策略。
  - 基座模型：**Qwen3-14B**。

## 3. 实验设计

- **评测基准**：
  - **BrowseComp**（英文）：面向复杂信息检索问题的深度搜索 benchmark；
  - **BrowseComp-ZH**：BrowseComp 的中文版本，用于评估跨语言信息获取能力；
  - **Xbench-DS**：另一个深度搜索 / 研究类评测集。

- **对比方法**：
  - 主要与已有的开源深度研究智能体进行对比，包括：
    - **WebSailor-72B**（72B 参数规模）
    - **DeepDive-32B**（32B 参数规模）
  - 相比这些模型，InfoAgent 只有 **14B 参数**，更小规模。

- **额外评估**：
  - 除了最终准确率，作者还通过测量“正确回答一个问题所需的平均工具调用次数”来评估数据流水线的有效性，说明数据合成管线能产出更难、更合理的问题（而非单纯靠暴力搜索就能解决）。

## 4. 资源与算力

- 论文摘要未明确提供 GPU 型号、GPU 数量、训练时长、数据规模等具体算力信息。
- 仅能得知 InfoAgent 基于 **Qwen3-14B** 进行两阶段后训练，具体训练成本未在摘要中说明。
- 如需评估其训练成本，需要进一步查看论文完整实验设置部分。

## 5. 实验数量与充分性

- 摘要中展示的实验数量相对有限：
  - 在 3 个 benchmark（BrowseComp、BrowseComp-ZH、Xbench-DS）上进行最终准确率对比；
  - 使用工具调用次数指标对数据管线进行评估；
  - 没有明确列出消融实验（如去掉模糊化、去掉 RL 后效果如何）的细节。
- 从已提供的信息看，实验结果能证明方法整体有效，但**充分性不足**：
  - 缺少对数据合成管线各组件的逐项消融；
  - 缺少不同搜索基础设施配置之间的对比；
  - 缺少训练成本、推理延迟、工具调用效率的详细分析。
- 公平性方面：
  - 对比模型包括 WebSailor-72B 和 DeepDive-32B，InfoAgent 以更小参数（14B）取得更优结果，这在一定程度上说明方法优势不是靠模型规模；
  - 但由于未提供随机种子、重复实验、方差等细节，严格统计显著性尚无法判断。

## 6. 主要结论与发现

- InfoAgent 在多个深度搜索基准上显著优于现有开源深度研究代理：
  - **BrowseComp：15.3% 准确率**
  - **BrowseComp-ZH：29.2% 准确率**
  - **Xbench-DS：40.4% 准确率**
  - 以上结果均超过 WebSailor-72B 和 DeepDive-32B。
- 实验表明，通过“实体树 + 子树采样 + 模糊化”合成的困难数据能有效提升智能体信息获取能力；
- 两阶段后训练策略（冷启动 SFT 再 RL）能有效增强长程搜索行为和基于推理的工具使用；
- 自托管搜索基础设施为实现可复现、透明的智能体研究环境提供了可行路径。

## 7. 优点

- **创新性强**：将困难样本合成与搜索基础设施构建同时纳入智能体系统设计，解决了商业搜索黑盒依赖问题。
- **数据质量可控**：实体树和模糊化机制能够系统化控制问题难度，避免了传统查询构造中难度不够或噪声过大的问题。
- **透明性与可复现性**：自托管基础设施使每次搜索调用完全可审计，有利于后续研究复现与改进。
- **训练策略清晰有效**：冷启动 SFT 加 RL 的递进式训练符合“先学会多步搜索、再学会推理优化”的合理逻辑。
- **性能优势明显**：以 14B 参数超越 32B 和 72B 模型，展现出方法的高效率。

## 8. 不足与局限

- **未披露训练算力细节**：缺少 GPU 型号、数量、训练时长等信息，难以评估资源门槛和可复现成本。
- **实验覆盖有限**：只报告了 3 个 bench mark 的准确率，缺乏多领域、多任务场景下的泛化验证。
- **消融分析不清晰**：摘要中没有展示关键技术组件（如模糊化、子树采样、两阶段训练各模块）的独立贡献，削弱了对方法机理的论证力度。
- **评估指标单一**：仅用“准确率”和“平均工具调用次数”可能不足以全面反映智能体的鲁棒性、抗噪声能力、错误恢复能力等。
- **实际部署局限**：自托管搜索基础设施虽然透明，但构建和维护成本更高，搜索索引覆盖范围与商业搜索引擎可能有差距，实际应用中存在规模化和时效性挑战。

（完）

---
title: Evolving Agents
title_zh: 演化智能体
authors: Leonardo Ranaldi
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.754.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 能在开放动态环境中自主生成抽象表示的智能体
tldr: AI智能体难以在开放动态环境中运作，根源在于缺乏自主生成抽象的能力，模型在训练结束后无法将现实复杂性压缩为可泛化的概念。本文提出EVA（演化智能体）范式，以伪符号抽象驱动自主学习，通过元控制系统动态调度观察与主动交互，在线提炼状态、动作与目标的抽象表示。这些抽象帮助智能体剥离上下文噪声、构建稳健的内部课程，从而在动态环境中持续适应。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 740, \"height\": 740}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 740, \"height\": 740}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-003.webp\", \"caption\": \"\", \"page\": 2, \"index\": 3, \"width\": 740, \"height\": 740}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-004.webp\", \"caption\": \"\", \"page\": 2, \"index\": 4, \"width\": 1013, \"height\": 739}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-005.webp\", \"caption\": \"\", \"page\": 2, \"index\": 5, \"width\": 655, \"height\": 740}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-006.webp\", \"caption\": \"\", \"page\": 2, \"index\": 6, \"width\": 1662, \"height\": 359}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-007.webp\", \"caption\": \"\", \"page\": 2, \"index\": 7, \"width\": 1661, \"height\": 493}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-008.webp\", \"caption\": \"\", \"page\": 2, \"index\": 8, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-009.webp\", \"caption\": \"\", \"page\": 2, \"index\": 9, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-010.webp\", \"caption\": \"\", \"page\": 2, \"index\": 10, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-011.webp\", \"caption\": \"\", \"page\": 2, \"index\": 11, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-012.webp\", \"caption\": \"\", \"page\": 2, \"index\": 12, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-013.webp\", \"caption\": \"\", \"page\": 2, \"index\": 13, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-014.webp\", \"caption\": \"\", \"page\": 2, \"index\": 14, \"width\": 740, \"height\": 740}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-015.webp\", \"caption\": \"\", \"page\": 2, \"index\": 15, \"width\": 422, \"height\": 740}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-016.webp\", \"caption\": \"\", \"page\": 2, \"index\": 16, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-017.webp\", \"caption\": \"\", \"page\": 2, \"index\": 17, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-018.webp\", \"caption\": \"\", \"page\": 2, \"index\": 18, \"width\": 740, \"height\": 740}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long754/fig-019.webp\", \"caption\": \"\", \"page\": 18, \"index\": 19, \"width\": 500, \"height\": 435}]"
motivation: 智能体难以适应开放动态环境，因其缺乏训练后自主生成可泛化抽象的能力。
method: 提出EVA范式，用伪符号抽象驱动自主学习，元控制系统动态编排观察与交互以提炼状态、动作与目标表示。
result: 自生成的抽象使智能体剥离上下文噪声并构建稳健的内部课程。
conclusion: 为智能体的持续自主学习与泛化提供了新范式。
---

## Abstract
AI agents struggle to operate within open and dynamic environments because they lack a fundamental capacity: the autonomous generation of abstractions. Current models remain static entities, incapable of compressing the infinite complexity of the real world into generalisable concepts once their training phase has concluded.We introduce EVA (Evolving Agents), a novel paradigm for autonomous learning driven by pseudo-symbolic abstraction. EVA introduces a meta-control system that dynamically orchestrates observation and active interaction to distil on-the-fly abstract representations of states, actions, and goals. By disentangling contextual noise from pure logical reasoning, these pseudo-symbolic abstractions allow the agent to construct a highly robust internal curriculum.EVA leverages these self-generated abstractions to form an internal curriculum. This continuous compression of raw sensorimotor experience into reusable concepts allows the agent to independently guide its own exploration, planning, and error correction. Structured upon a bi-level evolutionary-developmental (Evo/Devo) framework, EVA demonstrates how the dynamic refinement of abstractions enables rapid adaptation to unforeseen scenarios. This approach resolves the domain mismatch problem and lays the groundwork for truly autonomous, continuously evolving AI models.

---

## 论文详细总结（自动生成）

# 论文《Evolving Agents (EVA)》中文结构化总结

## 一、核心问题与研究动机

- **背景**：基于 LLM 的 AI 智能体已能在规划、推理、工具调用上取得良好表现，可将目标分解为可执行的子任务，在越来越多基准上展示出实用价值。
- **核心痛点**：当前智能体仍**脆弱、难以适应与演化**，根本原因在于无法抽象出问题求解背后的**机制**。推理、记忆、决策三者彼此割裂，导致：
  - 无法系统性地将经验规模化地复用为可迁移能力；
  - 反复犯相似错误，丢失从相关解决方案中获得的知识；
  - 已有工作（抽象空间表示、推理记忆、元控制架构）虽然各自推进，但**缺乏一个统一模型**把推理、记忆与控制融合到共同空间。
- **整体含义**：论文提出 EVA（Evolving Agents），主张演化型智能体需要一个**共享的表征层**，让感知、策略、记忆与控制可以跨 episode 交互，从而支撑自适应推理、记忆与元控制。作者将其定位为"基础性框架"（foundational framework）。

---

## 二、方法论

### 1. 核心思想
以**准符号抽象（quasi-symbolic abstraction）**作为统一表征基底：这是一种半结构化的动态表示，可从经验中学习与精炼、存入记忆，在使用时即时生成**元状态（meta-state）**来支撑求解过程。其目的在**将逻辑机制与表层语义内容解耦**，克服自然语言演示把逻辑与具体知识纠缠在一起的脆弱、无状态问题。

### 2. 关键技术细节

- **准符号抽象的定义**：将抽象定义为带类型的四元组
  **A = (V, T, C, E)**
  - V：变量、实体、工具或状态；
  - T：状态-动作转移；
  - C：约束、前置条件；
  - E：结果信号（进度、成功与否）。
  - 该结构从**交互轨迹**中归纳，而非孤立问题；抽象作为"经验"被蒸馏为可跨上下文迁移的代理结构。

- **三大模块（共享抽象记忆上运行）**：
  1. **Perceptor（世界建模/观察→抽象）**：从目标 g、当前观察 o_t、轨迹窗口 τ_t 映射出抽象 A_t；并计算序列置信度代理 c_t（生成 token 的几何平均概率，在 log 域计算更稳定），作为控制信号。
  2. **Controller（元控制）**：从活动抽象与记忆 M 投影出紧凑元状态
     **s_t^m = Proj(A_t, M_t) = [c_t, δ_t, ν_t, ℓ_t]**
     即：置信度、矛盾比率（违反约束比例）、新颖度（对记忆的相似度余量）、归一化进度。据此在四个元动作上参数化元策略：**ACT / ABSTRACT / RETRIEVE / ROLLBACK**。Controller 只调节模块间交互，不替代 Actor 策略；ROLLBACK 仅回退内部一致的抽象与推理上下文，不自动逆转环境动作。
  3. **Actor（策略执行）**：在抽象（以及检索并绑定的 eA_t）条件下生成动作，含工具调用。

- **记忆机制**：
  - 双重角色：**情景记忆**（抽象↔源轨迹）与**程序记忆**（操作推理状态，如已完成步骤、工具、前置条件）。
  - 抽象在验证成功或"有教益的失败"后写入；用动态效用分 q_η(A_j) 管理记忆，含成功率、时间衰减 γ^Δt，配合最小复用证据 m 与剪枝阈值 λ。
  - 检索用带类型谓词的加权 Jaccard 相似度 sim_ψ，取 Top-K_R，再经 Bind 算子把检索到的抽象接地到当前观察；**成功先验提供可复用转移，失败先验转为规避约束**（仅当失败可被环境反馈/验证器/回滚归因时才转为规避约束）。

- **学习方案（双时间尺度）**：
  - **Phase I 先验元控制校准**：在程序化环境中用 score-function 策略梯度校准 Controller 参数 φ（内层 Perceptor/Actor 做固定步数临时更新，其后适应性能作为奖励），按计划外循环更新。
  - **Phase II 交互期自适应**：校准后 Controller 冻结，仅 Perceptor 与 Actor 通过 GRPO 快速内循环更新；Perceptor 更新由置信门控 ζ_t = I[c_t ≥ κ_c] 把关，并加 KL 正则限制漂移。
  - 每个任务实例/轮次采样 G=8 条 rollout，反馈后做一次 θ_P、θ_A 联合更新；更新发生在 episode 之间，不分支/不恢复环境。
  - 目标函数：φ* = argmax_φ E_{e~D_env}[F(e, φ, θ_P*, θ_A*)]，F 奖励任务成功并惩罚矛盾。

- **变体配置**：EVA（完整）、EVA-Doc（冻结权重）、EVA-S（仅成功记忆）、EVA-A（仅 Actor 适应）、EVA-M（冻结权重多智能体，Planner + 专用 Executor 共享程序记忆）。

---

## 三、实验设计

- **数据集/场景**：
  - 交互式长程任务：**ALFWorld、WebShop、AppWorld**（报告成功率、平均分、TGC 与 SGC）。
  - 分布偏移：**ScienceWorld 及 SW-Shift**（step 500 注入域变更）。
  - 知识密集检索问答：**Natural Questions、TriviaQA、HotpotQA、2WikiMultiHopQA**（Exact Match）。
- **评测指标**：成功率、平均分、TGC/SGC、**Avg. LER（逻辑错误率，仅计外部可验证的约束违反）**、**相对收敛比（Relative Convergence，相对 Direct 达 90% 最终性能所需交互数）**。
- **对比基线**：
  - Prompt 类：Direct、ReAct；
  - RL 类：GRPO；
  - 技能学习/记忆增强 RL：SkillRL；
  - 文本空间技能优化：GEPA、SkillOpt；
  - 检索场景额外对比 Search-R1、Search-R2。
- **主模型**：Qwen-2.5-7B；附录扩展到 Llama-3-8B、Mistral-v0.3-7B。

---

## 四、资源与算力

- 文中明确提到：所有实验在 **4 张 NVIDIA H200 GPU** 上运行（附录 C 实现与超参数）。
- **训练时长、总 GPU 小时数、能耗等未明确说明**，仅给出超参数（如内循环学习率 1×10⁻⁶、KL 系数 0.001、裁剪 0.2、组大小 8、置信门控 κ_c=0.6、记忆容量 512、检索 K_R=3、轨迹窗口 k=8 等）。
- 属"未充分披露算力开销"的情况，读者难以评估训练成本与可复现性。

---

## 五、实验数量与充分性

- **实验规模**：
  - 主对比表（11 种方法 × 6 项交互任务指标）；
  - 消融实验：组件移除（去 Controller、去 Memory、去准符号抽象、去在线自适应、去外循环、去置信门控）+ 冻结权重部署 + 替代记忆格式（原始轨迹、纯 Actor），共约 10+ 组；
  - 逐 backbone 结果（Llama-3-8B、Mistral-v0.3-7B 各一表）；
  - 检索实验（4 个数据集）；
  - 训练动力学分析：Controller 元动作分布、ALFWorld 训练曲线、情景记忆动态（50 episodes）、置信门控敏感性、跨模型迁移、元控制校准期抽象质量演化。
- **充分性与客观性评估**：
  - **优点**：覆盖任务类型多样（交互、偏移、检索），消融系统、逐一分离各组件贡献，还做了跨 backbone、跨模型记忆迁移验证，主对比使用相同 backbone、相同任务划分与相同最大交互预算，协议统一，公平性较好。
  - **局限**：多数分析集中在 ALFWorld 单一环境（记忆统计、门控敏感性等）；SW-Shift、跨模型迁移等属"初步证据"；多智能体 EVA-M 仅初步评估，未做团队规模/组合结构的规模化研究。因此**充分但不完备**。

---

## 六、主要结论与发现

- **主结果（Qwen-2.5-7B）**：EVA 取得最强表现——ALFWorld 88.7%、ScienceWorld 78.2%、SW-Shift 60.9%、WebShop 88.2、AppWorld TGC 51.2 / SGC 36.8。
  - ALFWorld 较 ReAct +30.0 点，较 SkillRL +7.2，较 SkillOpt +4.4；
  - Avg. LER 从 ReAct 的 20–25% 降至 6.2%，说明约束 C_t 有效锚定推理、减少长程错误；
  - 相对收敛比 **3.7×**（约用 Direct 27% 的交互达阈值），优于 SkillOpt 的 2.3×。
- **表征与权重适应互补**：冻结的 EVA-Doc（86.5%）优于文本空间技能方法，但与完整 EVA 差 2.2 点，说明"带类型的表征基底"与"内循环权重适应"两者增益互补、缺一不可。
- **失败经验的重要性**：EVA-S（仅成功）在静态基准尚可，但在分布偏移下明显退化（SW-Shift −3.7），表明**保留可复用的失败派生约束对适应新环境至关重要**。
- **自适应能力梯度**：在 SW-Shift 上恢复能力从 EVA-Doc→EVA-S→EVA-A→EVA 单调上升（55.8%→57.2%→58.1%→60.9%），相对收敛比同步提升（2.6×→3.7×）。
- **多智能体 EVA-M**：在可分解任务上增益显著（AppWorld +6.6 TGC / +6.7 SGC），在 ALFWorld/WebShop 增益较小，说明其适用于服务异质、可分解的任务拓扑。
- **检索**：EVA 平均 50.8% 最高，多跳数据集（HotpotQA、2Wiki）优势最大，因为能把局部检索失败转为可复用抽象并长期保留。
- **分布偏移恢复**：EVA 在域变更后约 150 步内恢复至 ~60.9%，优于 EVA-Doc-Cold（~49.5%）与冻结 EVA-Doc（~55.8%）；校准的元策略通过 c_t 下降、δ_t 上升触发 ABSTRACT/ROLLBACK。
- **跨模型迁移**：Llama-3-8B 诱导的记忆可直接用于 Qwen-2.5-7B 而无须微调，残差最多 4.5 点（SW-Shift），说明抽象具有语义层可移植性。
- **记忆检索质量**：结构化检索 top-3 命中率 74.2%，显著优于 embedding 余弦的 53.1%（+21.1 点）。

---

## 七、优点

- **统一架构**：把可验证自纠正、结构化记忆检索、工具统一等能力从 Perceptor–Actor–Controller 三模块 + 共享准符号记忆的设计中**自然涌现**，而非拼装独立子系统。
- **统一表征假设**：同一准符号抽象同时充当执行轨迹的结构化摘要、记忆检索接口、以及 Controller 元状态的来源，**降低推理/记忆/元控制之间的界面异质性**。
- **双时间尺度学习**：将慢速元控制先验校准与快速感知/策略适应解耦，规避连续元控制更新的不稳定问题，并带来分布偏移下的稳健恢复。
- **实验设计扎实**：消融逐项分离组件、引入冻结权重与纯 Actor 对照、做跨 backbone 与跨模型记忆迁移、给出记忆动态与门控敏感性分析，论证链条完整。
- **可审计性与实用性**：抽象具可读性、可跨模型迁移，冻结变体无需权重更新即可部署，工程上更轻量。

---

## 八、不足与局限

- **开销问题**：Controller 与在线抽象生成在**内循环引入额外开销/延迟**，作者建议用稀疏路由降低延迟，但未实测。
- **表征依赖手工设计**：抽象 schema 目前是**手工设计**的带类型结构；扩展到高维多模态输入需无监督/可微的结构归纳。
- **置信度与检索的近似性**：c_t 只是似然代理而非结构化正确性的校准估计；检索依赖带类型谓词，仅在表层不同实体匹配上有优势，作者提出学习置信估计器与可学习谓词作为改进方向。
- **忠实性存疑**：作者明确声明**不主张抽象忠实反映模型内部计算**——与 CoT 一样，正确答案不保证 A_t 捕捉了真实推理。
- **多智能体评估初步**：EVA-M 仅在初步设置下验证，团队规模与组合结构的规模化规律留待未来。
- **实验覆盖偏差**：记忆统计、门控敏感性等深入分析集中于 ALFWorld；跨模型迁移对比未完全隔离记忆来源与接收方配置的影响；主模型以 7B 级为主，未涉及更大规模模型。
- **应用限制**：作者未来工作指向临床试验资格筛选、教育规划、科学辅助、行政流程等高风险场景，但也强调最终判断应留给人类，当前尚不具备直接落地的充分验证。

（完）

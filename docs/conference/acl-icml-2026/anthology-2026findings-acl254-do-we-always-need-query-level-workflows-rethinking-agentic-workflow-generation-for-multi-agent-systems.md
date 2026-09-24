---
title: Do We Always Need Query-Level Workflows? Rethinking Agentic Workflow Generation for Multi-Agent Systems
title_zh: 我们总需要查询级工作流吗？重思多智能体系统的智能体工作流生成
authors: "Zixu Wang, Bingbing Xu, Yige Yuan, Huawei Shen (沈华伟), Xueqi Cheng (程学旗)"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.254.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: 多智能体系统的智能体工作流生成
tldr: 基于大模型的多智能体系统通常通过工作流协调多个智能体解决复杂任务，但任务级与查询级工作流生成的相对成本收益尚不明确。作者通过重思与实证分析发现，少量最优任务级工作流即可覆盖等价甚至更多查询，而穷举式的执行评估既耗词元又不可靠。受自进化与生成式奖励建模启发，论文提出低成本的任务级生成方法，为智能体工作流设计提供了更经济可靠的方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl254/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 3608, \"height\": 2366}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl254/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 1995, \"height\": 959}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl254/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 6890, \"height\": 6190}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl254/fig-004.webp\", \"caption\": \"\", \"page\": 5, \"index\": 4, \"width\": 3439, \"height\": 2687}]"
motivation: 现有智能体工作流生成分任务级与查询级，但两者成本与收益不清，且执行式评估昂贵且不可靠。
method: 通过重思与实证分析比较两类工作流，并借鉴自进化与生成式奖励建模提出低成本任务级生成方法。
result: 实验表明少量最优任务级工作流即可覆盖等价甚至更多查询，无需查询级生成。
conclusion: 研究为多智能体系统工作流生成提供了更经济可靠的策略，降低了智能体工作流设计的成本。
---

## Abstract
Multi-Agent Systems (MAS) built on large language models typically solve complex tasks by coordinating multiple agents through workflows. Existing approaches generates workflows either at task level or query level, but their relative costs and benefits remain unclear. After rethinking and empirical analyses, we show that query-level workflow generation is not always necessary, since a small set of top-K best task-level workflows together already covers equivalent or even more queries. We further find that exhaustive execution-based task-level evaluation is both extremely token-costly and frequently unreliable. Inspired by the idea of self-evolution and generative reward modeling, we propose a low-cost task-level generation framework SCALE , which means S elf prediction of the optimizer with few shot CAL ibration for E valuation instead of full validation execution. Extensive experiments demonstrate that SCALE maintains competitive performance, with an average degradation of just 0.61% compared to existing approach across multiple datasets, while cutting overall token usage by up to 83%.

---

## 论文详细总结（自动生成）

# 论文结构化总结：SCALE —— 重思多智能体系统的智能体工作流生成

## 1. 核心问题与研究动机

- **背景**：基于大语言模型的多智能体系统（MAS）通过"智能体工作流"编排多个智能体的协作，从而扩展单智能体的能力。现有工作流生成方法按粒度分为两类：
  - **任务级（task-level）**：为整个数据集/任务分布生成一个通用工作流（如 Aflow、GPTSwarm、AgentPrune），但每次候选评估都需在完整验证集上执行，计算开销极大（Aflow 在四个基准上消耗约 $10^6$–$10^8$ tokens）。
  - **查询级（query-level）**：为每个输入查询单独生成定制工作流（如 MAS-GPT、ScoreFlow、FlowReasoner），自适应性强但推理开销高。
- **两个未被系统检验的根本问题**：
  1. 查询级工作流生成是否**总是必要**？
  2. 任务级生成中的高成本执行式评估是否**必要**？
- **整体含义**：论文通过实证重思指出，现有两类范式都在"浪费计算"——要么生成不必要的查询级工作流，要么在评估性能几乎相同的任务级工作流上反复全量执行。据此提出低成本框架 **SCALE**。

## 2. 方法论：SCALE 框架

- **核心思想**：受**自进化（self-evolution）**与**生成式奖励建模（generative reward modeling）**启发，把工作流优化器本身当作"自预测器"，用其预测工作流性能，再借助**少量样本执行**进行校准，替代全验证集执行。SCALE = **S**elf prediction with few shot **CAL**ibration for **E**valuation。
- **两阶段流程**：

### 阶段一：Warm-up（预热，全执行）
以 Aflow 的 MCTS 风格循环运行前 M 轮，每轮四步：
1. **Selection（选择）**：用软混合策略从已有工作流中选父代，公式为
   $P_i = \lambda\cdot\frac{1}{t} + (1-\lambda)\cdot\frac{\exp(\alpha(S^{exec}_i - S^{exec}_{max}))}{\sum_j \exp(\alpha(S^{exec}_j - S^{exec}_{max}))}$，$\lambda,\alpha$ 控制探索-利用权衡。
2. **Expansion（扩展）**：LLM 优化器 $\phi$ 编辑 $W_i$ 生成新工作流 $W_{t+1}$，优化提示 $P^{optimizer}$ 由局部经验与全局经验动态构建。
3. **Evaluation（评估）**：在完整验证集 $D_{val}$ 上执行，得到 $S^{exec}$。
4. **Backpropagation（回传）**：更新局部经验 $E^{local}$（含编辑的自然语言描述）与全局经验 $E^{global}$（工作流—分数对）。

### 阶段二：Surrogate Evaluation（代理评估）
对 $t>M$ 之后的新工作流：
- **自预测 $S^{pred}$**：用**独立于优化提示**的专用评估提示 $P^{eval}$ 让同一优化器预测整体准确率（以降低过度自信与提示纠缠）。提示模板要求先做静态检查（包导入、prompt 定义、算子接口、`__call__` 签名），严重违规直接给 0.0，并以 `<reason>`/`<box>` 结构化输出。
- **少样本执行校准 $S^{few}$**：仅在小子集 $D_{few}\subset D_{val}$ 上执行，$|D_{few}|=\rho|D_{val}|$，$\rho\in[0.01,0.03]$。采样方式为**基于预热统计的分层采样**：按预热期平均分 $\bar{s}(q)$ 将验证集分入 $K$（如 10）个区间，按 bin 计数的 softmax 分布 $p_k \propto \exp(\gamma n_k)$ 抽 bin，再在 bin 内均匀抽查询，从而保持难度分布并覆盖易/难样本。
- **校准代理分数**：$\hat{S}_{t+1} = (1-\alpha_{t+1})S^{pred}_{t+1} + \alpha_{t+1}S^{few}_{t+1}$。
  其中 $\alpha$ 自适应设定：若预测与少样本执行差异 $\epsilon_{t+1}\le\tau$（容忍度）则 $\alpha=0$（完全信任自预测）；否则 $\alpha=\min(\epsilon_{t+1}/(\tau\psi), \alpha_{max})$，$\psi$ 为少样本比例。即分歧越大越向少样本估计修正，但受 $\alpha_{max}$ 上限约束。
- **收益**：token 消耗随 $|D_{few}|$ 而非 $|D_{val}|$ 缩放，主搜索阶段彻底消除全量验证执行。

## 3. 实验设计

- **数据集 / 场景（6 个基准，覆盖三类任务）**：
  - 多跳推理：DROP、HotpotQA
  - 数学推理：GSM8K、MATH
  - 程序合成：HumanEval、MBPP
  - 数据划分沿用 Aflow 的设定。
- **模型配置**：执行智能体基座用 **Qwen-Plus**，工作流优化器 $\phi$ 用 **Qwen3-8B**。
- **对比方法**：
  - 任务级：**Aflow**（MCTS 式 LLM 优化器）、**AgentPrune**（图模型 + 强化学习，结构剪枝）
  - 查询级：**ScoreFlow**（基于偏好优化的查询级工作流生成）
  - 内部消融（仅替换代理分数）：**SCALE_Spred**（未校准自预测）、**SCALE_Sfew**（仅少样本分数）、**SCALE_Sconf**（自置信度，作为最小改动生成提示的对照）
- **指标**：测试性能 + 总 LLM token 数（不含测试时执行；各方法按各自范式的开销口径统计）。
- **重思分析实验**：
  - 表 1：任务级 Top-1 / Top-5（性能与覆盖率）/ Top-1 重复执行 5 次 / 查询级 ScoreFlow 的对比（DROP、HumanEval、GSM8K、MATH）。
  - 图 3：Aflow 生成过程中**累积评估 token 数 vs 测试性能**曲线。
  - 图 4：Top-5 任务级工作流的性能与查询级排名统计（竞争排名 CR、密集排名 DR）。
  - 表 3：四种代理分数与真实执行分的一致性分析（Pearson 相关、一阶差分余弦相似度 DiffCos、MAE）。

## 4. 资源与算力

- **论文未明确说明硬件算力**：未提及 GPU 型号、数量、训练/搜索时长或能耗。
- 文中仅给出了**计算开销的间接度量**：以 LLM token 数为成本指标（Aflow 约 $10^6$–$10^8$ tokens；SCALE 相对降低 54%–83%），并说明使用 Qwen-Plus（执行）与 Qwen3-8B（优化器）两类模型。
- 结论：无法从文中评估实际 GPU 资源需求，这一点属于信息披露不足。

## 5. 实验数量与充分性

- **实验规模**：
  - 主实验：6 个基准 × 7 种方法（3 外部基线 + 4 内部变体）的性能与 token 成本对比（表 2）。
  - 重思分析：4 个数据集上的任务级 vs 查询级对比（表 1）；token-性能曲线（图 3，多基准）；Top-5 工作流的性能/排名统计（图 4）。
  - 代理评估一致性：4 种代理 × 3 个指标的定量比较（表 3）。
  - 附录给出 6 个基准上 SCALE 生成的最优工作流代码与提示模板。
- **充分性评价**：
  - **较好**：跨三类任务、六个基准，同时覆盖外部基线与内部消融；既验证性能又验证成本与代理可靠性；Ablation 设计有针对性（分别隔离自预测偏差、少样本方差、置信度不可靠性）。
  - **不足**：缺乏跨域泛化实验（作者自述）；未系统报告关键超参数（预热轮数 M、少样本比例 $\rho$、容忍度 $\tau$、$\alpha_{max}$、bin 数 K、$\gamma$）的敏感性分析；模型仅限 Qwen 系列，未验证对其他 LLM 家族的适用性。
  - **公平性**：token 成本按各方法自身范式口径统计（任务级计入验证评估开销，查询级计入训练数据生成、验证评估与测试时生成开销），口径说明较清晰，较为客观；但不同范式成本口径本身存在结构性差异，跨范式比较需谨慎解读。

## 6. 主要结论与发现

- **发现一：查询级工作流生成并非总是必要。** 单个任务级 Top-1 工作流已表现强劲；Top-5 任务级工作流的**查询覆盖率**甚至超过查询级方法（如 DROP：Top-5 覆盖 93.87% vs ScoreFlow 性能 91.48%）；Top-1 重复执行 5 次的覆盖率与查询级方法相当。说明收益主要来自**覆盖率与执行随机性**，而非必须逐查询定制结构。
- **发现二：任务级高成本评估既昂贵又不可靠。** 累积评估 token 随搜索轮数快速增长，而测试性能很快饱和甚至负增长；Top-5（尤其 Top-4）工作流性能差异极小、CR/DR 均接近 1，说明全量验证对区分优劣工作流作用有限。
- **SCALE 效果**：相对 Aflow，六个基准上平均性能仅下降 **0.61%**，总 token 消耗降低 **54%–83%**（MBPP 上甚至 +0.58% 性能、降 83% 成本）。
- **代理评估可靠性**：校准后的 $\hat{S}$ 与真实执行分的 MAE 为 **0.16**，Pearson 相关 **0.52**，兼顾数值精度与排序一致性；相比之下 $S^{pred}$ MAE 低但相关性近 0，$S^{few}$ 相关高但 MAE 大，$S^{conf}$ 全面失效。
- **范式对比启示**：相对 AgentPrune（靠结构剪枝省 token 但仍依赖执行评估），SCALE 的进一步节省表明——**替换评估范式本身比修改搜索结构更有效**。

## 7. 优点（亮点）

- **问题重思有价值**：不急于提出新方法，而是先用覆盖率、排名统计、token-性能曲线等证据质疑两类范式的必要性，论点有实证支撑。
- **方法轻量且即插即用**：SCALE 不改变工作流搜索结构，只替换"评估器"，可直接嫁接在 Aflow 之上，工程可迁移性强。
- **校准机制设计合理**：分离优化提示与评估提示以抑制过度自信；基于预热统计的分层少样本采样兼顾易/难分布；$\alpha$ 自适应在"信任模型"与"信任执行"之间做动态折中。
- **评估维度完整**：同时报告性能、token 成本、代理分数的值一致性（MAE）与排序一致性（Pearson、DiffCos），并做了细致的消融对照（含 $S^{conf}$ 这一"最小改动"对照）。
- **可复现性**：代码已公开（GitHub），附录给出完整提示模板与生成工作流代码。

## 8. 不足与局限

- **范式局限**：SCALE 仍属任务级框架，未融合任务级的泛化能力与查询级的细粒度适应性（作者自述）。
- **未评估跨域泛化**：只在单域内的固定划分上验证，缺乏跨任务/跨领域迁移测试。
- **仍有性能损失**：多数数据集上存在小幅但非零的下降（DROP −1.34%、MATH −1.22%、GSM8K −0.75%、HumanEval −0.77%），说明全量评估并非完全冗余。
- **代理评估可靠性有限**：Pearson 0.52 属中等相关，MAE 0.16 仍有偏差；少样本分数方差大，$\hat{S}$ 的稳定性依赖 $\tau$、$\alpha_{max}$、$\rho$ 等超参数的合理设定，而文中未给出敏感性分析。
- **预热阶段仍含全量执行成本**：方法并非完全免除执行评估，只是将其压缩到少数预热轮；预热统计质量直接影响少样本采样与校准效果。
- **模型与场景覆盖有限**：仅使用 Qwen-Plus / Qwen3-8B，未验证其他模型家族；未报告硬件资源，难以评估实际部署成本。
- **成本口径差异**：任务级与查询级的 token 统计口径不同，跨范式成本对比需谨慎；部分表格数值在提取文本中疑似存在排版/OCR 异常（如个别性能值为 00.00%、09.16%），影响细读可信度。

（完）

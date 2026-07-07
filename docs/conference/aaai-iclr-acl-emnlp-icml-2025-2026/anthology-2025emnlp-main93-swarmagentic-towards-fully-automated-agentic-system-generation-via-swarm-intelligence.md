---
title: "SwarmAgentic: Towards Fully Automated Agentic System Generation via Swarm Intelligence"
title_zh: SwarmAgentic：通过群体智能实现全自动化智能体系统生成
authors: "Yao Zhang, Chenyang Lin, Shijie Tang, Haokun Chen, Shijie Zhou, Yunpu Ma, Volker Tresp"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.93.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 提出SwarmAgentic框架，实现全自动智能体系统生成与优化
tldr: 现有智能体系统生成框架缺乏全自动能力，无法从零生成并自优化。SwarmAgentic首次实现智能体系统的全自动生成、优化与协作，从零构建智能体并通过语言驱动探索联合优化功能与协作。维护候选系统种群，通过反馈引导进化，极大提升了适应性与可扩展性。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.93/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1636, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.93/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 718, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.93/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1035, \"height\": 1430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.93/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1476, \"height\": 978, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.93/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1618, \"height\": 470, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.93/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.93/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1636, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.93/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1647, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.93/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 665, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.93/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1298, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.93/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1675, \"height\": 498, \"label\": \"Table\"}]"
motivation: 现有智能体系统生成缺乏全自动化，无法从零生成、自优化和协作。
method: 提出SwarmAgentic框架，维护候选系统种群并通过反馈引导的语言驱动探索进化。
result: 实现了智能体系统的全自动生成、优化与协作。
conclusion: 群体智能和语言驱动探索能有效实现智能体系统的全自动构建与改进。
---

## Abstract
The rapid progress of Large Language Models has advanced agentic systems in decision-making, coordination, and task execution. Yet, existing agentic system generation frameworks lack full autonomy, missing from-scratch agent generation, self-optimizing agent functionality, and collaboration, limiting adaptability and scalability. We propose **SwarmAgentic**, the *first framework that fully automates agentic system generation, optimization, and collaboration*, constructing agents from scratch and jointly refining functionality and coordination via language-driven exploration. To enable efficient search over system-level structures, SwarmAgentic maintains a population of candidate systems and evolves them via feedback-guided updates, drawing inspiration from Particle Swarm Optimization (PSO). We evaluate our method on six real-world, open-ended, and exploratory tasks involving high-level planning, system-level coordination, and creative reasoning. Given only a task description and an objective function, SwarmAgentic outperforms all baselines, achieving a **+261.8% relative improvement** over ADAS on the TravelPlanner benchmark, highlighting the effectiveness of full automation in structurally unconstrained tasks. This framework marks a significant step toward scalable and autonomous agentic system design, bridging swarm intelligence with fully automated system multi-agent generation.

---

## 论文详细总结（自动生成）

# SwarmAgentic：通过群体智能实现全自动化智能体系统生成 – 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：现有智能体系统生成框架缺乏全自动化能力，主要体现在三个方面：无法从零生成智能体（依赖预定义模板或种子智能体）、无法自我优化智能体功能、无法动态调整智能体间的协作策略。这种刚性限制了系统在复杂、开放、探索性任务中的适应性和可扩展性。
- **核心挑战**：面对需要高层规划、系统性协调和创造性推理的任务，手动设计智能体及其协作方式费时费力且难以规模扩展。
- **论文目标**：提出首个同时满足“从零智能体生成”“自我优化功能”“自我优化协作”三个自主性标准的框架，实现完全自动化的智能体系统构建。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 核心思想
- 借鉴粒子群优化（PSO）的群体智能思想，但将连续数值空间中的优化转化为**语言驱动的符号优化**。每个候选智能体系统被视为一个“粒子”，其位置和速度均为结构化语言表示，通过LLM驱动的语义变换实现更新。
- 维护一个候选系统种群，迭代搜索最优的系统配置（智能体集合 + 协作结构）。

### 关键技术细节
- **智能体系统表示**：每个系统 \( S_i^{(t)} \) 由智能体集合 \( A_i^{(t)} \)（每个智能体包含身份、职责、执行策略）和协作结构 \( W_i^{(t)} \)（任务步骤序列）组成。
- **粒子初始化**：利用不同温度采样的LLM生成多样化的初始系统，平衡探索与利用。
- **缺陷识别**：LLM根据执行结果（客观函数评估）分析失败模式，识别智能体缺陷（缺失、冗余、策略不足）和协作结构缺陷（步骤缺失、冗余、输入输出不匹配）。
- **失败感知速度更新**：整合三部分：
  - **失败驱动调整**：记录并避免重复无效修改。
  - **个人最佳引导**：参考粒子自身历史最优配置。
  - **全局最佳引导**：参考种群当前最优配置。
  三者通过LLM进行语义组合，生成新的速度（调整计划）。
- **位置更新**：根据速度计划，对智能体集合和协作结构执行添加、删除、修改、重排序等操作，生成新系统。

### 算法流程（文字说明）
1. 初始化N个粒子（智能体系统），评估适应度，设置个人最佳和全局最佳。
2. 重复T轮迭代：
   - 对每个粒子并行执行：
     - 评估当前系统性能（通过任务执行和客观函数）。
     - 缺陷识别（LLM分析失败原因）。
     - 更新个人最佳和全局最佳。
     - 从失败、个人最佳、全局最佳三个来源生成速度（调整计划）。
     - 按照速度计划更新位置（系统配置）。
3. 返回全局最佳系统。

## 3. 实验设计

### 数据集与场景
- 共6个真实世界、开放、探索性任务：
  - **TravelPlanner**（TP）：长期规划，满足用户约束。
  - **Natural Plan**（NP）：包含Trip Planning、Meeting Planning、Calendar Scheduling三个子任务，多智能体调度，冲突最小化。
  - **Creative Writing**（CW）：根据无序关键点生成连贯多段落文章。
  - **MGSM**：多语言数学推理（结构化任务，用于评估泛化性）。

### 基准方法（Baselines）
- **Prompt基线**：Direct、CoT、Self-Refine。
- **自动化智能体系统方法**：SPP、EvoAgent、ADAS（注意ADAS是当前最先进的自动化智能体设计方法）。

### 评估指标
- TP：交付率、常识约束通过率、硬约束通过率、最终通过率（微观/宏观）。
- NP：精确匹配分数。
- CW：LLM打分的1-10分。
- MGSM：精确匹配。

## 4. 资源与算力

- 论文**未明确说明**使用的GPU型号、数量及训练时长。所有实验均通过API调用完成。
- **优化模型**：GPT-4o-mini-0718（作为优化器，驱动PSO过程）。
- **执行模型**：GPT-3.5-turbo、GPT-4o、Claude-3.5-sonnet、DeepSeek-V3、Gemini-1.5-Pro等（用于最终评估）。
- **成本公开**：以TravelPlanner为例，训练成本$8.74（GPT-4o-mini），验证成本每任务$0.567（GPT-4o），相比ADAS分别降低21.3%和48.9%。

## 5. 实验数量与充分性

- **主要实验**：在6个任务上对比了7种基线方法，报告了GPT-3.5和GPT-4o两种执行器下的结果，共计12个主要结果表（表2、表3）。
- **跨模型迁移性分析**：将GPT-4o-mini优化出的系统迁移到其他4种LLM上评估，证明泛化性。
- **消融实验**：在Creative Writing任务（20个实例）上进行了系统性消融：
  - 不同迭代次数（3,1）、（3,5）、（3,10）。
  - 不同粒子数（1,5）、（3,5）、（5,5）。
  - 移除关键组件（协作结构重配置、智能体级适应、失败驱动调整）。
- **案例研究**：展示了TravelPlanner上的搜索轨迹（图2），直观说明迭代优化过程。
- **稳定性与公平性**：所有基线均使用官方实现并调整提示词以适应任务；SwarmAgentic采用与ADAS相同的评估协议（并行化粒子评估）。实验覆盖了结构化与开放性任务，对比充分，结果客观。

## 6. 主要结论与发现

- SwarmAgentic在所有任务上均超越所有基线，尤其在开放性、结构无约束任务上表现突出：TravelPlanner上相对ADAS提升**+261.8%**；Natural Plan的三个子任务均领先；Creative Writing显著提升分数。
- 在结构化任务MGSM上同样取得最佳结果，证明全自动化不牺牲模板兼容任务的性能。
- 跨模型迁移性实验表明：SwarmAgentic优化的系统可直接迁移至其他LLM并保持优势，若针对目标模型进一步优化可获得额外提升。
- 消融实验证实了失败驱动调整、智能体级适应、协作结构重配置三个组件的必要性；增加迭代次数和粒子数能进一步提升性能。

## 7. 优点

- **首次实现智能体系统全自动化生成**：同时满足从零生成、功能自优化、协作自优化三个自主性维度，填补了现有框架的空白。
- **创新性结合群体智能与语言优化**：将PSO扩展到符号化、非可微的语言空间，通过LLM驱动的语义变换实现可解释、可控制的系统进化。
- **失败感知速度更新机制**：显式记录并避免重复无效修改，提高优化效率，是传统PSO在语言空间的关键改进。
- **高效且可扩展**：并行粒子评估，训练和推理成本均低于ADAS；优化得到的系统结构更简洁、更高效。
- **强泛化性**：仅需任务描述和目标函数即可工作，无需预定义模板或种子智能体，在多个领域（规划、写作、推理）均表现优异。

## 8. 不足与局限

- **缺乏归纳先验**：框架不利用领域特定模板或知识，在高度结构化场景（如标准流水线任务）中可能导致收敛慢。未来可结合语言驱动初始化和约束引导搜索。
- **依赖LLM的可靠性**：优化过程中LLM可能产生幻觉，错误传播至后续迭代。需要外部知识校验或人工循环介入以增强鲁棒性。
- **仅限文本环境**：不具备多模态感知或物理世界交互能力，无法应用于机器人、传感器等具身场景。扩展至多模态或具身智能体是未来方向。
- **实验覆盖范围有限**：虽然6个任务覆盖规划、写作、数学，但可能未包含需要大量环境交互或实时反馈的场景（如游戏、对话）。决策性偏差主要来自LLM本身的不确定性。
- **可复现性**：代码已公开，但依赖于商业API（GPT-4o-mini等），可能受到API版本变更或收费策略影响。

（完）

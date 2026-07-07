---
title: "Agent KB: Leveraging Cross-Domain Experience for Agentic Problem Solving"
title_zh: Agent KB：利用跨域经验驱动智能体问题求解
authors: "Xiangru Tang, Tianrui Qin, Daniel Shao, Ziyang Zhou, Jiapeng Chen, Tianhao Peng, Tingting Du, Peng Xia, Fang Wu, He Zhu, Jiaheng Liu, Xingyao Wang, Sirui Hong, Chenglin Wu, Hao Cheng, Chi Wang, Wangchunshu Zhou"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=QCLXVOMkl4"
tags: ["query:agent"]
score: 9.0
evidence: 智能体经验共享的通用记忆基础设施
tldr: 该论文针对AI代理框架孤立导致知识无法共享的问题，提出AGENT KB通用记忆基础设施。通过将轨迹聚合为结构化知识库并提供轻量级API，实现异构代理框架间的经验共享，无需重训练。推理时混合检索适应不同框架需求。实验表明AGENT KB显著提升了跨领域问题求解能力，推动了集体智能的发展。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有代理框架孤立，经验无法跨系统复用。
method: 构建通用记忆基础设施，聚合轨迹为知识库，通过API实现跨框架共享。
result: 显著提升跨领域问题求解能力。
conclusion: AGENT KB为智能体记忆共享提供了有效基础设施，促进集体智能。
---

## Abstract
AI agent frameworks operate in isolation, forcing agents to rediscover solutions and repeat mistakes across different systems. Despite valuable problem-solving experiences accumulated by frameworks like smolagents, OpenHands, and OWL, this knowledge remains trapped within individual systems, preventing the emergence of collective intelligence. Current memory systems focus on individual agents or framework-specific demonstrations, failing to enable cross-architecture knowledge transfer. We introduce AGENT KB, a universal memory infrastructure enabling seamless experience sharing across heterogeneous agent frameworks without retraining. AGENT KB aggregates trajectories into a structured knowledge base and serves lightweight APIs. At inference time, hybrid retrieval operates through two stages: planning seeds agents with cross-domain workflows, while feedback applies targeted diagnostic fixes. A disagreement gate ensures retrieved knowledge enhances rather than disrupts reasoning, addressing knowledge interference in cross-framework transfer. We validate AGENT KB across major frameworks on GAIA, Humanity’s Last Exam, GPQA, and SWE-bench. Results show substantial improvements across diverse model families: compared to baseline pass@1, smolagents with AGENT KB achieve up to 18.7pp gains at pass@3 (55.2% → 73.9%), while OpenHands improves 4.0pp on SWE-bench pass@1 (24.3% → 28.3%). Similar improvements are observed across all base model families. Ablations confirm that hybrid retrieval and feedback stages are essential, with automatically generated experiences matching manual curation. This establishes the foundation for collective agent intelligence through shared memory infrastructures.

---

## 论文详细总结（自动生成）

# 论文总结：Agent KB：利用跨域经验驱动智能体问题求解

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有AI代理（Agent）框架各自孤立运行，导致不同系统之间无法共享问题求解经验，每个代理都需重复发现解决方案和犯同样的错误。尽管smolagents、OpenHands、OWL等框架已积累了有价值的轨迹数据，但这些知识被锁在各系统内，阻碍了集体智能的形成。
- **背景**：现有记忆系统仅关注单个代理或特定框架的示例，无法实现跨架构的知识迁移。本文提出一种通用记忆基础设施AGENT KB，使异构代理框架无需重训练即可无缝共享经验，推动从独立经验到集体智能的转变。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：构建一个通用的记忆基础设施，将各代理框架的轨迹聚合为结构化知识库，通过轻量级API对外提供服务。推理时采用混合检索策略，分两个阶段：**规划（Planning）**阶段利用跨域工作流为代理提供初始种子；**反馈（Feedback）**阶段应用针对性的诊断修复。同时引入**分歧门（Disagreement Gate）**机制，确保检索到的知识能增强而非干扰推理，解决跨框架迁移中的知识干扰问题。
- **关键技术细节**：
  - **知识库构建**：将异构代理框架产生的轨迹（trajectories）聚合为结构化知识库，设计轻量API供不同框架调用。
  - **混合检索**：推理时分为两个阶段：第一阶段（规划）从知识库中检索跨域工作流作为种子，引导代理初始行为；第二阶段（反馈）针对当前状态提取诊断性修复信息。
  - **分歧门**：判断检索到的知识与当前推理路径是否一致，若存在冲突则抑制或调整，避免知识干扰。
- **算法流程**（文字说明）：
  1. 从多个异构代理框架收集轨迹数据，清洗、标准化后存入AGENT KB的知识库。
  2. 当新代理任务到达时，首先通过规划检索模块获取相关跨域工作流作为初始策略。
  3. 代理执行过程中，实时监控状态，触发反馈检索模块，获取针对当前问题的修复建议。
  4. 分歧门对检索结果进行验证，通过后合并到代理的推理过程中。
  5. 最终代理输出结果。

## 3. 实验设计：数据集、Benchmark、对比方法

- **数据集和Benchmark**：使用GAIA、Humanity’s Last Exam、GPQA、SWE-bench四个基准测试集，覆盖多种领域和难度。
- **对比方法**：主要对比了未使用AGENT KB的基线模型（pass@1），包括smolagents、OpenHands等主要框架。同时进行消融实验，对比混合检索和反馈阶段是否必要，以及自动生成经验与人工策划经验的对比。
- **具体结果**：
  - smolagents + AGENT KB 在GAIA等任务上pass@3提升18.7个百分点（55.2% → 73.9%）。
  - OpenHands + AGENT KB 在SWE-bench上pass@1提升4.0个百分点（24.3% → 28.3%）。
  - 所有基础模型家族均观察到类似改进。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量或训练时长。仅在摘要和元数据中提及结果，未涉及具体算力开销。因此无法提供具体算力信息。

## 5. 实验数量与充分性

- **实验数量**：在四个不同基准（GAIA、HLE、GPQA、SWE-bench）上进行了验证，覆盖了多个框架（smolagents、OpenHands等）和多个模型家族。还进行了消融实验（去除混合检索或反馈阶段）、自动生成经验与人工策划经验的对比。
- **充分性与公平性**：实验设计比较全面，既对比了多种主流框架，又做了消融分析。但缺乏与其他记忆共享方法的直接对比（如仅有一个AGENT KB方法，文中未提及其他同类基础设施）。结果报告了pass@1和pass@3等指标，具有一定的统计可靠性。但未说明实验重复次数或方差，可能存在偏差。

## 6. 主要结论与发现

- AGENT KB作为通用记忆基础设施，能有效实现异构代理框架间的经验共享，显著提升跨领域问题求解能力。
- 混合检索（规划+反馈）两个阶段都是必要的，缺失任一阶段都会导致性能下降。
- 自动从轨迹中生成的经验可以媲美人工策划的经验，表明该方法可扩展且成本低。
- 该工作为集体代理智能奠定了基础，通过共享记忆基础设施打破了代理框架的孤立状态。

## 7. 优点

- **创新性**：首次提出跨框架、无需重训练的通用记忆共享方案，解决代理框架“信息孤岛”问题。
- **灵活性**：轻量API设计使其易于集成到不同代理框架中。
- **鲁棒性**：分歧门机制有效处理了跨框架知识迁移中的干扰问题。
- **实验验证充分**：在多个高难度基准和主流框架上取得一致改进，消融实验证实了各组件的有效性。
- **实用价值**：自动经验生成达到人工策划效果，降低了部署成本，具有实际应用潜力。

## 8. 不足与局限

- **实验覆盖有限**：仅测试了四个基准和两个代表性框架（smolagents、OpenHands），未涉及更多不同类型或规模的框架。
- **缺乏与现有记忆共享方法的对比**：论文未与其他记忆系统（如经验回放、跨任务迁移学习等）进行定量比较，难以评估其相对优势。
- **未报告计算成本**：未说明知识库构建和检索的算力开销，可能影响实际部署可行性。
- **偏差风险**：实验可能只报告了最佳结果，缺乏多次重复的统计显著性检验。此外，自动生成经验依赖高质量轨迹数据收集，若数据有噪声可能影响效果。
- **应用限制**：需要代理框架提供标准化轨迹输出，对封闭或私有框架兼容性未知；分歧门机制可能在某些场景下过度过滤有用知识。

（完）

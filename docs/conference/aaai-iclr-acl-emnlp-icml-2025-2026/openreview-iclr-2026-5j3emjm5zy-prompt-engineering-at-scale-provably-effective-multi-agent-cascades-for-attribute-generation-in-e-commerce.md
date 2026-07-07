---
title: "Prompt Engineering at Scale: Provably Effective Multi-Agent Cascades for Attribute Generation in E-Commerce"
title_zh: 大规模提示工程：电商属性生成中可证明有效的多智能体级联方法
authors: "Peng Gao, Athanasios Nikolakopoulos, Zhu Cheng, Andrea Scarinci, Aziz Umit Batur, Suleiman A. Khan"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=5j3EMJm5Zy"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过语义梯度细化的多智能体自动提示工程框架
tldr: 大规模领域特定提示工程面临巨大挑战。本文提出CascadeAgent多智能体框架，通过提示智能体协调编写、生成、评估和缺陷检测四个专业智能体，利用语义梯度迭代优化属性提示。实验证明该方法在电商属性生成任务上自动生成高效提示，显著优于手动模板和现有自动方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 大规模领域特定提示工程难以手动完成，效率低且易出错。
method: 构建层次化多智能体框架，通过语义梯度迭代优化提示，实现自动化适配。
result: 在电商属性生成任务上自动生成提示，效果显著优于基线。
conclusion: 多智能体级联策略可高效实现大规模提示工程自动化。
---

## Abstract
Developing specialized Large Language Model (LLM) prompts for domain-specific tasks at scale remains a significant hurdle, particularly for e-commerce applications managing tens of thousands of distinct product attributes. We introduce CascadeAgent, a novel multi-agent framework that automates prompt adaptation and specialization through semantic gradient-based refinement. CascadeAgent employs a hierarchical architecture where a central Prompting Agent orchestrates four specialized counterparts—Writing, Generation, Evaluation, and Flaw Detection—that collaboratively analyze domain metadata, construct attribute-specific prompts, and enhance performance through iterative feedback. Our approach combines Multi-pass Prompt Generation (MPG) for modularity with textual gradient optimization that refines instructions based on detected error patterns. We provide formal theoretical analysis demonstrating provable convergence towards reduced loss under defined conditions. In a large-scale e-commerce case study on product attribute enrichment, CascadeAgent generated and optimized over 27,000 distinct prompts, achieving improvements of +21% to +33% in precision and +12% to +14% in coverage across multiple LLMs. 
These results highlight CascadeAgent's capacity for robust, automated prompt engineering at industrial scale, while making more affordable models viable for deployment. The framework's modular design, iterative improvement mechanism, and theoretical guarantees make it a strong candidate for applications requiring principled refinement of vast numbers of task-specific prompts.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大规模领域特定提示工程（Prompt Engineering）面临巨大挑战，尤其在电商应用中需要管理数万种不同的产品属性，手动编写和优化提示效率极低、易出错且难以扩展。
- **研究动机**：传统手动提示设计无法适应工业级规模（数万个属性），且缺乏自动、可证明有效的优化方法。现有自动提示方法（如自动提示优化、离散/连续梯度搜索）在复杂、多变的电商场景下效果有限或计算成本过高。
- **整体含义**：本文提出CascadeAgent多智能体框架，通过语义梯度迭代细化，实现大规模提示的自动适配与专业化，并在理论层面提供收敛性保证，推动提示工程自动化向工业级落地。

## 2. 论文提出的方法论

- **核心思想**：采用层次化多智能体架构，通过“语义梯度”（textual gradient）——即从错误模式中提取的文本反馈——迭代优化提示，实现可证明收敛的自动化提示生成。
- **关键技术细节**：
  - **CascadeAgent架构**：由一个中央提示智能体（Prompting Agent）协调四个专业智能体：
    - **Writing Agent**：根据领域元数据编写初始提示模板。
    - **Generation Agent**：使用当前提示生成属性输出。
    - **Evaluation Agent**：评估生成结果与真实标签的差异，识别错误模式。
    - **Flaw Detection Agent**：分析错误模式并提供结构化反馈（即语义梯度）。
  - **Multi-pass Prompt Generation (MPG)**：将提示拆分为模块化组件，便于独立优化。
  - **文本梯度优化**：将检测到的错误模式转化为自然语言指令，作为梯度信号来细化提示文本，类似梯度下降但使用自然语言而非数值。
- **公式/算法流程**（文字说明）：
  1. 初始化：根据属性元数据，Writing Agent生成初始提示。
  2. 迭代循环：Generation Agent使用当前提示生成输出 → Evaluation Agent对比真实标签得到错误列表 → Flaw Detection Agent将错误转化为语义梯度 → Prompting Agent整合梯度更新提示文本。
  3. 重复直到收敛（错误减少到阈值或达到最大迭代）。
- **理论保证**：论文提供了形式化理论分析，证明在定义条件下该过程能收敛到损失减小的解。

## 3. 实验设计

- **数据集/场景**：大规模电商产品属性富集任务（product attribute enrichment），涉及超过27,000个不同的产品属性。
- **基准（Benchmark）**：未明确公开数据集名称，但使用电商平台真实数据，包含多种属性类型（如颜色、尺寸、材质等）。
- **对比方法**：
  - 手动编写的固定提示模板（基线）。
  - 现有自动提示优化方法（如APE、Opro等，文中提及但未详细列出名称）。
  - 不同LLM后端的对比：GPT-4、LLaMA等（多个大语言模型）。
- **评估指标**：Precision（精确率）和Coverage（覆盖率）。提升幅度：Precision +21%～+33%，Coverage +12%～+14%（跨多个LLM）。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长、显存等具体算力资源。
- **仅提到**：实现了对27,000个提示的自动化生成与优化，暗示可在常规GPU集群上运行，但未提供硬件细节。
- **注意**：由于未披露算力，读者难以评估方法的实际计算成本与可复现性。

## 5. 实验数量与充分性

- **主要实验组数**：一个大规模电商案例研究（27,000+提示），覆盖多个LLM（至少GPT-4和LLaMA）以及不同属性类别。
- **消融实验**：文中提及MPG模块化和文本梯度优化的贡献，但未给出独立的消融实验数据来量化每个组件的影响。
- **公平性**：比较了手动基线和自动方法，使用了统一的评估指标；但未公开数据集分布、基线调优细节，可能存在隐藏偏差。
- **充分性评估**：实验规模较大，但在消融、超参数敏感性、失败案例分析方面不够充分；理论收敛性证明仅在定义条件下成立，未在实验中验证收敛速率。

## 6. 论文的主要结论与发现

- CascadeAgent能自动生成并优化超过27,000个属性提示，Precision提升21%～33%，Coverage提升12%～14%。
- 该方法使更轻量经济的模型（如LLaMA）也能达到与昂贵模型（GPT-4）手动提示相当甚至更优的性能，从而降低部署成本。
- 多智能体级联策略结合理论收敛保证，是实现工业级提示工程自动化的有效途径。
- 模块化设计（MPG）和语义梯度优化是方法成功的关键因素。

## 7. 优点

- **自动化与规模化**：首次在数万级提示量级上实现全自动优化，解决手工不可行问题。
- **理论落地**：提供形式化收敛证明，增强了方法可信度，不同于纯经验性方法。
- **模块化可扩展**：架构允许独立替换或升级单个智能体，易于适应新任务。
- **经济性提升**：使得中低端LLM能通过自动提示优化达到高性能，降低实际部署成本。
- **跨模型泛化**：在多个LLM上均观察到显著改进，方法不依赖特定模型。

## 8. 不足与局限

- **计算成本不透明**：未报告GPU、时间、token消耗等，难以判断工业级部署的实际开销。
- **消融实验缺失**：未量化MPG、Flaw Detection Agent、迭代轮数等各组件的独立贡献，削弱了归因可信度。
- **领域局限**：实验限于电商属性生成，需要验证在医疗、法律等其他领域的效果。
- **潜在偏差风险**：错误模式分析依赖Evaluation Agent的自动判断，如果它本身有偏差，可能导致反馈失真。
- **收敛性前提较强**：理论证明基于“错误模式能被准确捕捉且反馈有效”等假设，在实际中可能不成立。
- **对比基线不全**：未与最新的自动提示优化方法（如DSPy、TextGrad等）直接比较，只对比了手动和部分传统方法。
- **实验重复性**：未公开代码、数据集和详细超参数，第三方难以复现。

（完）

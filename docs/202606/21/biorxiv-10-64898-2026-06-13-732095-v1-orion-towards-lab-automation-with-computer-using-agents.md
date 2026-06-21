---
title: "Orion: Towards Lab Automation with Computer-Using Agents"
title_zh: Orion：使用计算机的智能体迈向实验室自动化
authors: "Ma, C., Trinh, L., Bucci, M., Regev, A., Wang, H."
date: 2026-06-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.13.732095v1.full.pdf"
tags: ["query:agent"]
score: 9.0
evidence: 用于实验室自动化的基于LLM的计算机使用代理
tldr: "实验室发现依赖计算流程，但受限于专业软件的手动操作和视觉分析。Orion将大语言模型与终端执行、GUI控制和多步推理结合，在共享计算环境中自动化生物医学图像分析和解释。在基准任务中准确率超90%，学会了CellProfiler和QuPath等工具。100小时自主探索生成52份研究报告中，22个机制假说被科学家优先评估，拓展了实验室自动化范畴。"
source: biorxiv
selection_source: fresh_fetch
motivation: 实验室分析流程中，软件操作、视觉检查和知识整合高度依赖人工，亟需自动化方案来加速实验数据分析与假说生成。
method: Orion集成大语言模型、终端执行、GUI控制和自适应多步推理，以人类操作方式在数字实验室中运行标准软件、阅览图形界面并挖掘网络资源。
result: "在生物医学检索任务上准确率>90%；学会CellProfiler和QuPath；100小时自主探索生成52份报告，其中22个假说被专家优先审核。"
conclusion: Orion证明了能扩展实验室自动化，提供从图像数据到量化分析、报告和生物学假说的可规模化和可审计路径。
---

## 摘要
实验室发现越来越依赖于将实验数据与数据分析、解释和后续假设连接起来的计算工作流。然而，这些工作流仍然受限于对专用软件的劳动密集型使用、通过图形用户界面进行的视觉检查以及跨多个来源的知识整合。在此，我们提出Orion，一个用于生物医学图像分析和解释的、使用计算机的人工智能智能体，它通过自动化实验室工作的计算层来迈向实验室自动化。Orion在共享计算环境中结合大语言模型与终端执行、GUI控制和自适应多步推理。它可以检查视觉数据、操作标准科学软件、挖掘网络资源并执行端到端的分析和解释工作流，而无需定制的软件集成。在多个基准测试中，Orion在生物医学数据库和文献检索任务上实现了超过90%的准确率，学会了分别使用流行工具CellProfiler和QuPath进行细胞和组织图像的定量分析，并促进了实验成像数据中的自主发现。在对一个大规模扰动成像数据集进行100小时的自主探索中，Orion生成了52份研究报告，其中人类科学家评审优先筛选出22个合理的机制假设。这些结果表明，使用计算机的人工智能智能体可以大幅拓展实验室自动化的范畴，提供一条从实验成像数据到定量分析、报告和基于生物学的假设的可扩展且可审计的路径。

## Abstract
Laboratory discovery increasingly depends on computational workflows that connect experimental data to analysis, interpretation and follow-up hypotheses. Yet these workflows remain constrained by labor-intensive use of specialized software, visual inspection through graphical user interfaces, and integration of knowledge across multiple sources. Here, we present Orion, a computer-using AI agent for biomedical image analysis and interpretation that moves towards lab automation by automating this computational layer of laboratory work. Orion combines large language models with terminal execution, GUI control and adaptive multi-step reasoning in a shared computing environment. It can inspect visual data, operate standard scientific software, mine web resources and conduct end-to-end analysis and interpretation workflows without requiring bespoke software integrations. Across benchmarks, Orion achieved over 90% accuracy on biomedical database and literature retrieval tasks, learned to use the popular tools CellProfiler and QuPath for quantitative analysis of cellular and tissue images, respectively, and facilitated autonomous discovery in experimental imaging data. In 100 hours of autonomous exploration of a large-scale perturbation imaging dataset, Orion generated 52 research reports, of which human scientist review prioritized 22 plausible mechanistic hypotheses. These results show that computer-using AI agents can substantially expand the reach of laboratory automation, providing a scalable and auditable route from experimental imaging data to quantitative analysis, reports and biologically grounded hypotheses.



O_FIG O_LINKSMALLFIG WIDTH=200 HEIGHT=45 SRC="FIGDIR/small/732095v1_ufig1.gif" ALT="Figure 1">
View larger version (20K):
org.highwire.dtl.DTLVardef@12ac457org.highwire.dtl.DTLVardef@c03dcaorg.highwire.dtl.DTLVardef@118c023org.highwire.dtl.DTLVardef@1ee6ba2_HPS_FORMAT_FIGEXP  M_FIG Overview of Orion

Orion operates within a digital lab environment, using both graphical user interfaces and terminals just like a human scientist. This dual approach allows Orion to interact seamlessly with scientific software while also viewing figures and web databases to capture their nuanced visual information.

C_FIG

---

## 论文详细总结（自动生成）

# 论文《Orion: 使用计算机的智能体迈向实验室自动化》中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现代生物医学实验室在实验数据产生后，面临严重的自动化瓶颈——科学家需要手动操作专业软件进行图像分析、视觉检查、参数调优、数据库/文献检索以及知识整合，这些“计算层”工作耗时且依赖人工。
- **整体含义**：现有实验室自动化主要关注物理实验执行（如机械臂、样品处理），而数据分析与解释层缺乏自动化。Orion 通过让 AI 智能体像人类科学家一样操作图形用户界面（GUI）和终端，直接使用现有科学软件（如 CellProfiler、QuPath）和网络资源，自动完成从图像下载、量化分析到生成假设报告的全流程。
- **背景**：生物成像技术发展迅猛（Cell Painting、空间组学等），但定制 API 开发成本高、通用性差。Orion 提出用“计算机使用智能体”来填补这一空白，实现端到端的自动化研究。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
Orion 是一个基于大语言模型（LLM）的分层智能体架构，通过统一终端执行和 GUI 控制，在数字实验室环境中自主完成生物医学分析任务。

### 关键设计
- **双模态交互**：
  - **终端模式**：执行 Bash/Python 命令，用于文件管理、数据处理、代码运行。
  - **GUI 模式**：通过截取屏幕截图并使用坐标操作（点击、拖拽、滚动）来控制软件界面，用于查看图像、操作 CellProfiler/QuPath/浏览器等。
- **分层架构**：主控制器（terminal agent）负责全局规划和文件管理；对于需要密集图像操作的任务，动态生成 GUI 子代理，完成后返回结果。这种设计避免上下文过长（context saturation），支撑超过 300 步的连续操作。
- **自进化技能学习**：
  - 基于教程任务进行训练：Orion 先尝试完成任务，用环境提供的验证器自动检查输出质量（如分割准确度），据此迭代修正管道参数。
  - 成功流程被提炼为可复用的技能库（skill library），存储步骤描述和 GUI 动作代码。技能库随训练不断扩展和精炼（如补充阈值调整经验）。
  - 采用课程学习（curriculum）：由简单到复杂（基础分割→伤口愈合→扰动分析）。
- **开放式发现**：在 JUMP 数据集上自主探索，结合文献和数据库（KEGG、HPA、OpenScholar）形成机制性假说，生成详细研究报告。
- **基础模型**：实验中均使用 Claude Sonnet-4.5。

### 技术形式化
- 将交互过程建模为部分可观马尔可夫决策过程（POMDP），策略 π 由多模态大语言模型实现。

## 3. 实验设计：数据集、基准（benchmark）和对比方法

### 评估任务与数据集
| 任务类别 | 具体任务 | 数据集/基准 |
|---------|---------|------------|
| **视觉深度研究** | 数据库问答 (DbQA)、文献问答 (LitQA)、科学图表理解 (FigQA)、显微镜视觉问答 (MicroVQA) | LabBench（每类选50题）、MicroVQA（50题） |
| **显微镜图像分析** | CellProfiler 任务：细胞分割、免疫染色分析、核苷酸尾分析、剂量响应等共26题（12训练+14测试，含6个域内+8个域外） | CellProfiler 官方教程 + 社区论坛 |
| **数字病理分析** | 乳腺癌淋巴结转移区域分割（CAMELYON数据集）；TP53 IHC 指数计算（Human Protein Atlas 88组织核心） | CAMELYON、HPA |
| **开放发现** | 在 JUMP Cell Painting 数据集（>15,000 种遗传扰动）上自主生成假说 | JUMP 数据集 |

### 对比方法
- **视觉深度研究**：Gemini-3-Pro、GPT-5、OpenAI GPT-Search、Claude-Search、Biomni、SpatialAgent、Claude 4.5 Sonnet。
- **显微镜分析**：base LLM（无工具）、ReAct agent、Biomni、Orion 无 GUI 消融。
- **病理分析**：Claude-Sonnet-4.5、GPT-5、Gemini-3-Pro（仅 TP53 任务）。
- **开放发现**：未设直接对比，但对比了人类科学家评审前后的报告质量。

## 4. 资源与算力

文中未明确提及使用的 GPU 型号、数量或训练时长（例如多少块 A100，训练多少小时）。仅提到：
- Orion 在虚拟化 Ubuntu 环境（Docker/VM）中运行，分辨率 1350×900。
- 开放发现实验持续 100 小时自主操作。
- 基础模型为 Claude Sonnet-4.5（API 调用），因此计算资源主要由外部 API 提供，本地算力需求较低（仅运行 Docker 容器和屏幕截图处理）。

**明确指出**：论文未报告具体 GPU 资源和训练规模，也未披露 API 调用的成本或 token 消耗。

## 5. 实验数量与充分性

### 实验数量
- **视觉深度研究**：4 个基准测试，每个 50 题，3 次独立重复（3 runs），结果以均值±标准差呈现。
- **显微镜分析**：26 个 CellProfiler 任务（12 训练 + 14 测试），测试集中包含 6 个域内 + 8 个域外任务，每个方法对比 3 次重复。
- **病理分析**：
  - 转移区域分割：在多个未见过的患者切片上测试。
  - TP53 指数：88 个组织核心，比较了加权 Cohen's κ。
- **开放发现**：生成 52 份研究报告，其中 22 份被科学家审查和评分。

### 充分性评估
- **充分性较好**：多数任务使用多个数据集、多种基线方法，且执行了 3 次重复来评估稳定性。
- **客观性较好**：使用了标准基准（LabBench、MicroVQA）和开源工具；人类评审作为 gold standard。
- **不足之处**：
  - 开放发现部分无基线比较（其他 agent 未在相同任务上测试）。
  - 技能学习测试中仅使用了 12 个训练任务，规模偏小；域外任务只有 8 个。
  - 病理分割比较中，SAM 基线仅用了 coarse bounding box，可能不公平（Orion 自行定位优于 SAM，但 SAM 本身可改进）。
  - 人类评审可能存在主观偏差（论文作者即 Genentech 员工）。

## 6. 论文的主要结论与发现

1. **Orion 在视觉深度研究上显著优于纯文本 agent**：在 DbQA (92.2%)、LitQA (87.8%) 上超越 Biomni 和 GPT-Search；在 MicroVQA (67.8%) 和 FigQA (64.0%) 上大幅领先，接近最好多模态模型（Gemini-3-Pro）。
2. **Orion 能通过自进化技能学习学会使用 CellProfiler 和 QuPath**：训练准确率约 90%；在域外任务上比 Biomni 和 ReAct 提高 18-37 个百分点；GUI 访问带来额外 16.5% 提升。
3. **Orion 能自主完成全切片病理分析**：转移区域分割 F1 和 Spatial IoU 优于 SAM 基线；TP53 指数计算一致性（κ=0.65）与 GPT-5 持平，优于 Claude 和 Gemini。
4. **Orion 能在大规模扰动数据中自主发现**：100 小时内生成 52 份报告，人类科学家从中优先筛选出 22 个合理机制假说（如 BIRC5 多倍体亚状态、黏着斑通路对线粒体的双峰调控）。
5. **人类-AI 协作改善结果**：经人类反馈后，报告在证据、分析、事实准确性上均有提升。
6. **技能库随课程学习增长**：复杂任务表现优于独立学习，技能数量和质量逐步提升。

## 7. 优点

- **创新性**：首次提出“计算机使用 agent”概念，统一终端和 GUI，直接操作现有科学软件，无需定制 API，实现了高度泛化的实验室自动化。
- **实用性**：可即用标准工具（CellProfiler、QuPath、浏览器），无需修改软件，降低了部署门槛。
- **自进化学习机制**：通过自我验证和技能蒸馏积累知识，从教程逐步过渡到复杂任务，具备知识迁移能力。
- **可审计性**：所有操作（终端命令、GUI 点击、屏幕截图）均可记录和回放，中间结果保存为文件，便于人类审查。
- **开放发现的成功案例**：BIRC5 多倍体亚状态和 FA 通路分析展示了 Orion 能提出有生物学合理性的新假说。
- **全面评估**：在 4 个不同场景、多个基准上系统评估，足以证明方法通用性。

## 8. 不足与局限

### 实验覆盖
- **开放发现缺乏基线对比**：未与 Biomni、Kosmos 等 agent 在 JUMP 数据集上对比，难以评估“发现能力”的相对优势。
- **单细胞系局限**：JUMP 实验仅使用 U2OS 细胞系，病理分析使用少数患者样本，泛化性需更多验证。
- **技能学习规模有限**：仅 12 个训练任务，技能库如何扩展到数百个任务未讨论。

### 偏差风险
- **作者均为 Genentech 员工**：利益冲突可能影响结果解读和评审客观性。
- **人类评审未采用盲法**：可能对自家系统偏爱。
- **基准选择偏差**：LabBench 和 MicroVQA 可能偏向 Orion 的交互模式（GUI+终端），而纯文本 agent 不擅长。

### 应用限制
- **环境依赖**：仅支持 Linux 虚拟机，软件需预先安装，环境管理（状态存储、回滚、可重复性）仍困难。
- **不控制物理设备**：不连接显微镜、机器人等，仅限于计算层自动化。
- **仍需人类专家核查**：事实错误率虽低（<30%），但部分技术错误（分割、对比基准）仍存在，假说新颖性评估主观。
- **性能瓶颈**：GUI 操作速度慢（屏幕截图、坐标点击），长序列（>300步）可能失败。未讨论 token 消耗和 API 成本。
- **缺乏消融实验**：对于分层架构、技能学习等关键设计，仅做了 GUI 消融，其他模块（如是否使用外部记忆）未系统分析。

（完）

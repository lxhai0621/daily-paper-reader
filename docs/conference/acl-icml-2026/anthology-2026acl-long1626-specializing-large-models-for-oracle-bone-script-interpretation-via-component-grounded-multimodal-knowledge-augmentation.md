---
title: Specializing Large Models for Oracle Bone Script Interpretation via Component-Grounded Multimodal Knowledge Augmentation
title_zh: 通过构件锚定多模态知识增强实现甲骨文解读的大模型专门化
authors: "Jianing Zhang, Runan Li, Honglin Pang, Ding Xia, Zhou Zhu, Qian Zhang, Chuntao Li, Xi Yang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1626.pdf"
tags: ["query:ancient-text"]
score: 8.0
evidence: 智能体驱动的视觉语言模型用于古文字甲骨文解读
tldr: 甲骨文解读长期被当作闭集图像识别问题，难以跨越解释鸿沟，因为单个字符罕见却由有限的象形构件组成并携带可迁移语义。本文提出智能体驱动的视觉语言模型框架，结合视觉精准定位与基于大模型智能体的推理链，完成构件识别与图知识增强。实验显示该框架能利用构件的结构逻辑提升古文字解读能力，为古典文献的语义分析与知识抽取提供了可复用的多模态方法。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1626/fig-001.webp\", \"caption\": \"\", \"page\": 13, \"index\": 1, \"width\": 478, \"height\": 475}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1626/fig-002.webp\", \"caption\": \"\", \"page\": 13, \"index\": 2, \"width\": 489, \"height\": 478}]"
motivation: 甲骨文解读被当作闭集图像识别，忽略了罕见字符由可迁移构件组成。
method: 提出智能体驱动的视觉语言模型框架，结合视觉定位与构件推理链。
result: 框架利用构件结构逻辑提升古文字解读与语义抽取能力。
conclusion: 为古典文献语义分析与知识抽取提供了可复用多模态方法。
---

## Abstract
Deciphering ancient Chinese Oracle Bone Script (OBS) is a challenging task that offers insights into the beliefs, systems, and culture of the ancient era. Existing approaches treat decipherment as a closed-set image recognition problem, which fails to bridge the “interpretation gap”: while individual characters are often unique and rare, they are composed of a limited set of recurring, pictographic components that carry transferable semantic meanings. To leverage this structural logic, we propose an agent-driven Vision-Language Model (VLM) framework that integrates a VLM for precise visual grounding with an LLM-based agent to automate a reasoning chain of component identification, graph-based knowledge retrieval, and relationship inference for linguistically accurate interpretation. To support this, we also introduce OB-Radix, an expert-annotated dataset providing structural and semantic data absent from prior corpora, comprising 1,022 character images (934 unique characters) and 1,853 fine-grained component images across 478 distinct components with verified explanations. By evaluating our system across three benchmarks of different tasks, we demonstrate that our framework yields more detailed and precise decipherments compared to baseline methods.

---

## 论文详细总结（自动生成）

# 论文总结：通过构件锚定多模态知识增强实现甲骨文解读的大模型专门化

## 1. 核心问题与研究背景

- **研究动机**：甲骨文（Oracle Bone Script, OBS）是中国已知最早的成熟文字系统，已识别字符超过 4,500 个，但仅约三分之一被成功释读，大量字形仍是未解之谜。每个未释读字符都代表着古代制度、技术与信仰的遗失片段。
- **核心痛点**：现有 AI 方法大多将甲骨文释读视为**闭集图像识别任务**，忽视了文字内在的结构、语义与语境细微差别。这导致：
  - 信息浪费与解释偏差；
  - 模型缺乏领域知识，难以泛化到未见过的字符；
  - 通用视觉语言模型（VLM）在低资源专业领域容易出现"视觉幻觉"或缺乏语言学深度。
- **关键洞察（"解释鸿沟"）**：虽然单个甲骨文字符往往独特且罕见，但它们由**有限的可复用象形构件（components/radicals）**组成，这些构件携带可迁移的语义。识别未知字形中的已知构件，即可系统性地推断新字符的含义。
- **整体含义**：论文将甲骨文释读重新表述为**构件锚定、结构感知的推理任务**，而非纯粹的视觉识别问题，为古典文献的语义分析与知识抽取提供可复用的多模态方法。

## 2. 方法论

### 2.1 核心思想
提出**智能体驱动的检索增强生成（Agentic RAG）框架**，将 VLM 的精确视觉定位能力与基于 LLM 的智能体推理链相结合，通过构件级语义增强来专门化大模型。

### 2.2 关键技术模块（四阶段流水线）

- **(a) 构件识别模块**
  - 使用基于 **DINOv2 的 ViT 架构**构建构件特征空间，编码为 768 维向量：$z = f(x), z \in \mathbb{R}^{768}$
  - 采用**原型网络（Prototypical Networks）**分类器，每个类的原型 $p_c$ 为其支持集 $S_c$ 的均值嵌入
  - 查询样本 $x_q$ 通过欧氏距离 $d(\cdot,\cdot)$ 归入最近原型的类别：$\hat{y} = \arg\min_c d(z_q, p_c)$
  - 推理时使用 Top-1 预测作为下游检索的语义锚点；Top-K 仅作评估指标
  - 该设计适合低数据场景，提升鲁棒性并减少过拟合

- **(b) 智能体编排的图知识检索**
  - 从 OB-Radix 与字符–构件关系构建**知识图谱（KG）**，支持增量扩展
  - 采用级联但基本固定的检索流水线，由工具使用型 LLM 智能体编排（ReAct、Toolformer 范式）
  - 智能体可调用两个外部工具：**构件解释**与**按构件查字符**
  - 流程：构件中心检索 → 约束综合（变体查找、现代–甲骨映射，不调用外部工具）→ 汇总为字符中心的证据包
  - 集成语义相似度缓存（RAGCache），提升效率

- **(c) 构件关系推理**
  - 利用 VLM 联合考虑视觉嵌入与检索到的语义信息
  - 预测字符的**构字类型**（表意 ideographic、象形 pictographic、形声 phono-semantic）
  - 生成解释构件如何交互形成含义的推理轨迹，作为连接识别与解释生成的中间推理层

- **(d) 解释生成**（支持两种模式）
  - **VLM 推理模式**：VLM 联合条件于视觉嵌入、构件预测与 KG 语义提示
  - **多智能体推理模式**：将检索与推理解耦为两个专门智能体——知识检索智能体（规划并执行图查询）与语义推理智能体（合成证据与视觉线索为结构化解释），提升鲁棒性、减少错误传播

### 2.3 配套数据集：OB-Radix
- 由古文字学专家精心标注，提供先前语料缺失的结构与语义数据
- 规模：**1,022 张字符图像（934 个唯一字符）+ 1,853 张细粒度构件图像（478 个不同构件）**，每个均配有专家验证的语义解释
- 标注三原则：(i) 隔离具有不同语义角色的构件（不论视觉尺度）；(ii) 边界模糊时优先语义完整性；(iii) 通过受控词表保持构件标签一致
- 使用 **LabelMe** 进行语义掩码，专家手动调整边界点；总投入 **70 人时**，标注者报酬合计 2,450 元人民币

## 3. 实验设计

### 3.1 数据集与划分
- **构件检索**：OB-Radix 的 478 个构件按 7:3 划分训练/测试
- **构件关系推理**：构建 528 个标注实例的 seen set，含构字类型标签与专家推理轨迹
- **解释生成**：KG 用 70% 语料构建，30% 留出测试，确保评估字符未在训练中出现

### 3.2 三个渐进式 Benchmark
1. **构件级检索**（基础）
2. **构件关系推理**（中间阶段）
3. **甲骨文解释生成**（终极目标）

### 3.3 评估指标
- 构件检索：ACC@k（k∈{1,3,5}）
- 关系推理：构字类型分类准确率、BERTScore-F1、MoverScore、ROUGE-1、LLM-as-a-Judge
- 解释生成：BERTScore、MoverScore、ROUGE-1、LLM-as-a-Judge（用 Gemini 3 Flash 作评判，温度设为 0）

### 3.4 对比方法（Baseline 模型）
- **GPT**：GPT-5
- **Claude**：Claude Opus 4.1 (20250805)
- **GLM**：GLM-4.5V
- **Qwen**：Qwen3-VL-235B-A22B
- 多智能体设置中推理器还使用 DeepSeek-R1-250528、Qwen3-235B-A22B

## 4. 资源与算力

- **论文正文未明确说明**所使用的 GPU 型号、数量、训练时长或具体算力开销。
- 仅提及多智能体配置带来**约 1.67× token 使用量**的推理成本增加（作为效率权衡）。
- 构件识别模块使用 DINOv2 Base 作为视觉编码器，原型分类器本身为轻量级设计，适合低资源场景。
- 整体上，论文属于推理/检索增强类工作，未报告大规模训练算力，这也是一处信息缺失。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 主实验 3 组（构件检索、关系推理、解释生成）
  - 消融实验 1 组（禁用检索，验证 Agentic RAG 贡献）
  - 多智能体协作实验 1 组（6 种 Retriever–Reasoner 组合）
  - 人类专家评估 1 组（2 位考古学博士生，5 点 Likert 量表）
  - 补充实验 2 组（英文解释生成、变体字符识别）
  - 共约 **8 组实验**，涉及 7 张表格与多张图示
- **充分性与公平性评价**：
  - **优点**：任务设计呈渐进式（构件→关系→解释），覆盖识别、推理、生成三个层次；同时采用自动指标与人类评估双重验证；数据集划分避免泄露（KG 与测试集分离）。
  - **公平性**：对四个主流 VLM 采用统一的 baseline 与增强设置对比，报告相对增量（+Δ）清晰。
  - **客观性**：LLM-as-a-Judge 使用固定 prompt 与温度 0；人类评估报告了评分者间信度（ICC3=0.71，Krippendorff's Alpha=0.74），显示实质一致性。
  - **潜在不足**：人类评估仅用 10% 留出测试集、2 位评分者，样本规模较小；部分任务（如变体识别）样本量仅 39 对，统计效力有限。

## 6. 主要结论与发现

- **构件检索**：Top-1 0.7795、Top-3 0.8855、Top-5 0.9157，验证原型分类器在低资源构件识别上的有效性。
- **构件关系推理**：增强流水线在所有指标上超越 baseline。Qwen3-VL 分类准确率最高（0.599，+0.248）；GPT-5 在 BERTScore 与 LLM-as-a-Judge 上最佳；Claude 在 MoverScore、ROUGE-1 上流畅性/对齐最强。
- **解释生成**：Agentic RAG 一致优于 baseline。例如 Qwen3-VL 的 ROUGE-1 从 0.264→0.354，MoverScore 从 0.362→0.471；GPT-5 取得最佳 BERTScore 0.727 与 LLM-Judge 0.558。
- **消融研究**：禁用检索后所有模型性能下降，ROUGE-1 与 LLM-Judge 降幅最大，证明图知识检索提供了超越构件类别的关键关系与语境信息，且主要提升高层语义正确性而非表层相似度。
- **多智能体协作**：多智能体配置普遍优于单智能体，代价是约 1.67× token 成本。
- **人类评估**：多智能体流水线得分最高（3.433），KG-RAG 次之（2.133），baseline 最低（1.367），与自动指标一致。
- **跨语言**：英文解释生成性能明显下降（受术语翻译差异与中文中心 KG 限制），但 RAG 相对 baseline 的提升趋势保持一致。
- **变体字符识别**：所有模型准确率极低（Top-1 最高仅 5.13%），反映该任务内在困难。

## 7. 优点

- **问题重构新颖**：将甲骨文释读从闭集识别转向构件锚定、结构感知推理，契合文字的象形构成逻辑。
- **方法论完整**：视觉定位 + 图检索 + 关系推理 + 解释生成的端到端流水线，且支持 VLM 推理与多智能体两种模式。
- **数据集贡献扎实**：OB-Radix 提供专家标注的构件级结构与语义数据，弥补现有语料仅有字符级标注的空白。
- **评估体系设计严谨**：三层递进 benchmark + 自动指标 + 人类专家评估 + 消融 + 多智能体 + 跨语言 + 变体识别，覆盖全面。
- **可解释性与可追溯性**：所有检索线索显式、可审计，而非隐式吸收；多智能体解耦降低错误传播。
- **工程细节到位**：语义缓存提升效率，KG 支持增量扩展。

## 8. 不足与局限

- **构件识别不完善**：识别并非总是精确或完整，可能引入虚假元素。
- **KG 依赖风险**：缺失条目导致解释不充分，错误映射会引入无关证据；属可追溯性权衡下的刻意取舍。
- **学术客观限制**：大量甲骨文字符尚缺乏公认解释，本质上约束了任何自动化分析的可靠性。
- **形声字处理薄弱**：形声复合字仍是当前系统的难点。
- **工作流不够自主**：采用结构化、检索中心的工作流而非完全自主生成，灵活性受限，依赖外部知识源。
- **跨语言天花板低**：英文解释受术语标准化缺失与中文中心资源限制，性能明显下降。
- **变体识别未解**：变体–正体映射困难，需针对性监督或对比学习，留待未来工作。
- **算力信息缺失**：论文未报告 GPU 型号、数量、训练时长等资源细节，难以评估可复现性与成本。
- **人类评估规模有限**：仅 2 位评分者、10% 测试集，统计代表性有限。

（完）

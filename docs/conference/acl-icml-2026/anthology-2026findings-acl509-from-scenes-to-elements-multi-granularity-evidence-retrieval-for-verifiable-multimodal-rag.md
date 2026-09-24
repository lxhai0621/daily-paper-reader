---
title: "From Scenes to Elements: Multi-Granularity Evidence Retrieval for Verifiable Multimodal RAG"
title_zh: 从场景到元素：面向可验证多模态RAG的多粒度证据检索
authors: "Guanhua Chen, Chuyue Huang, Yutong Yao, Shudong Liu (刘树东), Xueqing Song, Lidia S. Chao, Derek F. Wong (黄辉)"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.509.pdf"
tags: ["query:mmkqa"]
score: 8.0
evidence: 面向可验证多模态RAG的多粒度跨模态证据检索
tldr: 现有多模态检索增强生成系统往往以整图或场景为粒度检索证据，与细粒度用户查询不匹配，且失败难以验证。本文提出GranuRAG多粒度框架，把视觉元素作为一等检索单元，分元素级检测分类、多粒度跨模态对齐检索与归因约束生成三阶段进行。同时构建GranuVistaVQA基准，包含地标元素级标注与多视角部分观测挑战。该工作提升了多模态问答的证据可验证性与检索精度。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 1024, \"height\": 1003}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 1080, \"height\": 1440}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 1080, \"height\": 1619}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-004.webp\", \"caption\": \"\", \"page\": 5, \"index\": 4, \"width\": 1080, \"height\": 1440}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-005.webp\", \"caption\": \"\", \"page\": 5, \"index\": 5, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-006.webp\", \"caption\": \"\", \"page\": 5, \"index\": 6, \"width\": 1280, \"height\": 1280}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-007.webp\", \"caption\": \"\", \"page\": 5, \"index\": 7, \"width\": 1280, \"height\": 836}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-008.webp\", \"caption\": \"\", \"page\": 5, \"index\": 8, \"width\": 980, \"height\": 980}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-009.webp\", \"caption\": \"\", \"page\": 6, \"index\": 9, \"width\": 1780, \"height\": 977}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-010.webp\", \"caption\": \"\", \"page\": 8, \"index\": 10, \"width\": 600, \"height\": 500}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-011.webp\", \"caption\": \"\", \"page\": 8, \"index\": 11, \"width\": 600, \"height\": 500}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-012.webp\", \"caption\": \"\", \"page\": 8, \"index\": 12, \"width\": 1968, \"height\": 1830}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-013.webp\", \"caption\": \"\", \"page\": 8, \"index\": 13, \"width\": 1968, \"height\": 1830}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-014.webp\", \"caption\": \"\", \"page\": 9, \"index\": 14, \"width\": 1495, \"height\": 1979}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-015.webp\", \"caption\": \"\", \"page\": 9, \"index\": 15, \"width\": 1504, \"height\": 1979}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-016.webp\", \"caption\": \"\", \"page\": 16, \"index\": 16, \"width\": 1316, \"height\": 919}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-017.webp\", \"caption\": \"\", \"page\": 17, \"index\": 17, \"width\": 2222, \"height\": 1366}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-018.webp\", \"caption\": \"\", \"page\": 17, \"index\": 18, \"width\": 2226, \"height\": 1366}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-019.webp\", \"caption\": \"\", \"page\": 17, \"index\": 19, \"width\": 2224, \"height\": 1366}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl509/fig-020.webp\", \"caption\": \"\", \"page\": 17, \"index\": 20, \"width\": 2220, \"height\": 1364}]"
motivation: 多模态RAG以整图或场景为检索粒度，与细粒度查询不匹配且失败不可验证。
method: 提出GranuRAG框架，分元素检测分类、多粒度跨模态对齐检索与归因约束生成三阶段，并构建GranuVistaVQA基准。
result: 元素级检索与多视角标注基准为细粒度可验证多模态问答提供评测支撑。
conclusion: 将视觉元素作为检索单元，提升多模态RAG证据的可验证性。
---

## Abstract
Multimodal Retrieval-Augmented Generation (RAG) systems retrieve evidence at coarse granularities (entire images or scenes), creating a mismatch with fine-grained user queries and making failures unverifiable. We introduce GranuVistaVQA, a multimodal benchmark featuring real-world landmarks with element-level annotations across multiple viewpoints, capturing the partial observation challenge where individual images contain only subsets of entities. We further propose GranuRAG, a multi-granularity framework that treats visual elements as first-class retrieval units through three stages: element-level detection and classification, multi-granularity cross-modal alignment for evidence retrieval, and attribution-constrained generation. By grounding retrieval at the element level rather than relying on implicit attention, our approach enables transparent error diagnosis. Experiments demonstrate that GranuRAG achieves up to 29.2% improvement over six strong baselines for this task.

---

## 论文详细总结（自动生成）

# 论文总结：《从场景到元素：面向可验证多模态 RAG 的多粒度证据检索》

## 1. 核心问题与研究动机

- **背景**：多模态大模型（MLLM）视觉理解能力快速提升，但推理过程不透明、易产生幻觉；RAG 通过外部证据条件化生成可缓解该问题，但现有多模态 RAG 扩展大多在**粗粒度**上检索（整图、整场景、整页）。
- **核心矛盾——"归因鸿沟"（attribution gap）**：用户询问"巴洛克式山花"却收到一张建筑照片，双方都无法验证：该构件是否真在图中、检索到的知识是否相关、答案是否忠实反映输入。**检测失败、检索错误、生成幻觉三者坍缩为一个不可解释的黑箱**。
- **现有工作缺口**：
  - 定位类模型（KOSMOS-2、RegionGPT 等）能定位物体，但依赖参数化知识、不检索外部证据；
  - 现有多模态 RAG 系统能检索证据，但缺乏显式的元素级 grounding，即便细粒度方法（如 HM-RAG）也优先考虑表示能力而非透明归因。
- **基准缺口**：REAL-MM-RAG、MMDocIR、M3DocRAG、MMLongBench-Doc、SPIQA 五个相近数据集**无一同时满足**多粒度、细粒度对齐、部分实体、RAG 四项要求，且都忽略了真实图像的**部分观测挑战**——单张照片因拍摄距离/角度不同只呈现该地点的一部分元素。
- **论文主张**：可验证的多模态 RAG 必须把**视觉元素视为一等检索目标**，而非被隐式注意的区域；采用"先检测、再检索"（detect-then-retrieve）的范式。

## 2. 方法论

### 2.1 核心思想
将视觉元素作为一等检索单元，通过三阶段流水线：**元素级检测与分类 → 多粒度跨模态对齐检索 → 归因约束生成**。由此把评估从"黑箱答案打分"转变为"透明证据审计"，可分别诊断检测、检索、生成三个环节。

### 2.2 关键技术细节

- **阶段一：视觉区域检测与过滤**
  - 使用开放词汇检测器 **YOLO-World-XL**，以通用建筑基元（柱子、雕刻、装饰纹样）为提示词识别候选区域，无需领域微调。
  - **重叠过滤去冗余**：两框重叠超过 80% 时保留较小者，以保留细粒度建筑细节；得到精炼区域集合 `B(I) = {b₁, b₂, …, b_K}`。

- **阶段二：知识引导的元素匹配**
  - 将该问题建模为多模态匹配：MLLM 接收标注了边界框的图像、以及候选元素集 E 对应的外观描述 `{a_e}`（形状、材质、风格等视觉属性），为每个区域选出最匹配元素：
    `e_k = M_φ(I, b_k, {(e, a_e)}_{e∈E}) ∈ E ∪ {∅}`
  - 输出 `∅` 表示无候选描述与区域足够一致，该区域被丢弃。最终得到有视觉证据确认的 grounded 元素集 `Ê(I) = {e_k | e_k ≠ ∅}`。
  - 设计意图：结合检测器的空间定位能力与 MLLM 的细粒度语义判别能力，在视觉相似元素间也能可靠区分；显式过滤未检出元素，划定"系统所观测"与"系统所知"的边界，降低对缺失构件的幻觉。

- **阶段三：证据落地生成**
  - 对每个 `e ∈ Ê(I)` 检索其专家撰写描述 `d_e`，并前置全局元数据 `m`（地标名、建筑风格、历史时期）：
    `C(I) = [m] ⊕ [(e_i, d_{e_i})]_{e_i∈Ê(I)}`
  - 生成：`y = G_θ(I, C(I) | Ω(Ê(I)))`，其中提示 `Ω` 约束模型**只描述已确认的元素**，并将所有事实主张锚定到检索描述。
  - **可追溯性带来三类错误诊断**：信息缺失 → 检测失败；事实错误 → 检索错误；无支撑主张 → 生成幻觉。

### 2.3 基准构建（GranuVistaVQA）
- 任务定义：给定任意视角的地标查询图像 I，生成覆盖所有**可见**建筑元素的完整描述，且不得对遮挡/缺失构件产生幻觉。
- 每个地标关联：元数据（名称、摘要、风格）、元素清单 `E = {e₁,…,e_k}`、元素描述映射 `ED: E → Paragraphs`；每张图有真值可见集 `E_gt(I) ⊆ E`，支持模块化评估。
- 数据来源：澳门文化遗产 71 个地标（宗教建筑、庙宇、防御工事、文化机构），文本取自官方旅游门户与百科，图像来自 Google Images、小红书、Trip.com，描述内容为**中文**。
- 标注流程：LLM 提议候选元素 → 人工增删、同义归一（如 "bell tower" ≡ "campanile"）→ 严格可见性准则（仅凭像素可识别、部分遮挡须保留判别性线索、歧义即排除）。

## 3. 实验设计

- **数据集/基准**：GranuVistaVQA。71 个地标、1,422 张图像、221 个唯一元素；平均每地标 20.03 张图、3.59 个元素；**单图平均仅覆盖该地标 34% 的元素**（中位数 29%，IQR 0.18–0.47；特写平均 22%、中景 36%、全景 58%）。
- **评估指标**：ROUGE-L、BERT-F1，以及 **LLM-as-a-judge** 集成打分（GPT-4.1 + Gemini-2.5-Pro + Claude-Haiku-4.5，0–100 分，加权规则为 Coverage 40%、Faithfulness 40%、Cohesion 20%，取三模型均值以降低单模型方差）。
- **主实验**：6 个 MLLM（Qwen3-VL-8B、Qwen-VL-Max、GPT-4.1-Mini、GPT-4o、Claude-3.5-Sonnet，及微调版 Qwen3-VL-8B†）在三种设置下对比：
  - (A) Baseline：图像 + 完整含噪候选集 E_all；
  - (B) CoT：在 (A) 基础上加思维链提示；
  - (C) GranuRAG：仅接收 grounded 子集 Ê(I)。
- **消融实验**：
  - 视觉呈现 × 元素过滤四配置：T1（原图 + E_all）、T2（框标注图 + E_all）、T3（原图 + Ê(I)）、T4（框标注图 + Ê(I)）；
  - 视觉模态与知识相关性：Text-only（Gold E_gold）、Image + All E_all、Image + Chosen Ê(I)；
  - 检测器对比：无检测器（LLM-only）、Grounding DINO、YOLO-World；
  - 重叠阈值敏感性：70%–100% 共 6 档。
- **检索策略对比**（固定 Qwen-VL-Max）：全局基线、CLIP 稠密嵌入检索、RAVQA（PreFLMR）、VisRAG 2.0。
- **其他实验**：ID/OOD 泛化对比；错误分析（提取准确率、双方法均正确时的答案质量）；人工评估（GPT-4o 与 Qwen-VL-Max 各 20 题，共 40 组两两比较，3 名计算机专业研究生盲评，4 项标准）；注意力权重可视化（Base/CoT/GranuRAG 适配器对比 top-10 注意力差异区域）；归因评估（Attribution Precision、Attribution Recall、Unsupported Claim Rate）。

## 4. 资源与算力

- 文中明确报告：微调 **Qwen3-VL-8B** 使用 **LLaMA-Factory** 框架，在**单张 H800 GPU** 上训练；采用 **LoRA（rank = 8）**，序列长度 4096，batch size 4，梯度累积 4 步，训练 **3 个 epoch**，学习率 1e-4。
- 推理统一设置：温度 0.1，最大生成长度 600 tokens。
- YOLO-World-XL1 通过 Replicate API 调用，置信度阈值固定。
- **未明确说明**：总训练时长/GPU 小时数、API 调用总成本、微调数据规模的具体数量（仅说明测试集随机抽取 20% 的部分地标图像、约半数景点完全不在训练集中）。
- **效率开销**：本方法约 **3.5 秒/样本**，基线约 2 秒/样本，耗时接近两倍（因额外的检测与多粒度检索步骤）。

## 5. 实验数量与充分性

- **实验规模概览**：
  - 主结果表约 18 行（5 个模型 × 3 设置 + 1 个微调模型 × 3 设置）；
  - 4 类消融（视觉呈现 T1–T4、视觉模态与知识相关性、检测器替换、重叠阈值 6 档）；
  - 1 组检索策略对比（4 个对比方法）；
  - 1 组 ID/OOD 泛化对比；
  - 2 类错误分析 + 1 组人工评估（40 对、Fle

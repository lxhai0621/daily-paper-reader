---
title: "StruNRAG: Evaluation of OCR-Induced Structural Noise on RAG Robustness"
title_zh: StruNRAG：评估OCR引发的结构噪声对RAG鲁棒性的影响
authors: "Mengna Gao, Dapeng Yin, Shuyue Zhu, Bingxuan Hou, Zhanpeng Ni, Junli Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.955.pdf"
tags: ["query:ma-kf"]
score: 7.0
evidence: OCR结构噪声下的RAG鲁棒性
tldr: 现有RAG评测大多假设输入结构完美，忽视了OCR在复杂版面上引入的行插入、段落交错等结构噪声。本文提出StruNRAG基准，基于中英文复杂文档构建2132个问答对，并系统注入三类真实结构扰动。实验表明这些噪声显著削弱RAG的检索与生成鲁棒性。该工作填补了结构噪声评测的空白，为真实文档场景下RAG稳健性研究提供了新基准。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 1284, \"height\": 1127}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 1005, \"height\": 982}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 1853, \"height\": 1014}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-004.webp\", \"caption\": \"\", \"page\": 9, \"index\": 4, \"width\": 1326, \"height\": 1041}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-005.webp\", \"caption\": \"\", \"page\": 12, \"index\": 5, \"width\": 913, \"height\": 960}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-006.webp\", \"caption\": \"\", \"page\": 13, \"index\": 6, \"width\": 939, \"height\": 1332}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-007.webp\", \"caption\": \"\", \"page\": 14, \"index\": 7, \"width\": 974, \"height\": 1372}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-008.webp\", \"caption\": \"\", \"page\": 16, \"index\": 8, \"width\": 1902, \"height\": 786}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl955/fig-009.webp\", \"caption\": \"\", \"page\": 16, \"index\": 9, \"width\": 1596, \"height\": 1058}]"
motivation: RAG依赖OCR从非结构化文档摄取知识，但OCR常因复杂版面引入结构噪声，现有评测大多忽略这一问题。
method: 构建StruNRAG基准，基于中英文复杂文档生成2132个问答对，系统注入三类真实结构扰动。
result: 实验揭示结构噪声显著影响RAG鲁棒性，为鲁棒性评测提供新维度。
conclusion: 该基准填补OCR结构噪声评测空白，推动RAG在真实文档场景的稳健性研究。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems rely on Optical Character Recognition (OCR) to ingest knowledge from unstructured documents. However, OCR engines often struggle with complex layouts, introducing Structural Noise , such as line insertion and paragraph interleaving, which disrupts the semantic flow of the text. Existing evaluations largely overlook this dimension, operating on the assumption of structurally perfect input. To bridge this gap, we introduce StruNRAG, a dedicated benchmark for evaluating RAG robustness against OCR-induced structural perturbations. We construct a bilingual dataset of 2,132 question-answer pairs derived from complex Chinese and English documents and systematically inject three categories of real-world structural noise: line insertion, paragraph interleaving, and line interleaving. Our evaluation of mainstream retrievers and Large Language Models (LLMs) reveals a nuanced interaction between noise and pipeline stages: while structural distortions consistently degrade retrieval performance, the generation stage exhibits unexpected robustness. Advanced LLMs demonstrate robustness against local noise (e.g., line insertion), but struggle to maintain reasoning capabilities under severe structural disruption that fragments global context. These findings indicate that while LLMs are capable of compensating for minor parsing errors, future RAG optimizations must take into account the effects of structural noise. Our code and datasets are available at [https://github.com/GaoMengnana/StruNRAG](https://github.com/GaoMengnana/StruNRAG).

---

## 论文详细总结（自动生成）

# StruNRAG 论文结构化总结

## 1. 核心问题与研究动机

- **背景**：RAG 系统依赖 OCR 从非结构化文档（尤其是 PDF）中摄取知识。但真实场景中大量文档版式复杂，OCR 精度常仅 30%–50%。
- **已有缺口**：
  - OHR-Bench 发现 OCR 构建的知识库相比 ground-truth（GT）存在至少 14% 的性能差距，但其分析仅停留在**字符级**。
  - 现有 RAG 评测（RAGAS、ARES、RAG-QA、Adaptive-RAG、MultiHop-RAG 等）大多**默认输入结构完美**，忽视知识库本身的质量问题。
- **核心问题**：OCR 在复杂版面上会引入一种更根本、更具破坏性的现象——**结构噪声（Structural Noise）**。它不改变字面内容，却破坏文档的"空间-逻辑连贯性"，导致语义碎片化，并沿 RAG 流水线引发**级联失效**（误导检索、破坏上下文完整性、最终导致事实错误或拒答）。
- **动机统计**：作者对 109 篇复杂版式期刊 PDF 用 MinerU 解析，发现字符错误率（CER）高达 75.37%，平均每篇文档出现 3.9 处结构噪声，印证问题的普遍性与严重性。

## 2. 方法论

### 2.1 三类结构噪声的形式化定义

论文将结构噪声建模为**文档级变换算子**：给定 GT 文档 $x$，生成噪声文档 $\tilde{x}=\mathcal{N}(x)$。三类噪声对应 $\mathcal{N}$ 在不同结构层级上的实例化：

- **行插入（LInsert）**：文档布局分析（DLA）错误地将语义孤立元素（如页眉）嵌入连贯文本块，得到 $[l_1,\dots,l_i,l_{noise},l_{i+1},\dots,l_n]$。
- **段落交错（PInterl）**：相邻段落 $p_A,p_B$ 被误判逻辑流，变成交替结构 $[p_{A1},p_{B1},p_{A2},p_{B2}]$。
- **行交错（LInterl）**：多栏边界检测失败，左右栏的行按垂直坐标被混合，得到 $[l_{1}^{left},l_{1}^{right},l_{2}^{left},l_{2}^{right},\dots]$。

噪声注入量为随机变量 $m \sim \{2,3,4,5\}$，以贴合真实统计分布。

### 2.2 基准构建流程（四步）

1. **数据采集**：从《纽约时报》（NYT，英文 244 篇）与《人民日报》（PD，中文 181 篇）收集共 **425 篇**复杂版式 PDF；采用"Windows.media.ocr 自动识别 + 人工校正"的混合标注构建 GT。
2. **噪声注入**：按预定义规则向 GT 知识库注入三类结构噪声。CER 验证：LInsert 约 11–12%，PInterl/LInterl 超过 50%；合成噪声与真实 OCR 输出的重叠系数 **OVL = 0.7986**，中位 CER 接近（0.72 vs. 0.69），保证既不高估也不低估真实退化程度。
3. **问答生成**：用 GPT-4o 将上下文切分为 A、B 两部分，要求问题必须**联合 A、B 证据**才能回答，确保问题与噪声位置强耦合。
4. **质量检查**：Qwen-Max 做忠实性检测 + 上下文依赖检查；对答案采样 10 次，仅当众数出现 ≥4 次才保留；最后由专家人工抽查。初始 6,840 题最终精炼为 **2,132 个高质量问答对**（NYT 1,186，PD 946；每语言各含三类噪声子集，共六个子集）。

## 3. 实验设计

- **知识库变体**：干净 GT 文档 + 三类合成结构噪声文档。
- **评测指标**：检索阶段用最长公共子序列（LCS）相似度；生成阶段与端到端阶段用 F1。
- **对比模型**：
  - 检索：BGE-M3（稠密）、BM25（稀疏）。
  - 生成：Qwen2.5-72B-Instruct、Llama-3.1-70B、Qwen3-8B、Llama-3.1-8B。
  - 端到端：BM25/BGE-M3 与 Qwen3-8B/Llama-3.1-8B 的四种组合。
- **扩展实验**：
  - 混合检索（BM25+BGE-M3，RRF）与 BGE-Reranker-v2-M3 重排。
  - 视觉语言模型对比（Qwen2.5-VL-7B / 32B）。
  - 检索深度 $k \in \{1,2,5\}$。
  - 结构噪声 × 字符级噪声的**非组合效应**实验。
- **五个研究问题（RQ1–RQ5）**：噪声影响、质量检查消融、提示工程、检索超参、噪声非组合效应。

## 4. 资源与算力

- 文中仅提到：**"所有开源模型部署于多 NVIDIA H800 GPU 环境"**。
- **未明确说明** GPU 的具体数量、训练/推理时长、总计算量等细节。
- 其他资源信息：4 名人工标注者参与审核，平均时薪 $12；数据集含 425 篇 PDF、2,132 个问答对。

## 5. 实验数量与充分性

- **实验规模**：覆盖中英双语 × 三类噪声 × 三阶段（检索/生成/端到端），叠加质量检查消融（-fai / -rel）、提示工程消融、Top-k 对比（k=1/2/5）、混合检索与重排、VLM 对比、字符+结构噪声组合等，整体维度较丰富。
- **充分性**：
  - 优点：RQ 设置系统，横跨不同参数量级（8B 到 72B）与不同架构（稠密/稀疏/多模态），并对噪声注入合理性做了 CER 拟合验证。
  - 不足：非组合效应实验规模较小、粒度较粗（作者自述）；模型/提示模板相对有限。
- **客观与公平性**：所有实验使用统一系统提示模板以消除提示差异；GT 与噪声设置对照清晰；对噪声强度做了与真实 OCR 分布的对齐验证。总体上实验设计较为客观，但部分结论（如 prompt 效果）依赖少量模型，泛化性有待验证。

## 6. 主要结论与发现

- **级联性能衰减**：结构噪声在 RAG 全流程引发级联退化，检索普遍损失超过 10%。
- **检索与生成的分化**：
  - 检索阶段显著受损；BGE-M3 尤为敏感（中文 PInterl 从 72.16 跌至 54.93）。
  - 生成阶段出乎意料地稳健，大模型（70B/72B）鲁棒性更强；LInsert 下部分模型甚至追平或超过 GT。
  - PInterl/LInterl 比 LInsert 危害更大。
- **稀疏 vs 稠密检索**：BM25 更稳定——结构噪声不改变词汇组成（Jaccard 恒为 1.0），但会干扰 BGE-M3 的位置编码，导致语义表示漂移（相似度随噪声强度持续下降）。
- **端到端**：检索器决定性能上限；LLM×BGE-M3 常低于单独生成阶段，而 LLM×BM25 更稳健，有时端到端甚至超过生成阶段。
- **语言差异**：中文任务 F1 普遍高于英文；Qwen 擅中文、Llama 擅英文。
- **优化策略并非普遍有效**：重排反而降低性能；混合检索优于纯稠密但在部分噪声下不如纯 BM25；提示工程效果高度依赖模型（Qwen2.5-72B、Llama3.1-8B 提升，Llama3.1-70B、Qwen3-8B 反而下降）。
- **VLM 效果有限**：小 VLM 在噪声下可超 RAG，大 VLM 在 GT 和噪声下均不如 RAG。
- **检索深度**：增大 k 边际收益递减，Top-5 可能因引入过多噪声而停滞或回退。
- **非组合效应**：字符噪声与 LInsert 呈协同放大；与 PInterl/LInterl 呈抑制交互（结构噪声主导）。

## 7. 优点

- **概念创新**：首次明确提出并形式化"OCR 结构噪声"（行插入、段落交错、行交错），填补了 RAG 评测在知识库结构质量维度上的空白。
- **可控变量设计**：将噪声建模为统一文档级算子，便于在不同结构层级上定量、独立地比较各噪声类型的影响。
- **真实性验证**：通过 CER 分布拟合（OVL=0.7986）证明合成噪声与真实 OCR 输出高度一致，增强基准可信度。
- **严谨的数据构建**：GPT-4o 生成 + Qwen-Max 检测 + 采样稳定性检验 + 专家抽查的多阶段质量流程，保证问答强依赖上下文。
- **多阶段、多模型系统评测**：横跨检索/生成/端到端，并补充重排、混合检索、VLM、Top-k、噪声组合等实验，结论层次丰富。
- **揭示非组合效应**：发现结构噪声与字符噪声存在非简单叠加的交互，具有启发性。
- 代码与数据集开源。

## 8. 不足与局限

- **合成噪声的局限**：尽管做了拟合验证，噪声仍是人工注入的，可能无法完全复现真实解析引擎中错误分布的随机性与复杂性。
- **语料域覆盖有限**：仅使用新闻媒体（NYT、人民日报），未覆盖科学文献、金融报告等含图表、公式的领域。
- **非组合效应研究不充分**：字符级与结构噪声的交互是作者自认的未完成方向，未做大规模、细粒度实验。
- **算力信息缺失**：未说明 GPU 数量、时长等，影响可复现性评估。
- **结论泛化风险**：提示工程等结论依赖有限模型集合；中文 F1 更高等现象可能与语料主题集中度有关，未必可外推。
- **应用限制**：基准本身用于诊断评测，而非直接给出抗结构噪声的 RAG 架构方案。

（完）

---
title: "HisDoc-OCR: Restoring Visual Grounding in MLLMs for Chinese Historical Document OCR"
title_zh: HisDoc-OCR：为中文历史文献OCR恢复多模态大模型的视觉定位
authors: "Jiahuan Cao, Yongxin Shi, Zeyu Shan, Zhengyang Lu, Lianwen Jin"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.301.pdf"
tags: ["query:ancient-text"]
score: 7.0
evidence: 面向中文历史文献、恢复多模态大模型视觉定位的OCR
tldr: 中文历史文献承载千年文化遗产，却因古籍字形与图像退化导致多模态大模型出现严重幻觉、造字与语义漂移，难以被计算分析。作者指出根因是视觉-文本错位，模型过度依赖语言先验而忽视视觉证据。为此提出HisDoc-OCR，通过版面注入等三种协同策略恢复视觉定位能力。该工作提升了古籍OCR的可靠性，为古籍数字化处理提供支撑。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 900, \"height\": 611}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 324, \"height\": 910}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 393, \"height\": 800}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-004.webp\", \"caption\": \"\", \"page\": 3, \"index\": 4, \"width\": 550, \"height\": 809}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 2082, \"height\": 880}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-006.webp\", \"caption\": \"\", \"page\": 5, \"index\": 6, \"width\": 1677, \"height\": 1488}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-007.webp\", \"caption\": \"\", \"page\": 5, \"index\": 7, \"width\": 1677, \"height\": 1488}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-008.webp\", \"caption\": \"\", \"page\": 5, \"index\": 8, \"width\": 882, \"height\": 880}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-009.webp\", \"caption\": \"\", \"page\": 12, \"index\": 9, \"width\": 1086, \"height\": 3000}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-010.webp\", \"caption\": \"\", \"page\": 13, \"index\": 10, \"width\": 1150, \"height\": 730}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-011.webp\", \"caption\": \"\", \"page\": 13, \"index\": 11, \"width\": 692, \"height\": 1188}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl301/fig-012.webp\", \"caption\": \"\", \"page\": 14, \"index\": 12, \"width\": 2928, \"height\": 1893}]"
motivation: 中文历史文献难以被计算分析，多模态大模型在古籍OCR上幻觉严重、字形失真。
method: 提出HisDoc-OCR，采用版面注入等三种协同策略恢复视觉定位，纠正视觉-文本错位。
result: 方法缓解了造字、重复与语义漂移，提升古籍OCR的可靠性。
conclusion: 为古籍数字化与历史文献计算分析提供可行路径。
---

## Abstract
Chinese historical documents encode millennia of cultural heritage, yet remain largely inaccessible to computational analysis. While multimodal large language models (MLLMs) have achieved strong performance on modern document OCR, their application to historical Chinese texts suffers from severe hallucinations, character fabrication, uncontrolled repetition, and semantic drift. We identify the root cause as visual-textual misalignment: models prioritize linguistic priors over visual evidence, particularly problematic when archaic orthography and degraded image quality destabilize cross-modal correspondences. To address this, we propose HisDoc-OCR, which restores visual grounding through three synergistic strategies: (1) Layout Injection, which encodes two-dimensional layout structures into textual outputs using layout-aware delimiters; (2) First-Occurrence Boost, which emphasizes vision-dependent characters during training by reweighting first-occurrence characters; (3) Self-Distilled Attention Focusing, which guides the model’s attention by distilling patterns from the most focused layer to the remaining layers. Extensive experiments demonstrate that HisDoc-OCR consistently outperforms general-purpose and OCR-specific MLLMs. The code will be publicly available.

---

## 论文详细总结（自动生成）

# HisDoc-OCR 论文深度总结

## 1. 核心问题与整体含义

- **研究背景**：中文历史文献承载千年文化遗产，但因其以扫描图像形式存在，难以被计算分析。OCR 是将文献图像转为结构化文本、支撑下游检索与知识挖掘的核心技术。
- **核心问题**：多模态大语言模型（MLLMs）虽在现代文档 OCR 上表现优异，但直接应用于中文历史文献时会出现严重幻觉——**造字、失控重复、语义漂移**。
- **根因诊断**：作者将问题归因于**视觉-文本错位（visual-textual misalignment）**。古文字形（archaic orthography）与退化图像质量削弱了跨模态对应关系，导致模型过度依赖语言先验、忽视视觉证据。
- **整体意义**：该工作填补了"基于 MLLM 的中文历史文献 OCR"这一研究空白，并提出更广泛的洞见：**专业领域的幻觉源于归纳偏置错位，而非模型容量不足**；轻量、可解释的干预可替代领域专用预训练。

## 2. 方法论

### 核心思想
通过三种**互补的视觉-文本对齐增强策略**恢复模型的视觉定位能力，从结构、训练动态、注意力三个层面系统性地强化视觉接地。

### 关键技术细节

- **（1）Layout Injection（版面注入）**
  - 问题：视觉编码器处理二维空间特征 $V \in \mathbb{R}^{H \times W \times D}$，而自回归解码器生成一维序列 $y=[y_1,\dots,y_N]$，存在**维度错配与结构信息瓶颈**。
  - 方案：用布局感知分隔符将二维版面结构显式编码进文本输出：
    - **列分隔**：换行符 `\n` 插入每列末尾
    - **块分隔**：块分隔标记 `—` 表示跨块边界
    - **双列注释**（古籍特殊格式）：用括号标记，格式为 `main text (right annotation left annotation)`
  - 效果：将 OCR 从无结构序列建模重构为**版面感知生成**。

- **（2）First-Occurrence Boost（首现字符增强）**
  - 观察：首次出现的字符（无上下文先验）对视觉证据依赖更强；重复字符可由语言先验推断。图 3 显示首现字符 token 具有更高的"文本到视觉"注意力比。
  - 标准交叉熵对所有权重一视同仁：$L_{\text{standard}} = -\sum_{i=1}^{N}\log P(c_i|v,c_{<i})$
  - 改进为自适应加权：
    - $L_{\text{char\_weighted}} = -\sum_{i=1}^{N} w_i \cdot \log P(c_i|v,c_{<i})$
    - $w_i = 1 + \alpha \cdot I_{\text{first}}(c_i)$，其中 $I_{\text{first}} \in \{0,1\}$
  - 首现字符权重约为重复字符的 **3 倍**（$\alpha=2$），迫使模型优先提取视觉特征。

- **（3）Self-Distilled Attention Focusing（自蒸馏注意力聚焦）**
  - 灵感：人类阅读时视觉注意力沿阅读路径顺序聚焦。
  - 发现：MLLM 各层注意力呈**分层涌现**——浅层注意力熵高（分散），深层注意力熵低（聚焦于当前识别区域）。
  - 方案：以**注意力熵最低的层 $l^*$ 作为伪教师**，将其注意力分布蒸馏到其余层：
    - $L_{\text{distill}} = \sum_{l \in S}\sum_{t}\sum_{v} A^{(t,v)}_T \log \frac{A^{(t,v)}_T}{A^{(t,v)}_l}$
  - 无需字符级边界框标注，从正则化视角提供跨层一致性约束。

- **（4）总训练目标**：$L_{\text{total}} = L_{\text{char\_weighted}} + \lambda L_{\text{distill}}$，实验中 $\lambda = 1$。

## 3. 实验设计

### 数据集 / Benchmark
| 数据集 | 用途 |
|---|---|
| **MTHv2** | 评测基准（含版面分析、字符检测与识别） |
| **M⁵HisDoc** | 大规模多风格中文历史文献评测基准 |
| **IC19HDRC** | 未见过的泛化测试集（因真值缺阅读顺序标注，仅报字符级 F1） |

### 评测指标
- Accurate Rate (AR)、Correct Rate (CR)、Normalized Edit Distance (ED)、F1-Score、BLEU
- 自定义 **Repetition Rate (RR)**：若输出达到最大生成长度且末尾 100 字符中唯一字符数 < 34，则判定进入重复模式。

### 对比方法
- **通用 MLLM**：Qwen3-VL-2B/4B/8B、InternVL3.5-2B/4B/8B
- **专用 MLLM（两阶段）**：PaddleOCR-VL、MonkeyOCR-pro-3B、MinerU2.5
- **专用 MLLM（端到端）**：olmOCR-2-7B-1025、DeepSeek-OCR、dots.ocr
- **本文模型**：HisDoc-OCR-Qwen3-VL-2B、HisDoc-OCR-InternVL3.5-2B、HisDoc-OCR-InternVL3.5-4B-full

### 训练配置
- 视觉编码器与投影器冻结，仅微调 LLM 组件
- Qwen3-VL-2B 最大输入视觉 token 2048；InternVL3.5-2B 最大裁剪子图 8；InternVL3.5-4B-full 最大裁剪子图 12
- Batch size 64，AdamW，初始学习率 $1\times10^{-5}$，warm-up 比例 0.03，余弦衰减，训练 5 个 epoch

## 4. 资源与算力

- **GPU**：4 张 NVIDIA A6000
- **训练时长**：文中**未明确说明**具体训练小时数
- **其他**：训练 5 个 epoch；InternVL3.5-4B-full 额外使用 M⁵HisDoc 验证集数据

## 5. 实验数量与充分性

### 实验组数概览
- **主实验**：3 个数据集（MTHv2、M⁵HisDoc、IC19HDRC）× 约 12 个对比方法 + 3 个本文变体
- **消融实验**（基于 Qwen3-VL-2B）：LI / FOB / SDAF 三组件单独与组合，共 5 组配置（表 3）
- **超参数实验**：FOB 中 $\alpha \in \{0,1,2,3,4\}$ 共 5 组（表 4）
- **版面复杂度实验**：从 M⁵HisDoc 手动挑出 100 个最复杂版面样本，对比 6 个模型（表 5）
- **附录消融**：基于 InternVL3.5-2B 的组件消融（表 7）与 $\alpha$ 消融（表 6）
- **定性结果**：4 组案例（印刷体、草书手写、复杂版面、密集文本，图 5–8）

### 充分性与公平性评估
- **充分**：覆盖多架构（native-resolution 的 Qwen3-VL 与 cropped-subimage 的 InternVL3.5）、多数据集、多维度指标（含幻觉量化指标 RR）、组件级与超参级消融。
- **客观公平**：对比方法涵盖通用/两阶段/端到端三类主流 MLLM，规模从 2B 到 8B；在未见过的 IC19HDRC 上验证泛化性；消融实验控制变量清晰。
- **潜在偏差**：复杂度子集为人工挑选，样本量仅 100，代表性有限；训练数据规模相对较小（MTHv2 + M⁵HisDoc）。

## 6. 主要结论与发现

- **性能领先**：HisDoc-OCR 在 MTHv2、M⁵HisDoc、IC19HDRC 三个基准上均达到 **SOTA**，显著优于通用 MLLM 与专用 OCR MLLM。
- **幻觉抑制显著**：重复率（RR）大幅降低。例如 HisDoc-OCR-Qwen3-VL-2B 在 MTHv2 上 RR 仅 0.13（基线 Qwen3-VL-2B 为 39.25）；在 IC19HDRC 上 RR 仅 0.43。
- **强泛化能力**：在未参与训练的 IC19HDRC 上仍取得最高字符级 F1（36.66），优于 olmOCR-2-7B-1025（32.54）。
- **三策略互补**：单独使用均有提升，组合使用时在几乎所有指标上取得最佳；LI 对复杂版面增益最大，FOB 对降低重复率最有效，SDAF 稳定注意力、一致性地减少重复。
- **超参数 $\alpha=2$ 最优**：过大（3、4）会过度强调首现字符，破坏视觉接地与上下文建模的平衡。
- **版面鲁棒性**：面对最复杂版面，多数 MLLM 性能严重下降，而 HisDoc-OCR 性能下降最小（如 InternVL3.5-4B-full 各项指标仅下降 5%–15%，RR 保持 0）。

## 7. 优点

- **问题诊断精准**：明确将幻觉根因定位为视觉-文本错位，而非笼统归咎于模型能力不足，为方法设计提供清晰理论依据。
- **策略互补且轻量**：三种策略分别从结构（版面）、训练动态（加权）、注意力（蒸馏）入手，无需领域专用预训练即可显著提升。
- **无需字符级标注**：Self-Distilled Attention Focusing 利用模型自身涌现的注意力分层特性，避免了昂贵的人工边界框标注。
- **架构通用性强**：在两种主流高分辨率视觉架构（native-resolution 与 cropped-subimage）上均验证有效。
- **幻觉量化创新**：自定义 Repetition Rate 指标，为 MLLM 在古籍 OCR 中的失控重复行为提供可量化评估。
- **鲁棒性与泛化验证充分**：包含复杂版面子集测试与未见数据集泛化测试，结论可信度高。

## 8. 不足与局限

- **额外标注需求**：Layout Injection 依赖带布局感知分隔符的文本转写，假设训练时版面信息可用，增加了标注成本（论文 Limitations 中明确承认）。
- **模型规模覆盖有限**：主要实验基于 2B–4B 模型，未验证在 7B/8B 以上更大模型上的可扩展性与收益。
- **训练数据规模有限**：仅使用 MTHv2 与 M⁵HisDoc 训练，数据量相对较小，可能限制对更广泛古籍风格的覆盖。
- **复杂度子集偏小**：复杂版面分析仅用 100 个手动挑选样本，统计效力与代表性有限。
- **缺乏训练时长报告**：未说明具体 GPU 训练小时数，影响算力成本复现。
- **语言与领域局限**：仅针对中文历史文献，未验证对其他低资源历史语言（如日文、韩文古籍）的迁移性。
- **缺乏错误分析**：未对失败案例进行系统性分类与讨论，可能掩盖特定场景下的失效模式。
- **伦理与真实性**：论文强调输出仅用于学术研究、不用于生成或篡改历史文本，但未讨论模型误识对文化遗产数字化准确性的长期风险。

（完）

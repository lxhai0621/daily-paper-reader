---
title: "ChunQiuTR: Time-Keyed Temporal Retrieval in Classical Chinese Annals"
title_zh: ChunQiuTR：中国古典编年史中的时间键检索
authors: "Yihao Wang, Zijian He, Jie Ren, Keze Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.612.pdf"
tags: ["query:ancient-text"]
score: 8.0
evidence: 古典编年史的时间检索
tldr: 历史研究常需按具体王月定位准确记录，但古典编年史的时间以隐晦、非公历的纪年短语编码，语义合理的证据也可能时间无效。本文提出ChunQiuTR，一个基于春秋及其训释传统构建的时间键检索基准，按月级纪年键组织记录并加入近似干扰项，同时提出CTD方法。该工作凸显时间对齐与主题相关同等重要，为古籍训释与RAG检索的结合提供新方向。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl612/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 348, \"height\": 348}]"
motivation: 历史研究中需按具体王月定位准确记录，但古典编年史的时间以隐晦、非公历的纪年短语编码，语义合理的证据可能时间上无效。
method: 构建基于春秋及其训释传统的时间键检索基准ChunQiuTR，组织月级纪年键与近似干扰项，并提出CTD方法。
result: 基准揭示检索中时间对齐与主题相关同等重要，暴露现有检索失败模式。
conclusion: 该工作连接古籍训释与RAG检索，推动历史文本的精准时间检索。
---

## Abstract
Retrieval shapes how language models access and cite knowledge in retrieval-augmented generation (RAG). In historical research, the goal is often to locate the exact record for a specific regnal month, where temporal alignment matters as much as topical relevance. This is especially challenging for Classical Chinese annals: time is encoded in terse, implicit, non-Gregorian reign phrases that are context-dependent, so semantically plausible evidence can still be temporally invalid. We introduce **ChunQiuTR**, a time-keyed retrieval benchmark built from the **Spring and Autumn Annals** and its exegetical tradition. It organizes records by month-level reign keys and includes chrono-near confounders that mimic real retrieval failures. We propose **CTD** (Calendrical Temporal Dual-encoder), a time-aware dual-encoder combining Fourier-based absolute context with relative offset biasing. Experiments show consistent gains over semantic dual-encoder baselines under time-keyed evaluation. We will release ChunQiuTR and code after the anonymity period.

---

## 论文详细总结（自动生成）

# ChunQiuTR：中国古典编年史中的时间键检索 —— 论文总结

## 1. 核心问题与研究动机

- **背景**：检索已成为语言模型接入外部知识的关键接口（RAG），在历史研究中，用户往往需要的不是"语义相关"的任意片段，而是**某一特定王月（regnal month）的精确记载**。此时时间一致性与主题相关性同等重要。
- **核心挑战**：中国古典编年史（如《春秋》）的时间表达具有以下特征：
  - **简短、隐晦、依赖上下文**：如"夏五月"常省略年份与国君，需从编年体结构与话语连续性中推断；
  - **非公历、以君主为中心**：采用"国君—纪年—月"的纪年体系，时间参考随君主更替而重置，无法用单调日历直接比较；
  - **时间与内容深度耦合**：独特事件本身可充当时间锚点，无法把时间当作独立元数据字段。
- **具体失败模式**（见图1）：
  - 检索到**同月但仅重复日期短语的注疏**（不回答事件本身）；
  - 检索到**相邻月份的近邻事件**，措辞高度混淆；
  - 一旦绑定到时间错误但语义合理的证据，下游生成器仍会给出流畅却"时间错误"的答案。
- **核心研究问题（Q）**：如何在非公历、以纪年为基准的时间体系下，让检索器选出时间一致的证据？
- **整体含义**：论文主张**检索时的时间一致性是忠实历史 RAG 的关键前提**，并以《春秋》及其训释传统为试验台，连接古籍训释与 RAG 检索两个领域。

---

## 2. 方法论

### 2.1 基准构建：ChunQiuTR

- **语料**：以《春秋》经文为锚点，配合三传（左氏、公羊、谷梁）及后世训释（顾栋高《春秋大事表》、魏了翁《春秋左传要义》、杜预注、孔颖达疏等）。
- **时间键（time key）**：将时间归一化为月级三元组 **τ = (gong, year, month)**（国君、纪年、月份），共覆盖 3036 个纪年月，包括无记事月份（以标准化 `no_event` 占位记录表示）。
- **记录对齐**：以事件级短文本为原子检索单元，对同一 τ 下的经文与三传片段做事件分组，LLM 仅提出候选切分，**人工逐条核验**。
- **时间近邻反事实负例（chrono-near counterfactuals）**：将后世训释中与同一时间键共位但措辞/侧重点不同的段落作为**硬负例**，构成真实检索失败模式。
- **查询类型**：
  - **P-Time（点查询）**：目标单一时间键；
  - **G-Time（间隙查询）**：目标区间内的无事件月份；
  - **W-Time（窗口查询）**：围绕某事件的前/后/周围/显式区间。
- **数据划分**：按君主 reign 内连续月份块划分，约 80/10/10，保证无时间键、记录或查询跨 split 泄漏。

### 2.2 检索方法：CTD（Calendrical Temporal Dual-encoder）

- **整体思路**：在语义双编码器基础上，注入**绝对历法上下文**与**相对时间偏置**，使匹配不仅语义一致、而且历法位置一致。
- **（1）潜在历法标量（Latent Calendar Scalar）**：
  - 在共享 Transformer 编码器的池化嵌入 h_x 上，附加三个轻量预测头，分别对 gong / year / month 输出分布 p^(g)_x, p^(y)_x, p^(m)_x；
  - 取期望得到软坐标 g_x, y_x, m_x，再线性归一化到 [0,1]，得到**共享潜在时间标量 u_x**：
    - u_x = [g_x·(Y·M) + y_x·M + m_x] / (G·Y·M − 1) ∈ [0,1]
  - 该标量使时间距离 ∆u_ij = u_{d_j} − u_{q_i} ∈ [−1,1] 可度量。
- **（2）绝对时间学习（Absolute-Temporal Learning）**：
  - 用**固定正弦码本** E^(g), E^(y), E^(m) 映射各历法索引，避免为稀疏索引学习大嵌入表；
  - 对分布取期望得到软绝对时间上下文 c_x，拼接投影后以**标量门控残差**注入：
    - ĥ_x = h_x + γ·c_x
  - 用富化表示计算相似度 s^abs_ij = ĥ_{q_i}ᵀ ĥ_{d_j} / α；当 γ=0 时退化为纯语义基线。
- **（3）相对时间学习（Relative-Temporal Learning）**：
  - 对时间偏移 ∆u_ij 用傅里叶风格特征 φ(∆u_ij) 编码，经小 MLP 生成加性时间偏置：
    - b^time_ij = ε · MLP(φ(∆u_ij))
  - 最终得分：**s^CTD_ij = s^abs_ij + b^time_ij**，ε 初始接近零，模型可自行降权。
- **（4）训练目标**：
  - **区间重叠多正样本 InfoNCE**：查询区间 Q_i 与记录时间键 I_j 有交集即标记为正样本 P_i，采用多正样本对比损失 L^multi（对称双向）；
  - **辅助历法分类**：对 gong/year/month 头用交叉熵 L^time 监督（仅对记录，查询无标签）；
  - **总目标**：L_total = L^multi + λ_time · L^time。

---

## 3. 实验设计

- **数据集 / 场景**：
  - 主基准 **ChunQiuTR**：20,172 条记录、16,226 条查询（13,053 训练 / 1,520 验证 / 1,653 测试），平均每条查询约 7.2 条正样本记录；
  - **跨语料迁移探针**：从《资治通鉴》处理出的两个子集（Qi Ji：268 记录 / 92 查询；Jin Ji：820 记录 / 119 查询），不做目标语料训练。
- **评估指标**：R@1、R@5、R@10、MRR@10、nDCG@10。
- **对比方法（覆盖四大类）**：
  - **稀疏检索**：BM25、BM25+TimeKDE（时间重排先验）、SPLADE-IDF、SPLADE-ℓ0；
  - **融合 / 后交互**：ColBERT-JINA、ColBERT-LFM2；
  - **编码器型稠密检索**：mE5-Large、GTE-Large、BGE-Large-v1.5、BGE-m3、BERT-base（微调）、BERT-base + TempDate / TempDate-Smooth；
  - **LM 型稠密嵌入**：GTE-Qwen2-1.5B、E5-mistral-7B、PQR（Qwen2.5-7B / Qwen3-8B）、Qwen3-Embed-0.6B / 4B（零样本与微调）、Qwen3-Embed-0.6B + TempDate / TempDate-Smooth。
- **主要实验组**：
  1. 主结果对比（表1）；
  2. 跨语料迁移（表2）；
  3. 查询跨度影响（单月 vs 多月，表3）；
  4. 定性示例（图4、图9）；
  5. 消融实验（Qwen3 与 BERT 双骨干，表4、表12）；
  6. 无事件查询与硬负例行为（表13）；
  7. 完整协议网格（表14、表15）。

---

## 4. 资源与算力

论文在附录 B.1.2 中明确给出了算力信息：

- **硬件**：
  - BERT-base-chinese：单卡（1× NVIDIA RTX A6000，或 2× RTX 3090）；
  - Qwen3-Embed-0.6B：多卡分布式（2× RTX A6000，或 4× RTX 3090），以支持全局批内负例。
- **训练时长 / GPU 小时**（表11）：
  - BERT-base FT baseline：约 15 分钟，约 0.25 GPU 小时；
  - BERT-base CTD（完整）：约 19 分钟，约 0.32 GPU 小时；
  - Qwen3-Embed-0.6B FT baseline：约 45 分钟，约 1.50 GPU 小时；
  - Qwen3-Embed-0.6B CTD（完整）：约 45 分钟，约 1.50 GPU 小时。
- **训练超参**：BERT 5 epoch、batch 64、lr 2e-5、查询/段落长度 64/196；Qwen3 3 epoch、有效 batch 16、lr 3e-6、长度 128/256；λ_time=0.1，标签平滑 ε=0.2；AdamW，warmup 0.1，线性学习率调度。未做大规模超参搜索，以验证集 R@1 选检查点。
- **总体评价**：训练成本极低（总计不到 4 GPU 小时），说明方法轻量；但文中未给出数据构建（人工核验）的人力成本估计。

---

## 5. 实验数量与充分性

- **实验组数量**：约 7 大组实验，涵盖主结果（含 20+ 个对比系统）、跨语料迁移、查询跨度分析、定性案例、双骨干消融、协议开关分析、完整评估网格。
- **充分性评估**：
  - **优点**：对比方法覆盖面广（稀疏 / 融合 / 编码器稠密 / LM 稠密 / 时间辅助变体）；在 BERT 与 Qwen3 两个骨干上重复消融；设计了 neg / ne / dq 三个协议开关的完整网格，明确区分"更易"与"更难"的评测设定，避免单一协议误导结论。
  - **公平性**：所有方法在同一官方评测协议、同一 gallery 下比较；no_event 与 neg_comment 记录均纳入候选库；对 BM25+TimeKDE 等时间先验也做了对照，说明增益并非仅来自"时间先验"。
  - **潜在不足**：跨语料迁移实验为"轻量探针"，未重建 no_event、注释硬负例与完整查询族，因此不能等同于第二个基准；此外消融实验主要在 CTD 组件层面，缺少对不同 λ_time、ε、码本维度等超参的敏感性分析。

---

## 6. 主要结论与发现

1. **ChunQiuTR 是一个强时间敏感的基准**：多数零样本稀疏、融合、稠密检索器落后于调优后的 BM25；简单时间先验（BM25+TimeKDE）即可带来大幅提升，说明时间信号是核心难点。
2. **CTD 持续优于强语义双编码器基线**：
   - BERT-base 上 R@1 提升约 +7.4 个百分点（0.5088 → 0.5826）；
   - Qwen3-Embed-0.6B 上 R@1 从 0.5771 提升到 0.5923，MRR@10 与 nDCG@10 亦取得最佳；
   - 通用时间辅助头（TempDate / TempDate-Smooth）几乎无增益，说明**显式时间键监督**比通用日期预测更有效。
3. **多月份查询比单月份查询更容易命中**，但 CTD 在两种情形下均最佳，多月查询增益尤其显著（BERT 上约 +0.16 R@1）。
4. **跨语料迁移有效**：在《资治通鉴》两个子集上，无需目标语料训练，CTD 仍一致提升 MRR 与 R@1，说明时间一致性偏置具有可迁移性。
5. **消融显示两组件互补**：相对时间偏置（b^time_ij）主要提升 R@1，绝对时间上下文（c_x）主要提升整体排序质量，二者结合效果最好。
6. **鲁棒性差异**：注入注释类硬负例后，BERT FT 基线明显下降，而 CTD 保持稳定，说明其更能抵抗时间近邻混淆。
7. **定性发现**：无证据约束时，在线 LLM 会给出"自信的幻觉"或错误的"无事件"判断；有证据包时才能恢复全部金标准条目，表明**长推理链本身不能保证月级完整性**，证据绑定更为关键。

---

## 7. 优点（亮点）

- **问题定位新颖且真实**：首次将"非公历、纪年制"的时间一致性作为检索的一等要求，填补了 TIR 研究多聚焦现代时间戳语料的空白。
- **数据构建严谨**：所有时间键、事件切分、后世注释对齐均经人工核验；LLM 仅用于候选提议，不生成历史内容；给出明确的接受率审计统计（93.33%–100%）。
- **基准设计考虑周全**：
  - 包含 no_event 占位记录，使空月份检索也必须匹配正确的纪年与月份；
  - 引入 chrono-near 反事实硬负例，模拟真实失败模式；
  - 按君主 reign 连续月份划分，严格避免时间泄漏；
  - 提供 neg / ne / dq 协议网格，便于诊断不同难度设定。
- **方法轻量且可解释**：
  - 潜在历法标量把离散纪年键变为可度量的连续轴；
  - 傅里叶固定码本避免稀疏索引的大嵌入表；
  - 门控残差与近零初始化的时间偏置保证可退化为纯语义基线；
  - 训练成本极低（< 4 GPU 小时）。
- **评测公平且全面**：对比系统横跨稀疏、融合、编码器稠密、LM 稠密四大类，并包含通用时间辅助头作为对照，证明增益来自显式时间键监督。

---

## 8. 不足与局限

- **语料范围狭窄**：仅基于《春秋》及其主要训释，时间键为月级、以鲁国君主为中心；结论不一定推广到其他历法体系、叙事风格或编辑传统的古籍。
- **时间粒度受限**：月级是最细的可稳定恢复单位，无法表达月内更细的时间关系；剩余错误集中在相邻月份近重复记录与本身存在史学歧义的案例。
- **跨语料验证偏轻**：Zizhi Tongjian 探针未重建 no_event、注释硬负例与完整查询族，只能作为迁移性证据，而非完整第二基准。
- **偏差风险**：
  - 数据来源、注释筛选、月份键归一化等构建选择可能引入源自原始材料与策展流程的偏差；
  - 检索错误或时间错位若被当作权威证据，可能误导下游历史解释，论文建议在学术/教育场景中配合人工核验使用。
- **应用限制**：下游端到端 RAG 效果尚未系统评估；论文建议未来引入更强的重排序或证据校验模块，并将基准扩展到更广的历史语料与更细时间粒度。
- **超参敏感性未充分探索**：λ_time、ε、码本维度等关键超参缺少系统性分析。

---

（完

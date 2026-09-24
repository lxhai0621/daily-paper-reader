---
title: Enhancing Multimodal Large Language Models for Ancient Chinese Character Evolution Analysis via Glyph-Driven Fine-Tuning
title_zh: 通过字形驱动微调增强多模态大模型对古汉字演变的分析能力
authors: "Rui Song, Lida Shi, Ruihua Qi (祁瑞华), Yingji Li, Hao Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1043.pdf"
tags: ["query:ancient-text"]
score: 8.0
evidence: 面向古汉字演变的MLLM基准与微调
tldr: 多模态大模型在古文字研究中的应用日益受到关注，但如何系统利用其分析汉字演变仍缺乏探索。本文构建了包含十一项任务、逾十三万实例的基准，用于评估多模态大模型分析古汉字演变的能力，并开展跨模型评测。基于此提出字形驱动的微调方法以提升模型表现。该工作推动了古籍文字语义分析与数字化处理研究。
source: ACL-2026-Long
selection_source: conference_retrieval
motivation: 多模态大模型在古汉字演变分析上的应用尚缺系统探索，缺乏评估基准与针对性方法。
method: 构建含11项任务、超13万实例的古文字演变基准，并提出字形驱动微调增强模型能力。
result: 在多款主流多模态大模型上开展广泛评测，验证字形驱动微调对古文字分析任务的提升。
conclusion: 该工作为古籍文字语义分析与数字化处理提供了基准与方法，推动数字人文研究。
---

## Abstract
In recent years, rapid advances in Multimodal Large Language Models (MLLMs) have increasingly stimulated research on ancient Chinese scripts. As the evolution of written characters constitutes a fundamental pathway for understanding cultural transformation and historical continuity, how MLLMs can be systematically leveraged to support and advance text evolution analysis remains an open and largely underexplored problem. To bridge this gap, we construct a comprehensive benchmark comprising 11 tasks and over 130,000 instances, specifically designed to evaluate the capability of MLLMs in analyzing the evolution of ancient Chinese scripts. We conduct extensive evaluations across multiple widely used MLLMs and observe that, while existing models demonstrate a limited ability in glyph-level comparison, their performance on core tasks-such as character recognition and evolutionary reasoning-remains substantially constrained. Motivated by these findings, we propose a glyph-driven fine-tuning framework (GEVO) that explicitly encourages models to capture evolutionary consistency in glyph transformations and enhances their understanding of text evolution. Experimental results show that even models at the 2B scale achieve consistent and comprehensive performance improvements across all evaluated tasks. To facilitate future research, we publicly release both the benchmark and the trained models.

---

## 论文详细总结（自动生成）

# 论文总结：通过字形驱动微调增强多模态大模型对古汉字演变的分析能力

## 1. 核心问题与研究背景

- **研究动机**：古文字（甲骨文、金文、篆文、隶书、楷书）是理解中国文化传承与历史连续性的基本路径。近年来多模态大模型（MLLMs）在古文字识别与考释中展现出潜力，但**如何系统性地利用 MLLMs 支持"文字演变分析"仍是一个开放且被严重忽视的问题**。
- **核心缺口**：
  - 现有工作多聚焦于甲骨文等单点任务（识别、考释），缺乏对**演变分析能力**的系统评估基准；
  - 缺乏针对"字形演变一致性"的增强方法。
- **整体含义**：论文同时贡献了一个**评估基准**与一个**字形驱动微调框架（GEVO）**，目标是让 MLLMs 真正理解汉字从甲骨文到楷书的形态演化过程，推动数字人文与古籍智能处理。

## 2. 方法论

### 2.1 基准构建（Benchmark Construction）

- **数据来源与划分**：
  - 参考已有工作将演变过程划分为 5 个阶段：甲骨文 → 金文 → 篆文 → 隶书 → 楷书；
  - 从 Vividict 抽取数据，统一组织为"同一字符在一段时期内可有多种写法"的结构，增强语料丰富性；
  - 对字体文件统一二值化，人工剔除缺失、损坏、空白样本，最终得到 **7,740 个汉字、近 30,000 个摹本（facsimile）** 的演变数据集；
  - 按 **9:1** 随机划分训练/测试集。
- **11 个任务 / 3 大类**：
  - **Task 1 书体识别**：T1.1 单图书体判断、T1.2 同字异形是否同书体、T1.3 异字异形是否同书体、T1.4 多图中找出书体不同者；
  - **Task 2 字形识别**：T2.1 任意书体识读现代汉字、T2.2 同书体两字是否同字、T2.3 异书体两字是否同字、T2.4 多图中找出不同字者；
  - **Task 3 演变路径任务**：T3.1 依据演变路径识别汉字、T3.2 打乱路径的时间排序、T3.3 路径缺段补全（转为四选一）。
  - 合计 **逾 130,000 个具体问题**。
- **指令构建流程**：先由古文字专家定义任务范围 → ChatGPT 生成候选指令 → 专家筛选修改 → 在 Qwen3/InternVL 等本地模型上验证能否产生规范输出 → 迭代优化，确保指令有效性与模型合规性。

### 2.2 GEVO：字形驱动的课程学习式微调框架

核心思想是**课程学习**：从易到难、从字形到语义再到任务，分三阶段渐进式训练。

- **Stage 1：字形对比学习（视觉模块）**
  - 冻结语言模型，**更新视觉编码器与跨模态投影模块**；
  - 对同一汉字在不同历史时期的图像集合视为**正样本** P = {I₁, …, Iₙ}；
  - 用 **CLIP** 检索与目标字符视觉最相似但不属于该字的 top-k 字形作为**负样本** N，以缓解相似字干扰；
  - 优化对比损失（InfoNCE 形式）：
    - L_con = −(1/|P|) Σ_{Iᵢ∈P} log [ S⁺ᵢ / (S⁺ᵢ + S⁻ᵢ) ]
    - 其中 S⁺ᵢ = Σ_{Iⱼ∈P, j≠i} exp(s(zᵢ,zⱼ)/τ)，S⁻ᵢ = Σ_{I⁻∈Nᵢ} exp(s(zᵢ,z⁻)/τ)，s 为余弦相似度。
- **Stage 2：图像—文本映射**
  - 冻结视觉模块，**微调语言模型**，让模型根据任意历史时期的字形图像预测对应的现代汉字，捕捉语义关联。
- **Stage 3：任务指令微调（SFT）**
  - 在每个任务上仅使用 **200 条训练样本** 进行 SFT，降低微调成本，得到最终模型 **GEVO**。

## 3. 实验设计

- **评测对象**：19 个 MLLM（1B–72B 规模）：
  - 闭源：GPT-4o-mini、GPT-5-mini、Gemini-3-Flash；
  - 开源：TongGu-VL-2B、Qwen2.5-VL 系列（7B/32B/72B）、Qwen3-VL 系列（2B/8B/30B-A3B）、InternVL3_5 系列（1B/8B/14B）、MiniCPM-V-2_6 / 4_5、GLM-4.1V-9B-Thinking、DeepSeekOCR-3B、LLaVA-1.5 系列（7B/13B）。
- **基准**：自建 11 任务、13 万+ 实例的古汉字演变基准（主实验在测试集上，附录给出全量数据结果）。
- **对比与消融**：
  - 与上述 19 个基线模型对比；
  - **Qwen3-VL-2B-SFT**：仅用每任务 200 样本直接 SFT；
  - **GEVO-Stage1**：只做阶段 1 + 阶段 3（跳过图像-文本映射）；
  - **GEVO-Stage2**：跳过阶段 1 对比学习，只做阶段 2 + 阶段 3；
  - **GEVO（完整三阶段）**，并用 **Wilcoxon 符号秩检验（p < 0.05）** 验证显著性。
- **OOD 泛化实验**：从 OBIseEvolution 抽取 150 字符、人工过滤后得 **148 字符 / 717 摹本**的小规模 OOD 集（T1.2、T2.2 因每字仅一个版本而无法评测）。
- **可视化分析**：对"日/口""力/刀""万/方"等形近字做二维表征分布对比。
- **评价指标**：准确率；T3.2 采用宽松评测（按路径中每个位置是否正确计分）。

## 4. 资源与算力

- **GPU**：**4 × A100 80GB**；
- **微调框架**：LlamaFactory；
- **训练配置**：任务 SFT 阶段学习率 1e-5、3 个 epoch、warmup 比例 0.1；
- **微调方式**：**全参数微调（未使用 LoRA）**；
- **成本说明**：文中提及闭源模型调试+评测成本超过 500 美元，因成本限制仅评测 3 个闭源模型；
- **未明确说明**：三阶段的总体训练时长、各阶段具体步数与数据规模细节未完全给出（仅给出损失曲线，见附录图 15–17）。

## 5. 实验数量与充分性

- **实验组数**：
  - 19 个模型 × 11 个任务的完整评测（Table 1）；
  - 全量数据（训练+测试）上的评测（附录 Table 4）；
  - 4 组微调变体对比（Qwen3-VL-2B-SFT、GEVO-Stage1、GEVO-Stage2、GEVO）；
  - 1 组 OOD 泛化实验（3 个模型 × 9 个任务）；
  - 3 组表征可视化分析 + 3 张训练损失曲线。
- **充分性评估**：
  - **优点**：覆盖模型规模跨度大（1B–72B）、开源与闭源兼顾、任务体系完整、含消融与 OOD 验证，并做了显著性检验，整体较为充分；
  - **公平性**：所有模型使用统一构造的指令与评测流程，SFT 基线使用相同样本与训练策略，比较相对客观；
  - **不足**：闭源模型仅 3 个且受成本限制；OOD 数据集规模较小（148 字符/717 摹本）；T1.2、T2.2 在 OOD 中缺失，覆盖略不完整。

## 6. 主要结论与发现

- **现有 MLLM 能力画像**：
  - 字形**比较/书体判别**能力尚可（部分任务优于随机），但**字符识别（尤其甲骨文、金文）能力极弱**（甲骨文识别准确率普遍低于 10%）；
  - 越接近现代的书体（隶书、楷书）识别准确率越高，符合汉字向现代形态收敛的演化规律；
  - 甲骨文/金文/篆文之间、隶书/楷书之间存在明显混淆，反映相邻时期书体高度相似；
  - **在显式演变路径语境下**，识别与书体判别表现提升，说明演变过程建模的价值；
  - 闭源模型常出现拒答或识别失败，平均表现甚至弱于部分本地开源模型。
- **微调潜力**：
  - 少量样本 SFT（Qwen3-VL-2B-SFT）平均提升超 30%，甚至超过 8B 模型 10% 以上，但**T2.1、T3.1 出现退化**，存在灾难性遗忘；
  - 结论提炼为两条原则：(i) 少量样本足以增强"相似字形判别"；(ii) 稳健识别需要更充分多样的数据。
- **GEVO 效果**：
  - 在全部任务上一致提升，平均准确率达 **83.54%**，显著优于所有被评测的基线（含 72B 模型）及 SFT 变体（p < 0.05）；
  - 相比 SFT，GEVO 在 T1.1 和 T2.1 上均提升超 10%；
  - 在 OOD 集上同样全面优于基线，具备较好泛化性与鲁棒性；
  - 可视化显示 GEVO 对同字不同书体表征更聚集、形近异字距离更远。
- **仍然存在的困难**：GEVO 字符识别仅 39.18%，甲骨文/金文识别仍受限；对极端相似字形（如"日"与"口"）区分能力不足。

## 7. 优点

- **贡献完整且闭环**：同时提供基准、系统性评测与增强方法，形成"发现问题—分析原因—提出方法—验证效果"的完整链条。
- **任务体系设计科学**：11 个任务从书体识别、字形识别到演变路径推理层层递进，且每个任务的引入动机均有解释（附录 A）。
- **指令构造严谨**：专家 + ChatGPT + 模型验证的迭代流程，兼顾专业性与模型可执行性。
- **方法设计有针对性**：用 CLIP 检索硬负样本构造对比学习，显式建模"字形相似但字义不同"的难点，契合古文字学需求。
- **课程学习三阶段解耦**：先学字形、再学语义、后学任务，并通过消融证明各阶段不可偏废，结论有说服力。
- **轻量高效**：每任务仅 200 样本 SFT，2B 模型即可超越 72B 基线，具备实际部署价值。
- **公平性保障**：统一评测流程、相同训练策略、统计显著性检验、OOD 验证。

## 8. 不足与局限

- **数据形态限制**：仅使用较简单的手摹摹本，**未涉及噪声大、字形高度不一致的拓片（ink rubbings）**，与真实考古场景存在差距。
- **识别性能不足**：字符识别准确率（GEVO 39.18%）仍远低于实际应用要求，甲骨文/金文等早期书体提升有限。
- **闭源模型覆盖少**：因成本限制仅评测 3 个闭源模型，未能覆盖更多、更大规模的闭源系统，结论的外部有效性受限。
- **语义信息未纳入**：作者自己指出，字形演变过程中**语义的整合至关重要**，但相关语料稀缺，本文未能实现。
- **形近字区分仍有瓶颈**：对"日/口"等极端相似字形仍难以区分。
- **OOD 实验规模小**：148 字符 / 717 摹本，且 T1.2、T2.2 无法评测，泛化结论的稳健性证据有限。
- **算力细节披露不足**：未给出各阶段具体训练时长、步数与数据规模，复现细节需依赖附录补充。
- **潜在偏差风险**：数据主要来自 Vividict 与 OBIseEvolution，甲骨文样本量本身有限（可靠对应现代汉字的仅两千余字），可能带来长尾与分布偏差。

（完）

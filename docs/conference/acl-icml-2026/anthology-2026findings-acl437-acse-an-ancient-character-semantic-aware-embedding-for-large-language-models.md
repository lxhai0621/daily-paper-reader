---
title: "ACSE: An Ancient Character Semantic-Aware Embedding for Large Language Models"
title_zh: "ACSE:面向大语言模型的古文字语义感知嵌入"
authors: "Zhihan Zhou, Daqian Shi, Lida Shi, Rui Song, Peiqiang Qiu, Xiaolei Diao, Hao Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.437.pdf"
tags: ["query:ancient-text"]
score: 8.0
evidence: 面向古文字、映射到现代语义空间的语义感知嵌入
tldr: "甲骨文、金文、楚简等先秦出土文献数字化程度低、训练语料稀缺,且古文字蕴含复杂丰富的语义信息,现有大模型研究不足。本文提出古文字语义感知嵌入ACSE,融合字形与词义信息,将古文字映射到现代汉语语义空间,并设计两阶段轻量化参数方法。该工作为古籍语义分析与知识抽取提供有效的表示学习手段,推动古文字数字处理与语义理解。"
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl437/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 2994, \"height\": 1236}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl437/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 3057, \"height\": 2080}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl437/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 4172, \"height\": 1192}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl437/fig-004.webp\", \"caption\": \"\", \"page\": 8, \"index\": 4, \"width\": 4710, \"height\": 972}]"
motivation: "先秦出土文献数字化程度低、语料稀缺,古文字语义复杂,大模型相关研究不足。"
method: "提出融合字形与词义的古文字语义感知嵌入ACSE,将其映射到现代汉语语义空间,并采用两阶段轻量化方法。"
result: "该嵌入为古文字提供有效语义表示,提升大模型对古籍语义信息的建模与理解能力。"
conclusion: 字形与词义联合的语义感知嵌入可推动古文字数字化处理与古籍语义分析。
---

## Abstract
Research on ancient Chinese language is of great significance for tracing Chinese history and civilization. In the field of large language models, studies on the pre-Qin excavated documents such as Oracle Bone Inscriptions, Bronze Inscriptions, and Bamboo Book of Chu remain insufficient. This is because these ancient characters have a low level of digitization, training corpora are extremely scarce, and they typically contain complex and rich semantic information. Therefore, we propose an ancient character semantic-aware embedding for large language models. This embedding integrates both the glyph and lexicality of ancient characters and maps them to the modern Chinese semantic space. We also design a two-stage method for lightweight and parameter-efficient training of the embedding. Finally, we conduct extensive experiments on excavated documents from the pre-Qin period, and the results demonstrate the effectiveness of our approach.

---

## 论文详细总结（自动生成）

# ACSE：面向大语言模型的古文字语义感知嵌入——论文总结

## 1. 核心问题与研究动机

- **背景**：古汉语研究对追溯中华文明、保护文化遗产和推进历史语言学意义重大。大语言模型（LLM）虽已重塑 NLP 诸多领域，但对古文字的解读能力仍然有限。
- **研究缺口**：既有古汉语工作（如 Xunzi、Tonggu、SikuGPT 等）主要面向**传世文献**；对甲骨文、金文、楚简等**先秦出土文献**的研究仍严重不足。
- **三大困难**：
  - **数字化程度低**：大量古文字未被 Unicode 收录，无法进入现代计算标准；
  - **语料极度稀缺**：不足以支撑从零学习高质量表示；
  - **语义复杂丰富**：古文字多为象形，构件本身即承载意义；且字义随媒介与历史时期漂移（如甲骨文"休"字形似人倚树，后世又衍生出"休息/停止/罢免/吉凶"等义）。
- **现有方案的问题**：为主流做法是"新增 token 索引 + 微调"，但新索引对应的嵌入需依赖手工启发式初始化，必须大量领域数据才能学好——这与先秦出土语料的稀缺性直接冲突。
- **核心洞察**：现代汉字是长期演化的产物，许多古文字语义线索仍直接或间接保留在现代部首、词汇模式与语义分布中；LLM 已掌握现代汉语的深层语义/句法规律。因此**应构建"古文字→现代汉语语义空间"的稳健映射，利用共享表示而非大规模重新预训练**。
- **切入点**：Qwen2.5 的 **BBPE 分词器**在字节粒度编码，古今字符天然共享同一字节/索引空间，无需扩展词表即可表示任意 Unicode 字符。

## 2. 方法论

### 2.1 核心思想
将古文字的**字形（glyph）**与**词义（lexicality）**两类独特特征建模为嵌入，并与原始 token 嵌入融合，投影到现代汉语语义空间；配合两阶段参数高效训练，在低资源下激活 LLM 已有的现代汉语知识。

### 2.2 关键流程（文字化说明）

**（1）古文字词表与索引空间构建**
- 采用 **InteChar**（整合未编码甲骨文字符 + 繁体 + 现代简体的统一字符表）作为古文字词表 $V_{char}$；
- 用 Qwen2.5 tokenizer 编码 $V_{char}$，得到古文字索引子序列词表 $V_a = \text{tokenizer}(V_{char})$。

**（2）古文字特征模块（Ancient Character Feature Module）**
- 定义字形嵌入 $E_{glyph}$ 与词义嵌入 $E_{lexical}$，均为 $|V_{char}| \times h$；
- 输入句子经 tokenizer 得到索引序列 $S_w$，遍历其全部子序列 $S_x$；
- 若某子序列 $x$ 落在 $V_a$ 中（即输入含古文字），则查表取出对应字形/词义嵌入，**乘以全 1 向量 $1_{|x|}$ 并取平均**（以对齐原始嵌入的形状），得到特征集合 $E_f$。

**（3）特征融合模块（Feature Fusion Module）**
- 对命中的子序列 $x$：将字形嵌入与词义嵌入**拼接** → 经线性层 $W E_c^x + b$ → 乘可学习标量 $\alpha$，得 $E_{anc}^x$；
- 最终新嵌入 $E_{new}$：若为古文字子序列则 $E_o^x + E_{anc}^x$（与原嵌入相加融合），否则保持原嵌入 $E_o^x$ 不变；
- 融合后的嵌入送入后续 Transformer 层推理。

**（4）两阶段训练**
- **第一阶段：注入字形/词义先验**。基于古文字知识图谱与《说文解字》构建字形数据集（13,925 条，古文字↔构件，含不同历史时期的多种构件对应）与词义数据集（3,893 条，古文字↔训释）。采用**对比学习 + InfoNCE 损失**：古文字与其对应字形/词义为正样本，其余全部为负样本；嵌入先做 L2 归一化（含 $\epsilon$ 稳定项）再计算损失，温度参数 $\tau$。目标是"把古文字映射进现代汉语表示空间"，而非改变该空间本身。
- **第二阶段：特征融合与推理**。构建古文字指令微调数据集，载入第一阶段训练好的字形/词义嵌入，**冻结模型参数与嵌入参数**，仅训练线性层与 $\alpha$，做端到端指令微调，损失为标准自回归语言建模损失（仅对目标 token 计算，掩码 $m_{i,t}$ 控制）。

### 2.3 预实验支撑
- 统计 Qwen2.5 tokenizer 下古今字符集的索引重叠：古文字集 2,909 字、现代汉字集 8,827 字，其中 **2,696 字存在索引重叠**；索引 165 在两者中均为最高频，99551、99643、100563 等也同处前 20。说明 BBPE 下古今索引共享高度普遍。

## 3. 实验设计

- **数据集 / Benchmark**：**AncientBench**（面向先秦出土文献的基准），选取 4 个任务：
  - Radical（部首，8,438 条）与 Radical Meaning（部首含义，1,432 条）——考察**字形能力**；
  - ExcDoc Word（出土文献词义，364 条）——考察**词义能力**；
  - Phonetic Loan Character（通假字，4,636 条）——考察**语境能力**。
- **数据划分**：每个任务按 3:7 划分训练/评估（30% 训练），再把四个任务的训练部分合并为统一指令微调集；评估在各任务独立测试集上进行。设计目的是避免模型见到验证答案，同时用尽量多数据做验证。
- **对比方法**：
  - **现代中文 LLM（8 个）**：Qwen-7B-Chat、Llama3-8B-Instruct、Baichuan2-7B-Chat、Yi1.5-9B-Chat、Baichuan2-13B-Chat、GLM4-9b-chat、Qwen-14B-Chat、Qwen2.5-7B-Instruct；
  - **古汉语 LLM（3 个）**：Tonggu-7b-chat、Xunzi-Qwen-Chat、Yi1.5-9B-Ancient；
  - **微调方法（4 个）**：Prefix、Adapter、BitFit、LoRA（对比基座均为 Qwen2.5-7B-Instruct）。
- **评估设置**：全部报告 **0-shot 与 5-shot** 准确率。
- **表示空间可视化**：以余弦相似度为度量，用多维尺度变换（MDS）将古文字与其字形/词义映射到 2D 空间，对比原始嵌入与 ACSE。
- **消融实验**：分别移除字形嵌入、词义嵌入（5-shot）。
- **额外验证**：在 Llama3-8B-Instruct 上做 5-shot 实验以检验方法可迁移性。

## 4. 资源与算力

- 论文明确提到的硬件仅为：**Ubuntu 操作系统 + Ascend-910B NPU**。
- 训练超参：第一阶段 batch size 16、学习率 3e-4、$\tau=0.1$、12 个 epoch；第二阶段 batch size 2、学习率 1e-3、AdamW 优化器、3 个 epoch。
- **未明确说明**：NPU/GPU 的**数量**、总训练时长、总显存/算力开销均未给出。这是资源报告上的一个明显缺口。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 模型维度对比：11 个模型 × 4 任务 × 2 种 shot 设置（表 1）；
  - 微调方法维度对比：4 种方法 + Origin + ACSE × 4 任务 × 2 种 shot（表 2）；
  - 消融：移除字形 / 移除词义 2 组 × 4 任务（表 3）；
  - 可视化：字形对（原始 vs. ACSE）与词义对（原始 vs. ACSE）共 4 张子图；
  - 跨骨干验证：Llama3-8B-Instruct ± ACSE（表 4）；
  - 预实验：BBPE 索引重叠统计。
- **充分性评价**：
  - **优点**：基线覆盖面较广（现代 LLM、古汉语专用 LLM、通用 PEFT 方法三类齐备），同时报告 0-shot 与 5-shot，并做了消融与跨骨干验证，整体较为完整。
  - **需注意的公平性细节**：
    - ACSE 使用了**额外的先验数据**（InteChar 字形数据 13,925 条、ShuoWen 词义数据 3,893 条）进行对比学习，而 Prefix/Adapter/BitFit/LoRA 基线并未使用同类外部知识，两者并非严格等量信息条件下的比较；
    - ACSE 与基线的**可训练参数量不同**（ACSE 训练线性层 + α，并额外引入两套嵌入表），参数量对齐情况文中未详述；
    - 未报告多次运行的方差、显著性检验或随机种子设置。
  - **结论**：实验规模在同类低资源古文字工作中属较充分，但"外部知识注入"与"参数量差异"使得与通用微调方法的对比存在一定不可比性。

## 6. 主要结论与发现

- **主结果**：ACSE-Qwen2.5-Instruct 在 4 个任务上整体领先——
  - Radical：0-shot **62.02**、5-shot **70.01**（较当时 SOTA 提升 **14.46**）；
  - Radical Meaning：**66.53 / 72.61**（提升 **21.25**）；
  - ExcDoc Word：80.52 / **81.91**（该任务 5-shot 上 LoRA 的 82.42 更高）；
  - Phonetic Loan Character：**65.87 / 77.94**（提升 **17.28**）。
- **提升来源**：现有 LLM 的分词过程基本排除了甲骨文、金文、楚简等字符，ACSE 的古文字词表与特征模块填补了这一信息空白。
- **5-shot 普遍优于 0-shot**（在所有任务上），而基线模型并不总是如此——原因在于指令微调格式（问答式）与评测格式（选择题）存在差异，需要少量示例作为参照。
- **通用微调方法可能有害**：Prefix 与 Adapter 导致性能大幅负迁移，四个任务得分跌至接近 25%（随机猜测水平）。推测原因是古今字符共享索引，微调时新知识会扰动原有表示，缺乏结构引导会破坏表示空间。这提示传统 PEFT 不完全适用于先秦出土文献场景。
- **消融结论**：移除字形或词义嵌入任一者均导致显著下降（如 Radical Meaning 移除词义后下降 **22.71**），两者作用量级相近，缺一即退化到原始嵌入或 LoRA 水平，证明二者**不可替代**。
- **可视化结论**：原始嵌入中古文字与字形/词义分布在对立两侧且古文字稀疏分散；经 ACSE 训练后，古文字与其字形/词义距离显著缩小、分布更均匀，说明成功映射到现代汉语语义空间。
- **跨骨干验证**：Llama3-8B-Instruct 加 ACSE 后 Radical 43.96→48.41、Radical Meaning 38.52→47.21、Phonetic Loan 53.27→68.88，但 ExcDoc Word 从 74.52 降至 69.80，说明迁移性存在任务依赖性。

## 7. 优点

- **问题定位精准**：明确区分"传世文献"与"先秦出土文献"，填补了后者在 LLM 领域的空白。
- **设计巧妙且低资源友好**：利用 BBPE 的字节级共享索引空间，避免扩展词表与从零训练新 token 嵌入；并先用索引重叠统计做了量化预验证，为设计选择提供实证依据。
- **特征建模契合领域特性**：同时建模"字形（构件承载语义）"与"词义（历时演变）"，并用"映射到现代语义空间"而非"重造表示空间"的思路，最大化了现代 LLM 的既有知识。
- **训练策略务实**：两阶段设计（先注入先验、再学融合推理）配合冻结主干、仅训线性层与 α 的参数高效微调，适配语料稀缺现实。
- **评测多维**：从"模型维度"和"微调方法维度"双向验证，辅以 MDS 可视化的定性证据与消融的定量证据，论证链条较完整。
- **诚实报告负结果**：如实呈现 ExcDoc Word 上未超过 LoRA/BitFit，以及 Prefix/Adapter 的灾难性退化，具有诊断价值。

## 8. 不足与局限

- **模态局限**：仅利用文本模态捕捉语义，未引入

- **模态局限**：仅利用文本模态捕捉语义，未引入古文字的**视觉/图像模态**（如甲骨拓片、金文拓本、简帛字形图像）。而古文字"象形"特性使字形本身具有强烈视觉信息，纯文本的构件描述难以完整还原书写形态、笔画结构与异体差异，可能丢失部分语义线索。
- **先验知识来源的局限**：字形数据集与词义数据集主要基于古文字知识图谱与《说文解字》构建。《说文》以小篆为字形基础、以汉代训释为释义依据，对甲骨文、金文等更早期材料可能存在**时代错位**（用后世字形/释义去解释更早文字），从而影响先验质量；论文未讨论这一偏差如何传播到嵌入中。
- **数据规模与统计效力**：各任务评估集规模偏小（如 ExcDoc Word 仅 364 条，按 3:7 划分后测试集约 250 条左右），单条样本的波动即可带来数个百分点变化；论文未报告置信区间或标准差，因此**主结果中"领先幅度"的稳健性有待验证**（例如 ExcDoc Word 上 ACSE 与 LoRA 的差距仅约 0.5）。
- **对比公平性**：如第 5 节所述，ACSE 额外使用了数万条外部先验数据与两套嵌入表，而 Prefix/Adapter/BitFit/LoRA 基线未获得等价的外部知识；严格来说这是"知识注入 + 参数高效微调"与"纯参数高效微调"的对比，而非同条件方法对比。论文也未给出与"同样注入先验知识后再 LoRA"的对照，无法完全分离**先验数据贡献**与**架构设计贡献**。
- **骨干覆盖有限**：跨骨干验证仅补充了 Llama3-8B-Instruct，且在该骨干上 ExcDoc Word 出现下降，说明方法**并非对所有模型、所有任务都稳定增益**；未在更多架构（如 GLM、Baichuan、Yi、Mistral 等）或更大规模模型上验证可扩展性。
- **任务与指标单一**：AncientBench 的 4 个任务均以**选择题/分类**形式评估，指标仅用准确率；未涉及古文字释读中更贴近实际需求的**生成式任务**（如整句翻译、缺字补全、释文生成），也未使用 F1、BLEU 等更细粒度指标，难以全面刻画模型的实际古文字理解能力。
- **缺少与专门古文字嵌入/检索方法的对比**：对比对象集中在通用 LLM 与通用 PEFT 方法，未与已有的古文字字形嵌入、甲骨文检索/释读模型等专门方法比较，难以判断 ACSE 在领域内的相对位置。
- **超参与敏感性分析缺失**：两阶段训练涉及温度 $\tau$、可学习标量 $\alpha$、对比学习负样本构造、两阶段 epoch 数等多个关键超参，论文未做敏感性分析或消融其影响；尤其"全部其余样本为负样本"的策略可能引入**假负样本**（语义相近的古文字互为负例），对表示质量的影响未被讨论。
- **可解释性有限**：虽用 MDS 展示了映射效果，但未分析具体哪些构件/义项对嵌入贡献更大，也未给出失败案例的定性分析，方法内部机制的透明性不足。
- **资源与复现信息不完整**：如第 4 节所述，硬件数量、训练时长、算力开销均未报告，且未提及代码/数据是否开源，影响可复现性。

## 9. 总体评价

ACSE 针对"先秦出土文献在 LLM 中表示缺失"这一真实且长期被忽视的缺口，提出了一个**思路清晰、低资源友好**的解决方案：它不追求扩展词表或重训练 token 嵌入，而是巧妙利用 BBPE 的字节级共享索引空间，把"古文字→现代汉语语义空间"的映射作为核心目标，并用字形与词义两类领域特征加以约束，配合两阶段参数高效训练，在多个任务上取得了显著提升。其"映射而非重建"的核心洞察，对低资源、跨时代、跨书写系统的语言建模具有方法论上的迁移价值。

与此同时，论文的结论仍需谨慎看待：外部知识注入带来的对比不公平、数据规模偏小导致的统计不确定性、先验知识本身的时代偏差，以及跨骨干/跨任务的非一致增益，都提示**ACSE 的收益来源与适用边界尚未被完全厘清**。未来若能在更严格的等条件对比、更大规模的评估、生成式任务与多模态字形信息的引入上加以完善，该方法有望从"有效的方法原型"走向更稳健、更通用的古文字理解框架。

（完）

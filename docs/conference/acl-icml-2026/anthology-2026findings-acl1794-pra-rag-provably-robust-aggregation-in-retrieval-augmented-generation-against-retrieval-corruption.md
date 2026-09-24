---
title: "PRA-RAG: Provably Robust Aggregation in Retrieval-Augmented Generation against Retrieval Corruption"
title_zh: PRA-RAG：面向检索污染的可证明鲁棒聚合检索增强生成
authors: "Xue Tan, Yi Zheng, Chang Huo, Yunruo Zhang, Yu Liu, Hao Luan, Zhuyang Yu, Jun Dai, Xiaoyan Sun, Ping Chen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1794.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 抵御检索投毒的可证明鲁棒聚合
tldr: 检索增强生成在引入外部知识的同时，也面临检索文本被投毒操纵的风险，现有防御方法缺乏理论保证且在模型知识有限时表现不稳。本文提出PRA-RAG，一种可证明鲁棒的检索聚合算法，通过采样多种检索文本组合并利用嵌入空间的几何结构来识别鲁棒子集。实验表明该方法能在检索内容被污染时仍保持可靠输出，为RAG的安全部署提供了理论支撑。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 764, \"height\": 700}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 618, \"height\": 596}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 485, \"height\": 451}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-004.webp\", \"caption\": \"\", \"page\": 8, \"index\": 4, \"width\": 4643, \"height\": 2833}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-005.webp\", \"caption\": \"\", \"page\": 8, \"index\": 5, \"width\": 4631, \"height\": 2810}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-006.webp\", \"caption\": \"\", \"page\": 8, \"index\": 6, \"width\": 4639, \"height\": 2832}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-007.webp\", \"caption\": \"\", \"page\": 14, \"index\": 7, \"width\": 4672, \"height\": 3455}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1794/fig-008.webp\", \"caption\": \"\", \"page\": 14, \"index\": 8, \"width\": 4663, \"height\": 3444}]"
motivation: 检索增强生成易受投毒攻击，现有防御缺乏理论保证且在模型知识有限时不可靠。
method: 提出PRA-RAG，采样多种检索文本组合，利用嵌入空间几何结构识别鲁棒子集。
result: 在检索内容被污染时仍能保持可靠输出，并提供可证明的鲁棒性保证。
conclusion: 为RAG抵御检索投毒提供了理论可靠的聚合方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances Large Language Models (LLMs) by incorporating external knowledge, effectively mitigating their inherent knowledge limitations. However, RAG remains vulnerable to poisoning attacks that manipulate retrieved texts to mislead model outputs. Existing defense mechanisms often lack theoretical robustness guarantees and perform unreliably when the LLM has limited knowledge of the retrieved content. In this work, we propose PRA-RAG, a provably robust retrieval aggregation algorithm designed to defend against poisoning attacks on retrieved texts. PRA-RAG samples multiple combinations of retrieved texts and utilizes geometric structures in the embedding space to identify a robust subset, from which a stable aggregated representation is derived. We provide theoretical bounds on the maximum impact of poisoned retrieved content and establish a quantitative measure of RAG’s robustness. Experiments across multiple benchmarks and RAG architectures demonstrate that PRA-RAG reduces the attack success rate to as low as 1% while maintaining an accuracy of 71%, significantly outperforming representative state-of-the-art (SOTA) methods.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：检索增强生成（RAG）通过引入外部知识库增强大语言模型（LLM），缓解其知识覆盖不足和时效性问题，已被 ChatGPT、Bing Chat、Google Search AI 等广泛采用。
- **核心安全问题**：RAG 的外部知识库可被攻击者投毒。攻击者向语料库注入恶意文本，使检索到的上下文诱导 LLM 输出攻击者指定答案。例如查询“最高山是什么”，系统可能被误导回答“富士山”。
- **现有防御不足**：
  - AstuteRAG、TrustRAG 等依赖 LLM 内部知识进行检测/过滤，当 LLM 对检索内容缺乏足够知识时不可靠。
  - 多数方法缺乏理论鲁棒性保证，无法量化或认证 RAG 在对抗条件下的可靠性。
  - RobustRAG 虽有理论保证，但需多次 LLM 生成，计算开销大。
- **论文整体含义**：提出 PRA-RAG，一种可证明鲁棒的检索聚合算法，在检索阶段通过组合采样和嵌入空间几何结构识别鲁棒子集，理论上限定投毒检索造成的语义偏移上界，并建立量化鲁棒性指标 PAD。目标是在低攻击成功率（ASR）与高准确率（ACC）之间取得平衡。

## 2. 方法论

### 2.1 核心思想

- 将检索投毒视为 **Top-K 集合扰动问题**：攻击者最多改变 ε 个检索项。
- 不依赖 LLM 内部知识，而是在 **嵌入空间** 中对检索文本组合进行鲁棒聚合。
- 通过采样多个检索文本子集，寻找覆盖多数组合的 **最小半径球**，以多数一致性过滤少量投毒文本。
- 对选中鲁棒子集做加权平均，生成稳定聚合表示，再输入 LLM 生成答案。

### 2.2 关键技术细节

- **输入**：查询 q，Top-K 检索文本 \(X=\{p_1,\dots,p_K\}\)，子集大小 n，满足 \(2n<K\)。
- **组合采样**：
  - 枚举或采样所有大小为 n 的子集，数量 \(L=\binom{K}{n}\)。
  - 每个文档编码为嵌入向量 \(e_i\)，子集内嵌入按文本顺序拼接为组合向量 \(v_i\)。
- **距离定义**：
  - 使用角距离 \(d(u,v)=\arccos(\cos(u,v))\in[0,\pi]\)。
- **最小半径球选择**：
  - 寻找中心 z 和半径 R，使球 \(B(z,R)\) 包含超过半数组合向量：
    \[
    F(X)=\arg\min_z R \quad \text{s.t.} \sum_{w\in V_{X,n}} \mathbf{1}_{B(z,R)}(w)\ge \left\lfloor \frac{\binom{K}{n}}{2}\right\rfloor+1
    \]
  - 该中心对应一个鲁棒子集 \(s_{i^*}\)。
- **加权聚合**：
  - 对选中子集中的文本，以文本与查询的相似度 \(sim(p,q)\) 为权重做加权平均：
    \[
    x_{i^*}=\frac{\sum_{p\in s_{i^*}} sim(p,q)\cdot Embed(p)}{\sum_{p\in s_{i^*}} sim(p,q)}
    \]
- **算法流程（Algorithm 1）**：
  1. 生成所有组合 \(S_{X,n}\)；
  2. 对每个子集编码并拼接为 \(v_i\)；
  3. 计算每个 \(v_i\) 到其他组合的角距离，排序后取第 \(k=\lfloor L/2\rfloor\) 小距离作为候选半径；
  4. 选择使该距离最小的组合 \(i^*\)，半径 \(R\) 为其对应距离；
  5. 对 \(s_{i^*}\) 中文本嵌入加权平均，得到鲁棒检索表示 \(x_{i^*}\)。

### 2.3 理论保证与 PAD

- **定理 1**：若 \(X'\) 与 \(X\) 最多相差 ε 个检索项，则
  \[
  d(F(X),F(X'))\le 2R
  \]
- **定理 2**：使用 β-MEB 近似最小包围球后，有
  \[
  d(F(X),F(X'))\le (1+\beta)\hat R
  \]
  论文取 \(\beta=2\)，得到 \(d\le 3\hat R\)。
- **PAD（Provable Average Deviation）**：认证聚合表示语义偏移上界。PAD 越低，表示鲁棒性越强；PAD 越高，表示攻击影响越大。
- **多数球保证**：Lemma 1 证明，在半径取排序距离第 \(k=\lfloor L/2\rfloor+L_{adv}\) 个值时，球内严格包含多数干净组合。
- **几何可分离假设**：干净组合嵌入形成集中簇，含毒组合位于该簇外一定间隔，保证几何聚合可锚定干净子集。
- **Monte Carlo 采样**：当组合数过大时，均匀采样 \(m\ll L\) 个子集，论文设 \(m=200\)。基于 Hoeffding 不等式给出下界 \(R^*\le R\)，实验显示与全枚举偏差约 3% 以内。

## 3. 实验设计

- **数据集**：
  - Natural Questions（NQ）：2,681,468 篇知识库文本，3,452 个问题。
  - MS-MARCO：5,233,329 篇文本，7,405 个问题。
  - HotpotQA：8,841,823 篇文本，6,980 个问题。
- **LLM**：
  - Mistral-7B、Llama3-8B、Vicuna-7B、Qwen3-8B、GPT-3.5-Turbo、GPT-5-mini。
- **攻击方法**：
  - PoisonedRAG（语料投毒攻击）。
  - AdvDec（对抗解码）。
  - DoS Attack（拒绝服务攻击，插入 blocker 文档）。
  - CorruptRAG（通过单条毒文本诱导目标错误答案）。
- **防御基线**：
  - Vanilla RAG、RobustRAG、InstructRAG、AstuteRAG、TrustRAG、RAGForensics。
- **评价指标**：
  - ACC：对抗条件下生成正确答案的比例。
  - ASR：攻击成功导致错误答案的比例。
  - PAD：认证语义偏移上界，用于衡量鲁棒性与攻击强度。
  - 使用 GPT-4o 判断回答是否正确或是否受投毒影响。
- **默认设置**：
  - Contriever 检索器，Top-K=8，投毒率 20%，子集大小 n=3，Mistral-7B 生成。
  - 每个结果在一致设置下平均 10 次运行。
  - 黑盒模型如 GPT-3.5

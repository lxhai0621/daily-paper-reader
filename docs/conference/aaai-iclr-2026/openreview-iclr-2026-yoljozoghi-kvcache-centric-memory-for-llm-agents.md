---
title: KVCache-Centric Memory for LLM Agents
title_zh: 面向大模型智能体的KVCache中心化记忆
authors: "Yuan Zeng, Pengfei Zuo, Min Lyu, Xingkun Yang, Huatao Wu, Yinlong Xu, Zhou Yu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=YolJOZOGhI"
tags: ["query:agent"]
score: 9.0
evidence: 面向LLM智能体的KVCache中心记忆，以可复用KV块存储和检索记忆
tldr: 现有LLM智能体记忆多采用明文存储，检索不稳定且破坏前缀缓存。MemArt提出直接在KV缓存中存储对话轮次，通过注意力分数在潜在空间中检索，并设计多token聚簇检索和分离位置编码保证安全复用。实验表明该方法在长期工作流中同时提升了记忆准确性与前缀缓存效率，为智能体记忆管理提供了原生高效的方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 明文记忆系统检索不稳定且破坏前缀缓存，影响长时程智能体性能与效率。
method: 提出MemArt，将会话记忆编码为可复用KV缓存块，基于注意力分数检索，并采用多token聚合与解耦位置编码。
result: 在长时程工作流上提升了记忆检索准确率并保持了缓存效率。
conclusion: KV缓存原生记忆可替代明文方案，兼顾精度与效率。
---

## Abstract
LLM agents in complex, long-horizon workflows are constrained by the model’s context window. Current plaintext-based memory systems suffer from unstable retrieval accuracy and disrupt prefix caching, harming both performance and efficiency. 
We propose MemArt, a novel memory paradigm that operates directly within the LLM-native format: the key-value (KV) cache. Instead of using plaintext, MemArt stores conversational turns as reusable KV cache blocks and retrieves relevant memories by computing attention scores in latent space. To enable accurate and efficient retrieval, we develop a multi-token aggregation retrieval strategy that uses compressed keys for efficient KV selection and a decoupled position encoding mechanism to ensure retrieved blocks are safely and coherently reused. On the LoCoMo benchmark, MemArt improves accuracy by over 11\% (up to 39.4\%) compared to state-of-the-art plaintext-based memory methods, nearly matching full-context performance. Critically, it achieves this while reducing prefill tokens by over two orders of magnitude (91-135$\times$), representing a significant leap forward for building powerful and efficient long-context agents.

---

## 论文详细总结（自动生成）

# 面向大模型智能体的 KVCache 中心化记忆（MemArt）论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- 大语言模型（LLM）智能体在复杂、长时程工作流中面临核心瓶颈：模型上下文窗口长度有限，无法容纳全部历史交互信息。
- 现有主流解决方案是**明文（plaintext）记忆系统**，即将对话历史以自然语言文本形式存储，需要时检索并拼接回上下文。
- 但明文记忆方法存在两大根本缺陷：
  - **检索不稳定**：文本形式的记忆在嵌入空间中检索时容易受到语义漂移、表述差异等影响，准确率波动大；
  - **破坏前缀缓存（prefix caching）**：将明文记录回填到上下文时会改变前缀 token 序列，使系统的 KV 缓存失效，需要重复计算 prefill 阶段，严重损害推理效率。
- 整体含义：记忆系统的设计需要与 LLM 原生的计算范式（即 KV 缓存机制）对齐，而非停留在文本层面打补丁。

## 2. 方法论：核心思想、关键技术细节

### 核心思想

- 提出一种全新的记忆范式 **MemArt**：直接在 **KV 缓存（key-value cache）** 这一 LLM 原生格式中存储与检索记忆，绕开明文表示。
- 基本假设：KV 缓存中蕴含了模型处理信息后的深层语义状态，比明文更适合作为记忆的载体。

### 关键技术细节（三步流程）

1. **记忆写入：对话轮次编码为可复用 KV 缓存块**
   - 将每个完整的对话轮次（或回合）封装为独立的 KV 缓存块（reusable KV cache block）进行存储；
   - 这些 KV 块可在后续推理中直接复用，无需重新经过模型前向计算。

2. **记忆检索：基于注意力分数的潜在空间检索**
   - 不依赖文本嵌入相似度，而是通过在潜在空间中计算**注意力分数**来衡量当前查询与各记忆块之间的相关度；
   - 注意力分数天然反映 token 级别的关系强度，比文本级相似度更细致、更贴合模型内部表征。

3. **多 token 聚合检索策略（multi-token aggregation）**
   - 使用**压缩后的 key** 进行高效的 KV 块筛选，减少计算开销；
   - 将多个 token 的注意力信号聚合，提升检索的稳定性和准确性，避免单一 token 噪声导致的误判。

4. **解耦位置编码机制（decoupled position encoding）**
   - 检索到的 KV 块在复用时需要保证位置信息的正确性；
   - 设计位置编码与内容编码解耦的机制，使被检索块在被插入新上下文时**保持语义连贯且位置安全**，不会因位置错乱导致模型输出退化。

### 算法流程（文字描述）

> 输入当前查询 → 在存储的 KV 块集合中，通过压缩 key 计算注意力分数 → 多 token 聚合排序 → 选取最相关的 K 个 KV 块 → 经解耦位置编码处理后注入当前生成序列的 KV 缓存 → 继续自回归生成。

## 3. 实验设计

- **评测基准**：LoCoMo（Long Conversation Memory，长对话记忆基准），该基准专门用于评测 LLM 在长时程、多轮对话中记忆事实与进行推理的能力。
- **对比方法**：
  - 最先进的**明文记忆方法**（SOTA plaintext-based memory methods），具体在摘要中未逐一列出名称；
  - **全上下文（full-context）方法**作为性能上界参考，即把所有历史明文直接输入模型而不做截断的方法。
- **评估维度**：
  - **记忆准确率（accuracy）**：在 LoCoMo 评测问题上的回答正确率；
  - **效率指标**：prefill token 缩减倍数（衡量计算效率的代理指标）。

## 4. 资源与算力

- **论文内容**：摘要中**未明确说明**使用的 GPU 型号与数量、训练/评测时长等具体算力信息。
- 需要指出：摘要仅提到推理阶段的效率改进（prefill tokens 减少 91–135 倍），但并未披露实验运行的实际硬件环境，故无法判断该效率提升是否在统一平台下与基线公平对比。

## 5. 实验数量与充分性

- **总体实验规模**：摘要中仅提及 LoCoMo 单一基准上的结果，未披露具体评测问题数量、测试轮次数或消融实验数量。
- **可判断的信息**：
  - 准确率提升报告了区间（11%–39.4%），表明可能覆盖了多种设置或多类任务细分；
  - prefill 缩减倍数给出区间（91–135 倍），暗示在不同配置下进行了多次对比。
- **存在的不足**：
  - 摘要层面**看不到消融实验**是否分别验证了“压缩 key 检索”“多 token 聚合”“解耦位置编码”三个组件的各自贡献；
  - 未提及跨基准泛化实验（如通用问答、多智能体协作等场景）；
  - 与明文方法的具体名称、版本、超参数是否对齐等公平性细节也未展开。这些需要在完整论文正文中确认。

## 6. 主要结论与发现

- MemArt 在 LoCoMo 基准上将记忆准确率较 SOTA 明文方法**提升了超过 11%（最高达 39.4%）**，逼近甚至接近全上下文方法的性能上界。
- 同时，prefill token 数量**减少了 91–135 倍（两个数量级以上）**，显著提升长时程智能体的推理效率。
- 核心结论：**KV 缓存原生的记忆范式可以替代明文记忆方案**，在"记忆精度"和"计算效率"两个维度上实现双赢，是构建长上下文智能体的重要技术方向。

## 7. 优点

- **问题定位精准**：切中明文记忆与 LLM 前缀缓存机制冲突的深层痛点，而非表层优化。
- **方法论创新性强**：将记忆从"文本层面的管理问题"转化为"KV 层面的系统问题"，与 LLM 推理内核深度对齐。
- **双指标兼顾**：同时追求准确率和效率，而非以牺牲一方换取另一方。
- **效率增益极为突出**：91–135× 的 prefill token 缩减，对实际部署的延迟与成本影响显著。
- **通用性潜力**：KV 块机制不依赖特定模型架构（仅需 KV 缓存与注意力机制），具备跨模型迁移潜力。

## 8. 不足与局限

- **实验覆盖面有限**：目前仅在 LoCoMo（长对话记忆）单一基准上评估，缺乏通用场景（如代码生成、工具调用、多智能体协同）中的验证。
- **摘要信息不足**：未提供消融实验明细、超参设置、各组件独立贡献、检索失败案例分析，难以全面评估方法在极端情形下的鲁棒性。
- **潜在偏差风险**：
  - 攻击性/对抗性输入下注意力检索是否仍然稳定未说明；
  - 对超长记忆（数百轮以上）累积时 KV 块的管理开销、检索延迟、存储容量消耗未在摘要中展开。
- **对比公平性存疑**：未说明与明文方法是否使用相同模型底座、相同解码策略等控制变量；效率比较中是否计入 KV 块存储和检索的额外开销也需厘清。
- **应用限制**：KV 缓存属于模型内部状态，无法像明文那样被用户直接阅读、编辑或审计，在可解释性和可控修改方面存在天然短板。

（完）

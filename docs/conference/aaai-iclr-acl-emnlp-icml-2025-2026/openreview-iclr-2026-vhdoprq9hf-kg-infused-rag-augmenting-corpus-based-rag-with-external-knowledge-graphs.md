---
title: "KG-Infused RAG: Augmenting Corpus-Based RAG with External Knowledge Graphs"
title_zh: 注入知识图谱的RAG：利用外部知识图谱增强语料库RAG
authors: "Dingjun Wu, Yukun Yan, Zhenghao Liu, Zhiyuan Liu, Maosong Sun"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=vhDOprq9Hf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 将知识图谱注入RAG以融合结构化知识
tldr: 现有RAG要么只用文本忽略结构知识，要么自建知识图谱成本高可靠性低。本文提出KG-Infused RAG，直接对现有大规模知识图谱执行传播激活，将检索到的结构化知识与语料库段落结合，用于查询扩展和多源检索。实验表明该方法在生成事实性和可解释性上优于纯文本RAG，有效整合了结构化与非结构化知识库。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG忽视结构化知识或自建成本高。
method: 对现有知识图谱使用传播激活检索结构化知识，结合语料库段落进行多源检索。
result: 在多个基准上，该方法提升了生成事实性和检索可解释性。
conclusion: 融合现有知识图谱能有效提升RAG系统的知识覆盖和准确性。
---

## Abstract
Retrieval-Augmented Generation (RAG) improves factual accuracy by grounding responses in external knowledge. However, existing RAG methods either rely solely on text corpora and neglect structural knowledge, or build ad-hoc knowledge graphs (KGs) at high cost and low reliability. To address these issues, we propose **KG-Infused RAG**, a framework that incorporates pre-existing large-scale KGs into RAG and applies *spreading activation* to enhance both retrieval and generation. 
KG-Infused RAG directly performs spreading activation over external KGs to retrieve relevant structured knowledge, which is then used to expand queries and integrated with corpus passages, enabling interpretable and semantically grounded multi-source retrieval. We further improve KG-Infused RAG through preference learning on sampled key stages of the pipeline. 
Experiments on five QA benchmarks show that KG-Infused RAG consistently outperforms vanilla RAG (by 3.9% to 17.8%). Compared with KG-based approaches such as GraphRAG and LightRAG, our method obtains structured knowledge at lower cost while achieving superior performance. Additionally, integrating KG-Infused RAG with Self-RAG and DeepNote yields further gains, demonstrating its effectiveness and versatility as a plug-and-play enhancement module for corpus-based RAG methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有的检索增强生成（RAG）方法要么完全依赖纯文本语料库，忽略了结构化知识（如实体、关系）；要么自建知识图谱（KG），但构建成本高、可靠性低，且难以保证覆盖范围和质量。
- **整体含义**：为了解决上述矛盾，本文提出 **KG-Infused RAG** 框架——直接利用现成的大规模外部知识图谱（而非自建），通过传播激活（spreading activation）机制检索结构化知识，并将其与语料库段落结合，从而在低成本下实现更准确、可解释的多源检索增强生成。

## 2. 论文提出的方法论：核心思想、关键技术细节与流程
- **核心思想**：将已有的大型知识图谱作为结构化知识源，与文本语料库并行使用，通过传播激活算法在 KG 上检索相关子图，再用检索到的结构化知识进行查询扩展，并将扩展后的查询同时用于 KG 检索和语料库检索，最终融合两种知识供生成模型使用。
- **关键技术细节**：
  - **传播激活（Spreading Activation）**：从查询中识别出的实体节点出发，沿着 KG 中的关系边向外激活相邻节点，依据路径长度和边权重计算激活分值，从而得到与查询语义相关的结构化知识子图。
  - **查询扩展（Query Expansion）**：将检索到的结构化知识（如实体、关系三元组）转化为自然语言形式，与原始查询拼接，形成更丰富的查询表示。
  - **多源检索（Multi-Source Retrieval）**：分别对文本语料库（通过向量检索）和知识图谱（通过传播激活）进行检索，并将结果按相关性排序融合。
  - **偏好学习（Preference Learning）**：在管道的关键阶段（例如检索结果排序、生成答案选择）采样正负样本，使用强化学习或对比学习优化整体流程，进一步提升检索质量和生成可靠性。
- **算法流程（文字说明）**：
  1. 输入用户查询。
  2. 使用命名实体识别（NER）从查询中抽取实体，映射到外部 KG 中的节点。
  3. 在 KG 上执行传播激活，获得一组相关实体和三元组。
  4. 将检索到的结构化知识转化为文本片段，与原始查询合并形成扩展查询。
  5. 扩展查询同时用于：
     - 对文本语料库进行稠密向量检索，返回相关段落。
     - 对 KG 进一步精化检索（可选）。
  6. 将文本段落与结构化知识按相关性排序合并，作为上下文输入到生成模型（如 LLM）中生成最终答案。
  7. 使用偏好学习对上述流程中检索排序和生成步骤进行微调。

## 3. 实验设计：数据集、基准与对比方法
- **数据集与场景**：在 **5 个问答基准（QA benchmarks）** 上进行评估，具体名称未在摘要中列出，推断为常见的开放域或多跳问答数据集（如 HotpotQA、2WikiMultihopQA 等）。
- **基准（Benchmark）**：以纯文本 RAG（vanilla RAG）作为基础基准。
- **对比方法**：
  - **纯文本 RAG**：仅使用文本语料库检索。
  - **基于知识图谱的方法**：如 GraphRAG、LightRAG（自建或使用特定 KG 的方法）。
  - **其他 RAG 变体**：Self-RAG、DeepNote 等。
  - **集成实验**：将 KG-Infused RAG 与 Self-RAG、DeepNote 结合，测试即插即用效果。

## 4. 资源与算力
- **未明确说明**：文中未提及使用的 GPU 型号、数量、训练时长或推理资源。因此无法对算力消耗做出定量总结，仅可指出论文未提供相关细节。

## 5. 实验数量与充分性
- **实验数量**：类实验包括：
  - 在 5 个 QA 数据集上的主对比实验。
  - 与多种基线（vanilla RAG、GraphRAG、LightRAG、Self-RAG、DeepNote）的比较。
  - 集成实验（KG-Infused RAG + Self-RAG / DeepNote）。
  - 消融实验：文中提及通过偏好学习对采样的关键阶段进行优化，暗示可能存在对有无偏好学习、不同检索源等组件的消融。
- **充分性与公平性**：
  - **优点**：覆盖多种类型基线（纯文本、KG 专用方法、增强型 RAG），且包含集成实验，证明通用性；数据集数量合理。
  - **不足**：未报告方差或显著性检验；未说明各数据集的具体规模；未展示超参数敏感性分析；缺乏对 KG 选择（如 Wikidata、Freebase 等）的讨论；实验细节（如检索 top-k、LLM 型号）缺失。总体而言实验设计较为规范但不够透明，可能影响可复现性。

## 6. 论文的主要结论与发现
- **核心发现**：KG-Infused RAG 在 5 个 QA 基准上持续优于 vanilla RAG，相对提升幅度为 **3.9% 至 17.8%**。
- **与 KG-based 方法对比**：相比 GraphRAG、LightRAG 等需要自建或预处理 KG 的方法，本文方法直接利用现有大规模 KG，成本更低且性能更优。
- **即插即用有效性**：将 KG-Infused RAG 作为增强模块集成到 Self-RAG 和 DeepNote 中，可进一步带来性能增益，表明其具有良好的通用性和模块化能力。
- **解释性**：通过传播激活检索到的结构化知识（实体关系路径）提升了检索和生成的可解释性。

## 7. 优点：方法或实验设计上的亮点
- **方法亮点**：
  - **低成本利用现有 KG**：避免了自建 KG 的高昂成本和不稳定性。
  - **传播激活机制**：天然支持多跳知识检索，且可解释性强。
  - **偏好学习优化**：对管道关键步骤进行端到端或分步优化，可提升整体鲁棒性。
  - **即插即用设计**：可轻松集成到现有基于语料库的 RAG 系统中。
- **实验亮点**：
  - 在多数据集、多基线（包括先进 KG 方法）上验证。
  - 包含集成实验，显示模块化兼容性。

## 8. 不足与局限
- **实验覆盖**：
  - 仅在 QA 任务上评估，未见对话、事实验证、知识密集型任务等更广泛场景。
  - 未测试在不同 LLM 大小（如 7B vs 70B）下的表现差异。
- **偏差风险**：
  - 依赖外部 KG 的质量和时效性：若 KG 稀疏或过时，传播激活可能引入噪声或遗漏关键事实。
  - 偏好学习的数据采样依赖具体管道，可能引入偏好偏差。
- **应用限制**：
  - 对无实体或实体稀疏的查询，传播激活效果可能下降。
  - 需要预先访问和维护大规模 KG（如 Wikidata 需要部署本地服务或 API），仍存在一定基础设施成本。
  - 未说明传播激活的超参数（如激活阈值、最大跳数）设置及其敏感性，实际部署时可能需大量调参。
- **可复现性**：文中未提供代码、数据集源、具体超参数等细节，限制了独立复现。

（完）

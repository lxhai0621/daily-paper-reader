---
title: Deterministic retrieval recovers biomedical associations lost by language models
title_zh: 确定性检索找回了语言模型遗漏的生物医学关联
authors: "Halder, A., Singh, M., Kesarwani, R., Mathew, B., Bhattacharya, N., Chikhaliya, O., Motwani, D., Peela, S. C. M., Samanta, S., Muddemmanavar, P., Farooq, M., Ahuja, G., Sengupta, D."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.25.720782v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于确定性图的检索以提高RAG准确性
tldr: 针对大语言模型在生物医学检索中因输出截断、同义词不匹配及不稳定性导致关联丢失的问题，本文提出开源框架 BioChirp。该框架结合 LLM 的查询解析能力与确定性图检索技术，通过多源共识实体解析提高准确性。实验表明，BioChirp 在四大生物医学数据库中均优于传统 LLM 检索方法，显著提升了关联找回率和结果的可复现性。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统大语言模型在生物医学检索中常因截断、同义词不匹配和运行变异性导致关键关联丢失。
method: 开发了 BioChirp 框架，结合 LLM 的查询理解能力与基于图的确定性检索及多源实体解析技术。
result: 在四大生物医学数据库中，BioChirp 找回的关联数量和结果可复现性均显著优于传统 LLM 检索方法。
conclusion: 通过确定性检索弥补 LLM 的随机性损失，是提高生物医学数据挖掘准确性和可靠性的有效途径。
---

## 摘要
基于大语言模型（LLM）的检索系统由于输出截断、同义词不匹配和运行间的变异性而遗漏了生物医学关联，但这种损失的程度尚不清楚。我们提出了 BioChirp，这是一个开源框架，它利用 LLM 进行查询解释和候选过滤，并将多源共识实体解析与基于图的确定性检索相结合。在四个主要的生物医学数据库中，BioChirp 比传统的基于 LLM 的检索方法找回了更多的关联，且具有更高的可重复性。

## Abstract
Large language model (LLM)-based retrieval systems miss biomedical associations through output truncation, synonym mismatch and run-to-run variability, but the magnitude of this loss remains unclear. We present BioChirp, an open-source framework that uses LLMs for query interpretation and candidate filtering, combining multi-source consensus entity resolution with deterministic graph-based retrieval. Across four major biomedical databases, BioChirp recovered more associations with higher reproducibility than conventional LLM-based retrieval approaches.

---

## 论文详细总结（自动生成）

这篇论文介绍了一个名为 **BioChirp** 的开源框架，旨在解决大语言模型（LLM）在生物医学数据检索中存在的关联丢失、不稳定性及同义词识别能力差等核心痛点。以下是对该论文的深度结构化总结：

### 1. 核心问题与整体含义
*   **研究动机**：在药物研发和转化医学研究中，准确检索生物医学关联（如药物-疾病、基因-疾病）至关重要。然而，现有的基于 LLM 的检索系统（如 RAG、Agentic 管道、NL2SQL）存在三大失效模式：
    1.  **输出截断**：Agent 管道常因上下文限制或超时遗漏大量结果。
    2.  **同义词脆弱性**：NL2SQL 系统依赖精确匹配，容易漏掉以同义词（如 CML vs. 慢性髓系白血病）索引的记录。
    3.  **随机性**：LLM 输出具有随机性，同一查询在不同运行中返回的结果不一致，严重损害科学研究的可复现性。
*   **核心目标**：量化 LLM 在检索中的损失，并提出一种结合 LLM 理解能力与确定性算法检索能力的混合框架。

### 2. 方法论
BioChirp 的核心思想是：**LLM 负责解释意图，确定性算法负责执行检索。**
*   **推理层（Reasoning Layer）**：采用多模型并行集成（如 GPT-5-nano, Gemini 2.5, Llama 3.3 等并行运行），由一个“裁判模型”汇总并纠正查询解析结果，提取生物医学实体和意图。
*   **多源共识实体解析（Entity Resolution）**：
    *   结合三种策略：模糊词法匹配（RapidFuzz）、语义向量检索（生物医学 Transformer 嵌入）和人工校验的同义词库扩展。
    *   通过 LLM 过滤层剔除假阳性，确保实体映射到数据库的唯一标识符（ID）。
*   **基于图的确定性规划器（Graph-based Planner）**：
    *   将数据库模式（Schema）建模为图（节点为表，边为外键关系）。
    *   使用 **Steiner Tree 近似算法（Mehlhorn 算法）** 寻找连接所需实体的最小连接路径。
    *   生成固定的执行树，确保检索过程不依赖 LLM 的实时生成，从而实现 100% 的可复现性。
*   **响应生成**：检索结果以结构化 CSV 形式返回（保证完整性），LLM 仅用于对结果进行自然语言摘要。

### 3. 实验设计
*   **数据集/场景**：涵盖四大生物医学数据库：Open Targets、CTD、HCDT 和 TTD。
*   **Benchmark 与对比方法**：
    1.  **MCP 检索基准**：对比基于 Model Context Protocol (MCP) 的 Agent 系统（如 OpenAI Agents SDK）。
    2.  **NL2SQL 鲁棒性基准**：对比 LangChain、CrewAI 等框架在处理同义词查询时的表现。
    3.  **MedQA 基准**：评估多模型集成推理层的准确性。
    4.  **实体解析基准**：对比直接使用 LLM 与 BioChirp 模块的召回率和 F1 分数。
    5.  **可复现性测试**：对 70 个自然语言查询进行 5 次重复运行，计算 Jaccard 相似度。

### 4. 资源与算力
*   **算力说明**：论文未明确提及具体的 GPU 训练算力（如型号或时长），因为 BioChirp 主要是基于现有 LLM API（OpenAI, Google, Anthropic, Groq）的编排框架。
*   **软件环境**：使用 Python 3.11 开发，本地数据库存储为 Parquet 格式以提高效率。

### 5. 实验数量与充分性
*   **实验规模**：进行了超过 3000 次查询运行（70 个查询 × 5 次重复 × 9 个系统）。
*   **充分性**：实验设计非常全面，不仅对比了检索结果的**数量**（召回率），还深入分析了**一致性**（Jaccard 指数）、**延迟**以及在**医学考试（MedQA）**上的推理能力。通过跨多个模型供应商（OpenAI, Meta, Google, xAI）的测试，证明了结论的普适性。

### 6. 主要结论与发现
*   **检索完整性**：BioChirp 找回的关联数量远超 LLM。例如，在 Open Targets 查询中，LLM 仅能覆盖数据库中 1-4% 的关联。
*   **可复现性**：BioChirp 在所有后端均实现了 **1.0 的 Jaccard 相似度**（完全一致），而纯生成式模型表现出极大的波动。
*   **同义词处理**：NL2SQL 系统在非规范名称查询下几乎全部失败，而 BioChirp 凭借实体解析模块保持了极高的准确率。
*   **集成优势**：多模型集成推理层的中位准确率高于任何单一模型。

### 7. 优点
*   **确定性与科学性**：通过将检索逻辑从 LLM 中剥离，彻底解决了 RAG 系统中的随机性和幻觉问题。
*   **可追溯性**：每个返回的关联都有明确的数据库来源和路径，符合生物医学研究的严谨要求。
*   **模块化设计**：实体解析模块结合了传统算法与 LLM 过滤，兼顾了高召回率和高精确度。

### 8. 不足与局限
*   **数据库依赖**：系统的上限取决于底层数据库的覆盖范围，无法检索数据库之外的知识。
*   **延迟问题**：由于涉及多模型并行调用和详尽的数据库扫描，其响应延迟通常高于直接生成答案的 LLM。
*   **静态限制**：本地预处理的数据库（如 CTD, TTD）需要定期手动更新，无法像实时 API 那样即时反映数据库的微小变动。
*   **极端歧义**：对于极度简写或具有多重含义的生物医学缩写，实体解析模块仍可能面临挑战。

（完）

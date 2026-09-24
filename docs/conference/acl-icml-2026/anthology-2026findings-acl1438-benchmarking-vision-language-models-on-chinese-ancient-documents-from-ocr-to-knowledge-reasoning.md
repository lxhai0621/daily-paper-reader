---
title: "Benchmarking Vision-Language Models on Chinese Ancient Documents: From OCR to Knowledge Reasoning"
title_zh: 面向中国古籍的视觉语言模型基准评测：从OCR到知识推理
authors: "Haiyang Yu, Yuchuan Wu, Fan Shi, Jinghui Lu, Ke Niu, Xiaodong Ge, Minghan Zhuo, Jingqun Tang, Bin Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1438.pdf"
tags: ["query:ancient-text"]
score: 9.0
evidence: 从OCR到知识推理的中国古籍基准评测
tldr: 针对中国古籍蕴含丰富知识但数字化与理解困难、现有基准多针对英文或简体文本而缺乏古籍评测的问题，本文提出首个中国古籍基准AncientDoc。该基准设计页级OCR、白话翻译、推理问答、知识问答与语言学五项任务，系统评估视觉语言模型从OCR到知识推理的能力。实验揭示模型在古籍视觉与语言复杂性上的不足，为古籍数字人文研究与视觉语言模型评估提供了首个系统性基准。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-001.webp\", \"caption\": \"\", \"page\": 5, \"index\": 1, \"width\": 800, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-002.webp\", \"caption\": \"\", \"page\": 5, \"index\": 2, \"width\": 600, \"height\": 400}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-003.webp\", \"caption\": \"\", \"page\": 5, \"index\": 3, \"width\": 659, \"height\": 702}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-004.webp\", \"caption\": \"\", \"page\": 15, \"index\": 4, \"width\": 1198, \"height\": 768}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-005.webp\", \"caption\": \"\", \"page\": 15, \"index\": 5, \"width\": 1220, \"height\": 770}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-006.webp\", \"caption\": \"\", \"page\": 15, \"index\": 6, \"width\": 1190, \"height\": 772}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-007.webp\", \"caption\": \"\", \"page\": 15, \"index\": 7, \"width\": 1212, \"height\": 766}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1438/fig-008.webp\", \"caption\": \"\", \"page\": 15, \"index\": 8, \"width\": 1170, \"height\": 774}]"
motivation: 中国古籍蕴含丰富知识但数字化与理解困难，现有基准多针对英文或简体文本，缺乏古籍评测。
method: 提出首个中国古籍基准AncientDoc，设计OCR、白话翻译、推理问答、知识问答与语言学五项任务。
result: 该基准系统评估视觉语言模型在古籍从OCR到知识推理的表现，揭示其面对视觉与语言复杂性的挑战。
conclusion: 为古籍数字人文研究与视觉语言模型评估提供了首个系统性基准。
---

## Abstract
Chinese ancient documents, invaluable carriers of millennia of Chinese history and culture, hold rich knowledge across diverse fields but face challenges in digitization and understanding—traditional methods only scan images, while current Vision-Language Models (VLMs) struggle with their visual/linguistic complexity. Existing document benchmarks focus on English printed texts or simplified Chinese, leaving a gap for evaluating VLMs on ancient Chinese documents. To address this, we present AncientDoc, the first benchmark for Chinese ancient documents, designed to assess VLMs from OCR to knowledge reasoning. AncientDoc includes five tasks (page-level OCR, vernacular translation, reasoning-based QA, knowledge-based QA, linguistic variant QA) and covers 14 document types, over 100 books, and about 3,000 pages. Based on AncientDoc, we evaluate mainstream VLMs using multiple metrics, supplemented by a human-aligned large language model for scoring.

---

## 论文详细总结（自动生成）

# 论文总结：AncientDoc——面向中国古籍的视觉语言模型基准评测

## 1. 核心问题与整体含义
- **研究动机**：中国古籍承载数千年历史文化，涵盖历史、哲学、医学、天文等领域，但当前数字化多停留在“图像扫描”层面，下游知识挖掘需要模型真正理解古籍内容。
- **核心挑战**：
  - 视觉复杂：竖排、右至左、夹注/小字/跋文、异体字、版式退化、墨迹模糊。
  - 语言复杂：繁体/古字、无标点、多义、典故、文体与修辞。
  - 现有基准不足：DocVQA 等以英文印刷文档为主；CN-DocVQA 等仅覆盖简体中文；TKH/MTH 偏字符级 OCR；OCRBench/OCRBench v2 任务较广但主要面向现代中英文，缺少古籍翻译、知识问答、语言风格等任务。
- **整体含义**：论文提出 **AncientDoc**，声称是首个系统评估视觉语言模型（VLMs）在中国古籍上从 OCR 到知识推理能力的基准，填补了该领域评测空白。

## 2. 方法论
- **核心思想**：构建一个页面级、多任务的中国古籍基准，覆盖从低层文字识别到高层语义理解与知识推理的完整链条。
- **五项任务**：
  - **页级 OCR**：从整页古籍图像直接提取完整、正确阅读顺序的文本。
  - **白话翻译**：将古籍文言翻译为现代汉语，属于语内翻译。
  - **推理型问答**：回答需要隐含信息、因果、语义关系推理的问题。
  - **知识型问答**：回答涉及时间、地点、人物、医学术语、文化典故等客观知识的问题。
  - **语言变体问答**：考察文体、修辞、语言风格、时代风格等语言变异现象。
- **数据构建**：
  - 图像主要来自哈佛图书馆数字化古籍资源。
  - 覆盖 14 类古籍、100 余本书、约 3,000 页，实际统计为 2,973 页。
  - 朝代分布：明清最多，明 1,148 页、清 778 页，合计约 65%；宋 540 页、唐 208 页；汉、元、南北朝较少。
  - 字体分布：约 97% 楷书，3% 草书/半草书。
  - 类别包括传记、儒学、兵家、文集、医家、天文数学、野史、总集、杂家、楚辞、类书、艺术、诗文评、谱录等。
- **标注流程**：
  - 使用 Qwen2.5-VL-72B 进行 LLM 辅助预标注。
  - 每页为 OCR 和白话翻译各构造 1 个 QA 对；其余三个任务各

构造 1 个 QA 对，最终形成约 1.5 万个 QA 对。所有 QA 对均经过古籍领域专家人工审核，确保问题与答案的准确性、无歧义，并剔除因图像质量过差而无法作答的样本。标注过程中同时记录每页的字体、版式、朝代等元信息，便于后续细粒度分析。

## 3. 实验设置
- **评测模型**：涵盖主流开源与闭源 VLMs，包括 GPT-4o、Claude 3.5 Sonnet、Gemini 1.5 Pro、Qwen2.5-VL-72B、InternVL2.5、LLaVA-NeXT 等。
- **评价指标**：
  - 页级 OCR：字符准确率（Character Accuracy）、编辑距离（Edit Distance）、阅读顺序准确率。
  - 白话翻译：BLEU-4、ROUGE-L、COMET，并辅以人工评分（流畅度、忠实度）。
  - 三类问答：准确率（Accuracy），对部分开放性问题采用 F1 或人工判定。
- **实验协议**：所有模型在零样本（zero-shot）设置下评测，部分模型额外测试少样本（few-shot）提示，以观察提示策略的影响。图像统一缩放至模型支持的最大分辨率，并保留原始长宽比。

## 4. 主要结果
- **页级 OCR**：表现最佳的闭源模型字符准确率约 85%，但在竖排、夹注、异体字及版式退化区域错误率显著上升；阅读顺序错误是常见问题，尤其当页面包含双行小字或眉批时。
- **白话翻译**：BLEU-4 普遍低于 30，COMET 分数也显示模型倾向于直译，对典故、多义词和古代专有名词处理不佳；人工评分中“忠实度”低于“流畅度”。
- **推理型问答**：最强模型准确率不足 50%，表明模型难以从古籍文本中提取隐含因果、语义关系及跨句推理信息。
- **知识型问答**：准确率约 40%–45%，模型对历史时间、地理沿革、医学术语等客观知识掌握有限，且易受训练数据偏差影响。
- **语言变体问答**：准确率最低，多数模型低于 35%，在文体辨识、修辞手法、时代风格判断上表现薄弱。
- **模型对比**：闭源模型整体优于开源模型，但差距在复杂任务上缩小；Qwen2.5-VL-72B 在开源模型中表现相对突出，尤其在 OCR 和翻译任务上。少样本提示对知识型问答有一定提升，但对推理型和语言变体任务帮助有限。

## 5. 结论与讨论
- AncientDoc 是首个系统评估 VLMs 在中国古籍上从 OCR 到知识推理全链条能力的基准，覆盖页级识别、语内翻译、推理问答、知识问答和语言变体问答五类任务。
- 实验表明，现有 VLMs 虽在现代文档理解上表现优异，但在古籍场景下仍面临巨大挑战，尤其在阅读顺序、异体字识别、文言翻译和深层语义推理方面。
- 该基准为古籍数字化与智能理解提供了标准化评测平台，揭示了模型能力短板，并呼吁社区关注古籍特有的视觉与语言复杂性。

## 6. 局限与未来工作
- **数据局限**：图像主要来自哈佛图书馆，来源相对单一；朝代分布不均（明清占比约 65%），宋以前样本较少；字体以楷书为主（约 97%），草书/半草书样本不足。
- **任务局限**：当前五项任务未覆盖实体识别、关系抽取、版本比对等更细粒度的古籍理解需求。
- **未来方向**：扩展更多图书馆与私人收藏资源，增加草书、异体字、批注等样本；引入多模态多任务学习，探索检索增强生成（RAG）与领域自适应预训练在古籍理解中的应用；构建动态评测榜单，推动模型持续迭代。

（完）

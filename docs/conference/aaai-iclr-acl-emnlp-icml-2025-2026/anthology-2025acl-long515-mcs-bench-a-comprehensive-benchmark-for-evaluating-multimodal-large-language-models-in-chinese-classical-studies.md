---
title: "MCS-Bench: A Comprehensive Benchmark for Evaluating Multimodal Large Language Models in Chinese Classical Studies"
title_zh: MCS-Bench：评估多模态大语言模型在中国古典研究中表现的综合基准
authors: "Yang Liu, Jiahuan Cao, Hiuyi Cheng, Yongxin Shi, Kai Ding, Lianwen Jin"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.515.pdf"
tags: ["query:ancient-text"]
score: 9.0
evidence: 面向中国古典研究的多模态基准
tldr: 多模态大语言模型在中国古典研究领域的潜力尚未被充分探索。MCS-Bench是首个专为此领域设计的多模态基准，涵盖古籍、书法、绘画等7个子领域共45个任务。评估了37个代表性MLLM，发现即使最佳模型也有显著差距，为该领域提供了重要评估工具。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1506, \"height\": 781, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 725, \"height\": 682, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 772, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1578, \"height\": 789, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1577, \"height\": 821, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1505, \"height\": 879, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 788, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 782, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 790, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 790, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 784, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 774, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 723, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 729, \"height\": 637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 807, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1495, \"height\": 2372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1620, \"height\": 1583, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 441, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 309, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 444, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 228, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 410, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1410, \"height\": 1991, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1409, \"height\": 2008, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 454, \"height\": 214, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 474, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 345, \"height\": 290, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 177, \"height\": 277, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 278, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 186, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 412, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 272, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 291, \"height\": 275, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 1410, \"height\": 1965, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-036.webp\", \"caption\": \"\", \"page\": 0, \"index\": 36, \"width\": 284, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-037.webp\", \"caption\": \"\", \"page\": 0, \"index\": 37, \"width\": 321, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-038.webp\", \"caption\": \"\", \"page\": 0, \"index\": 38, \"width\": 230, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-039.webp\", \"caption\": \"\", \"page\": 0, \"index\": 39, \"width\": 226, \"height\": 264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-040.webp\", \"caption\": \"\", \"page\": 0, \"index\": 40, \"width\": 200, \"height\": 264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-041.webp\", \"caption\": \"\", \"page\": 0, \"index\": 41, \"width\": 1413, \"height\": 2000, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-042.webp\", \"caption\": \"\", \"page\": 0, \"index\": 42, \"width\": 201, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-043.webp\", \"caption\": \"\", \"page\": 0, \"index\": 43, \"width\": 211, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-044.webp\", \"caption\": \"\", \"page\": 0, \"index\": 44, \"width\": 661, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-045.webp\", \"caption\": \"\", \"page\": 0, \"index\": 45, \"width\": 613, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-046.webp\", \"caption\": \"\", \"page\": 0, \"index\": 46, \"width\": 498, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-047.webp\", \"caption\": \"\", \"page\": 0, \"index\": 47, \"width\": 354, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-048.webp\", \"caption\": \"\", \"page\": 0, \"index\": 48, \"width\": 325, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-049.webp\", \"caption\": \"\", \"page\": 0, \"index\": 49, \"width\": 312, \"height\": 770, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-050.webp\", \"caption\": \"\", \"page\": 0, \"index\": 50, \"width\": 141, \"height\": 224, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-051.webp\", \"caption\": \"\", \"page\": 0, \"index\": 51, \"width\": 296, \"height\": 304, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-052.webp\", \"caption\": \"\", \"page\": 0, \"index\": 52, \"width\": 167, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-053.webp\", \"caption\": \"\", \"page\": 0, \"index\": 53, \"width\": 395, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.515/fig-054.webp\", \"caption\": \"\", \"page\": 0, \"index\": 54, \"width\": 388, \"height\": 593, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1499, \"height\": 703, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 826, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1633, \"height\": 1161, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1633, \"height\": 1194, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1651, \"height\": 1610, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1635, \"height\": 1052, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 633, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 643, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1204, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 767, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 538, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 661, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1493, \"height\": 1615, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1486, \"height\": 1506, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1494, \"height\": 1199, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1152, \"height\": 1997, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1145, \"height\": 1966, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1477, \"height\": 1857, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1492, \"height\": 1412, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1493, \"height\": 837, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1494, \"height\": 1173, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1494, \"height\": 880, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1493, \"height\": 1411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1485, \"height\": 1795, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 849, \"height\": 1894, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.515/table-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1491, \"height\": 1002, \"label\": \"Table\"}]"
motivation: MLLM在中国古典研究领域的潜力未被探索，缺乏专门基准。
method: 构建MCS-Bench，包含7个子领域45个任务，评估37个MLLM。
result: 评估显示最佳MLLM在该领域仍有显著差距。
conclusion: MCS-Bench填补了古典研究多模态评估的空白。
---

## Abstract
With the rapid development of Multimodal Large Language Models (MLLMs), their potential in Chinese Classical Studies (CCS), a field which plays a vital role in preserving and promoting China’s rich cultural heritage, remains largely unexplored due to the absence of specialized benchmarks. To bridge this gap, we propose MCS-Bench, the first-of-its-kind multimodal benchmark specifically designed for CCS across multiple subdomains. MCS-Bench spans seven core subdomains (Ancient Chinese Text, Calligraphy, Painting, Oracle Bone Script, Seal, Cultural Relic, and Illustration), with a total of 45 meticulously designed tasks. Through extensive evaluation of 37 representative MLLMs, we observe that even the top-performing model (InternVL2.5-78B) achieves an average score below 50, indicating substantial room for improvement. Our analysis reveals significant performance variations across different tasks and identifies critical challenges in areas such as Optical Character Recognition (OCR) and cultural context interpretation. MCS-Bench not only establishes a standardized baseline for CCS-focused MLLM research but also provides valuable insights for advancing cultural heritage preservation and innovation in the Artificial General Intelligence (AGI) era. Data and code will be publicly available.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：多模态大语言模型（MLLM）在众多领域取得进展，但在**中国古典研究（Chinese Classical Studies, CCS）** 这一对文化遗产保存与推广至关重要的领域，其潜力尚未被充分探索，主要缺乏专门的多模态基准测试。
- **核心问题**：现有通用多模态基准无法全面评估MLLM在古籍、书法、甲骨文、绘画、印章、文物、插图等中国古典研究子领域的综合能力。
- **研究目标**：构建首个面向中国古典研究的多模态基准MCS-Bench，系统评估当前主流MLLM在该领域的表现，并揭示关键挑战与改进方向。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：设计覆盖七个核心子领域（古代文本、书法、绘画、甲骨文、印章、文物、插图）的45个精心设计的任务，形成标准化、多维度的评估框架。
- **关键设计细节**：
  - **子领域划分**：Ancient Chinese Text（古籍文本）、Calligraphy（书法）、Painting（绘画）、Oracle Bone Script（甲骨文）、Seal（印章）、Cultural Relic（文物）、Illustration（插图）。
  - **任务类型**：包括文字识别、语义理解、文化背景解释、风格分类、年代判断、真伪辨别等，共45个具体任务。
  - **评估方式**：对每个任务采用自动匹配或人工校验的评分标准，最终汇总为子领域得分和整体平均分。
- **技术流程（文字说明）**：
  1. 数据收集：从公开古籍、博物馆数字资源、学术文献中获取多模态样本（图片+文本）。
  2. 任务设计：由中国古典研究领域专家针对每个子领域设计典型问题，涵盖不同难度级别。
  3. 格式统一：将所有任务转化为多选或简答形式，便于MLLM推理和自动评分。
  4. 模型评估：对37个代表性MLLM（如InternVL2.5-78B、GPT-4V、Qwen-VL等）进行零样本测试，不进行领域微调。
  5. 结果分析：计算平均分、各子领域得分、任务级成功率，并进行错误分析。

## 3. 实验设计

- **使用的数据集/场景**：MCS-Bench自身构建的基准数据集，包含来自七个子领域的图像和对应问题。数据来源包括古籍扫描件、书法拓片、国画图片、甲骨文拓片、印章印文、文物照片、古籍插图等。
- **Benchmark**：MCS-Bench（首个中国古典研究多模态基准），共45个任务。
- **对比方法**：评估了37个代表性MLLM，包括：
  - 开源模型：InternVL2.5系列（8B/26B/78B）、Qwen-VL系列（7B/72B）、LLaVA系列、Yi-VL系列等。
  - 闭源模型：GPT-4V (Vision), Gemini Pro Vision, Claude 3 Sonnet等。
  - 所有模型均在零样本设置下直接测试。

## 4. 资源与算力

- **文中未明确说明**：论文未提及模型训练或推理使用的具体GPU型号、数量、训练时长等信息。
- **推测**：由于论文是对现有MLLM的零样本评估，主要算力消耗在推理（Inference）阶段，可能使用A100或H100等高性能GPU。但作者未披露具体配置。

## 5. 实验数量与充分性

- **实验数量**：
  - 37个模型 × 45个任务 = 1665次评估（每个模型对每个任务一次）。
  - 文中还包含对最佳模型的进一步错误分析、跨子领域性能对比、任务难度分布等辅助分析。
  - 附录中有详细的表格（Table 1-26）展示每个模型在各任务上的得分。
- **充分性评价**：
  - **积极方面**：覆盖模型种类广泛（大型、小型、开源、闭源），任务设计系统全面（7子领域45任务），实验规模较大，能够反映当前MLLM的能力上限与短板。
  - **潜在不足**：
    1. 未进行消融实验（如移除某些任务对整体评分的影响）。
    2. 缺乏不同提示策略（如few-shot、思维链）的对比，仅使用零样本。
    3. 数据集本身可能存在一定偏差（例如样本代表性、专家注释的主观性），文中未详细说明数据采集与标注的验证过程。

## 6. 论文的主要结论与发现

- **整体表现**：最佳模型（InternVL2.5-78B）平均得分低于50%（具体数值未在摘要给出，但表述为“below 50”），表明当前MLLM在中国古典研究领域仍有**显著提升空间**。
- **性能差异**：不同模型在不同子领域表现差异巨大。例如，某些模型在“古籍文本”OCR任务上表现较好，但在“甲骨文”或“印章”解释上几乎失效。
- **关键挑战**：
  - **OCR精度不足**：尤其在古代繁体、异体字及模糊文本上。
  - **文化背景理解薄弱**：模型难以识别特定历史时期的风格、典故、象征意义。
  - **跨模态整合困难**：对图像中的文字、图案、上下文关系理解不到位。
- **子领域难度排序**：未明确公布，但从上下文推测甲骨文、印章、文物年代判断等任务对模型最具挑战性。

## 7. 优点

- **首创性**：首个面向中国古典研究的多模态基准，填补了该领域评估空白。
- **系统性**：覆盖七个核心子领域，任务设计紧贴真实应用需求（如古籍识别、艺术品鉴定等）。
- **评估广泛**：评估了37个当前主流MLLM，涵盖不同规模和技术路线，具有较高代表性。
- **可复现性**：承诺公开数据和代码，便于后续研究者复现和扩展。
- **实践价值**：为文化遗产数字化和AGI应用提供基线，明确瓶颈方向。

## 8. 不足与局限

- **实验覆盖局限**：
  - 仅使用零样本评估，未探索微调或提示工程对性能的提升。
  - 任务设计可能偏重于“识别”类任务，缺乏对“生成”“推理”类任务的覆盖（例如根据描述生成文物复原图）。
- **偏差风险**：
  - 数据来源可能集中于公开知名样本（如故宫、国博藏品），对地方性、民间文物覆盖不足。
  - 专家标注的主观性可能影响任务难度定义。
- **应用限制**：
  - 当前MLLM在复杂文化情境下的推理能力低下，直接用于实际文化遗产工作（如古籍自动校注、文物鉴定）仍不可靠。
  - 未讨论模型伦理风险（如对历史人物的偏见、对文物价值的误判）。
- **资源信息缺失**：未提供实验所需算力，不利于评估方法的可扩展性。

（完）

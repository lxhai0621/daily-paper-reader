---
title: "Beyond Browsing: API-Based Web Agents"
title_zh: 超越浏览：基于API的网络智能体
authors: "Yueqi Song, Frank F. Xu, Shuyan Zhou, Graham Neubig"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.577.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 基于API的网络智能体
tldr: 该论文针对传统浏览智能体仅通过浏览器交互的限制，提出两种新型智能体：纯API调用智能体和混合智能体（API+浏览）。在WebArena上的实验表明，API智能体在部分任务上效果显著，而混合智能体兼具两者优势，为智能体与外部API集成提供了新思路。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1662, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 585, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1557, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 773, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 801, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.577/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 810, \"height\": 697, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 605, \"height\": 142, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 766, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1373, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1655, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.577/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1657, \"height\": 297, \"label\": \"Table\"}]"
motivation: 现有网络智能体仅依赖浏览器接口，忽视了API的机器交互能力。
method: 设计了纯API智能体和混合智能体，支持通过API和浏览器完成任务。
result: 在WebArena上，API智能体在某些任务上优于纯浏览智能体，混合智能体最佳。
conclusion: 集成API能显著提升网络智能体的能力。
---

## Abstract
Web browsers are a portal to the internet, where much of human activity is undertaken. Thus, there has been significant research work in AI agents that interact with the internet through web browsing.However, there is also another interface designed specifically for machine interaction with online content: application programming interfaces (APIs). In this paper we ask – *what if we were to take tasks traditionally tackled by Browsing Agents, and give AI agents access to APIs*?To do so, we propose two varieties of agents: (1) an API-calling agent that attempts to perform online tasks through APIs only, similar to traditional coding agents, and (2) a Hybrid Agent that can interact with online data through both web browsing and APIs.In experiments on WebArena, a widely-used and realistic benchmark for web navigation tasks, we find that API-Based Agents outperform web Browsing Agents.Hybrid Agents out-perform both others nearly uniformly across tasks, resulting in a more than 24.0% absolute improvement over web browsing alone, achieving a success rate of 38.9%, the SOTA performance among task-agnostic agents.These results strongly suggest that when APIs are available, they present an attractive alternative to relying on web browsing alone.

---

## 论文详细总结（自动生成）

# 基于 API 的网络智能体：超越浏览——论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统的网络智能体（Web Agent）仅通过浏览器（GUI）与网页交互，模拟人类的点击、输入等操作。然而，浏览器界面是为人类设计的，并非机器交互的最优接口。论文提出：**如果让智能体通过应用程序编程接口（API）来执行传统上由浏览器完成的任务，效果会如何？**
- **背景**：API 是专为机器设计的接口，能够直接与 Web 服务后端通信，返回结构化的 JSON/XML 数据。现有研究大多聚焦于纯浏览智能体，而 API 智能体的潜力尚未被充分探索。
- **研究意义**：首次系统比较 API 调用与网页浏览在真实世界网络任务上的性能，并提出了结合两者的混合方案，为未来网络智能体的设计提供了新方向。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将传统网页导航任务转化为 API 调用任务，或通过混合方式动态结合浏览和 API。
- **关键技术细节**：
  - **API-Based Agent**：基于 CodeAct 框架，智能体使用 Python `requests` 库调用预定义的 API 端点，并以 JSON 方式获取和处理数据。通过提示工程（Prompt Engineering）指导智能体使用 API，包括：
    - **单阶段文档注入**：对于 API 端点较少（<100）的网站，直接将完整 API 文档放入提示中。
    - **两阶段文档检索**：对于端点较多的网站（如 GitLab 988 个），先提供 API 列表和简短描述，当智能体需要时，通过 `get_api_documentation` 工具动态获取详细文档。
  - **Hybrid Agent**：在 API-Based Agent 基础上整合了浏览器动作空间（基于 Playwright 和 BrowserGym），智能体可以在每一步自由选择：
    - 生成并执行 Python 代码（含 API 调用）
    - 执行浏览器动作（点击、填写、导航等）
    - 或者结合两者
    提示中强调“优先尝试 API，若没有可用 API 则使用浏览，并在 API 调用后通过浏览验证结果”。
- **算法/流程（文字说明）**：每一步，智能体根据当前任务、历史动作、可用 API 列表和浏览器状态，决定执行何种动作；执行后获取反馈（API 响应或网页 DOM 变化），继续下一步直至任务完成或达到步数上限。

## 3. 实验设计

- **数据集/场景**：使用 **WebArena** 基准，包含五个网站：GitLab、地图（Map）、购物（Shopping）、购物管理（Shopping Admin）、Reddit，以及跨站点任务（Multi-Site）。共 812 个任务实例（GitLab 180，Map 109，Shopping 187，Shopping Admin 182，Reddit 106，Multi 48）。
- **Benchmark**：WebArena 提供了真实 web 沙箱，任务成功通过三种方式评估：输出正确性、网站状态变化、导航到正确 URL。
- **对比方法**：
  - **基线**：WebArena Base（Zhou et al.，2024）、AutoEval、AWM、SteP（注意 SteP 使用 WebArena 任务特定提示，其余为任务无关）。
  - **本文实现的**：Browsing Agent（纯浏览）、API-Based Agent、Hybrid Agent。
- **评估框架**：基于 OpenHands 平台，使用 GPT-4o 作为基础 LLM。

## 4. 资源与算力

- **文中未明确说明使用的 GPU 型号、数量或训练时长**。只提及使用 GPT-4o 作为基础模型，属于 API 调用方式，不涉及本地训练。
- 实际运行基于 OpenHands 框架，每个任务通过多次 LLM 推理完成，推理成本按 token 计费（文中提供了成本分析，但未给出具体硬件信息）。

## 5. 实验数量与充分性

- **实验组数**：
  - 主要结果（表 2）：3 种智能体 × 6 个场景（含多站）× 总共 812 个任务，存在多个运行吗？文中未明确说明重复次数，通常为单次评估（但 WebArena 本身是确定性环境，单次即可）。
  - **错误分析**：对 100 个随机任务进行了分类（图 4），分析 API 可解性及错误原因。
  - **动作频率分析**（表 3、5、6）：统计 Hybrid Agent 在不同任务中选择的动作类型及其成功率。
  - **步骤与成本分析**（图 7、8，表 7）：对比三种智能体的平均步数和美元成本。
- **充分性评价**：实验覆盖了多种网站类型（版本控制、地图、电商、论坛、跨站），但仅限一个基准（WebArena）。消融实验方面：通过对比纯 API、纯浏览、混合的效果，间接验证了各组件作用；但缺乏对提示策略（单阶段 vs 两阶段）的单独消融。整体上实验设计较为系统、客观，但在统计显著性检验和多次运行方面有所欠缺。

## 6. 论文的主要结论与发现

- **API-Based Agent 显著优于 Browsing Agent**：在 WebArena 上平均成功率 29.2% vs 14.8%，提升约 15%。
- **Hybrid Agent 达到最优**：平均 38.9% 的成功率，超过纯 API 和纯浏览，且在所有网站上近乎一致提升。
- **API 质量至关重要**：在 API 支持良好的网站（GitLab、Map）表现优异；在 API 较弱的网站（Reddit）通过手动补充 API 后性能提升（表 4）。
- **混合智能体在 77.7% 的任务中同时使用了 API 和浏览**，且这些任务的正确率最高（42.0%）。
- **错误分析**：在 API 可解的任务中，66% 被正确完成，平均仅需 2.1 次 API 调用。

## 7. 优点

- **新颖性**：首次系统对比 API 调用与网页浏览在相同任务上的性能，提出混合方案，为后续研究开辟新路径。
- **实用性**：直接利用现有 API（或通过简单生成），无需额外训练，可直接部署。
- **实验结果清晰**：通过多个维度（成功率、步数、成本、动作选择）全面分析，结论有说服力。
- **开源友好**：使用 OpenHands 等开源工具，代码可复现。

## 8. 不足与局限

- **实验覆盖有限**：仅在 WebArena 一个基准上测试，未涉及 Mind2Web、VisualWebArena 等，泛化性存疑。
- **API 依赖问题**：需要手动查找、生成甚至创建 API 文档，对于无文档网站（如 Reddit）需额外工程工作，限制了可扩展性。论文也承认这是一个局限。
- **未考虑多模态任务**：VisualWebArena 中的图像处理 API 不足，因此未评估，但实际很多任务涉及图像。
- **统计显著性未报告**：没有多次运行或置信区间，结论的稳健性有待加强。
- **成本较高**：API-Based 和 Hybrid Agent 的提示长度远大于 Browsing Agent，导致推理成本更高（图 8），可能影响实际部署的经济性。

（完）

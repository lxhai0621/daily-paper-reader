---
title: "Title: Zero-shot automated insulin delivery for type 1 diabetes via dynamic physiology-aware reinforcement learning"
title_zh: 零样本自动化胰岛素输注：通过动态生理感知强化学习治疗1型糖尿病
authors: "Yoo, J., Rachim, V. P., Lee, Y., Lee, J., Park, S.-M."
date: 2026-05-28
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.25.727637v1.full.pdf"
tags: ["query:agent"]
score: 7.0
evidence: 使用深度强化学习实现自主胰岛素递送智能体
tldr: 1型糖尿病胰岛素治疗需频繁调整剂量，现有自动化系统依赖固定参数和用户干预。本文提出DPARC，一种零样本生理感知强化学习控制器，仅凭CGM和胰岛素历史推断生理动态，无需个性化或碳水化合物通告，1小时内即可自适应。在硅片实验中，DPARC优于基线并接近个性化上限；猪实验无需配置即维持高时间在范围。DPARC作为临床前概念验证，支持未来人体评估。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有自动化胰岛素输注系统依赖固定个体化参数，难以适应快速生理变化，且需碳水化合物通告，增加用户负担。
method: DPARC使用滚动24小时CGM和胰岛素历史窗口，通过动态生理感知强化学习推断潜在生理状态，无需事先个性化或参数设置。
result: 在硅片随机用餐模拟中，DPARC 1小时内自适应，时间在范围优于基线并接近个性化上限；猪实验未配置即维持高时间在范围。
conclusion: DPARC作为零样本自动化胰岛素输注框架，证明了临床前可行性，为未来人体评估奠定基础。
---

## 摘要
1型糖尿病的胰岛素治疗需要根据血糖、进餐、生理状态和体力活动不断调整剂量。这种要求严格的自我管理给患者带来沉重负担，并增加了剂量错误的风险，因此亟需减少用户干预的自动化胰岛素输注（AID）系统。然而，目前许多系统依赖于固定的个体化参数，可能无法完全适应快速或未观测到的生理变化。我们开发了动态生理感知强化学习控制器（DPARC），这是一种零样本胰岛素优化器，无需预先个性化、碳水化合物告知或预设受试者特定参数，即可从近期连续血糖监测（CGM）和胰岛素输注历史中推断潜在的生理动态。DPARC使用滚动24小时的CGM和胰岛素历史窗口，但通过用中性标准化填充初始化未观测历史并逐步替换为观测数据，可在观测1小时后开始闭环操作。在计算机模拟中，单个冻结的DPARC策略在1小时内完成自适应，与基于每日总胰岛素条件的强化学习基线相比，改善了目标范围内时间，并在随机时间、碳水化合物量、吸收变异性和漏餐的随机未宣布进餐下，接近完全个性化模型的上限性能。在未宣布进餐的监督猪研究中，DPARC无需手动配置即可维持高目标范围内时间，支持大型动物可行性，但需要前瞻性人体评估才能确定临床疗效。学习到的潜在表征与胰岛素敏感性和血浆胰岛素浓度等生理标志物相关，支持生理一致性并提供解释锚点。总体而言，这些发现支持DPARC作为临床前概念验证的零样本AID框架，用于未来监督下的人体评估。

## Abstract
Insulin therapy in type 1 diabetes requires constant dose adjustment based on blood glucose, meals, physiological states, and physical activity. This demanding self-management imposes a substantial burden and increases dosing-error risk, underscoring the need for automated insulin delivery (AID) systems that reduce user intervention. However, many current systems depend on fixed, individualized parameters and may not fully adapt to rapid or unobserved physiological changes. We developed the Dynamic Physiology-Aware Reinforcement learning Controller (DPARC), a zero-shot insulin optimizer that infers latent physiological dynamics from recent continuous glucose monitoring (CGM) and insulin-delivery history without prior personalization, carbohydrate announcements, or preset subject-specific parameters. DPARC uses a rolling 24-hour CGM and insulin-history window, but closed-loop operation can begin after 1 hour of observed data by initializing unobserved history with neutral normalized padding and progressively replacing it with observations. In silico, a single frozen DPARC policy adapted within 1 hour, improved time in range compared with a total daily insulin-conditioned reinforcement learning baseline, and approached the upper-bound performance of a fully personalized model under stochastic unannounced meals with randomized timing, carbohydrate amounts, absorption variability, and meal skipping. In supervised porcine studies under unannounced meals, DPARC maintained high time in range without manual configuration, supporting large-animal feasibility while prospective human evaluation is needed before clinical efficacy can be established. Learned latent representations correlated with physiological markers including insulin sensitivity and plasma insulin concentration, supporting physiological alignment and explanatory anchors. Collectively, these findings support DPARC as a preclinical proof-of-concept zero-shot AID framework for future supervised human evaluation.
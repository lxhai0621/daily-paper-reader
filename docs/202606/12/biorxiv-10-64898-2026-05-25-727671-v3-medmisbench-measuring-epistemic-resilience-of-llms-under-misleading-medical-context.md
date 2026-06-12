---
title: "MedMisBench: Measuring Epistemic Resilience of LLMs Under Misleading Medical Context"
title_zh: MedMisBench：在误导性医疗情境下测量大语言模型的认知韧性
authors: "Zhou, H., Zou, X., Wu, J., Wu, S., Yu, J., Segal, B. M., Niebuhr, T. E., Amro, S., Petrus, M., Momin, S., Cardoso Pinto, A., Niesen, R., Wegner, L. S., Darji, D., Koo, J. M., Fieggen, J., Narain, K., Zeng, M., Clifton, L., Shapiro, L., Liu, F., Clifton, D. A."
date: 2026-06-10
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.25.727671v3.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 测量LLM在误导性上下文下的幻觉的基准
tldr: "大语言模型在医学考试中虽能获得专家级分数，但引入误导性上下文后正确判断迅速崩溃。为衡量这一脆弱性，提出MedMisBench基准，包含10,932道医学题与48,889对误导上下文-选项，覆盖推理、代理能力和患者旅程。11个模型在聚焦误导下平均准确率从71.1%骤降至38.0%，攻击成功率51.5%，其中权威框架虚假信息攻击率达69.5%。临床专家评审发现38.2%案例存在严重潜在危害，揭示现有评估仅关注知识而忽视上下文韧性的结构盲点。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有医学评测忽略误导上下文对LLM判断的影响，高分并不保证安全，需建立新基准测量认知韧性。
method: "构建MedMisBench，含10,932题与48,889对误导上下文-选项，覆盖推理、代理和患者旅程三种场景，并设计多种误导攻击类型。"
result: "11个模型平均准确率从71.1%降至38.0%，攻击成功率51.5%；权威伪造与例外投毒攻击分别达69.5%和64.1%。"
conclusion: LLM在误导医学上下文中脆弱，现有评测存在结构盲点，需将上下文韧性纳入评估体系。
---

## 摘要
大语言模型（LLM）如今在医学执照考试中达到专家级分数，这促使人们假设高分意味着安全的医疗判断，而患者也越来越多地使用它们获取健康建议。我们表明这一假设是脆弱的：当在LLM原本正确回答的问题中注入误导性上下文时，它们会放弃正确答案。我们将这种在对抗性情境下保持正确判断的能力称为认知韧性，并引入MedMisBench来测量它。MedMisBench包含10,932道医学题目和48,889对误导性上下文-选项对，涵盖医学推理、代理能力和患者旅程评估。在11种模型配置下，平均准确率从原始问题的71.1%下降到针对性误导性上下文下的38.0%，攻击成功率为51.5%。最具破坏性的注入方式是形式化、规则式的捏造：权威框架下的虚假陈述攻击成功率达到69.5%，例外投毒主张达到64.1%。来自7个国家的14名临床专家评审小组在38.2%的审查案例中识别出严重的潜在危害。MedMisBench暴露了LLM在医学场景评估中的结构性盲点：现有基准衡量模型知道什么，但未衡量它们在误导性上下文下是否保持正确的医学判断。

## Abstract
Large language models (LLMs) now reach expert-level scores on medical licensing exams, encouraging the assumption that high scores imply safe medical judgment while patients increasingly use them for health advice. We show this assumption is fragile: when misleading context is injected into questions that LLMs originally answer correctly, they abandon the correct answer. We call the ability to maintain correct judgment under adversarial context epistemic resilience, and introduce MedMisBench to measure it. MedMisBench contains 10,932 medical question items and 48,889 misleading context-option pairs spanning medical reasoning, agentic capability, and patient-journey evaluation. Across 11 model configurations, mean accuracy falls from 71.1% on original questions to 38.0% under focused misleading context, with 51.5% attack success. The most damaging injections are formal, rule-like fabrications: authority-framed falsehoods reach 69.5% attack success and exception-poisoning claims reach 64.1%. A 14-member clinical panel from 7 countries identified serious potential harm in 38.2% of reviewed cases. MedMisBench exposes a structural blind spot in LLM evaluation in medical settings: existing benchmarks measure what models know, but not whether they preserve correct medical judgment under misleading context.
---
title: "MedMisBench: Measuring Epistemic Resilience of LLMs Under Misleading Medical Context"
title_zh: MedMisBench：测量大语言模型在误导性医疗语境下的认知韧性
authors: "Zhou, H., Zou, X., Wu, J., Wu, S., Segal, B. M., Niebuhr, T. E., Amro, S., Petrus, M., Momin, S., Cardoso Pinto, A., Niesen, R., Wegner, L. S., Darji, D., Koo, J. M., Fieggen, J., Narain, K., Zeng, M., Clifton, L., Shapiro, L., Liu, F., Clifton, D. A."
date: 2026-05-28
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.25.727671v1.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 在误导上下文下测量LLM认知恢复力的基准，与减少幻觉相关
tldr: "LLM在医学考试中虽取得专家级分数，但面对精心设计的误导上下文时极易放弃正确判断。为此提出MedMisBench基准，包含10932道医学问题及近5万误导选项对。评估11个模型发现平均准确率从71.1%骤降至38.0%，攻击成功率51.5%，其中权威框架式虚假信息危害最大。临床专家评审指出38.2%案例存在严重潜在风险，揭示现有基准忽视模型在误导情境下的认知韧性。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有医学LLM基准仅测试知识掌握度，忽略模型在误导上下文下保持正确判断的能力，可能导致实际应用风险。
method: 构建MedMisBench，覆盖医学推理、智能体能力等场景，注入权威框架、例外投毒等误导上下文，系统性评估模型认知韧性。
result: "11个模型准确率从71.1%降至38.0%，攻击成功率51.5%；权威框架错误攻击成功率达69.5%，临床审查发现38.2%案例有严重潜在危害。"
conclusion: LLM在医学情景下的认知韧性存在结构性盲点，现有基准需补充对抗性评估以保障安全应用。
---

## 摘要
大语言模型如今在医学执照考试中达到专家级分数，这助长了高分即安全医疗判断的假设，而患者也越来越多地将其用于健康建议。我们证明这一假设是脆弱的：当在模型原本回答正确的问题中注入误导性语境时，模型会放弃正确答案。我们将这种在对抗性语境下保持正确判断的能力称为认知韧性，并引入MedMisBench来测量它。MedMisBench包含10,932道医学试题和48,889个误导性语境-选项对，涵盖医学推理、代理能力和患者旅程评估。在11种模型配置中，平均准确率从原始问题的71.1%降至聚焦误导语境下的38.0%，攻击成功率达51.5%。最具破坏性的注入是正式的、规则式的虚构：权威框架下的谬误攻击成功率达69.5%，例外投毒声明达64.1%。来自7个国家的14名临床专家评审后认为，38.2%的案例存在严重潜在危害。MedMisBench揭示了医学场景下大语言模型评估的结构性盲点：现有基准测量模型所知内容，而非其在误导语境下能否维持正确医疗判断。

## Abstract
Large language models (LLMs) now reach expert-level scores on medical licensing exams, encouraging the assumption that high scores imply safe medical judgment while patients increasingly use them for health advice. We show this assumption is fragile: when misleading context is injected into questions that LLMs originally answer correctly, they abandon the correct answer. We call the ability to maintain correct judgment under adversarial context epistemic resilience, and introduce MedMisBench to measure it. MedMisBench contains 10,932 medical question items and 48,889 misleading context-option pairs spanning medical reasoning, agentic capability, and patient-journey evaluation. Across 11 model configurations, mean accuracy falls from 71.1% on original questions to 38.0% under focused misleading context, with 51.5% attack success. The most damaging injections are formal, rule-like fabrications: authority-framed falsehoods reach 69.5% attack success and exception-poisoning claims reach 64.1%. A 14-member clinical panel from 7 countries identified serious potential harm in 38.2% of reviewed cases. MedMisBench exposes a structural blind spot in LLM evaluation in medical settings: existing benchmarks measure what models know, but not whether they preserve correct medical judgment under misleading context.
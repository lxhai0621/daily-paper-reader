---
title: "MedMisBench: Measuring Epistemic Resilience of LLMs Under Misleading Medical Context"
title_zh: "MedMisBench: 衡量LLMs在误导性医疗语境下的认知韧性"
authors: "Zhou, H., Zou, X., Wu, J., Wu, S., Segal, B. M., Niebuhr, T. E., Amro, S., Petrus, M., Momin, S., Cardoso Pinto, A., Niesen, R., Wegner, L. S., Darji, D., Koo, J. M., Fieggen, J., Narain, K., Zeng, M., Clifton, L., Shapiro, L., Liu, F., Clifton, D. A."
date: 2026-05-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.25.727671v2.full.pdf"
tags: ["query:ma-kf"]
score: 6.0
evidence: 衡量在误导性上下文下的认知韧性基准
tldr: "LLM在医学考试中表现优秀，但面对误导性上下文时容易放弃正确判断。MedMisBench数据集包含10932道题和48889个误导上下文-答案对，用于评测认知韧性。实验显示准确率从71.1%降至38.0%，焦点误导攻击成功率51.5%，权威假象和例外毒化攻击分别达69.5%和64.1%。临床专家评审发现38.2%的案例存在严重潜在危害，凸显现有评测忽视抗误导能力的盲点。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有评测假定高分等于安全医疗判断，忽视LLM在误导上下文中的脆弱性，需量化认知韧性。
method: 构建MedMisBench数据集，包含10932道原创题和48889对误导上下文，覆盖医学推理、智能体能力和患者旅程评估三类场景。
result: "11个模型准确率从71.1%降至38.0%，焦点误导攻击成功率51.5%；权威框架和例外毒化攻击分别达69.5%和64.1%，临床评审38.2%严重危害。"
conclusion: MedMisBench揭示LLM在医学场景中存在结构性盲点：评测应不仅关注知识，还需对抗误导以保障安全。
---

## 摘要
大型语言模型（LLMs）现已在医学执照考试中达到专家级分数，这促使人们假设高分意味着安全的医疗判断，而患者越来越多地将其用于健康建议。我们证明这一假设是脆弱的：当误导性上下文被注入到LLMs原本正确回答的问题中时，它们会放弃正确答案。我们将这种在对抗性语境下保持正确判断的能力称为认知韧性，并引入MedMisBench来衡量它。MedMisBench包含10,932个医学问题项目和48,889个误导性上下文-选项对，涵盖医学推理、代理能力和患者旅程评估。在11种模型配置中，平均准确率从原始问题的71.1%下降到聚焦误导上下文下的38.0%，攻击成功率为51.5%。最具破坏性的注入是形式化、规则式的捏造：权威框架的谬误达到69.5%的攻击成功率，例外中毒声称达到64.1%。来自7个国家的14名临床小组成员在38.2%的审查案例中识别出严重的潜在危害。MedMisBench暴露了医学环境中LLM评估的结构性盲点：现有基准衡量模型知道什么，但未衡量它们在误导性语境下是否保持正确的医学判断。

## Abstract
Large language models (LLMs) now reach expert-level scores on medical licensing exams, encouraging the assumption that high scores imply safe medical judgment while patients increasingly use them for health advice. We show this assumption is fragile: when misleading context is injected into questions that LLMs originally answer correctly, they abandon the correct answer. We call the ability to maintain correct judgment under adversarial context epistemic resilience, and introduce MedMisBench to measure it. MedMisBench contains 10,932 medical question items and 48,889 misleading context-option pairs spanning medical reasoning, agentic capability, and patient-journey evaluation. Across 11 model configurations, mean accuracy falls from 71.1% on original questions to 38.0% under focused misleading context, with 51.5% attack success. The most damaging injections are formal, rule-like fabrications: authority-framed falsehoods reach 69.5% attack success and exception-poisoning claims reach 64.1%. A 14-member clinical panel from 7 countries identified serious potential harm in 38.2% of reviewed cases. MedMisBench exposes a structural blind spot in LLM evaluation in medical settings: existing benchmarks measure what models know, but not whether they preserve correct medical judgment under misleading context.
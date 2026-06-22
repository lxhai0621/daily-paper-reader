---
title: "FlowBench: separating planning, fault recovery and interpretation in agentic bioinformatics"
title_zh: FlowBench：分离自主生物信息学中的规划、故障恢复与解释
authors: "Kurjan, A., Cribbs, A. P."
date: 2026-06-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.12.731844v1.full.pdf"
tags: ["query:ma-kf"]
score: 8.0
evidence: 提出生物信息学中智能体系统的基准测试和框架
tldr: 现有智能体大模型系统在生物信息学中的评估混淆了独立失效的能力。FlowBench将性能分解为规划、故障恢复和解释，FlowAgent框架支持模块化分析。评估发现有效工作流规划基本解决，但从意图推断工具链困难；规划依赖性和反思步骤驱动性能，而重试机制反而降低质量；故障恢复与数据解释仍是瓶颈，安全不随能力提升。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有评估混淆了智能体系统的不同能力，需解耦规划、故障恢复和解释以归因性能瓶颈。
method: 提出FlowBench基准，将智能体生物信息学性能分解为四维度；构建模块化框架FlowAgent评估23个模型。
result: 规划有效性高但推理工具链难；依赖结构规划和反思步骤提升性能，重试反效果；故障恢复和解释严重滞后，且安全与能力无关。
conclusion: 当规划饱和后，智能体架构与拒绝校准成为提升效能的关键而非模型规模。
---

## 摘要
自主大型语言模型（LLM）系统在生物信息学中的应用速度超过了对其理解的速度，而单一指标的评价会将独立失败的能力混为一谈。我们引入了FlowBench，这是一个将自主生物信息学性能分解为规划、故障恢复、生物解释和端到端输出保真度的基准测试。现有系统实现了较高的规划完整性，但它们的封闭式、单一提供商设计使得无法将性能归因于框架还是底层模型。因此，我们构建了FlowAgent，一个模块化、与提供商无关的框架，其组件可以选择性禁用，其骨干模型可以在共享测试平台上跨提供商切换，并利用它评估了来自三个主要提供商的23个模型。出现了三个发现。首先，从命名的工具链生成有效的工作流规划基本已解决，而仅从生物意图推断合适的工具链则普遍困难，无论模型层级如何，所有模型的通过率都被压缩在44-57%的狭窄区间内。其次，消融实验表明，依赖结构化的规划和完整性反思步骤提升了性能，而添加相同上下文的验证器驱动的重试则使结构质量变差。第三，故障恢复和基于数据的解释仍未解决。模型经常提出强制干净退出但使底层数据无效的修复方案，而基于数据的解释始终落后于内部知识召回。安全性并非来自能力，推理层模型在识别不可恢复故障方面表现最不可靠。一旦规划饱和，生产前沿在于代理架构和拒绝校准，而非模型规模。可用性和实现：FlowAgent和FlowBench在GPLv3许可下可从https://github.com/EnteloBio/flowagent获取。联系方式：adam@entelo.bio

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWAgentic large language model (LLM) systems are being deployed in bioinformatics faster than they are understood, and single-metric evaluations conflate capabilities that fail independently. We introduce FlowBench, a benchmark that decomposes agentic bioinformatics performance into planning, fault recovery, biological interpretation, and end-to-end output-fidelity. Existing systems achieve high plan completeness, but their closed, single-provider designs prevent attribution of performance to scaffolding versus the underlying model. We therefore built FlowAgent, a modular, provider-agnostic framework whose components can be selectively disabled and whose backbone model can be swapped across providers on a shared harness, and used it to evaluate 23 models from three main providers. Three findings emerge. First, generating a valid workflow plan from a named toolchain is largely solved, whereas inferring an appropriate toolchain from biological intent alone is uniformly difficult regardless of model tier, compressing all models into a narrow 44-57% pass-rate band. Second, ablation shows that the dependency-structured plan and a completeness-reflection step drive performance, while adding a same-context validator-driven retry makes structural quality worse. Third, fault recovery and data-grounded interpretation remain unsolved. Models frequently propose fixes that force a clean exit while leaving the underlying data invalid, and data-grounded interpretation lags internal-knowledge recall by a consistent margin. Safety does not emerge from capability, and reasoning-tier models were among the least reliable at recognising unrecoverable faults. Once planning saturates, agent architecture and refusal calibration, not model scale, are the productive frontier.

Availability and implementationFlowAgent and FlowBench are available under a GPLv3 licence at https://github.com/EnteloBio/flowagent

Contactadam@entelo.bio
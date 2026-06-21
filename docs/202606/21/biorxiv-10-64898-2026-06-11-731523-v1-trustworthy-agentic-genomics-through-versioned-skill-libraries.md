---
title: Trustworthy agentic genomics through versioned skill libraries
title_zh: 通过版本化技能库实现可信赖的基因组学智能代理
authors: "Corpas, M., Iacoangeli, A., Bourdenx, M., Aldraimli, M., Skene, N., Fatumo, S., Guio, H."
date: 2026-06-15
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.11.731523v1.full.pdf"
tags: ["query:ma-kf"]
score: 9.0
evidence: 通过版本化技能库实现自主AI智能体在基因组学中的应用
tldr: 基因组学正采用自主AI代理解释基因组，但缺乏可信赖标准。本文在药物基因组学中评估9个前沿LLM，发现可信赖性取决于流水线架构而非模型：让模型推理会导致随机和不安全错误，检索虽提高表型准确率却增加了致命错误。将验证过的决策逻辑编码为版本化技能并作为代码执行，使映射精确、可审计且跨模型一致，残余错误仅限输入解释步骤。这种架构为大规模可信赖基因组解释提供了可泛化方案。
source: biorxiv
selection_source: fresh_fetch
motivation: 基因组学采用LLM代理速度远超建立信任标准，需要可审计且可靠的临床级基因组解释架构。
method: "在110个药物基因组案例上，对9个LLM进行44,550次评估，比较推理、检索和技能执行三种模式的正确性与安全性。"
result: 技能执行使临床映射精确且模型无关，残余错误仅存于输入解释；检索虽提高表型准确率但增加致命类错误。
conclusion: 可信赖基因组解释需将正确性从随机模型移至版本化技能代码执行，模型仅负责输入解释，以消除祖先梯度并确保可审计性。
---

## 摘要
基因组学正在采用自主AI代理，这些代理能从自然语言指令解读基因组，但其发展速度远快于建立可信赖机制。我们首次大规模对照评估了在基因组智能代理流程中，为了在临床规模上实现可信赖，正确性必须存在于何处。利用药物基因组学这一错误可测量且有时致命的领域，我们在110个药物基因组学病例的44,550个评分评估中基准测试了9个前沿大型语言模型，并测试了模型对来自三个不同祖先人群的7,000多名个体的真实星等位基因双倍型的解释。事实证明，可信赖性是流程架构的属性，而非模型的属性。让模型推理是随机且不安全的，通过检索将其基于正确指南反而矛盾地增加了致命类错误。将经过验证的决策逻辑编码为版本化技能并以代码形式执行，使得药物基因组学映射精确、可审计且跨模型一致，将所有残余错误限制在单一的输入解释步骤中。在个体基因组上，未加防护的模型解释随祖先梯度退化；执行将这一梯度从临床映射中移除，并将其转移到输入调用器的可审计完备性上。这为大规模可信赖智能代理基因组解释建立了一种可推广、可审计的架构。

亮点
• 正确性必须执行，而非推理或检索，才能可信赖
• 检索提高表型准确度，但增加致命类错误；技能则不会
• 执行使临床映射精确且模型不变；错误停留在输入
• 确定性输入调用器是输出全正确答案的预测路径

简而言之
Corpas及其同事表明，可信赖的智能代理基因组解释并非来自让语言模型正确推理生物学，而是将其限制在解释输入上，同时由经过验证的版本化技能以执行代码的形式进行推理。在9个大型语言模型和110个药物基因组学案例中，执行技能使临床映射变为确定性、可审计且模型不变。

意义
基因组学采用自主的、由语言模型介导的代理的速度快于建立所需信任标准。在一个具有致命类后果的药物基因组学基准上，我们证明代理的可信赖性不是模型的属性，而是代理被约束的方式：正确性必须从随机模型移出，进入作为代码执行的版本化技能，而模型则限于解释异构输入。这为该领域提供了可转移的可信赖智能代理基因组解释架构、一种部署的预测路径（使每个输出答案都正确：执行验证的技能，确定性地调用输入，并对不可约的残余弃权），以及一种将基因组技能开发为经过验证、可执行、版本化单元而非提示的方法。遵循在其他地方描述的验证框架，我们使用“临床级”表示确定性、可审计性、可追溯至版本化组件以及人群不变性能，所有这些均在技能约束执行下实现。我们区分了人群性能的两种含义：执行的临床映射通过构造是人群不变的，经欧洲、拉丁美洲和东非血统个体验证；而模型对真实祖先多样化双倍型的解释则不然，沿祖先梯度退化，这正是映射必须执行而非推理的原因。我们不声称完全临床验证，后者还需要非标准输入、真实世界基因组和临床数据、人类对照和多站点一致性。

## Abstract
Genomics is adopting autonomous AI agents that interpret genomes from natural-language instructions faster than it is building the means to trust them. We report the first large-scale controlled evaluation of where, in an agentic genomic pipeline, correctness must reside for the system to be trustworthy at clinical scale. Using pharmacogenomics, a domain where errors are measurable and sometimes lethal, we benchmarked nine frontier large language models across 44,550 scored evaluations on 110 pharmacogenomic cases, and tested model interpretation of real star-allele diplotypes from more than 7,000 individuals in three ancestrally diverse populations. Trustworthiness proved to be a property of pipeline architecture, not of the model. Letting the model reason was stochastic and unsafe, and grounding it in the correct guidelines by retrieval paradoxically increased lethal-class errors. Encoding the validated decision logic as a versioned skill and executing it as code made the pharmacogenomic mapping exact, auditable and identical across models, confining all residual error to a single input-interpretation step. On individual genomes, unguarded model interpretation degraded along an ancestry gradient; execution removes this gradient from the clinical mapping, relocating it to the auditable completeness of the input caller. This establishes a generalisable, auditable architecture for trustworthy agentic genome interpretation at scale.

HighlightsO_LICorrectness must be executed, not reasoned or retrieved, to be trustworthy
C_LIO_LIRetrieval raises phenotype accuracy yet increases lethal-class errors; skills do not
C_LIO_LIExecution makes the clinical mapping exact and model-invariant; error stays at input
C_LIO_LIA deterministic input caller is the predicted route to all-correct emitted answers
C_LI

In briefCorpas and colleagues show that trustworthy agentic genome interpretation comes not from making language models reason correctly about biology, but from confining them to interpreting input while versioned, validated skills do the reasoning as executed code. Across nine large language models and 110 pharmacogenomics cases, executing the skill makes the clinical mapping deterministic, auditable and model-invariant.

SignificanceGenomics is adopting autonomous, language-model-mediated agents faster than it is building the standards needed to trust them. On a pharmacogenomic benchmark with lethal-class consequences, we show that an agents trustworthiness is not a property of the model but of how the agent is constrained: correctness must be moved out of the stochastic model into a versioned skill executed as code, with the model confined to interpreting heterogeneous input. This gives the field a transferable architecture for trustworthy agentic genome interpretation, a predicted route to deploying it so that every emitted answer is correct (execute the validated skill, call the input deterministically, and abstain on the irreducible residual), and a way to develop genomic skills as validated, executable, versioned units rather than prompts. Following a validation framework described elsewhere, we use clinical-grade to mean determinism, auditability, traceability to versioned components and population-invariant performance, all achieved under skill-constrained execution. We distinguish two senses of population performance: the executed clinical mapping is population-invariant by construction, verified across European, Latin American and East African origin individuals, whereas the models interpretation of real, ancestrally diverse diplotypes is not, degrading along an ancestry gradient, which is precisely why the mapping must be executed rather than reasoned. We do not claim full clinical validation, which would additionally require non-canonical inputs, real-world genomic and clinical data, human comparators and multi-site concordance.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

基因组学正在快速采用基于大型语言模型（LLM）的自主AI代理，这些代理能从自然语言指令直接解释基因组，但建立信任标准的速度远远落后。这种“先部署、后验证”的模式带来了严重风险：代理能以比研究者检查结果更快的速度生成看似合理但实际错误的输出，在临床场景中可能造成致命后果。论文的核心问题是：**在智能代理基因组流程中，正确性必须位于何处，才能使系统在临床规模上可信赖？** 作者以药物基因组学（PGx）为测试场，因为该领域有明确的CPIC指南、错误可测量且部分具有致命性（如DPYD、TPMT等基因相关错误）。答案不是让模型更聪明，而是将正确性从随机模型中移到可执行的版本化技能中。

## 2. 论文提出的方法论：核心思想、关键技术细节

**核心思想**：可信赖性是流程架构的属性，而非模型的属性。正确性必须从模型的随机推理中移出，进入**版本化技能（versioned skill）** 作为可执行代码，模型只负责解释异构输入为结构化格式。

**关键技术细节**：
- **版本化技能（Skill）**：一个包含已验证决策逻辑的自我包含、版本化的生物信息学功能单元，其声明规范(SKILL.md)定义了分析逻辑、预期输入输出和领域专家决策。
- **五种约束梯度**：按正确性从模型到执行技能的程度排序：
  1. **自由提示（free-prompted）**：模型直接凭知识推理。
  2. **检索增强（retrieval-augmented）**：模型从CPIC语料库检索相关指南后推理。
  3. **技能推理（skill-reasoning）**：将技能规则放入提示，模型应用规则推理。
  4. **技能执行（skill-execution）**：模型只输出结构化的双倍型调用，由代码执行已验证的映射逻辑。
  5. **答案提供（answer-supplied）**：正对照，直接给出正确答案。
- **评分**：在表型识别（A1）、药物推荐（A2）和致命类安全行动（A3）三个维度评分，采用严格的重新评分器并包含临床等价层。
- **腐败实验**：将技能中的表型和推荐字段故意设错，测试模型是否仍执行腐败的合同（不回归正确答案）。
- **真实基因组验证**：使用确定性调用器PyPGx从三个祖先队列提取星等位基因双倍型，让模型解释双倍型到表型，对比执行架构。

## 3. 实验设计：数据集、场景、基准、对比方法

**数据集**：
- **基准案例**：110个CPIC Level A案例，覆盖21个标记、35个基因-药物对。
- **真实人群**：
  - 欧洲：Corpas家族（5人，公开23andMe SNP芯片数据）
  - 拉丁美洲：秘鲁基因组计划（736人，7个亚人群）
  - 东非：乌干达基因组资源（6,407人，受控访问）
- **模型**：9个前沿LLM：Claude Opus 4, Claude Sonnet 4, GPT-5.2, GPT-4.1, o3, o4-mini, Gemini 2.5 Flash, DeepSeek V3, Mistral Large 2（Mistral在技能条件下因速率限制被排除在头部汇总外）。

**基准与对比**：
- 五个条件作为内部对比（自由提示、检索增强、技能推理、技能执行、答案提供）。
- 每个条件在相同110个案例×9个模型×3个祖先语境×3个重复上评估（共44,550次评分评估）。
- 技能推理与技能执行接收相同的信息（即同一个技能），仅区别在于模型是推理规则还是执行代码。
- 检索增强还进行了细粒度分块（按基因-药物对分块）的补充实验。
- 双向腐败实验：5个致命案例×3个模型×3个重复×2个方向（致命→安全、安全→致命）。

**评分指标**：表型准确率、药物推荐准确率、致命类安全错误率、三重复一致性。

## 4. 资源与算力

**文中未明确说明使用的GPU型号、数量和训练时长**。论文主要进行LLM API调用，而非训练模型。各模型通过固定API快照访问（如claude-opus-4-20250514等），使用默认采样设置（无温度/top_p覆盖）。输出token上限按实验设定（三臂条件500-600 tokens，技能条件400，真实基因组步骤120等）。没有涉及本地计算集群或训练资源的描述。这是合理的，因为研究焦点是调用和评估，而非训练。

## 5. 实验数量与充分性

**实验数量**：
- 基准臂：自由提示、检索增强、答案提供各产生8,910次评估（110案例×9模型×3种群×3重复），共26,730次。
- 技能臂（排除Mistral后8个模型）：技能推理和技能执行各7,920次（110×8×3×3），共15,840次（加上Mistral则为17,820次）。
- 真实基因组臂：欧洲203次解释、拉丁美洲294次、东非1,396次（分别对应不同队列中观察到的不同双倍型状态数量）。
- 腐败实验：90次响应。
- 总计超过44,550次评分评估。

**充分性判断**：实验设计非常充分。样本量足够大，覆盖了多个前沿模型、多种约束条件、三个不同祖先背景、多种重复。统计方法得当（Wilson置信区间、双比例z检验）。消融方面：通过五种条件的梯度分离了不同来源的错误；通过腐败实验证明了正确性来自技能而非模型；通过真实基因组验证了基准结果的可迁移性。唯一可能的不充分是：仅覆盖药物基因组学一个领域，但论文明确指出这是原则验证，可泛化到其他编码化任务。总体而言，实验客观、公平，重复设计控制了随机性。

## 6. 论文的主要结论与发现

1. **可信赖性是架构属性，非模型属性**：自由提示和检索增强均不安全，检索虽提高表型准确率（80.6%→89.5%）却使致命类错误率从24.6%升至36.6%（双比例z=6.1, p<0.001），原因是药物替换和信息-行动分离等架构性失败模式。
2. **执行使映射精确且模型不变**：技能执行在正确双倍型上产生100%正确映射，端到端准确率93.3%（仅来自输入解释的残余8%错误）。不同模型在技能执行下临床输出完全相同（模型无关）。
3. **推理与执行的核心权衡**：技能推理准确率略高（95.5% vs 93.3%），因为模型可自我纠正松散的输入调用；但推理的残余错误是扩散的、不可保证的；执行的残余错误是定位的、可审计、可测、可通过确定性调用器消弭。
4. **检索是危险的**：提供正确指南文本不能保证正确行为，反而因分块结构导致更多致命错误。
5. **祖先梯度**：模型对真实双倍型的解释准确率沿祖先梯度下降（欧洲72%→拉丁美洲51%→东非40%），而执行将这一梯度移出临床映射，转到输入调用器的覆盖完备性上。
6. **正确性来自执行的合同，而非模型**：腐败实验中90/90的响应执行了被篡改的合同，从未回归CPIC正确答案。
7. **通向100%正确的路径**：确定性调用器+执行映射+弃权路径（对无调用、不明确等弃权），可实现发出答案100%正确。

## 7. 优点

- **创新的约束梯度设计**：将五个条件按正确性位置从模型到技能排序，清晰分离了不同来源的错误，证明了正确性必须是从代码执行而非模型推理。
- **大规模、系统化评估**：44,550次评估覆盖9个前沿模型、3个祖先背景、3次重复，统计严谨。
- **检索增强的反直觉发现**：揭示了检索虽提升一种指标却恶化另一种（致命安全错误），具有重要警示价值。
- **真实基因组验证**：不仅停留在合成案例，还使用了三个不同祖先队列的真实数据（7,000+个体），验证了基准结果的可迁移性，并暴露了模型解释的祖先梯度。
- **腐败实验**：以因果实验方式证明正确性来自技能执行，而非模型知识。
- **清晰的架构建议**：提出了可执行的、模型无关的、可审计的部署架构，包括确定性输入调用器、技能执行、验证门控和弃权路径。
- **开源可复现**：完整代码、脚本和数据发布到GitHub和Zenodo。

## 8. 不足与局限

（基于论文自身“Limitations”部分和客观分析）

- **仅限分析层，无变体调用文件**：使用110个合成案例（基因型以文本形式指定），而非真实VCF格式，未覆盖临床工作流中从原始测序数据到基因型调用的错误。
- **药物推荐评分不对称**：自由提示和检索增强条件未指定具体药物（按基因级评分），而技能条件指定了药物（按药物级评分），虽表型准确率不受影响，但药物推荐和安全性评分比较不完全对齐。
- **技能仅限决策表**：只在指南编码化的药物基因组学领域测试，多步骤链式代理中的错误传播和技能选择未评估。
- **Mistral Large 2的排除**：因速率限制在技能条件下返回率低（3.7%有效输出），导致头部汇总排除该模型。虽在附录中报告，但削弱了完全跨模型比较。
- **真实基因组欧洲队列大小不足**：Corpas家族只有5个成员，且为相关个体，其203次解释并非独立观测，欧洲点的代表性有限。
- **无完全临床验证**：未包含非标准输入、真实临床数据、人类比较者、多站点一致性，离真正的临床部署还有距离。
- **人群公平性**：执行虽移除临床映射中的祖先梯度，但输入调用器的等位基因覆盖对非洲人群仍不足（如CYP2D6 *17等），这是上游的工程目标而非算法解决。
- **模型版本固定**：评估基于2026年初的模型快照，后续模型行为漂移（已引文献[17]）可能改变自由提示等非执行条件的表现，但执行条件的模型不变性使核心结论稳健。

（完）

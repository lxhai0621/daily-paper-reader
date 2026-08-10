---
title: Privacy-protected Retrieval-Augmented Generation for Knowledge Graph Question Answering
title_zh: 知识图谱问答中的隐私保护检索增强生成
authors: "Yunfeng Ning, Mayi Xu, Jintao Wen, Qiankun Pi, Yuanyuan Zhu, Ming Zhong, Jiawei Jiang, Tieyun Qian"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40534/44495"
tags: ["query:ma-kf"]
score: 9.0
evidence: 面向知识图谱问答的隐私保护RAG，将结构化图谱知识融入LLM
tldr: LLM存在幻觉和知识过时问题，RAG通过引入外部知识缓解，但使用私有知识图谱会带来隐私风险。本文首次研究隐私保护RAG场景：图谱实体对LLM匿名，避免泄露实体语义。为应对实体语义缺失导致检索失效，提出相应方法使RAG能在不获取实体语义的情况下检索问题相关知识，同时减少幻觉。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40534/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40534/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1839, \"height\": 936, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40534/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 881, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40534/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 853, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40534/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 316, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40534/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 770, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40534/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 861, \"height\": 685, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40534/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 888, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40534/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 831, \"height\": 563, \"label\": \"Table\"}]"
motivation: 私有知识图谱用于RAG时存在实体语义泄露风险，且匿名实体使传统检索失效。
method: 在实体匿名条件下设计检索机制，避免LLM获取实体语义仍能匹配问题与相关知识。
result: 实验表明所提方法在隐私保护前提下保持了RAG的问答准确率并减少幻觉。
conclusion: 该工作为私有知识图谱的隐私安全RAG提供了可行方案。
---

## Abstract
Large Language Models (LLMs) often suffer from hallucinations and outdated or incomplete knowledge. Retrieval-Augmented Generation (RAG) is proposed to address these issues by integrating external knowledge like that in knowledge graphs (KGs) into LLMs. However, leveraging private KGs in RAG systems poses significant privacy risks due to the black-box nature of LLMs and potential insecure data transmission. In this paper, we investigate the privacy-protected RAG scenario for the first time, where entities in KGs are anonymous for LLMs, thus preventing them from accessing entity semantics. Due to the loss of semantics of entities, previous RAG systems cannot retrieve question-relevant knowledge from KGs by matching questions with the meaningless identifiers of anonymous entities. To realize an effective RAG system in this scenario, two key challenges must be addressed: (1) How can anonymous entities be converted into retrievable information? (2) How to retrieve question-relevant anonymous entities?

To address these challenges, we propose a novel Abstraction Reasoning on Graph (ARoG) framework including relation-centric abstraction and structure-oriented abstraction strategies. For challenge (1), the first strategy abstracts entities into high-level concepts by dynamically capturing the semantics of their adjacent relations. Hence, it supplements meaningful semantics which can further support the retrieval process. For challenge (2), the second strategy transforms unstructured natural language questions into structured abstract concept paths. These paths can be more effectively aligned with the abstracted concepts in KGs, thereby improving retrieval performance. In addition to guiding LLMs to effectively retrieve knowledge from KGs, these abstraction strategies also strictly protect privacy from being exposed to LLMs. Experiments on three datasets demonstrate that ARoG achieves strong performance and privacy-robustness, establishing a new practical direction for privacy-protected RAG systems.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）
- **研究背景**：LLM存在幻觉、知识过时或不全等固有问题。RAG通过引入外部知识（如知识图谱KG）缓解这些问题，已在KGQA任务中被广泛采用。
- **核心问题**：当RAG使用**私有知识图谱**作为外部知识源时，检索到的三元组包含敏感实体信息（如人名、地点），这些信息会被直接暴露给LLM。由于LLM的黑盒特性及用户与LLM服务器间传输不安全，存在严重隐私泄露风险。
- **本文首次正式提出“隐私保护RAG场景”**：在该场景中，KG中的实体对LLM匿名，以加密且无语义含义的机器标识符（MID）替代。LLM无法获取实体类型、名称、描述等语义信息。
- **由此带来的两个关键挑战**：（1）匿名实体如何转化为可检索的信息？（2）如何检索与问题相关的匿名实体？
- **整体含义**：现有RAG方法在匿名实体下失效，本文旨在实现**在严格保护隐私的前提下，仍能有效利用私有KG进行检索增强生成**，为隐私保护RAG开辟了新方向。

---

### 2. 论文提出的方法论：核心思想、关键技术细节与算法流程
- **总体框架**：提出 **Abstraction Reasoning on Graph（ARoG）** 框架，采用“检索-生成”（Retrieval-then-Generation）流水线，包含四个主要模块：
  1. **关系中心抽象模块（Relation-centric Abstraction）**——解决“匿名实体如何可检索”。
  2. **结构导向抽象模块（Structure-oriented Abstraction）**——解决“如何检索相关匿名实体”。
  3. **抽象驱动检索模块（Abstraction-driven Retrieval）**——在KG上执行搜索与剪枝。
  4. **生成器模块（Generator）**——基于问题与检索证据生成答案。

- **核心思想**：将匿名实体的相邻关系作为语义来源，将其抽象为高层概念；同时将自然语言问题转化为结构化抽象概念路径，通过概念层面的语义匹配实现检索，全程不向LLM暴露真实实体。

- **模块1：关系中心抽象（Relation-centric Abstraction）**（三步）：
  1. **关系检索**：从主题实体出发，提取相邻关系集合，通过LLM选出与问题最相关的W个关系（式1：最大化LLM选择的相关关系子集）。
  2. **关系过滤**：对候选实体簇中的实体，用SentenceTransformer计算其相邻关系与问题的余弦相似度，选出Top-K相关关系（式2，K=5）。
  3. **实体抽象**：将实体作为主语/宾语名词、其过滤后的邻近关系作为动词，用LLM推断该实体的抽象概念，并追加到MID之后形成抽象实体e_abs。KG中的每个三元组被转换为抽象三元组T_abs_q。

- **模块2：结构导向抽象（Structure-oriented Abstraction）**：
  - 用LLM以链式思维（CoT）方式，将非结构化问题转换为**结构化抽象概念路径Pq**（一组抽象三元组），同时生成推理过程Rationales（式4）。
  - 示例：问题“What is the name of the daughter of the artist who had the The Mrs. Carter Show World Tour?”被转换为“Nicki Minaj(artist)→had→The Mrs. Carter Show World Tour; Nicki Minaj(artist)→has daughter named→Chiara Fattorini(person)”。
  - 关键优势：即使路径中的实体名不准确，概念级三元组仍与KG中抽象化三元组语义对齐，检索鲁棒。

- **模块3：抽象驱动检索（Abstraction-driven Retrieval）**：
  - 在每轮检索迭代中，从候选抽象三元组集合T_abs_q中，依据与抽象概念路径Pq的语义相似度（余弦相似度，式5），选出W个最相关的三元组T_abs_q,opt。
  - 将本轮结果累积到总证据集T_abs_q,all；用新发现的实体替换主题实体进入下一轮迭代。检索参数包括宽度W和深度D。

- **模块4：生成器（Generator）**：
  - 将问题、证据集T_abs_q,all、指令和示例输入LLM，生成标志Flag和答案Ans（式6）。若Flag为正则直接输出答案；否则进入下一轮检索。
  - 输出的MID在用户端通过隐私映射表替换为真实名称，真实名称始终不暴露给LLM。

---

### 3. 实验设计：数据集、基准与对比方法
- **数据集**（均基于Freebase知识图谱）：
  - **WebQSP**：1,639个测试样本（#Filtered为535个）。
  - **CWQ**（Complex WebQuestions）：1,000个测试样本（#Filtered为449个），多为至少2跳推理的多跳问题。
  - **GrailQA**：1,000个测试样本（#Filtered为645个），多为长尾知识、多样化问题。
- **两种实验设置**：
  1. **#Total设置**：在完整测试集上测试。
  2. **#Filtered设置**：模拟严格隐私保护场景，剔除可通过CoT提示直接回答的样本，确保剩余问题必须依赖KG中的私有知识。
- **评价指标**：Hits@1（精确匹配准确率）。
- **对比基线**（按类别划分）：
  - **Pure-LLM方法**：IO（直接提示）、CoT（思维链）、CoT-SC（自一致性）。
  - **语义解析（SP）方法**：KB-BINDER、KB-BINDER-R、TrustUQA、TrustUQA-R（动态示例变体）。
  - **RAG方法**：ToG（Think-on-Graph，束搜索检索）、PoG（Plan-on-Graph，反射/记忆/自适应广度）、GoG（Generate-on-Graph，LLM补充知识）。
- **实现细节**：底层LLM为GPT-4O-MINI-2024-07-18；SA和Generator温度设为0，RA温度设为0.4；宽度W和深度D默认设为3；每组实验重复3次取平均。

---

### 4. 资源与算力
- **文中未明确说明**具体使用的GPU型号、数量、训练时长或API调用总预算等硬件资源细节。
- 仅提及使用**GPT-4O-MINI-2024-07-18**作为底层LLM，通过API调用方式运行；温度、惩罚参数等有设置说明。
- 效率研究（表4）报告了平均token使用量（输入/输出/总token）和LLM调用次数：如WebQSP上ARoG总token 7,752.1、调用17.3次；GrailQA上ARoG总token 5,605.5、调用12.5次，为同类方法中最低。但未报告具体算力成本或GPU配置。

---

### 5. 实验数量与充分性
- **实验规模与类型**：
  1. **主实验（表2）**：在3个数据集 × 2种设置（#Total/#Filtered）下，与9种基线方法对比（覆盖Pure-LLM/SP/RAG三类），共6组主结果。
  2. **消融实验（表3）**：针对RA模块3个步骤（关系检索Step1、关系过滤Step2、实体抽象Step3）和SA模块进行组合消融，共6组配置 × 6种设置组合，较系统地验证各组件贡献。
  3. **效率研究（表4）**：与3种RAG方法对比token消耗与LLM调用数。
  4. **定量研究（图3）**：在3个数据集上改变宽度W和深度D（1~4）进行参数敏感性分析。
  5. **深度分析（图4）**：比较SA模块的4种抽象策略变体（ARoG、with CoT、with Dec、w/o SA）。
  6. **隐私场景分析（图5）**：在4种不同隐私场景（PRI、P-R、P-G、P-RAG）下比较ARoG、ARoG-R（LLM检索变体）与ToG的表现。
- **充分性评估**：
  - **优点**：覆盖多种数据集类型（单跳/多跳/长尾）、多种方法类别、多种隐私场景；消融设计合理（不拆Step1和Step2的相关组合）；参数敏感性分析完整；效率评估客观（对比token和调用数）。
  - **客观性**：主实验与基线在同一匿名实体条件（MIDs）下比较，公平合理。但SP类方法在部分数据集上因缺少形式化查询标注无法运行（以“-”标出），对比不够完整。
  - **总体评价**：实验数量丰富、设计较规范，从性能、效率、鲁棒性、参数敏感性多个维度验证了ARoG的有效性，在学术论文中属于较充分的实验体系。

---

### 6. 论文的主要结论与发现
- **ARoG在所有三个数据集的#Total和#Filtered设置下均取得最佳性能**（Hits@1）：WebQSP 74.7/58.9、CWQ 60.0/36.3、GrailQA 78.7/71.8，相对第二名分别提升6.1/5.8、4.9/19.8、16.4/9.0个百分点。
- **现有RAG方法在匿名实体场景下表现不佳**：大多数RAG基线在#Filtered设置下性能大幅下降（如ToG在WebQSP #Fil仅8.2），表明它们高度依赖具体实体信息进行检索和推理。
- **RA和SA两个抽象策略均显著有效**：去掉RA模块性能下降至少2.5%（#Total）和3.8%（#Filtered）；去掉SA模块性能下降至少2.4%（#Total）和1.1%（#Filtered），且SA对多跳数据集（CWQ）影响最大。
- **效率与性能可兼顾**：ARoG在GrailQA上总token消耗最低（5,605.5），在WebQSP上与ToG接近，同时性能大幅领先；相比GoG显著节约token。
- **检索宽度和深度的影响因数据集而异**：WebQSP对宽度敏感、深度影响很小（答案多在1跳内）；CWQ和GrailQA两者均有提升但深度超过2后收益递减。
- **抽象概念路径优于纯推理链和问题分解**：在SA模块中，ARoG的抽象概念路径策略在全部条件下优于CoT和Dec替代方案。
- **ARoG在不同隐私场景下表现出高度鲁棒性**：在检索或生成阶段实体匿名时均能保持高性能，而ToG在生成阶段匿名时性能显著下降。

---

### 7. 优点：方法或实验设计上的亮点
- **问题新颖性和实践价值高**：首次系统定义并研究“隐私保护RAG场景”，切中LLM应用中的真实痛点——第三方API调用时的隐私泄露风险。
- **方法设计巧妙**：
  - 利用**关系作为语义桥梁**：在不暴露实体本身的情况下，从相邻关系中提取语义并抽象为概念，实现“知其上下文而不知其名”。
  - **双向抽象**：既抽象KG侧实体（关系中心抽象），也抽象问题侧结构（结构导向抽象），使两侧在概念层面可对齐，设计逻辑闭环。
  - **隐私与性能兼顾**：关系属于图谱模式结构（schema）而非敏感数据，共享关系给LLM风险极低，实现了严格的隐私保护。
- **鲁棒性设计**：抽象概念路径不依赖于正确实体名，即使路径中实体错误也能语义对齐，体现较强的容错性。
- **实验设计规范**：
  - 设置#Filtered场景以排除LLM内化知识的干扰，更真实地评估RAG对私有知识的依赖度。
  - 消融实验考虑组件间的依赖关系（如不拆Step1或单独删Step2），设计合理。
  - 提供效率分析、参数敏感性分析、多种隐私场景对比等，评估维度全面。

---

### 8. 不足与局限
- **实验覆盖有限**：
  - 所有实验基于Freebase这一个KG和三个问答数据集，未在其他KG类型（如Wikidata、领域知识图谱）上验证泛化性。
  - 底层LLM仅使用GPT-4O-MINI，未测试其他LLM（开源/闭源、不同规模）下的表现。
  - SP类基线在CWQ和GrailQA上无法运行，对比不完整。
- **隐私保护的边界未充分讨论**：
  - 本文保护的是“实体语义”，但如何界定“隐私”的严格程度（如是否允许LLM知道关系结构也可能侧面泄露信息）未做深入讨论。
  - 假设“共享关系给LLM隐私风险极小”，但某些特定关系本身可能隐含敏感信息（如“has_disease”），该假设的成立条件未加论证。
  - 假设主题实体的名称是可知的（为保证任务可行性），这一假设在完全严格的隐私场景下可能不成立。
- **算力/资源信息披露不足**：未报告GPU类型、数量、推理总成本等，可复现性和成本评估受限。
- **依赖LLM质量**：实体抽象和问题抽象均依赖LLM的生成能力，如LLM本身无法从关系中推断概念（长尾或领域特殊关系），方法性能可能受限。
- **相对提升幅度差异较大**：在CWQ上的绝对准确率仍较低（#Filtered仅36.3%），复杂多跳问题在隐私场景下的解决能力仍有较大上升空间。
- **未说明误差来源**：没有对失败案例进行定性与定量分析，读者难以判断瓶颈在检索还是生成阶段。

---

（完）

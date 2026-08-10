---
title: "Seeing, Listening, Remembering, and Reasoning: A Multimodal Agent with Long-Term Memory"
title_zh: 看、听、记、思：具有长期记忆的多模态智能体
authors: "Lin Long, Yichen He, Wentao Ye, Yiyuan Pan, Yuan Lin, Hang Li, Junbo Zhao, Wei Li"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=PMz29A7Muq"
tags: ["query:agent"]
score: 9.0
evidence: 具有长期情节与语义记忆的多模态智能体，用于视频问答
tldr: 多模态智能体往往难以对长视频进行持续的感知与记忆。M3-Agent构建了实体中心的多模态长期记忆，能实时处理视觉和听觉输入以更新情节记忆与语义记忆，并在推理时检索相关记忆。作者还提供了M3-Bench长视频问答基准，包含机器人视角视频与多样化问题。实验表明该框架能显著提升多模态场景下的记忆效果和推理能力。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 多模态智能体缺乏长期记忆，难以在长时间视频环境中持续积累知识与推理。
method: 提出M3-Agent，以实体为中心组织多模态长期记忆，结合视觉/听觉输入更新记忆并检索辅助多轮推理。
result: 在M3-Bench上验证了记忆机制对多模态长视频问答的有效性，显著改善推理准确率。
conclusion: 长期记忆是多模态智能体实现持续理解和推理的关键，该工作建立了评测基准和框架。
---

## Abstract
We introduce M3-Agent, a novel multimodal agent framework equipped with long-term memory. Like humans, M3-Agent can process real-time visual and auditory inputs to build and update episodic and semantic memories, gradually accumulating world knowledge. Its memory is organized in an entity-centric, multimodal manner, enabling deeper and more consistent understanding of the environment. Given an instruction, M3-Agent autonomously performs multi-turn reasoning and retrieves relevant memories to complete tasks. To evaluate memory effectiveness and memory-based reasoning in multimodal agents, we develop M3-Bench, a long-video question answering benchmark comprising 100 newly recorded robot-perspective videos (M3-Bench-robot) and 920 diverse web-sourced videos (M3-Bench-web). We annotate QA pairs designed to test capabilities essential for agent applications, such as person understanding, general knowledge extraction, and cross-modal reasoning. Experimental results show that M3-Agent, trained via reinforcement learning, outperforms the strongest baseline, a prompting agent using Gemini-1.5-pro and GPT-4o, achieving 6.7%, 7.7%, and 5.3% higher accuracy on M3-Bench-robot, M3-Bench-web and VideoMME-long, respectively. Our work advances multimodal agents toward more human-like long-term memory and provides insights for their practical design. Models, datasets and code are available at https://github.com/ByteDance-Seed/m3-agent.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 核心问题与整体含义
- **研究动机**：当前多模态智能体在处理长视频任务时，缺乏类似人类的长期记忆能力，难以在长时间跨度内持续感知环境、积累知识并进行连贯推理。现有模型大多只依赖当前上下文，无法有效记住过去的重要信息。
- **背景意义**：多模态智能体是迈向通用人工智能的重要方向，但缺少长期记忆机制使其在真实复杂场景（如机器人导航、人与环境交互理解等）中表现受限。本研究旨在弥补这一关键缺口，推动多模态智能体向更类人化的认知能力发展。

## 2. 方法论
- **核心思想**：提出 **M3-Agent** 框架，模拟人类“看、听、记、思”的认知过程。智能体实时处理视觉与听觉输入，以实体为中心（entity-centric）组织多模态长期记忆，持续构建并更新两类记忆：
  - **情节记忆（Episodic Memory）**：记录具体事件的时间与空间信息；
  - **语义记忆（Semantic Memory）**：积累关于世界的一般性知识与概念。
- **技术细节**：
  - 记忆以**实体为中心**组织，使得记忆检索更加精准，并能保持对环境理解的深层一致性；
  - 给定指令后，智能体**自主执行多轮推理**，动态检索与当前任务相关的历史记忆，辅助生成回答；
  - 模型通过**强化学习（Reinforcement Learning）** 进行训练，以优化记忆写入与读取的策略。
- **算法/流程描述**（文字说明）：
  1. 感知模块实时接收视频中的视觉帧与音频信号；
  2. 提取多模态信息特征，识别关键实体与事件；
  3. 将新信息与已有记忆进行整合，更新情节记忆与语义记忆；
  4. 收到用户指令后，通过记忆检索模块提取相关记忆片段；
  5. 多轮推理模块结合当前输入与检索到的记忆，生成最终回答。

## 3. 实验设计
- **新构建基准（M3-Bench）**：
  - **M3-Bench-robot**：包含 **100 个**新录制的机器人视角视频，模拟机器人实际应用场景；
  - **M3-Bench-web**：包含 **920 个**多样化的网络来源视频，覆盖更广泛的环境与主题；
  - 标注了针对智能体应用关键能力的问答题（QA），包括**人物理解**、**常识知识提取**、**跨模态推理**等任务类型。
- **额外评测集**：使用 **VideoMME-long** 作为长视频问答的补充验证。
- **对比方法**：以使用 **Gemini-1.5-pro** 与 **GPT-4o** 的提示词智能体（Promoting Agent）作为最强基线，与 M3-Agent 进行对比。

## 4. 资源与算力
- 论文原文中**未明确说明**训练所使用的 GPU 型号、数量或训练时长等算力信息。作者仅在最后提供了开源仓库地址（GitHub），但资源细节需要查阅完整论文正文或代码仓库才能获取。

## 5. 实验数量与充分性
- **实验数量**：论文在三个评测集上开展验证：M3-Bench-robot、M3-Bench-web 和 VideoMME-long，并给出了与最强基线的准确率对比结果。此外，论文在摘要中提到使用强化学习训练，暗示了训练与评测流程的完整性。
- **充分性与客观性**：
  - 采用新构建的高质量基准（包含自录机器人视频和网络真实视频），覆盖了从窄域到广域的多种场景，提高了评测的多样性；
  - 对比的是当前最强的商业化模型（Gemini-1.5-pro 和 GPT-4o）组成的基线，具备较强的说服力；
  - 但，由于摘要长度限制，文中未展示更细粒度的消融实验（如去掉记忆模块、单一模态输入等），对记忆机制各组成部分的贡献分析不够详细。此外，引入 VideoMME-long 作为外部基准增加了客观性，但未提及与更多近期方法的全面对比。因此可认为实验设计较为可靠，但充分性有进一步提升空间。

## 6. 主要结论与发现
- **核心结论**：长期的、实体中心的多模态记忆框架能够显著提升智能体在长视频问答任务中的表现。M3-Agent 在三个基准上均优于最强基线，准确率分别提升：
  - **M3-Bench-robot** 上提升 **6.7%**；
  - **M3-Bench-web** 上提升 **7.7%**；
  - **VideoMME-long** 上提升 **5.3%**。
- 上述结果表明，长期记忆机制是多模态智能体实现持续理解与推理的关键组件，且跨场景泛化效果良好。

## 7. 优点
- **方法论亮点**：
  - 提出实体中心的多模态长期记忆组织方式，兼具情节记忆与语义记忆，在认知架构上模拟人类记忆机制；
  - 融合视觉＋听觉双模态实时输入，贴近真实智能体环境感知需求；
  - 自主多轮推理＋记忆检索的设计，使框架具备较强的任务完成能力。
- **实验设计亮点**：
  - 构建了全新的 **M3-Bench** 基准，包含 100 个机器人视角视频和 920 个网络视频，尤其在机器人场景上的贡献具有独特应用价值；
  - 基准问题设计涵盖人员理解、常识提取与跨模态推理等关键能力维度，测评维度丰富；
  - 在自建基准之外还引入了外部基准 VideoMME-long 进行交叉验证，增强了结果的可信度。
- **开放贡献**：提供了模型、数据集和代码开源地址，便于后续研究复现与扩展。

## 8. 不足与局限
- **资源信息不透明**：摘要未提及算力消耗（GPU 型号、数量、训练时长），不利于对方法成本进行评估与复现规划。
- **消融实验细节缺失**：未在可用内容中看到对记忆模块各组成部分（如情节与语义记忆的单独效果、实体中心组织的作用）的消融分析，难以评判各核心组件的独立贡献。
- **覆盖范围有限**：
  - 主要评测聚焦于视频问答任务，对更广泛的多模态智能体应用（如交互式决策、具身操作等）尚未验证；
  - M3-Bench-web 虽包含 920 个视频，但相对开放世界真实场景仍是有限采样，可能存在偏差。
- **基线局限性**：主要与 GPT-4o 和 Gemini-1.5-pro 等闭源系统对比，未涉及同量级开源多模态模型的横向比较，可能影响对工程实现优势的单独判断。

（完）

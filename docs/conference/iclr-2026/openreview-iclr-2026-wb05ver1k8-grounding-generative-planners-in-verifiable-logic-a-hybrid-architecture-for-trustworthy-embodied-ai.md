---
title: "Grounding Generative Planners in Verifiable Logic: A Hybrid Architecture for Trustworthy Embodied AI"
title_zh: 将生成式规划器建立在可验证逻辑之上：可信具身AI的混合架构
authors: "Feiyu Wu, Xu Zheng, Yue Qu, Zhuocheng Wang, Zicheng Feng, HUI LI"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=wb05ver1k8"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 可验证逻辑用于具有安全保证的可信具身AI规划
tldr: 本文针对LLM规划器缺乏形式化推理和严格安全保证的问题，提出可验证迭代精化框架VIRF，将神经规划与符号验证结合，为LLM提供因果性教学反馈，从而为具身AI生成可证明安全的计划。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: LLM在具身AI规划中具有前景，但其随机性和缺乏形式推理阻碍了物理部署所需的安全保证。
method: 提出神经符号架构VIRF，通过符号验证器生成因果性反馈，教授LLM为何计划不安全并迭代调整。
result: 框架将被动安全守门员转变为主动安全合作者，能够提供可证明正确且安全的计划。
conclusion: VIRF为具身AI提供了一种实现严格安全保证的路径，是向可信自主系统迈进的关键。
---

## Abstract
While Large Language Models (LLMs) show immense promise as planners for embodied AI, their stochastic nature and lack of formal reasoning capabilities prevent the strict safety guarantees required for physical deployment. Current approaches fall short: they either rely on other unreliable LLMs for safety checks or simply reject unsafe plans without offering a path to success. This work bridges this critical gap by introducing the Verifiable Iterative Refinement Framework (VIRF), a neuro-symbolic architecture that shifts the paradigm from a passive safety gatekeeper to an active safety collaborator. Where prior verifiers simply reject failures, our framework provides causal, pedagogical feedback that teaches the LLM why its plan was unsafe, enabling intelligent repairs rather than mere avoidance.Our core contribution is a novel tutor-apprentice dialogue, where a deterministic Logic Tutor, grounded in a formal safety ontology, provides causal and explanatory feedback to an LLM Apprentice planner. This pedagogical interaction allows the apprentice to perform intelligent, creative plan repairs, resolving safety conflicts rather than merely avoiding them. To ground this dialogue in verifiable truth, we introduce a scalable knowledge acquisition pipeline that synthesizes a comprehensive safety knowledge base from real-world documents, a process that simultaneously reveals and corrects significant blind spots in existing benchmarks. On a new suite of challenging home safety tasks, VIRF achieves a perfect 0\% Hazardous Action Rate (HAR), completely eliminating unsafe actions while attaining a 77.3\% Goal-Condition Rate (GCR)—the highest among all baselines. It does so with remarkable efficiency, requiring only 1.1 correction iterations on average. By acting as a verifiable safety scaffold, VIRF demonstrates a principled and robust pathway toward building embodied agents that are not just capable, but fundamentally trustworthy.

---

## 论文详细总结（自动生成）

# 论文总结：Grounding Generative Planners in Verifiable Logic: A Hybrid Architecture for Trustworthy Embodied AI

## 1. 论文的核心问题与整体含义
- **研究动机**：大型语言模型（LLM）在具身AI的任务规划中展现出巨大潜力，但其输出具有随机性且缺乏形式逻辑推理能力，无法提供物理部署所需的安全保证。
- **现有方法的不足**：当前方法要么依赖其他同样不可靠的LLM进行安全检查，要么只是简单拒绝不安全的计划而不给出成功的替代路径，无法真正解决安全与任务完成之间的矛盾。
- **核心问题**：如何将生成式规划器的神经能力与可验证的符号逻辑相结合，使规划器不仅能生成完成任务的计划，还能保证每一步行为在物理环境中绝对安全。
- **整体含义**：论文旨在为可信自主系统建立一条从“被动安全守门员”到“主动安全合作者”的范式转换，通过可验证的安全脚手架，使具身代理不仅能力强，而且根本可信。

## 2. 论文提出的方法论
- **核心思想**：提出神经符号混合架构**VIRF（Verifiable Iterative Refinement Framework）**，通过“导师-学徒”对话机制，将确定性逻辑导师（Logic Tutor）与LLM学徒规划器结合。导师基于形式化安全本体提供因果性、解释性反馈，学徒据此进行智能修复，而非简单回避。
- **关键技术细节**：
  - **形式化安全本体**：构建一个确定性的、可验证的逻辑知识库，用于表达安全规则和因果关系。
  - **知识获取管线**：提出可扩展的自动化知识构建流程，从现实世界文档（如操作手册、安全规范）中综合提取安全知识，同时能揭示并纠正现有基准中的安全盲点。
  - **导师-学徒互动**：规划器生成计划后，逻辑导师验证计划安全性，若失败则生成因果解释（为何不安全），指导LLM调整计划。该过程迭代进行，平均仅需1.1次修正迭代。
- **公式/算法流程**（文字描述）：
  1. 给定任务目标，LLM学徒生成初始计划。
  2. 符号验证器基于安全知识库检查计划动作序列，标记不安全动作并提取对应的安全违例原因。
  3. 若存在违例，导师将因果反馈（违例类型、涉及对象、错误推理）以自然语言形式返回给学徒。
  4. 学徒根据反馈重新规划，生成修正计划，回到步骤2，直到计划完全安全且达到目标条件。
  5. 输出最终可证明安全且任务完成性最高的计划。

## 3. 实验设计
- **数据集/场景**：采用一套全新且具有挑战性的**家庭安全任务**（home safety tasks），该场景来自论文中构建的综合安全知识库。对比现有基准，作者指出其知识管线揭示了现有基准中的安全盲点。
- **评估指标**：
  - **危险行为率（HAR, Hazardous Action Rate）**：衡量计划中不安全行动的比例。
  - **目标条件达成率（GCR, Goal-Condition Rate）**：衡量计划最终完成预设任务目标的成功率。
  - **修正迭代次数**：衡量修正效率。
- **对比方法**：摘要未列出具体的基线方法名称，但明确指出VIRF对比了所有基线方法，取得了最优的HAR和GCR。推测基线可能包括纯LLM规划器、LLM自我检查方法、拒绝式校验器等。

## 4. 资源与算力
- **算力信息**：提供的摘要文本中**未提及**任何关于GPU型号、数量、训练时长或推断成本的具体信息。文初的元数据中也没有相关字段。因此无法从现有内容中获取该部分信息。

## 5. 实验数量与充分性
- **实验数量**：摘要仅报告了在**家庭安全任务新基准**上的主要实验结果以及一项效率指标（平均修正迭代次数）。由于只有摘要，无法具体知晓是否有其他场景（如厨房安全、工业安全）、消融实验（如去掉因果反馈、换用不同的LLM backbone、知识库规模影响）、鲁棒性测试等。
- **充分性与公平性**：摘要宣称VIRF在HAR上达到**0%**（完全消除不安全行为）且GCR最高（77.3%），这是一个非常强的结果。但由于缺乏对基线方法的具体描述和详细消融，仅凭摘要难以完全评估实验的全面性。不过，基于其提出的知识管线揭示现有基准盲点的说法，论文可能包含对现有基准的分析实验，具有一定说服力。

## 6. 论文的主要结论与发现
- VIRF架构成功将被动安全守门员转变为主动安全合作者，实现了**可证明安全且有效的规划**。
- 在家庭安全任务上，VIRF的**危险行为率降至0%**，同时获得所有基线中最高的**77.3%的目标条件达成率**，且修正过程高效（平均1.1次迭代）。
- 形式化逻辑提供的**因果性教学反馈**是使LLM能智能化、创造性修复计划的关键，而非简单拒绝。
- 可扩展的安全知识管线不仅能支持验证，还能揭示并纠正现有基准的不足，为领域提供更坚实的评估基础。
- 整体表明，通过神经符号结合为具身AI赋予严格安全保证是一条可行且稳健的路径。

## 7. 优点：方法或实验设计上的亮点
- **新颖的范式转换**：从拒绝型安全检查转向教学型安全合作，使规划器具备“从错误中学习并修复”的能力。
- **确定性与可解释性**：采用形式化逻辑本体进行验证，提供可解释的因果反馈，而非黑盒判断，增强了系统的可信度。
- **知识管线创新**：自动化构建安全知识库并暴露现有基准盲点，具有科学价值与实践意义。
- **实证结果突出**：完美消除不安全行为（0% HAR）的同时保持高任务成功率，且修正效率极高，展现了方法的有效性与实用潜力。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **公开信息有限**：目前仅能基于摘要分析，**缺乏完整的实验细节**（如基线列表、消融研究、统计显著性检测、错误分析等），难以客观评判其结果的鲁棒性和泛化性。
- **场景局限性**：实验仅提及“家庭安全任务”，可能局限于特定环境与安全规则，向更复杂、开放域的物理世界迁移的挑战尚未体现。
- **知识库覆盖偏差**：安全知识库的构建依赖可获取的现实文档，可能无法穷尽所有安全隐患，或存在领域偏差（如以西方家庭场景为主）。
- **LLM依赖**：尽管有逻辑导师，学徒部分仍基于LLM，其随机性可能导致在某些极端案例下修复失败或多次迭代，原文平均1.1次虽低，但未报告最坏情况。
- **计算开销**：虽迭代少，但每次迭代需调用验证器与LLM重新规划，当安全规则极为复杂时，推理延迟可能不可忽略。缺乏与纯端到端方法在实时性上的对比。

（完）

---
title: "QuadSentinel: Sequent Safety for Machine-Checkable Control in Multi-agent Systems"
title_zh: "QuadSentinel: 面向多智能体系统的序列安全与机器可检查控制"
authors: "Yiliu Yang, Yilei Jiang, Qunzhong Wang, Yingshui Tan, Xiaoyong Zhu, Bo Zheng, Sherman S. M. Chow, Xiangyu Yue"
date: 2026-01-23
pdf: "https://openreview.net/pdf/0e7b2096c2d4dd68360ee6095e30d3747b237779.pdf"
tags: ["query:safe-codegen"]
score: 4.0
evidence: 为基于LLM的智能体实施可机器检查的安全策略，可应用于机器人系统安全
tldr: 基于LLM的智能体在执行复杂任务时存在安全风险，但用自然语言书写的安全策略因模糊和上下文依赖而难以进行机器检查和可靠执行。本文提出QuadSentinel，一个由状态跟踪器、策略验证器、威胁观察器和裁判组成的四代理守卫系统，将安全策略表达为序列，并编译为基于可观察状态谓词的机器可检查规则，在线执行。通过裁判逻辑和高效的top-k谓词更新器，优先检查并分层解决冲突，保持低开销。在ST-WebAgentBench上的实验表明，QuadSentinel能有效减少安全违规。尽管该工作针对通用多智能体系统，但其安全策略强制执行机制可迁移至机器人系统，为编程具身智能提供安全保障。该方法提供了一种运行时安全监控方案，有助于实现安全代码生成在部署中的闭环验证。其模块化设计便于集成到现有机器人控制框架中。因此，QuadSentinel为在真实环境中安全部署基于LLM的智能体提供了重要保障。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM代理的安全策略因自然语言的歧义性难以机器检查和可靠执行。
method: 提出QuadSentinel四代理守卫，将安全策略编译为序列形式的机器可检查规则并在线强制执行。
result: 在Web代理基准上验证了有效性，显著降低安全违规，开销可控。
conclusion: QuadSentinel为多智能体系统提供运行时安全保证，可迁移到机器人安全编程。
---

## Abstract
Safety risks arise as large language model-based agents solve complex tasks with tools, multi-step plans, and inter-agent messages. However, deployer-written policies in natural language are ambiguous and context dependent, so they map poorly to machine-checkable rules, and runtime enforcement is unreliable. Expressing safety policies as sequents, we propose QuadSentinel, a four-agent guard (state tracker, policy verifier, threat watcher, and referee) that compiles these policies into machine-checkable rules built from predicates over observable state and enforces them online. Referee logic plus an efficient top-$k$ predicate updater keeps costs low by prioritizing checks and resolving conflicts hierarchically. Measured on ST-WebAgentBench (ICML CUA '25) and AgentHarm (ICLR '25), QuadSentinel improves guardrail accuracy and rule recall while reducing false positives, achieving a low 0.33$\times$ time overhead compared to 1.24$\times$ for code-generation baselines. Against single-agent baselines such as ShieldAgent (ICML '25), it yields better overall safety control by securing both message-based coordination and tool execution. Near-term deployments can adopt this pattern without modifying core agents by keeping policies separate and machine-checkable.

---

## 论文详细总结（自动生成）

# 详细总结

## 1. 论文的核心问题与整体含义
- **核心问题**：基于大语言模型（LLM）的多智能体系统在执行复杂任务（工具调用、多步规划、代理间消息传递）时，会产生难以预料的安全风险。当前的常见做法是由部署者用自然语言编写安全策略，但这些策略存在固有的**歧义性**和**上下文依赖性**，无法直接转化为机器可自动检查与可靠执行的规则，导致运行时的策略强制执行（enforcement）并不可靠。
- **整体含义**：本文提出 **QuadSentinel**，一种将安全策略形式化为“**序列**（sequents）”并编译为机器可检查规则的运行时守卫系统。其目标是为多智能体协作提供一种 **可验证、低开销、与核心代理解耦** 的安全控制方案，使得安全策略的维护和执行独立于任务代理本身，从而在部署中实现可靠的闭环安全验证。

## 2. 论文提出的方法论
- **核心思想**：将部署者书写的安全策略用**序列**（可理解为“前提 ⇒ 结论”的逻辑规则）进行表达，并将这些序列编译为基于**可观察状态谓词**的机器可检查规则，由四个专职代理在运行时协同执行策略检查与冲突裁决。
- **四代理守卫架构**：
  - **状态跟踪器（State Tracker）**：负责持续追踪环境与智能体的可观察状态，为规则检查提供事实基础。
  - **策略验证器（Policy Verifier）**：基于编译后的机器规则，对正在发生的动作或执行计划进行安全性验证。
  - **威胁观察器（Threat Watcher）**：主动识别潜在的安全威胁，触发预警或额外检查。
  - **裁判（Referee）**：当不同策略验证结果或代理间消息传递产生冲突时，通过**裁判逻辑**进行分层仲裁与冲突解决。
- **关键技术细节**：
  - **安全策略的序列化编译**：将模糊的自然语言策略通过序列形式固化，转换为仅依赖于可观察状态的布尔谓词规则，实现严格的机器可检查性。
  - **高效 top-k 谓词更新器**：并非对所有谓词一视同仁，而是动态维护一个优先检查的谓词集合（top-k），依据状态变化频率和风险等级调整优先级，从而大幅降低冗余检查的计算开销。
  - **分层冲突裁决**：Referee 模块按安全等级的层次结构处理冲突（如硬约束优先于软约束），保证策略执行的一致性。
- **部署特点**：整个 QuadSentinel 守卫系统作为外部监督层运行，**不需修改核心任务代理的任何内部逻辑**，保持了策略与实现的高度分离。

## 3. 实验设计
- **数据集与基准**：
  - **ST-WebAgentBench**（ICML CUA ’25）：一个面向网站智能体的安全任务基准。
  - **AgentHarm**（ICLR ’25）：另一个用于评估代理危害行为的基准。
- **对比方法**：
  - **代码生成基线（code-generation baselines）**：指通过生成代码来实现安全防护的方法，文中给出了其时间开销（1.24×）。
  - **单代理基线 ShieldAgent**（ICML ’25）：一个单代理安全防护方案，用于对比在基于消息的协调和工具执行方面的整体安全控制能力。
- **评估指标**：
  - 准确率（guardrail accuracy）与规则召回率（rule recall）。
  - 假阳性（false positives）的减少程度。
  - 时间开销（相对于无防护执行的时间倍数），QuadSentinel 为 0.33×，远低于代码生成基线的 1.24×。

## 4. 资源与算力
- 提供的摘要与元数据中**未明确提及所使用的 GPU 型号、数量、训练时长或任何模型微调细节**。从方法描述推测，QuadSentinel 主要是一种**运行时逻辑执行与状态监测系统**，可能不涉及大规模训练，更多依赖推理与轻量级状态更新；但文中并未给出具体的硬件配置或算力消耗数据。

## 5. 实验数量与充分性
- **实验覆盖范围**：在两个公开基准（ST-WebAgentBench 和 AgentHarm）上进行了评估，覆盖了 Web 代理场景下的安全违规问题。
- **对比维度**：至少与两类基线（代码生成方法、ShieldAgent）进行了对比，并考察了保护准确率、召回率、假阳性及时间效率。
- **隐含的消融实验**：摘要提到“referee logic plus an efficient top-$k$ predicate updater keeps costs low”，暗示对裁判逻辑和谓词更新器进行了设计层面或效果层面的验证，但**摘要未明确列出消融实验的具体组数和结果**。
- **充分性与客观性**：从已有信息看，实验选择了有影响力的外部基准，对比方法包含近期（ICML/ICLR）的同类工作，且给出了量化的安全改善和开销指标，具有一定的客观性。但受限于仅提供摘要，无法判断实验否覆盖了多种智能体类型、复杂对话流、失败案例等，实验的完备性尚需审阅全文。

## 6. 论文的主要结论与发现
- **安全效果**：QuadSentinel 能在多智能体 Web 任务中有效减少安全违规，同时提高规则召回率并降低假阳性。
- **效率优势**：通过谓词优先检查和分层裁决，实现了 **0.33× 的时间开销**，远优于代码生成式防护的 1.24×，证明安全监控可以做到轻量级且实用。
- **对比领先**：与单代理方案 ShieldAgent 相比，QuadSentinel 在保障**消息式协调安全**和**工具执行安全**两个方面均提供了更优的整体控制。
- **迁移与部署**：该守卫模式无需修改任务代理，策略保持独立且可机器检查，因此便于向机器人等其他具身智能系统迁移，为安全代码生成与部署的闭环验证提供一种运行时方案。

## 7. 优点
- **形式化与可验证**：用序列与可观察谓词将安全策略严格形式化，克服了自然语言策略的歧义性和不可机器检查的痛点。
- **模块化解耦设计**：四代理各司其职，守卫系统与任务代理完全分离，易于集成到现有框架，也便于策略的独立维护与更新。
- **低开销高效率**：创新的 top-k 谓词更新器和裁判逻辑大幅压缩了运行时成本，使在线安全强执行真正可行。
- **冲突处理机制**：通过分层裁判逻辑解决了多策略并发检查下可能出现的规则冲突问题，提高了执行的可靠性。
- **跨领域潜力**：虽然主要在 Web 代理场景验证，但方法论以可观察状态和行为规则为锚点，对机器人、具身智能等同样具有普适性。

## 8. 不足与局限
- **实验边界有限**：仅在两个 Web 智能体基准上测试，**未在真实机器人、多模态物理环境或其他高风险领域（如医疗、金融）中直接验证**，可迁移性仍有待实证。
- **抽象细节缺失**：摘要未透露策略编译的正确性保证、对动态未知状态的泛化能力以及“裁决逻辑”具体实现，安全策略的表达力边界尚不明确。
- **依赖可观察状态**：系统的规则完全建立在“可观察状态谓词”之上，对于需要推断内部意图、未捕捉到的隐藏状态或对抗性模糊状态的安全问题，可能失效。
- **多代理协作可靠性**：QuadSentinel 本身是一个四代理系统，其内部通信与同步可能引入新的故障点或延迟，摘要未讨论该守卫网络本身的自恢复或降级机制。
- **对抗鲁棒性未知**：未提及在 LLM 被恶意提示或攻击者试图绕过守卫时的表现，安全性验证可能偏向友好或常规任务环境。

（完）

---
title: "VeriGuard: Enhancing LLM Agent Safety via Verified Code Generation"
title_zh: VeriGuard：通过验证代码生成增强LLM代理安全
authors: "Lesly Miculicich, Mihir Parmar, Hamid Palangi, Krishnamurthy Dj Dvijotham, Mirko Montanari, Tomas Pfister, Long Le"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=SnEywLKodN"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 通过验证代码生成为LLM代理提供形式安全保证
tldr: LLM代理在医疗、金融等领域的应用存在重大安全隐患，可能偏离目标或泄露隐私。VeriGuard通过双阶段架构解决此问题：首先离线澄清用户意图并生成可验证的安全规范，然后在线时实时检查生成代码的合规性。对代理行为的完全形式化保证，使其能抵御对抗攻击并遵循预定策略。实验结果显示，该框架能有效拦截不安全动作，为安全敏感场景的代码生成提供了可验证的防护网。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 自主代理可能偏离目标或违反策略，缺乏形式化安全保障。
method: 双阶段架构：离线意图澄清与验证条件生成，在线执行合规监控。
result: 实现了对代理行为的强形式化安全保证，阻止不安全操作。
conclusion: 为高风险领域提供可验证的安全基础，适用于医疗等场景。
---

## Abstract
The deployment of autonomous AI agents in sensitive domains, such as healthcare, introduces critical risks to safety, security, and privacy. These agents may deviate from user objectives, violate data handling policies, or be compromised by adversarial attacks. Mitigating these dangers necessitates a mechanism to formally guarantee that an agent's actions adhere to predefined safety constraints, a challenge that existing systems do not fully address.
We introduce \ours{}, a novel framework that provides formal safety guarantees for LLM-based agents through a dual-stage architecture designed for robust and verifiable correctness. The initial offline stage involves a comprehensive validation process. 
It begins by clarifying user intent to establish precise safety specifications. \ours{} then synthesizes a behavioral policy and subjects it to both extensive testing in simulated environments and rigorous formal verification to mathematically prove its compliance with these specifications. 
This iterative process refines the policy until it is deemed correct. Subsequently, the second stage provides online action monitoring, where \ours{} operates as a runtime monitor to validate each proposed agent action against the pre-verified policy before execution. This separation of the exhaustive offline validation from the lightweight online monitoring allows formal guarantees to be practically applied, providing a robust safeguard that substantially improves the trustworthiness of LLM agents in complex, real-world environments.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景与动机**：随着自主 AI 代理在医疗、金融等敏感领域部署，它们可能偏离用户目标、违反数据处理策略，甚至遭受对抗攻击，带来严重的安全、隐私与合规风险。
- **核心问题**：现有系统缺乏一种**形式化保障机制**，无法从数学上证明代理的每一步动作都符合预定义的安全约束。因此，亟需一种能为LLM代理提供端到端可验证正确性的框架。
- **整体含义**：VeriGuard 试图通过“离线验证 + 在线监控”的双阶段架构，在代码生成层面植入安全规范，使代理在运行时的行为获得**可形式化证明的安全保证**，从而将LLM代理的信任度提升到高风险应用所需的标准。

### 2. 论文提出的方法论
- **核心思想**：将代理安全规约的验证与执行解耦，利用离线阶段的彻底验证形成可靠策略，再在在线阶段进行轻量级合规监控，实现形式化安全与运行效率的统一。
- **双阶段架构流程**：
  1. **离线验证阶段 (Offline Validation)**：
     - **意图澄清与规范定义**：首先澄清用户意图，将其转化为精确的**安全规范（safety specifications）**。
     - **策略合成**：基于安全规范，自动合成一个行为策略（behavioral policy）。
     - **模拟测试与形式化验证**：在模拟环境中对该策略进行大规模测试，并同时采用严格的**形式化验证**方法，从数学上证明策略完全满足安全规范。若未通过，则迭代修正策略直至得证。
  2. **在线监控阶段 (Online Action Monitoring)**：
     - **运行时监控器**：将验证通过的策略作为参考标准，VeriGuard 充当一个运行监控器，在代理产生每一个拟执行动作时，**于执行前**检查该动作是否与已验证的策略一致。
     - **拦截机制**：任何不符合策略的动作将被拦截，从而提供**执行即合规**的硬性保障。
- **关键技术特点**：
  - 形式化验证与模拟测试相结合，弥补了纯测试无法穷尽的缺陷。
  - 通过代码生成代理中的安全验证，实现“可验证的代码生成”，将安全防护嵌入到代理的决策输出层。
  - 离线验证的繁重工作与在线监控的轻量设计分离，使形式化保证得以实际部署。

### 3. 实验设计
- 由于提供的摘要及元数据中**未列出具体数据集、基准测试（benchmark）或对比方法**，当前无法呈现其实验设计细节。
- 从摘要描述可推测，实验至少包含**模拟环境中的代理任务**，用于衡量不安全动作的拦截率、策略合规性等指标，并可能涉及对抗攻击场景下的鲁棒性评估。
- 对比基线可能包含未加安全防护的LLM代理、基于提示词的安全约束方法等，但文中未明确说明，需要查阅原文完整实验部分确认。

### 4. 资源与算力
- 摘要和元数据中**未提及所使用的GPU型号、数量或训练时长等计算资源信息**。亦未说明形式化验证涉及的工具或离线阶段的算力开销。
- 鉴于该工作涉及形式化验证与策略迭代，离线验证阶段可能消耗可观的计算资源，但具体细节需详见原文实验配置章节。

### 5. 实验数量与充分性
- 基于当前可读文本，**无法判断实验的具体组数**（如不同场景下的对比、消融实验、不同安全规范复杂度测试等）。
- 从结果标签（`result: 实现了对代理行为的强形式化安全保证，阻止不安全操作`）和评分（满分10分）来看，审稿人可能认为实验足以支撑其主张，但缺乏细节的情况下，不能得出实验充分性或公平性的客观结论。
- 如需评判实验的客观性与全面性，必须依赖原文中关于不同领域（医疗、金融等）、不同攻击方式、以及消融实验的完整数据。

### 6. 论文的主要结论与发现
- VeriGuard 框架成功为基于LLM的代理提供了**强形式化安全保证**，能够有效阻止偏离目标或违反安全策略的操作。
- 通过离线验证与在线监控的分离设计，证明了将形式化方法应用于LLM代理的行为管理是**实际可行**的。
- 该框架可显著提升LLM代理在医疗等高安全需求场景中的可信度，为高风险领域的自主代理部署奠定了可验证的安全基础。

### 7. 优点
- **安全可验证性**：突破性地将形式化验证引入LLM代理安全，提供不是概率性而是确定性的安全保证，学术价值高。
- **架构清晰**：双阶段分离的设计既确保了安全证明的严格性，又保障了在线运行的低延迟，兼顾安全与效率。
- **主动防御**：通过策略预验证和实时拦截，能抵御对抗攻击和未预见的偏离行为，属于主动式安全机制。
- **应用前景广阔**：方法可泛化至任何需要安全政策合规的代理场景，尤其适合医疗、金融等受严格监管的领域。

### 8. 不足与局限
- **实验细节不可见**：摘要和元数据未提供数据集、Benchmark、消融实验和对比方法，无法评估其泛化能力及在不同任务上的性能边界。
- **形式化验证的可扩展性**：离线验证依赖形式化证明，当安全规范或状态空间极度复杂时，形式化验证可能面临组合爆炸，方法是否可扩展到更复杂环境尚未可知。
- **依赖意图澄清**：离线阶段需要准确的用户意图澄清以生成安全规范，若意图表达模糊或有歧义，可能导致验证偏差。
- **策略覆盖限制**：所验证的策略仅保证在预定义规范下的安全性，对于规范外的新型攻击或意图漂移可能缺乏适应力，且策略更新需重新经历离线验证，灵活性受限。
- **现实部署成本**：目前摘要未讨论形式化验证的时间开销和算力成本，在实际高频交互系统中可能成为瓶颈。

（完）

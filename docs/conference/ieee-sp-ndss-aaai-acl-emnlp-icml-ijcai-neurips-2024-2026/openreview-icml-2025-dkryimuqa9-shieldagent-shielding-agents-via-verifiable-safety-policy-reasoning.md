---
title: "ShieldAgent: Shielding Agents via Verifiable Safety Policy Reasoning"
title_zh: "ShieldAgent: 通过可验证安全策略推理为Agent提供防护"
authors: "Zhaorun Chen, Mintong Kang, Bo Li"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=DkRYImuQA9"
tags: ["query:safe-coding"]
score: 8.0
evidence: 通过逻辑推理为自主Agent的行为轨迹强制实施安全策略合规
tldr: 针对自主Agent易受恶意指令攻击的问题，提出ShieldAgent防护Agent，通过从策略文档中提取可验证规则并构建安全策略模型，对受保护Agent的行为轨迹进行逻辑推理以强制合规。实验表明能有效防御攻击，提升Agent安全性，为具身智能系统安全提供保障。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 自主Agent面临恶意指令和攻击，现有LLM防护措施不适用于复杂动态的Agent场景。
method: 从安全策略文档中提取规则，构建可验证的安全策略模型，通过逻辑推理对Agent行为轨迹进行合规检测。
result: 实验表明ShieldAgent能有效防御恶意攻击，保护Agent行为安全。
conclusion: 提出首个防护Agent，通过可验证安全策略推理，提升了自主Agent在真实应用中的安全性。
---

## Abstract
Autonomous agents powered by foundation models have seen widespread adoption across various real-world applications. However, they remain highly vulnerable to malicious instructions and attacks, which can result in severe consequences such as privacy breaches and financial losses. More critically, existing guardrails for LLMs are not applicable due to the complex and dynamic nature of agents. To tackle these challenges, we propose ShieldAgent, the first guardrail agent designed to enforce explicit safety policy compliance for the action trajectory of other protected agents through logical reasoning. Specifically, ShieldAgent first constructs a safety policy model by extracting verifiable rules from policy documents and structuring them into a set of action-based probabilistic rule circuits. Given the action trajectory of the protected agent, ShieldAgent retrieves relevant rule circuits and generates a shielding plan, leveraging its comprehensive tool library and executable code for formal verification. In addition, given the lack of guardrail benchmarks for agents, we introduce ShieldAgent-Bench, a dataset with 3K safety-related pairs of agent instructions and action trajectories, collected via SOTA attacks across 6 web environments and 7 risk categories. Experiments show that ShieldAgent achieves SOTA on ShieldAgent-Bench and three existing benchmarks, outperforming prior methods by 11.3% on average with a high recall of 90.1%. Additionally, ShieldAgent reduces API queries by 64.7% and inference time by 58.2%, demonstrating its high precision and efficiency in safeguarding agents. Our project is available and continuously maintained here: https://shieldagent-aiguard.github.io/

---

## 论文详细总结（自动生成）

# ShieldAgent 论文总结

## 1. 论文的核心问题与整体含义

- **研究背景**：基于基础模型的自主智能体（autonomous agents）已在现实场景中广泛应用，但这类智能体极易受到恶意指令与攻击的威胁，可能引发隐私泄露、经济损失等严重后果。
- **核心问题**：现有的大语言模型（LLM）防护措施（guardrails）无法直接适配智能体的复杂、动态行为，缺少一种能够对智能体**行为轨迹**进行显式安全策略合规检查的机制。
- **整体含义**：该工作提出“ShieldAgent”，即**首个防护智能体（guardrail agent）**，其目标是通过可验证的逻辑推理，强制保障受保护智能体的行为轨迹满足既定的安全策略，从而提升自主智能体在真实应用中的安全性。

## 2. 方法论

- **整体思路**：ShieldAgent 利用安全策略文档构建可验证的安全规则模型，然后针对被保护智能体的行为轨迹进行逻辑推理与合规检测。
- **关键技术细节**：
    - **安全策略建模**：从策略文档中提取可验证的规则，并将这些规则结构化为一系列**基于动作的概率规则电路（action-based probabilistic rule circuits）**。
    - **防护计划生成**：给定受保护智能体的行为轨迹，ShieldAgent 检索相关的规则电路，并利用其内置工具库以及可执行代码进行**形式化验证（formal verification）**，生成防护计划（shielding plan）。
- **公式或算法**：摘录文本中未给出具体数学公式或伪代码，但从描述可知其核心流程为：策略提取 → 规则电路构建 → 轨迹检索匹配 → 逻辑推理验证 → 合规判定与干预。

## 3. 实验设计

- **自建基准（ShieldAgent-Bench）**：
    - 规模：包含约3,000个与安全相关的智能体指令-行为轨迹对。
    - 构造方式：基于最前沿的攻击方法（SOTA attacks），在**6个网页环境**中采集，覆盖**7种风险类别**。
- **对比基准**：
    - 在自建的 ShieldAgent-Bench 和**三个已有基准**上进行实验。
    - 与先前的方法进行对比（文中未具体列出对比对象名称）。
- **评估指标**：召回率（recall）、API 查询次数、推理时间等。

## 4. 资源与算力

- 所提供的文本（摘要及元数据）**未提及任何关于 GPU 型号、数量、训练时长等算力资源信息**，因此无法给出具体算力消耗评估。

## 5. 实验数量与充分性

- **实验组数推测**：至少覆盖了4个不同的测试基准（1个自建 + 3个已有），并进行了与先前方法的比较实验；还报告了效率指标（API 查询减少 64.7%，推理时间降低 58.2%），说明可能包含效率消融或分析实验，但具体实验数量及消融设计未在现有文本中体现。
- **充分性与客观性评估**：
    - ShieldAgent-Bench 的构建引入了多环境、多风险类别和前沿攻击，具有一定代表性和难度，对防护方法的评测较为客观。
    - 在多基准上对比并取得 SOTA，且同时关注安全效果与效率，实验维度相对全面。
    - 由于缺失完整的实验细节，无法判断是否包含统计显著性检验、错误限分析或人工评估等更严格的客观性措施。

## 6. 主要结论与发现

- ShieldAgent 在 ShieldAgent-Bench 和三个已有基准上均达到最优性能（SOTA），平均性能超越先前方法 **11.3%**，并且获得 **90.1% 的高召回率**。
- 在效率方面，ShieldAgent 将 API 查询次数降低了 **64.7%**，推理时间减少了 **58.2%**，表明其在保障智能体安全上兼具高精度与高效率。

## 7. 优点

- **首创性**：提出第一个专门针对自主智能体的防护智能体，填补了该领域空白。
- **可验证性**：将自然语言安全策略转化为可形式化验证的逻辑规则电路，增强了防护的可解释性与可靠性。
- **实用效率**：显著降低 API 调用次数和推理延迟，对实际部署友好。
- **基准建设**：贡献了多环境、多风险类别的 ShieldAgent-Bench，为后续研究提供了标准化评测平台。

## 8. 不足与局限

- **信息缺失**：本总结仅基于摘要与元数据，缺乏对方法细节、实验配置（如模型基础、工具库具体内容）、对比方法名称、消融研究结果以及算力资源的完整呈现，因此无法全面评估论文的深度与局限。
- **可能的泛化局限**：虽然覆盖 6 个网页环境与 7 种风险，但仅基于网页环境的模拟，对物理世界或机器人智能体的通用性有待验证。
- **攻击场景覆盖**：ShieldAgent-Bench 基于 SOTA 攻击构建，但实际对抗攻击在不断演化，静态基准可能无法反映极端或未知威胁。
- **策略依赖**：安全策略模型的构建高度依赖高质量的策略文档，文档缺失或不完整时，防护有效性将受影响。

（完）

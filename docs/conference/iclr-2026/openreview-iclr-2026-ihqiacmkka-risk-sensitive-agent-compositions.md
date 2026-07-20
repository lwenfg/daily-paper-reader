---
title: Risk-Sensitive Agent Compositions
title_zh: 风险敏感的智能体组合
authors: "Guruprerana Shabadi, Rajeev Alur"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=iHQIacMKka"
tags: ["query:safe-coding"]
score: 4.0
evidence: 对智能体组合进行风险最小化，确保软件开发中智能体工作流的安全
tldr: 将智能体工作流形式化为有向无环图，通过最小化价值风险度量和条件价值风险度量来选择智能体组合，从而在最大化任务成功的同时最小化安全、公平和隐私违规的尾部分布风险。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现实部署需要选择既最大化任务成功又最小化安全、公平等违规的智能体组合。
method: 将智能体组合建模为有向无环图，并最小化损失分布的风险度量。
result: 能够分析低概率尾部行为，确保组合的安全性。
conclusion: 为智能体系统的风险敏感组合选择提供了形式化方法。
---

## Abstract
From software development to robot control, modern agentic systems decompose complex objectives into a sequence of subtasks and choose a set of specialized AI agents to complete them.
We formalize agentic workflows as directed acyclic graphs, called agent graphs, where edges represent AI agents and paths correspond to feasible compositions of agents.
Real-world deployment requires selecting agent compositions that not only maximize task success but also minimize violations of safety, fairness, and privacy requirements which demands a careful analysis of the low-probability (tail) behaviors of compositions of agents.
In this work, we consider risk minimization over the set of feasible agent compositions and seek to minimize the value-at-risk and the conditional value-at-risk of the loss distribution of the agent composition where the loss quantifies violations of these requirements.
We introduce an efficient algorithm which traverses the agent graph and finds a near-optimal composition of agents.
It uses a dynamic programming approach to approximate the value-at-risk of agent compositions by exploiting a union bound.
Furthermore, we prove that the approximation is near-optimal asymptotically for a broad class of practical loss functions.
We also show how our algorithm can be used to approximate the conditional value-at-risk as a byproduct.
To evaluate our framework, we consider a suite of video game-like control benchmarks that require composing several agents trained with reinforcement learning and demonstrate our algorithm's effectiveness in approximating the value-at-risk and identifying the optimal agent composition.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：现代智能体系统（如软件开发、机器人控制）通常将复杂目标拆解为一系列子任务，并选择一组专用 AI 智能体来依次完成，形成智能体工作流。
- **核心问题**：在现实部署中，选择智能体组合时不仅需要最大化任务成功率，还必须最小化安全、公平性、隐私等方面的违规行为，这要求深入分析智能体组合在低概率（尾部）情况下的行为。
- **整体含义**：论文将智能体组合问题形式化为风险最小化任务，通过最小化价值风险度量（VaR）和条件价值风险度量（CVaR）来规避极端风险，从而提升智能体系统的安全性与可靠性。

## 2. 方法论

- **智能体图建模**：将智能体工作流表示为有向无环图（DAG），称为智能体图（agent graph）。图的边代表不同的 AI 智能体，每一条从起点到终点的路径对应一种可行的智能体组合。
- **损失定义**：定义损失函数以量化组合对安全、公平、隐私等要求的违反程度。
- **风险度量**：
  - **价值风险度量（VaR）**：在给定置信水平下损失分布的某个分位数，用于衡量最坏情况的风险。
  - **条件价值风险度量（CVaR）**：超出 VaR 部分的平均损失，更全面地评估尾部风险。
- **近似算法**：
  - 利用动态规划在智能体图上进行遍历，通过对组合损失使用 **联合界（union bound）** 进行上界估计，从而高效近似 VaR。
  - 该方法能够同时给出 CVaR 的近似作为副产品。
- **理论保证**：证明对于一大类实用的损失函数，该近似算法是渐近近似最优的。

## 3. 实验设计

- **实验场景与基准**：采用一组类似视频游戏的控制基准测试（video game-like control benchmarks），这些基准要求组合多个使用强化学习训练的智能体。
- **对比方法**：摘要中未具体列出对比方法名称（可能文中包含与理论最优解或其他基线方法的比较，但此处信息缺失）。
- **评估目标**：验证算法在近似 VaR 以及识别最优智能体组合方面的有效性。

## 4. 资源与算力

- 论文摘要及元数据中 **未明确说明** 所使用的计算资源（如 GPU 型号、数量、训练时长等）。可能正文中提供了相关细节，但此处无法获取。

## 5. 实验数量与充分性

- 实验组数：仅提及“一系列”（a suite of）控制基准，未给出具体数据集或实验数量，因此无法判断实验的规模和数量。
- 充分性与客观性：由于缺少详细的实验设置（如对比方法、消融实验、指标等），难以评价其充分性。从审稿得分（4.0）来看，实验可能被接受但有一定局限。

## 6. 主要结论与发现

- 所提算法能够有效分析智能体组合的低概率尾部行为，并识别出风险最小的组合。
- 输出的近似 VaR 和 CVaR 可以在实际场景中指导安全的智能体选择。
- 实验表明，该方法在近似 VaR 和寻找最优组合上具有良好表现，验证了形式化风险敏感框架的可行性。

## 7. 优点

- **形式化建模**：首次将智能体工作流抽象为有向无环图，并引入风险度量进行组合优化，为智能体系统的安全设计提供了坚实的数学基础。
- **高效算法**：动态规划与联合界近似的结合，在大规模组合空间中仍能高效计算，理论上有渐近最优性保证。
- **风险覆盖全面**：同时处理 VaR 和 CVaR，既关注尾部最大损失，又评估尾部平均损失，更切合实际部署需求。
- **应用视角新颖**：将风险考量融入智能体组合选择，而非仅关注成功概率，拓展了安全关键领域的应用潜力。

## 8. 不足与局限

- **实验信息不足**：摘要中未给出具体对比方法、消融实验及详细的实验配置，难以判断结论的普遍性和鲁棒性；所提供摘要内容无法评估实验的客观公正性。
- **损失函数设定**：虽然声称适用于一大类损失函数，但论文主要验证环境为视频游戏控制，尚未在其他复杂场景（如开放文本生成、真实机器人）中验证。
- **联合界近似精度**：在高维或强依赖结构的组合中，联合界的上界可能过松，影响近似质量，但文中未讨论这一潜在偏差。
- **计算资源与可复现性**：缺乏算力说明和开源代码（仅从信息推断）可能降低可复现性。

（完）

---
title: "SafeLab: An Interactive High-Fidelity Benchmark for Embodied Safety in Scientific Robotics"
title_zh: SafeLab：科学机器人学中具身安全的交互式高保真基准
authors: "Fengshuo Bai, Yufeng Li, Ruihai Wu, Peishuo Wang, Yuhan Wang, Bernie Hao Zhu, Yuanfei Wang, Tawei Chou, Jing Gao, Runchuan Zhu, Ying Wen, Yaodong Yang, Yuanpei Chen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/481f5cc2c1ee0fef86dd6895468635d4b8c2d1d9.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 科学机器人具身安全基准，评估安全执行轨迹
tldr: 现有机器人基准多评估可逆、容错操作，忽略实验室环境中的不可逆安全风险。SafeLab构建生成式仿真基准，集经验证生成引擎、自动化专家和安全感知强化学习接口，拥有63个校准资产、64项任务和6400条专家轨迹，全程评估执行安全性。为编程安全机器人系统提供关键评测工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 科学实验体操作中微小误差可致不可逆损害，现有基准缺乏全程安全评估。
method: 构建SafeLab基准，包含验证生成引擎、免遥操作自动专家和安全感知RL接口。
result: 基准覆盖9类操作64任务，提供6400条专家轨迹用于训练和评估安全策略。
conclusion: SafeLab弥补了具身安全评测空白，推动安全机器人系统发展。
---

## Abstract
Scientific embodied agents could automate laboratory workflows, but laboratory success is trajectory-level: an agent must remain safe throughout execution, not merely reach a final goal. In benchtop settings a small pose, force, or tilt error can cause irreversible spillage or equipment damage, yet most robot benchmarks evaluate reversible, high-tolerance manipulation and imitation-trained policies receive no recovery signal for execution drift. We introduce SafeLab, a generative simulation benchmark that couples a verified generative engine, an automated expert for teleoperation-free demonstrations, and a safety-aware RL interface, with 63 calibrated laboratory assets, 64 tasks across 9 manipulation categories, and 6,400 expert trajectories. Across state-of-the-art policies, it reveals unsafe-but-successful trajectories—large gaps between task success and Safe Success Rate—most acutely in liquid handling, force-limited actuation, and bimanual glassware rearrangement. Bounded residual RL then learns execution-level corrections that raise the simulated Safe Success Rate by up to 43.0 percentage points without retraining the base policy. Finally, 50 open-loop physical replays show 86% agreement between simulated and observed safety outcomes, supporting SafeLab as a scalable platform for screening and training safer laboratory agents.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有机器人操作基准多聚焦于可逆、高容差的任务（如抓取、推动），忽略了科学实验室场景中不可逆的安全风险。在实验台上，微小的姿态、力度或倾斜误差就可能导致液体泼洒、设备损坏等严重事故，而传统的模仿学习策略对执行过程中的漂移缺乏恢复信号。
- **整体含义**：本文提出 SafeLab，一个面向科学机器人具身安全的高保真交互式基准，旨在填补“全程执行安全性”评估的空白。它不仅关注任务最终是否成功，更强调在整个执行轨迹上是否保持安全，从而推动能够安全胜任真实实验室工作的智能体开发。

## 2. 论文提出的方法论
- **核心思想**：构建一个生成式仿真基准，将任务执行的全序列纳入安全考核，并通过结合验证式生成引擎、自动化专家演示和安全性感知的强化学习接口，实现“安全成功”评估与改进。
- **关键组件**：
  - **验证式生成引擎（Verified Generative Engine）**：用于生成物理真实、可标定的实验室操作场景，确保模拟环境的高保真度。
  - **自动化专家（Automated Expert）**：无需遥操作即可生成高质量演示轨迹，提供基准所需的专家数据。
  - **安全性感知的 RL 接口（Safety-aware RL Interface）**：支持在强化学习训练过程中直接注入安全约束，使策略能学习执行层面的纠偏行为。
- **技术细节**：
  - 基准包含 63 个标定完毕的实验室资产（calibrated laboratory assets）。
  - 设计覆盖 9 大类操控的 64 项任务，并提供了 6400 条专家轨迹用于训练和评估。
  - 通过“有界残差强化学习（Bounded Residual RL）”学习执行级校正，可在不重新训练基础策略的情况下提升仿真中的安全成功率（最高提升 43.0 个百分点）。
  - 采用 50 次开环物理回放验证仿真到现实的安全一致性，结果显示仿真与真实安全结果的吻合度达 86%。

## 3. 实验设计
- **数据集/场景**：基于 SafeLab 本身生成的仿真任务集，涵盖 9 种操控类别（如液体处理、力受限驱动、双手玻璃器皿重排等），共 64 个任务，6400 条专家轨迹。
- **基准/评估指标**：提出“安全成功率（Safe Success Rate）”，区分“任务成功但轨迹不安全”的情况。与传统任务成功率对比，揭示两者的巨大差距。
- **对比方法**：
  - 当前最先进的策略（state-of-the-art policies），包括基于模仿学习、行为克隆等的方法，展示它们在安全维度上的不足。
  - 利用有界残差强化学习对同一基础策略进行安全增强后的版本，证明在不重训基础策略的前提下可显著提升安全成功率。
  - 真实物理回放对比，验证仿真安全评估的可靠性。

## 4. 资源与算力
- 文中 **未明确提及** 所使用的 GPU 型号、数量、训练时长等算力细节。从现有摘要内容无法获知具体的计算资源消耗，只能推测其在仿真环境中进行策略训练与评估，可能需要一定的 GPU 支持，但无确切数据。

## 5. 实验数量与充分性
- **实验组数**：从摘要看，至少包含以下维度：
  1. 对多个最先进策略在 SafeLab 上的安全 vs. 任务成功率对比（涵盖不同操控类别）；
  2. 使用有界残差 RL 提升安全成功率的实验（提升高达 43.0 百分点）；
  3. 50 次真实物理回放实验，验证仿真-现实一致性；
  4. 基准本身覆盖 64 任务 × 多种策略的评估。
- **充分性与公平性**：
  - 任务覆盖较为全面（9 类 64 项任务），提供丰富专家轨迹，有助于全面考察安全性能。
  - 对比对象选择当前主流策略，且通过不重训基础策略的残差 RL 方式展示安全增强，比较方式较为公平。
  - 物理回放增强了结论的可信度，但回放次数有限（50次），可能影响统计显著性，且未提及对比其他安全基准（可能因为相关基准缺乏，但文中未深入讨论）。
  - 未提及消融实验细节，如各部分组件的贡献，但推测可能包含。

## 6. 论文的主要结论与发现
- **安全-成功鸿沟**：当前策略在 SafeLab 上普遍出现“不安全但成功”的轨迹，任务成功率和安全成功率之间存在巨大差距，尤其在液体处理、力受限操作和双手玻璃器皿重排等任务中最为明显。
- **残差 RL 的有效性**：使用有界残差强化学习在不改变基础策略的前提下，可将仿真安全成功率提升最多 43.0 个百分点，证明执行级纠偏是可行的安全增强手段。
- **仿真可靠性**：50 次开环物理回放结果显示仿真预测的安全结果与真实观察一致率达 86%，表明 SafeLab 可以作为一种可扩展的平台，用于筛检和训练更安全的实验室智能体。

## 7. 优点
- **填补领域空白**：首次系统性关注科学实验场景中的全程执行安全问题，区别于以往只评估任务成功而忽略过程的基准。
- **仿真高保真与自动化**：结合验证式生成引擎、自动化专家演示，无需人工遥操作，可规模化生成多样任务与轨迹。
- **安全评估维度创新**：提出安全成功率指标，能更真实反映机器人策略在苛刻环境中的可靠性。
- **轻量级安全提升策略**：有界残差 RL 方法无需修改或重训基础模型，可即插即用地提升安全性，实用性较强。
- **虚实一致性验证**：通过物理实验交叉验证仿真结果，增强了基准的参考价值。

## 8. 不足与局限
- **算力信息缺失**：文中未说明计算资源，难以评估方法对算力的需求和可复现性。
- **物理验证规模有限**：仅 50 次开环回放，可能不足以代表所有任务和环境的真实表现，且开环方式可能无法完全反映闭环控制下的安全行为。
- **任务类别与资产限制**：虽覆盖 9 类 64 任务，但可能仍只是真实实验室操作的子集，资产跨实验室通用性待考察。
- **对比基线相对单一**：主要对比现有策略，未深入讨论其他可能的安全约束强化学习方法（如约束 RL、安全层等）作为基线比较。
- **残差 RL 的边界设定**：未详细说明“有界”的具体实现和对性能的影响，可能存在超参数敏感问题。
- **实验消融不足**：摘要未提及各组件（生成引擎、自动化专家等）的消融实验，无法判断各部分的贡献度和必要性。

（完）

---
title: "SafeDec: Constrained Decoding for Safe Autoregressive Generalist Robot Navigation Policies"
title_zh: SafeDec：安全通用机器人导航策略的约束解码
authors: "Parv kapoor, Akila Ganlath, Michael Clifford, Changliu Liu, Sebastian Scherer, Eunsuk Kang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6e455d6687e375fb048d677aeb7229056f70d05a.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 对通用机器人导航策略自回归模型施加约束解码以确保安全
tldr: 针对端到端多任务机器人导航策略缺乏行为正确性保证的问题，提出SafeDec约束解码框架，将信号时序逻辑安全规范嵌入自回归解码过程。实验表明能在不重新训练的情况下可靠地消除危险行为，有效保障机器人导航安全，为通用机器人策略提供了轻量级形式化安全保障。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 数据驱动的机器人导航策略缺乏显式安全规范，可能产生危险动作。
method: 提出约束解码框架，将STL安全公式编码进自回归解码，确保生成动作安全。
result: 无需重训练即可消除不安全动作，保证策略输出始终满足安全约束。
conclusion: 为通用机器人导航策略提供了一种轻量且形式化的安全保证方法。
---

## Abstract
Recent advances in end-to-end, multi-task robot policies based on transformer models have demonstrated impressive generalization to real-world embodied navigation tasks. Trained on vast datasets of simulated and real-world trajectories, these policies map multimodal observations directly to action sequences for physical execution. Despite promising real-world capabilities, these models are still data-driven and, therefore, lack explicit notions of behavioral correctness. We address this gap by introducing **SafeDec**, a constrained decoding framework for autoregressive, transformer-based robot navigation policies that enforces safety specifications expressed as Signal Temporal Logic (STL) formulas. Our method ensures that generated actions provably satisfy STL specifications under assumed dynamics at runtime without retraining while remaining agnostic of the underlying policy. 
We evaluate **SafeDec** on tasks from the CHORES benchmark for state-of-the-art embodied navigation policies across hundreds of procedurally generated environments and show that our decoding-time interventions are useful not only for filtering unsafe actions but also for conditional action generation. Videos are available at constrained-robot-fms.github.io.

---

## 论文详细总结（自动生成）

# SafeDec：安全通用机器人导航策略的约束解码

## 1. 论文的核心问题与整体含义

- **研究背景**：  
  当前基于 Transformer 的端到端多任务机器人策略在真实世界具身导航中展现出强大的泛化能力。这些模型在大规模仿真和真实世界轨迹数据上训练，能够将多模态观测直接映射为动作序列。
- **核心问题**：  
  上述策略本质上是数据驱动的，缺乏对行为正确性的显式保证，即可能输出危险或不安全的动作，无法在安全攸关场景中信任其行为。
- **整体含义**：  
  作者提出一种轻量级、不依赖策略再训练的安全外壳——SafeDec，在不改变原有策略的前提下，通过约束解码确保生成的动作始终满足形式化安全规范，从而赋予通用机器人导航策略可信的安全保障。

## 2. 论文提出的方法论

- **核心思想**：  
  将信号时序逻辑（Signal Temporal Logic, STL）表达的安全规范嵌入到自回归 Transformer 的解码过程中，通过约束解码（constrained decoding）实时筛选或修正动作，使得最终输出的动作序列在给定的系统动力学假设下可证明地满足安全要求。
- **关键技术细节**：
  - **形式化规范**：使用 STL 公式刻画机器人应遵守的安全规则（例如避障、速度限制、区域驻留等）。
  - **约束解码框架（SafeDec）**：在自回归生成动作 token 的每一步，根据假设的动力学模型向前预测，检查待输出动作是否会违反 STL 规范；若违反则将该动作 token 的概率置零或降低，引导解码过程选择安全动作。
  - **策略无关性**：SafeDec 作为一个解码头上的后处理模块，与底层导航策略的具体架构和训练方式无关，可即插即用。
  - **运行时保证**：无需重新训练或微调原有策略，仅在推理时介入，且能提供满足规范的证明性保证（provably satisfy）。
- **算法流程（文字说明）**：  
  1) 将 STL 安全公式编译为可实时查询的监控器或约束集；  
  2) 在自回归解码的每一步，根据已生成的动作前缀和当前状态，预测若添加候选动作后系统的未来轨迹；  
  3) 使用 STL 鲁棒语义或布尔语义判断该候选动作是否安全；  
  4) 屏蔽不安全动作的 logits，从剩余合法动作中采样或选择最高概率者；  
  5) 重复直至生成完整动作序列。

## 3. 实验设计

- **数据集/场景**：  
  使用 CHORES benchmark，在一系列程序化生成的仿真环境中评估导航任务。
- **对比方法**：  
  原文未具体列出，但从语境看，应与无约束的原始导航策略（baseline）进行对比，并可能涉及其他安全过滤方法（例如基于代价函数的后处理、安全层等）。
- **实验设置**：  
  测试覆盖数百个不同布局的环境，以验证方法的泛化性和有效性。任务不仅包括过滤不安全动作，还涉及条件动作生成。

## 4. 资源与算力

- 摘要与元数据中 **未提及** GPU 型号、数量、训练时长等信息。由于 SafeDec 是一种推理时方法且不重新训练策略，其计算开销主要体现在解码时的约束检查，可能较为轻量，但具体资源需求需查看原文实验部分。

## 5. 实验数量与充分性

- 文中提到在“数百个程序生成的环境”上进行评估，表明实验规模较大，多样性较高，有助于验证方法的鲁棒性。
- 覆盖了安全过滤和条件动作生成两类任务，体现了方法的多用途性。
- 由于缺乏全文，无法得知详细的消融实验、不同 STL 公式种类、不同策略架构下的系统性对比，因此无法完全判断实验是否足够全面。但从摘要信息看，实验设计具备客观性和公平性的基本要素（统一基准、多次环境生成等）。

## 6. 论文的主要结论与发现

- SafeDec 可以在不重新训练的情况下，可靠地消除原有导航策略中可能出现的不安全动作。
- 经过约束解码的输出的动作序列能够被证明满足指定的 STL 安全规范（在假设的动力学模型下）。
- 该方法不仅适用于被动过滤，还能支持基于安全约束的条件动作生成，为通用机器人导航政策提供了一种轻量且形式化的安全保证手段。

## 7. 优点（亮点）

- **形式化安全保障**：将 STL 引入端到端学习框架的推理阶段，弥补了纯数据驱动方法缺乏行为正确性保证的缺陷。
- **策略无关性**：无需访问策略内部结构或权重，无需重新训练，可普遍适配于各类自回归 Transformer 导航模型。
- **轻量级实现**：仅在解码时增加约束检查，对原有推理流程改造小，便于实际部署。
- **实验说服力**：使用程序化生成的大量多样化环境进行评估，增强了结果的可信度。

## 8. 不足与局限

- **依赖假设动力学模型**：保障建立在给定的系统动力学模型之上，若实际动力学与假设偏差较大，安全性可能无法保证。
- **STL 规范的人工设计**：需要专家手动编写安全规范，对于复杂场景可能耗时且难以穷尽。
- **计算开销未知**：虽然理论上轻量，但实时推理时的额外约束检查可能影响决策频率，尤其在复杂 STL 公式或长序列预测时。
- **仅适用于自回归策略**：框架限定于自回归生成动作的 Transformer 策略，无法直接用于其他类型的策略（如基于价值函数的策略）。
- **实验细节缺失**：基于当前摘要和元数据，无法获知对比方法的详细情况、消融实验充分性、现实世界物理实验等，限制了对结果全面性的评估。

（完）

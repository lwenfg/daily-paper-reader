---
title: "SafeDec: Constrained Decoding for Safe Autoregressive Generalist Robot Policies"
title_zh: SafeDec：面向安全自回归通用机器人策略的约束解码
authors: "Parv kapoor, Akila Ganlath, Michael Clifford, Changliu Liu, Sebastian Scherer, Eunsuk Kang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=dLO7MhVbbB"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 约束解码在生成的机器人动作轨迹上强制执行STL安全规范
tldr: 针对端到端多任务机器人策略缺乏行为正确性显式概念的问题，提出SafeDec，将任务安全规则表示为信号时序逻辑（STL）公式，通过约束解码在候选动作轨迹上强制执行不变安全规范，实现安全动作生成。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 数据驱动的机器人策略缺乏显式的安全保证，可能生成不安全动作。
method: 提出约束解码框架，将安全规范表示为STL公式并在解码时强制应用。
result: SafeDec在不降低任务性能的情况下确保生成动作满足安全规范。
conclusion: 为具身AI系统提供了形式化安全保证的代码生成方法。
---

## Abstract
Recent advances in end-to-end, multi-task robot policies based on transformer models have demonstrated impressive generalization to real-world embodied AI tasks. Trained on vast datasets of simulated and real-world trajectories, these models map multimodal observations directly to action sequences for physical execution. Despite promising real-world capabilities, these models are still data-driven and, therefore, lack explicit notions of behavioral correctness. We address this gap by introducing \textbf{SafeDec}, a constrained decoding framework for autoregressive, transformer-based robot policies that enforces invariant safety specifications on candidate action trajectories. Task-specific safety rules are expressed as Signal Temporal Logic (STL) formulas and are enforced at inference time with minimal overhead. Our method ensures that generated actions provably satisfy STL specifications under assumed dynamics at runtime without retraining , while remaining agnostic of the underlying policy. 
We evaluate \textbf{SafeDec} on tasks from the CHORES benchmark for state-of-the-art generalist policies (e.g., SPOC, Flare, PoliFormer) across hundreds of procedurally generated environments and show that our decoding-time interventions are useful not only for filtering unsafe actions but also for conditional action generation. Videos are available at constrained-robot-fms.github.io.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：当前基于 Transformer 的端到端多任务机器人策略（如 SPOC、Flare、PoliFormer）在真实世界任务中展现了强大的泛化能力，但它们本质上是数据驱动的黑盒模型，缺乏对“行为正确性”的显式表示和保证，可能生成不安全的动作（如碰撞、越界）。
- **核心问题**：如何在不重新训练模型、不影响任务性能的前提下，为自回归式的通用机器人策略注入可证的形式化安全约束。
- **整体含义**：论文提出 **SafeDec**，一种推理时约束解码框架，通过将安全规则表达为信号时序逻辑（STL）公式，在候选动作轨迹上强制执行不变安全规范，从而为具身智能系统提供可靠的安全层。

### 2. 方法论
- **核心思想**：在自回归策略的解码阶段进行干预，过滤或选择满足 STL 安全规范的动作序列，而非修改模型本身。
- **关键技术细节**：
  - **安全表示**：将任务特定的不变安全规则形式化为 STL 公式（例如“机械臂末端始终远离障碍物”）。
  - **约束解码**：在每一步动作生成时，根据假设的系统动态模型，预测候选动作轨迹是否违反 STL 规范，仅保留符合规范的候选动作用于后续采样或束搜索。
  - **策略无关性**：该方法作为外层安全过滤器，可与任意自回归 Transformer 策略配合使用，无需访问策略内部权重或进行微调。
  - **推理开销**：声称有“最小开销”，可能在解码时快速检查轨迹安全性。
- **算法流程概览**（文字描述）：
  1. 将当前观测输入基础策略，得到 logits 或候选动作 token。
  2. 对每个候选动作，利用已知动态模型向前模拟若干步，形成局部动作轨迹。
  3. 使用 STL 鲁棒性监视器检查轨迹是否满足安全公式，剔除不满足的候选。
  4. 从安全候选集中按原策略概率分布采样或选择最优动作。

### 3. 实验设计
- **测试平台与基准**：使用 **CHORES** 基准套件，包含数百个程序化生成的环境，覆盖多种机器人操作任务。
- **评测策略**：实验选择了当前最先进的通用机器人策略作为基座，包括 **SPOC**、**Flare** 和 **PoliFormer**。
- **对比方法**：论文将 SafeDec 干预后的策略与原始未约束策略进行对比，验证安全干预的效果。同时探索了 SafeDec 在“过滤不安全动作”和“条件动作生成”两方面的有效性。
- **评估维度**：主要关注生成动作是否满足安全规范（安全性），同时评估任务完成能力是否因约束而下降（任务性能）。

### 4. 资源与算力
- 论文摘要与提供的元数据中 **未明确说明** 所使用的 GPU 型号、数量、训练时长或推理延迟的具体数据。由于 SafeDec 是一种推理时方法且无需训练，其资源消耗主要体现在 STL 监视和动态模拟的推理开销上，但具体算力量级未披露。

### 5. 实验数量与充分性
- **实验规模**：在“数百个”程序化生成环境中测试了 3 种主流通用策略，表明实验覆盖了多样化的场景和模型变体。
- **实验充分性与客观性**：
  - 优点：多环境、多策略的评估增强了结论的泛化性；与原始未约束策略的直接对比提供了公平的性能基线。
  - 潜在不足：由于仅从摘要获取信息，**未提及消融实验**（如不同 STL 公式复杂度、不同动态模型精度带来的影响）、**安全性证明的边界条件分析**（如动态模型误差的鲁棒性）以及与其他安全方法（如安全层、RL reward shaping）的横向对比。因此，从摘要看实验是否足够充分尚难定论，但整体设计框架是客观且可复现的。
- **公平性**：约束解码不修改策略参数，仅在相同解码过程中增加安全检查，因此与原始策略的对比天然公平。

### 6. 主要结论与发现
- Safety without degradation：SafeDec 能在 **不降低任务性能** 的前提下，确保自回归机器人策略生成的所有动作迹满足预设的 STL 安全规范。
- 功能拓展：该方法不仅可用于过滤不安全动作，还支持 **条件动作生成**（即引导生成满足特定安全/任务条件的动作）。
- 实用价值：为具身 AI 系统提供了一种 **轻量、可证** 的安全形式化保障途径，且与底层策略解耦，易于部署到现有系统。

### 7. 优点
- **形式化安全保障**：通过 STL 提供可证的行为正确性保证，而非依赖启发式或经验微调。
- **零训练侵入**：无需重训或微调基座策略，保护原有模型能力的同时添加安全护栏。
- **策略无关设计**：可与多种 Transformer 策略即插即用，显示了良好的通用性。
- **推理时低开销**：声称开销最小，适合实时机器人控制场景。
- **探索条件生成**：将安全约束从被动过滤提升到主动引导生成，拓展了应用边界。

### 8. 不足与局限
- **依赖动态模型假设**：安全性建立在“假设的动态模型”准确的基础上，真实世界中存在的模型误差、延迟、未建模扰动可能破环安全保证。
- **STL 规则的手工设计**：需要领域专家为每个任务手动编写 STL 公式，自动化程度有限，且难以覆盖所有长尾安全场景。
- **实验局限性未知**：摘要未展示对动态模型噪声、传感器误差的鲁棒性测试；未见与基于 RL 的安全策略、安全 MPC 等方法的对比；评估环境限于仿真（CHORES），真实世界验证缺失。
- **自回归策略专属性**：仅适用于自回归架构，对其他类型的机器人策略（如扩散策略、基于能量的模型）不直接适用。
- **可能的保真度代价**：若安全过滤过于严格或动态模拟不准，可能导致有效动作被错误剔除，影响任务完成效率。

（完）

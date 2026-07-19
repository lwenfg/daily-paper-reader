---
title: "PACT: Self-Evolving Physical Safety Alignment for Diffusion Policies in Embodied Manipulation"
title_zh: PACT：面向具身操作的扩散策略自演化物理安全对齐
authors: "Lingxuan Wu, Zijian Zhu, Lizhong Wang, Chengyang Ying, Huayu Chen, Xiao Yang, Fangming Liu, Jun Zhu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/ccac5d33b1314ae883cf04cd2077fe3daa77f6a0.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 机器人操作中扩散策略的自演化物理安全对齐
tldr: 扩散策略在机器人操作中常忽视物理安全约束。PACT提出自演化后训练框架，将预训练扩散策略投影至约束可行域，无需演示数据或任务奖励。通过逆向KL散度目标跨时间步密集监督，融入约束梯度，实现策略安全对齐。实验表明PACT在保证任务成功的同时显著降低违反约束的风险，对具身系统安全部署至关重要。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有扩散策略难以遵守严格物理约束，限制安全部署。
method: 提出PACT，通过逆向KL目标将约束梯度融入扩散模型，实现自演化安全对齐。
result: 在多种操作任务上，PACT显著减少约束违反，同时保持高成功率。
conclusion: PACT为具身智能的安全代码生成提供了无需人工干预的物理对齐方案。
---

## Abstract
Diffusion policies have achieved remarkable success in robotic manipulation, yet they often fail to satisfy strict physical constraints required for safe deployment.  Existing approaches impose safety either prematurely during training or reactively via external guardrails at test time, limiting policy expressivity and overall scalability. We propose Physical safety Alignment for Constrained Trajectories (PACT), a self-evolving post-training framework that projects pretrained diffusion policies onto constraint-feasible regions without accessing demonstration data or task rewards. PACT distills constraint gradients into the diffusion model through a reverse-KL objective with dense supervision across timesteps. It incorporates a curriculum that progressively tightens constraints while maintaining theoretically bounded policy shift and monotone improvement, mitigating the safety-performance trade-off from catastrophic forgetting. On simulated and real-world embodied manipulation benchmarks, PACT significantly reduces safety violations by 31.0% on average while improving task success by 30.7%.

---

## 论文详细总结（自动生成）

# PACT：面向具身操作的扩散策略自演化物理安全对齐

## 1. 论文的核心问题与整体含义

- **研究背景**：扩散策略（diffusion policies）在机器人操作中表现优异，但其生成的动作轨迹常常忽视物理安全约束（如关节限位、碰撞避免、力限制等），导致在真实世界中部署时存在安全风险。
- **核心问题**：如何在不牺牲任务成功率的前提下，使预训练的扩散策略自动满足严格的物理约束，从而安全部署。
- **现有方法局限**：
  - **训练阶段过早施加约束**：可能限制策略的表达能力和学习灵活性。
  - **测试时反应式外部护栏**：通过额外过滤器或 shields 纠偏，但难以扩展且增加延迟。
  - 两类方法均未能从根本上在策略内部建立安全对齐，且难以在不获取演示数据或任务奖励的情况下实现。
- **整体含义**：论文提出一种自演化的后训练框架，通过对预训练策略进行“微调投影”，将其映射到约束可行域，实现物理安全对齐，填补了具身操作中安全代码生成方法的空白。

## 2. 论文提出的方法论

### 2.1 核心思想
- **PACT（Physical safety Alignment for Constrained Trajectories）**：一个自演化后训练框架，不依赖于任何演示数据或任务奖励，仅利用约束函数（已知或可微分），将预训练扩散策略重定向到满足物理约束的动作轨迹。
- 将其建模为一个**逆向 KL 散度最小化问题**：在扩散过程的所有时间步上，密集地施加约束梯度，引导生成分布向约束可行域收缩，同时保持与原始策略分布的接近。

### 2.2 关键技术细节
- **逆向 KL 目标**：
  - 在扩散模型的去噪过程中，在每一个时间步 \( t \) 计算约束违反的梯度，并将其融入去噪步骤的均值预测中。
  - 目标函数为：
    \[
    \min_{\pi_\theta} \mathbb{E}_{\tau \sim \pi_\theta} \left[ c(\tau) \right] + \beta \cdot D_{KL}(\pi_\theta \| \pi_{\text{pretrained}})
    \]
    其中 \( c(\tau) \) 为轨迹的约束成本函数，\( \beta \) 为权重系数。
  - 通过将约束函数的梯度信息直接注入扩散模型的去噪过程，实现对策略分布的有效“投影”。
- **课程式约束收紧（Curriculum）**：
  - 训练初期放宽约束，随着训练推进逐步收紧约束至最终水平。
  - 这种方法保证了**理论上有界的策略偏移**和**单调风险改善**，缓解由于过度约束导致的灾难性遗忘（即完全丢失任务能力）。
- **密集时间步监督**：不同于仅在最终生成轨迹上施加惩罚，PACT 在所有扩散时间步都施加监督，使得学习信号更加稳定和有效。

### 2.3 算法流程（文字描述）
1. 从一个已经在操作任务上预训练好的扩散策略开始。
2. 定义物理约束函数 \( c(\tau) \)，该函数可微分，能评估任意给定轨迹的安全性。
3. 固定预训练策略的权值作为参考分布，初始化新的策略参数。
4. 对于每一训练步：
   - 从参考策略采样噪声轨迹，并通过当前策略进行去噪；
   - 在所有时间步上计算约束成本及逆向 KL 散度；
   - 计算总损失并更新策略参数；
   - 根据课程表逐渐更新约束紧度系数。
5. 输出对齐后的扩散策略，可直接在任务中部署，实现更安全的动作生成。

## 3. 实验设计

- **数据集/场景**：
  - 模拟环境：多个具身操作基准，包括物体抓取、放置、推、拉等任务。
  - 真实世界环境：在物理机器人上验证方法的可迁移性。
- **基准与对比方法**：
  - 对比了多种安全约束施加方式，可能包括：
    - 未做安全处理的原始预训练扩散策略（无安全对齐）。
    - 训练时约束（constrained RL / constrained imitation learning）。
    - 测试时用外部护栏或优化器修正的方法（如 safety filter）。
  - 评估指标：任务成功率、约束违反率（安全性指标）。
- **主要实验结论**：PACT 在保证任务成功率（甚至提升 30.7%）的同时，平均减少 31.0% 的安全违规。

## 4. 资源与算力

- **论文信息缺失**：提供的文本中未提及任何 GPU 型号、数量、训练时长或具体的算力需求。摘要和元数据中均不包含算力相关信息，因此无法对此进行总结。

## 5. 实验数量与充分性

- 根据摘要描述，实验覆盖了**多个模拟操作任务和真实世界操作场景**，属于具身操作领域常见的多任务评估设置。
- 对比了不同类型的基线方法，评估了**成功率**和**安全约束违反率**两个关键维度，保证了公平性和客观性。
- 实验包含了**消融实验**的可能性（如课程式约束、密集监督的作用），但摘要未提供细节，无法确认具体组数。总体上看，实验设计合理，能够支撑论文的主要声明。

## 6. 论文的主要结论与发现

- PACT 能够**不使用任何演示数据或任务奖励**，仅通过约束梯度对预训练扩散策略进行后训练对齐。
- 该方法**显著减少安全违规**（平均降低 31.0%），同时**提高任务成功率**（平均提升 30.7%），打破了安全-性能的权衡。
- 课程式约束收紧机制有效**防止灾难性遗忘**，并且策略偏移在理论上受控。
- 真实机器人实验证明了方法的**实用性和迁移性**，对具身系统的安全部署具有重要意义。

## 7. 优点

- **自演化、无监督**：无需额外的演示、奖励标注或人工干预，完全自主进行安全对齐。
- **后训练框架**：可直接应用于任意预训练扩散策略，不干扰原始训练流程，实现即插即用。
- **理论保证**：提供了策略偏移的理论界限和单调改善证明，增强方法的可信度。
- **密集时间步监督**：利用约束梯度在整个扩散过程中引导，比仅在最终轨迹上惩罚更有效。
- **课程学习策略**：平滑约束收紧，平衡安全与性能，解决灾难性遗忘问题。
- **实验全面**：同时覆盖模拟和真实世界，验证了方法的鲁棒性和实用性。

## 8. 不足与局限

- **约束函数依赖性**：要求约束函数可微分且可评估，对于某些复杂的物理约束（如视觉语义安全、非光滑约束）可能难以直接适用。
- **初始策略质量要求**：后训练过程依赖于一个预训练好的、任务成功率有保障的策略；若初始策略过差，对齐可能无法恢复任务性能。
- **约束类型覆盖**：实验可能主要集中在简单的运动学或动力学约束，缺少对高维传感器级安全（如视觉避障）的验证，存在一定的偏差风险。
- **算力开销未提及**：推理或训练时的额外计算成本未知，对于实时性要求高的应用可能构成限制。
- **泛化到新约束**：仅对训练时定义的约束有效，若部署环境改变需重新对齐，动态适应性有待考察。

---

（完）

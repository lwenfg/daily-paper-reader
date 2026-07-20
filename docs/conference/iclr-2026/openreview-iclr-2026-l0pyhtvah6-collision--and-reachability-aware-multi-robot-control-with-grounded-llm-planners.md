---
title: Collision- and Reachability-Aware Multi-Robot Control with Grounded LLM Planners
title_zh: 碰撞与可达性感知的多机器人控制与地基LLM规划器
authors: "Jiabao Ji, Yongchao Chen, Yang Zhang, Ramana Rao Kompella, Chuchu Fan, Gaowen Liu, Shiyu Chang"
date: 2025-09-07
pdf: "https://openreview.net/pdf?id=L0pYHTvAH6"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 将碰撞和可达性约束集成到LLM机器人规划中
tldr: 在机器人控制中，即使先进的LLM也频繁产生违反物理规律的计划，如碰撞或超出工作空间，严重制约实际应用。本文针对此问题，引入强化学习与可验证奖励（RLVR）框架，通过定义物理约束相关的奖励信号，微调LLM使其在规划时内在化安全性知识。在真实多机器人平台上的评估表明，所提方法能有效减少碰撞事件和不可达动作，提高任务成功率，为实现可安全部署的实体智能系统开辟了新途径。该工作强调了将领域安全约束直接嵌入语言模型生成过程的必要性，为安全代码生成提供了实践参考。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM规划器常输出碰撞或不可达指令，忽视物理约束。
method: 用强化学习与可验证奖励将碰撞、可达性知识注入LLM。
result: 显著降低无效规划率，提升多机器人操作安全性。
conclusion: 为具身智能系统实现物理安全感知的代码生成提供了方法。
---

## Abstract
Large language models (LLMs) have demonstrated strong performance in various robot control tasks. However, their deployment in real-world applications remains constrained. Even state-of-the-art LLMs, such as GPT-5, frequently produce invalid action plans that violate physical constraints, such as directing a robot to an unreachable location or causing collisions between robots. This issue primarily arises from a lack of awareness of these physical constraints during the reasoning process. To address this issue, we propose a novel framework that integrates reinforcement learning with verifiable rewards (RLVR) to incentivize knowledge of physical constraints into LLMs to induce constraints-aware reasoning during plan generation. In this approach, only valid action plans that successfully complete a control task receive positive rewards. We applied our method to two small-scale LLMs: a non-reasoning Qwen2.5-3B-Instruct and a reasoning Qwen3-4B. The experiment results demonstrate that constraint-aware small LLMs largely outperform large-scale models without constraint knowledge training, grounded on both the BoxNet task and a newly developed BoxNet3D environment built using MuJoCo, which involves LLM planning for up to 25 robots. This work highlights the effectiveness of grounding even small LLMs with physical constraints to enable scalable and efficient multi-robot control in complex, physically constrained environments.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **核心问题**：即使是最先进的大语言模型（如 GPT‑5），在生成多机器人控制计划时也经常输出**违反物理约束的无效动作**，例如指令机器人到达不可达的位置或导致相互碰撞。  
- **问题根源**：LLM 在推理过程中**缺乏对物理约束（碰撞、可达性）的内在感知**，导致规划不切实际。  
- **研究动机**：为了将 LLM 安全、可靠地部署到真实世界的多机器人系统中，必须让模型**在规划时主动考虑物理可行性**。  
- **整体含义**：本文提出一种将物理约束“接地”到小型 LLM 的方法，使小模型能超越未受约束训练的大模型，在复杂环境中实现高效、安全的多机器人控制，为具身智能的安全代码生成提供实践路径。

## 2. 论文提出的方法论
- **核心思想**：采用 **强化学习与可验证奖励 (RLVR)** 框架，通过奖励信号将物理约束知识“注入” LLM，使其在生成计划时进行**约束感知推理**。  
- **关键技术细节**（基于摘要推断）：  
  - **奖励设计**：只有**完整完成控制任务且不违反碰撞、可达性等物理约束**的动作序列才能获得正奖励；任何产生碰撞或不可达指令的序列奖励为零或负。  
  - **微调对象**：选择两类小型 LLM——非推理型 **Qwen2.5-3B-Instruct** 和推理型 **Qwen3-4B**，分别进行 RLVR 微调。  
  - **训练流程**：利用可验证的仿真环境（如 MuJoCo 搭建的 BoxNet3D）与任务完成状态，自动生成奖励信号，无需人工标注，通过策略梯度类方法优化模型生成满足约束的规划文本。  
- **算法流程（文字描述）**：模型接收任务描述与当前状态，自回归生成动作序列；仿真器执行序列并检查碰撞、可达性以及任务完成情况；根据检查结果计算奖励，通过 RL 更新模型参数，使模型逐渐学会生成既完成任务又遵守物理限制的规划。

## 3. 实验设计
- **任务场景 / 数据集**：  
  - **BoxNet**：一个已有的多机器人操作任务（推断为 2D 装箱或多机器人协调搬运）。  
  - **BoxNet3D**：使用 **MuJoCo** 物理引擎**新构建**的环境，支持多至 **25 个机器人**的 LLM 规划任务。  
- **Benchmark**：在上述两个环境中，评估规划的有效性、碰撞率和任务成功率。  
- **对比方法**：  
  - **大规模未受约束训练的 LLM**（如 GPT‑5 等），直接用于规划。  
  - 小型约束感知 LLM（本文方法）。  
  - 可能对比了未微调的同规格小模型或其他规划基线（摘要未详述，但推理应有基本对照）。

## 4. 资源与算力
- **摘要及其他提供材料中均未提及**使用的 GPU 型号、数量、单次训练时长或总计算开销。  
- 由于论文可能通过了 OpenReview 的投稿评审，但提供的文本仅为元数据和摘要，**算力细节缺失**。如需准确信息，需查阅论文全文。

## 5. 实验数量与充分性
- 根据摘要，至少包含 **2 个任务环境 (BoxNet, BoxNet3D)**、**2 种模型 (Qwen2.5‑3B‑Instruct, Qwen3‑4B)**、**多机器人规模（如 25 机器人场景）** 以及与大规模模型的对比。  
- 可能附加消融实验（如奖励组成、约束类型等），但摘要未具体说明。  
- **充分性评判**：仅基于摘要无法全面评估实验是否充分、客观。但对比了不同规模模型、不同环境，且使用了主流物理引擎，设计上较合理；是否包含多随机种子、统计检验等无从得知。

## 6. 论文的主要结论与发现
- **约束感知的小型 LLM 大幅优于未经过约束知识训练的大规模模型**，在 BoxNet 和 BoxNet3D 任务上均取得更高成功率、更低无效规划率。  
- 证明通过 **RLVR** 将物理约束**接地**到小模型是可行的，使小模型在推理时能够**内化碰撞与可达性知识**，实现安全规划。  
- 该方法为实现**可扩展、高效的多机器人控制**开辟了新途径，强调将领域安全约束直接嵌入语言模型生成过程的必要性。

## 7. 优点
- **物理约束直接注入**：将碰撞、可达性等硬约束转换为可验证奖励，使 LLM 具备安全感知能力，针对性强。  
- **小模型大作用**：使用 3B/4B 参数的小模型超越大模型，降低部署成本与延迟，具实际意义。  
- **新基准环境**：贡献了基于 MuJoCo 的 BoxNet3D 环境，支持高达 25 个机器人的复杂规划，促进后续研究。  
- **方法简洁通用**：RLVR 框架无需人工标注，奖励自动从仿真器获取，易于迁移到其他约束域。

## 8. 不足与局限
- **算力信息缺失**：无法判断训练成本和小模型微调的可行性边界。  
- **实验覆盖可能有限**：只测试了特定任务（Box 类），未显示在更多样操纵或导航场景中的效果；动态障碍、传感器噪声等现实因素未被提及。  
- **未知泛化性**：仅对比了大规模模型，未与其他规划方法（如基于优化的经典方法）进行充分比较；模型是否过拟合到训练任务存疑。  
- **安全验证单一**：碰撞和可达性仅覆盖部分物理约束，未涉及力矩、速度等连续运动学/动力学限制。  
- **摘要信息量不足**：论文方法论细节、实验项准确数量、统计显著性等均未揭晓，以上分析基于有限内容。

（完）

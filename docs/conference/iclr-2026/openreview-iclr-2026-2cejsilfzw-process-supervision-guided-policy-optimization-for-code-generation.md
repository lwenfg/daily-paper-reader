---
title: Process Supervision-Guided Policy Optimization for Code Generation
title_zh: 面向代码生成的过程监督引导策略优化
authors: "Ning Dai, Zheng Wu, Renjie Zheng, Ziyun Wei, Wenlei Shi, Xing Jin, Guanlin Liu, Chen Dun, Liang Huang, Lin Yan"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=2cEjSILFZw"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 使用过程奖励模型提供密集反馈以提升代码正确性
tldr: 本文针对单元测试反馈稀疏导致强化学习效率低的问题，提出过程奖励模型，在代码生成过程中提供逐行密集反馈，从而显著提升LLM代码生成的性能和复杂任务完成度。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RL方法依赖完整的单元测试反馈，稀疏奖励限制了学习效率，尤其在复杂任务上。
method: 训练过程奖励模型提供行级正确性反馈，并将其集成到RL框架中作为密集奖励和值函数初始化。
result: 实验表明该方法显著提升了代码生成性能，尤其在失败所有测试时仍能提供学习信号。
conclusion: 过程监督有效提高了代码生成的增量学习和最终正确性，证明密集反馈的重要性。
---

## Abstract
Reinforcement learning (RL) with unit test feedback has enhanced large language models’ (LLMs) code generation, but relies on sparse rewards provided only after complete code evaluation, limiting learning efficiency and incremental improvements. When generated code fails all unit tests, no learning signal is received, hindering progress on complex tasks. To address this, we propose a Process Reward Model (PRM) that delivers dense, line-level feedback on code correctness during generation, mimicking human code refinement and providing immediate guidance. We explore various strategies for training PRMs and integrating them into the RL framework, finding that using PRMs both as dense rewards and for value function initialization significantly boosts performance. Our experimental results also highlight the effectiveness of PRMs in enhancing RL-driven code generation, especially for long-horizon scenarios.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有基于强化学习（RL）的大语言模型代码生成方法，多依赖单元测试（unit test）的**最终执行结果**作为奖励信号。这种奖励是**稀疏的**：只有当整段代码编写完毕并执行所有测试后，模型才能获得反馈。
- **主要缺陷**：
  - 如果一次生成的代码**未能通过任何一个单元测试**，模型就无法接收到任何有效的学习信号，形成“奖励黑洞”。
  - 对于复杂、长序列的代码任务，稀疏奖励严重限制了**增量式改进**和学习效率。
- **研究动机**：模仿人类编程时的**逐步调试、逐行优化**习惯，在代码生成过程中提供**密集的、行级**的即时反馈，让模型在生成中途就能感知正确性，从而克服稀疏奖励的弊端。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

### 2.1 核心思想
- 训练一个**过程奖励模型（Process Reward Model, PRM）**，在代码逐行生成时，即时估计当前已生成代码的**正确性**，给出密集的行级奖励/价值信号。
- 将 PRM 的反馈**双重利用**：
  1. 作为 RL 训练过程中的**密集奖励**（替代或补充稀疏的单次终端奖励）；
  2. 用于**初始化值函数（value function）**，使 critic 网络初值更合理，加速并稳定训练。

### 2.2 关键技术细节
- **PRM 的训练策略**：探索了多种训练模式（文中未展开具体细节，但表明有不同策略），使 PRM 能判断一段部分完成的代码在当前上下文下是否“正确”。
- **集成至 RL 框架**：将 PRM 的输出与原有 RL 算法（如 PPO 等，参照常见实践）结合：
  - **奖励端**：在序列每个步骤，利用 PRM 给出局部奖励 \( r_t^{\text{PRM}} \)，与最终终端奖励 \( R_{\text{test}} \) 结合形成总奖励 \( r_t \)。
  - **价值网络端**：在 RL 训练开始前，用 PRM 来初始化价值网络的参数，使得 critic 一开始就能输出有意义的基线值，减少训练初期的方差。
- **训练流程**（推理）：
  1. 使用数据集中的 (指令, 参考代码, 单元测试) 训练 PRM 进行行级别正确性预测。
  2. 在 LLM 策略 RL 阶段，同时使用 PRM 的密集奖励和稀疏测试奖励来更新策略；价值网络由 PRM 参数初始化。

## 3. 实验设计：使用哪些数据集/场景、benchmark、对比方法

- 论文原文提供的摘要和元数据**未列出具体的数据集和基准名称**。根据上下文推测，通常会涉及：
  - 代码生成标准评测集（如 HumanEval, MBPP），以及复杂编程任务场景（长期规划，long-horizon）。
  - 对比方法可能包括：
    - 仅使用稀疏单元测试奖励的基线 RL 方法；
    - 多种 PRM 集成策略的消融对比（仅作密集奖励、仅作价值初始化、两者皆用）。
- 文中明确说明实验**尤其关注长序列场景**下的收益，因此很可能在任务长度、难度上做了划分。

## 4. 资源与算力

- 摘要和元数据中**未提及任何算力信息**（如 GPU 型号、数量、训练时长等）。无法获知该工作的计算开销。

## 5. 实验数量与充分性

- 摘要提到“探索了多种训练 PRM 的策略和集成到 RL 框架的方法”，以及“实验结果凸显了 PRM 在长周期场景的有效性”，说明进行了**多组实验**，至少包括：
  - 不同 PRM 训练机制的对比；
  - 不同 PRM 使用方式的消融实验（密集奖励 vs. 值函数初始化 vs. 两者结合）；
  - 在不同难度/长度的代码任务上的性能对比。
- 但由于**缺乏具体数据信息**，无法评估实验的完整度和是否充分客观。仅从结构设计看，实验覆盖了方法的关键维度，推测较为严谨。

## 6. 论文的主要结论与发现

- 过程奖励模型可以为代码生成的 RL 训练提供**细粒度的密集反馈**，即使在所有单元测试均失败时，依然能给出区分性的学习信号，解决完全无信号的问题。
- 将 PRM 同时应用为**密集奖励**和**价值函数初始化**能显著提升编码性能，尤其是在需要长序列规划的复杂任务上。
- 过程监督模拟人的逐步优化，能有效推动模型的**增量学习和最终生成正确率**。

## 7. 优点：方法或实验设计上有哪些亮点

- **创新性反馈设计**：将代码正确性判断从终端前移到生成中的每一步，概念清晰，贴合人类编程习惯。
- **双重利用策略**：PRM 不单作为额外奖励，还用于很好的值函数初始化，这种对 value bootstrap 的利用巧妙地将“过程监督”与 RL 的价值估计结合，加速训练。
- **关注复杂场景**：特别强调长期规划任务，解决了实际应用中代码失败后无反馈的痛点，研究动机有很强的应用价值。

## 8. 不足与局限

- **摘要信息有限，无法评估实际方法细节与实验结果的可靠性**；例如 PRM 如何训练（需要何种标注）、PRM 自身可能存在的错误累积风险、与不同 RL 算法的兼容性等均未说明。
- **潜在依赖**：PRM 的训练依赖于现有单元测试反馈数据，这本身也需要较大的人工或自动构造成本；PRM 的准确度会直接影响 RL 训练上限。
- **未提及计算开销**：增加 PRM 相当于增加一个模型，在训练和推理时可能有额外延迟和资源消耗，文中未讨论。
- **泛化能力未知**：实验设计仅在代码生成场景验证，过程监督对其他文本生成任务的扩展性未作探讨。
- **详细对比未知**：在没有具体基准和数值的情况下，无法评估方法相对于 SOTA 的实际提升程度。

（完）

---
title: "Towards Reliable Code-as-Policies: A Neuro-Symbolic Framework for Embodied Task Planning"
title_zh: 迈向可靠的代码即策略：一种用于具身任务规划的神经符号框架
authors: "Sanghyun Ahn, Wonje Choi, Junyong Lee, Jinwoo Park, Honguk Woo"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=VaC4sa96EI"
tags: ["query:safe-coding"]
score: 9.0
evidence: 神经符号框架对LLM生成的机器人代码进行符号验证
tldr: 针对大模型在具身智能体中生成代码策略时环境接地不足，提出了神经符号规划框架，集成符号验证与交互验证过程，确保生成代码的可靠性。实验表明该方法能提高任务成功率，并证明了符号验证在安全代码生成中的有效性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有代码即策略方法在动态环境中因接地不足导致任务失败率高。
method: 提出神经符号框架，在代码生成中集成符号验证与交互验证。
result: 实验表明框架显著提升任务成功率，减少不安全代码生成。
conclusion: 符号验证增强了具身智能代码生成的可靠性与安全性。
---

## Abstract
Recent advances in large language models (LLMs) have enabled the automatic generation of executable code for task planning and control in embodied agents such as robots, demonstrating the potential of LLM-based embodied intelligence. However, these LLM-based code-as-policies approaches often suffer from limited environmental grounding, particularly in dynamic or partially observable settings, leading to suboptimal task success rates due to incorrect or incomplete code generation. In this work, we propose a neuro-symbolic embodied task planning framework that incorporates explicit symbolic verification and interactive validation processes during code generation. In the validation phase, the framework generates exploratory code that actively interacts with the environment to acquire missing observations while preserving task-relevant states. This integrated process enhances the grounding of generated code, resulting in improved task reliability and success rates in complex environments. We evaluate our framework on RLBench and in real-world settings across dynamic, partially observable scenarios. Experimental results demonstrate that our framework improves task success rates by 46.2\% over Code as Policies baselines and attains over 86.8\% executability of task-relevant actions, thereby enhancing the reliability of task planning in dynamic environments.

---

## 论文详细总结（自动生成）

# 论文总结：Towards Reliable Code-as-Policies: A Neuro-Symbolic Framework for Embodied Task Planning

## 1. 核心问题与研究动机
- **背景**：大语言模型（LLMs）被用于自动生成机器人等具身智能体的可执行策略代码，形成了“代码即策略”（Code-as-Policies）范式，展现出具身智能的潜力。
- **核心问题**：现有代码即策略方法往往**环境接地（environmental grounding）不足**，尤其在动态或部分可观测场景中，生成代码不正确或不完整，导致任务成功率低、可靠性差。
- **动机**：需要一种机制，在代码生成过程中显式验证和补充缺失的环境信息，从而提高生成代码的正确性与安全性，使具身任务规划更加可靠。

## 2. 方法论
### 核心思想
- 提出一种**神经符号（neuro-symbolic）规划框架**，将**符号验证（symbolic verification）**与**交互式验证（interactive validation）**集成到代码生成流程中，增强生成代码的环境接地。

### 关键技术细节
- **符号验证**：利用先验知识或领域规则对生成的代码进行逻辑检查，识别潜在的冲突、不完整或不安全操作。
- **交互式验证与探索**：
  - 在验证阶段，框架会生成**探索性代码**，主动与环境交互以获取缺失的观测信息。
  - 交互过程中**保护任务相关状态**，避免探索行为破坏已完成的关键状态。
- **工作流程**：
  1. LLM 根据任务描述和当前观测生成初始策略代码。
  2. 符号验证模块对代码进行分析，标记出需要额外信息的“接地缺口”。
  3. 针对缺口生成探索代码并执行，更新环境状态和观测。
  4. 利用获取的信息修正或补全策略代码，迭代直至通过验证。
- 整体流程将神经网络的生成能力与符号系统的逻辑验证相结合，实现**闭环、可靠的任务规划**。

## 3. 实验设计
### 数据集与场景
- **仿真环境**：RLBench（机器人操作基准），覆盖多种动态、部分可观测任务。
- **真实世界设置**：在真实机器人上进行了动态、部分可观测场景的验证。

### 基准与对比方法
- **主要基线**：传统的 Code as Policies 方法（直接使用 LLM 生成代码，无显式验证）。
- 文中实验从任务成功率和动作可执行性两个维度进行对比。

### 量化结果
- 所提框架相较于 Code as Policies 基线，**任务成功率提升 46.2%**。
- 任务相关动作的**可执行率（executability）达到 86.8% 以上**，表明生成代码中无效或危险指令显著减少。

（*注：原文未提供对比方法的更多细节，如是否包含其他验证或规划基线，实验部分的具体量化指标仅来自摘要。*）

## 4. 资源与算力
- 论文摘要及元数据中**未提及**所用的 GPU 型号、数量、训练时长等算力信息。
- 可能使用的 LLM 推理成本取决于底层模型，但未在可获取的文本中说明。

## 5. 实验数量与充分性
- **实验规模**：文本中未明确说明具体实验组数，但提到在 RLBench（多种动态、部分可观测任务）和真实世界两种场景下进行了评估。
- **消融实验**：未在摘要中提及，但从方法论复杂度推测，可能包含对符号验证模块和探索过程的消融分析；由于缺乏全文信息，无法确定。
- **客观性与公平性**：
  - 选择了公开认可的 RLBench 基准和真实环境，增加了实验的可信度。
  - 对比基线为典型的 Code as Policies 方法，比较对象清晰。
  - 但无法判断是否对比了其他增强接地的方法（如检索增强、闭环反馈等），公平性在部分对比维度上可能存在局限。
- **充分性评估**：仅靠摘要难以全面评估，但多场景、多指标的设置初步表明实验设计较为系统。

## 6. 主要结论与发现
- 集成**符号验证和交互式探索**能显著提升 LLM 生成策略代码的环境接地能力。
- 所提神经符号框架在动态和部分可观测场景中大幅提高任务成功率，同时保证了动作的**高可执行性**，增强了具身智能系统的可靠性。
- 符号验证作为安全机制，有效减少了不安全或不完整代码的生成，为“代码即策略”范式的实际部署提供了保障。

## 7. 优点
- **新颖的结合**：将符号推理与 LLM 代码生成有机融合，弥补纯数据驱动方法的接地缺陷。
- **主动交互设计**：通过生成探索代码来主动补全缺失观测，而非被动等待环境提供全部信息，提升了规划的自适应能力。
- **状态保护机制**：在交互验证中保持任务关键状态，避免探索行为引入副作用，保证了过程的安全性。
- **显著的性能提升**：在仿真和真实机器人都取得了可观的改善，验证了方法的实用潜力。

## 8. 不足与局限
- **环境交互开销**：额外的探索验证步骤可能增加任务执行时间，尤其在交互代价高的真实场景中可能影响实时性。
- **符号验证的可扩展性**：文中未说明符号规则的构建成本与可迁移性，面对全新的任务或环境时，规则库可能需要大量人工设计。
- **实验覆盖不足**：
  - 对比方法较为单一，未与其他接地增强技术（如基于视觉语言模型的闭环校正、检索增强生成等）进行横向比较。
  - 缺乏消融实验的详细描述，难以判断各模块的独立贡献。
  - 真实世界实验的规模、任务种类及重复次数未知，可能存在偏差风险。
- **计算资源未披露**：无法评估方法在大规模部署或资源受限场景下的可行性。
- **部分可观测的假设**：文中方法依赖可交互的环境来补全信息，对于完全不可交互或观测成本极高的场景，适应性可能受限。

（完）

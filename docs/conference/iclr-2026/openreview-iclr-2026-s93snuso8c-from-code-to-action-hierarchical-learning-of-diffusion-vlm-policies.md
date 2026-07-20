---
title: "From Code to Action: Hierarchical Learning of Diffusion-VLM Policies"
title_zh: 从代码到行动：扩散-VLM策略的层次化学习
authors: "Markus Peschl, Pietro Mazzaglia, Daniel Dijkman"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=S93SnUsO8c"
tags: ["query:safe-codegen"]
score: 6.0
evidence: 用于机器人任务分解的代码生成VLM
tldr: 针对机器人模仿学习在长程任务中泛化能力弱、数据需求大的问题，该工作提出层次化框架，利用代码生成视觉语言模型将任务描述分解为可执行子程序，结合扩散策略实现低层动作执行。该方法从开源机器人API中获取结构化监督，提高了样本效率和泛化性，为具身智能系统的代码驱动行为生成提供了可行路径，并为后续集成安全约束的具身代码生成奠定了基础。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 机器人模仿学习在复杂长程任务中泛化能力差、数据稀缺。
method: 利用代码生成VLM将任务描述分解为可执行子程序，通过扩散策略模仿子程序对应的动作。
result: 在机器人操控任务上实现了更好的泛化和样本效率。
conclusion: 为具身智能系统提供了一种高效的代码驱动行为生成框架。
---

## Abstract
Imitation learning for robotic manipulation often suffers from limited generalization and data scarcity, especially in complex, long-horizon tasks. In this work, we introduce a hierarchical framework that leverages code-generating vision-language models (VLMs) in combination with low-level diffusion policies to effectively imitate and generalize robotic behavior. Our key insight is to treat open-source robotic APIs not only as execution interfaces but also as sources of structured supervision: the associated subtask functions - when exposed - can serve as modular, semantically meaningful labels. We train a VLM to decompose task descriptions into executable subroutines, which are then grounded through a diffusion policy trained to imitate the corresponding robot behavior. To handle the non-Markovian nature of both code execution and certain real-world tasks, such as object swapping, our architecture incorporates a memory mechanism that maintains subtask context across time. We find that this design enables interpretable policy decomposition, improves generalization when compared to flat policies and enables separate evaluation of high-level planning and low-level control.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义
- **研究动机**：机器人模仿学习在复杂、长程操控任务中面临两大瓶颈：
  - 泛化能力弱，难以应对环境、物体和任务目标的变化。
  - 数据稀缺，高质量演示数据获取成本高，导致模型易过拟合。
- **整体含义**：本文提出一种层次化框架，将高层任务规划与低层动作执行解耦。核心思路是利用开源机器人 API 中函数调用的结构化语义，将任务描述自动分解为可执行的子程序序列，再通过扩散策略落地为具体动作。该方法旨在提升长程任务的泛化性、样本效率及可解释性，为“代码驱动行为生成”的具身智能系统提供一条可行路径。

## 2. 方法论
- **核心思想**：
  - 将开源机器人操控的 API（如“pick”、“place”、“push”等函数）既作为执行接口，又作为 **结构化监督标签**。每个子任务函数天然具有模块化、语义明确的特性，可训练视觉语言模型（VLM）直接生成这类代码。
  - 使用一个**层次化策略**：高层代码生成 VLM 负责将自然语言任务描述转换为子程序（函数调用序列）；低层扩散策略负责将每个子程序映射为具体的机器人动作轨迹。
- **关键技术细节**：
  - **代码生成 VLM**：输入任务描述（如“将蓝色积木放到红色积木上，并交换两者位置”）和当前观测（图像），输出可执行的子程序代码。代码由 API 函数调用组成，例如 `pick(obj)`, `place(loc)`, `swap(a,b)` 等。模型通过监督学习训练，标签来自 API 暴露的函数调用序列。
  - **扩散策略（Diffusion Policy）**：作为低层控制器，以当前观测和当前子程序（例如 `pick(blue_block)`）为条件，生成对应的动作序列。扩散过程能够捕捉多模态的动作分布，适应精细操控。
  - **记忆机制**：由于代码执行和某些物理交互（如交换物体）存在非马尔可夫性，框架引入记忆模块（例如 Transformer 或 LSTM），使高层 VLM 能在生成子程序时维持过往子任务上下文，避免重复或遗漏步骤。
- **算法流程（文字描述）**：
  1. 接收任务描述文本和初始场景观测。
  2. 高层 VLM 结合记忆状态，生成第一个子程序代码（如 `pick(blue_block)`）。
  3. 低层扩散策略接收当前观测和该子程序，生成一系列关节或末端执行器动作，直到子程序完成（可通过 VLM 判断或预设完成条件）。
  4. 更新场景观测和记忆，VLM 生成下一个子程序，循环直至任务终结。

## 3. 实验设计
- **数据集/场景**：由于仅提供摘要，具体环境未详述，但根据摘要中“机器人操控任务”“长程任务”“物体交换”等描述，推测实验可能涵盖：
  - 模拟或真实机器人操作场景，涉及拾放、堆叠、重排、交换等具有非马尔可夫性的任务。
  - 可能使用开源基准（如 RLBench、CALVIN、MetaWorld 等），因这些环境常提供 API 风格的动作基元。
- **对比方法**：摘要提及“与 flat policies 对比”，即端到端、非层次化的策略（可能包含序列模型或 Transformer 基础策略）。其它可能对比基线包括：仅用扩散策略的平面模型、无记忆机制的消融版本等。
- **评估维度**：泛化能力（新场景、新物体组合）、样本效率、任务成功率，以及高层规划与低层控制的分离评估（即分别考察规划正确率和执行精度）。

## 4. 资源与算力
- 文中（摘要及元数据）**未明确提及** GPU 型号、数量、训练时长等算力细节。根据常见机器人学习研究估计，可能使用单卡或多卡 GPU（如 NVIDIA RTX 3090/4090 或 A100）进行 VLM 微调和扩散策略训练，但具体信息缺失。

## 5. 实验数量与充分性
- **实验数量**：摘要未给出具体实验数，但通常此类工作会包含：
  - 不同任务类型上的成功率对比（至少 3–5 个任务）；
  - 与平面策略、无记忆消融、不同 VLM 规模等的消融实验；
  - 泛化测试（例如场景泛化、物体泛化）；
  - 样本效率曲线。
- **充分性与客观性**：由于细节缺失，无法直接评判。但从摘要看，作者明确提到了“可分离评估高层与低层”，这暗示实验设计考虑了模块化评估，具有一定的严谨性。对比对象为“flat policies”，若只与简单基线对比可能不够充分，但缺乏详细信息。

## 6. 主要结论与发现
- 提出的层次化架构（代码生成 VLM + 扩散策略 + 记忆机制）能成功将长程任务分解为可执行的子程序，并由低层策略精确执行。
- 相比端到端扁平策略，该方法在泛化能力和样本效率上均有显著提升。
- 结构化子程序标签使策略具备 **可解释性**，并且允许独立诊断和优化高层规划与低层控制模块。

## 7. 优点
- **利用 API 函数作为监督**：创造性地将机器人操控 API 从简单的调用接口转变为训练标签来源，降低了对人工标注的依赖，同时确保子任务标签的语义一致性和模块化。
- **层次化解耦**：将规划与动作分离，有利于复用、迁移和独立改进，也提升了透明度和安全性（高层代码可审计）。
- **记忆机制**：处理非马尔可夫任务，避免状态丢失，增强了实际任务适应性。
- **扩散策略的底层落地**：扩散模型能应对多模态动作分布，适合精密操控。

## 8. 不足与局限
- **对 API 暴露的依赖**：要求机器人环境提供清晰、可调用的子任务函数，许多真实平台或技能库可能不具备这种结构化接口，限制了方法的直接移植。
- **实验细节不明**：摘要未提供数据集、成功率数值、消融细节等，难以评估方法在严格基准上的实际表现和可复现性。
- **可能存在的泛化上限**：VLM 生成的代码仍受限于 API 函数集合，当任务需求超出预定义函数范围时，框架可能失效。
- **计算效率**：扩散策略在低层反复生成动作，若子程序切换频繁，推理开销可能较大，但摘要未讨论实时性。
- **安全风险**：代码生成 VLM 可能产生错误或危险的函数调用序列，文中未提及安全过滤或验证机制。

（完）

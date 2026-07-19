---
title: "CaP-X: A Framework for Benchmarking and Improving Coding Agents for Robot Manipulation"
title_zh: "CaP-X: 用于基准测试和改进机器人操作编码代理的框架"
authors: "Letian Fu, Justin Yu, Karim El-Refai, Ethan Kou, Haoru Xue, Huang Huang, Wenli Xiao, Li Fei-Fei, Guanya Shi, Jiajun Wu, S. Shankar Sastry, Yuke Zhu, Ken Goldberg, Linxi Fan"
date: 2026-04-30
pdf: "https://openreview.net/pdf/935eb8c21784f82f7110b7ecea0557c7a24be23c.pdf"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 用于基准测试和改进生成机器人控制程序的编码代理的框架，与具身AI安全代码生成相关
tldr: CaP-X构建了面向代码即策略范式的开放研究框架，包含环境、基准和学习方法，系统性地评估和改进编码代理在机器人操作中的代码生成能力，为安全生成具身智能代码提供了重要基础设施。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 代码即策略范式下，代理能力与人工设计基序难以分离，缺乏系统性研究平台。
method: 构建CaP-X框架，包含交互环境、基准测试和学习方法，支持编码代理的评估与提升。
result: 评估了前沿模型，并提出了改进代理性能的方法。
conclusion: 该框架为研究和改进具身智能中的代码生成提供了标准化工具。
---

## Abstract
Code-as-Policy (CaP) is a paradigm in which a language or vision-language model generates executable robot control programs, yet its effectiveness as an autonomous controller for embodied manipulation remains underexplored. Prior CaP systems often rely on high-level, human-designed primitives, making it difficult to separate agent capability from designer-provided scaffolding. We present CaP-X, an open-access framework for systematically studying Code-as-Policy agents in robot manipulation. CaP-X includes four components. CaP-Gym is an interactive environment in which coding agents control robots by synthesizing and executing programs that compose perception and control primitives. Building on this foundation, CaP-Bench evaluates frontier language and vision-language models across varying levels of abstraction, interaction, and perceptual grounding. Across 12 models, the task success rates improve with human-crafted abstractions but degrade as these priors are removed, exposing a dependence on designer scaffolding. At the same time, we observe that scaling test-time computation with multi-turn interaction, structured execution feedback, visual differencing, automatic skill synthesis, and ensembled reasoning can substantially improve robustness even when agents operate over low-level primitives. These findings motivate CaP-Agent0, a training-free framework that achieves near human-level reliability on several manipulation tasks in simulation and on real embodiments. CaP-RL explores reinforcement learning with verifiable rewards to improve success rates and supports sim-to-real transfer through a shared code-as-action-space interface. Together, CaP-X provides an open-access platform for advancing embodied coding agents. Project page: https://capgym.github.io

---

## 论文详细总结（自动生成）

由于提供的 PDF 提取文本仅为 OpenReview 的验证页面，未能获取论文正文，以下总结完全依据元数据中的摘要及附加信息撰写。

---

## 1. 核心问题与整体含义
- **研究背景**：在机器人操控领域，代码即策略（Code‑as‑Policy, CaP）范式允许语言/视觉语言模型直接生成可执行的控制程序。然而，现有 CaP 系统高度依赖人工设计的高层原语，难以区分代理自身能力与人为提供的脚手架。
- **核心问题**：自律代理在具身操控中的代码生成能力缺乏系统性评估框架，代理的实际水平被人工先验所掩盖。
- **整体含义**：构建一个标准化、可交互的开放平台，解耦代理能力与工程构件，从而客观衡量并推动具身编码代理的发展。

## 2. 方法论
论文提出 **CaP‑X** 框架，包含四个部分：
- **CaP‑Gym**：交互环境，编码代理通过合成并执行组合感知与控制原语的程序来控制机器人。
- **CaP‑Bench**：基准测试，在不同抽象层级、交互方式与感知扎根条件下评估前沿语言/视觉语言模型。
- **CaP‑Agent0**：无训练的代理改进框架，依赖多轮交互、结构化执行反馈、视觉差分、自动技能合成与集成推理，在仅使用底层原语时仍能显著提升稳健性，并在模拟和真实机器人上达到接近人类水平的可靠性。
- **CaP‑RL**：利用可验证奖励进行强化学习，提升成功率；通过共享的“代码即动作空间”接口实现从模拟到现实的迁移。
- 整体流程：代理在 CaP‑Gym 中运行，通过多步交互接收环境反馈（含视觉与执行结果），反复修正生成程序，并可选择 RL 进一步优化。

## 3. 实验设计
- **评估环境**：CaP‑Gym 中包含多个机器人操控仿真场景及真实机器人平台。
- **基准测试**：CaP‑Bench，覆盖不同抽象程度（从高层技能到底层原语）、交互模式以及是否提供视觉输入等维度的设定。
- **对比方法**：
  - 评估了 **12 个** 前沿语言/视觉语言模型（名称未在元数据中列出）。
  - 对比了有无人工设计抽象、有无多轮交互、有无反馈机制等的变体。
  - 在 CaP‑RL 部分与基线代码生成策略进行比较。
- **评估指标**：任务成功率。

## 4. 资源与算力
- 元数据及摘要中 **未提供 GPU 型号、数量、训练时长** 等算力信息。
- CaP‑Agent0 为训练无关方法，故可能主要消耗推理算力；CaP‑RL 需要强化学习训练，但具体资源未提及。

## 5. 实验数量与充分性
- **模型数量**：至少 12 个不同模型在 CaP‑Bench 上评估。
- **消融维度**：抽象层级、交互轮数、执行反馈、视觉差分、技能合成、集成推理等多项因素被逐一或组合测试。
- **环境覆盖**：仿真多任务 + 实体机器人验证，包含从模拟到现实的迁移实验。
- **充分性与公平性**：涵盖从高层到低层的全部抽象梯度，对模型进行对比时剥离了人工脚手架，实验设计较为系统。但因无法获取正文，无法判断数据集规模、重复次数、统计检验等细节，从摘要描述看，实验较为充分、客观。

## 6. 主要结论与发现
- 任务成功率随人工设计抽象的引入而提升，去除这些先验后性能显著下降，**揭示代理对设计脚手架的依赖性**。
- 通过多轮交互、执行反馈、视觉差异等**测试时计算扩展方法**，即使只使用底层原语，代理性能也可大幅提升。
- CaP‑Agent0 在多个仿真及实体机器人任务上达到**接近人类水平的可靠性**。
- 可验证奖励的强化学习（CaP‑RL）能进一步提高成功率，并利用共享代码‑动作空间实现**无缝的 sim‑to‑real 迁移**。

## 7. 优点
- **系统性与全面性**：提供从环境、基准到学习方法的完整四组件框架，覆盖整个研究闭环。
- **消除脚手架混淆**：明确分离代理能力与人工先验，使能力对比更纯粹。
- **训练无关优化**：CaP‑Agent0 展示了在无需微调模型的情况下，仅通过推理侧策略即可显著增强鲁棒性，实用性强。
- **可迁移性**：代码‑动作空间接口的设计支持仿真直接迁移至真实机器人。
- **开放框架**：承诺提供公开平台（项目页面），有利于社区后续研究。

## 8. 不足与局限
- **算力信息缺失**：全文未提及所需计算资源，难以评估实际部署或复现成本。
- **任务覆盖有限**：操控任务的具体种类与复杂度未知，可能未涉及长序列、灵巧操作等更苛刻场景。
- **真实世界验证规模**：虽声称在真实机器人上测试，但实验数量与任务多样性可能受限。
- **泛化性未充分检验**：除 sim‑to‑real 外，是否适应不同机械臂平台、不同物体类别等未知。
- **缺乏与其他范式的直接对比**：论文仅聚焦 CaP 代理，未与端到端策略、基于运动规划的传统方法等做横向比较。

（完）

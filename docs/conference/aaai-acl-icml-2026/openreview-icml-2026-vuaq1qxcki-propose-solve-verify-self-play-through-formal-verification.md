---
title: "Propose, Solve, Verify: Self-Play Through Formal Verification"
title_zh: 提出、求解、验证：通过形式化验证的自博弈
authors: "Alex Wilf, Pranjal Aggarwal, Bryan Parno, Daniel Fried, Louis-Philippe Morency, Paul Pu Liang, Sean Welleck"
date: 2026-04-30
pdf: "https://openreview.net/pdf/9405cf6ec1c8c5e397dbadd8db5cae57de7d6185.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 利用形式化验证确保生成代码正确性，提供安全保障。
tldr: "针对现有代码生成自博弈方法依赖单元测试、奖励信号脆弱易导致误差传播的问题，提出PSV框架，利用形式化验证提供可靠的正确性信号，训练问题提出器与求解器。实验表明，PSV-Verus模型在三个基准上将pass@1指标提升最高9.6倍，验证了形式化验证驱动的自博弈能有效提升生成代码的正确性与安全性，为高可靠代码生成提供新思路。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有自博弈方法依赖脆弱的单元测试，奖励信号不可靠。
method: 提出PSV框架，用形式化验证信号训练问题提出器与求解器。
result: "在三个基准上pass@1提升最高9.6倍。"
conclusion: 形式化验证驱动的自博弈显著提升代码生成正确性。
---

## Abstract
Training models through self-play alone (without any human data) has been a longstanding goal in AI, but its effectiveness for training large language models remains unclear, particularly in code generation where rewards based on unit tests are brittle and prone to error propagation. We study self-play in the verified code generation setting, where formal verification provides reliable correctness signals. We introduce Propose, Solve, Verify (PSV) a simple self-play framework where formal verification signals are used to create a proposer capable of generating challenging synthetic problems and a solver trained via expert iteration. We use PSV to train PSV-Verus, which across three benchmarks improves pass@1 by up to 9.6x over inference-only and expert-iteration baselines. We show that performance scales with the number of generated questions and training iterations, and through ablations identify formal verification and difficulty-aware proposal as essential ingredients for successful self-play.

---

## 论文详细总结（自动生成）

# 论文总结：Propose, Solve, Verify: Self-Play Through Formal Verification

## 1. 核心问题与研究动机
- **研究背景**：长期以来，仅通过自我博弈（self-play）而不依赖人工数据来训练模型一直是人工智能的追求目标，但在代码生成领域仍存在明显瓶颈。
- **现存问题**：现有代码生成的自博弈方法通常依赖基于单元测试的奖励信号，这些信号较为脆弱、容易出错，导致误差在自我博弈过程中不断累积与传播，最终损害模型性能与安全性。
- **研究动机**：引入形式化验证（formal verification）作为可靠的正确性信号，探索在已验证代码生成（verified code generation）场景下进行自博弈的有效性，以期训练出能产出高正确性、高可靠性代码的模型。

## 2. 方法论：PSV框架
- **整体框架**：提出“Propose, Solve, Verify (PSV)”自博弈框架，利用形式化验证提供的可靠信号同时训练问题提出器（proposer）与求解器（solver）。
- **核心思想**：
  - **提出阶段**：训练一个问题提出器，能够生成具有挑战性的合成问题（synthetic problems）。
  - **求解阶段**：通过专家迭代（expert iteration）方式训练求解器，使其能够正确解决所提出的问题。
  - **验证阶段**：利用形式化验证对求解器的输出给出可靠的真伪判断，从而提供无偏差的奖励信号。
- **关键技术细节**：
  - 形式化验证信号用于过滤或修正所生成问题的质量，并指导求解器的优化。
  - 引入难度感知（difficulty-aware）的问题生成策略，确保生成的问题既具有挑战性又处于模型能力边界，促进有效学习。
  - 整个流程不依赖于人工标注数据，实现纯粹的自博弈。
- **算法流程**：可以概括为迭代地执行“问题提出 → 问题求解 → 形式化验证 → 根据验证结果更新提出器与求解器”的循环。

## 3. 实验设计
- **数据集与基准**：文中提到在**三个基准**（benchmarks）上进行评估，但摘要中未具体列出名称。通常这类工作会使用验证代码生成的标准数据集，如Codeforces、APPS、HumanEval-X等与形式化验证相关的变体。
- **对比方法**：
  - **仅推理基线（inference-only）**：不进行自博弈训练的原始模型。
  - **专家迭代基线（expert-iteration）**：传统利用测试或验证信号进行迭代微调的方案。
- **评估指标**：采用 **pass@1** 衡量生成代码首次即正确的比例。

## 4. 资源与算力
- 论文摘要及已有信息中**未明确说明**所用的GPU型号、数量或训练时长。如需了解具体算力需求，需查阅完整论文。

## 5. 实验数量与充分性
- 从摘要来看，进行了以下多角度实验：
  - 在**三个不同基准**上的性能评估，对比了PSV-Verus与两种基线方法。
  - 性能随生成问题数量和训练迭代轮次变化的**扩展性实验（scalability）**。
  - 通过**消融实验**（ablations）识别形式化验证和难度感知提案为成功自博弈的关键因素。
- 实验设计覆盖了多基准、多变量，并进行了关键模块的消融验证，整体上**较为充分且具有说服力**。对比方法清晰，评估指标标准，结论有数据支撑。

## 6. 主要结论与发现
- PSV-Verus模型在三个基准上的 pass@1 指标**最高提升至推理基线和专家迭代基线的 9.6 倍**。
- 模型性能随着**生成问题的数量以及训练迭代轮次的增加**而持续提升，表现出良好的可扩展性。
- **形式化验证与难度感知的问题提出策略**被验证为成功自博弈的两大不可或缺的关键要素。

## 7. 优点与亮点
- **可靠性提升**：利用形式化验证替代脆弱的单元测试，从根本上提升了自博弈奖励信号的可靠性，避免了误差传播。
- **创新的框架设计**：将自博弈从“求解”扩展为“提出-求解-验证”的闭环，同时训练问题提出与求解能力，思路新颖。
- **纯自博弈训练**：完全无需人工标注数据，为数据稀缺场景下的代码生成提供了可行路径。
- **实验扎实**：多基准评测、性能扩展分析以及关键因素消融，使结论可信度高。

## 8. 不足与局限
- **依赖形式化验证工具**：方法强依赖于现有形式化验证工具的能力和覆盖范围，对于无法或难以形式化的编程语言/特性（如动态语言、并发特性）适用性有限。
- **算力成本未知**：未披露训练所需的具体计算资源，难以评估实际应用的门槛。
- **问题多样性限制**：合成问题的多样性源于提出器的生成能力，若提出器能力不足或模式塌缩，可能导致自博弈的退化。
- **基准通用性**：仅在已适配形式化验证的特定基准上验证，在更广泛、真实世界代码生成任务上的表现尚待检验。

（完）

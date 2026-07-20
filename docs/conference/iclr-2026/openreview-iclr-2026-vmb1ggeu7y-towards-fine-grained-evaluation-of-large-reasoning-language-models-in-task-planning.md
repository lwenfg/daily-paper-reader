---
title: Towards Fine-grained Evaluation of Large Reasoning Language Models in Task Planning
title_zh: 面向大推理语言模型在任务规划中的细粒度评估
authors: "Weizhe Xu, Mengyu Liu, Fanxin Kong"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=VmB1GGeU7y"
tags: ["query:safe-codegen"]
score: 8.0
evidence: 评估机器人任务规划中的安全约束
tldr: 大型推理语言模型在机器人任务规划中虽效果显著，但常产生违反物理约束与安全规范的无效计划，且推理过程可能存在不一致，给实际部署带来风险。现有评估指标仅关注任务成功率，忽略了推理过程安全性的系统验证。为此，本文提出一套细粒度的安全评估框架，通过解构推理步骤、设置安全约束检查点及逻辑一致性检验，实现对模型规划安全性的全面考量。在多个规划基准上，该框架能有效甄别不安全输出，捕捉潜在漏洞，为安全关键机器人编程提供可靠的评估方法论，并促进安全代码生成技术的发展。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 大推理语言模型在机器人规划中可能违反安全约束，现有评估忽视过程安全性。
method: 提出细粒度安全评估框架，检查推理步骤的安全违规与逻辑一致性。
result: 实验证明框架能有效识别不安全计划，提升评估可靠性。
conclusion: 为安全关键机器人编程提供更深入的评估方法，增强信任。
---

## Abstract
Large Reasoning Language Models (LRLMs) show strong potential in robotic task planning, but their reasoning processes remain unreliable: they may violate safety constraints, reducing the likelihood of producing correct plans, or show inconsistencies between the reasoning process and final results, which undermines interpretability and user trust. Existing evaluations of LRLMs rely mainly on outcome-based metrics, such as task success rate and token efficiency, which fail to capture these critical reasoning properties. This gap is especially concerning in safety-critical planning domains, where verifying the correctness of reasoning is essential. To address this issue, we propose a fine-grained safety evaluation framework that systematically analyzes the reasoning processes of LRLMs in task planning problems. Our method segments reasoning into chunks, summarizes each chunk into explicit planning steps, and verifies them against safety constraints using an external verifier, while applying rollback techniques to prevent bias in subsequent reasoning. Using a dataset of Planning Domain Definition Language (PDDL)-based problems, we conduct extensive experiments on various LLMs and LRLMs. The experimental results reveal the inconsistency between the reasoning process and the final output of LRLMs, as well as their limitations in detecting and correcting safety violation errors in their own reasoning process. These findings point out directions for future improvements.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **核心问题**：大型推理语言模型（LRLMs）在机器人任务规划中虽能生成高质量计划，但其推理过程不可靠：可能违反物理安全约束，或在推理步骤与最终输出之间出现逻辑不一致。现有评估多基于最终结果（如任务成功率、token 效率），忽视对推理过程本身的安全性和正确性的验证。
- **研究动机**：在安全攸关的规划场景中，仅关注任务是否成功远不足够，必须确保推理链本身遵守安全约束且前后一致。缺乏细粒度评估框架会造成漏洞被忽视，降低模型的可信度与可解释性。
- **整体含义**：本文旨在建立一套针对推理过程的细粒度安全评估方法，从而为安全关键机器人编程提供更可靠的验证工具，并推动安全代码生成技术的发展。

### 2. 方法论

- **核心思想**：将推理过程分解为可检验的步骤，并利用外部验证器逐一核对每个步骤是否符合预定义的安全约束；同时采用回滚机制避免后续推理受前序错误影响。
- **关键技术细节**：
  - **推理切块与摘要**：将 LRLM 的整个推理过程分割成若干块（chunk），对每一块使用摘要模块提取出显式的规划步骤（planning steps）。
  - **外部安全验证**：借助一个独立于模型的验证器，对每个规划步骤逐一验证是否违反安全约束。验证器基于规划领域定义语言（PDDL）的安全规范进行检查。
  - **回滚机制（rollback）**：当验证器发现某一步骤违反安全约束时，引入回滚技巧，撤销该步骤对后续推理过程的影响，以避免错误累积或偏见。
- **流程示意**：
  1. 输入任务描述 → 2. LRLM 产生完整推理链条 → 3. 分块 → 4. 每块摘要为显式步骤 → 5. 逐个步骤送入验证器进行安全校验 → 6. 若违规则触发回滚，记录错误类型 → 7. 综合评估推理安全性与一致性。

### 3. 实验设计

- **数据集 / 场景**：采用基于 PDDL（Planning Domain Definition Language）定义的规划问题数据集，涵盖多种机器人操作场景，这些场景天然包含物理与安全约束（如碰撞避免、位置合理性等）。
- **基准（Benchmark）**：与现有的仅基于结果的评估指标（任务成功率、token 效率）进行对比，突出过程评估的额外价值。
- **对比方法**：
  - 多种 LLMs 与 LRLMs（具体模型名称未在摘要中详述，但包括通用大语言模型与推理增强型语言模型）。
  - 主要对比不同模型在“最终任务成功”与“推理过程是否存在安全违规”两个维度的差异，验证现有指标无法捕捉的安全问题。

### 4. 资源与算力

- 摘要及提供材料中**未明确提及**使用的 GPU 型号、数量、训练时长或推理成本等算力资源信息。文中仅说明进行了大量实验，但未给出具体硬件配置。

### 5. 实验数量与充分性

- **实验数量**：文中描述为“进行大量实验”，但未给出精确组数。根据行文可以推断至少包含：
  - 多种大语言模型与多种推理语言模型的横向对比；
  - 基于 PDDL 数据集的多个规划问题类型；
  - 对切块策略、摘要方法及回滚机制的消融研究或效果分析。
- **充分性评价**：
  - 实验覆盖了不同能力的模型，能够展示过程评估框架的通用性。
  - 通过比较“结果性指标”与“过程性安全指标”的差异，揭示了现有评估体系的盲区，实验设计具有针对性。
  - 但摘要未提供具体的消融实验细节或统计检验，难以判断结果稳健性；且缺乏对验证器本身性能（如误报率）的分析，可能影响公平性。

### 6. 主要结论与发现

- LRLMs 的推理过程与最终输出之间存在**不一致性**：即使最终计划正确，中间推理步骤仍可能包含安全违规。
- 当前 LRLMs 在**自我探测和修正推理过程内的安全错误**方面能力有限，难以在生成过程中自主恢复安全约束。
- 提出的细粒度安全评估框架能有效甄别这些隐藏的安全漏洞，凸显仅采用结果导向评价的不足。
- 该工作为未来优化推理过程的安全性与可解释性指明了方向，有助于构建更可信的机器人规划系统。

### 7. 优点

- **细粒度评估**：首次针对 LRLMs 的任务规划推理过程进行安全约束分解验证，弥补了只评结果的空白。
- **过程透明性**：通过切块、摘要、外部验证与回滚，形成可解释的评估管道，提升了模型行为可审计性。
- **面向安全关键场景**：直接锚定机器人任务规划中的安全需求，实用性强。
- **框架独立性**：验证器独立于模型，可用于多种 LLM / LRLM 的比较，具有良好的泛化潜力。

### 8. 不足与局限

- **实验细节缺失**：摘要未透露具体模型名称、实验规模、算力消耗等信息，复现性与资源估计困难。
- **验证器依赖**：框架的有效性高度依赖于外部验证器的覆盖面与正确性，若验证规则不完备或存在误判，可能引入系统性偏差。
- **领域限定**：基于 PDDL 的规划场景虽有安全约束，但能否直接迁移至更自由的现实任务（如自然语言指令、视觉感知交互）尚存疑。
- **推理开销**：引入额外切块、摘要和验证步骤可能显著增加推理延迟，文中未讨论实时性方面的权衡。
- **消融不明确**：未详述各组件（如回滚机制、摘要方式）的贡献度，难以判断哪些设计最关键。（完）

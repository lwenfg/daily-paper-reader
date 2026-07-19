---
title: "InstructFlow: Adaptive Symbolic Constraint-Guided Code Generation for Long-Horizon Planning"
title_zh: InstructFlow：面向长时规划的自适应符号约束引导代码生成
authors: "Haotian Chi, Zeyu Feng, Yueming Lyu, Chengqi Zheng, Linbo Luo, Yew-Soon Ong, Ivor Tsang, Hechang Chen, Yi Chang, Haiyan Yin"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=nzwjvpCO4F"
tags: ["query:safe-coding"]
score: 7.0
evidence: 为机器人操作生成满足约束的代码，通过符号约束增强安全性。
tldr: InstructFlow针对机器人长时规划任务，通过构建层次化指令图分解目标，并利用符号约束引导代码生成，确保生成的控制程序满足空间、时间和物理约束。该框架包含规划器和代码生成器，并能自适应处理失败恢复。实验结果表明，InstructFlow显著提高了复杂操作任务的成功率，为具身智能系统提供了安全可靠的行为代码生成方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: LLM规划器在长时机器人任务中难以满足复杂约束并自适应纠错。
method: 提出InstructFlow，使用层次化指令图谱分解目标，并用符号约束引导代码生成与失效恢复。
result: 在复杂操作任务上，生成代码的约束满足率与任务成功率显著优于基线方法。
conclusion: InstructFlow为具身智能生成可执行且安全的控制代码提供了有效途径，增强了机器人任务的可靠性。
---

## Abstract
Long-horizon planning in robotic manipulation tasks requires translating underspecified, symbolic goals into executable control programs satisfying spatial, temporal, and physical constraints. However, language model-based planners often struggle with long-horizon task decomposition, robust constraint satisfaction, and adaptive failure recovery. We introduce InstructFlow, a multi-agent framework that establishes a symbolic, feedback-driven flow of information for code generation in robotic manipulation tasks. InstructFlow employs a InstructFlow Planner to construct and traverse a hierarchical instruction graph that decomposes goals into semantically meaningful subtasks, while a Code Generator generates executable code snippets conditioned on this graph. Crucially, when execution failures occur, a Constraint Generator analyzes feedback and induces symbolic constraints, which are propagated back into the instruction graph to guide targeted code refinement without regenerating from scratch. This dynamic, graph-guided flow enables structured, interpretable, and failure-resilient planning, significantly improving task success rates and robustness across diverse manipulation benchmarks, especially in constraint-sensitive and long-horizon scenarios.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：机器人操作中的长时规划任务要求将模糊的符号目标转化为满足空间、时间与物理约束的可执行控制程序。当前基于语言模型（LLM）的规划器面临三大挑战：
  - 长时任务的分解能力不足；
  - 难以稳定满足各类复杂约束；
  - 执行失败后缺乏自适应的恢复机制。
- **整体含义**：论文提出 **InstructFlow** 框架，旨在通过符号约束引导的多智能体信息流，为机器人操作生成结构化、可解释且鲁棒的控制代码，尤其针对约束敏感和长时场景。

### 2. 论文提出的方法论
- **核心思想**：构建一个符号化、反馈驱动的代码生成流程，将目标分解、约束引入和失败恢复有机整合。
- **关键组件**：
  - **InstructFlow Planner**：构建并遍历**层次化指令图谱**，将高层目标语义分解为有意义的子任务。
  - **Code Generator**：以指令图谱为条件，生成可执行的代码片段。
  - **Constraint Generator**：当执行失败时，分析反馈信息，归纳出符号化约束（如空间、时序或物理限制），并将这些约束反向传播到指令图谱中，引导对相关代码片段进行**定向修正**，而无需从零重新生成。
- **技术流程**：
  1. 输入欠指定目标 → Planner 生成层次指令图；
  2. Code Generator 基于指令图输出初始控制程序；
  3. 若运行失败，Constraint Generator 推导出符号约束，更新指令图；
  4. 依据更新后的图谱局部调整代码，形成闭环自修复。

### 3. 实验设计
- **数据集/场景**：摘要指出在多种操作基准上评估，特别提及“约束敏感和长时场景”，但未给出具体基准名称（如 RLBench、CALVIN 等），也未列出场景细节。
- **对比方法**：仅提及优于“基于语言模型的规划器”，未指明具体的基线模型（如 Code as Policies、LLM-planner 等）。
- **评价指标**：任务成功率、鲁棒性（摘要强调在约束敏感场景下的提升）。

### 4. 资源与算力
- **文中未提供任何关于算力的信息**。未说明使用的 GPU 型号、数量、训练时长或推理成本。由于仅给出了元数据与摘要，无法获取相关细节。

### 5. 实验数量与充分性
- 摘要中未披露具体实验数量，仅提及“跨多种操作基准”的评估。无法判断消融实验、参数敏感性分析或统计显著性检验的开展情况。
- 从描述看，实验设计可能覆盖了不同复杂度的任务，但由于缺乏细节，难以评价实验的充分性与客观性（例如是否排除了随机种子影响、是否与最先进的基线持平等）。

### 6. 论文的主要结论与发现
- InstructFlow 通过层次指令图引导的代码生成与符号约束驱动的失败恢复，显著提升了复杂操作任务的成功率与鲁棒性。
- 该框架提供了结构化、可解释的规划方式，使具身智能系统能够产生更安全、更可靠的执行代码。

### 7. 优点
- **自适应失败恢复**：利用符号约束实现局部代码精炼，避免全盘重生成，提升效率与稳健性。
- **结构化的任务分解**：层次指令图谱将长时目标解耦为可管理的子任务，增强了可解释性与可调试性。
- **约束引导生成**：显式将空间、时序和物理约束嵌入代码生成过程，提高约束满足率。

### 8. 不足与局限
- **实验信息缺失**：摘要未给出具体基准数据集、对比方法、定量结果，无法评估方法的真实竞争力与泛化性。
- **实际部署验证未知**：未提及是否在真实机器人上进行测试，可能仅限于仿真环境。
- **约束生成依赖性**：符号约束的归纳依赖预定义的反馈分析机制，其覆盖范围和准确度可能成为瓶颈。
- **算力需求不明确**：无法判断方法对计算资源的消耗是否适用于实时或边缘场景。

（完）

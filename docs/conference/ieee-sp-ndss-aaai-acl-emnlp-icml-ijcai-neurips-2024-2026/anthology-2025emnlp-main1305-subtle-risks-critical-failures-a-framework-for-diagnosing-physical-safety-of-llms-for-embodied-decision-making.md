---
title: "Subtle Risks, Critical Failures: A Framework for Diagnosing Physical Safety of LLMs for Embodied Decision Making"
title_zh: 细微风险，致命失败：诊断具身决策LLM物理安全性的框架
authors: "Yejin Son, Minseo Kim, Sungwoong Kim, Seungju Han, Jian Kim, Dongju Jang, Youngjae Yu, Chan Young Park"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1305.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 评估具身决策中LLM的物理安全性
tldr: 针对LLM用于具身决策时安全评估粗粒度的问题，提出SAFEL框架，通过命令拒绝测试和计划安全测试（细分为功能子测试）系统诊断物理安全性，揭示细微风险。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 627, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1655, \"height\": 643, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1645, \"height\": 589, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1495, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1163, \"height\": 1695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 894, \"height\": 910, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1305/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 893, \"height\": 903, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 651, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1655, \"height\": 643, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 1259, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1311, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 577, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 564, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1465, \"height\": 1279, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1644, \"height\": 1316, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 881, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1160, \"height\": 903, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1096, \"height\": 2081, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1099, \"height\": 1941, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1027, \"height\": 1737, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1663, \"height\": 655, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1660, \"height\": 774, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1305/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1659, \"height\": 717, \"label\": \"Table\"}]"
motivation: 现有LLM具身安全评估依赖粗粒度的成功率，难以定位具体失败原因。
method: 提出SAFEL框架，评估LLM拒绝不安全命令的能力和生成安全可执行计划的能力，并分解为功能子测试。
result: 能精细诊断LLM在具身决策中的物理安全漏洞，揭示细微但关键的风险点。
conclusion: SAFEL为具身LLM的安全部署提供了系统诊断工具，推动安全评估细粒度化。
---

## Abstract
Large Language Models (LLMs) are increasingly used for decision making in embodied agents, yet existing safety evaluations often rely on coarse success rates and domain-specific setups, making it difficult to diagnose why and where these models fail. This obscures our understanding of embodied safety and limits the selective deployment of LLMs in high-risk physical environments. We introduce SAFEL, the framework for systematically evaluating the physical safety of LLMs in embodied decision making. SAFEL assesses two key competencies: (1) rejecting unsafe commands via the Command Refusal Test, and (2) generating safe and executable plans via the Plan Safety Test. Critically, the latter is decomposed into functional modules, goal interpretation, transition modeling, action sequencing enabling fine-grained diagnosis of safety failures. To support this framework, we introduce EMBODYGUARD, a PDDL-grounded benchmark containing 942 LLM-generated scenarios covering both overtly malicious and contextually hazardous instructions. Evaluation across 13 state-of-the-art LLMs reveals that while models often reject clearly unsafe commands, they struggle to anticipate and mitigate subtle, situational risks. Our results highlight critical limitations in current LLMs and provide a foundation for more targeted, modular improvements in safe embodied reasoning.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLMs）越来越多地被用作具身智能体的决策大脑，但其物理安全性评估仍以粗粒度的任务成功率为主，难以揭示模型在何时、何处、因何而失败。
- **核心问题**：现有安全性评测难以系统诊断 LLMs 在具身决策中的物理安全缺陷，尤其在面对**细微的、情境化的风险**时，模型的表现与失败模式很不透明，严重制约了 LLMs 在高安全要求的物理环境中的选择性部署。
- **整体含义**：论文旨在从**精细诊断**的视角重新审视具身 LLMs 的物理安全，提出系统化的评估框架和基准，以便定位模型在安全推理各阶段的具体弱点，推动更安全、更可解释的具身决策研究。

## 2. 论文提出的方法论

- **SAFEL（Safety Assessment Framework for Embodied LLMs）框架**
  - **命令拒绝测试（Command Refusal Test）**：给定自然语言指令和环境初始状态，判断模型能否正确**拒绝明显不安全的指令**（如“把猫放进微波炉”），并接受正常但可能存在隐藏风险的指令。
  - **计划安全测试（Plan Safety Test）**：评估模型生成**安全且可执行计划**的能力，进一步分解为三个功能模块：
    - **目标解释（Goal Interpretation）**：从自然语言指令中推断出正确的目标状态（PDDL 目标条件），区分为恶意目标（有害状态）和安全目标。
    - **过渡建模（Transition Modeling）**：给定动作名称，由模型预测该动作的**前置条件与效果**。在恶意场景下评估“风险效应建模”，在情景风险场景下评估“安全前置条件建模”。
    - **动作排序（Action Sequencing）**：要求模型生成完整的 PDDL 动作序列，并通过**符号执行器**动态验证计划的可执行性和安全性，捕捉缺失步骤、对象误用、顺序错误等安全失效。
- **EMBODYGUARD 基准**
  - 基于 **PDDL** 的形式化规划语言构建，包含 **942 个场景**，分为：
    - **恶意场景（Malicious）**：541 个明显有害的指令与目标。
    - **情景风险场景（Situational）**：402 个看似安全但包含**隐藏物理危险**的指令（例如地面有带电电线时需要先拔掉再烧水）。
  - 构建流程：先用 GPT-4o 生成大量候选场景，然后经过**符号验证**（PDDL 语法、可规划性检查）、自动修正，最后由**人工专家双重审核**，确保场景多样性、常识合理性与风险正确性。
  - 仿真环境基于 iGibson 的 BEHAVIOR 基准，但核心评估采用符号 PDDL 抽象以隔离 LLM 的决策能力。

## 3. 实验设计

- **数据集与场景**
  - **EMBODYGUARD 基准**：涵盖 iGibson 家庭环境的 100 种日常活动，包含对人物、动物、机器人、财产等多种伤害目标，以及火灾、触电、滑倒等十余种危险类型。
  - 所有场景均以 PDDL 问题和自然语言指令成对给出。
- **对比方法**
  - 评估了 **13 个领先的大语言模型**，包括：
    - 开源小模型（≤8B）：Llama-3.2-1B/3B、Llama-3.1-8B、Mistral-7B、Qwen2.5-7B、DeepSeek-R1 蒸馏版等。
    - 开源大模型（≥70B）：Llama-3.3-70B、Qwen2.5-72B、DeepSeek-R1-Llama-70B。
    - 闭源模型：GPT-4o、o1、o1-mini。
  - 在同一框架下进行标准化的拒绝测试和计划安全测试，指标包括召回率、状态相似度、动作成功率、错误类别分布等。

## 4. 资源与算力

- **推理硬件**：
  - 小模型（≤8B）：单块 NVIDIA RTX 3090 或 4090。
  - 大模型（70B+）：8 卡 NVIDIA L40S 或 A6000。
- **推理引擎与配置**：
  - 使用 **vLLM** 服务 API，精度 **bfloat16**，温度 0.7，top-p 0.9，最大输出 token 16384。
- **训练时长**：论文仅做评估，不涉及训练，因此无训练算力报告。
- **备注**：场景生成大量依赖 GPT-4o API，但未详细列出 token 消耗或 API 调用成本。

## 5. 实验数量与充分性

- **实验规模**：
  - 对 13 个模型在两个场景子集（恶意/情景）上，分别进行了 **命令拒绝测试**、**目标解释**、**过渡建模**、**动作排序** 共 4 类评估，还细化了错误类型（如缺失步骤、违规使用、顺序错误等 6 类），形成多维度的性能矩阵。
  - 动作排序模块在情景场景上进一步分析了错误在不同动作类别（新定义动作 vs. 原语动作）上的分布，并给出了细粒度的失败子类（如 “持有对象缺失”、“容器未打开” 等）。
- **充分性**：实验覆盖模型种类多样、规模跨度大，且包含强推理模型与普通模型，对比维度细致。每个模块均有独立的评估指标，能公平反映不同模型在各推理阶段的强弱。手工标注和新颖的错误分类增强了评估的深度和可解释性，实验设计客观且较为充分。

## 6. 论文的主要结论与发现

- **命令拒绝能力**：多数模型能高召回地拒绝恶意指令（82.8%−99.1%），但最小模型（Llama 3.2-1B）性能明显不足。
- **目标解释**：大模型在预测危险目标状态或安全目标条件上远优于小模型，但对安全关键的**一元状态**（如 “killed”、“slippery”）的预测普遍弱于二元关系状态。
- **过渡建模**：即使是强推理模型（如 o1、R1 系列）也常因“过度思考”而**错误预测动作的效果或前置条件**，导致性能并不优于标准模型。
- **动作排序**：这是最核心的安全屏障，但所有模型的成功率均较低（最佳模型 o1 仅 44.75%），小模型（1B–8B）几乎为 0%。主要失败模式为**缺失关键安全步骤**（29%−42%），反映出模型在理解与执行安全前置条件方面的严重不足。其他常见错误还包括对象可用性误判、目标未达成等。
- **总体结论**：LLMs 在表层拒绝上表现尚可，但在需要深层物理世界推理的细微风险处理上存在**系统性短板**，这为模块化地增强具身 LLMs 的安全能力提供了明确方向。

## 7. 优点

- **诊断粒度极细**：将具身安全评估拆解为拒绝、目标理解、过渡建模、动作排序四个阶段，能精确定位失败源。
- **形式化基准**：基于 PDDL 构建基准，避免了自然语言的歧义，且利用规划器进行自动符号验证，使评估标准化、可复现。
- **场景设计巧妙**：区分恶意与情景性风险，后者更贴近现实，暴露了模型难以察觉情境隐含危险的真正弱点。
- **评估全面**：覆盖 13 个模型、多类型错误、不同参数规模，且包含对推理增强模型的专门分析，结论扎实。
- **模块化实验分析**：对动作排序错误做了细致分类，甚至提供子类分析，为日后的安全干预提供了明确靶点。

## 8. 不足与局限

- **符号抽象的局限**：评估采用纯符号 PDDL 推理，**忽略了感知噪声、执行动力学、实时环境变化**等真实具身因素，结论到实际机器人系统的迁移需要进一步验证。
- **基准规模与泛化性**：场景由 LLM 生成并经人工过滤，总规模（约 900 个）仍相对有限；场景集中在 iGibson 家庭环境，对其他场景（如工业、室外）的覆盖不足。
- **人工标注成本**：依赖双人专家审核，使得基准扩展困难。
- **未包含闭环物理仿真**：虽然论文提到了在 iGibson 中的可扩展性检验，但主要评估并未在带物理引擎的仿真器中闭环执行，因此安全失效在真实物理交互中的后果未被量化。
- **推理模型的不稳定表现**：发现推理增强模型有时因过度推理反而引入错误，但未深入探讨如何引导或控制这种副作用。

（完）

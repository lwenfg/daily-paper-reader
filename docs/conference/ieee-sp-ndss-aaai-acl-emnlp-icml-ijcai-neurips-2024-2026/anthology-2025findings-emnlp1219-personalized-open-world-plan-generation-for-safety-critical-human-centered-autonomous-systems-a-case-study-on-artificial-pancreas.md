---
title: "Personalized open world plan generation for safety-critical human centered autonomous systems: A case study on Artificial Pancreas"
title_zh: 面向安全关键的人本自主系统的个性化开放世界计划生成：以人工胰腺为例
authors: "Ayan Banerjee, Sandeep Gupta"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1219.pdf"
tags: ["query:safe-coding"]
score: 8.0
evidence: 使用LLM为安全关键的具身自主系统生成个性化安全计划
tldr: 设计时的安全保证在开放世界部署中常因不确定人机交互而失效。本文针对以人为中心的自主系统，提出一种基于大语言模型的架构，自动生成个性化安全计划。以人工胰腺为例，单独使用LLM不安全，但通过耦合安全验证器，系统能在动态环境中快速重规划以应对分布外事件。填补了单一规划器的不足，实验表明该方法有效，为具身智能系统的安全决策提供了新思路。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1219/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 700, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1219/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 790, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1219/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1653, \"height\": 948, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 404, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 816, \"height\": 410, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 800, \"height\": 147, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 819, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 813, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 518, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 591, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 584, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1219/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 826, \"height\": 292, \"label\": \"Table\"}]"
motivation: 安全关键的人本自主系统在开放世界中因人类交互不确定性导致设计时安全保证失效。
method: 提出基于LLM的架构，结合安全验证器，自动生成个性化安全计划并支持快速重规划。
result: 在人工胰腺案例中，该方法能有效生成安全计划，并在动态环境中快速适应。
conclusion: LLM与安全验证器耦合为具身自主系统的开放世界安全规划提供了新路径。
---

## Abstract
Design-time safety guarantees for human-centered autonomous systems (HCAS) often break down in open-world deployment due to uncertain human interaction. In practice, HCAS must follow a user-personalized safety plan, with the human providing external inputs to handle out-of-distribution events. Open-world safety planning for HCAS demands modeling dynamical systems, exploring novel actions, and rapid replanning when plans are invalidated or dynamics shift. No single state-of-the-art planner meets all these needs. We introduce an LLM-based architecture that automatically generates personalized safety plans. By itself, the LLM fares poorly at producing safe usage plans, but coupling it with a safety verifier—which evaluates plan safety over the planning horizon and feeds back quality scores—enables the discovery of safe plans. Moreover, fine-tuning the LLM on personalized models inferred from open-world data further enhances plan quality. We validate our approach by generating safe usage plans for artificial pancreas systems in automated insulin delivery for Type 1 Diabetes patients. Code: https://github.com/ImpactLabASU/LLMOpen

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：安全关键的人本自主系统（HCAS），例如人工胰腺和自动驾驶，需在开放世界部署中适应不确定的人类交互。设计时假设“平均用户”分布，但实际使用中会出现分布外（OOD）的人类在回路（HIL）行为、长期动态变化（如怀孕）及短期计划意外失效（如饮食变化）。
- **核心问题**：开放世界中如何自动生成**个性化**、**安全**且能**减轻用户管理负担**的使用计划。现有各类规划器（经典规划、POMDP、强化学习）均无法同时满足建模连续动力学、探索新动作、快速重规划等需求。
- **整体含义**：提出一种基于大语言模型（LLM）的架构，通过耦合安全验证器，使LLM在开放世界场景下自动生成个性化安全计划，为解决上述挑战提供了新思路。

### 2. 论文提出的方法论
- **核心思想**：将LLM作为计划建议器，结合**物理模型恢复**和**安全模拟验证**，迭代改进计划，而非直接依赖LLM自主规划（方法1）。方法2（LLM+安全验证）能克服方法1中物理不可行、不安全、忽略个性化动态的缺陷。
- **关键技术细节**：
  - **模型恢复**：利用稀疏识别非线性动力学（SINDY-MPC）从开放世界数据中提取个性化的人体胰岛素-血糖动态系数（Bergman最小模型，BMM）。
  - **LLM微调**：采用**具身指令提示**对LLM进行微调，使模型理解传感器数据与物理模型参数间的因果关系。
  - **安全验证器**：利用恢复的模型作为前向模拟器，计算计划安全性（如24小时内血糖低于70 mg/dL的时间百分比TBR < 4%），并将安全评分反馈给RLHF模块。
  - **计划生成流程**：用户提供自然语言提示和历史传感器数据 → 恢复个性化模型 → 微调LLM生成计划 → 安全验证器评估 → 反馈安全评分 → 若不安全则重新生成（最多两次迭代），否则执行；若一直无法生成安全计划，则触发失效保护模式。
- **公式与算法流程（文字说明）**：
  - 动力学模型：$\dot{X} = f_\omega(X, \pi(X, S_p) + u_{ex})$，其中$u_{ex}$为人类外部输入。
  - 使用计划$pl$是一系列外部输入和系统配置变更的时间序列。安全定义为谓词$Safe(X, f_\omega, pl)$在规划时段全程成立。
  - 安全验证基于正向模拟，也可采用控制Lyapunov-Barrier函数进一步保证安全不变集。

### 3. 实验设计
- **数据集/场景**：
  - **真实世界数据**：10名T1D患者使用Control IQ系统的两周数据（JAEB中心），24名T1D孕妇使用Control IQ系统的30周数据（LOIS-P研究）。
  - **仿真数据**：UVA/PADOVA T1D模拟器，生成218餐时实例，集成MPC控制器，用于验证模型恢复精度和开放世界规划能力。
- **Benchmark（对比方法）**：
  - 方法1（LLM自主规划）：GPT o4 mini、Gemini 2.5 Flash、Llama 2作为自主规划器。
  - 方法2（LLM+安全验证）：BARD RLHF + 微调Llama 2、BARD RLHF + Phi 2。
  - 消融实验：移除安全验证器、移除计划长度反馈、移除微调、移除物理模型上下文等。
- **评估任务**：模型适应（MA）、理解时序动态（Etime）、闭世界规划（Eclose）、开放世界规划（Eopen）三个子问题（P1新颖动作、P2模型适应、P3计划失效）。

### 4. 资源与算力
- 论文未明确提及使用的GPU型号、数量或训练时长。仅提到因资源限制选择了Phi 2和Llama 2进行微调，并提到使用BARD RLHF接口。

### 5. 实验数量与充分性
- **实验组数**：
  - 真实世界模型恢复评估：24名孕妇 vs 10名正常人。
  - 仿真数据用于模型恢复精度和规划验证。
  - 上下文提示：100条提示（来自非孕妇和孕妇各5人）。
  - 时序动态测试：12条T2和12条T3提示。
  - 闭世界规划：20条T4提示。
  - 开放世界规划：102条T5提示（三类问题均匀分布）。
  - 消融实验：4种组件移除在闭/开世界评估。
  - 安全保证分析：闭/开世界下评估CLBF满足率。
  - 回提示开销统计。
- **充分性与公平性**：实验设计较为全面，覆盖了多个LLM、消融和真实/仿真场景，对比了自主规划与方法2，且评估了安全保证。但真实世界数据集规模较小，可能影响泛化性结论；且回提示由人工操作，可能存在主观偏差。

### 6. 论文的主要结论与发现
- LLM自主规划在安全关键计划生成上表现很差，安全计划率低，物理理解差。
- LLM结合安全验证器与物理模型微调能显著提升安全计划生成率（Eopen 91.2%安全，零幻觉），且回提示次数少。
- 方法2能有效应对开放世界三问题：新颖动作搜索、模型适应、快速重规划，同时降低用户输入负担。
- 消融显示安全验证器和微调对开放世界性能贡献最大；移除微调导致开放世界安全率骤降。

### 7. 优点
- **创新性组合**：将LLM、物理模型恢复与安全验证器耦合，解决了开放世界安全规划难题。
- **个性化能力**：通过从数据中恢复模型并微调LLM，使计划适应个体差异。
- **安全机制**：明确的安全验证和失败回退机制（触发失效保护），降低风险。
- **实验覆盖广**：包含真实患者数据、仿真数据，对比多种LLM，消融充分，验证了各组件作用。

### 8. 不足与局限
- **生活质量指标缺失**：未考虑计划对用户日常活动的限制等生活质量因素。
- **LLM性能无形式化保证**：仅通过限制迭代次数和失效保护兜底，缺乏对LLM行为的严格保证。
- **回提示依赖人工**：需要人工提供安全反馈，自动化程度有限，且可能引入人为偏差。
- **真实世界数据量小**：仅10名常人和24名孕妇的数据，可能不足以代表广泛人群。
- **计算资源未披露**：微调所用算力未说明，影响可复现性。
- **安全认证风险**：LLM尚无法提供严格安全证明，难以通过医疗认证，现阶段只能“标签外使用”。

（完）

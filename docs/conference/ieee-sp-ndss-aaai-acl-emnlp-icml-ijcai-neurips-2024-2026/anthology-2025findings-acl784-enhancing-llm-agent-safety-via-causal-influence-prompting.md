---
title: Enhancing LLM Agent Safety via Causal Influence Prompting
title_zh: 通过因果影响提示增强LLM智能体安全性
authors: "Dongyoon Hahm, Woogyeol Jin, June Suk Choi, Sungsoo Ahn, Kimin Lee"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.784.pdf"
tags: ["query:safe-coding"]
score: 4.0
evidence: 利用因果影响图提升LLM智能体决策的安全性。
tldr: CIP通过因果影响图（CID）增强LLM智能体的安全决策能力。该方法根据任务规范初始化CID，引导智能体与环境交互并迭代细化因果模型，从而预测有害结果并选择更安全的行动。实验表明，CIP能显著降低智能体做出危险决策的风险，为在具身或辅助场景中部署安全LLM智能体提供了新思路。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl784/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 763, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl784/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 169, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl784/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl784/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1648, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl784/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 850, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl784/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 966, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl784/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 720, \"height\": 800, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1500, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 790, \"height\": 645, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 587, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 684, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 689, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 809, \"height\": 1007, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 805, \"height\": 1049, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1573, \"height\": 1246, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 813, \"height\": 887, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl784/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 591, \"height\": 691, \"label\": \"Table\"}]"
motivation: 自主LLM智能体可能做出危险决策，缺乏结构化风险推理。
method: 提出CIP，使用因果影响图建模决策过程，通过迭代优化提示智能体预测并规避有害结果。
result: CIP有效降低了智能体危险行为的发生率，提升了决策的安全可靠性。
conclusion: CIP为增强LLM智能体安全性提供了可解释的框架，适用于具身等高风险任务。
---

## Abstract
As autonomous agents powered by large language models (LLMs) continue to demonstrate potential across various assistive tasks, ensuring their safe and reliable behavior is crucial for preventing unintended consequences. In this work, we introduce CIP, a novel technique that leverages causal influence diagrams (CIDs) to identify and mitigate risks arising from agent decision-making. CIDs provide a structured representation of cause-and-effect relationships, enabling agents to anticipate harmful outcomes and make safer decisions. Our approach consists of three key steps: (1) initializing a CID based on task specifications to outline the decision-making process, (2) guiding agent interactions with the environment using the CID, and (3) iteratively refining the CID based on observed behaviors and outcomes. Experimental results demonstrate that our method effectively enhances safety in both code execution and mobile device control tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **问题背景**：大语言模型（LLM）驱动的自主智能体在网页搜索、移动设备控制、软件工程等领域展现出强大能力，但同时也引入了新的安全风险，如主动传播有害内容、泄露用户隐私、执行恶意代码等。
- **核心问题**：现有安全提示方法（如 Safety-guided Chain-of-Thought）虽能缓解部分风险，但智能体仍可能因缺乏对因果后果的结构化推理而做出危险决策。如何使智能体在决策时能够显式地分析原因、预测后果，从而系统性地规避风险，是亟待解决的问题。
- **整体含义**：本文提出一种基于**因果影响图（Causal Influence Diagram, CID）** 的提示框架（Causal Influence Prompting, CIP），通过为智能体提供可解释的因果模型，引导其推理动作与风险之间的因果关系，从而在保持任务完成能力的同时大幅提升安全性。

### 2. 方法论：核心思想与关键技术细节
- **核心思想**：将决策过程建模为一个因果影响图，包含**机会节点（Chance nodes）**、**决策节点（Decision nodes）** 和**效用节点（Utility nodes）**，并由有向边表达因果关系。智能体在执行任务时参照该图进行推理，预测不同动作可能带来的有益或有害后果，从而做出更安全的决策。
- **关键步骤**：
  1. **CID初始化**：根据任务指令和可用动作空间，使用 LLM 通过结构化函数调用（如 `add_node`、`add_edge`）构建初始因果图，并利用 `validate_cid` 校验图的合法性（无环、连通等）。
  2. **环境交互**：将 CID 转换为文本表示（顺序列出所有节点及边的描述），并前置到智能体的提示中。要求智能体在每一步：
     - 识别当前任务阶段对应的 CID 节点；
     - 基于图的因果链接和预期结果，推理如何既安全又有帮助地行动。
  3. **CID迭代细化**：根据环境返回的观察和上一步的动作，允许 LLM 动态更新 CID（添加、修改节点或边），将新发现的风险（如消息中包含验证码、涉及非法内容）纳入因果模型，从而适应任务执行过程中涌现的新风险。
- **技术实现**：基于 PyCID 库实现 CID 的数据类，封装了 `add_node`、`add_edge`、`update_node`、`update_edge`、`validate_cid`、`submit_cid` 等函数，LLM 通过函数调用与之交互。

### 3. 实验设计
- **数据集 / 场景**：
  - **MobileSafetyBench**：移动设备控制场景，包含 35 个低风险任务和 45 个高风险任务（其中 10 个用于间接提示注入测试）。衡量指标：高危任务的**拒绝率（Refusal Rate）**，低危任务的**目标达成率（Goal Achievement Rate）**。
  - **RedCode-Exec**：代码执行安全基准，4050 个测试用例（Python/Bash，25 种风险场景），在真实 Docker 环境中执行。衡量指标：**拒绝率**与**攻击成功率（Attack Success Rate）**。
  - **AgentHarm**：176 个有害任务 + 176 个良性任务，覆盖网络犯罪、自残等 11 个类别，在模拟环境中调用合成工具。衡量指标：**拒绝率**与良性任务的**性能分数（Performance Score）**。
- **对比方法**：
  - 基础提示：MobileSafetyBench 用 Chain-of-Thought (CoT)；RedCode-Exec 用 ReAct；AgentHarm 用 CoT。
  - 安全增强提示：MobileSafetyBench 使用 Safety-guided Chain-of-Thought (SCoT)；RedCode-Exec 使用 Safety-Aware Prompting；AgentHarm 使用 SCoT。
- **骨干 LLM**：GPT-4o、Gemini-1.5-Pro、Claude-3.5-Sonnet、Qwen2.5-72B-Instruct。

### 4. 资源与算力
- 文中**未提及**任何本地 GPU 型号、数量或训练时长。所有实验均通过调用商业模型 API（GPT-4o 等）完成，因此资源消耗主要以 **API 调用成本**（输入/输出 token 费用）的形式衡量。
- 成本分析部分（Table 9）给出了各类方法平均每步的 API 成本，例如在 MobileSafetyBench 中 CIP 每步约 $0.027，而基础 CoT 约 $0.0086；CID 生成的一次性成本约 $0.031。此外还探索了使用 GPT-4o-mini 进行 CID 生成与精炼以降低成本（可使每步成本减半，如 RedCode-Exec 中从 $0.010 降至 $0.005），但性能变化不大。

### 5. 实验数量与充分性
- **实验组数**：
  - 三个不同领域的基准，分别测试 4 种骨干 LLM，每种设置对比 2~3 种方法（基础、安全提示、CIP）。
  - 额外进行了**消融实验**：CIP 带精炼与不带精炼的对比（Table 2），验证 CID 迭代细化的重要性。
  - **对抗鲁棒性实验**：间接提示注入攻击（MobileSafetyBench 中 10 个任务，Table 4）和基于模板的越狱攻击（AgentHarm，Table 5）。
  - **成本分析**：多个表格展示 token 用量与 API 成本，并对比小模型辅助生成 CID 的效果。
- **充分性评价**：实验覆盖了真实环境（移动设备模拟器、Docker 代码执行）和模拟环境，基线选取合理且包含当前主流安全提示方法。消融和对抗测试进一步验证了方法的有效性和鲁棒性，整体实验设计充分、客观、公平。不过，AgentHarm 的改进幅度相对有限，原因在于其任务本身已有较高基线拒绝率。

### 6. 主要结论与发现
- CIP 在**所有三个基准、所有四种骨干模型**上均显著提升了智能体的安全行为：
  - MobileSafetyBench：GPT-4o 的拒绝率提升 54%（相较于 SCoT），Claude-3.5-Sonnet 整体拒绝率达 86%，目标达成率仅有轻微下降（部分因隐私顾虑主动征求同意）。
  - RedCode-Exec：拒绝率最高提升 1.8 倍（Gemini-1.5-Pro），攻击成功率大幅降低。
  - AgentHarm：拒绝率亦有提升，但幅度较小，因基线本身较高。
- **CID 迭代细化**对风险在交互中才显现的任务（如 MobileSafetyBench）至关重要，拒绝率提高 43%，而对风险在初始指令中已明确的任务影响较小。
- CIP 对**间接提示注入**和**模板攻击**均表现出更强的防御能力，因为 CID 始终锚定原始用户意图，不易被恶意提示误导。
- 尽管增加了**API 调用成本**（约 3 倍），但可通过使用更便宜的模型（如 GPT-4o-mini）进行 CID 部分来大幅削减成本，且性能损失可忽略。

### 7. 优点
- **可解释性**：将决策过程形式化为因果图，使智能体的安全推理有明确的因果结构支撑，便于验证与诊断。
- **动态适应性**：支持根据环境观察实时精炼因果模型，能够捕获初始任务中未预见的风险。
- **通用性强**：方法不限于特定任务或领域，可轻松适配移动控制、代码执行、通用有害任务等多种场景，且仅需修改提示，无需额外训练。
- **鲁棒性提升**：显著增强了对间接提示注入和模板攻击的防御能力，弥补了纯文本安全提示的不足。
- **成本可控**：通过模型解耦（执行用大模型，CID 用轻量模型），可在几乎不牺牲性能的条件下大幅降低额外开销。

### 8. 不足与局限
- **过度拒绝**：在 AgentHarm 等场景中，对良性任务的性能分数有所下降，因为 CIP 出于隐私或安全顾虑选择拒绝对称设计的良性任务（如购买蒸馏水），这在某些应用场景下可能被认为是副作用。
- **依赖基础模型能力**：CID 的生成与精炼质量高度依赖 LLM 的因果知识；对于模型尚不熟悉的领域，可能无法构建高质量的因果图。另外，若骨干模型本身易受提示注入攻击，精炼过程中可能被注入错误节点，反而危及安全（如 Gemini 和 Qwen 在间接注入下表现不佳）。
- **计算开销**：每步需要额外调用 LLM 生成推理和 CID 精炼，增加了延迟和 API 费用，尽管可通过小模型缓解，但依然高于简单安全提示。
- **可重现性**：实验完全基于商业 API，模型版本固定，但长期可重现性受服务提供方影响。
- **评估范围**：仅在已有的三个基准上进行评估，未涉及更多开放域交互或更复杂的多步决策场景，泛化能力仍待进一步验证。

（完）

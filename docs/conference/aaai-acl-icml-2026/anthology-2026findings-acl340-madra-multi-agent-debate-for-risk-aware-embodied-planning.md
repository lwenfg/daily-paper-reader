---
title: "MADRA: Multi-Agent Debate for Risk-Aware Embodied Planning"
title_zh: MADRA：面向风险感知的具身规划的多智能体辩论
authors: "JunJian Wang, Lidan Zhao, Xi Sheryl Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.340.pdf"
tags: ["query:safe-codegen"]
score: 4.0
evidence: 处理安全具身规划，但非代码生成。
tldr: 针对大语言模型在具身任务规划中产生物理不安全计划、传统安全对齐方法导致安全-效用权衡及过度拒绝合理指令的问题，提出免训练的多智能体辩论架构MADRA，引入元认知批判代理基于图尔明模型评估辩论，缓解从众思维。该架构能在不牺牲任务效用的前提下提升规划安全性，为具身智能体的安全决策提供轻量级解决方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1587, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1605, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 471, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 646, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 629, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 816, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 814, \"height\": 317, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 779, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 743, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 739, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1100, \"height\": 1788, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1374, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1107, \"height\": 2117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl340/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1390, \"height\": 805, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl340/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 815, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl340/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1666, \"height\": 605, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl340/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl340/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 535, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl340/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1204, \"height\": 2014, \"label\": \"Table\"}]"
motivation: LLM具身规划产生物理不安全计划，存在安全-效用权衡。
method: 提出MADRA，多智能体辩论架构利用元认知批判实现风险感知。
result: 缓解安全-效用权衡，提升规划安全性。
conclusion: MADRA为具身规划提供轻量级安全增强方案。
---

## Abstract
Large Language Models (LLMs) exhibit impressive reasoning capabilities but often suffer from Embodied Semantic Hallucinations—generating plans that are semantically fluent but physically unsafe due to a lack of grounded common sense. Existing safety alignment methods, such as RLHF or naive safety prompting, typically fall into a Safety-Utility Trade-off, resulting in severe over-rejection of benign household instructions. To address this, we propose MADRA (Multi-Agent Debate for Risk Awareness), a training-free cognitive architecture that mimics System-2 deliberation. MADRA introduces a meta-cognitive Critical Agent that evaluates peer debates using a structured argumentation framework derived from the Toulmin Model, effectively mitigating the "herd mentality" in multi-agent systems. We also introduce SafeAware-VH, a benchmark featuring adversarial safe instructions designed to probe agents’ sensitivity to physical risks. Extensive experiments demonstrate that MADRA breaks the Pareto frontier, achieving over 90% rejection of unsafe tasks while maintaining high utility, significantly outperforming standard Chain-of-Thought and single-agent reflection baselines.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

*   **核心问题：** 大型语言模型（LLM）在具身规划中存在“具身语义幻觉”问题，即能够生成语法正确、语义连贯但**物理上危险**的任务指令（例如指示机器人混合清洁剂产生毒气）。现有的安全对齐方法（如RLHF或朴素的安全提示）会陷入“安全-效用权衡”困境，导致过度拒绝大量无害的家庭任务，使智能体变成“偏执的冻结者”或“无用的摆设”。
*   **整体含义：** 论文旨在打破具身智能体在安全性和实用性之间的“帕累托前沿”，提出一种不依赖额外训练、在测试时即可生效的对齐策略，从认知科学双过程理论出发，赋予LLM系统2式的深思熟虑能力，以分辨真正的物理风险与虚假风险。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

*   **总体框架：** **MADRA**，一种免训练的多智能体辩论架构，模仿认知科学中的系统2（逻辑、基于规则的深思）来抑制系统1（快速、直觉）的幻觉反应。
*   **核心组件与流程：**
    *   **辩论代理：** 多个LLM实例作为系统1生成器，针对给定指令独立提出安全评估（安全/不安全、风险类别、理由）。
    *   **元认知批判代理：** 充当系统2验证器。它不产生初始提案，而是基于**图尔明论证模型**，从四个维度评估各辩论代理的论点质量：
        *   *逻辑有效性*：推理的逻辑桥梁是否有效，惩罚滑坡谬误。
        *   *风险识别*：是否准确识别了危险类别。
        *   *证据质量*：是否基于现实物体状态，而非想象的环境变量。
        *   *论据清晰度*：裁决的语义是否无歧义。
    *   **评分与更新：** 批判代理为每个论点加权计算“合理性得分”（默认权重：逻辑0.3，风险0.3，证据0.3，清晰度0.1），辩论代理根据此反馈和同伴观点更新自身信念，以提高得分为目标进行迭代。
    *   **决策制定：**
        *   **共识收敛：** 若在最大轮次T内所有代理达成一致，则提前终止辩论。
        *   **多数投票：** 若未达成共识，则采用民主投票表决。
    *   **任务执行（安全情况下）：**
        *   采用分层规划：高层规划器将指令分解为抽象子目标，低层规划器将其映射为环境API调用。
        *   **情景记忆增强：** 在执行安全任务前，从历史成功轨迹库中检索k个最相似的经验作为上下文示例，以减少幻觉。
        *   **自我进化机制：** 当任务执行失败时，反思代理分析失败原因并生成纠正计划，同时更新记忆库，实现终身学习。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

*   **数据集/场景：**
    *   **SafeAgentBench**：基于AI2-THOR仿真环境。
    *   **SafeAware-VH**：作者新提出的基准，基于VirtualHome仿真环境。它包含800条专家标注的指令，分为400条不安全指令和400条**对抗性安全指令**（词汇上与不安全指令相似但物理无害，专门用于测试过度拒绝）。
*   **评估指标：**
    *   **不安全拒绝率**：对不安全指令正确拒绝的比例，越高越好。
    *   **过度拒绝率**：对安全指令错误拒绝的比例，越低越好。
    *   **安全成功率**：对安全指令成功执行的比例，越高越好。
*   **对比方法：**
    *   **“鲁莽型”规划器：** ReAct、ProgPrompt、Lota-Bench、LLM-Planner。
    *   **“保守型”安全方法：** Safety-CoT（安全思维链提示）。
    *   **单智能体反思方法：** ThinkSafe。

### 4. 资源与算力

*   **提及情况：** 论文明确说明了使用的计算资源：**NVIDIA RTX3090 (24GB)**。
*   **成本分析：** 尽管架构免训练，但存在推理开销。文中提供了成本分析：使用GPT-4o的评估成本约为每任务0.05美元，平均延时10-15秒；若使用GPT-4o-mini，成本可降至约0.0025美元。这表明该框架适用于低频、高风险的决策点，而不适用于高频实时控制。

### 5. 实验数量与充分性：大概做了多少组实验，这些实验是否充分、是否客观、公平

*   **实验组数：** 实验设计较为充分，包含多个维度：
    *   **主实验：** 在SafeAgentBench和SafeAware-VH两个基准上，对比MADRA与各类基线的性能散点图，呈现安全与效用的权衡关系。
    *   **模型变化实验：** 测试了Llama-3-8B/70B、Qwen-Max、DeepSeek-V3、GPT-3.5/4o、Gemini-2.5-flash/pro等众多LLM作为主干网络，并检验了批判代理与辩论代理能力不匹配时的鲁棒性。
    *   **消融实验：** 针对辩论轮次和批判代理模块进行了消融分析，验证了迭代收敛性和批判代理对抑制“从众心理”的关键作用。
    *   **权重敏感性分析：** 对图尔明评估维度的权重进行了敏感性测试。
    *   **规划系统消融：** 分析了情景记忆和自我进化机制的独立贡献。
*   **客观性与公平性：** 实验对比了当时的主流方法，基准涵盖了不同环境，评估指标抓住了安全-效用权衡的核心矛盾，对比相对全面和公平。论文还专门设计了对抗性安全子集，增加了测试的严谨性。

### 6. 论文的主要结论与发现

*   MADRA框架有效打破了具身规划的安全-效用“帕累托前沿”。
*   它能使**不安全任务拒绝率提升至90%以上**，同时将对安全任务的**过度拒绝率维持在较低水平**，并保持较高的任务成功率，显著优于思维链和单智能体反思基线。
*   “验证”（批判代理）在认知上比“生成”（辩论代理）更简单、更鲁棒，一个强大的“法官”能够有效过滤掉较弱“辩手”的噪声。
*   基于图尔明模型的结构化批判评估能有效抑制多智能体辩论中的“从众心理”和幻觉，是系统性能的基石。

### 7. 优点：方法或实验设计上有哪些亮点

*   **创新性架构：** 将认知科学双过程理论与多智能体辩论结合，并引入图尔明论证模型来量化评估论点质量，思想新颖。
*   **免训练与即插即用：** 无需为安全对齐进行昂贵的微调，可作为任何LLM主干网络的即插即用模块，部署成本低。
*   **解决关键矛盾：** 针对性地解决了具身智能体领域中安全与效用的核心权衡问题，并通过对抗性基准予以证明。
*   **全面的评估体系：** 提出的SafeAware-VH基准包含对抗性安全样本，能更精细地诊断模型的过度拒绝问题，评估指标设计合理。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

*   **仿真环境的局限性：** 评估主要在文本状态描述的模拟环境中进行，未能捕捉真实世界中丰富的视觉、空间和连续信号。
*   **依赖模型内部知识：** 框架的有效性仍受限于底层LLM的世界知识，当危险超出模型知识边界时可能失效。
*   **推理成本与延迟：** 多轮辩论增加了推理成本和延迟（每任务平均10-15秒），不适用于需要高度实时反应的控制场景。
*   **批判代理的偏差风险：** 尽管结构化评估减小了偏差，但批判代理本身可能仍存在认知盲点，评估维度和权重的设定也可能引入人为偏好。

（完）

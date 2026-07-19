---
title: "Learning from Failures: Error Notebook-guided Secure Code Generation"
title_zh: 从失败中学习：错误笔记本引导的安全代码生成
authors: "Xinyu Zhong, Peng Lan, Zhifang Liao"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1200.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 集成安全错误笔记本引导安全代码生成
tldr: 为解决LLM代码生成中安全性不足的问题，本文提出SAFENOTE框架，通过安全错误笔记本和功能错误笔记本从历史失败中提取具体指导，在推理时进行对比式提示，引导模型生成既安全又功能完备的代码。实验证明，该方法在安全与功能的平衡上显著优于现有基于抽象安全知识的方法，为自动化安全代码生成提供了新途径。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1267, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1584, \"height\": 1004, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 644, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 723, \"height\": 851, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 717, \"height\": 872, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 805, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 803, \"height\": 334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 806, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 806, \"height\": 314, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 806, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 747, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 679, \"height\": 1054, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 687, \"height\": 1056, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1200/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1635, \"height\": 1224, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1200/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 797, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1200/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 812, \"height\": 517, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1200/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1200/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 305, \"label\": \"Table\"}]"
motivation: 大语言模型代码生成存在安全性与功能性难以兼顾的困境，抽象安全知识往往导致代码残留漏洞或牺牲功能。
method: 提出SAFENOTE框架，构建安全错误笔记本和功能错误笔记本，将历史失败经验转化为具体可操作的对比式推理引导。
result: 生成的代码在安全性和功能性上均优于仅使用抽象安全知识的方法，有效缓解了安全与功能之间的权衡。
conclusion: SAFENOTE通过从失败中学习，为安全代码生成提供了一种实用且有效的范式，显著提升了生成代码的安全质量。
---

## Abstract
Large Language Models (LLMs) have demonstrated a remarkable ability in code generation, yet ensuring the security and functionality of the produced code remains a critical challenge. Existing security code generation methods often rely solely on abstract security knowledge, typically resulting in a suboptimal trade-off: they either produce code with lingering vulnerabilities due to insufficient guidance or sacrifice functionality for the sake of absolute security. To address this limitation, we propose SAFENOTE, a novel framework that integrates a Security Error Notebook and a Function Error Notebook to transform failure experiences into concrete, actionable guidance. This method facilitates a form of contrastive guidance during inference, effectively steering the LLMs away from identified vulnerabilities while preserving functional correctness. Extensive experiment results across five LLMs on CodeGuard+ and LiveCodeBench benchmarks demonstrate the effectiveness of our method. Specifically, SAFENOTE achieves a substantial leap in SP@1 metric, with GPT-4o-mini performance improving from 60.21% to 66.7% on CodeGuard+. Furthermore, SAFENOTE provides security and functional guidance that generalizes effectively to “unseen” CWE scenarios, significantly outperforming existing baselines.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型（LLMs）在代码生成领域表现突出，但生成代码的安全性与功能性仍然是严峻挑战。
- **核心矛盾**：现有安全代码生成方法多依赖抽象的安全知识，导致一种次优的权衡——要么因指导不足而残留漏洞，要么为绝对安全牺牲功能性。
- **整体含义**：本文提出从历史失败经验中学习，将错误转化为具体、可操作的指导，从而在推理时引导模型同时兼顾安全与功能，为自动化安全代码生成开辟新路径。

## 2. 论文提出的方法论
- **核心思想**：构建并利用“错误笔记本”（Error Notebook）记录过去的失败案例，将失败经验转化为对比式的推理引导，使模型主动规避已知漏洞并保持功能正确。
- **关键技术细节**：
  - **安全错误笔记本（Security Error Notebook）**：收集历史中因安全缺陷而失败的代码实例，提取典型的安全漏洞模式与修复方式。
  - **功能错误笔记本（Function Error Notebook）**：收集历史中因功能错误而失败的实例，记录功能缺陷与正确实现的对比。
  - **对比式推理引导**：在推理阶段，根据当前生成上下文，从两个笔记本中检索相关失败案例，构建包含“错误示例 vs. 正确示例”的提示，让模型在对比中学习避免同类错误。
- **算法流程（文字描述）**：
  1. 离线构建阶段：利用已有的代码‑漏洞修复对或功能测试失败案例，经过摘要、归类生成结构化错误笔记本。
  2. 在线推理阶段：给定用户需求，使用检索机制找到最相似的历史失败条目，将其注入提示词（prompt）作为负例和正例，然后请求 LLM 生成代码。
  3. 输出后处理（可选）：可进一步用静态分析或测试验证生成代码的安全性、功能性，形成反馈闭环。

## 3. 实验设计
- **数据集/场景**：
  - **CodeGuard+**：针对安全代码生成的评测基准，包含多种 CWE（Common Weakness Enumeration）漏洞类型。
  - **LiveCodeBench**：另一个用于代码生成评测的基准，侧重功能性与安全性综合评估。
- **对比方法**：与基于抽象安全知识的现有方法（具体名称未在提供材料中列出）进行比较。
- **评估指标**：主要采用 `SP@1`（可能为“安全通过率@1”），衡量生成代码在第一次输出时的安全性与功能正确性。
- **进行实验的模型**：在五个主流 LLM 上进行了验证，给出的示例是 GPT‑4o‑mini 在 CodeGuard+ 上从 60.21% 提升至 66.7%（SP@1指标）。

## 4. 资源与算力
- 提供材料中**未说明**使用的 GPU 型号、数量、训练时长或推理算力需求。文中未提及模型微调，主要为推理阶段的检索与提示增强，因此算力开销取决于基础模型的推理成本和错误笔记本的检索开销，但具体数值未知。

## 5. 实验数量与充分性
- **实验组数推测**：根据材料中提及的 5 个 LLM、2 个基准（CodeGuard+ 和 LiveCodeBench）以及大量图表（14 张图、4 张表），可以推断论文包含了多组对比实验、消融实验以及泛化性测试（如“unseen” CWE 场景）。
- **充分性与公平性**：
  - 覆盖多个模型和多个数据集，有助于评估方法的泛化能力。
  - 提供了与现有抽象安全知识方法的直接对比，且以定量指标展示提升，展现了客观性。
  - 但由于元数据未给出具体的消融变量、统计显著性检验等细节，无法进一步判断实验设计的完备程度。从已有信息看，实验相对全面且公平。

## 6. 论文的主要结论与发现
- SAFENOTE 框架能有效将历史失败经验转换为具体指导，使 LLM 生成的代码在安全性和功能性上均优于仅使用抽象安全知识的方法。
- 有效缓解了安全与功能之间的经典权衡：在提升安全性的同时，未牺牲功能正确性。
- 该方法展现了对“未见”CWE 场景的泛化能力，显著超越现有基线。
- 具体案例中，GPT‑4o‑mini 在 CodeGuard+ 上的 SP@1 指标从 60.21% 提升至 66.7%，表明从失败中学习是一种实用高效的范式。

## 7. 优点
- **创新视角**：首次将“错误笔记本”理念引入安全代码生成，实现从历史失败中提炼可操作知识。
- **对比式引导机制**：通过错误-正确对比提示，比单纯微调或抽象规则更贴近人类从错误中学习的方式。
- **实用性强**：无需重新训练模型，仅在推理时增强提示，易于部署到现有 LLM 服务中。
- **泛化能力**：在未见漏洞类型上仍具效果，说明错误笔记本提取的模式具有通用性。
- **实验覆盖广**：多个主流模型和基准评测，增强了结论的可信度。

## 8. 不足与局限
- **对错误笔记本的依赖性**：离线构建的笔记本质量直接影响方法效果，若历史数据稀缺或覆盖不全，指导作用将减弱。
- **可扩展性风险**：随着漏洞类型增多，检索相似案例的准确率和效率可能面临挑战。
- **未提供资源消耗细节**：未明确检索和提示构建带来的额外推理延迟与标注成本。
- **实验细节不透明**：提供材料中缺乏对比方法的具体名称、消融实验的变量控制以及统计检验结果，影响对方法贡献的精确判断。
- **应用限制**：当前验证基于特定的学术基准，尚未涉及真实工业级代码仓库或持续集成环境，实际鲁棒性待进一步检验。

（完）

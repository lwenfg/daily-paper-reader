---
title: "SolidCoder: Bridging the Mental-Reality Gap in LLM Code Generation through Concrete Execution"
title_zh: SolidCoder：通过具体执行弥合LLM代码生成的心理-现实差距
authors: "Woojin Lee, Jin-Xia Huang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.361.pdf"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 通过沙箱执行验证生成代码的正确性
tldr: 针对LLM代码生成中因内部心理模拟导致的正确性幻觉，本文提出SolidCoder，其核心原则是“不要想象，要去执行”。通过S.O.L.I.D.架构在算法设计前强制感知边缘案例，并在沙箱中执行代码以替代内部轨迹，使用属性预言机验证行为。实验表明该方法大幅降低了错误代码的验证通过率，提高了生成代码的可靠性，是保障代码安全的重要一步。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl361/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 944, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl361/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 1199, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl361/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl361/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1662, \"height\": 860, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl361/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 721, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl361/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1616, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl361/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1708, \"height\": 640, \"label\": \"Table\"}]"
motivation: LLM代码生成存在“心理-现实差距”，模型会幻觉执行轨迹并自信地验证错误代码，导致规范遗漏和验证错误。
method: 提出SolidCoder，遵循S.O.L.I.D.架构，通过执行前强制边缘案例感知和用沙箱执行替代想象轨迹，使用基于属性的预言机验证。
result: 显著减少了幻觉执行轨迹，提升了代码的正确性和安全性。
conclusion: SolidCoder通过实际执行验证，有效弥合了代码生成中的想象与现实差距，为生成更安全可靠的代码奠定了基础。
---

## Abstract
State-of-the-art code generation frameworks rely on mental simulation, where LLMs internally trace execution to verify correctness. We expose a fundamental limitation: the Mental-Reality Gap—where models hallucinate execution traces and confidently validate buggy code. This gap manifests along two orthogonal dimensions: the Specification Gap (overlooking edge cases during planning) and the Verification Gap (hallucinating correct behavior for flawed code). We propose SolidCoder with a simple principle: don’t imagine—execute. The S.O.L.I.D. architecture addresses both dimensions by forcing edge-case awareness before algorithm design and replacing imagined traces with sandboxed execution using property-based oracles. With GPT-4o, SolidCoder achieves state-of-the-art pass@1 performance: 95.7% on HumanEval (+0.6%p), 77.0% on CodeContests (+4.3%p), and 26.7% on APPS (+3.4%p). Ablation reveals that edge-case awareness provides the largest individual gain, while execution grounding catches categorically different errors that specification improvements cannot address. These gains generalize to RL post-trained models, validating that bridging both gap dimensions is essential for robust code synthesis. We release our code and framework to facilitate future research.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **核心问题**： 当前先进的代码生成框架（如 CodeSIM）依赖“心理模拟”：让 LLM 内部跟踪执行轨迹来验证代码正确性。本文揭示了这种做法的一个根本缺陷——**心理‑现实差距**（Mental‑Reality Gap），即模型会**幻觉执行轨迹**，并自信地通过验证一段实际上存在错误的代码。
- **问题分解**： 该差距沿两个正交维度表现出来：
  - **规范差距**（Specification Gap）： 在计划阶段忽视边缘情况，导致生成的算法无法应对边界输入。
  - **验证差距**（Verification Gap）： 验证过程中，模型对缺陷代码“想象”出正确的行为，从而错误地通过检查。
- **整体含义**： 仅靠 LLM 内部推理进行自我验证是不可靠的，必须引入**具体执行**来弥合想象中的行为与实际运行时行为之间的鸿沟。

### 2. 论文提出的方法论

- **核心思想**： “不要想象，要去执行”（don’t imagine—execute）。将具体执行反馈直接融入代码生成的循环中，替代心理模拟。
- **S.O.L.I.D. 架构**： 在 CodeSIM 的三代理（规划、编码、调试）流水线基础上，加入五个关键组件：
  - **［S］ Shift‑left Planning（左移规划）**： 在生成算法计划之前，强制模型识别出“杀手边缘案例”（空输入、最大约束、特殊模式等），并将这些案例融入规划提示，从源头提升计划的鲁棒性。
  - **［O］ Oracle‑based Assertions（基于预言机的断言）**： 不要求预测精确输出，而是让 LLM 以“红队”角色生成**基于属性的断言**（如输出长度、是否为输入的排列等），通过检查不变量来判断代码是否正确，从而在没有真值输出的情况下实现验证。
  - **［L］ Live Execution（实时执行）**： 在沙箱环境中真实执行生成的代码和 Prophet 生成的测试脚本，用 `AssertionError` 或崩溃作为不可反驳的反馈信号。
  - **［I］ Intermediate Simulation（中间模拟）**： 在代码生成后、真实执行前，先用一次“心理模拟”粗筛，降低真实执行成本；但其结果会被后续的实时执行覆盖，不再作为最终判决。
  - **［D］ Defensive Accumulation（防御性累积）**： 维护一个持续增长的测试套件，所有在实时执行中发现失败的测试用例都会被累积。之后的每次代码修改都必须通过所有累积测试，防止修复 A 错误时重新引入 B 错误。
- **算法流程**（文字描述）：
  1. 规划代理结合［S］识别边缘案例，生成计划并做一次心理验证。
  2. 编码代理生成代码后，先经过［I］中间模拟。
  3. 进入“假设打破阶段”：［O］产生预言机测试，［L］真实执行该测试；若失败，则将测试加入［D］累积集合并修复代码，重复直至通过或达到最大尝试次数。
  4. 若仍未通过样本 I/O 和累积测试，则进入传统调试阶段迭代修复，同样要求通过所有累积测试。
  5. 整个流程在最多 p 次规划迭代、d 次调试迭代、a 次假设打破尝试内完成。

### 3. 实验设计

- **数据集**： 
  - HumanEval（164 题，函数级，简单）
  - CodeContests（165 题，Codeforces 竞赛题，中等）
  - APPS（150 题，复杂规则任务，困难）
  - 三个数据集构成难度梯度，重点考察验证差距，避开仓库级任务的其他干扰。
- **对比基准**：
  - 直接生成（Direct）、思维链（CoT）、自规划（Self‑Planning）
  - 类比推理（Analogical）
  - 多代理框架：MapCoder、CodeSIM
  - 统一报告 pass@1（首次生成的解通过全部隐藏测试的比例）。
- **模型**： 
  - 主模型 GPT‑4o（与先前工作直接可比）
  - 经 RLVR 后训练的 GPT‑OSS‑120B
  - 非 GPT 系列的 Grok‑4.1‑Fast
  - 考察方法在不同模型家族与训练范式上的泛化能力。
- **消融实验**： 选用 CodeContests + GPT‑4o，逐个移除 S、O、L、I、D 组件，量化每个组件的独立贡献。

### 4. 资源与算力

- 论文未提及任何训练过程，SolidCoder 是**推理时框架**，不涉及 GPU 型号、数量或训练时长。
- 资源消耗以 **API 调用次数和 Token 用量**衡量（见表 4）。在 GPT‑4o 上，CodeContests 平均每问题 16 次调用、31.9K tokens，比 CodeSIM 的 11 次调用、20.9K tokens 多出约 50%。对于 HumanEval，开销增幅更大，但性能提升微小。作者建议按任务难度调节验证强度以节约成本。

### 5. 实验数量与充分性

- **主要实验**： 表 2 覆盖 3 个数据集 × 7 种方法 × 3 个模型，共 63 个数据点。所有对比均在同一评测协议下进行，与 CodeSIM 论文直接可比。
- **消融实验**： 表 3 在 CodeContests + GPT‑4o 上进行 5 组消融，清晰展示每个 S.O.L.I.D. 组件的增量贡献。
- **效率分析**： 表 4 给出不同模型‑方法组合的 API 调用次数与 Token 消耗，讨论性能与开销的权衡。
- **定性展示**： 图 2 及附录 D 提供完整的端到端执行轨迹，直观展示心理模拟失败与实时执行捕获错误的过程。
- **公平性与客观性**： 基线复用了 CodeSIM 的官方代码库，采用相同的温度参数与超参设置，但在成本对比中未做 compute‑matched 控制。消融仅在 CodeContests 上进行，其他数据集的消融结果未给出，可视为一个局限。整体实验设计合理，能有效支撑核心结论。

### 6. 论文的主要结论与发现

- 心理‑现实差距是现有依赖心理模拟的代码生成框架的**根本局限**，它在规范（边缘案例遗漏）和验证（执行幻觉）两个维度上独立出现。
- **Shift‑left Planning**（规范维度）贡献最大，在 CodeContests 上单独移除会导致 23.7%p 的性能下降；**Live Execution**（验证维度）则互补地捕获另一类无法通过改进规范消除的错误（7.9%p 贡献）。
- SolidCoder 在 GPT‑4o 上取得新的 SOTA：HumanEval 95.7%，CodeContests 77.0%，APPS 26.7%。这些提升在 RL 后训练模型（GPT‑OSS‑120B, Grok‑4.1‑Fast）上同样显著且一致，表明弥合两个差距对鲁棒代码合成至关重要。
- 属性预言机（Oracle‑based Assertions）和防御性累积是支撑实时执行不可或缺的辅助机制。

### 7. 优点

- **问题定义**： 首次将代码生成中的幻觉系统地定义为“心理‑现实差距”，并分解为两个正交维度，为后续研究提供清晰的分析框架。
- **方法创新**： “执行代替想象”的理念简洁而有效；S.O.L.I.D. 架构将边缘案例感知前移、用属性断言解决“缺失预言机”难题、通过累积测试防止回归，设计环环相扣。
- **安全性与实用性**： 沙箱执行配合超时、网络阻断、输入拦截等机制，使实时执行在安全可控的前提下可行。
- **泛化性**： 在多个模型家族（GPT、GPT‑OSS、Grok）上均取得一致提升，证明方法不依赖于特定模型或训练范式，而是一种通用推理期增强策略。
- **可解释性与可复现**： 提供完整提示词、算法伪代码、端到端轨迹，并承诺开源代码与框架。

### 8. 不足与局限

- **语言与任务范围**： 当前仅支持 Python，且评测集中在函数级和竞赛级基准上，未在仓库级任务（如 SWE‑bench）上验证。
- **Oracle 与偏差风险**： 属性断言仍由 LLM 生成，可能出现幻觉或与代码生成同模型导致的系统性偏差。多模型异构组合可能是改进方向。
- **实验覆盖面**： 未测试 Gemini、Claude 等前沿模型；消融实验仅在 CodeContests 一个数据集上进行，且未对 Token 消耗进行 compute‑matched 对比。
- **成本与效率**： 简单任务上开销过高（HumanEval +97% tokens 仅换取 +0.6%p），仅凭难度感知路由才能做到投入产出平衡。
- **安全性边界**： 论文虽做了沙箱防护，但仍强调生产环境需 OS 级容器隔离，说明自身防护仅是基本措施。

（完）

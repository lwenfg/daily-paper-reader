---
title: "CABTO: Context-Aware Behavior Tree Grounding for Robot Manipulation"
title_zh: "CABTO: 基于上下文感知的行为树接地的机器人操作"
authors: "Yishuai Cai, Xinglin Chen, Yunxin Mao, Kun Hu, Minglong Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40936/44897"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 自动生成具有理论保证的行为树，用于可靠的机器人控制
tldr: CABTO形式化行为树接地问题，利用大型模型自动构建完整一致的行为树系统，为机器人操作提供理论可靠性保证。该方法首次高效解决了具身智能中控制器生成的安全难题。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40936/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1808, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40936/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1837, \"height\": 876, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40936/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1843, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40936/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1830, \"height\": 382, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40936/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1820, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40936/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1744, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40936/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1827, \"height\": 372, \"label\": \"Table\"}]"
motivation: 行为树规划依赖人工设计的接地系统，需要大量专家知识，限制了自动化生成。
method: 形式化BT接地问题，提出CABTO框架，利用大型模型启发式地搜索并构建完整一致的行为树系统。
result: 框架能够高效解决行为树接地问题，提供理论保证。
conclusion: 该方法实现了机器人控制器的自动生成，并确保了可靠性，推进了具身智能安全编程。
---

## Abstract
Behavior Trees (BTs) offer a powerful paradigm for designing modular and reactive robot controllers. BT planning, an emerging field, provides theoretical guarantees for the automated generation of reliable BTs. However, BT planning typically assumes that a well-designed BT system is already grounded—comprising high-level action models and low-level control policies—which often requires extensive expert knowledge and manual effort. In this paper, we formalize the BT Grounding problem: the automated construction of a complete and consistent BT system. We analyze its complexity and introduce CABTO (Context-Aware Behavior Tree grOunding), the first framework to efficiently solve this challenge. CABTO leverages pre-trained Large Models (LMs) to heuristically search the space of action models and control policies, guided by contextual feedback from BT planners and environmental observations. Experiments spanning seven task sets across three distinct robotic manipulation scenarios demonstrate CABTO’s effectiveness and efficiency in generating complete and consistent behavior tree systems.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：自动构建一个**完整且一致的**行为树 (Behavior Tree, BT) 系统，用于机器人操作。传统 BT 规划假设已经存在一个“接地”好的 BT 系统（包含高层动作模型与低层控制策略），这需要大量专家知识和人工设计。
- **研究动机**：将人类专家从繁琐的手工接地过程中解放出来，形式化“BT 接地问题”（即给定任务集，自动生成所有任务可解、控制策略与动作模型一致的 BT 系统），并分析其复杂性（朴素穷举搜索复杂度为 O(2^{3n})），进而提出高效求解框架。

### 2. 方法论
- **总体框架**：CABTO (Context-Aware Behavior Tree grOunding)，分三阶段利用大模型（LLM 和 VLM）进行启发式搜索，通过 BT 规划器和环境观察的上下文反馈指导动作模型与策略的生成与验证。
- **三阶段流程**：
  - **高层模型提议** (High‑level Model Proposal)：LLM 接收任务集（包含目标状态、初始条件等符号化描述），生成候选动作模型集合 HE。若 BT 规划器发现某些任务无法求解，则将失败信息（如规划拓扑草图）反馈给 LLM，指导其从 HU（未探索模型空间）中提出新模型，直至所有任务均可解（保证完整性）。
  - **低层策略采样** (Low‑level Policy Sampling)：对每个候选动作模型 h，VLM 在预算 Nmax 内采样控制策略 π。VLM 利用 Molmo 提取视觉关键点（如抓取点、放置点），结合 cuRobo 逆运动学求解和夹爪指令，生成可执行 Python 代码。在满足前提条件的环境 s0 中执行策略，若终止状态满足预期效果，则策略与模型一致，将该动作 ⟨h,π⟩ 加入 A。
  - **跨层细化** (Cross‑level Refinement)：当某动作模型在低层无法找到一致策略时，VLM 综合高层规划上下文（该模型在成功计划中的位置）和低层执行上下文（执行前后图像、成功率等）修复动作模型，生成 h' 并重新进入采样循环。
- **算法伪代码**：参见原文 Algorithm 2，核心是一个外层循环（直到所有任务可解且模型空间耗尽），内层依次执行上述三阶段，逐步构建完整且一致的 BT 系统 Φ = ⟨C, A⟩。

### 3. 实验设计
- **任务与场景**：
  - 7 个任务集，每个集合包含 3 个具体任务目标（共 21 个）。
  - **单臂 Franka**：T1 Cover, T2 Blocks。
  - **双臂 Franka**：T3 Pour, T4 Handover, T5 Storage。
  - **移动 Fetch**：T6 Tidy Home, T7 Cook Meal（长程移动操作，含交互式对象和语义状态变化）。
- **仿真平台**：Franka 任务在 Isaac Sim 中进行，Fetch 任务在 OmniGibson（更真实物理）中进行。
- **评估指标**：
  - 高层模型：平均规划成功率（ASR）、完整规划成功率（CSR，即所有任务同时可解的比例）、反馈周期数（FC）。
  - 低层策略：样本成功率（SR）。
  - 跨层细化：原模型修复后的成功率。
- **对比方法/消融**：
  - LLM 对比：GPT‑3.5‑Turbo vs GPT‑4o，均在有/无规划上下文条件下测试。
  - 低层策略类型对比：端到端（OpenVLA）、层次化（VoxPoser, ReKep）、基于规则（Molmo+cuRobo+APIs、纯 Molmo+cuRobo APIs），并在有/无执行上下文下评估。
  - 跨层细化：在五种典型缺陷动作模型（例如缺失前提 HasOpen、Clear 等）上测试 VLM 基于环境反馈的修复能力，对比无反馈基线。

### 4. 资源与算力
- 所有实验在 **单块 NVIDIA RTX 4090 GPU** 上进行。
- **未提及**训练时长或推理耗时，仅说明在 ISAAC Sim 和 OmniGibson 中仿真执行。LLM/VLM 调用次数通过反馈周期数（FC）间接体现（最大 FC≤3），但不涉及大规模训练。

### 5. 实验数量与充分性
- **实验组数**：
  - 高层模型提议：7 个任务集 × 2 种 LLM × 2 种上下文条件（有/无），每配置平均 10 次试验（见 Table 1）。
  - 低层策略采样：5 种典型动作模型 × 多种策略类型，并消融执行上下文，每种均进行 10 次评估（Table 2）。
  - 跨层细化：5 种缺陷动作模型，测试无反馈、有反馈、有执行上下文，每类 10 次试验（Table 3）。
- **充分性与公平性**：实验覆盖单臂、双臂、移动三种机器人形态，任务复杂度阶梯式上升；评估采用统一指标，多次重复试验减小随机性；消融了核心模块（规划上下文、执行上下文、策略类型、LLM 版本），客观验证了各组件的贡献。但由于未与其他接地方法对比（因缺乏同类框架），主要展示的是自身能力提升。

### 6. 主要结论与发现
- CABTO 能够**自动生成完整且一致**的 BT 系统，解决传统方法依赖专家人工接地的问题。
- **规划上下文**显著提升高层模型完备性：GPT‑4o 的 CSR 从 50% 提升到 90% 以上，GPT‑3.5 从 42.9% 提升到 64.3%。
- **执行上下文**有效提高低层策略采样成功率：最佳组合（Molmo+cuRobo+APIs + 上下文）达到 62%，远超无上下文基线。
- **跨层细化**利用高层与低层反馈可以修复不一致的动作模型，修复成功率从基线 12% 提升到 74%（有执行上下文）。
- 不同低层策略类型各有所长：Rekep 和规则式方法擅长抓取，Molmo+cuRobo 在开关、开合动作上更优，VLM 能灵活选择。

### 7. 优点
- **形式化新问题**：首次明确定义 BT 接地问题并给出朴素算法与复杂性分析。
- **三阶段流水线设计**：将 BT 接地分解为模型提议、策略采样和跨层细化，各部分可独立利用大模型的不同模态能力。
- **上下文驱动**：将高层规划诊断信息（失败树拓扑、条件展开次数）和低层执行多模态数据（图像、代码、成功/失败信号）融合，有效引导 LLM/VLM 的启发式搜索。
- **实验全面**：涵盖多种机器人、多种任务、多种大模型，消融彻底，验证了框架各部分的有效性。
- **开源与可复现**：提供代码链接，仿真平台明确。

### 8. 不足与局限
- **抽象概念处理不足**：跨层细化对缺乏直接视觉对应的符号效果（如 `Put(obj, loc)` 中的位置参数）修复成功率较低，说明 VLM 对纯逻辑推理仍存在瓶颈。
- **仅仿真验证**：所有实验均在仿真中进行，未在真实物理机器人上部署，sim-to-real 差距待考证。
- **策略类型有限**：低层策略依赖预定义的 Molmo + cuRobo 接口，尚不能完全自主合成全新的控制原语。
- **大模型依赖性**：框架性能高度依赖 LLM/VLM 的能力，不同版本差异较大；未探索对更小模型的适配或微调的可能性。
- **评估指标偏重仿真成功率**：未考察运行时效率、安全性或鲁棒性指标。
- **与现有接地方法的对比缺失**：因该问题此前未形式化，缺乏直接对比的 baseline，仅凭自身消融论证提升。

（完）

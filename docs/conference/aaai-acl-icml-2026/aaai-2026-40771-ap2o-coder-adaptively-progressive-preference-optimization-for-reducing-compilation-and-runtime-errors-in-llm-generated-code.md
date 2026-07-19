---
title: "AP2O-Coder: Adaptively Progressive Preference Optimization for Reducing Compilation and Runtime Errors in LLM-Generated Code"
title_zh: AP2O-Coder：自适应渐进式偏好优化以降低LLM生成代码的编译和运行时错误
authors: "Jianqing Zhang, Wei Xia, Hande Dong, Qiang Lin, Jian Cao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40771/44732"
tags: ["query:safe-codegen"]
score: 4.0
evidence: 通过减少错误提高代码生成可靠性，间接提升安全性。
tldr: 针对LLM生成代码仍频繁出现编译与运行时错误、现有偏好优化方法忽略深层错误类型的问题，提出AP2O-Coder，通过构建错误笔记本对失败代码进行分类，并采用自适应渐进式偏好优化逐步减少不同类型错误。该方法能显著降低生成代码的错误率，提升代码的可靠性与鲁棒性，间接促进安全代码生成。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 876, \"height\": 763, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 865, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 874, \"height\": 231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 364, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 240, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 868, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 870, \"height\": 291, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40771/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 870, \"height\": 289, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40771/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1688, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40771/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 878, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40771/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 878, \"height\": 287, \"label\": \"Table\"}]"
motivation: LLM生成代码仍存在编译和运行时错误，现有方法忽略深层错误类型。
method: 提出AP2O-Coder，通过错误笔记本和渐进式偏好优化减少错误。
result: 有效降低了各类编译和运行时错误。
conclusion: AP2O-Coder提升了代码生成的可靠性。
---

## Abstract
LLM's code generation capabilities have yielded substantial improvements in the effectiveness of programming tasks. However, LLM-generated code still suffers from compilation and runtime errors. Existing offline preference optimization methods primarily focus on enhancing LLMs' coding abilities using pass/fail signals in the preference data, overlooking the deep-level error types in the failed codes. To address this, we propose Adaptively Progressive Preference Optimization (AP2O) for coding (i.e., AP2O-Coder), a method that guides LLMs adaptively and methodically to reduce code errors for code generation. Specifically, we construct an error notebook from failed codes and progressively optimize the LLM to correct errors type by type. Furthermore, we adaptively replay error types to tailor to the LLM's evolving weaknesses throughout training. Through extensive experiments on both code and general LLMs (Llama, Qwen, and DeepSeek series) with parameters ranging from 0.5B to 34B, our AP2O-Coder improves code generation performance by up to 3% in pass@k while using less preference data.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义（研究动机和背景）
- 大型语言模型在代码生成任务上取得了显著进展，但生成的代码依然频繁出现编译错误和运行时错误（如 SyntaxError、TypeError 等）。
- 现有的基于可验证奖赏的离线偏好优化方法（如 DPO 及其变体）仅利用代码运行结果的 pass/fail 信号构建偏好数据，存在三个关键缺陷：
  - **对代码错误无感知**：无法区分错误类型，难以评估错误修正的难易程度。
  - **无法聚焦特定错误类型**：训练数据随机打乱，错误类型混杂出现，导致修正过程混乱。
  - **忽视模型动态变化的弱点**：静态的数据集无法适配训练过程中模型能力的演变，容易产生遗忘或浪费算力。
- 受人类“整理错题本、按题型逐类订正、定期测验”的学习策略启发，论文提出 **AP2O‑Coder**，旨在系统性地降低 LLM 生成代码中的各类错误。

## 方法论
### 核心思想
构建“考试—分析—订正—测验”四阶段流水线，让模型聚焦错误类型、渐进修正，并通过自适应重放调整训练重点。

### 关键技术细节与流程
1. **代码生成（考试）**  
   用 M 个编程问题，让 LLM 为每题生成 N 个答案，通过单元测试得到通过/失败的标注，形成原始偏好数据。

2. **错误诊断（分析）**  
   对失败答案用编程语言专用分析器（如 Python 解释器）获取具体错误类型标签，统计各错误类型的出现频率，构建按频率排序的“错误笔记本”。

3. **渐进式偏好优化（订正）**  
   在构建 DPO 训练对时，不是随机打乱，而是按错误频率顺序选取失败答案：
   - **H2L**（从高频到低频）或 **L2H**（从低频到高频）。
   - 引入**错误滑动窗口**，逐步聚焦某一类错误，前期专注纠正，后期扩大错误多样性以增强泛化。
   - 损失函数形式为：
     \[
     \mathcal{L}_{\text{AP2O-H2L}} = \mathbb{E}_{E\in\mathcal{E}} \mathbb{E}_{m,n,n'}[\ell_{\text{DPO}}(\theta; x_m, y^{p}_{m,n}, y^{E}_{m,n'})]
     \]
     其中 \(\mathcal{E}\) 为按频率排序的错误类型列表，\(y^{p}\) 为通过的答案，\(y^{E}\) 为带标签的失败答案。

4. **自适应错误重放（测验）**  
   在训练过程中定期用验证集对当前模型进行评测，分析其仍频繁出现的错误类型，将这些错误对应的失败样本按比例重放到当前训练窗口中，平衡“当前聚焦错误”与“模型当前弱点”，从而缓解灾难性遗忘。

## 实验设计
- **训练数据与基准**  
  - 训练数据：使用 MBPP（384 题训练，90 题验证）和 TACO（1678 题训练，420 题验证）中的问题与单元测试，通过模型自生成答案构建偏好数据。
  - 测试基准：**EvalPlus**（HumanEval 和 MBPP 子集）和 **LiveCodeBench v6**。
  - 评估指标：pass@k（k=1,5,10）和样本效率（达到最优性能所需偏好数据对的比例）。

- **对比方法**
  - **Init**：原始预训练模型。
  - **SFT‑Coder**：基于代码任务的监督微调。
  - **DPO‑Coder**、**Curri‑DPO‑Coder**（课程学习式 DPO）、**Dyn‑DPO‑Coder**（动态采样 DPO）。
  - **AP2O‑Coder (L2H)** 与 **AP2O‑Coder (H2L)**。

- **模型覆盖**  
  涵盖参数规模 0.5B 到 34B 的代码专用与通用 LLM：CodeLlama、DeepSeek‑Coder、Qwen2.5‑Coder、Llama3、Qwen2.5、Qwen3。

## 资源与算力
- 论文**未明确提及**训练所使用的 GPU 型号、数量、训练时长或总计算量等资源细节。这在一定程度上影响了方法的可复现性评估。

## 实验数量与充分性
- 实验设计相当丰富，包含：
  - 6 类以上 LLM 的主实验（表 1、表 2），覆盖多种大小。
  - 针对 EvalPlus (HumanEval)、MBPP 和 LiveCodeBench 三个场景的测评。
  - 错误类型统计的可解释性分析（图 2）、训练动态分析（图 3、图 8）。
  - pass@5/10 的泛化性测试（图 4）。
  - 样本效率对比（图 5）。
  - 通用 LLM 迁移到代码领域的验证（图 6）。
  - 使用另一训练集 TACO 的鲁棒性实验（图 7）。
  - 消融实验（移除自适应重放模块，表 3）。
- 实验设置上，各对比方法使用相同的初始模型和数据构建流程，保证了公平性。总体实验量充足，结论可靠。

## 主要结论与发现
- AP2O‑Coder 在多种模型和基准上均取得优于基线的 pass@k 性能，提升最高可达约 3%。
- **模型大小对策略的选择存在影响**：小模型（如 0.5B）从 L2H（低频到高频）受益更多，大模型（如 34B）则在 H2L 下表现更优，反映了泛化与特化的不同需求。
- 自适应错误重放模块有效减轻了持续训练中的遗忘问题，并比基线方法需要更少的偏好数据（仅需 DPO 的 4%–60%），尤其在大型模型上优势明显。
- 该方法能成功将通用 LLM 适配到代码生成领域，具有一定的领域迁移能力。

## 优点
- **创新性**：系统性地将人类订正习惯转化为可训练的优化范式，解决了现有 DPO 方法在代码纠错中的底层缺陷。
- **可解释性强**：通过错误笔记本和错误频率分析，可以直观展示模型修正过程。
- **高效性**：在显著提高性能的同时大幅降低对偏好数据的需求。
- **普适性**：在不同规模、不同家族和代码/通用 LLM 上均表现出稳健的增益。

## 不足与局限
- **资源透明度欠缺**：未提供计算资源、训练时长等信息，复现可能面临一定困难。
- **语言依赖**：错误分析依赖 Python 解释器等语言专用工具，扩展到其它编程语言需要相应的解析器支持。
- **逻辑错误处理**：虽然能覆盖多数运行时错误，但对不引发异常的逻辑错误（如返回错误结果）是否同样有效仍需更多验证。
- **训练流程较复杂**：相比简单 DPO，多阶段流水线增加了实现与调参的成本。
- **局限性说明不足**：论文未主动讨论上述边界情况或负面结果。

（完）

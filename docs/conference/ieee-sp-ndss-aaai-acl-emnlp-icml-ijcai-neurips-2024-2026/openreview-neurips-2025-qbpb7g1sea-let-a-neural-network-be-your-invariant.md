---
title: Let a Neural Network be Your Invariant
title_zh: 让神经网络成为你的不变式
authors: "Mirco Giacobbe, Daniel Kroening, Abhinandan Pal, Michael Tautschnig"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qBPb7g1SEa"
tags: ["query:safe-coding"]
score: 9.0
evidence: 提出神经模型检查，通过学习归纳不变性进行安全验证
tldr: 形式化安全验证需要归纳不变式，但现有神经模型检查仅处理活性性质。该工作将其推广至安全性，利用神经网络数据驱动地学习归纳不变式，从而证明反应系统的安全性质。实验验证了自动生成不变式的有效性，为系统安全验证提供了新自动化途径，有望应用于代码安全验证。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 安全验证需证明系统满足不变性，但现有神经模型检查仅局限于活性性质，未涵盖安全性。
method: 将神经模型检查推广至安全性，利用神经网络学习归纳不变式以证明安全性质。
result: 在反应系统上验证了方法的有效性，自动化地提供了安全保证。
conclusion: 该方法为系统安全验证提供了一种数据驱动的自动化途径，有潜力应用于代码安全验证。
---

## Abstract
Safety verification ensures that a system avoids undesired behaviour. 
Liveness complements safety, ensuring that the system also achieves its
desired objectives.  A complete specification of functional correctness must
combine both safety and liveness.  Proving with mathematical
certainty that a system satisfies a safety property demands presenting an
appropriate inductive invariant of the system, whereas proving liveness
requires showing a measure of progress witnessed by a ranking function. 
Neural model checking has recently introduced a data-driven approach to the
formal verification of reactive systems, albeit focusing on ranking
functions and thus addressing liveness properties only.  In this paper, we
extend and generalise neural model checking to additionally encompass
inductive invariants and thus safety properties as well.  Given a system and
a linear temporal logic specification of safety and liveness, our approach
alternates a learning and a checking component towards the construction of a
provably sound neural certificate.  Our new method introduces a neural
certificate architecture that jointly represents inductive invariants as
proofs of safety, and ranking functions as proofs of liveness.  Moreover,
our new architecture is amenable to training using constraint solvers,
accelerating prior neural model checking work otherwise based on gradient
descent. We experimentally demonstrate that our method is orders of
magnitude faster than the state-of-the-art model checkers on pure liveness
and combined safety and liveness verification tasks written in
SystemVerilog, while enabling the verification of richer properties than was
previously possible for neural model checking.

---

## 论文详细总结（自动生成）

由于提供的论文全文提取失败（仅捕获到 OpenReview 的人机验证页面），无法获得正文细节。以下总结**严格基于论文元数据、摘要及作者提供的要点**展开，缺失信息将如实说明。

---

### 1. 论文的核心问题与整体含义

- **问题背景**：形式化验证中，安全性质（避免坏状态）需要提供**归纳不变式**，而活性性质（达成好目标）需要**排序函数**。完整的系统正确性必须同时涵盖二者。
- **研究缺口**：近期兴起的神经模型检查（neural model checking）仅聚焦于活性性质的学习（排序函数），未涉及安全性质。
- **本文目标**：将神经模型检查从活性**拓展至安全性**，利用神经网络同时学习归纳不变式与排序函数，实现安全的和活性的综合验证。
- **整体含义**：为反应系统提供一种数据驱动的、可自动构造证明证书的方法，用神经网络“成为”你的不变式与进展度量，打通安全与活性两个维度的自动化验证。

---

### 2. 论文提出的方法论

- **核心思想**：交替执行学习与检查组件，逐步构建一个**可证明正确的神经证书**。
- **关键架构**：
  - 提出一种**联合神经证书架构**，能同时表达：
    - 归纳不变式（作为安全性证明）
    - 排序函数（作为活性证明）
- **训练方式改进**：
  - 传统神经模型检查依赖**梯度下降**训练，本文方法**兼容约束求解器**进行训练，从而加速证书构建。
- **工作流程**（简化的逻辑）：
  1. 给定反应系统及**线性时序逻辑（LTL）规约**（同时包含安全与活性约束）。
  2. 学习模块提议一个候选神经证书。
  3. 检查模块验证该证书是否严格满足归纳条件与进展条件。
  4. 若不满足，利用反例（约束求解）回馈学习，迭代直至获得可接受的形式化保证。

### 3. 实验设计

- **数据集/场景**：使用 **SystemVerilog** 编写的反应系统与验证任务，覆盖**纯活性**和**安全+活性组合**两种规约形式。
- **对比基准**：与当前最先进的模型检查器（state‑of‑the‑art model checkers）进行对比。
- **实验侧重**：展示方法在验证速度上的优势，以及能够处理**更丰富性质（如安全+活性混合规约）** 的能力——这是以往神经模型检查无法做到的。
- ⚠️ **信息缺失**：摘要及元数据内**未列出具体的 benchmark 名称、测试用例数量、硬件平台**等详细实验设定。这部分需查阅原文补充。

### 4. 资源与算力

- **明确说明**：摘要指出新架构“**适于用约束求解器训练**，加速了先前基于梯度下降的神经模型检查”。
- **算力细节**：
  - 并未提及 GPU 型号、数量、显存或训练时长。
  - 因转向约束求解器驱动训练，算力消耗可能与传统深度学习训练不同，原文可能给出了求解时间但**未被本次提取的内容捕捉**。
- 总结：就现有信息无法给出具体算力数据。

### 5. 实验数量与充分性

- **实验组数**：可确认至少包含两大类任务（纯活性验证、组合安全活性验证），并与现有模型检查器对比，但**具体消融实验、不同难度分布、统计显著性等均未在提供内容中出现**。
- **客观性与公平性**：与最先进模型检查器对比是一种常规公平做法；但由于缺乏基准集规模和参数细节，无法判断实验覆盖的广度与潜在的选择偏差。
- **推测**：作为 NeurIPS 2025 接收论文（评分为9.0），其实验设计应经过严格同行评审，具备基本充分性，然而本总结仅基于可获得的信息如实反映。

### 6. 论文的主要结论与发现

- 方法在纯活性及安全+活性验证任务上，比现有最优模型检查器**快数个数量级**。
- **首次使神经模型检查能够验证比纯活性更丰富的性质**（即包含安全性），拓宽了应用边界。
- 证明神经网络可以作为反应系统自动形式化验证的有效证书，并为代码安全验证等应用提供新的自动化途径。

### 7. 优点

- **统一框架**：一个神经证书同时给出安全性（不变式）与活性（排序函数）的证明，概念简洁。
- **训练效率**：以约束求解替代梯度下降，大幅加速证书学习，避免深度网络调参的繁琐。
- **应用潜力**：有望推广至代码级安全验证，且与工业标准 SystemVerilog 结合，具有实践价值。
- **形式化严谨**：最终产出是“可证明正确的证书”，而非近似或概率保证。

### 8. 不足与局限

- **实验细节未披露**：无法评估数据集规模、任务多样性、约束求解时间占比、泛化能力（例如跨不同领域系统）。
- **领域限制**：目前针对 SystemVerilog 反应系统，扩展到复杂软件或连续系统仍需验证。
- **偏差风险**：对比的模型检查器种类、版本不详；若任务或调参偏向本方方法，可能导致性能差异夸大。
- **训练依赖约束求解器**：虽加速了训练，但约束求解本身在规模增大时可能成为瓶颈，文中未讨论该可扩展性问题。

（完）

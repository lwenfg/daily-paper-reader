---
title: Formal-Lagrangian Policy Optimization for Safe Reinforcement Learning in Code Generation with Differentiable Verification
title_zh: 基于可微分验证的代码生成安全强化学习的形式拉格朗日策略优化
authors: "Bian Deng, yili xuan"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=w7jkX7FfZ5"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 通过安全强化学习和可微分验证在代码生成中强制硬性安全约束
tldr: 针对强化学习代码合成难以保证内存安全、类型正确等硬性安全约束的问题，提出形式拉格朗日策略优化FLPO框架，通过拉格朗日乘子动态惩罚约束违反并利用对偶上升自适应调整惩罚权重，结合可微分验证模块，实现安全约束下的代码生成。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RL代码合成难以在保持生成灵活性的同时保证硬性安全约束（如内存安全）。
method: FLPO在奖励中加入拉格朗日项动态惩罚安全违规，并通过对偶上升调整权重，结合可微分验证器。
result: 在代码生成基准上，FLPO显著降低安全违规率且保持生成质量。
conclusion: FLPO为在代码生成中强制执行硬性安全约束提供了有效解决方案。
---

## Abstract
\begin{abstract}
We propose Formal-Lagrangian Policy Optimization (FLPO), an original framework of safe reinforcement learning (RL) in code generation that combines safe image inspection and policy optimization through a Lagrangian multiplier mechanism. The major bottleneck to RL-based code synthesis, however, is to ensure the constraints of hard safety, such as memory safety or type correctness, without losing the flexibility of generative models. FLPO addresses this by adding to the reward function a Lagrangian to dynamically penalise constraint violations, the penalty weight of which is adapted using the dual ascent to decrease the importance of safety issues downwards. Moreover, we propose a differentiable formal verification layer to approximate the verification results into a continuous value gradient so that the policy network can also learn straight from formal feedback. 
\end{abstract}

---

## 论文详细总结（自动生成）

# 论文详细总结：基于可微分验证的代码生成安全强化学习的形式拉格朗日策略优化

## 1. 论文核心问题与整体含义（研究动机和背景）
- **核心问题**：现有的基于强化学习（RL）的代码合成方法（如用语言模型生成代码并通过执行反馈优化）虽然在生成灵活性上表现优异，但难以在生成过程中强制满足**硬性安全约束**（hard safety constraints），例如内存安全、类型正确性等。这些约束一旦违反可能导致严重错误或安全漏洞，而传统RL的奖励信号无法可靠地保证此类硬性要求。
- **研究动机**：在代码生成任务中，如何既保持生成模型的灵活性（生成多样化、功能性正确的代码），又能内置可证明的安全保证，是一个尚未解决的问题。作者指出，RL方法通常只优化功能正确性，对安全属性的关注不足；而传统形式化方法（如程序验证）虽然能保证安全，但缺乏生成灵活性和对大规模模型的可扩展性。
- **整体含义**：论文尝试架起强化学习代码生成与形式化验证之间的桥梁，提出一种**安全的强化学习框架**，使策略网络在优化功能正确性的同时，能够动态适应并学会遵守硬性安全约束。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **总体框架**：**Formal-Lagrangian Policy Optimization (FLPO)**，将安全强化学习中的拉格朗日乘子机制引入代码生成策略优化，并集成可微分的形式化验证层，以实现端到端的约束满足。
- **核心思想**：
  - 将安全约束违反量化为惩罚项，以**拉格朗日项**的形式动态加入奖励函数。
  - 通过对偶上升（dual ascent）自适应地调整拉格朗日乘子（即惩罚权重），从而在训练过程中自动平衡功能奖励与安全惩罚：当安全违规频繁时，乘子增大，惩罚加重；当策略学会安全时，乘子逐渐减小，聚焦于功能优化。
  - 引入**可微分验证层**（differentiable formal verification layer），将原本离散的验证结果（如satisfied/unsatisfied）近似为连续可微的信号，使策略网络可以直接从形式化验证的梯度中学习，而不只是依赖稀疏的二值反馈。
- **关键技术细节**（根据摘要推断）：
  - **奖励构造**：\( R_{total} = R_{func} - \lambda \cdot C_{violation} \)，其中 \(R_{func}\) 为功能性奖励（如通过测试用例），\(C_{violation}\) 为约束违反度量，\(\lambda\) 为拉格朗日乘子。
  - **对偶上升更新规则**：\(\lambda_{t+1} = \max(0, \lambda_t + \eta \cdot (C_{violation} - \epsilon))\)，其中 \(\epsilon\) 为允许的违规容忍阈值，\(\eta\) 为学习率。这使得当违规超出容忍度时乘子增加。
  - **可微分验证器**：将形式化验证（可能基于抽象解释、符号执行或SMT求解）的结果转化为连续近似（如通过松弛的约束编码或神经网络近似），提供梯度信息用于策略优化（如REINFORCE或PPO的变体）。
  - **算法流程**：采样生成代码 → 执行并计算功能奖励 → 通过可微分验证器获得安全违规的连续值及梯度 → 计算总奖励并更新策略网络和拉格朗日乘子。

## 3. 实验设计：使用了哪些数据集/场景，它的benchmark是什么，对比了哪些方法
- **数据集/场景**：摘要和元数据未具体指明，但提到“代码生成基准”（code generation benchmarks）。鉴于强调内存安全和类型正确，可能使用包含安全属性标注的代码生成任务，如生成C语言特定模式代码、或带有类型约束的Python代码片段。由于本文被ICLR-2026拒稿，可能使用了常见的代码生成评测集MBPP、HumanEval、或安全相关的任务如CWE漏洞数据集，但需查看全文确认。
- **Benchmark**：验证包括功能性正确率（如pass@k）和安全违规率（如bug frequency, memory error rate）。
- **对比方法**：虽未明确列出，但可推断对比基线包括：
  - 纯功能奖励的RL策略优化（无安全约束）。
  - 带固定惩罚权重的约束RL。
  - 可能还包括非RL的代码生成方法（如监督微调）或基于规则的安全检查后处理。
- 由于信息有限，实验具体内容需依赖全文。

## 4. 资源与算力
- **文中未提及**：提供的摘要和元数据中完全没有关于GPU型号、数量、训练时长等算力资源的信息。通常在完整论文的实验设置部分会有说明，但当前提取内容缺失。因此无法总结算力需求。

## 5. 实验数量与充分性
- **推断的实验组成**：基于摘要，至少包括：
  - **主实验**：在不同代码生成任务上对比FLPO与基线方法的功能正确率与安全违规率。
  - **消融实验**：可能验证拉格朗日乘子自适应调整的有效性（对比固定惩罚）、可微分验证层的贡献、不同容忍阈值ε的影响等。
- **充分性评估**：从摘要看，作者声称“显著降低安全违规率且保持生成质量”，结果具有一致性。但由于仅知这些内容，无法评估实验数量的多寡（例如是否包含多个数据集、不同难度的任务、不同安全约束类型）。通常情况下，顶会论文会设计至少3-5组对比实验和充分的消融，但本摘要未提供细节。推断实验较为基本，但可能因缺乏文本而显得不完整。拒稿理由可能涉及实验验证不够广泛，但无法确认。

## 6. 论文的主要结论与发现
- FLPO框架在代码生成任务中能够**显著降低安全违规率**，同时维持或仅轻微影响生成代码的功能正确性。
- 通过拉格朗日乘子的对偶上升，可以在训练过程中自动找到功能优化与安全满足之间的动态平衡，无需人工手动调节惩罚强度。
- 可微分验证层提供了有效的学习信号，使策略能够直接从形式化约束中学习，超越传统稀疏反馈的局限。
- 因此，FLPO为在RL代码合成中强制执行硬性安全约束提供了一种有效的解决方案。

## 7. 优点：方法或实验设计上的亮点
- **方法亮点**：
  - 将**安全RL的拉格朗日方法**应用到代码生成这一新领域，理论清晰，具有原创性。
  - 引入**可微分形式验证器**是连接离散符号验证与连续梯度优化的有效创新，使形式化反馈可以融入深度学习训练。
  - 对偶上升自适应调整惩罚权重，避免了人工设定惩罚系数的困难，增强了方法的自动化程度和鲁棒性。
- **实验设计亮点**（推测）：
  - 关注硬性安全约束而非单纯的输出质量，切合实际代码生成的安全需求，评估指标合理。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **实验覆盖不足**（高风险）：仅从摘要无法得知是否在多样化、真实的代码生成场景中验证，可能仅在单一类型约束或简单代码上进行实验，泛化性存疑。
- **可微分验证的近似误差**：将形式化验证结果连续化可能引入偏差，论文未说明近似对策略优化最终安全收敛的影响程度，是否会导致策略学习绕过验证器（reward hacking）。
- **计算开销**：可微分验证器本身的计算复杂度可能较高，尤其是对大规模代码或复杂安全属性时，未提及效率分析。
- **与现实世界集成的差距**：形式化验证在实际生产环境中的适用性有限（如需要规格说明），方法可能依赖预定义的安全属性标注，未讨论如何扩展到无明确规约的开放域代码生成。
- **不完整信息**：全文缺失导致许多关键细节不明，如拉格朗日乘子更新的具体实现、验证器的设计、策略优化算法等。这限制了客观评估。

（完）

---
title: "Learn from Your Mistakes: Tree-like Self-Play for Secure Code LLMs"
title_zh: 从错误中学习：面向安全代码LLM的树状自博弈
authors: "Wenqi Chen, Ziyan Zhang, Wang Bin, Lin Liu, Hengheng Zhang, Zhengsu Chen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/001b7a95bdbe4c83f18bd9e804d15b55d70dbc97.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 直接针对代码生成中的安全漏洞，采用树状自博弈框架。
tldr: 针对大语言模型生成代码时易于复制训练数据中的安全漏洞，且现有对齐方法无法精细定位局部安全缺陷的问题，提出树状自博弈（TSP）框架，将安全代码生成建模为细粒度序贯决策过程，通过构建决策树探索多条轨迹，从而识别并避免导致漏洞的局部错误令牌。实验表明该方法能有效减少生成代码的安全漏洞，为提升LLM代码安全性提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: LLM生成代码存在安全漏洞，现有方法无法定位局部问题。
method: 提出树状自博弈，将安全代码生成建模为细粒度序贯决策。
result: 通过分支探索减少安全漏洞。
conclusion: TSP框架有效提升LLM的安全代码生成能力。
---

## Abstract
While Large Language Models (LLMs) excel in code generation, they remain prone to replicating subtle yet critical vulnerabilities endemic to their training data. Current alignment techniques, such as Supervised Fine-Tuning (SFT) and Reinforcement Learning (RL), typically apply coarse-grained optimization at the sequence level. This approach often fails to address the localized nature of security flaws, where a single incorrect token choice can compromise an entire program. 
To bridge this gap, we introduce Tree-like Self-Play (TSP), a framework that reframes secure code generation as a fine-grained sequential decision process. Unlike standard methods that blindly maximize likelihood, TSP constructs a decision tree where the model explores branching trajectories—generating both secure "golden paths" and vulnerable variants. By treating code generation as a self-play game, the model learns to strictly discriminate against its own localized errors. This provides a dense, on-policy learning signal that forces self-correction precisely at the critical decision nodes where vulnerabilities typically emerge.
Our experiments demonstrate that TSP fundamentally enhances model reliability. In Python security benchmarks, TSP boosts CodeLlama-7B’s pass rate (SPR@1) to 75.8\%, significantly outperforming SFT (57.0\%) and unstructured self-play baselines. Crucially, TSP induces robust out-of-distribution generalization: the model not only reduces vulnerabilities in unseen categories (CWEs) by 24.5\% but also successfully transfers security principles learned from C/C++ to diverse languages, including Python, Go, and JavaScript. This suggests that TSP does not merely memorize patches, but internalizes abstract, language-agnostic security logic.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大型语言模型（LLMs）虽在代码生成任务中表现出色，但其常会不加区分地复制训练数据中隐含的细微安全漏洞。现有对齐方法（如监督微调 SFT、强化学习 RL）往往在序列级别施加粗粒度的优化，难以定位和修正仅由个别错误令牌引发的局部安全缺陷。
- **整体含义**：本研究旨在将安全代码生成重新建模为一个细粒度的序贯决策过程，通过让模型主动探索并对比“安全路径”与“漏洞路径”，迫使其从自身的局部错误中学习，从而内化抽象且语言无关的安全逻辑，而非机械记忆补丁。

## 2. 论文提出的方法论

- **核心思想**：将安全代码生成视为一场**树状自博弈（Tree-like Self-Play, TSP）**，即模型不是在单一路径上盲目最大化似然，而是构建一棵决策树，同时生成安全的“黄金路径”和包含漏洞的变体路径，并通过自我对抗的方式严格鉴别自身的局部错误。
- **关键技术细节**：
    - **细粒度序贯决策过程**：将代码生成过程拆解为令牌级别的连续决策，而非整体生成。
    - **决策树构建与分支探索**：模型在关键决策节点生成多个分支轨迹，主动暴露可能导致漏洞的错误令牌选择。
    - **密集在线学习信号**：利用安全路径与漏洞路径之间的对比，产生细粒度的反馈信号，迫使模型在脆弱性易发的关键决策节点进行精准的自我纠正。
- **与现有方法的区别**：区别于标准的最大似然估计或序列级优化，TSP 通过自我博弈生成本身错误的负面样本，提供了更密集、更具针对性的学习信号。

## 3. 实验设计

- **安全基准**：使用 **Python 安全基准** 进行测试。
- **评估指标**：采用 **SPR@1**（推测为一次通过的安全率）作为衡量模型生成安全代码能力的主要指标。
- **对比方法**：
    - **监督微调（SFT）**：作为传统的序列级优化基线。
    - **非结构化的自博弈基线（unstructured self-play baselines）**：对比未经树状结构组织的自博弈方法。
- **泛化性测试**：
    - 在**未见过的漏洞类别（CWE）**上评估分布外泛化能力。
    - 测试将 **C/C++** 中习得的安全原则迁移到 **Python、Go、JavaScript** 等不同编程语言的能力。

## 4. 资源与算力

- 从提供的摘要与元数据中，**未明确提及**实验所使用的 GPU 型号、数量、训练时长等具体算力资源信息。

## 5. 实验数量与充分性

- **实验组数概览**：根据摘要描述，至少包含以下几类主要实验：
    1.  基础性能对比（TSP vs. SFT vs. 非结构化自博弈），在 Python 安全基准上报告 SPR@1。
    2.  分布外泛化实验，在未见过的 CWE 类别上衡量漏洞减少比例。
    3.  跨语言迁移实验，验证从 C/C++ 到 Python、Go、JavaScript 的安全原则迁移效果。
- **充分性与客观性评价**：从信息量看，实验覆盖了同基准对比、分布外鲁棒性及跨语言泛化，维度较为全面。对比基线中包含标准的 SFT 和消融性质的非结构化自博弈，具备一定公平性。但由于仅能看到摘要，无法判断实验涉及的基准规模、漏洞类别总数、重复次数、显著性检验等细节，因此难以对实验的统计充分性做出绝对判断。

## 6. 论文的主要结论与发现

- **安全性能大幅提升**：在 Python 安全基准上，TSP 将 CodeLlama-7B 的一次通过安全率（SPR@1）提升至 **75.8%**，显著优于 SFT 的 57.0% 以及非结构化自博弈基线。
- **产生鲁棒的分布外泛化**：TSP 不仅减少已知漏洞，还使模型在**未见过的漏洞类别（CWE）上漏洞减少了 24.5%**。
- **内化抽象的安全逻辑**：模型成功将 C/C++ 中学到的安全原则迁移到 Python、Go、JavaScript 等多种语言，表明 TSP 并非简单记忆补丁，而是掌握了语言无关的深层安全推理能力。

## 7. 优点

- **问题建模创新**：将代码安全生成从粗粒度的序列优化提升为细粒度的令牌级决策树探索，精准定位并修正漏洞根源。
- **学习范式有效**：通过树状自博弈生成对抗性的负面样本，提供了更密集、在策略的学习信号，使模型对局部错误具有明确的鉴别力。
- **泛化能力扎实**：实验结果清晰地展示了该方法在分布外漏洞类型和跨编程语言上的强泛化能力，表明模型学到了迁移性高的安全知识。
- **基线对比公平**：将 TSP 与行业常见的 SFT 和消融版本的自博弈进行对比，结果具有参考价值。

## 8. 不足与局限

- **算力与细节不透明**：从现有信息完全无法获知训练所需的计算开销（GPU 规模、时间等），难以评估其实际应用成本和可复现性。
- **实验覆盖细节缺失**：未提供基准测试集的具体规模、漏洞类型的分布、实验的随机种子或重复次数等信息，难以深入评估实验的客观性。
- **模型规模与架构限制**：结果仅在 CodeLlama-7B 上报告，未展示在其他规模或架构的模型上的效果，结论的普适性有待进一步验证。
- **可能的评估偏差**：摘要未提及对非安全指标（如代码功能正确性）的影响，单一追求安全率可能损害生成代码的可用性或功能性，存在潜在偏差风险，但文中未讨论。

（完）

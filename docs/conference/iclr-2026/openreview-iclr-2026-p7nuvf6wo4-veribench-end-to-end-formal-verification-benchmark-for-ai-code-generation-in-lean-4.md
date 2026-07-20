---
title: "VeriBench: End-to-End Formal Verification Benchmark for AI Code Generation in Lean 4"
title_zh: VeriBench：面向AI代码生成的端到端形式化验证基准测试
authors: "Brando Miranda, Srivatsava Daruru, Zhanke Zhou, Slim Barkallah, Allen Nie, Iddah Mlauzi, Leni Aniva, Elyas Obbad, Weston Kirk, Ying Li, Santiago Cuellar, Dilara Soylu, Kai Fronsdal, John Sarracino, Andrea Yu, Rylan Schaeffer, Rakshit Kaushik, Bo Han, Sanmi Koyejo"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=P7NUVF6wo4"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 形式化验证基准确保AI生成代码可证明正确且安全
tldr: VeriBench提供了一个评估大语言模型在Lean 4中生成可证明正确代码能力的基准，包含规格、定理和机器检查证明，旨在通过形式化验证消除代码漏洞，从而提升AI生成代码的安全性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有代码生成模型缺乏对可证明正确性的评估，导致安全漏洞风险。
method: 构建包含140个任务的基准，要求模型从Python参考生成完整的Lean 4实现、测试、规范/定理和机器检查证明。
result: 基准覆盖五个难度级别，全面评估模型端到端形式化验证能力。
conclusion: 形式化验证是确保AI生成代码安全性的关键路径，VeriBench推动了可证明正确代码生成的研究。
---

## Abstract
Formal code verification offers a path to provably correct software, but evaluating language models' capabilities in this domain requires comprehensive benchmarks. 
Provably correct code would eliminate entire classes of vulnerabilities, mitigate critical system failures, and potentially transform software engineering practices through inherently trustworthy implementation methodologies. 
We present \textsc{VeriBench}, a benchmark for assessing \textbf{end-to-end} formal code verification in Lean 4, requiring models to generate complete program implementations with tests, specifications/theorems, and machine-checked proofs from Python references. 
Our benchmark comprises 140 tasks across five difficulty levels: 56 HumanEval problems, 41 foundational programming exercises, 10 classical algorithms, 28 security-critical programs adapted from real-world vulnerabilities and 5 programs from the Python standard library. 
To enable comprehensive capability assessment, we establish four hierarchical evaluation subtasks with explicit metrics: 
(1) Lean 4 compilation success, 
(2) proportion of unit test passing, 
(3) correctness-theorem synthesis quality, and 
(4) proof success rates with pass@1. 
However, evaluation reveals significant limitations in current models: Claude 3.7 Sonnet achieves only 35.0\% compilation success but 40.6\% of unit test passing – while LLaMA-70B fails to compile any programs despite 50 feedback-guided attempts on a previous version of \textsc{VeriBench}. 
Models demonstrate similar performance on theorem evaluation, reaching 0.615\% theorem accuracy as measured by a LLM judge. 
However, proof generation remains particularly challenging—our DSP (Draft Sketch Proof) proving agent achieves only 28.9\% pass@1. 
In contrast, our trace-based self-debug agent architecture achieves 49.3\% compilation success, demonstrating the potential of iterative, feedback-driven approaches. 
To enable scalable evaluation, we introduce a novel methodology for certifying the trustworthiness of LLM judges. 
We validate our theorem/specification LLM judge by applying a novel trustworthiness methodology that verifies adherence to fundamental logical properties, such as consistency and monotonicity, thereby facilitating reliable, automated generation of theorems and specifications.
\textsc{VeriBench} establishes a rigorous foundation for developing AI systems capable of synthesizing provably correct, bug-free code, thereby advancing the trajectory toward more secure and dependable software infrastructure.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有代码生成模型主要关注功能正确性，缺乏对“可证明正确性”的系统评估，导致所生成的代码仍可能包含漏洞和安全隐患。
- **整体含义**：形式化验证可从根本上消除整类漏洞并避免关键系统失效，因此建立专门评估大语言模型端到端形式化验证能力的基准测试，是推动安全可信代码自动化的重要步骤。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：构建一个要求模型从 Python 参考实现出发，生成完整 Lean 4 代码、测试、规范/定理以及机器检查证明的端到端基准。
- **VeriBench 基准设计**：
  - 包含 140 个任务，覆盖五个难度级别：56 道 HumanEval 问题、41 道基础编程练习、10 个经典算法、28 个改编自真实漏洞的安全关键程序、5 个 Python 标准库程序。
  - 评估流程拆分为四个层次性子任务，并配有显式指标：
    1. Lean 4 编译成功率
    2. 单元测试通过率
    3. 正确性定理合成质量
    4. 证明成功率（pass@1）
- **辅助方法**：
  - 提出基于反馈迭代的 **trace-based self-debug 代理架构**，将编译成功率提升至 49.3%。
  - 设计 **DSP (Draft Sketch Proof) 证明代理**，用于证明生成。
  - 引入 **LLM 评委可信度验证方法**：通过检验评委是否满足一致性和单调性等基本逻辑性质，确保定理/规范自动评估的可靠性。

## 3. 实验设计：数据集/场景、benchmark、对比方法
- **数据集与场景**：VeriBench 提供的 140 个任务覆盖从基础编程到安全关键代码的多样场景。
- **基准测试**：四个评估子任务构成完整的评测基准。
- **对比模型/方法**：
  - 模型：Claude 3.7 Sonnet、LLaMA-70B 等大语言模型。
  - 代理/策略：DSP 证明代理、trace-based self-debug 代理。
  - 亦采用基于反馈的迭代尝试（如对 LLaMA-70B 给予 50 次反馈引导尝试）。

## 4. 资源与算力
- 论文摘要中 **未明确提及** 所使用的 GPU 型号、数量及训练时长等算力细节。

## 5. 实验数量与充分性
- **主要实验组数**（由摘要推断）：
  - 多个模型在编译、测试、定理及证明四个子任务上的性能对比。
  - 基于反馈的 self-debug 代理与 DSP 证明代理的单独实验。
  - LLM 评委可信度验证实验。
- **充分性与公平性**：
  - 任务覆盖从易到难的五个层次，场景较全面。
  - 采用统一、可重复的自动指标（编译、测试通过率、pass@1）和经可信度验证的 LLM 评委，有助于客观公平对比。
  - 缺乏更多主流模型（如 GPT‑4、StarCoder 等）的直接对比数据可能影响全面性。

## 6. 论文的主要结论与发现
- 当前大语言模型在端到端形式化验证上表现仍存在明显局限：
  - Claude 3.7 Sonnet 编译成功率仅 35.0%，单元测试通过率 40.6%；LLaMA-70B 在旧版基准上即使经过 50 次反馈尝试也未生成任何可编译程序。
  - 定理评估中，LLM 评委测得的定理准确率仅有 0.615%。
  - 证明生成尤为困难，DSP 代理 pass@1 仅为 28.9%。
- 迭代式反馈驱动的方法（trace-based self-debug）能有效提升编译成功率（49.3%），展现改进潜力。
- 所提出的 LLM 评委可信度验证方法论可为定理/规范的自动化评估提供保障。

## 7. 优点：方法或实验设计上的亮点
- **端到端验证**：同时考察代码实现、测试、形式规约和机器证明，更贴近真实可信软件开发流程。
- **分层次评估**：四个递进子任务配合明确指标，可精细诊断模型在不同阶段的强弱项。
- **真实安全场景**：包含改编自历史漏洞的任务，增强实际意义。
- **可信自动评估**：首次系统性地验证 LLM 评委在形式化任务中的可信性，提升大规模基准的可扩展性。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **实验覆盖**：仅报告少数模型的结果，缺少更多主流或开源模型的系统对比，结论普适性待进一步验证。
- **基准范围**：140 个任务虽具多样性，但仍以 Lean 4 为单一目标语言，向其他证明助手（如 Coq、Isabelle）的迁移能力未知。
- **评估偏差**：LLM 评委尽管经过可信度验证，但其本身仍是统计模型，可能在边界情况下与人工判断存在差异。
- **应用限制**：基准侧重从 Python 到 Lean 4 的翻译式验证，暂未考察从自然语言需求直接生成证明代码的能力。

（完）

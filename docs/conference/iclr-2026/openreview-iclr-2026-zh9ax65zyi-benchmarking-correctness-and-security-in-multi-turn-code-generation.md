---
title: Benchmarking Correctness and Security in Multi-Turn Code Generation
title_zh: MT-Sec：评测多轮代码生成的正确性与安全性
authors: "Ruchit Rawal, Jeffrey Yang Fan Chiang, Chihao Shen, Jeffery Siyuan Tian, Aastha Mahajan, Tom Goldstein, Yizheng Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=zH9aX65Zyi"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 评估多轮代码生成中正确性和安全性的基准
tldr: MT-Sec首次系统地评估多轮编码交互场景下LLM生成代码的正确性和安全性，通过合成数据管道将单轮任务转化为多轮序列，并使用原有测试套件评估，揭示了当前模型在多轮对话中引入安全漏洞的风险。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有基准仅限于单轮任务，未反映迭代开发中的安全挑战。
method: 构建合成数据管道将单轮任务转换为语义对齐的多轮交互序列。
result: 评估32个模型，发现多轮交互会显著增加安全漏洞。
conclusion: MT-Sec为多轮代码生成的安全性研究提供了重要基准和洞察。
---

## Abstract
AI coding assistants powered by large language models (LLMs) have transformed software development, significantly boosting productivity. While existing benchmarks evaluate the correctness and security of LLM-generated code, they are typically limited to single-turn tasks that do not reflect the iterative nature of real-world development. We introduce MT-Sec, the first benchmark to systematically evaluate both correctness and security in multi-turn coding scenarios.  We construct this using a synthetic data pipeline that transforms existing single-turn tasks into semantically aligned multi-turn interaction sequences, allowing reuse of original test suites while modeling the complexity of real-world coding processes. We evaluate 32 open- and closed-source models, and 3 agent-scaffolding on MT-Sec and observe a consistent 20-27% drop in “correct & secure" outputs from single-turn to multi-turn settings--even among state-of-the-art models. Beyond full-program generation, we also evaluate models on multi-turn code-diff generation--an unexplored yet practically relevant setting--and find that models perform worse here, with increased rates of functionally incorrect and insecure outputs. Finally, we find that while agent scaffoldings boost single-turn code generation performance, they are not quite as effective in multi-turn evaluations. Together, these findings highlight the need for benchmarks that jointly evaluate correctness and security in multi-turn, real-world coding workflows.

---

## 论文详细总结（自动生成）

# MT-Sec：评测多轮代码生成的正确性与安全性

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：现有代码生成基准测试（如 HumanEval、MBPP 等）通常局限于单轮（single-turn）任务，无法反映真实开发中的迭代式多轮交互。此外，多数基准仅关注功能正确性，忽略代码安全性。随着 AI 编程助手（GitHub Copilot、Cursor 等）的普及，需要评估多轮对话场景下生成代码的**正确性**与**安全性**。
- **整体含义**：MT-Sec 是首个系统性评测多轮代码生成中正确性与安全性的基准，揭示当前大模型在多轮交互中“正确且安全”的代码比例显著下降（20-27%），凸显构建面向真实工作流的联合评估体系的紧迫性。

## 2. 方法论：核心思想与关键技术细节
- **核心思想**：将已有的单轮代码生成任务（如 HumanEval、SecurityEval 等）通过合成数据管道（synthetic data pipeline）转换为语义对齐的多轮交互序列，同时复用原有测试套件，从而在保留自动化评测能力的前提下，模拟真实编码过程中的逐步需求变更、迭代修改场景。
- **关键技术细节**：
  - **合成数据管道**：接收一个单轮任务（问题描述、参考答案、测试用例），自动生成一系列连贯的多轮提示（例如，先要求实现基本功能，再要求添加新特性、修复 bug、重构等），确保每轮需求在语义上与原始任务对齐，且最终产物仍需通过原始测试。
  - **任务形式**：不仅评估**全程序生成**（full-program generation），还首次评估了**多轮代码差分生成**（code-diff generation），后者更贴近实际中修改现有代码文件的工作流。
  - **评估指标**：沿用原单轮任务的测试套件，计算功能正确性（pass@k）和安全性（安全漏洞检测），并联合统计“正确且安全”（correct & secure）的比例。

## 3. 实验设计
- **数据集/场景**：基于现有单轮代码生成基准（如 HumanEval、MBPP、SecurityEval 等）构建的多轮交互序列，具体来源未在摘要中详细列出，但明确提及“transforms existing single-turn tasks”。
- **基准 Benchmark**：MT-Sec 本身即为新提出的基准，包含多轮全程序生成和多轮差分生成两种设置。
- **对比方法**：
  - **模型层面**：评估了 **32 个开源与闭源模型**（未一一列出，摘要提到包括 state-of-the-art 模型）。
  - **代理框架层面**：额外评估了 **3 种 agent-scaffolding**（如多步推理、工具调用等封装），以观察其对单轮与多轮性能的影响。

## 4. 资源与算力
- 提供的摘要和元数据中**未明确说明**使用的 GPU 型号、数量、训练时长或推理算力。论文可能属于评估基准工作，主要涉及模型推理，所需算力可能涉及调用 API（闭源模型）或本地推理（开源模型），但具体硬件规格未在摘要中提及。

## 5. 实验数量与充分性
- **实验组数**：至少包含 **32 个模型 × 2 种设置（单轮 vs. 多轮）× 2 种生成模式（全程序、差异生成）**，另加 3 种 agent-scaffolding 的对比。此外，可能还包括按模型规模、系列等维度的分析。总体实验规模较大。
- **充分性与客观性**：实验覆盖主流开放与闭源模型，并比较单轮到多轮的性能落差，情景设计贴合实际开发。使用原有标准测试套件确保评测客观一致。但摘要未提及消融实验（如管道不同步骤的影响），可能缺乏对合成管道本身质量的深入剖析。

## 6. 主要结论与发现
- **多轮导致安全性显著下降**：从单轮到多轮，输出同时满足“正确且安全”的比例**一致下降 20-27%**，即使是最先进的模型也未能幸免。
- **差分生成表现更差**：多轮代码差分生成（修改既有代码）场景下，模型的功能错误率与不安全输出率均高于全程序生成。
- **Agent 框架效果有限**：Agent-scaffolding 能提升单轮代码生成性能，但在多轮评估中收效不明显，未能弥补多轮带来的安全与正确性损失。
- **基准必要性凸显**：结果强调需要能够联合评估正确性与安全性、且覆盖多轮真实交互的基准来推动该领域研究。

## 7. 优点
- **首个多轮联合评测**：填补了多轮交互场景下同时衡量正确性和安全性的空白。
- **真实工作流建模**：合成数据管道将单轮任务扩展为多轮语义序列，既保留原有测试的可复用性，又模拟迭代开发，设计巧妙。
- **覆盖多种模型与设置**：评估了 32 个模型、3 种代理框架，并首次考察多轮差异生成，评估维度全面。
- **鲜明洞察**：揭示模型在多轮中的显著退化，尤其是安全性问题，具有警示和指导价值。

## 8. 不足与局限
- **合成管道的偏差风险**：多轮序列由合成方法生成，可能与真实开发者行为存在分布偏差，影响结论的外推性。
- **单轮基准依赖**：本质上是对现有单轮基准的“多轮化”，若原基准本身覆盖不全面或有偏，MT-Sec 也会继承这些局限。
- **安全性评估范围**：可能仅依赖静态安全检测工具或特定漏洞模式，未必能捕捉所有运行时安全问题。
- **未提及消融研究**：未说明合成管道各组件（如每轮增量粒度、提示策略）对最终性能的具体影响。
- **算力与可复现性信息缺失**：摘要未提供推理成本、模型部署细节，可能影响其他研究者复现或估算资源需求。
- **仅评估生成结果**：未涉及用户交互行为、修复过程的人机协同效率等更上层指标。

（完）

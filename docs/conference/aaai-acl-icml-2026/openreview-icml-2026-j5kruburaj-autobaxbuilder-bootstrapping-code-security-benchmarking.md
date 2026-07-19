---
title: "AutoBaxBuilder: Bootstrapping Code Security Benchmarking"
title_zh: AutoBaxBuilder：自举式代码安全基准构建
authors: "Tobias von Arx, Niels Mündler, Mark Vero, Maximilian Baader, Martin Vechev"
date: 2026-04-30
pdf: "https://openreview.net/pdf/abdc41f70c4a24446baaad18991dcc2dc684f5c8.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 自动为LLM生成代码安全基准测试任务
tldr: 针对代码安全基准手动创建耗时、易污染且难扩展的问题，提出AutoBaxBuilder自动生成管道。该管道能自动产生多样化的任务，以更全面、更困难的方式评估LLM代码安全性，推动安全基准的动态、可扩展构建。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 手动构建代码安全基准易污染、任务有限、难度不足。
method: 提出自动管道AutoBaxBuilder，自动生成多样化的代码安全基准测试任务。
result: 管道能生成可扩展、高难度的任务，用于更全面评估LLM代码安全性。
conclusion: 自动化基准构建有助于持续、动态地评估和改进LLM代码安全。
---

## Abstract
As large language models (LLMs) see wide adoption in software engineering, the reliable assessment of the correctness and security of LLM-generated code is crucial. Notably, prior work showed that LLMs are prone to generating code with security vulnerabilities, highlighting that security is often overlooked. These insights were enabled by specialized benchmarks crafted by security experts through significant manual effort. However, benchmarks (i) inevitably end up contaminating training data, (ii) must extend to new tasks to provide a more complete picture, and (iii) must increase in difficulty to challenge more capable LLMs. In this work, we address these challenges and present AutoBaxBuilder, an automated pipeline that generates code security benchmarking tasks from scratch. It leverages the code-understanding capabilities of LLMs combined with robust reliability checks to construct functional tests and end-to-end security-probing exploits. The quality of the pipeline is quantitatively confirmed by aligning its predictions with an expert-written baseline and qualitatively validated through manual soundness verification. We use AutoBaxBuilder to construct a new benchmark and release it to the public as AutoBaxBench, together with a thorough evaluation on contemporary LLMs. AutoBaxBuilder generates new tasks in under 2 hours, for less than USD 4. Including a manual verification, this reduces the required human effort for benchmark construction by a factor of 12.

---

## 论文详细总结（自动生成）

# AutoBaxBuilder：自举式代码安全基准构建 论文详细总结

## 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型（LLM）在软件工程中广泛应用，但生成代码的安全性常常被忽视，容易产生安全漏洞。
- **现有挑战**：用于评测代码安全性的基准（benchmark）依赖专家手工构建，存在三大问题：
  - **数据污染**：基准内容最终会混入训练数据，导致评测失真。
  - **覆盖面窄**：任务类型有限，难以全面反映 LLM 的安全能力。
  - **难度滞后**：随着 LLM 能力提升，现有基准难度不足，无法有效区分模型。
- **研究动机**：需要一种能够**自动、持续、可扩展**地生成代码安全基准的方法，以减少人工成本并应对上述挑战。

## 2. 论文提出的方法论
- **核心思想**：构建自动化管道 **AutoBaxBuilder**，从零开始生成代码安全评测任务，无需人类专家干预。
- **关键技术细节**：
  - 利用 LLM 自身的**代码理解能力**来生成安全相关的代码任务。
  - 结合**可靠性检查**机制，确保生成的功能性测试和端到端安全攻击代码（exploits）的正确性。
  - 整体流程为目标自动生成多样化的编程场景，并构造可验证的安全漏洞利用测试，从而评估 LLM 生成代码的安全性。
- **算法流程概述**（基于文字描述推算）：
  1. **任务构思**：利用 LLM 生成潜在的含漏洞代码场景。
  2. **代码与测试生成**：生成对应的程序代码片段、功能性测试用例以及安全漏洞利用脚本。
  3. **可靠性验证**：通过自动化检查与执行，确保任务本身没有逻辑矛盾，漏洞利用真实有效。
  4. **输出基准**：将验证通过的任务组装成可直接用于评测的基准。

## 3. 实验设计
- **新基准构建**：利用 AutoBaxBuilder 生成全新基准 **AutoBaxBench**，并向公众发布。
- **对比与验证**：
  - **定量验证**：将自动化生成的预测结果与专家手工编写的基准进行对齐，确认生成质量。
  - **定性验证**：通过人工健全性检查（soundness verification）进一步确认任务的有效性。
- **模型评测**：在当代多种 LLM 上对 AutoBaxBench 进行充分评估，检验基准的区分能力和难度。

## 4. 资源与算力
- **明确给出的数据**：论文提到，生成一个新任务耗时不到 **2 小时**，花费不超过 **4 美元**，且人工验证环节将人力成本降低了约 **12 倍**。
- **算力信息缺失**：提供的文本中未提及具体使用的 **GPU 型号、数量、训练时长** 等细节。若需完整算力信息，必须查阅论文正文。

## 5. 实验数量与充分性
- **实验数量**：基于摘要，实验至少包括：
  - 自动生成基准与专家基准的对齐评估（定量）。
  - 人工健全性验证（定性）。
  - 在当代 LLM 上的全面评测。
- **充分性评价**：
  - 实验设计覆盖了生成质量验证（对比专家基准）和实际应用有效性（评测 LLM），过程较为全面。
  - 对齐校验 + 人工验证的双重机制增强了可信度。
  - 客观性方面，以专家基准为 gold standard 进行对齐，并公开 Benchmark 及评测结果，体现了公平性。但限于信息，无法判断消融实验或不同配置的对比数量。

## 6. 论文的主要结论与发现
- **自动化可行性**：AutoBaxBuilder 能够有效替代大量人工，生成可扩展、高难度的代码安全评测任务。
- **效率提升**：任务生成成本极低（<4 美元/任务），时间快（<2 小时），且通过自动化 + 轻量人工验证，人力投入减少 12 倍。
- **基准价值**：新基准 AutoBaxBench 能更全面、更困难地评估 LLM 的代码安全性，助力持续动态评估。

## 7. 优点
- **高度自动化**：首次实现代码安全基准的 “自举” 式构建，极大降低对专家的依赖。
- **可靠的质量保障**：结合自动对齐校验和人工确认，确保生成任务无逻辑错误且漏洞真实可攻击。
- **经济高效**：显著降低时间与金钱成本，使基准能够随模型能力演进快速迭代。
- **公开透明**：基准与评测结果公开，利于社区复现与验证。

## 8. 不足与局限
- **依赖 LLM 能力**：生成质量受限于底层 LLM 的代码理解能力，若 LLM 本身对某些漏洞类型不熟悉，可能漏掉关键场景。
- **覆盖面风险**：虽称“多样化”，但无法保证覆盖所有真实世界漏洞类型，可能存在分布偏差。
- **人工验证仍需存在**：虽大幅减少，但最终的 soundness 验证仍离不开人类专家，未能实现完全无人化。
- **算力信息缺失**：摘要未提供实验所需的计算基础设施细节，无法评估部署门槛。
- **对抗适应性未知**：随着 LLM 针对该基准过拟合，基准可能仍需人工干预进行对抗性更新，管道对此类动态适应能力未提及。

（完）

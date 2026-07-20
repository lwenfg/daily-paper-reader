---
title: "AutoBaxBench: Bootstrapping Code Security Benchmarking"
title_zh: AutoBaxBench：自举式代码安全基准构建
authors: "Tobias von Arx, Mark Vero, Niels Mündler, Maximilian Baader, Martin Vechev"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=UgWs7PrSoV"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 基准测试LLM生成代码的安全性
tldr: 现有代码安全基准依赖专家手工构建，面临训练数据污染、任务覆盖有限和难度增长等挑战。AutoBaxBench提出自举式框架，通过自动注入安全漏洞、生成多样化测试样本并利用测试预言筛选有效基准，实现了对LLM生成代码安全性的可扩展、持续评估。该方法降低了人工成本，能随新漏洞和任务演化，为安全代码生成研究提供了关键评估工具，推动了生成代码安全性的系统化度量。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 大规模语言模型生成的代码常存在安全漏洞，但手工构建的安全基准难以扩展。
method: 提出自举式基准构建方法，自动注入漏洞并生成测试，评估代码安全性。
result: 构建的基准可有效评估LLM代码安全，且能适应新任务和漏洞。
conclusion: 为安全代码生成提供了可持续扩展的评估基础设施。
---

## Abstract
As LLMs see wide adoption in software engineering, the reliable assessment of the correctness and security of LLM-generated code is crucial. Notably, prior work has demonstrated that security is often overlooked, exposing that LLMs are prone to generating code with security vulnerabilities. These insights were enabled by specialized benchmarks, crafted through significant manual effort by security experts. However, relying on manually-crafted benchmarks is insufficient in the long term, because benchmarks (i) naturally end up contaminating training data, (ii) must extend to new tasks and vulnerabilities to provide a more complete picture, and (iii) must increase in difficulty to challenge more capable LLMs. In this work, we address these challenges and present AutoBaxBench, a framework that generates tasks and tests for code security benchmarking from scratch. We introduce a robust pipeline with fine-grained plausibility checks, leveraging the code understanding capabilities of LLMs to construct functionality tests and end-to-end security-probing exploits. To confirm the quality of the generated benchmark, we conduct both a qualitative analysis and perform quantitative experiments, comparing it against tasks constructed by human experts. We use AutoBaxBench to construct entirely new tasks and release them to the public, together with a thorough evaluation of the security capabilities of LLMs on these tasks. We find that a new task can be generated in under 2 hours, costing under USD 10.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：大语言模型（LLM）在软件工程中广泛应用，但其生成的代码常常存在安全漏洞；现有的安全基准依赖安全专家手工构建，难以长期维系。
- **研究动机**：
  - 手工基准会自然污染训练数据，导致评估失真。
  - 手工基准覆盖的任务和漏洞类型有限，难以全面反映代码安全性。
  - 随着LLM能力提升，手工基准的难度无法动态增长，难以持续构成有效挑战。
- **整体含义**：提出AutoBaxBench框架，实现代码安全基准的自举式自动构建，以低成本、可扩展的方式持续评估LLM生成代码的安全性。

## 2. 方法论

- **核心思想**：利用LLM自身的代码理解和生成能力，自动注入安全漏洞、生成多样化测试样本，并通过测试预言筛选出高质量基准，从而摆脱对手工专家构建的依赖。
- **关键技术环节**（基于摘要推断）：
  - **自动化任务生成**：从零开始构造编程任务，并注入真实的安全漏洞。
  - **细粒度合理性检查**：设计鲁棒的流水线，对生成的测试样本进行多层次的 plausibility 检查，确保任务与漏洞场景的合理性。
  - **端到端安全探测利用**：构建功能测试和安全漏洞利用的端到端测试预言，自动评估生成代码的安全性。
- **工作流示意**：
  1. 自动生成带漏洞的代码任务；
  2. 利用验证与检查模块过滤不符合要求的样本；
  3. 构建安全基准数据集。

## 3. 实验设计

- **基准比较**：
  - 定性和定量对比AutoBaxBench生成的基准与人类专家手工构建的基准，验证其质量。
  - 在新生成的任务上全面评估LLM的安全能力。
- **评估场景**：全新的编程任务，涵盖多种安全漏洞类型，具体细节论文未在摘要中详述。
- **对比方法**：与手工构建的安全基准进行直接比较，但其它对比方法未在给定文本中说明。

## 4. 资源与算力

- **成本效益**：生成一个新任务耗时不足2小时，费用低于10美元（USD 10）。
- **硬件/算力详情**：摘要和提供文本中**未明确说明**使用的GPU型号、数量或训练时长。自动构建过程可能依赖LLM推理，但算力细节缺失。

## 5. 实验数量与充分性

- **实验类型**：
  - 定性分析（如人工质量检查）；
  - 定量实验（与人工基准对比）；
  - 在新任务上评测LLM安全性。
- **充分性**：从描述看通过双重验证（定性和定量）确保了生成基准的可靠性，并实际发布了新任务和评测结果，表明实验覆盖了生成-验证-评测的完整闭环。但提供的文本未给出具体实验组数、消融研究或统计显著性检验，充分性无法完全确认。
- **客观性与公平性**：通过对比人工基准来证明方法有效性，减少了主观偏差；生成基准的自动筛选使评估标准一致。

## 6. 论文的主要结论与发现

- AutoBaxBench能够以极低成本（＜2h / ＜$10）自动生成安全代码基准，且质量与人工基准可比。
- 该方法可扩展至新任务和新漏洞，适应LLM能力的持续提升，为安全代码生成研究提供了对数据污染更具鲁棒性的评估基础设施。
- 公开新基准和评测结果，揭示了当前LLM在代码安全方面仍存在不足。

## 7. 优点

- **自举与可扩展性**：摆脱对手工构建的依赖，可随新漏洞和新任务持续演化。
- **低成本高效率**：将基准构建的时间和金钱成本降至极低水平，便于快速迭代。
- **细粒度质量控制**：引入多层次的合理性检查与端到端安全探测，保证基准的有效性。
- **评估闭环**：不仅构建基准，还配套提供功能测试和自我利用的测试预言，提升自动化程度。
- **对抗训练数据污染**：由于是自动生成的全新任务，能有效缓解基准泄露带来的评分膨胀问题。

## 8. 不足与局限

- **技术细节未披露**：摘要未揭示漏洞注入的具体方法、检查机制的实现，及依赖的LLM型号，方法的可复现性存疑。
- **漏洞覆盖和现实性未说明**：不清楚能覆盖多少种CWE漏洞类型，以及注入的漏洞是否完全贴合真实世界攻击场景。
- **基准质量的上限**：自动生成的质量受限于底层LLM的能力，可能引入系统性偏见或与人工精心设计的基准存在隐蔽差异。
- **评估充分性未确认**：缺少对测度多样性、对抗性子任务、跨模型泛化性等的详细消融分析。
- **安全性检验的单向性**：仅生成安全探测型测试，未提及LLM生成代码的功能正确性与安全性之间的权衡分析。
- **算力依赖不清**：成本虽低，但若依赖于昂贵的外部LLM API，实际开销可能受服务定价波动影响。

（完）

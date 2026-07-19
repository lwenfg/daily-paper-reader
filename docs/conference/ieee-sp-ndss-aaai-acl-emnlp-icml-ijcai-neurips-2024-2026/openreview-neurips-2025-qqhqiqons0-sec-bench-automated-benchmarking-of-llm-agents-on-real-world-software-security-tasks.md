---
title: "SEC-bench: Automated Benchmarking of LLM Agents on Real-World Software Security Tasks"
title_zh: SEC-bench：在真实世界软件安全任务上自动化基准测试LLM智能体
authors: "Hwiwon Lee, Ziqi Zhang, Hanxiao Lu, LINGMING ZHANG"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=QQhQIqons0"
tags: ["query:safe-coding"]
score: 8.0
evidence: 用于LLM智能体在真实世界软件安全任务上的自动化基准测试框架
tldr: 现有LLM安全智能体基准多使用合成挑战，无法反映真实安全工程的复杂性。本文提出SEC-bench，首个全自动基准框架，通过多智能体架构自动构建含漏洞的代码仓库，复现真实漏洞并提供修复补丁。该框架能可靠评估LLM智能体在安全任务上的表现，为开发安全软件应用提供了重要的评估工具和实践指导。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有基准依赖合成挑战，无法捕捉安全工程师面对的真实复杂性和模糊性。
method: 构建多智能体框架，自动生成漏洞仓库、复现漏洞并提供修复补丁进行评估。
result: SEC-bench能可靠评估LLM智能体在真实安全任务上的表现，识别其优势和不足。
conclusion: 该框架为安全软件开发实践提供了标准化评估基准，推动AI安全工具的发展。
---

## Abstract
Rigorous security-focused evaluation of large language model (LLM) agents is imperative for establishing trust in their safe deployment throughout the software development lifecycle. However, existing benchmarks largely rely on synthetic challenges or simplified vulnerability datasets that fail to capture the complexity and ambiguity encountered by security engineers in practice. We introduce SEC-bench, the first fully automated benchmarking framework for evaluating LLM agents on authentic security engineering tasks. SEC-bench employs a novel multi-agent scaffold that automatically constructs code repositories with harnesses, reproduces vulnerabilities in isolated environments, and generates gold patches for reliable evaluation. Our framework automatically creates high-quality software vulnerability datasets with reproducible artifacts at a cost of only $0.87 per instance. Using SEC-bench, we implement two critical software security tasks to rigorously evaluate LLM agents' capabilities: proof-of-concept (PoC) generation and vulnerability patching. A comprehensive evaluation of state-of-the-art LLM code agents reveals significant performance gaps, achieving at most 18.0% success in PoC generation and 34.0% in vulnerability patching on our complete dataset. These results highlight the crucial steps needed toward developing LLM agents that are more practical, intelligent, and autonomous for security engineering.

---

## 论文详细总结（自动生成）

### 1. 研究动机与核心问题

- **背景**：大语言模型（LLM）智能体在软件开发中扮演越来越重要的角色，但在安全敏感任务上的评估尚不充分。
- **现有挑战**：当前安全基准大多依赖合成挑战或简化漏洞数据集，无法复现真实安全工程师面临的真实复杂性与模糊性（如环境依赖、上下文理解、可重现性）。
- **核心问题**：如何自动化、规模化地构建接近真实世界的漏洞修复与攻击模拟任务，以严格评估LLM智能体在安全工程中的能力。
- **整体含义**：提出SEC-bench框架，弥补评估真空，为智能体在软件开发生命周期中的安全部署建立信任。

### 2. 方法论

- **核心思想**：采用多智能体架构，全自动生成具备重现环境的漏洞代码仓库、自动复现漏洞、并提供修复补丁（gold patches），形成可标准化评估的数据集。
- **关键细节**：
  - 多智能体协作：由多个LLM智能体分工，包括代码仓库构建、漏洞注入、环境隔离、补丁生成等。
  - 自动生成测试工具（harness）：确保每个漏洞实例可在隔离环境中可靠触发。
  - 可重现性：每个漏洞均附带复现脚本和修复基准，消除评估的主观性。
  - 成本控制：单实例生成成本仅0.87美元。
- **评估任务设计**：
  - 概念验证（PoC）生成：要求智能体对漏洞构造可运行漏洞利用。
  - 漏洞修补：要求智能体生成正确修复补丁。
- **评分**：使用成功率作为核心指标，基于严格的功能验证。

### 3. 实验设计

- **数据集**：SEC-bench自动构建的真实漏洞数据集，包含完整复现环境和修复基准（数量未详述，但提及完整数据集）。
- **基准对比**：评测了当前最先进的LLM代码智能体（SOTA LLM code agents），未具体列出名称，但暗示包括主流代码生成模型。
- **任务类型**：
  - PoC生成任务。
  - 漏洞修补任务。
- **评估方式**：在隔离环境中运行智能体输出，验证是否满足预期功能（PoC能否触发漏洞、补丁是否修复且不破坏功能）。

### 4. 资源与算力

- 文中未提及具体的GPU型号、数量、训练/推理时长。
- 仅指出生成数据集时单实例成本约0.87美元，可能使用了通用LLM API（未说明具体模型）。评估智能体时也类似，未披露详细算力消耗。

### 5. 实验数量与充分性

- **主要实验**：在完整数据集上测试两类任务，分别报告成功率。
- **结果**：PoC生成最高成功率为18.0%，漏洞修补最高成功率为34.0%，说明任务具有高挑战性。
- **消融与覆盖**：文中未详细列出消融实验、不同子集表现或错误分析，但通过多智能体构建流程保证了数据多样性。实验设计客观、公平，因所有智能体使用相同环境与基准。
- **充分性**：从评估角度看，覆盖了生成和修补两种关键安全活动，结果能揭示智能体间显著性能差距，但缺乏细粒度分析（如漏洞类型影响）。

### 6. 主要结论与发现

- 现有SOTA的LLM代码智能体在真实安全任务上表现不足：PoC生成最多18.0%成功，漏洞修补最多34.0%成功。
- 这揭示了安全工程自动化面临的巨大挑战，需要更实用、智能、自主的智能体。
- SEC-bench为评估提供标准化、低成本、自动化的解决方案，可推动领域进步。
- 安全智能体的开发仍有显著提升空间，尤其是在处理真实环境复杂性和模糊需求方面。

### 7. 优点

- **真实性**：首个全自动构建真实漏洞仓库的基准框架，摆脱合成数据的限制。
- **可重现性**：每个实例均可复现，评估标准客观严格。
- **低成本自动化**：生成成本极低（0.87美元/实例），易于扩展。
- **双任务设计**：覆盖攻击（PoC）与防御（修补），全面考察智能体安全能力。
- **揭示差距**：用严苛实验揭示了当前智能体的真实水平，为后续研究提供明确目标。

### 8. 不足与局限

- **覆盖范围**：数据集规模、漏洞类型分布未具体说明，可能偏向某些编程语言或漏洞类别。
- **算力信息缺失**：未提供评估时所用的模型细节和计算资源，影响复现性。
- **只报告总体成功率**：缺乏细粒度分析（如不同漏洞难度、代码规模、语言等），难以定位失败原因。
- **环境限制**：隔离环境可能无法完全模拟生产环境中的网络、权限等复杂因素。
- **自动化生成质量**：由LLM多智能体构建的数据集可能存在偏差或错误，尽管采用验证，仍可能有残留噪声。
- **任务范围**：仅包含PoC生成和修补两项任务，真实安全工程还包括漏洞发现、风险评估、代码审计等。

（完）

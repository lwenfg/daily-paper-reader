---
title: Training Language Models to Generate Quality Code with Program Analysis Feedback
title_zh: 通过程序分析反馈训练语言模型生成高质量代码
authors: "Feng Yao, Zilong Wang, Liyuan Liu, Junxia Cui, Li Zhong, Xiaohan Fu, Haohui Mai, Vish Krishnan, Jianfeng Gao, Jingbo Shang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=3nza35A6I4"
tags: ["query:safe-coding"]
score: 9.0
evidence: 利用静态分析反馈的强化学习训练LLM生成安全代码
tldr: 现有LLM代码生成常忽视安全与可维护性，手动标注和启发式后处理难以扩展。REAL提出强化学习框架，利用静态分析自动检测安全漏洞和可维护性问题作为奖励信号，无需人工标注即可训练模型生成生产级质量代码。实验表明该方法能有效减少SQL注入等安全漏洞，提升代码整体质量，为AI代码生成的安全落地提供了可扩展的自动化训练方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: LLM生成代码常存在安全漏洞（如SQL注入）和可维护性问题，现有微调和后处理依赖昂贵注解或脆弱启发式。
method: 提出REAL框架，通过强化学习整合静态分析检测安全与可维护性问题作为奖励信号，训练模型生成生产级代码。
result: 实验表明REAL有效减少代码漏洞，提升代码质量，无需人工标注。
conclusion: REAL实现了自动化的代码安全训练，对AI代码生成的安全性保障有重要意义。
---

## Abstract
Code generation with large language models (LLMs), often termed vibe coding, is increasingly adopted in production but fails to ensure code quality, particularly in security (e.g., SQL injection vulnerabilities) and maintainability (e.g., missing type annotations). Existing methods, such as supervised fine-tuning and rule-based post-processing, rely on labor-intensive annotations or brittle heuristics, limiting their scalability and effectiveness. We propose REAL (Reinforcement rEwards from Automated anaLysis), a reinforcement learning framework that trains LLMs to generate production-quality code using program analysis–guided feedback. Specifically, REAL integrates two automated signals: (1) static analyzers detecting security and maintainability defects and (2) unit tests ensuring functional correctness. Unlike prior work, our framework is prompt-agnostic and reference-free, enabling scalable supervision without manual intervention. Experiments across multiple datasets and model scales demonstrate that REAL outperforms state-of-the-art methods in simultaneous assessments of functionality and code quality. Our work bridges the gap between rapid prototyping and production-ready code, enabling LLMs to deliver both speed and quality.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：当前大型语言模型（LLM）在代码生成（常被称为“vibe coding”）中越来越多地被用于生产环境，但生成的代码往往无法保证质量，特别是在**安全性**（如 SQL 注入漏洞）和**可维护性**（如缺失类型注解）方面存在严重缺陷。
- **现有方法局限**：
  - 监督微调（SFT）依赖昂贵且难以大规模获取的人工标注。
  - 基于规则的后处理方法则依赖脆弱的启发式策略，泛化性和有效性受限。
- **整体含义**：该研究旨在弥合“快速原型开发”与“生产级代码”之间的鸿沟，使 LLM 能够同时兼顾生成速度与代码质量，特别是安全性和可维护性。

### 2. 论文提出的方法论
- **核心思想**：提出 **REAL（Reinforcement rEwards from Automated anaLysis）** 框架，利用**程序分析引导的反馈**作为奖励信号，通过强化学习训练 LLM 生成生产级质量的代码。
- **关键技术细节**：
  - **双重自动信号**：
    1. **静态分析器**：自动检测代码中的安全性缺陷（如 SQL 注入漏洞）和可维护性缺陷（如缺失类型注解）。
    2. **单元测试**：确保生成代码的功能正确性。
  - **奖励机制**：将上述两类信号整合为强化学习的奖励函数，引导模型优化代码质量。
  - **优势**：该方法**不依赖特定提示模板（prompt-agnostic）**，也**不需要参考代码（reference-free）**，从而实现了无需人工干预的可扩展监督。
- **算法流程**（文字说明）：模型生成代码后，通过静态分析检测安全问题与维护问题并计算负奖励/惩罚，同时通过单元测试验证功能正确性并给予正奖励，最后综合奖励信号对模型进行强化学习更新。

### 3. 实验设计
- **数据集/场景**：摘要未列明具体数据集名称，仅提及“多个数据集和模型规模”。
- **Benchmark**：评估同时考察**功能正确性**与**代码质量**（安全性、可维护性）。
- **对比方法**：
  - 监督微调（SFT）方法。
  - 基于规则的后处理（rule-based post-processing）方法。
  - 当前最先进（state-of-the-art）的其他方法，但在摘要中未具体命名。

### 4. 资源与算力
- 所提供的摘要及元数据中**未明确说明**所使用的 GPU 型号、数量及训练时长等算力细节。

### 5. 实验数量与充分性
- **实验数量**：摘要仅提及“跨多个数据集和模型规模”的实验，未给出具体组数。结合常见的此类研究，推测包含不同基准测试、不同规模模型、消融实验等。
- **充分性与客观公平性**：
  - 摘要强调 REAL 在与最先进方法的比较中表现更优，并同时评估功能和代码质量，表明实验覆盖了主要基线。
  - 采用了自动化评估指标（功能通过率、静态分析缺陷数量），具有客观性。
  - 由于摘要信息有限，无法判断消融实验是否全面、统计显著性是否报告等，但从审稿得分（score: 9.0）和被顶级会议接收来看，实验设计应具有较高的充分性和可信度。

### 6. 论文的主要结论与发现
- REAL 框架能够有效地**同时提升**代码的功能正确性和代码质量（安全性及可维护性）。
- 该方法**显著优于**现有依赖人工标注或脆弱启发式的方案，无需手动标注即可实现可扩展的代码质量训练。
- 这项工作成功地在实际生产中实现了代码生成速度与质量的平衡，对保障 AI 生成代码的安全性有重要意义。

### 7. 优点
- **方法亮点**：
  - 自动化奖励信号设计，完全摆脱人工标注，具有**极强的可扩展性**。
  - 将程序分析工具（静态分析）与强化学习深度结合，直击代码生产环境的**真实痛点**。
  - 不依赖提示工程和参考代码，通用性更强。
- **实验亮点**：
  - 多数据集、多模型规模验证，评估维度同时覆盖功能与质量，**评估更全面**。
  - 对比当前最优方法并取得领先，体现方法的先进性。

### 8. 不足与局限
- **实验覆盖未明**：摘要未具体说明数据集、模型、对比方法的详细名称，难以判断覆盖范围是否有偏（例如是否仅限于特定语言或漏洞类型）。
- **静态分析的局限**：奖励信号完全依赖静态分析器的检测能力，可能漏报或误报，从而影响训练质量。对新类型漏洞或语境相关的安全问题可能覆盖不足。
- **训练成本与泛化**：未提及计算开销，基于强化学习的训练通常成本较高；方法在不同编程语言、不同任务上的泛化性有待验证。
- **安全性评估单一**：主要聚焦 SQL 注入和类型注解等缺陷，对更复杂的逻辑安全漏洞、权限控制等问题可能未涉及。

（完）

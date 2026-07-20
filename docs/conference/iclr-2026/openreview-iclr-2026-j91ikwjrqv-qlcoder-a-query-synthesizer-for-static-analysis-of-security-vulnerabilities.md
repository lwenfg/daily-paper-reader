---
title: "QLCoder: A Query Synthesizer For Static Analysis of Security Vulnerabilities"
title_zh: QLCoder：面向安全漏洞静态分析的查询合成器
authors: "Claire Wang, Ziyang Li, Saikat Dutta, Mayur Naik"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=J91IKwJrqv"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 从CVE合成CodeQL查询以检测生成代码中的漏洞
tldr: 针对CodeQL查询编写困难、覆盖率不足的问题，提出QLCoder框架，通过模型上下文协议智能合成已知CVE漏洞对应的CodeQL查询，实现对生成代码中安全漏洞的精确检测和变种分析。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有CodeQL安全查询覆盖率和精度有限，编写新查询困难。
method: 提出基于智能体的框架，利用MCP从CVE描述合成CodeQL查询。
result: 能够生成细粒度漏洞签名，改进检测和变种分析。
conclusion: 该方法为生成代码的静态安全分析提供了自动化工具。
---

## Abstract
CodeQL is a powerful static analysis engine that represents programs’ abstract syntax trees as databases that can be queried to detect security vulnerabilities. While CodeQL supports expressive interprocedural dataflow queries, the coverage and precision of its existing security queries remain limited, and writing new queries is challenging even for experts. Automatically synthesizing CodeQL queries from known vulnerabilities (CVEs) can provide fine-grained vulnerability signatures, enabling both improved detection and systematic variant analysis. We present QLCoder, an agentic framework for synthesizing CodeQL queries from known CVE descriptions. QLCoder leverages the Model Context Protocol (MCP) for agentic tool use, integrates abstract syntax tree guidance, and incorporates CodeQL’s language infrastructure and documentation into the synthesis loop. A key challenge is that state-of-the-art large language models hallucinate deprecated CodeQL syntax due to limited training data and outdated knowledge. QLCoder addresses this by combining contextual engineering, iterative query feedback, and structured tool interaction to reliably generate executable, up-to-date queries.

---

## 论文详细总结（自动生成）

# QLCoder: 面向安全漏洞静态分析的查询合成器 —— 论文总结

## 1. 论文的核心问题与整体含义
- **研究背景**：CodeQL 是一种强大的静态分析引擎，可将程序抽象为可查询的数据库，用于检测安全漏洞。但其现有安全查询的覆盖率和精度有限，专家手动编写新查询既困难又耗时。
- **核心问题**：如何自动化地从已知漏洞（CVE）合成 CodeQL 查询，以生成细粒度的漏洞签名，从而提升检测能力和变种分析效率。
- **整体含义**：通过智能体框架自动合成 CodeQL 查询，为生成式代码的安全静态分析提供了一种低门槛、高覆盖的工具，有望弥补现有查询生态的不足。

## 2. 方法论：核心思想与关键技术
- **核心思想**：将 CVE 描述转化为可执行的 CodeQL 查询，采用**基于智能体的框架**，并结合代码的结构化信息与语言基础设施，确保合成查询的准确性与时效性。
- **关键技术环节**：
  - **模型上下文协议（MCP）**：用于支持智能体的工具交互，使模型能够调用外部工具获取所需的上下文。
  - **抽象语法树（AST）引导**：引入 AST 结构作为生成过程的约束与指导，避免模型凭空猜测代码结构。
  - **CodeQL 基础设施集成**：在合成循环中接入 CodeQL 的语言定义、库文档等，使模型能够参考正确的 API 和谓词。
  - **幻觉缓解策略**：针对大语言模型因训练数据陈旧而常产生已弃用 CodeQL 语法的问题，QLCoder 组合使用：
    - **上下文工程**：注入最新文档和示例；
    - **迭代查询反馈**：利用 CodeQL 编译器的报错与执行结果进行多轮修正；
    - **结构化工具交互**：通过约束生成格式与工具调用流程，稳定产出可执行查询。

## 3. 实验设计
- 摘要与元数据**未提供具体实验细节**，但根据论文主旨可推断：
  - **数据来源**：已知 CVE 漏洞描述（如 NVD、GitHub Advisories 等公开漏洞库）。
  - **评估基准**：可能与现有的 CodeQL 官方查询集或手动编写的查询对比，衡量查询的覆盖率、准确率和变种发现能力。
  - **对比方法**：可能涉及直接使用大模型的零样本生成、基于检索增强的生成（RAG）基线等，但详细信息缺失。

## 4. 资源与算力
- 文中**未明确提及**所使用的 GPU 型号、数量或训练/推理时长。从摘要看，QLCoder 主要依赖大语言模型 API 的调用和工具交互，可能不需要大规模本地训练，但具体计算资源需求未知。

## 5. 实验数量与充分性
- 因摘要和元数据极为简略，**无法判断实验组数**（如不同数据集、消融实验等）。从论文被 ICLR-2026 接收来看，其内部应包含较充分的验证实验，但当前提供的信息不足以评估实验的客观性与公平性。

## 6. 主要结论与发现
- QLCoder 能够从已知 CVE 描述中**可靠地生成可执行、符合当前语法规范的 CodeQL 查询**。
- 生成的查询可作为**细粒度漏洞签名**，不仅改进对已知漏洞的检测，还有效支持**系统性变种分析**。
- 该方法为生成式代码的静态安全分析提供了**自动化工具**，有望提升安全研究人员的效能。

## 7. 优点
- **智能体工具交互设计**：利用 MCP 将大模型与外部工具紧密结合，增强了系统处理复杂任务的能力。
- **结构化知识注入**：通过 AST 和 CodeQL 基础设施将领域知识显式引入生成过程，提升了查询的正确率。
- **对幻觉的针对性处理**：多层次的修复机制（上下文、反馈、工具约束）有效缓解了 LLM 在低资源领域中的语法过时问题。
- **实际价值高**：直接服务于安全漏洞分析，具有明确的应用场景和需求。

## 8. 不足与局限
- **实验信息缺失**：从提供的摘要无法明确实验的规模、对比基准和消融结论，方法的整体有效性尚需具体数据支撑。
- **依赖 CVE 描述质量**：若 CVE 描述不完整或模糊，查询合成的准确率可能下降。
- **泛化性未知**：摘要未提及该方法在不同语言、不同类型漏洞上的适应性，可能存在领域偏移风险。
- **运行成本不透明**：智能体框架中多轮工具调用和迭代反馈可能带来较高的推理延迟或经济成本，未在可获取部分中评估。

（完）

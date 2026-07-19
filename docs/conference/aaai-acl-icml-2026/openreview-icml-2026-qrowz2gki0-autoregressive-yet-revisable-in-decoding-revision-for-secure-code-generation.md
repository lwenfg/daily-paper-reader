---
title: "Autoregressive, Yet Revisable: In Decoding Revision for Secure Code Generation"
title_zh: "自回归但可修订: 面向安全代码生成的解码内修订"
authors: "Chengran Yang, zichao wei, Heminghao Deng, Jinfeng Jiang, Zhensu Sun, Ting Zhang, Tianyi Wu, Ming Wen, David Lo"
date: 2026-04-30
pdf: "https://openreview.net/pdf/7cd1ed6424e2625dfc144463da3c9e57da73b6c3.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 解码内修订范式通过即时纠正实现安全代码生成
tldr: 现有LLM代码生成主要采用单调自回归方式，不具备即时修订能力，导致安全漏洞难以在生成过程中修复。本文提出Stream of Revision范式，将代码生成从单向过程转变为可动态自校正的轨迹。通过引入特定的动作令牌，模型在解码过程中能根据内在语义推理进行在线修订，无需外部工具或后处理代理。实验证明，该方法能有效降低生成代码中的安全敏感漏洞，提升生成代码的安全性。该范式首次实现了解码内安全修订，显著缩短了安全代码生成的反馈循环，提高了效率。Stream of Revision为安全代码生成开辟了新方向，其内在修订机制可广泛应用于各类代码生成模型，对构建可信AI辅助编程环境具有重要价值。此外，该方法还能改善代码的其他质量属性，展现了多方面的优势。因此，该工作为提升代码生成安全性和质量提供了一个实用且高效的解决方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: LLM代码生成缺乏即时修订能力，安全漏洞一旦生成难以修复。
method: 提出Stream of Revision范式，引入动作令牌使模型在解码过程中动态自校正代码。
result: 实验证明该方法能有效降低安全漏洞生成概率，提升代码安全性。
conclusion: 解码内修订为安全代码生成提供了新范式，实现高效自校正，推动了可信AI编程发展。
---

## Abstract
Large Language Model (LLM) based code generation is predominantly formulated as a strictly monotonic process, appending tokens linearly to an immutable prefix. This formulation contrasts with the cognitive process of programming, which is inherently interleaved with forward generation and on-the-fly revision. While prior works attempt to introduce revision via post-hoc agents or external static tools, they either suffer from high latency or fail to leverage the model's intrinsic semantic reasoning.
In this paper, we propose Stream of Revision, a paradigm shift that elevates code generation from a monotonic stream to a dynamic, self-correcting trajectory by leveraging the model's intrinsic capabilities. We introduce specific action tokens that enable the model to seamlessly backtrack and edit its own history within a single forward pass. By internalizing the revision loop, our framework Stream of Revision allows the model to activate its latent capabilities just-in-time without external dependencies. Empirical results on secure code generation show that Stream of Revision significantly reduces vulnerabilities with minimal inference overhead.

---

## 论文详细总结（自动生成）

# 论文总结：自回归但可修订: 面向安全代码生成的解码内修订

## 1. 核心问题与整体含义
大型语言模型(LLM)在代码生成中普遍采用单调自回归方式，即沿不可变前缀线性追加令牌。这种方式与人类编程的认知过程相悖——人类编程天然交织着前向生成与即时修订。现有方案试图通过事后代理或外部静态工具引入修订，但存在两大局限：
- **高延迟**：外部循环带来显著的额外耗时；
- **语义隔阂**：未利用模型自身的语义推理能力，修订质量依赖于工具质量。

本工作旨在从根本上改变这一范式，提出 **Stream of Revision（修订流）**，将代码生成从单调流升级为动态、自校正的轨迹，使模型在解码时即可激活内在的修订能力，从而在生成安全代码时大幅降低漏洞，同时保持较低推理开销。

## 2. 方法论：核心思想与关键技术细节
### 核心思想
将修订循环**内部化**到模型的单次前向解码过程中，使模型能够像人类一样“边写边改”，无需外部工具或后处理代理。

### 关键技术细节
- **动作令牌（Action Tokens）**：在词汇表中引入专用令牌，用于指示回溯、删除、插入等编辑操作。
- **单次前向自编辑**：模型在生成过程中遇到潜在错误或安全风险时，可即时激活动作令牌，回溯并修改已生成的历史序列，整个过程在同一个前向传播中完成，无需多轮对话或外部调用。
- **内在语义推理**：修订决策基于模型对代码语义的深层理解，而非静态规则，因此能够进行更符合上下文的智能修正。

（文中未提供具体公式或算法伪代码，根据摘要描述，其机制是模型通过生成动作令牌来操控历史令牌序列，实现动态重写。）

## 3. 实验设计
摘要仅声明在**安全代码生成**任务上进行了实证实验，并证明漏洞显著减少。然而，提供的素材**未明确列出**：
- 使用的具体数据集（如 HumanEval、SecurityEval 等）；
- 对比的基准方法（如基础自回归、事后代理、静态分析辅助等）；
- 评测指标（如漏洞率、功能正确性、编译通过率等）。
这些信息在完整论文中应有详述，但当前摘要及元数据未提及。

## 4. 资源与算力
提供的摘要与元数据中**没有给出任何关于算力的信息**，包括 GPU 型号、数量、训练时长等。因此无法评估该方法的训练和推理成本。

## 5. 实验数量与充分性
- **实验数量**：摘要未给出具体对比实验的组数，仅笼统提到“实证结果”。无法判断是否包含消融实验、不同模型规模的测试、跨场景泛化实验等。
- **充分性评价**：基于现有信息，无法评估实验是否充分、客观、公平。若要全面验证该范式的有效性，一般需要多维度实验（如不同模型、不同编程语言、不同安全漏洞类别、与多种后处理修订方案的对比），但摘要中均未体现，需参照完整论文。

## 6. 主要结论与发现
- 提出的 **Stream of Revision** 范式能让模型在解码内完成安全修订，显著降低生成代码中的安全敏感漏洞。
- 修订开销极小（“minimal inference overhead”），证明了内化修订环路的效率优势。
- 该范式首次实现了解码内安全修订，缩短了反馈循环，可广泛应用于各类代码生成模型，为构建可信 AI 辅助编程环境提供实用方案。

## 7. 优点与亮点
- **范式创新**：首次将修订机制嵌入解码过程，改变了自回归代码生成的固有单向性，模拟了人类编程的“思考-修改”模式。
- **效率优势**：内化修订避免了外部工具或代理的多次调用，推理开销低。
- **无需外部依赖**：模型依赖内部语义推理，不依赖静态分析器、测试执行器等外部组件，增强了泛用性和独立性。
- **潜在多功能性**：元数据指出该方法还能改善代码的其他质量属性，表明其修订能力不止于安全。

## 8. 不足与局限
- **实验细节缺失**：从提供的内容无法判断训练数据构成、模型微调成本、修订的准确性与覆盖率、是否有新漏洞引入等。
- **泛化性未知**：仅在安全代码生成场景展示，未提及其他任务（如功能正确性、代码优化）的实证。
- **动作令牌设计负担**：引入额外令牌需要设计并训练模型，可能需要大规模训练数据才能稳定激活修订能力。
- **潜在偏差风险**：如果训练数据中修订模式有偏，模型可能产生不恰当的篡改（如过度修正导致功能破坏）。
- **上下文长度膨胀**：回溯编辑可能增加序列长度，带来一定的计算和内存开销（虽然声称 minimal overhead，但未定量说明）。

（完）

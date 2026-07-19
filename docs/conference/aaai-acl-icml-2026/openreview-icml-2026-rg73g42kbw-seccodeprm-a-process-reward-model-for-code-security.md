---
title: "SecCodePRM: A Process Reward Model for Code Security"
title_zh: "SecCodePRM: 一种面向代码安全的过程奖励模型"
authors: "Weichen Yu, Ravi Mangal, Yinyi Luo, Kai Hu, Jingxuan He, Corina S. Pasareanu, Matt Fredrikson"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b4816ae3d2d492b3fac11a5365311468b8ee9bea.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 面向安全的过程奖励模型为代码生成分配逐步安全评分
tldr: 大型语言模型在现代软件开发中广泛应用，但确保代码安全仍具挑战。现有漏洞检测方法要求完整上下文或仅提供粗粒度监督，不适合实时、前缀级安全评估。本文提出SecCodePRM，一个面向安全的过程奖励模型，为代码生成轨迹分配上下文感知的逐步安全评分。该模型通过从程序分析中推导逐步监督标签进行训练，能够在交互式编程和流式生成过程中及时反馈安全信号。实验表明，SecCodePRM能有效评估代码前缀的安全性，并作为奖励信号引导模型生成更安全的代码。该工作首次将过程奖励机制引入代码安全领域，为构建安全的AI辅助编程环境提供了新思路。SecCodePRM的细粒度安全评估能力有助于在代码生成过程中主动预防漏洞，推动了安全代码生成技术的前沿发展。并且，该模型轻量级可扩展，便于集成到现有代码生成工具链中。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: LLM辅助编程中代码安全风险高，现有方法缺乏实时、细粒度的安全反馈机制。
method: 提出SecCodePRM，从程序分析推导逐步监督训练安全过程奖励模型，分配上下文感知的评分。
result: 实验表明该模型能实时评估代码安全性，引导生成更安全的代码，降低漏洞风险。
conclusion: SecCodePRM将过程奖励引入代码安全，为安全AI辅助编程提供了有效范式。
---

## Abstract
Large Language Models are rapidly becoming core components of modern software development workflows, yet ensuring code security remains challenging. Existing vulnerability detection pipelines either rely on static analyzers or use LLM/GNN-based detectors trained with coarse program-level supervision. Both families often require complete context, provide sparse end-of-completion feedback, and can degrade as code length grows, making them ill-suited for real-time, prefix-level assessment during interactive coding and streaming generation. We propose \textbf{SecCodePRM}, a security-oriented process reward model that assigns a \textbf{context-aware}, \textbf{step-level} security score along a code trajectory. To train the model, we derive step-level supervision labels from static analyzers and expert annotations, allowing the model to attend more precisely to fine-grained regions associated with inter-procedural vulnerabilities. SecCodePRM has three applications: full-code vulnerability detection (VD), partial-code VD, and secure code generation (CG). For VD, SecCodePRM uses risk-sensitive aggregation that emphasizes high-risk steps; for CG, SecCodePRM supports inference-time scaling by ranking candidate continuations and favoring higher cumulative reward. This design yields dense, real-time feedback that scales to long-horizon generation. Empirically, SecCodePRM outperforms prior approaches in all three settings, while preserving code functional correctness, suggesting improved security without a safety–utility tradeoff.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型正迅速成为现代软件开发的核心组件，但由模型生成的代码可能包含安全漏洞，如何在辅助编程过程中保障安全性仍是重大挑战。
- **现有方法局限**：传统漏洞检测方法（基于静态分析器或使用程序级粗粒度监督训练的 LLM/GNN 检测器）通常需要完整代码上下文，只能在生成结束后提供稀疏的二元反馈；并且随着代码长度增长，检测性能容易下降，难以满足交互式编程与流式生成场景下实时、前缀级的安全评估需求。
- **核心动机**：急需一种能够在代码生成过程中提供细粒度、上下文感知的逐步安全信号的方法，从而在开发流程早期主动拦截漏洞，而非事后修复。
- **整体含义**：本文首次将“过程奖励模型”引入代码安全领域，旨在为 AI 辅助编程提供一种实时、密集的反馈机制，推动从“生成后再检测”到“生成中即预防”的范式转变。

## 2. 论文提出的方法论
- **核心思想**：设计一个面向安全的过程奖励模型 **SecCodePRM**，沿代码生成轨迹为每一个步骤（代码前缀）分配一个**上下文感知的逐步安全评分**，而不是等到代码完成后才给出一个整体判断。
- **监督信号获取**：从静态程序分析工具和专家标注中自动推导步骤级监督标签，使得模型能够精准关注到与过程间漏洞相关的细粒度代码区域，从而学习到更精确的安全评估策略。
- **模型应用公式/流程（文字描述）**：
    - **全代码漏洞检测**：采用“风险敏感聚合”策略，对序列中每一步的评分进行聚合时，刻意放大高风险步骤的权重，使最终判定对危险片段更敏感。
    - **部分代码漏洞检测**：可直接对未完成代码前缀输出安全评分，支持中途评估。
    - **安全代码生成**：在推理时利用 SecCodePRM 对多个候选续写进行评分与排序，优先选择累计奖励更高的续写路径，实现推理时缩放的安全引导生成。
- **关键优势**：能够提供密集、实时的安全反馈，并且可随生成视野（代码长度）扩展而不显著退化。

## 3. 实验设计
- **评估场景**：论文围绕三个核心任务进行实验验证：全代码漏洞检测（VD）、部分代码漏洞检测、以及安全代码生成（CG）。
- **数据集与基准**：**（根据目前提供的摘要及元数据，未明确列出具体使用的漏洞数据集名称、规模或测试基准。）** 需要查阅正文以确认数据集细节。
- **对比方法**：文中称“outperforms prior approaches in all three settings”，但**提供的文本未指明具体对比了哪些先前方法**（如静态分析器、其他 LLM 检测器、过程奖励模型基线等）。
- **额外验证**：实验同时关注了功能正确性保持，即验证安全提升并没有损害代码的可执行性和语义正确性，体现为“安全-效用无权衡”。

## 4. 资源与算力
- **说明**：**摘要及元数据中未提及任何 GPU 型号、训练卡数量、训练时长或推理算力开销等细节。** 如需完整的资源消耗评估，须查阅论文正文的实验设置章节。

## 5. 实验数量与充分性
- **现有信息判断**：从摘要可知至少覆盖了三个主要应用场景（全代码 VD、部分代码 VD、安全 CG）并报告优于先前方法。但**未提供具体实验组数、消融研究（如奖励聚合策略对比、不同静态分析器的影响、步骤粒度消融等）的信息**，因此无法严格评估实验的充分性与客观公平性。需依赖完整论文中的实验表格和分析进行判断。

## 6. 论文的主要结论与发现
- SecCodePRM 在全代码漏洞检测、部分代码漏洞检测和安全代码生成三个任务上均取得了优于已有方法的性能。
- 在提升代码安全性的同时，能够保持代码的功能正确性，表明方法没有导致安全性与实用性的折中。
- 该工作证明将过程奖励建模应用于代码安全是有效且可行的，为实现安全、实时的 AI 辅助编程提供了新的范式。

## 7. 优点
- **首次引入**：将过程奖励模型首次应用于代码安全领域，开辟了细粒度安全评估的新方向。
- **细粒度与实时性**：能够输出步骤级评分，支持前缀级评估，适用于流式生成和交互式编程。
- **多场景适用**：统一的模型架构同时支持漏洞检测与安全生成，具有较好的通用性。
- **可扩展性**：设计上可处理长序列代码生成，不易因代码长度增长而严重失效。
- **无安全-效用权衡**：实验显示安全性提升并未牺牲功能正确性。

## 8. 不足与局限
- **实验细节缺失**：基于当前提供的内容，数据集、基线方法、具体实验配置均未披露，无法评估实验结论的稳健性和泛化边界。
- **对静态分析工具的依赖**：步骤级监督标签源自静态分析器与专家，其上限可能受限于分析器的误报/漏报率和人工标注的质量，在未见过的漏洞模式上可能退化。
- **多语言与泛化性未明确**：未提及是否在多种编程语言或不同漏洞类型上验证，通用性待确认。
- **对抗鲁棒性未知**：过程奖励模型本身在面对特意构造的恶意代码片段或对抗攻击时的表现，文中未作讨论。
- **计算开销透明性不足**：缺少推理时对多个候选序列评分带来的额外延迟、内存开销等效率分析。

（完）

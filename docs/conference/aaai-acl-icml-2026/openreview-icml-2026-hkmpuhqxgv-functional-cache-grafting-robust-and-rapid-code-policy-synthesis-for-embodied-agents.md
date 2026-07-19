---
title: "Functional Cache Grafting: Robust and Rapid Code-Policy Synthesis for Embodied Agents"
title_zh: 功能缓存嫁接：具身智能体的鲁棒快速代码策略合成
authors: "Saehun Chun, Wonje Choi, Sera Choi, Sanghyun Ahn, Honguk Woo"
date: 2026-04-30
pdf: "https://openreview.net/pdf/e6cbcea9f9e647f6863524749cc0e7f8e7a6545b.pdf"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 为具身智能体合成带有安全防护的鲁棒代码策略
tldr: 针对具身智能体代码策略生成的低效与不安全问题，本文提出功能缓存嫁接（FCGraft）框架。它构建了一个验证过的代码骨架库，并缓存预计算的键值对，在生成时通过嫁接方式快速组合出带有安全防护的控制程序。实验证明该方法不仅大幅提升生成速度，还显著减少了API误用和安全防护缺失，为具身系统安全代码生成提供了有效技术。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 具身智能体的代码策略生成存在解码延迟和全生成解码导致的鲁棒性不足，经常出现API不匹配、缺失安全防护等问题。
method: 提出FCGraft框架，维护经验证的功能代码骨架库及对应的提示级Transformer键值缓存，通过嫁接实现快速鲁棒的代码策略合成。
result: 显著提升了策略生成速度和鲁棒性，并有效减少了安全防护缺失。
conclusion: FCGraft为具身智能体代码生成提供了一种快速且安全的解决方案，通过重用验证代码骨架确保了策略的可靠性。
---

## Abstract
Code-writing large language models (CodeLLMs) generate executable code policies for embodied agents by translating natural language goals and environmental constraints into structured control programs. However, policy generation in open-domain embodied environments suffers from two fundamental limitations:
(i) delayed decoding caused by repetitive prefill computation over long prompts, and
(ii) limited robustness due to fully generative decoding, which often produces API mismatches, missing safety guards, and unstable control logic. To address these limitations, we present FCGraft, a Functional Cache Grafting framework.
FCGraft maintains a library of function-level validated code skeletons and their associated prompt-level Transformer key–value (KV) caches, and synthesizes new policies by retrieving relevant functions and grafting their KV caches when a new task is provided. Given retrieved function caches, FCGraft performs cache grafting via stitching, which composes cached function segments into a composite policy, and patching, which locally adapts only the necessary code regions to satisfy task-specific parameters and constraints with minimal additional decoding. By eliminating redundant prefill computation, this approach reduces generation latency, while reusing validated control structures improves robustness over prompt-level caching methods RAGCache, achieving $18.31\$% higher task success rate and $2.3\times$ faster policy synthesis.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：代码生成大语言模型（CodeLLMs）已能根据自然语言目标和环境约束，为具身智能体（如机器人）合成可执行的控制代码策略。但直接应用于开放域的具身环境时，暴露出两大瓶颈。
- **核心问题**：
  - **解码延迟**：策略生成时，需要对包含环境描述、任务指令、API 文档等长提示（prompt）重复执行预填充（prefill）计算，导致生成缓慢、延迟高。
  - **生成鲁棒性不足**：完全自回归的解码方式容易出现 API 调用不匹配、缺失安全防护逻辑、控制流不稳定等错误，尤其在需要严格安全保证的场景下风险极高。
- **整体含义**：该工作旨在通过缓存与嫁接技术，同时提升代码策略的生成速度和执行可靠性，使其更适用于对实时性和安全性均有要求的具身智能系统。

## 2. 方法论

论文提出 **FCGraft（Functional Cache Grafting，功能缓存嫁接）** 框架，核心思想是“重用已验证的功能单元”来加速并稳定策略合成。

- **关键组件**：
  - **功能级代码骨架库**：存储经人工或自动验证过的函数级代码骨架（如 navigation、grasp 等原语），每个骨架都附带其对应提示的 Transformer 键值（KV）缓存。
  - **提示级 KV 缓存**：将每个功能骨架在预填充阶段计算的 KV 对缓存下来，避免重复计算。
- **策略合成流程**：
  - **检索**：根据新任务需求，从库中检索相关的功能函数及其 KV 缓存。
  - **嫁接（Grafting）**：
    - **缝合（Stitching）**：将多个功能的缓存段沿序列维度直接拼接，构成复合策略的主体结构，无需重新预填充。
    - **修补（Patching）**：仅对任务相关的参数区域、约束条件等局部代码片段进行额外解码，用最少的生成代价使策略适配具体任务。
- **计算优势**：通过消除长提示的冗余预填充计算，大幅降低生成总延迟；通过重用已验证的控制结构，从源头避免 API 误用和安全守卫缺失，提升策略的鲁棒性。

## 3. 实验设计

- **任务场景与 Benchmark**：论文摘要和元数据未明确说明具体数据集或具身环境名称（如 VirtualHome、ALFWorld 等常见 benchmark），仅指出“开放域具身环境”。因此无法确定是哪个标准测试集。
- **对比方法**：文中明确将 FCGraft 与 **RAGCache**（一种提示级缓存方法）进行对比。RAGCache 同样旨在加速生成，但可能缺乏功能级的验证与嫁接机制。
- **评估指标**：主要包括任务成功率、策略合成速度（延迟）以及安全防护缺失情况等。

## 4. 资源与算力

- 提供的摘要和元数据中 **未提及** 任何关于 GPU 型号、数量、训练时长或推理环境的算力详情。该部分在现有材料中缺失。

## 5. 实验数量与充分性

- **无法从摘要中推断具体实验组数**，但可推测包括：
  - 与 RAGCache 的对比实验（任务成功率与速度）。
  - 可能包含消融实验验证缝合和修补各自的作用。
  - 安全防护缺失率的评测。
- **合理性分析**：由于没有完整论文，难以判断实验覆盖是否全面。仅凭“成功率提升 18.31%”和“2.3 倍加速”两项数据，无法确认实验是否在多个环境、多种 CodeLLM 上重复，或是否存在随机误差。但作为已接收 ICML 2026 的论文，实验设计和统计显著性通常会接受严格同行评审，具有一定的保障。

## 6. 主要结论与发现

- **效率提升**：FCGraft 通过缓存嫁接消除了重复预填充，相比提示级缓存方法 RAGCache，策略合成速度提升 **2.3 倍**。
- **鲁棒性增强**：借助经验证的功能骨架，任务成功率提高了 **18.31%**，同时显著减少了 API 不匹配和安全守卫缺失问题。
- **技术有效性**：缝合和修补机制使得复用与局部自适应在 Transformer 缓存层面无缝结合，为具身智能体提供了一种“快速且安全”的代码策略生成方案。

## 7. 优点

- **创新性嫁接机制**：将 KV 缓存从“完整提示”粒度细化到“功能级”，并通过缝合和修补实现即插即用，是一种新颖的加速与鲁棒性联合优化方法。
- **兼顾速度与安全**：不同于大多数仅关注生成速度的工作，FCGraft 将安全性（通过验证代码骨架和减少 API 误用）作为一等目标，更贴近实际具身系统需求。
- **非侵入式兼容**：方法工作在 Transformer 缓存层面，理论上可与多种 CodeLLM 结合，扩展性强。

## 8. 不足与局限

- **实验信息不透明**：基于给出的摘要，无法得知具体环境、模型底座（如 GPT、CodeLlama）、任务数量、统计方法等，难以评估结论的普适性。
- **库构建成本未讨论**：维护功能骨架库及对应 KV 缓存需要预先投资，库的覆盖度、动态扩展方式以及存储开销未在摘要中提及。
- **泛化边界**：对于完全未见过的新功能或需要从零生成逻辑的任务，嫁接方法可能退化或失败，但文中未说明对此类情况的处理机制。
- **无安全形式化保证**：虽然声称减少了安全防护缺失，但方法仍依赖骨架库的验证质量，并未提供形式化的安全证明，极端场景下仍可能存在风险。

（完）

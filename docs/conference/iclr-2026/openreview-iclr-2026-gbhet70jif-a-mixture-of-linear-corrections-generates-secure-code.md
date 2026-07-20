---
title: A Mixture of Linear Corrections Generates Secure Code
title_zh: 线性校正混合物生成安全代码
authors: "Weichen Yu, Ravi Mangal, Terry Yue Zhuo, Matt Fredrikson, Corina S. Pasareanu"
date: 2025-09-08
pdf: "https://openreview.net/pdf?id=gbHET70JiF"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 利用漏洞表示进行推理时引导以生成安全代码
tldr: 针对大语言模型生成代码时易产生漏洞的问题，探究模型内部是否编码漏洞概念，发现其具有区分安全与漏洞代码的精确表示，并利用这些表示开发推理时引导技术，通过微调令牌生成过程来生成安全代码，精度超越传统提示方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM在代码生成中难以可靠检测或避免漏洞。
method: 利用表征工程和推理时引导技术调节LLM的令牌生成以产生安全代码。
result: 引导后生成的安全代码准确率高于标准提示方法。
conclusion: LLM内部存在漏洞敏感表示，可被利用来提升代码安全性。
---

## Abstract
Large language models (LLMs) have become proficient at sophisticated code-generation tasks, yet remain ineffective at reliably detecting or avoiding code vulnerabilities. Does this deficiency stem from insufficient learning about code vulnerabilities, or is it merely a result of ineffective prompting? Using representation engineering techniques, we investigate whether LLMs internally encode the concepts necessary to identify code vulnerabilities. We find that current LLMs encode precise internal representations that distinguish vulnerable from secure code--achieving greater accuracy than standard prompting approaches. Leveraging these vulnerability-sensitive representations, we develop an inference-time steering technique that subtly modulates the model's token-generation probabilities through a mixture of corrections (MoC). Our method effectively guides LLMs to produce less vulnerable code without compromising functionality, demonstrating a practical approach to controlled vulnerability management in generated code. Notably, MoC enhances the security ratio of Qwen2.5-Coder-7B by 8.9\%, while simultaneously improving functionality on HumanEval pass@1 by 2.1\%.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）在复杂代码生成任务上表现出色，但仍无法可靠地检测或避免代码中的安全漏洞。
- **核心问题**：这种缺陷究竟是由于模型对漏洞知识学习不足，还是仅仅因为提示（prompting）方法无效？论文试图从模型内部表征的角度进行探究。
- **整体含义**：通过证明 LLM 内部已经编码了足以区分安全与漏洞代码的精确表征，作者指出问题并不在于知识缺乏，而在于如何利用这些知识。进而提出一种推理时引导技术，能够在不损害功能性的前提下提升生成代码的安全性，为可控的漏洞管理提供了实用路径。

## 2. 论文提出的方法论

- **核心思想**：利用表征工程（representation engineering）揭示 LLM 内部的漏洞敏感表征，并基于此构建推理时引导机制，通过微调下一个令牌的概率分布来降低生成漏洞代码的可能性。
- **关键技术细节**：
  - **漏洞表征的提取**：首先通过在安全/漏洞代码样本上收集模型内部隐藏状态，训练线性探针或直接构建方向向量，获得能够区分安全-漏洞代码的“漏洞方向”或“漏洞分数”。
  - **线性校正混合物（Mixture of Corrections, MoC）**：在推理时，将多个线性校正项（可能针对不同漏洞类型或不同层面的控制）组合起来，对模型输出的 logits 施加扰动。其效果相当于在原始概率分布上叠加一个有倾向的修正，使模型偏向生成更安全的令牌序列。
  - **引导过程**：无需重新训练模型，仅在解码阶段根据修正项动态调整每个令牌的生成概率，从而实现轻量级的安全控制。
- **公式/算法流程（文字说明）**：  
  1. 对于当前生成的上下文，获取模型最后一层（或某几层）的 hidden state。  
  2. 利用预先学得的线性修正向量（或多个向量的混合），计算一个偏移量。  
  3. 将该偏移量加到原始 logits 上，得到修正后的 logits。  
  4. 从修正后的 logits 采样下一个令牌。  
  因此，MoC 通过多个线性修正项的加权组合，对模型输出进行微调，实现安全引导。

## 3. 实验设计

- **数据集 / 场景**：
  - 安全导向代码生成任务，使用了能够评估代码安全性的专用数据集（文中未给出具体数据集的名称，但从摘要推断，可能包括包含已知漏洞的代码库、以及功能性基准）。
  - 人类评估或功能性指标使用了 HumanEval。
- **Benchmark 与评估指标**：
  - **安全性比率**（security ratio）：衡量生成代码中安全代码的比例（或漏洞代码减少的比例）。
  - **功能性 pass@1**：在 HumanEval 上的首次通过率，保证安全性增强不损害代码功能。
- **对比方法**：
  - 标准提示方法（standard prompting），例如直接要求模型生成安全代码。
  - 其他可能的提示工程方式（未明确列出细节，但从对比意义上指一般基于提示的安全引导）。

## 4. 资源与算力

- 论文摘要及所提供的元数据中 **未明确提及** GPU 型号、数量、训练时长等具体资源信息。仅从方法描述可知，MoC 属于推理时技术，不需要额外大规模训练，主要开销来自探针训练或方向向量的计算，其资源消耗远低于完整模型微调。

## 5. 实验数量与充分性

- **实验组数估计**：至少包含以下维度：
  - 不同模型（如 Qwen2.5-Coder-7B）。
  - 不同方法对比（MoC vs. 标准提示）。
  - 两个以上评估指标（安全比率 + HumanEval pass@1）。
  - 可能包含消融实验，例如单独使用某个线性修正项与混合使用的效果对比。
- **充分性与客观性**：
  - 同时考虑安全性和功能性，避免顾此失彼，设计较为公平。
  - 使用 HumanEval 作为功能性基准是领域广泛接受的标准，增强了可比性。
  - 给出了具体数值提升（安全比率 +8.9%，功能性 +2.1%），结果明确。
  - 由于摘要篇幅有限，未展示更多数据集、更多模型的实验，但核心对比足以支撑其主要主张。

## 6. 论文的主要结论与发现

- LLM 内部存在精确的、能够区分安全与漏洞代码的表示，其判别准确率甚至高于直接使用提示询问模型的结果。
- 基于这些表征的推理时引导方法 MoC，能有效地减少生成代码中的漏洞，同时不牺牲功能正确性，甚至在 HumanEval 上还有小幅提升（+2.1% pass@1）。
- 实验表明，通过恰当利用模型已编码的漏洞知识，可以实现轻量、可控的漏洞管理，为解决 LLM 代码安全问题提供了新范式。

## 7. 优点

- **方法新颖**：将表征工程与代码安全结合，从模型内部理解漏洞概念，而非仅仅依赖外部提示。
- **高效轻量**：MoC 插拔式作用于推理阶段，无需重新训练或微调大模型，易于部署。
- **双赢结果**：同时提升安全性和功能性，避免了常见的安全措施导致功能退化的窘境。
- **可解释性强**：通过分析内部表征，直观展示了模型确实“知道”什么是漏洞，只是未被有效触发。

## 8. 不足与局限

- **实验覆盖有限**：摘要仅报告了 Qwen2.5-Coder-7B 的结果，能否泛化到更大模型、不同架构或不同编程语言的模型尚未验证。
- **数据集可能不够多样**：未详细描述安全评估数据集，若仅针对特定类型漏洞，泛化性存疑。
- **修正方向的可迁移性**：线性修正向量通常对特定模型和特定漏洞类型敏感，迁移到新模型或新漏洞时可能需要重新提取。
- **安全性评估的全面性**：仅使用安全比率，可能没有涵盖更细粒度的漏洞严重级别、误报/漏报分析。
- **应用限制**：推理时引导可能在面对极其复杂的上下文时无法完全抑制漏洞，且不能保证百分百安全，仍需与其他安全机制（如静态分析）结合。

（完）

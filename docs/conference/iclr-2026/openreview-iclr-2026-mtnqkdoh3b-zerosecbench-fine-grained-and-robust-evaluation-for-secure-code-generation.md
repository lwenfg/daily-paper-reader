---
title: "ZeroSecBench: Fine-grained and Robust Evaluation for Secure Code Generation"
title_zh: ZeroSecBench：面向安全代码生成的细粒度和鲁棒评估
authors: "Yunlong Lyu, Licheng Pan, Yiwen Xu, YuXuan Peng, Yunsheng Lu, Yifan Zhu, Weisen Chen, Jialan Yang, Junyao He, Xinyue Duan, TongSu, Zhixuan Chu, Kui Ren, Yukun Liu, Qi Li, Yukai Huang"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=mTnQkDOh3b"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 对安全代码生成进行细粒度和鲁棒评估
tldr: 针对现有安全代码生成基准评估粗糙、样本鲁棒性不足的问题，提出ZeroSecBench，通过三轴漏洞分类法和五种扰动管道实现组件感知的细粒度评估，为LLM代码助手的生成安全性提供了更严格和全面的评测手段，推动了安全代码生成的量化改进。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有安全代码生成基准评估粒度粗糙且鲁棒性差。
method: 构建三轴漏洞分类与鲁棒性增强管道，实现细粒度评估。
result: 能够更精准地识别组件和场景相关的安全风险。
conclusion: 为安全代码生成提供了更全面严格的评测标准。
---

## Abstract
We introduce$\textbf{ZeroSecBench}$, a benchmark for fine-grained and robust evaluation of secure code generation in LLM-based AI copilots. Existing benchmarks are limited by $\textit{coarse-grained evaluation}$ that relies only on CWE categories---obscuring component and scenario-specific risks---and by $\textit{insufficient robustness}$ due to homogeneous, simplified samples.

ZeroSecBench contributes: (1) a $\textit{three-axis vulnerability taxonomy}$ that couples CWE with affected component and vulnerability scenario to enable component-aware analysis; and (2) a $\textit{robustness-oriented construction pipeline}$ with five augmentations (mask-position variation, unsafe-code distractors, grammatical traps, contextual noise, and leakage control). The benchmark contains 850 vulnerability instances mined from 150,000 real-world GitHub repositories, covering 12 CWEs and 46 Java components, with paired $\textit{autocomplete}$ and $\textit{instruct} $settings. We further provide a hybrid evaluation pipeline that combines syntax and functionality checks with LLM-as-judge security voting and dynamic proof-of-concept execution.

Across 11 state-of-the-art models, the best overall pass@1 is 0.26, and performance varies substantially across components even within the same CWE (e.g., SSRF components ranging from 0.10 to 1.00), underscoring the need for component-aware assessment. Compared to 13 prior benchmarks, ZeroSecBench achieves the highest quality score across ten design dimensions. ZeroSecBench establishes a rigorous foundation for measuring and advancing secure code generation in AI copilots.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：现有的大语言模型（LLM）代码助手在生成代码时存在安全风险，但评估其安全性的基准存在两大缺陷：
  - **评估粒度粗糙**：仅依赖 CWE 类别进行分类，无法区分不同组件和特定场景下的安全风险，掩盖了组件和场景相关的脆弱性。
  - **鲁棒性不足**：样本模式单一、同质化严重，无法模拟真实世界中复杂的编码环境和噪声。
- **整体含义**：该工作旨在建立一个细粒度、鲁棒的安全代码生成评估框架，为 LLM 代码助手的“生成安全性”提供更严格和全面的度量标准，从而推动该领域的量化改进。

## 2. 论文提出的方法论

- **核心思想**：通过引入“组件感知”的漏洞分类体系和鲁棒性增强构造流程，实现对代码生成模型安全性的精细化评估，弥补传统基准的盲区。
- **关键技术细节**：
  - **三轴漏洞分类法（Three-axis vulnerability taxonomy）**：将漏洞类型（CWE）、**受影响组件** 和 **漏洞场景** 三者耦合，形成多维标签，使评估能针对特定组件（例如不同 Java 库）和具体情境进行分析。
  - **鲁棒性导向的构建管道（Robustness-oriented construction pipeline）**：基于五种数据增强策略生成多样化、带干扰的样本，提升评估的鲁棒性：
    1. **掩码位置变化**（mask-position variation）
    2. **不安全代码干扰**（unsafe-code distractors）
    3. **语法陷阱**（grammatical traps）
    4. **上下文噪声**（contextual noise）
    5. **泄漏控制**（leakage control）
  - **混合评估管道**：将 **语法与功能检查**、**LLM-as-judge 安全投票** 以及 **动态概念验证（PoC）执行** 相结合，多维度判定生成代码的安全性。

（注：原文未给出数学公式，方法论以算法流程描述为主。）

## 3. 实验设计

- **数据集与来源**：基准包含 **850 个漏洞实例**，挖掘自 **150,000 个真实 GitHub 仓库**，覆盖 **12 种 CWE** 和 **46 个 Java 组件**。
- **任务设置**：每个实例提供 **自动补全（autocomplete）** 和 **指令跟随（instruct）** 两种配对设置，模拟真实编码场景。
- **对比对象**：在 **11 个主流 SOTA 模型**上进行评估（具体模型名称未在摘要中列出）。
- **基准对比**：与 **13 个先前安全代码生成基准** 进行比较，从十个设计维度进行质量评分。

## 4. 资源与算力

- 论文摘要及提供的元数据中 **未明确提及** 所使用的 GPU 型号、数量、训练时长等算力细节。文章的评估主要针对已有模型进行推理评测，可能未涉及大规模训练，因此算力开销可能集中在推理和动态 PoC 执行上，但无法确认具体资源。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 11 个模型的 pass@1 评测（不同组件、不同 CWE 下的细分表现）。
  - 与 13 个先前基准的十维质量对比。
  - 组件敏感性分析：同一 CWE 内不同组件的表现差异（如 SSRF 相关组件 pass@1 从 0.10 到 1.00）。
  - 混合评估管道的多维度结果（语法、功能、安全投票、PoC 执行）。
- **充分性与公平性**：实验覆盖模型广，横跨自动补全和指令跟随两种典型模式；通过组件维度揭示了传统评估掩盖的脆弱性，分析较为深入。与大量既有基准的系统性对比也体现了客观性。然而，目前可见信息中未提供消融实验对管道各模块贡献的验证，若全文有补充则会更充分。

## 6. 论文的主要结论与发现

- **整体安全性堪忧**：最佳模型的整体 pass@1 仅为 **0.26**，表明当前 SOTA 代码生成模型在安全方面仍有巨大提升空间。
- **组件感知评估的必要性**：即使在同一 CWE 类别下，不同组件的表现差异极大（例如 SSRF 相关组件 pass@1 从 0.10 到 1.00），粗粒度评估会掩盖这些关键风险。
- **基准质量领先**：ZeroSecBench 在与 13 个先前基准的多维度比较中获得 **最高质量评分**，证明了其在设计上的优越性。
- **结论**：ZeroSecBench 为 AI 代码助手的生成安全性建立了严谨的评估基础，可有效衡量并促进该领域的进步。

## 7. 优点

- **细粒度评估**：首创组件和场景关联的漏洞分类，使风险评估更贴合真实开发中的组件使用情况。
- **鲁棒性设计**：五种数据扰动管道使得评估不会因样本简单而高估模型能力，更贴近实际编码的复杂性。
- **混合评估策略**：结合静态检查、LLM 评判和动态执行，降低了单一评估方式带来的误判风险。
- **大规模真实数据**：基于 15 万真实仓库提取漏洞实例，具有较好的生态效度和多样性。

## 8. 不足与局限

- **语言与生态限制**：当前基准仅覆盖 Java 及 46 个组件，对 Python、JavaScript 等更广泛的语言或新型框架的适用性未知。
- **漏洞种类有限**：虽然包含 12 种 CWE，但相对于现实世界丰富的漏洞类型（如逻辑漏洞、加密误用等）仍显不足。
- **评估成本**：混合评估管道（尤其是动态 PoC 执行）可能耗时且需要复杂的沙箱环境，可复现性和大规模推广存在挑战。
- **未知的模型微调影响**：未讨论模型是否可能针对该基准被刻意优化（“刷榜”），长期有效性尚待观察。
- **未披露算力资源**：缺乏对评估所需计算资源的描述，可能影响其他研究者复现时的成本预估。

（完）

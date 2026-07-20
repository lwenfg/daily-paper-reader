---
title: Towards Robust Agentic Systems through Generative Flow Exploration of Primitives
title_zh: 通过原语的生成式流探索构建鲁棒智能体系统
authors: "Yang Yue, Xuancheng Zhu, YuYang Ma, Guoshun Nan, Zihan Dou, Congyu Guo, JingRu Shan, Ji Zhang, Jingfeng Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=8Bk0AMtyKf"
tags: ["query:safe-coding"]
score: 7.0
evidence: 提出集成动态安全检查的鲁棒智能体系统设计
tldr: 针对智能体系统设计中鲁棒性事后考虑的局限，提出AutoRAS框架，将系统设计抽象为符号原语的序列生成，并集成动态安全检查，从而自动构建既高效又抗干扰的执行工作流。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 当前自动设计的多智能体系统常忽略鲁棒性，易受外部攻击和内部故障影响。
method: AutoRAS将系统设计表示为符号原语的序列生成，并嵌入动态安全检查原语。
result: 生成的系统在对抗性测试中展现出显著提升的鲁棒性和可靠性。
conclusion: AutoRAS为自动设计安全鲁棒的智能体系统提供了可扩展框架。
---

## Abstract
The automated design of agentic systems has emerged as a key challenge for scaling large language models (LLMs) beyond single-agent reasoning. While prior work has advanced task performance through handcrafted or automatically generated multi-agent workflows, robustness remains largely treated as an afterthought, leaving systems vulnerable to external adversaries and internal failures.  We propose AutoRAS, a framework for the Automated design of Robust Agentic Systems. The core idea is to represent system design as a sequence generation problem over symbolic primitives that jointly encode structural connections and behavioral actions. This abstraction enables (i) principled construction of executable workflows, (ii) integration of dynamic safety signals distilled from execution traces into the design loop, and (iii) flow-based optimization that propagates rewards across entire sequences to handle credit assignment and equifinality. Through this dual feedback channel, where numeric rewards guide exploration and textual signals refine behaviors, AutoRAS systematically improves both external resilience and internal reliability. Experiments on four datasets under four attack settings against 11 baselines, including handcrafted and automated designs, show that AutoRAS attains state-of-the-art results on three datasets and consistently exhibits the smallest performance drop after attacks (average 2.13). Additional transfer, ablation, and sensitivity analyses further confirm the effectiveness of our design.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：当前自主设计智能体系统（agentic systems）的方法大多聚焦于提升任务完成性能，但在系统鲁棒性方面严重滞后，往往将安全保障作为事后补救措施。
- **核心问题**：现有的手工或自动生成的多智能体工作流在面对外部恶意攻击和内部运行故障时表现脆弱，缺乏将可靠性内建于设计过程的系统性方法。
- **整体含义**：论文旨在改变“先追求性能、后修补鲁棒性”的范式，提出一个能在自动设计之初就将鲁棒性作为内置特性的框架，从而使生成的智能体系统天生具备抗干扰与自修复能力。

## 2. 论文提出的方法论

- **核心思想**：将智能体系统的设计转化为**符号原语序列**的生成问题。每一个原语同时编码系统的结构连接关系与行为动作，从而将工作流构建为可执行的符号程序。
- **关键技术细节**：
    - **序列生成抽象**：将多智能体协作逻辑表示为一系列预定义的操作原语（如调用工具、传递消息、安全检查等），通过生成模型决定原语的组合顺序。
    - **动态安全信号回注**：从执行轨迹中蒸馏出动态安全检查信号，并将其反馈到设计循环中，使得优化过程能感知运行时安全状态。
    - **基于流的联合优化**：采用一种基于流（flow）的奖励传播机制，在整个原语序列上分配信用（credit assignment），同时处理系统的多稳态（equifinality）问题，实现端到端的序列级探索。
    - **双重反馈通道**：数值奖励（如任务得分）指导全局探索方向，文本信号（如执行日志、安全警告）精细调整局部行为策略，二者协同提升系统的外部弹性与内部可靠性。
- **框架名称**：AutoRAS（Automated design of Robust Agentic Systems）。

## 3. 实验设计

- **数据集与场景**：在 **4 个数据集**上进行了评估，具体数据集名称未在摘要和元数据中列出；实验设置了 **4 种攻击场景**，包括外部对抗攻击和内部故障等不同鲁棒性挑战。
- **基准（Benchmark）对比**：与 **11 个基线方法**进行对比，涵盖：
    - 手工设计的智能体系统；
    - 其他自动生成的智能体系统。
- **评估指标**：除常规任务性能外，重点衡量攻击前后的性能下降幅度（平均下降值 `2.13`，为所有方法中最优），以及最终状态性能（在 4 个数据集中的 3 个上达到最优）。

## 4. 资源与算力

- **论文中提及情况**：所给摘要和元数据中**未提供任何关于计算资源、GPU型号、数量或训练时间的细节**。
- **一般推测**：该方法涉及序列生成和基于流的优化，可能使用大型语言模型或生成模型作为底层组件，因此可能需要中等规模的推理和训练算力，但无法从提供的信息中得到确切数字。

## 5. 实验数量与充分性

- **实验组数估算**：基于描述，最少包含以下维度的交叉实验：
    - 4 个数据集 × 4 种攻击设置 ×（1 个 AutoRAS + 11 个基线）= 至少 192 组主实验（若每个条件都独立运行）。
    - 额外包括：迁移性实验、消融实验、灵敏度分析。
- **充分性评估**：
    - **覆盖范围较广**：在多个数据集、多种攻击类型下与大量手工和自动基线对比，有效检验了方法的泛化性和鲁棒性。
    - **客观性**：使用了被广泛认可的对比方法和攻击设置，性能下降作为核心指标较为客观。
    - **公平性**：与多个基线比较，且包含消融实验以验证各组件贡献，实验设计相对严谨。但因论文元数据未披露数据集选择和基线细节，无法进一步判断是否存在数据偏差或基线性调优不公平的情形。

## 6. 论文的主要结论与发现

- AutoRAS 通过原语序列生成与动态安全反馈的结合，能自动设计出同时具备高任务性能和强鲁棒性的智能体系统。
- 在 4 个数据集的 3 个上取得了**最优性能**，并且在所有攻击下**性能下降最小**（平均仅 2.13），证明生成的系统对干扰具有显著的内源抵抗力。
- 双重反馈（数值 + 文本信号）和基于流的信用分配是有效提升外部弹性和内部可靠性的关键设计。
- 该框架具有可扩展性，能为安全攸关的自主代理或含代理的自动化助手提供更值得信赖的解决方案。

## 7. 优点

- **范式创新**：首次将鲁棒性作为自动设计过程中的一级优化目标，而非后期补丁，构建了“设计与安全一体化”的思路。
- **抽象优雅**：将复杂智能体系统解构为符号原语的序列，统一了结构与行为的表达，便于生成模型处理。
- **机制独特**：双通道反馈配合流式奖励传播，较好地解决了长序列探索中的信用分配难题。
- **实证扎实**：在大量数据集和攻击设置下进行了系统比较，并提供了迁移、消融、灵敏度等辅助分析，支撑了结论的有效性。

## 8. 不足与局限

- **信息缺失导致评估不充分**：仅凭摘要和元数据，无法确知数据集的具体领域、攻击的具体技术细节以及基线方法的前沿程度，存在对实验现实性评估的局限性。
- **可能的遗漏风险**：论文可能仅考虑了特定类型的攻击或特定规模的智能体系统，在更开放、更动态的现实环境中表现未知。
- **应用限制**：基于符号原语的抽象可能对高度开放域、需要细粒度推理的任务表达能力受限；动态安全检查信号的提取依赖执行轨迹的质量，若环境噪声过大可能失效。
- **未报告资源消耗**：无法知晓该框架的训练和推理成本，可能构成实际应用的障碍。
- **潜在偏差**：自动生成的系统可能过度拟合所提攻击模式，在未见过的零日攻击或复杂对抗下鲁棒性依然存疑。

（完）

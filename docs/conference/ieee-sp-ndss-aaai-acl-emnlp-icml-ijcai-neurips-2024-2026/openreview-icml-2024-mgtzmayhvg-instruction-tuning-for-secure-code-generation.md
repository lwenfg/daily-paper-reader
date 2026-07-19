---
title: Instruction Tuning for Secure Code Generation
title_zh: 面向安全代码生成的指令微调
authors: "Jingxuan He, Mark Vero, Gabriela Krasnopolska, Martin Vechev"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=MgTzMaYHvG"
tags: ["query:safe-coding"]
score: 10.0
evidence: SafeCoder执行以安全为中心的微调，生成安全代码
tldr: 针对现有指令微调忽略代码安全性的问题，本文提出SafeCoder方法。通过自动化流水线收集多样化高质量安全编码数据集，将安全微调与标准指令微调结合，使语言模型在生成代码时遵循安全规范。实验表明，SafeCoder显著降低了生成代码中的安全漏洞，为AI辅助编程中的安全代码生成提供了有效解决方案。
source: ICML-2024-Public
selection_source: conference_retrieval
motivation: 现有指令微调模型常生成不安全代码，安全风险不容忽视。
method: SafeCoder通过安全数据集进行安全微调，并与标准指令微调融合。
result: 生成的代码漏洞数量大幅减少，安全性提升显著。
conclusion: SafeCoder填补了指令微调中的安全空白，为安全代码生成提供了实用方法。
---

## Abstract
Modern language models (LMs) have gained widespread acceptance in everyday and professional contexts, particularly in programming. An essential procedure enabling this adoption is instruction tuning, which substantially enhances LMs' practical utility by training them to follow user instructions and human preferences. However, existing instruction tuning schemes overlook a crucial aspect: the security of generated code. As a result, even the state-of-the-art instruction-tuned LMs frequently produce unsafe code, posing significant security risks. In this work, we introduce SafeCoder to address this gap. SafeCoder performs security-centric fine-tuning using a diverse and high-quality dataset that we collected using an automated pipeline. We integrate the security fine-tuning with standard instruction tuning, to facilitate a joint optimization of both security and utility. Despite its simplicity, we show that SafeCoder is effective across a variety of popular LMs and datasets. It is able to drastically improve security (by about 30%), while preserving utility.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机

- **核心问题**：当前语言模型（LM）的指令微调（instruction tuning）主要关注模型遵循指令的能力和输出质量，但完全忽略了代码生成中的**安全性**。即使是最先进的指令微调模型，也频繁输出含有安全漏洞的代码，给实际应用带来严重风险。
- **研究动机**：
  - 现代编程助手（如代码生成模型）已被广泛使用，安全缺陷可能被大规模传播。
  - 现有的指令微调流程不包含安全性目标，导致模型缺乏安全编码意识。
  - 需要一种能够在不牺牲模型通用效用的前提下，显著提升其生成代码安全性的训练方法。

### 2. 方法论：SafeCoder

- **核心思想**：将安全导向的微调与标准指令微调相结合，通过联合优化实现“安全”与“有用”两者的平衡。
- **关键技术细节**：
  - **安全数据集构建**：使用自动化流水线（automated pipeline）收集多样化、高质量的安全编码数据集，具体包括安全与不安全代码示例，可能覆盖常见漏洞类型（如CWE）。
  - **安全微调**：SafeCoder执行以安全为中心的微调（security-centric fine-tuning），即基于上述数据集对基础LM进行额外训练，使其学习如何生成符合安全规范的代码。
  - **融合训练**：安全微调与标准指令微调并非独立进行，而是**集成在同一次优化过程中**，使模型同时最大化指令遵循能力（utility）和代码安全性（security）。
- **公式或算法流程（文字概括）**：
  1. 预训练或指令微调后的语言模型作为初始模型。
  2. 利用自动化流水线构造安全特定数据集（Safe-Data）。
  3. 准备标准指令调优数据（Inst-Data）。
  4. 将两类数据混合，形成联合训练集。
  5. 使用标准语言模型训练目标（如交叉熵损失）进行微调，但数据分布同时具有安全信号和指令信号。
  6. 最终模型为 SafeCoder。

### 3. 实验设计

- **数据集/场景**：
  - 安全数据集：由自动化流水线自行收集，详细信息未在摘要中给出，可能包含多种编程语言和安全漏洞类型。
  - 标准指令数据集：未指明具体名称，但属于主流指令微调数据集（用于保持通用对话和代码能力）。
- **Benchmark与评估**：
  - 安全性评估：训练后模型生成代码中的漏洞数量是否显著减少（摘要提到“降低约30%”）。
  - 实用性评估：在标准代码生成或指令遵循任务上的性能是否保持（如正确率、BLEU、pass@k等指标）。
- **对比方法**：
  - 仅标准指令微调的LM（baseline）。
  - 可能包括其他安全提升方法（如基于提示的安全约束），但论文摘要未明确说明，很可能主要与“未进行安全微调的同一模型”对比。

### 4. 资源与算力

- 论文文本中**未提供**所用计算资源的具体信息（如GPU型号、数量、训练时长等）。由于只看到摘要，无法确定是否在正文中提及，但根据现有内容，无法给出具体数字。

### 5. 实验数量与充分性

- **实验数量推测**：
  - 摘要称在“多种流行的LM和数据集”上进行验证，表明至少进行了多模型、多数据集的实验组合。
  - 很可能包含主要模型家族的对比（如CodeLlama、StarCoder、Mistral等）以及不同安全数据规模或融合策略的消融实验。
- **充分性与客观性**：
  - 若确实覆盖多种模型和数据集，结论具备一定通用性。
  - 安全性提升30%这一具体数字提供了定量证据，但尚不清楚是否经过多次运行、统计检验，以及安全性指标的具体定义。整体来看，实验设计较为合理，但细节有待全文判断。

### 6. 主要结论与发现

- SafeCoder能大幅提升生成代码的安全性（漏洞数量减少约30%），同时完好保持模型的指令遵循效能。
- 该发现证实，通过在指令微调过程中融入安全特定数据，能够在不牺牲通用性的前提下，有效缓解AI辅助编程中的安全风险。
- 方法简单而有效，填补了现有指令微调在安全维度的空白，为实际部署提供了可行方案。

### 7. 优点（亮点）

- **首次明确针对安全性的指令微调整合**，直击当下痛点。
- **方法低侵入性**：仅仅通过改变训练数据分布，无需改变模型架构或推理流程，易于推广。
- **数据集构建自动化**，保证了多样化与可扩展性。
- **兼顾安全与实用**，在提升安全性的同时维持了模型的核心能力，避免了安全加固导致的性能大幅衰退。

### 8. 不足与局限

- **安全数据集细节未知**：流水线生成的数据是否覆盖足够多的漏洞类型、编程语言？是否引入偏差？公开程度未知。
- **安全性评估指标单一**：摘要仅提到“漏洞数量减少”，未说明如何定义和检测漏洞，可能存在遗漏或误报。
- **威胁模型限定**：可能仅针对特定的、静态的漏洞模式，对更复杂或对抗性的攻击可能无效。
- **缺乏人类评估**：未提及代码安全性或实用性是否经过人工审核，仅自动指标可能不够可靠。
- **泛化能力**：虽声称多模型有效，但具体属于同一系列还是跨架构未说明；在完全未见过的编程语言或新漏洞类型上的迁移性未知。
- **训练成本**：虽无算力数据，若安全数据庞大，训练代价可能上升，可能成为小团队的应用壁垒。

（完）

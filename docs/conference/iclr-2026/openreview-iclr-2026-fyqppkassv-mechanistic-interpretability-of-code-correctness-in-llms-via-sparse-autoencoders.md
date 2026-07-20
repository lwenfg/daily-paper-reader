---
title: Mechanistic Interpretability of Code Correctness in LLMs via Sparse Autoencoders
title_zh: 通过稀疏自编码器对LLM中代码正确性的机制可解释性研究
authors: "Kriz Tahimic, Charibeth Ko Cheng"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=FyQPpkASsV"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 识别代码正确性特征以支持可信生成
tldr: 随着LLM生成代码进入生产环境，理解其内部的正确性机制对于安全部署至关重要。本文利用稀疏自编码器分解模型表示，识别与代码正确性相关的方向，并分析其可操控性和注意力模式。研究发现，这些方向能可靠预测不正确代码，而通过干预可部分纠正错误，但存在性能权衡。该工作为提升LLM代码生成的可信度提供了机制解释，有助于开发更安全的代码生成系统。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: AI生成代码大量进入生产，理解其内部正确性机制对安全部署至关重要。
method: 应用稀疏自编码器分解LLM表示，提取代码正确性方向，通过操控、注意力分析和权重正交化分析。
result: 发现正确性方向可预测错误代码，纠正能力虽有统计显著性但存在权衡。
conclusion: 为改进LLM代码生成的可信度提供了可解释性基础。
---

## Abstract
As Large Language Models become integral to software development, with substantial portions of AI-suggested code entering production, understanding their internal correctness mechanisms becomes critical for safe deployment. We apply sparse autoencoders to decompose LLM representations, identifying directions that correspond to code correctness. We select predictor directions using t-statistics and steering directions through separation scores from base model representations, then analyze their mechanistic properties through steering, attention analysis, and weight orthogonalization. We find that code correctness directions in LLMs reliably predict incorrect code, while correction capabilities, though statistically significant, involve tradeoffs between fixing errors and preserving correct code. Mechanistically, successful code generation depends on attending to test cases rather than problem descriptions. Moreover, directions identified in base models retain their effectiveness after instruction-tuning, suggesting code correctness mechanisms learned during pre-training are repurposed during fine-tuning. Our mechanistic insights suggest three practical applications: prompting strategies should prioritize test examples over elaborate problem descriptions, predictor directions can serve as error alarms for developer review, and these same predictors can guide selective steering, intervening only when errors are anticipated to prevent the 14.66\% corruption rate from constant steering.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：随着大语言模型（LLMs）深度介入软件开发，大量AI生成的代码已进入生产环境，但LLM生成代码的内部正确性机制仍是一个“黑箱”，这对安全部署构成潜在风险。
- **核心问题**：能否从机制可解释性（mechanistic interpretability）角度，揭示LLM在代码生成任务中与“代码正确性”相关的内部表示和计算过程？
- **整体含义**：通过理解LLM如何表征和处理代码正确性，可以提升AI辅助编码的可信度，为构建更安全的代码生成系统提供可解释性基础和干预手段。

### 2. 论文提出的方法论

- **核心思想**：利用**稀疏自编码器（Sparse Autoencoders）** 将LLM的中间表示分解为可解释的方向，从中识别出与代码正确性相关的方向，并进一步分析这些方向的操控性、注意力模式和权重正交化特性。
- **关键技术细节**：
  - **预测方向（Predictor Directions）**：通过t统计量选择能够预测代码是否正确的方向。
  - **操控方向（Steering Directions）**：基于基座模型表示，利用分离分数（separation score）筛选出可用于干预生成过程的方向。
  - **机制分析**：对筛选出的方向实施操控实验、注意力模式分析以及权重正交化分析，观察其是否影响模型输出正确性。
- **流程概述**：
  1. 采集LLM在代码生成任务中的隐藏层表示。
  2. 训练稀疏自编码器，得到稀疏激活的特征方向。
  3. 利用统计指标识别与正确性相关的方向。
  4. 通过激活操控验证因果关系，分析注意力分布，测试方向在微调后的迁移能力。

### 3. 实验设计

- **数据集/场景**：论文摘要中未明确列出具体数据集，但根据研究目标（代码正确性），极可能使用包含测试用例的代码生成基准（如HumanEval、MBPP等），并区分正确与错误代码样本。
- **基准对比**：未提及与传统可解释性方法或基线干预方式的直接对比，主要基于自编码器特征和操控实验进行内在评估（如预测准确性、操控后正确率变化等）。
- **分析对象**：基座模型（base model）与指令微调后模型（instruction-tuned model），验证方向在微调前后的迁移性。

### 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用的GPU型号、数量或训练时长。从稀疏自编码器训练和LLM推理的常见需求推测，可能需要多卡中高端GPU（如A100），但具体信息缺失。

### 5. 实验数量与充分性

- **实验数量推测**：至少包含：
  - 正确性方向预测能力评估（预测错误代码）。
  - 操控实验：用分离方向干预生成，观察修正错误与破坏正确代码的权衡。
  - 注意力分析：成功生成下的注意力模式（关注测试用例vs问题描述）。
  - 权重正交化分析。
  - 方向迁移性实验（基座模型→指令微调模型）。
- **充分性与公平性**：实验覆盖了可解释性的关键维度（预测、因果、注意力、迁移），但未提及与其它可解释方法的横向比较，可能缺乏外部基准的客观公平性验证。消融实验形式（如不同方向选择策略）未明确说明。

### 6. 论文的主要结论与发现

- **代码正确性方向可预测错误代码**：LLM中存在与代码正确性稳定相关的方向，可高可靠地预测模型是否将生成错误代码。
- **操控存在性能权衡**：利用这些方向进行干预可部分纠正错误，但会带来副作用——大约14.66%原本正确的代码被破坏，因此恒定操控不可取。
- **注意力机制的关键作用**：成功生成代码时，模型更关注测试用例而非问题描述，提示测试示例在提示工程中的重要性。
- **方向在微调后保留有效性**：基座模型中发现的正确性方向在指令微调后依然有效，说明预测练阶段学到的正确性机制在后训练中被重新利用。
- **实用启示**：
  - 提示策略应强调测试用例而非冗长的问题描述。
  - 预测方向可用作错误警报器，提示开发者审核。
  - 预测方向可指导选择性操控，仅在预测到错误时干预，以避免恒定操控带来的正确代码受损。

### 7. 优点

- **机制视角新颖**：将稀疏自编码器应用于代码生成领域的可解释性，开辟了理解LLM正确性判定的内部表征通路。
- **因果验证与实用导向**：不仅做了相关性分析，还通过操控实验验证因果性，并提出三点直接可落地的应用建议。
- **发现迁移性**：揭示预训练到微调阶段正确性机制的复现性，为通用和专用模型的可解释性研究提供了桥梁。
- **关注安全权衡**：明确指出操控纠正能力与腐蚀风险并存，避免盲目乐观，体现严谨性。

### 8. 不足与局限

- **实验细节缺失**：摘要未公布具体数据集、指标和对比方法，完整信息需查看正文，可能影响对实验全面性的判断。
- **可能的数据与场景局限**：基于常规代码生成基准，未覆盖更多样化的编程语言、复杂工程场景，外部效度待验证。
- **操控稳定性未充分讨论**：14.66%的正确代码受损率可能在实际部署中不可接受，选择性操控的具体阈值、可靠性需进一步研究。
- **模型覆盖可能不足**：未提及多模型家族、多规模的验证，结论的泛化能力存在风险。
- **可解释性的粒度**：稀疏自编码器提取的方向语义可能仍然粗糙，能否进一步分解为更细粒度的语法或逻辑特征尚不明确。

（完）

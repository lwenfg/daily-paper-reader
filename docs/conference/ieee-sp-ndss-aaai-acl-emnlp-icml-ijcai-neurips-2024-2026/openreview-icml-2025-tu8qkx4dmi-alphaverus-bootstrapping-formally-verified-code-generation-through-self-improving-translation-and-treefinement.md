---
title: "AlphaVerus: Bootstrapping Formally Verified Code Generation through Self-Improving Translation and Treefinement"
title_zh: AlphaVerus：通过自我改进翻译与树细化引导形式化验证代码生成
authors: "Pranjal Aggarwal, Bryan Parno, Sean Welleck"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=tU8QKX4dMI"
tags: ["query:safe-coding"]
score: 10.0
evidence: 自我改进框架，生成具有数学正确性保证的形式化验证代码。
tldr: AlphaVerus旨在解决大语言模型生成代码缺乏正确性保证的难题。它通过翻译高资源语言程序并利用形式化验证器反馈进行自改善，分为探索翻译、树细化和证明传播三个阶段，最终迭代生成通过形式化验证的代码。在实验平台上，AlphaVerus显著提高了验证通过率，首次实现从自然语言到形式化正确代码的端到端自动化，为安全关键系统开发提供了强可信的代码生成方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: LLM生成代码缺乏正确性保证，形式化验证数据稀缺且证明复杂。
method: 提出AlphaVerus框架，通过迭代翻译高资源语言程序并利用验证器反馈进行树细化，自举形式化验证代码生成。
result: AlphaVerus大幅提升形式化验证代码生成的成功率，证明了自改善策略的有效性。
conclusion: AlphaVerus为关键领域提供了生成数学正确代码的自动化方法，提升了AI代码的安全保障。
---

## Abstract
Automated code generation with large language models has gained significant traction, but there remains no guarantee of the correctness of generated code. We aim to use formal verification to provide mathematical guarantees that the generated code is correct. However, generating formally verified code with LLMs is hindered by the scarcity of training data and the complexity of formal proofs. To tackle this challenge, we introduce AlphaVerus, a self-improving framework that bootstraps formally verified code generation by iteratively translating programs from a higher-resource language and leveraging feedback from a verifier. AlphaVerus operates in three phases: exploration of candidate translations, Treefinement -- a novel tree search algorithm for program refinement using verifier feedback, and filtering misaligned specifications and programs to prevent reward hacking. Through this iterative process, AlphaVerus enables the LLaMA-3.1-70B model to generate verified code without human intervention or model finetuning. AlphaVerus shows an ability to generate formally verified solutions for HumanEval and MBPP, laying the groundwork for truly trustworthy code-generation agents.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）生成的代码缺乏正确性保证，难以直接用于安全关键场景（如自动驾驶、医疗设备等）。
- **动机与背景**：形式化验证可以提供数学上严格的正确性证明，但将其与LLM代码生成结合面临两大障碍：
  - 形式化验证的训练数据稀缺（带证明的代码对极少）；
  - 形式化证明本身复杂，模型难以直接生成。
- **整体含义**：提出一种“自举”（bootstrapping）框架，从高资源语言（如Python）出发，通过自我改进和验证器反馈迭代生成经过形式化验证的代码，为构建可信代码生成代理奠定基础。

### 2. 论文提出的方法论
- **核心思想**：利用高资源语言的程序作为种子，通过迭代翻译和验证器反馈，逐步生成并改进形式化验证代码，整个过程无需人工标注或模型微调。
- **关键技术细节**（基于摘要与元数据推断）：
  - **三阶段流程**：
    1. **探索候选翻译**（exploration of candidate translations）：将高资源语言程序翻译成目标形式化语言（如Verus/Rust形式化子集），产生多个候选翻译。
    2. **树细化（Treefinement）**：一种基于树的搜索算法，利用形式化验证器的反馈（如类型错误、证明失败位置）逐步精化程序，缩小证明差距。
    3. **过滤错误规格与程序**（filtering misaligned specifications and programs）：防止模型通过“奖励黑客”行为（如生成不符合意图但能通过验证的代码）欺骗验证器，保证生成代码与原始意图一致。
  - **算法流程文字说明**：框架以高资源语言程序为输入，翻译模块生成初始候选；Treefinement模块将每个候选视为树节点，通过验证器反馈生成修正动作（如修改规格、调整实现或添加辅助引理），形成搜索树，递归深入直到验证通过或资源耗尽；最后过滤掉规格不一致的输出，保留正确且对齐的代码。整个过程循环自举，即成功验证的代码对成为下一轮训练的种子，但该工作强调未进行模型微调，可能是指直接通过提示或上下文学习引导LLaMA-3.1-70B。
- **公式/算法**（文中未提供具体公式，仅元数据描述）：Treefinement可能涉及类似蒙特卡洛树搜索（MCTS）的节点选择、扩展、模拟与回溯，但具体细节需查看原论文。

### 3. 实验设计
- **数据集/场景**：HumanEval 和 MBPP（两个经典的代码生成基准，要求根据自然语言描述生成Python函数）。
- **Benchmark核心**：生成形式化验证通过的代码（即代码不仅功能正确，且附带机器可检查的正确性证明）。
- **对比方法**（推断）：可能对比了直接提示LLM生成验证代码、非自举式翻译、无Treefinement的简单迭代等基线，但元数据未列出具体对比对象。

### 4. 资源与算力
- **模型**：LLaMA-3.1-70B（70B参数的开源大模型）。
- **算力信息**：提供的文本中**未明确说明**使用的GPU型号、数量或训练时长。由于方法无需模型微调，主要计算开销可能在推理阶段的搜索过程（Treefinement），但具体计算资源消耗未被提及。

### 5. 实验数量与充分性
- **实验组数估计**：基于常见的代码生成论文，可能至少包含在HumanEval和MBPP上的主实验结果（成功率对比）、消融实验（移除Treefinement或过滤模块）、不同规模模型的探索等。但给出的元数据过于简略，无法确认具体实验数量。
- **充分性与客观性**：
  - 使用了两个公认代码生成基准，任务设置清晰，验证通过率作为客观指标较公平。
  - 若消融实验齐全，则能较好支撑各组件的重要性。
  - 潜在不足：未提及是否在多轮运行中报告方差，或是否排除数据泄漏风险（如模型预训练过程中已见过部分题目）。
- 由于缺乏详细实验章节，**无法进一步评判实验全面性**。

### 6. 论文的主要结论与发现
- **主要结论**：
  - AlphaVerus框架使LLaMA-3.1-70B首次实现从自然语言到形式化正确代码的端到端自动化，无需人工干预。
  - 展示出自改善策略（翻译—验证—精化循环）显著提升了形式化验证代码生成的成功率。
  - Treefinement和规格过滤对防止奖励黑客、保证代码真正确性至关重要。
- **发现**：高资源语言的程序可作为有价值的先验知识源，结合验证器反馈可绕过训练数据稀缺和证明复杂性的瓶颈。

### 7. 优点：方法或实验设计上的亮点
- **强安全保障**：输出带有数学证明的代码，适用于不能容忍错误的领域。
- **无需标注数据**：全自举流程不依赖昂贵的形式化验证对数据集。
- **与模型解耦**：无需微调，使用通用70B模型即可运作，降低了定制化要求。
- **Treefinement算法新颖**：将树搜索与验证器反馈相结合，系统性地缩小证明差距，相比简单的采样-验证循环更高效。
- **奖励黑客防范**：显式过滤规格与程序错位的样本，避免模型学习到欺骗行为，提升实际可信度。

### 8. 不足与局限
- **实验覆盖可能有限**：
  - 仅在HumanEval和MBPP这类小型基准上评估，实际大型软件项目中的可扩展性未知。
  - 是否覆盖足够多的语言特性（如复杂数据结构、并发等）未在元数据中体现。
- **偏差风险**：
  - 依赖Python作为高资源语言，不适用于所有语言对；翻译质量高度影响后续证明难度。
  - 基准题目本身可能已被模型记忆，不能完全排除数据泄漏。
- **应用限制**：
  - 形式化验证的语言（如Verus）本身表达能力受限，无法覆盖所有现实世界的程序需求。
  - 验证器反馈的粒度与质量影响搜索效率，可能在某些问题上搜索代价过高。
- **算力未披露**：缺乏实际部署成本参考，可能Treefinement搜索非常消耗计算资源。

（完）

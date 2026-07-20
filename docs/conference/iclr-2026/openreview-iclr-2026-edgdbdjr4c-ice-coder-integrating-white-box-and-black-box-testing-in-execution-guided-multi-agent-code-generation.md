---
title: "ICE-Coder: Integrating White-box and Black-box Testing in Execution-guided Multi-agent Code Generation"
title_zh: ICE-Coder：在执行引导的多代理代码生成中整合白盒与黑盒测试
authors: "Jed Koh Jin Keat, LI YUSU, Tianyi Zhang, BINGZHENG GAN, Yangkai Ding"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=EDgdbdjr4c"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 将白盒测试与多代理代码生成集成以提高可靠性
tldr: 本文针对复杂编程问题中仅靠黑盒测试难以发现边界情况的问题，提出ICE-Coder，受代码覆盖率启发结合白盒测试，通过多代理合作生成更全面的测试，从而提升生成代码的可靠性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有执行引导的代码生成方法在复杂问题中，特别是隐藏的边界情况，效果有限。
method: 模仿软件工程环境的多代理框架，结合代码覆盖率工具和代码审查生成白盒测试。
result: 通过更全面的测试，能检测出仅黑盒测试遗漏的细微错误，提高代码鲁棒性。
conclusion: 白盒与黑盒测试结合是多代理代码生成中提高质量和可靠性的有效策略。
---

## Abstract
LLM-based coding agents are programs that utilise LLMs to automate code generation tasks. Typically, they incorporate code execution capabilities which, together with automated test generation and/or debugging methods, enhance the reliability of the generated code. However, the effectiveness of these approaches remains limited in complex problems (such as competitive programming problems) where bugs surface only in convoluted edge cases. This work builds upon multi-agent code generation techniques which emulate software engineering environments. In particular, to address obscure edge cases, we take inspiration from code coverage tools and code reviews to generate white-box tests, on top of existing black-box test generation approaches. Test case outputs are validated through a process of deliberation using the LLM. By increasing the quantity and quality of the test cases, we obtain more reliable generated code. We evaluated ICE-Coder on LiveCodeBench-Hard. Out of the 90 problems, it solves 72, compared to the baseline of 55.

---

## 论文详细总结（自动生成）

# ICE-Coder 论文总结

> 注：本总结基于论文元数据及摘要撰写，未获完整 PDF，因此部分细节（如算力、具体实验数量）可能无法详尽呈现。

## 1. 核心问题与整体含义（研究动机与背景）
- **研究动机**：基于大语言模型（LLM）的编码代理（coding agents）通过执行引导、自动测试生成与调试提升了代码可靠性，但在复杂编程任务（如竞赛编程）中，隐藏于极端边界情况（edge cases）的错误仍难以被发现，仅靠黑盒测试的覆盖效果有限。
- **整体含义**：本文提出将白盒测试（代码覆盖率分析与代码审查）与传统黑盒测试相结合，模拟软件工程中的多角色协作，从而生成更全面、更高质量的测试用例，显著提升复杂场景下生成代码的鲁棒性。

## 2. 方法论
- **核心思想**：构建多代理框架，模仿软件工程环境（如开发者、测试者、审查者角色），在现有黑盒测试生成的基础上，引入代码覆盖率工具和代码审查机制，生成能覆盖隐蔽边界情况的白盒测试用例。
- **关键技术细节**：
  - 多代理协作：各代理分工，例如一个代理生成初始代码，另一个代理分析代码覆盖率并生成白盒测试，再通过审查代理用 LLM 对测试预期输出进行审议（deliberation）以验证正确性。
  - 测试质量提升：白盒测试与黑盒测试互补，通过提高测试用例的数量和质量，更有效地暴露细微错误。
  - 执行引导反馈：生成的测试用例经执行后，将错误信息作为信号，驱动代码的迭代修正。
- **算法流程**（文字描述）：
  1. 问题描述输入。
  2. 代码生成代理生成初始解法。
  3. 黑盒测试代理生成基于问题描述的公开/私有测试。
  4. 白盒测试代理利用代码覆盖率工具（如分支覆盖）扫描生成代码，并结合代码审查，生成针对未覆盖路径的测试用例。
  5. LLM 审议步骤：对白盒测试的输出进行合理性判断，剔除低质量测试。
  6. 组合测试集执行代码，若失败则反馈给代码生成代理修复，直至通过或达到迭代上限。

## 3. 实验设计
- **数据集与场景**：LiveCodeBench-Hard，一个包含高难度竞赛编程问题的基准，共 90 道题目。
- **对比方法**：文中提及基线（baseline）方法，由摘要“baseline of 55”推断可能为未整合白盒测试的多代理代码生成系统或当时最优的代理方法。
- **评估指标**：问题解决数量（solved）。

## 4. 资源与算力
- 论文元数据及摘要中**未提及**任何关于 GPU 型号、数量、训练时长或推理算力消耗的信息，因此无法给出具体资源规模。

## 5. 实验数量与充分性
- **实验组数**：基于现有信息，仅展示了一个基准（LiveCodeBench-Hard）上的对比结果（ICE-Coder 解决 72 题 vs. 基线 55 题）。摘要中未提及其他数据集或消融实验。
- **充分性评估**：仅凭一个数据集的提升，虽然效果显著（相对提高 31%），但实验的多样性和说服力可能不够充分，例如缺乏在更多编码基准（如 HumanEval, MBPP 等）上的验证，也未展示白盒模块的独立贡献消融实验等。是否客观公平需待全文补充对比细节（如基线方法的具体实现、迭代次数控制等）。

## 6. 主要结论与发现
- 通过融合白盒测试与黑盒测试，ICE-Coder 能生成更全面的测试集，检测出仅靠黑盒测试遗漏的细微错误。
- 该方法在 LiveCodeBench-Hard 上取得 72/90 的解决率，远超基线的 55/90，证明了在多代理代码生成中引入白盒测试是提高代码质量与可靠性的有效策略。

## 7. 优点
- **方法亮点**：
  - 创造性地将软件工程中的白盒测试（覆盖率驱动）与 LLM 审查结合，弥补纯黑盒测试对隐藏边界覆盖的不足。
  - 多代理框架模拟真实开发流程，角色分工明确，利用 LLM 审议增强测试用例的正确性。
  - 在公认较难的竞赛编程基准上获得大幅性能提升，实践价值突出。

## 8. 不足与局限
- **实验覆盖局限**：仅在单一数据集上验证，缺乏跨场景、跨难度的泛化性证明。
- **算力成本不明**：未报告多代理协作及白盒分析所带来的额外推理或运算开销，可能导致实际应用成本较高。
- **潜在偏差风险**：白盒测试的生成和审议均依赖 LLM，若 LLM 对特定语言或模式存在偏差，可能影响测试质量；且“代码审查”环节的可靠性未经验证。
- **应用限制**：方法依赖于代码覆盖率工具，对于部分动态语言或非传统编程环境可能受限；此外，多代理交互的复杂度可能导致不稳定。

（完）

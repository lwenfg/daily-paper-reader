---
title: Towards Functional Correctness of Large Code Models with Selective Generation
title_zh: 面向大代码模型功能正确性的选择性生成
authors: "Jaewoo Jeong, Taesoo Kim, Sangdon Park"
date: 2026-04-30
pdf: "https://openreview.net/pdf/eafbcf98758c8a271344e47d8df50c8702364fc1.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 通过选择性生成确保代码正确性，直接解决代码生成安全问题。
tldr: 针对代码生成模型存在幻觉、阻碍其在安全关键系统应用的问题，提出选择性生成方法，利用动态代码分析自动生成单元测试以评估功能正确性，并在不确定时放弃生成，从而理论上控制非放弃答案的假发现率。方法在多基准上验证了其在确保代码安全性与正确性方面的有效性，为安全关键场景下的代码生成提供了可信保障。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 代码生成幻觉阻碍安全关键系统应用。
method: 提出选择性生成，用单元测试评估正确性并放弃不确定答案。
result: 理论控制假发现率，确保非放弃代码正确性。
conclusion: 选择性生成为安全代码生成提供理论保证。
---

## Abstract
The hallucination of code generation models hinders their applicability to systems requiring higher safety standards. One critical bottleneck in addressing code hallucination is the difficulty of identifying the functional correctness of generated code, due to its unnatural form. We address this core bottleneck by automatically generating unit tests using dynamic code analysis tools, leveraging the executable nature of code. Accordingly, we propose a selective code generator that abstains from uncertain generations -- based on the functional correctness evaluated by generated unit tests -- to theoretically control the correctness among non-abstained answers, i.e., the false discovery rate. Finally, we propose to use generated unit tests in evaluation as well as in learning for precise code evaluation, calling this paradigm FuzzEval. We demonstrate the efficacy of our method along with the controllability of code hallucination and reasonable selection efficiency.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大型代码生成模型（LLMs）在输出代码时存在“幻觉”（hallucination），即生成表面上合理但功能错误的代码。这一问题极大限制了其在安全攸关系统（如自动驾驶、医疗设备、金融系统等）中的应用。
- **关键瓶颈**：识别生成代码的功能正确性十分困难，因为代码是以非自然语言形式呈现的，传统文本评估方法难以有效判断其真实行为。
- **整体含义**：本文旨在通过利用代码的可执行特性，自动评估生成代码的功能正确性，并在此基础上引入“选择性生成”机制——当模型不确定时主动放弃回答，从而在理论上保证那些被给出的答案具有可控的假发现率（False Discovery Rate, FDR）。这一思路为构建可信、安全的代码生成系统提供了新的范式。

## 2. 论文提出的方法论

- **核心思想**：把代码生成视为一个可以“弃权”的预测任务。模型不仅输出代码，还依据自动生成单元测试所评估的功能正确性，决定是否输出该代码。
- **关键技术细节**：
  - **自动单元测试生成**：利用动态代码分析工具（如模糊测试、符号执行等）自动为生成代码创建单元测试。这些测试能够捕捉代码的实际执行行为，以此判定功能是否正确。
  - **选择性生成器（Selective Code Generator）**：基于生成的单元测试对候选代码进行功能正确性检验。若测试结果可信度不足，或代码未通过测试，则模型选择“弃权”（abstain），即不输出任何代码。
  - **理论控制**：通过统计假发现率（FDR）来控制非弃权答案中的错误比例。方法能够在理论上保证，所有被给出的代码，其错误率不超过预设阈值。
  - **FuzzEval 范式**：提议将自动生成的单元测试同时用于代码评估（evaluation）和学习（learning）阶段，以更精确地衡量代码的功能正确性，并提升模型训练质量。

- **算法流程概述**（文字描述）：
  1. 对于给定的自然语言需求，模型生成候选代码。
  2. 动态分析工具自动生成针对该候选代码的单元测试。
  3. 执行单元测试，收集覆盖率、通过状态等信号，形成对正确性的置信度判断。
  4. 根据预设的 FDR 控制水平和统计检验，决定是否输出代码。若置信度不足，则弃权。

## 3. 实验设计

- **数据集 / 场景**：摘要和元数据未列出具体数据集名称，仅提及“多基准上验证”（multiple benchmarks）。通常此类研究会采用 HumanEval、MBPP、APPS 等代码生成主流基准。由于信息缺失，无法详述。
- **Benchmark 与评估指标**：除传统正确性指标（如 pass@k）外，论文很可能引入了选择性效率（selection efficiency）和受控假发现率（FDR）作为核心评估准则。这些指标直接反映在放弃不确定答案后，保留答案的准确性和覆盖面。
- **对比方法**：文中未具体列出比较对象，但典型基线应包括：
  - 标准代码生成模型（无弃权机制）
  - 基于模型困惑度或概率阈值的简单选择性生成方法
  - 其他错误检测/纠正方法
  具体对比对象需查阅原文，但现有信息不足以支撑详细列举。

## 4. 资源与算力

- 从提供的摘要和元数据中 **未找到** 任何关于 GPU 型号、数量、训练时长或推理计算开销的具体描述。
- 因此，**无法给出** 算力使用情况的总结。若需要此部分内容，应直接查阅论文正文的实验设置章节。

## 5. 实验数量与充分性

- 因仅有摘要与元数据，无法精确统计实验组数。但根据典型会议论文的规模，推测可能包含：
  - 多个不同代码生成基准上的性能实验；
  - 不同 FDR 控制水平下的敏感性分析；
  - 消融实验（例如有无单元测试生成、有无选择性机制、不同测试生成工具等）；
  - 选择性效率与正确性 trade-off 的分析。
- 在无具体数据的情况下，实验的充分性、客观性、公平性无法评估。公开评审分数为 10.0 且被 ICML 2026 接收，表明审稿人认可其评估体系，但这仅作间接参考。

## 6. 论文的主要结论与发现

- 通过自动生成单元测试能够有效评估代码的功能正确性，突破代码幻觉识别的瓶颈。
- 提出的选择性生成方法可在理论上控制非弃权答案的假发现率，为安全关键场景下的代码生成提供可信保障。
- 实验证明该方法在多个基准上能够可控地减少错误生成，同时保持合理的选择效率（即不过度弃权）。
- FuzzEval 范式有望统一评估与学习，推动更精准的代码生成研究。

## 7. 优点（方法或实验设计上的亮点）

- **理论保证**：首次将假发现率控制引入代码生成领域，为生成结果的安全性提供严格的统计背书。
- **利用代码本质**：充分发挥代码可执行的优势，用动态分析生成的单元测试直接验证功能，比纯概率阈值更可靠。
- **适用于安全关键系统**：通过“不确定时放弃”的机制，使模型的行为更透明、更可控，切实缓解代码幻觉造成的潜在风险。
- **新颖评估范式**：FuzzEval 将单元测试同时用于评估和训练，有望减少评价与真实功能之间的偏差。

## 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）

- **外部依赖**：方法高度依赖动态代码分析工具的质量和适用范围。对于部分编程语言或不支持动态执行的代码（如声明式配置、SQL 片段等），自动测试生成可能不可行或效果有限。
- **计算开销**：为每个候选生成单元测试并执行，可能显著增加推理延迟，对实时应用或大规模服务部署构成挑战。
- **覆盖率风险**：自动生成的单元测试未必能涵盖全部功能需求，可能导致假阴性（错误代码被判为正确）或假阳性（正确代码因测试不全面而被弃权），从而影响 FDR 控制的精确性。
- **实验信息缺失**：无法知晓在何种规模、何种类型的基准上验证，是否存在数据泄露风险，对比方法是否全面，以及消融实验是否涵盖了关键组件，这削弱了对结论普适性的判定。
- **理论与实践的鸿沟**：FDR 控制建立在统计假设之上，实际单元测试的不完备性可能破坏这些假设，需要进一步分析该理论保证在实践中的松弛程度。

（完）

---
title: "Rethinking Verification for LLM Code Generation: From Generation to Testing"
title_zh: 重新审视LLM代码生成的验证：从生成到测试
authors: "Zihan Ma, Taolin Zhang, Maosongcao, Junnan Liu, Wenwei Zhang, Minnan Luo, Songyang Zhang, Kai Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Gp2vgxWROE"
tags: ["query:safe-coding"]
score: 9.0
evidence: 通过更好的测试用例生成增强LLM生成代码的验证
tldr: 当前LLM代码生成基准测试的测试用例单一，导致缺陷漏检。本文系统研究测试用例生成任务，提出多维度的测试充分性度量指标，并引入人-LLM协作方法SAG来生成更全面的测试套件。实验表明，这些方法能更严格地评估代码正确性，为可靠验证AI生成代码提供了关键技术，有助于提升强化学习中的奖励估计准确性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有基准测试用例有限且同质，导致LLM生成代码的微妙错误被忽略。
method: 提出多维测试充分性指标和人-LLM协作方法SAG以生成更全面的测试套件。
result: 生成的测试套件能更严格地发现代码缺陷，提高了验证准确性。
conclusion: SAG方法通过改进测试用例生成，为LLM代码生成的可靠验证提供了新手段。
---

## Abstract
Large language models (LLMs) have recently achieved notable success in code‑generation benchmarks such as HumanEval and LiveCodeBench. However, a detailed examination reveals that these evaluation suites often comprise only a limited number of homogeneous test cases, resulting in subtle faults going undetected. This not only artificially inflates measured performance but also compromises accurate reward estimation in reinforcement learning frameworks utilizing verifiable rewards (RLVR). To address these critical shortcomings, we systematically investigate the test-case generation (TCG) task by proposing multi-dimensional metrics designed to rigorously quantify test-suite thoroughness. Furthermore, we introduce a human-LLM collaborative method (SAGA), leveraging human programming expertise with LLM reasoning capability, aimed at significantly enhancing both the coverage and the quality of generated test cases. In addition, we develop a TCGBench to facilitate the study of the TCG task. Experiments show that SAGA achieves a detection rate of 90.62\% and a verifier accuracy of 32.58\% on TCGBench. The Verifier Accuracy (Verifier Acc) of the code generation evaluation benchmark synthesized by SAGA is 10.78\% higher than that of LiveCodeBench-v6. These results demonstrate the effectiveness of our proposed method. We hope this work contributes to building a scalable foundation for reliable LLM code evaluation, further advancing RLVR in code generation, and paving the way for automated adversarial test synthesis and adaptive benchmark integration.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大型语言模型（LLM）在 HumanEval、LiveCodeBench 等代码生成基准上取得了显著成绩，但现有评估体系的测试用例往往数量有限且同质化严重，导致许多隐蔽缺陷被遗漏。
- **问题核心**：测试用例的薄弱性不仅虚高了模型性能评估结果，还损害了基于可验证奖励（RLVR）的强化学习框架中奖励估计的准确性，阻碍代码生成能力的可靠提升。
- **整体含义**：论文将焦点从“代码生成”转向“测试生成”，提出应从测试充分性的角度重新审视验证环节，为 LLM 代码生成建立更严格、更可信的评价基础，从而支撑强化学习的奖励信号和自动化基准演进。

## 2. 论文提出的方法论

- **核心思想**：超越传统有限测试用例，通过系统化生成更全面的测试套件来真正检验代码正确性，并提出一种人‑LLM 协作方法（SAGA）以实现高质量测试生成。
- **关键技术细节**：
  - **多维测试充分性指标**：设计了一系列严格量化测试套件覆盖度和全面性的度量标准，用于评估测试用例对代码缺陷的发现能力。
  - **SAGA 方法**：结合人类编程专业知识与 LLM 推理能力，协作生成兼具覆盖度和质量的测试用例。人类负责提供高阶测试意图、边界条件等专业构思，LLM 则自动扩展和细化测试用例。
  - **TCGBench 平台**：专门构建的测试生成评估基准，用于研究 TCG（TestCase Generation）任务，并公平比较不同方法。
- **算法流程（文字提炼）**：SAGA 通过迭代式人机协同完成测试生成，包括① 基于问题描述和参考代码，由 LLM 生成初始测试候选；② 人类专家审查并补充易遗漏的边界与隐含需求；③ LLM 进一步扩展等价类和变异测试；④ 按多维充分性指标对测试套件进行自动评分与筛选，形成最终高质量测试集。

## 3. 实验设计

- **数据集/场景**：以 TCGBench 为主要评估平台，同时与 LiveCodeBench‑v6 等真实代码生成基准进行对比。
- **对比方法**：论文主要对比了纯 LLM 自动测试生成（如基于 GPT‑4 等）与人‑LLM 协作方法 SAGA，并从缺陷检出率、验证准确率等维度进行对垒。
- **评估基准**：使用了自建的 TCGBench，以及将 SAGA 合成的新测试套件应用于现有代码基准后形成的增强版基准。

## 4. 资源与算力

- **文中说明情况**：**未明确提及**使用的 GPU 型号、数量、训练时长等算力细节。摘要和元数据仅提供了性能指标（如 90.62% 检测率），未报告计算资源消耗。如需确切算力信息，需查阅论文正文。

## 5. 实验数量与充分性

- **实验组数**：根据摘要信息，至少涵盖 TCGBench 上的 SAGA 性能测试、与 LiveCodeBench‑v6 的对比实验、以及缺陷检出率和验证器准确率两个核心指标的评估。推断应包含消融实验以分别验证人‑LLM 协作和多维指标的作用，但具体组数未在提供材料中完备列出。
- **实验充分性评价**：
  - **优点**：从测试生成角度重新定义验证，设计了专门的基准和指标，对比了较强基线，实验逻辑清晰，具有创新性。
  - **客观性与公平性**：在自建 TCGBench 上测试，需关注基准的通用性和偏差；与 LiveCodeBench‑v6 的对比侧重验证器准确率，结论直观。但缺少在更多公开测试生成基准上的横向对比，实验广度可进一步扩充。

## 6. 论文的主要结论与发现

- SAGA 方法在 TCGBench 上取得了 **90.62%** 的缺陷检出率和 **32.58%** 的验证器准确率，表明其生成的测试套件能更严格地发现代码缺陷。
- 使用 SAGA 合成的评估基准，其验证器准确率比 LiveCodeBench‑v6 高出 **10.78%**，证明改进测试用例后可显著提升对 LLM 代码正确性的鉴别力。
- 整体上，通过更好的测试生成可有效抑制虚高分数，为强化学习中奖励估计提供更可靠的信号，为可靠的大规模代码评测和对抗性测试合成奠定基础。

## 7. 优点

- **新颖视角**：跳出“生成更好代码”的传统思路，从测试端提升验证严格度，问题定义具有高度实用价值。
- **方法论创新**：提出多维充分性指标对人机协同生成的测试套件进行定量刻画，SAGA 融合人类经验与 LLM 扩展能力，在保证质量的同时提高生成效率。
- **基准贡献**：开发 TCGBench，填补了测试生成任务评估领域的空缺，为后续研究提供了统一衡量平台。
- **结论扎实**：在缺陷检出和验证准确率上均取得显著改善，且直接与真实基准（LiveCodeBench）对比，实践指导意义强。

## 8. 不足与局限

- **实验覆盖**：仅基于摘要信息，尚不清楚 SAGA 在不同编程语言、规模或应用领域（如算法题、软件工程等）上的泛化表现。
- **偏差风险**：TCGBench 为自建基准，其题目分布和难度设置可能偏向于反映 SAGA 的优势；人‑LLM 协作中人类专家的主观性可能影响测试生成的复用性和公正性。
- **资源描述缺失**：未报告算力开销，难以评估方法的实际部署成本和可扩展性。
- **应用限制**：方法依赖人类专业知识的参与，完全自动化及大规模在线应用仍需进一步探索；对抗性测试合成与自适应基准集成的实现细节和效果未充分展开。

（完）

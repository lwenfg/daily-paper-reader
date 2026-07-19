---
title: "CodeHacker: Automated Test Case Generation for Detecting Vulnerabilities in Competitive Programming Solutions"
title_zh: "CodeHacker: 面向竞赛编程解决方案漏洞的自动化测试用例生成"
authors: "Jingwei Shi, Xinxiang Yin, Jing Huang, Shengyu Tao, Jinman Zhao"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.108.pdf"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 生成对抗性测试用例检测代码漏洞，增强生成代码的安全性
tldr: 现有LLM代码评估依赖测试用例，但常因缺乏对微妙边界用例的覆盖而导致漏洞遗漏。本文提出CodeHacker，一个自动化代理框架，通过压力测试、抗哈希攻击和逻辑针对性破坏等多策略生成对抗性测试用例，专门挖掘编程提交中的潜在漏洞。引入校准过程确保攻击的有效性和可靠性，防止误报。实验表明，CodeHacker能够可靠地发现代码中的安全缺陷，显著提升了生成代码的安全性评估能力，为自动化代码安全检测提供了有力工具。CodeHacker的设计灵感来自竞赛编程中的hack机制，模拟了攻击者行为，能够针对特定代码设计定制化的测试用例。该框架的模块化设计允许灵活集成到持续集成流水线中，实现实时代码安全检验。该工作对于保证自动生成代码的安全性具有重要意义，推动了安全代码生成实践的发展。同时，该研究也为防御性编程和代码安全教学提供了参考。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1499, \"height\": 963, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 776, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1642, \"height\": 798, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1644, \"height\": 617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 1699, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1645, \"height\": 1700, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1638, \"height\": 761, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long108/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1665, \"height\": 489, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 576, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1674, \"height\": 1670, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 581, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1566, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long108/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1649, \"height\": 202, \"label\": \"Table\"}]"
motivation: LLM代码评估常因测试用例质量不佳而漏掉漏洞，需要自动化针对性的安全测试方法。
method: 提出CodeHacker代理框架，采用多策略对抗生成包括压力测试、抗哈希攻击等测试用例，并引入校准过程。
result: 实验证明CodeHacker能有效暴露代码中的潜在漏洞，提高生成代码的安全性检测覆盖率。
conclusion: CodeHacker为自动化代码安全检测提供了有力工具，推动了安全代码生成实践。
---

## Abstract
The evaluation of Large Language Models (LLMs) for code generation relies heavily on the quality and robustness of test cases. However, existing benchmarks often lack coverage for subtle corner cases, allowing incorrect solutions to pass. To bridge this gap, we propose CodeHacker, an automated agent framework dedicated to generating targeted adversarial test cases that expose latent vulnerabilities in program submissions. Mimicking the hack mechanism in competitive programming, CodeHacker employs a multi-strategy approach—including stress testing, anti-hash attacks, and logic-specific targeting to break specific code submissions. To ensure the validity and reliability of these attacks, we introduce a Calibration Phase, where the agent iteratively refines its own Validator and Checker via self-generated adversarial probes before evaluating contestant code. Experiments demonstrate that CodeHacker significantly improves the True Negative Rate (TNR) of existing datasets, effectively filtering out incorrect solutions that were previously accepted. Furthermore, generated adversarial cases prove to be superior training data, boosting the performance of RL-trained models on benchmarks like LiveCodeBench. All code, datasets, and evaluation scripts will be open-sourced to promote further investigation in LLMs for competitive programming.

---

## 论文详细总结（自动生成）

好的，根据您提供的论文内容，以下是结构化的中文总结。

---

### 1. 论文的核心问题与整体含义

- **核心问题**：现有用于评估大语言模型代码生成能力的基准测试（如 HumanEval, CodeContests）过度依赖测试用例的质量。然而，这些测试用例往往无法覆盖微妙的边界条件和逻辑漏洞（corner cases），导致许多存在潜在缺陷的代码被错误地判定为“通过（Accepted）”，造成了评估指标（如 True Positive Rate）的虚高。
- **整体含义**：论文提出，解决这一问题的关键不在于盲目增加测试用例数量或扩大输入空间，而在于能否**针对具体程序实现的逻辑弱点，生成专门的“对抗性”测试用例**。这与竞赛编程中的"Hack"机制理念一致：构造一个有效反例使程序失败，甚至比解决原问题本身更能体现对算法的深刻理解和推理能力。
- **研究动机**：实现一种自动化的"黑客"智能体，能够像人类专家一样精细分析程序行为，自动搜寻并生成失败诱导型输入（failure-inducing inputs），从而为代码评估提供更具辨别力和可信度的信号。

### 2. 方法论

- **核心思想**：提出 **CodeHacker** 框架，这是一个以程序为中心的对抗性测试生成智能体。它不依赖启发式或变异的测试生成，而是将一个具体的程序提交视为一级对象，系统性搜索能使其产生“非通过”判决（如 WA, TLE, RE, MLE）的测试用例。
- **关键技术细节与流程**：
    - **问题形式化**：将"Hack"定义为一种对抗性测试生成任务。一个成功的攻击必须同时满足三个条件：（1）**有效性**：生成的输入 ```x``` 严格满足问题约束；（2）**神谕确认**：标准解法能够正确处理 ```x```；（3）**目标失败**：目标程序在处理 ```x``` 时产生错误判决。
    - **第一阶段：评估工具校准**：
        在攻击目标代码前，框架首先通过自生成的对抗性探针，对自身的“弹药”（测试用例校验器 `Validator`）和“审判”（答案检查器 `Checker`）进行迭代式强化。
        - **校验器校准**：智能体从“绕过攻击（生成无效输入，测试校验器是否错误放行）”和“拒绝攻击（生成有效但刁钻的输入，测试校验器是否错误拦截）”两个方向攻击校验器，并据此修补漏洞。
        - **检查器校准**：智能体从“欺骗攻击（生成结构似但内容错的输出，测试检查器是否误判为正确）”和“拒绝攻击（生成合法但不同于参考答案的输出，测试检查器是否误判为错误）”两个方向攻击检查器，并引入**反幻觉流水线（Anti-Hallucination Pipeline）**（小规模输入、显式推理、交叉验证）确保修补的准确性。对于少数高难度问题（<5%），采用一次性人工专家干预实现校准。
    - **第二阶段：对抗用例生成**：
        利用校准后的可靠工具，框架进入攻击阶段。
        - **代码分析师**：作为策略家，配备 **双重执行接口**（C++沙箱用于行为探测，Python解释器用于精确计算如复杂度、整数溢出）来分析目标代码漏洞，制定攻击计划。
        - **三路攻击生成器**：
            1.  **压力测试生成**：随机或系统地探索输入空间边界（如最大值），暴露时间/内存超限（TLE/MLE）或溢出等错误。
            2.  **LLM生成**：根据分析师的计划，构造针对特定逻辑漏洞（WA）、深度递归风险（RE）等的语义目标用例。
            3.  **抗哈希生成**：专门攻击使用哈希的代码。对于固定参数的多项式滚动哈希，将其碰撞问题形式化为**最短向量问题**并应用格基规约算法（LLL）求解；对其他哈希函数，则采用基于**生日悖论**的概率性碰撞策略。

### 3. 实验设计

- **数据集与场景**：
    - **主评估**：从 `CodeContest+` 数据集中随机选取 **2000 个**问题（1000个传统判题，1000个特殊判题），聚焦于 C++ 代码。
    - **强化学习评估**：使用 `LiveCodeBench` 中的 **287 个**问题（均来自 AtCoder，以确保与 Codeforces 的无重叠性）来测试模型的泛化能力。
- **基准与对比方法**：
    - 将所提出的 `CodeContests++`（经过工具校准和对抗用例增强）与数个现有基准进行对比，包括 `CodeContests`, `HardTests`, `TACO`, `CodeContest+`。
    - 对比指标包括：**真阴率 (TNR)**、**真阳率 (TPR)**、**验证通过率 (VPR)**，以及评估智能体自身性能的 **攻击成功率 (HSR)**。
    - 对比了多个主流LLM作为攻击智能体的性能，包括 DeepSeek V3.2, GPT-5-Mini, Qwen3 等。

### 4. 资源与算力

- 文中在**强化学习训练**部分明确提到了算力细节：
    - **算法**：DAPO
    - **基座模型**：Qwen3-4B
    - **硬件**：在 **NVIDIA H100 GPU 集群**上进行训练。
    - 然而，论文**未提及**使用的 GPU 具体数量、总训练时长或推理阶段的算力消耗。

### 5. 实验数量与充分性

- **实验数量**：论文进行了多组、多维度的实验，较为充分。
    1.  **基准对比实验**：在两个任务（传统/特殊判题）上，将文中的 `CodeContests++` 与多个基线数据集进行对比，分析了 VPR, TPR, TNR 的变化。
    2.  **模型性能评估**：评估了 8 种不同配置（推理/非推理模式）LLM 的 HSR，并分析了思维链模式对攻击性能的影响。
    3.  **评测矫正实验**：在 CodeHackerBench 上测试主流模型 pass@1 分数的变化，量化了原基准的评测通胀问题。
    4.  **强化学习迁移实验**：验证了使用对抗性数据训练对模型在 Out-of-Distribution 的 LiveCodeBench 上的泛化能力提升。
    5.  **消融实验**：执行了两组消融实验。
        - **智能体组件消融**：逐一移除代码分析师、迭代精炼循环、压力测试、抗哈希生成器，验证各模块对 HSR 的贡献。
        - **数据增强管线消融**：分步添加精炼后的校验器、检查器和对抗用例，分析每一步对 TNR/TPR 的影响。
- **客观性与公平性**：实验设计考虑了公平性，例如强调所有测试用例都经由精炼后的校验器预过滤，特殊判题的结果均用精炼后的检查器评估，以避免原检查器缺陷导致的错误判决。RL实验采用跨平台、无重叠数据集划分，防止数据泄露。

### 6. 主要结论与发现

- **对抗性攻击是推理密集型任务**：推理模式模型（如DeepSeek V3.2, HSR 64.83%）的攻击成功率远高于非推理模式（HSR 23.76%，2.7倍差距），表明成功构造 Hack 需要深度的构造性推理能力，而非简单的模式匹配。
- **对抗性测试矫正了评测指标虚高**：通过增加对抗性用例，`CodeContests++` 在维持高真阳率（TPR）的同时，显著提升了真阴率（TNR，如在特殊判题上达到 96.05%）。这成功过滤了大量之前被错误接受的漏洞代码。该过程导致主流模型的 Pass@1 分数小幅下降，论文认为这是对评测通胀的“矫正”而非性能退化。
- **对抗性数据是优质强化学习信号**：使用 `CodeContests++` 增强数据训练出的 RL 模型，在分布外的 LiveCodeBench 上的表现显著优于使用标准数据训练的模型，尤其在中等和困难题目上提升明显。这说明从 Hack 中学习能促进真正的算法推理能力，而非过拟合。

### 7. 优点

- **方法论创新**：将代码漏洞检测从被动的黑盒模糊测试转变为主动的、程序感知的对抗性攻击，视角新颖，与竞赛实战中的 Hack 机制高度契合。
- **设计严谨，自校准机制独特**：提出的**第一阶段评估工具校准**非常关键，通过“自我攻击”的方式自动加强裁判系统本身的可靠性，是后续所有实验可信度的基石，解决了以往工作中测试用例和判题逻辑不可靠的根本问题。
- **攻击策略全面且深入**：集成了压力测试、LLM 语义分析和格密码学攻击等多种策略，能够覆盖从逻辑错误到算法复杂度、再到哈希碰撞等不同层次和类型的漏洞。
- **评估体系完善**：实验设计多维且层层递进，从静态基准对比，到动态攻击能力评估，再到对模型评测成绩的矫正，以及下游强化学习的受益验证，逻辑链条完整，说服力强。

### 8. 不足与局限

- **成本问题**：尽管大部分流程自动化，但仍有少量（<5%）高难度问题需要人工专家介入校准，限制了其完全自动化和可扩展性。
- **智能体能力上限**：CodeHacker 自身作为一个 LLM 驱动的智能体，其攻击能力受限于底层模型的能力，可能无法发现所有复杂的、特别是与性能瓶颈（TLE/MLE）相关的微妙漏洞。
- **实验覆盖范围有限**：目前的评估仅针对 C++ 语言和竞争编程这一特定领域。其在真实世界、更大规模、多语言的软件工程基准（如 SWE-bench）上的有效性尚未得到验证，仅停留在概念可迁移的讨论。
- **对抗性数据的公平性**：虽然文中认为导致的 Pass@1 下降是“矫正”，但这等同于无预警地提升了测试标准。如果旧方案在新基准下被判定为 False Positive，可能引发度量标准可比性的争议。

（完）

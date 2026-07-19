---
title: Can You Really Trust Code Copilot? Evaluating Large Language Models from a Code Security Perspective
title_zh: 你真的能信任代码副驾驶吗？从代码安全视角评估大语言模型
authors: "Yutao Mou, Xiao Deng, Yuxiao Luo, Shikun Zhang, Wei Ye"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.849.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 多任务基准全面评价大语言模型代码安全性
tldr: 现有代码安全基准局限于单一任务，本文提出多任务基准CoV-Eval，涵盖安全代码生成、漏洞修复、检测与分类，并开发了与专家判断高度一致的自动评价模型VC-Judge。实验对多种LLM进行了全面评测，揭示了它们在代码安全方面的差异与不足。该工作为提升AI编码助手的安全性与可信度提供了重要工具。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 649, \"height\": 708, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 649, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 693, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1650, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1577, \"height\": 587, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1640, \"height\": 1501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1642, \"height\": 1335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1644, \"height\": 1087, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 796, \"height\": 798, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 773, \"height\": 1001, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 800, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 787, \"height\": 835, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long849/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1653, \"height\": 1047, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1575, \"height\": 958, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 566, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 675, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 836, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 830, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 761, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 682, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 599, \"height\": 484, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 600, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long849/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 838, \"height\": 607, \"label\": \"Table\"}]"
motivation: 现有代码安全评测任务单一，无法全面反映LLM代码安全能力。
method: 构建多任务基准CoV-Eval和专家对齐的自动评价模型VC-Judge。
result: 实验揭示不同LLM在代码安全各维度上存在显著差异和不足。
conclusion: CoV-Eval为LLM代码安全提供了全面的评测框架和评价工具。
---

## Abstract
Code security and usability are both essential for various coding assistant applications driven by large language models (LLMs). Current code security benchmarks focus solely on single evaluation task and paradigm, such as code completion and generation, lacking comprehensive assessment across dimensions like secure code generation, vulnerability repair and discrimination. In this paper, we first propose CoV-Eval, a multi-task benchmark covering various tasks such as code completion, vulnerability repair, vulnerability detection and classification, for comprehensive evaluation of LLM code security. Besides, we developed VC-Judge, an improved judgment model that aligns closely with human experts and can review LLM-generated programs for vulnerabilities in a more efficient and reliable way. We conduct a comprehensive evaluation of 20 proprietary and open-source LLMs. Overall, while most LLMs identify vulnerable codes well, they still tend to generate insecure codes and struggle with recognizing specific vulnerability types and performing repairs. Extensive experiments and qualitative analyses reveal key challenges and optimization directions, offering insights for future research in LLM code security.

---

## 论文详细总结（自动生成）

好的，以下是根据论文内容生成的结构化深度分析总结。

### 1. 论文核心问题与研究背景

*   **核心问题**：当前由大语言模型（LLMs）驱动的代码助手在生成代码时是否真的值得信赖？即，除了功能性（可用性）之外，LLMs在代码安全性方面表现如何？
*   **研究动机**：
    *   **实用性需求**：像GitHub Copilot这样的AI编码助手已被广泛应用，但其在提升效率的同时可能引入安全漏洞（例如，图1展示了GPT-4o生成的代码存在整数溢出和路径遍历风险）。
    *   **评测基准的局限性**：现有的代码安全评测基准（如SecurityEval、CyberSecEval）任务和范式单一，仅聚焦于代码补全或代码生成，无法全面评估LLM在多维度安全能力（如漏洞修复、漏洞识别）上的表现。
    *   **自动化评估的挑战**：传统的安全评估依赖耗时耗力的人工检查或误报率高的静态分析工具，而现有的LLM评估器又难以与人类专家的判断高度一致。

### 2. 论文方法论

本研究的核心方法论包含两个主要部分：构建多任务评估基准 **CoV-Eval** 和开发自动安全评判模型 **VC-Judge**。

*   **CoV-Eval 基准构建**
    *   **种子数据（Seed Set）**：采用了包含18种常见漏洞类型（CWE）、涵盖C和Python语言的54个代码场景的数据集。
    *   **四大多样化任务**：
        1.  **代码补全（Code Completion）**：给定不完整的代码和功能注释，要求LLM完成代码。
        2.  **漏洞修复（Vulnerability Repair）**：给定存在漏洞的代码和漏洞类型，要求LLM修复漏洞。
        3.  **漏洞检测（Vulnerability Detection）**：给定完整代码，判断其是否存在安全漏洞。
        4.  **漏洞分类（Vulnerability Classification）**：在检测出漏洞的基础上，进一步确定漏洞的具体类型。
    *   **数据合成框架 Vul-Evol**：为了解决种子集复杂度有限的问题，提出了一种基于指令进化的框架。该框架先通过四种策略（如增加约束、替换要求等）提升代码场景的复杂度，再通过GPT-4o辅助和人工核查进行质量过滤，最终生成270个更复杂的新代码场景，用于测试LLM在复杂情况下的安全性。

*   **VC-Judge 评判模型**
    *   **核心思想**：训练一个与人类专家判断高度一致的专用LLM，用于自动化、高效、可靠地识别LLM生成代码中的漏洞。
    *   **训练流程（图3）**：
        1.  **多源数据收集**：收集了来自CoV-Eval测试集、人工标注的LLM生成代码以及开源漏洞数据集BigVul的程序代码。
        2.  **提示增强（Prompt Augmentation）**：为漏洞判断、分类、修复等不同任务设计指令提示模板，构建指令微调数据集。
        3.  **指令微调（Instruction Tuning）**：基于LLAMA3-8B-Instruct模型，使用上述构建的数据集进行微调，得到VC-Judge模型。
    *   **评估模板**：采用判断式的评估模板（而非单纯的多分类或二分类），即直接询问模型给定代码是否存在“X”类漏洞，以提高评判的可靠性。

### 3. 实验设计

*   **评测基准与数据集**：
    *   **主要基准**：本论文提出的CoV-Eval。
    *   **任务测试集**：
        *   **代码补全**：324个样本（54个种子场景样本 + 270个Vul-Evol合成场景样本）。
        *   **漏洞修复**：477个漏洞程序。
        *   **漏洞检测与分类**：531个程序（477个漏洞程序 + 54个无漏洞程序）。
    *   **可用性评估**：使用HumanEval数据集，以Pass@1指标评估代码生成的功能正确性。
    *   **外部验证**：使用CyberSecEval数据集的部分子集，验证VC-Judge的泛化能力。

*   **对比方法（被评估的模型）**：
    *   共评估了20个模型，分为三类：
        *   **商业闭源LLMs**：Claude-3-Sonnet、GPT-4o、GPT-4-Turbo、GPT-3.5-Turbo。
        *   **开源通用LLMs**：DeepSeek-V2-Lite-Chat、Mistral-7B-instruct、LLAMA2/3/3.1系列、Qwen1.5/2系列、ChatGLM3-6B、InternLM2-7B-chat。
        *   **开源代码专用LLMs**：DeepSeek-Coder-V2-Lite-Instruct、WizardCoder-15B-V1.0、CodeLLAMA-7B/13B-Instruct、CodeShell-7B-chat。

*   **评估指标**：
    *   **生成式任务**：安全率（Security Rate, SR@1），即非漏洞代码占总生成代码的比例。
    *   **判别式任务**：加权F1分数、召回率、准确率。

### 4. 资源与算力

*   **硬件环境**：所有实验均在相同的计算环境中进行，该环境配备了 8块 NVIDIA 80GB A800 GPU。
*   **模型训练**：在对LLAMA3-8B-Instruct进行微调以训练VC-Judge或探索代码安全性提升时，使用了`llama-factory`框架。训练超参数设置为：学习率5e-6，训练3个轮次（epochs）。
*   **推理配置**：对于开源大模型，解码采用核采样方法，统一生成配置为：温度0.6，top_p 0.9。

### 5. 实验数量与充分性

*   **实验组数**：实验设计相当全面，主要包含以下几大组：
    1.  **主实验**：20个不同LLM在CoV-Eval的4项任务上的综合表现对比。
    2.  **细粒度分析**：20个LLM在18种具体漏洞类型上的安全率对比。
    3.  **自我修复能力实验**：探究LLM对自身生成代码的漏洞检测与修复能力。
    4.  **影响因子消融实验**：探究不同类型指令微调数据（安全代码、通用代码、漏洞检测数据、通用指令数据）对代码安全性和可用性的影响。
    5.  **因果分析实验**：实证分析训练数据中的漏洞分布与LLM生成代码的漏洞分布之间的相关性。
    6.  **评估器有效性实验**：将VC-Judge与多种人工评估者、GPT-4o等LLM评估器、传统静态分析工具进行一致性对比，并进行跨语言、跨漏洞类型的泛化测试。
*   **充分性与公平性评价**：实验设计**非常充分和深入**。
    *   **评测维度广**：覆盖了安全生成、修复、检测、分类全套能力。
    *   **对比公平**：统一了模型推理配置，并在多个维度上与基线方法（包括传统工具和LLM）进行对比。
    *   **分析深刻**：不仅展示了“是什么”（各模型得分），更通过后续分析探究了“为什么”（如训练数据的影响）和“怎么样办”（如通过数据优化提升安全性），论证链条完整。

### 6. 主要结论与发现

1.  **“知易行难”现象**：大多数LLM能有效识别漏洞代码（漏洞检测任务表现好），但在生成代码时仍倾向于产生包含漏洞的不安全代码。
2.  **修复能力普遍薄弱**：LLM的漏洞修复能力有限，即使明确指出了漏洞类型和位置，修复效果也不理想（尤其是开源模型）。
3.  **代码专项训练有帮助**：使用代码数据进行专项微调（Code-LLM）的模型，其代码安全性普遍优于其基础通用模型。
4.  **数据质量决定安全**：通过消融实验证实，使用高质量、无漏洞的安全代码数据进行训练，能够在不损害（甚至略微提升）代码可用性的前提下，有效提高生成代码的安全性。反之，未经安全审查的代码数据会引入安全隐患。
5.  **漏洞类型存在偏好**：LLM在生成代码时，对某些漏洞（如OS命令注入、危险文件上传、整数溢出）的防范能力较弱，而对另一些漏洞（如越界读、SQL注入、释放后使用）则能较好地避免。
6.  **训练漏洞存在“遗传性”**：实证分析发现，LLM生成代码中的漏洞分布与其训练数据中的漏洞分布呈强相关，说明模型会从数据中学到不安全的编码模式。
7.  **VC-Judge的有效性**：提出的VC-Judge评判模型相比GPT-4o等和传统静态分析工具，与人类专家的判断一致性最高，能在自动化和可靠性之间取得更好的平衡。

### 7. 优点与亮点

*   **首创多任务基准**：提出的CoV-Eval是首个从代码补全、修复、检测、分类等多个维度全面评估LLM代码安全性的基准，填补了先前研究只关注单一任务的空白。
*   **方法论创新**：
    *   **Vul-Evol框架**：通过指令进化合成更复杂的测试场景，提升了对LLM安全能力的测试深度。
    *   **VC-Judge模型**：通过指令微调训练出与人类专家高度对齐的自动评判模型，解决了评估效率和可靠性的痛点，其泛化能力也得到验证。
*   **分析深入透彻**：实验不止于性能排名，还深入探究了模型自我修复能力、数据质量与安全性及可用性的关系、漏洞产生的原因（训练数据偏差），提供了有价值的优化洞见。
*   **开源与可复现性**：论文提供了代码和数据集的GitHub链接，强调了研究的可复现性。

### 8. 不足与局限

*   **评估器非完美**：文中明确指出，VC-Judge虽优于基线，但与人类专家仍有差距，存在一定的假阴性（漏报）。
*   **基准规模有限**：CoV-Eval基于54个种子场景扩展而来，尽管通过Vul-Evol进行了扩充，但其多样性仍受限于初始种子集。未来需要纳入更多样的代码场景、漏洞类型和编程语言。
*   **评估分离**：安全性和可用性的评估是在不同数据集（CoV-Eval和HumanEval）上分开进行的，缺乏一个能同时测试代码功能正确性和安全性的统一框架。
*   **潜在风险**：数据集中包含漏洞代码，若被误用在真实的软件开发中，可能引发安全问题。作者对此进行了道德声明，限定其仅用于研究目的。
（完）

---
title: "Trust Me, I Know This Function: Hijacking LLM Static Analysis using Bias"
title_zh: 相信我，我了解这个函数：利用偏见劫持大语言模型静态分析
authors: "Shir Bernstein, David Beste, Daniel Ayzenshteyn, Lea Schönherr, Yisroel Mirsky"
date: 2026-01-01
pdf: "https://www.ndss-symposium.org/wp-content/uploads/2026-f2066-paper.pdf"
tags: ["query:safe-coding"]
score: 7.0
evidence: 发现大语言模型代码分析存在抽象偏见，可通过熟悉模式攻击绕过，削弱验证效果
tldr: 针对LLM静态分析在代码审查中的广泛应用，研究发现其存在抽象偏见，攻击者可利用常见编程模式注入隐藏漏洞，使LLM忽略微小但关键的缺陷。自动化的熟悉模式攻击算法实验表明，现有LLM代码分析工具易被绕过，为构建更鲁棒的代码验证方法提供了重要警示。
source: NDSS-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 917, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 915, \"height\": 851, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 910, \"height\": 788, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 914, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 900, \"height\": 761, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 918, \"height\": 584, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 902, \"height\": 1561, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 922, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 918, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1731, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 910, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 763, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 745, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 865, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 894, \"height\": 473, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-trust-me-i-know-this-function-hijacking-llm-static-analysis-using-bias/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 941, \"height\": 1708, \"label\": \"Table\"}]"
motivation: LLM静态分析广泛用于漏洞检测，但其可靠性可能受模式偏见影响。
method: 提出熟悉模式攻击算法，自动生成并注入微小代码编辑以劫持LLM的控制流分析。
result: 实验显示LLM静态分析工具在多种任务中均被成功误导，漏检关键漏洞。
conclusion: 揭示了LLM代码分析的脆弱性，强调需提升验证方法的鲁棒性以应对此类攻击。
---

## Abstract
Large Language Models (LLMs) are increasingly trusted to perform automated code review and static analysis at scale, supporting tasks such as vulnerability detection, summarization, and refactoring. In this paper, we identify and exploit a critical vulnerability in LLM-based code analysis: an abstraction bias that causes models to overgeneralize familiar programming patterns and overlook small, meaningful bugs. Adversaries can exploit this blind spot to hijack the control flow of the LLM’s interpretation with minimal edits and without affecting actual runtime behavior. We refer to this attack as a Familiar Pattern Attack (FPA). We develop a fully automated, black-box algorithm that discovers and injects FPAs into target code. Our evaluation shows that FPAs are not only effective against basic and reasoning models, but are also transferable across model families (OpenAI, Anthropic, Google), and universal across programming languages (Python, C, Rust, Go). Moreover, FPAs remain effective even when models are explicitly warned about the attack via robust system prompts. Finally, we explore positive, defensive uses of FPAs and discuss their broader implications for the reliability and safety of code-oriented LLMs. Large Language Models (LLMs) are increasingly trusted to perform automated code review and static analysis at scale, supporting tasks such as vulnerability detection, summarization, and refactoring. In this paper, we identify and exploit a critical vulnerability in LLM-based code analysis: an abstraction bias that causes models to overgeneralize familiar programming patterns and overlook small, meaningful bugs. Adversaries can exploit this blind spot to hijack the control flow of the LLM’s interpretation with minimal edits and without affecting actual runtime behavior. We refer to this attack as a Familiar Pattern Attack (FPA). We develop a fully automated, black-box algorithm that discovers and injects FPAs into target code. Our evaluation shows that FPAs are not only effective against basic and reasoning models, but are also transferable across model families (OpenAI, Anthropic, Google), and universal across programming languages (Python, C, Rust, Go). Moreover, FPAs remain effective even when models are explicitly warned about the attack via robust system prompts. Finally, we explore positive, defensive uses of FPAs and discuss their broader implications for the reliability and safety of code-oriented LLMs.

---

## 论文详细总结（自动生成）

好的，以下是对论文《Trust Me, I Know This Function: Hijacking LLM Static Analysis using Bias》的详细、结构化总结。

### 1. 论文的核心问题与整体含义

**核心问题**：论文揭示了大语言模型在用于代码静态分析时存在一个关键漏洞——“抽象偏见”。模型在面对常见、熟悉的编程模式（如排序、素数检查等算法）时，倾向于进行高层次的语义概括，直接套用其“记忆”中的行为，而跳过了对代码具体实现的细节推理，从而忽略代码中隐藏的微小但致命的错误。

**整体含义（研究动机与背景）**：
-   **背景**：大语言模型正日益被信赖并大规模应用于自动化代码审查、漏洞检测、代码摘要和重构等任务。这些应用建立在LLM能准确、鲁棒地理解代码的假设之上。
-   **动机**：论文旨在证明这种信任是错误的。通过展示“抽象偏见”如何被武器化，研究者警告，依赖LLM的自动化代码分析工作流存在被系统性地误导的风险，可能导致漏报恶意代码或虚报代码行为，对软件供应链安全构成严重威胁。

### 2. 论文提出的方法论

**核心思想**：提出并系统化了一种名为**熟悉模式攻击**的新型对抗样本攻击。攻击者通过在看似无害的、结构熟悉的代码片段中嵌入微小的、不改变程序实际运行时行为的错误（如将 `<=` 改为 `<`），来劫持LLM对代码控制流的解释，让模型“看到”不存在的逻辑，或“忽略”实际执行的逻辑。

**关键技术细节 - 算法流程 (`Algorithm 1`)**：
论文开发了一套完全自动化、黑盒的攻击生成算法，无需梯度信息。其流程如下：
1.  **生成熟悉模式函数 `P`**：使用LLM生成一个实现常见算法且输入 `a` 对应的输出 `v` 可预测的函数 `P`。
2.  **生成欺骗模式 `P' = P + Δ`**：对 `P` 进行微小的语义级扰动 `Δ`，得到变体 `P'`，该变体在运行时对相同输入 `a` 会输出不同的值 `v'`，但必须语法正确且外观上仍像是一个正常的算法实现。
3.  **注入并验证FPA样本 `x'`**：将 `P'` 注入到目标代码 `x` 中，用它来主导一个条件分支，以控制某个攻击者期望的“目标行为 `t`”的执行。然后，通过LLM查询和实际执行来验证：
    *   **运行时不变性**：`exec(x ⊕ (P', t))` 必须等于 `exec(x)`，即程序的实际输出不变。
    *   **解释被劫持**：对于LLM，`f(x ⊕ (P', t))` 应该错误地预测为 `f(x ⊕ (P, t))`，即模型认为“目标行为 `t`”会发生，但实际并未发生。

**公式化表述 (`Equation 1`)**：
论文将FPA的生成定义为一个约束优化问题，目标是最小化“对抗风险” `RA` 和“对抗成本” `C` 之和：
`minΔ RA(x′, f) + λ · C(Δ)`
*   **对抗风险 (`RA`)**：多次推理中，LLM对攻击样本 `x'`的解释偏离其原始解释的概率。
*   **对抗成本 (`C`)**：衡量扰动 `Δ` 的隐蔽性和自然度的主观惩罚项。
*   **硬约束**：`exec(x') = exec(x)`，即修改后的程序必须可执行且功能等价。

### 3. 实验设计

**数据集与场景**：
-   **静态分析场景**：使用LLM生成50个多样化的Python函数（涵盖数据验证、安全守卫、分类等）作为目标代码 `X`。评估LLM是否能正确预测程序的输出。
-   **防御性应用场景**：
    -   **防代码抄袭**：同上50个Python样本，评估LLM在代码重写后是否能保持原有功能。
    -   **防网页抓取**：从一个公开的HTML/CSS数据集选取样本，评估LLM抓取网页时是否会包含攻击者注入的无意义内容。
-   **真实世界代码与智能体场景**：取50个拥有超过1000颗星的GitHub Python仓库，将FPA注入到超过150行的代码文件中。使用两个商用代码智能体（Cursor和GitHub Copilot，后端均为GPT-5）来判断代码行为。

**基准方法与对比**：
-   对于每个攻击样本`x' = x ⊕ P'`，设置两个基线进行对比：
    -   **原始程序 `x`**：未做任何修改。
    -   **良性模式注入 `x ⊕ P∅`**： 注入了函数 `P`（即无bug的熟悉模式），且不改变原程序逻辑。用于证明性能下降是 `P` 中的错误导致的，而非函数 `P` 本身造成的复杂性。

**评估模型（非推理与推理）**：
-   **非推理模型**：GPT-4o， Claude 3.5 Sonnet， Gemini 2.0 Flash。
-   **推理模型**：GPT-o3， Claude 4.0 (Extended Thinking)， Gemini 2.5 Pro。

### 4. 资源与算力

论文**未明确提及**具体的GPU型号、数量或训练时长。攻击生成和评估过程完全基于对商业黑盒API的查询，资源消耗主要以**API调用成本**和**时间**来衡量。

-   **攻击生成成本**：
    -   基础模型：生成一个FPA大约需要5-7分钟，花费约0.38美元。
    -   推理模型：成本更高，例如Gemini 2.5 Pro约需1小时和3.67美元，GPT-o3约需4.5小时和13.40美元。
-   **实验评估成本**：单次评估实验（覆盖50个目标程序和10个欺骗模式的各种组合，每个10次重复）平均花费约150美元。
-   **代码智能体评估**：使用了后端的GPT-5，但未报告具体的API成本。

### 5. 实验数量与充分性

实验设计全面，覆盖广泛，具备充分性和客观性：
-   **多模型鲁棒性**：攻击在来自三家不同公司（OpenAI， Anthropic, Google）的六款当前最先进的基础和推理模型上进行了验证。
-   **跨模型、跨语言可转移性**：这是实验的关键部分。证明了用GPT-4o在Python下生成的FPA，可以成功欺骗Claude和Gemini；并且将Python欺骗模式翻译为C、Rust和Go后，攻击仍然有效。
-   **攻击规模**：使用算法生成了大量欺骗模式（例如GPT-o3生成了88种），并且从发现率曲线来看，空间远未饱和。
-   **真实性测试**：在50个真实GitHub仓库上对实战代码智能体进行了黑盒攻击测试。
-   **适应性对手**：通过设计专门的防御提示词警告模型此攻击的存在，测试了攻击的顽固性。
-   **攻击隐蔽性**：将FPA与传统的代码混淆技术（使用不同级别的`tigress`不透明谓词）进行了可检测性对比。
-   **性能开销**：测量了注入FPA后的微小运行时开销（平均65.82微秒）
-   **消融实验**：对函数名和变量名进行随机化替换，验证了攻击源于结构偏见而非标识符记忆。

### 6. 论文的主要结论与发现

-   **抽象偏见是真实且可利用的漏洞**：LLM在分析代码时会因“熟悉”而忽略细节，即使代码中存在确定性错误。
-   **FPA攻击高效、可扩展、可转移**：自动生成的、微小的代码扰动即可使顶尖LLM的代码解释准确率从约90%急剧下降至10-20%。该攻击可在黑盒设置下，跨模型族和编程语言工作。
-   **攻击对推理模型和防御提示具有鲁棒性**：即使是专门设计用于复杂推理的模型，以及明确被警告攻击存在的模型，也无法抵御FPA。
-   **FPA具有双重用途**：该技术不仅能被恶意使用，还能用于防御性目的，如抵抗基于LLM的代码剽窃、网页抓取和水印追踪。
-   **LLM“理解”代码的深层隐患**：该研究揭示了LLM在代码理解上依赖模式匹配而非真正语义分析的本质，这对于依赖LLM执行安全关键任务的行业是一个严重警示。

### 7. 优点

-   **发现新漏洞**：首次系统性定义和研究了LLM代码分析中的“抽象偏见”漏洞，并将其武器化为一种新的攻击范式。
-   **攻击方法巧妙且强大**：攻击不依赖传统混淆，极其隐蔽且成本低。其自动化、黑盒、可转移和跨语言的特性使其具有极高的现实威胁性。
-   **评估极为全面**：实验覆盖了多个顶尖模型、多种编程语言、实际代码库和商业智能体，同时还评估了防御场景和对抗适应能力，证据链条完整且严谨。
-   **兼顾攻防的视角**：不仅揭示了攻击面，还探讨了该技术的防御性用途，展现了研究的深度和对更广泛安全生态影响的思考。
-   **影响深远**：揭示了现有LLM训练范式（数据去重难以解决）和推理框架（静态分析难以规模应用）在面对此类攻击时的根本性困境。

### 8. 不足与局限

-   **攻击类型尚属“针对性”**：论文主要展示的是“针对性”攻击，即诱导模型产生特定错误预测。虽然提到了“非针对性”攻击（仅需产生任意错误），但未对其深入评估。
-   **生成成本与效率**：尽管攻击成功率高，但为每个目标或模型生成高效FPA仍有成本，尤其是在使用昂贵的推理模型时，尽管这仅是一次性投入。
-   **防御性应用的对手模型单一**：在评估防御性应用（如防抄袭）时，仅测试了LLM直接重写代码的能力，可能没有覆盖其他更高级的、结合了动态分析的代码重写工具。
-   **缓解策略探索有限**：虽然论文指出了提示工程和数据去重的无效性，但它并未深入探索或提出更具前景的缓解方案（如特定微调），将此作为了开放问题。
-   **可检测性评估的相对性**：FPA之所以隐蔽，部分原因在于当前工作流默认不执行动态分析。如果生产环境改变，强制添加轻量级的符号执行或沙箱测试，攻击的有效性会降低。论文将这种不执行动态分析作为前提假设，这点值得商榷。

（完）

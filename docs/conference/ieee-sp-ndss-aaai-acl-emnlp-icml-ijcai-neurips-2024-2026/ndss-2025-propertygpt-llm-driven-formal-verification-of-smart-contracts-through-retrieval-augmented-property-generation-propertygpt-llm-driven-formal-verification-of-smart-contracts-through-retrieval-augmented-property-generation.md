---
title: "PropertyGPT: LLM-driven Formal Verification of Smart Contracts through Retrieval-Augmented Property Generation"
title_zh: PropertyGPT：通过检索增强属性生成实现LLM驱动的智能合约形式化验证
authors: "Ye Liu, Yue Xue, Daoyuan Wu, Yuqiang Sun, Yi Li, Miaolei Shi, Yang Liu"
date: 2025-01-01
pdf: "https://www.ndss-symposium.org/wp-content/uploads/2025-1357-paper.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 自动化生成智能合约形式化验证的属性
tldr: 针对智能合约形式化验证中人工编写属性费时且覆盖不足的问题，提出PropertyGPT，利用检索增强的大语言模型自动生成不变式、前置/后置条件等属性，提升验证效率和安全性。
source: NDSS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1724, \"height\": 547, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 926, \"height\": 1261, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 926, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 820, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 846, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 973, \"height\": 1167, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 919, \"height\": 611, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 969, \"height\": 170, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 907, \"height\": 593, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1732, \"height\": 477, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 922, \"height\": 799, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 930, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-propertygpt-llm-driven-formal-verification-of-smart-contracts-through-retrieval-augmented-property-generation/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1250, \"height\": 2210, \"label\": \"Table\"}]"
motivation: 智能合约形式化验证缺乏自动化属性生成，依赖专家手动编写，成本高且易遗漏。
method: 结合检索增强生成，利用大语言模型从类似合约和历史属性中检索并生成全面的验证属性。
result: 能自动生成高质量的验证属性，与现有验证工具结合，提高安全漏洞发现率。
conclusion: PropertyGPT展示了LLM在自动生成形式化验证属性方面的潜力，推动了智能合约安全验证的自动化。
---

## Abstract
Formal verification is a technique that can prove the correctness of a system with respect to a certain specification or property. It is especially valuable for security-sensitive smart contracts that manage billions in cryptocurrency assets. Although existing research has developed various static verification tools (or provers) for smart contracts, a key missing component is the automated generation of comprehensive properties, including invariants, pre-/post-conditions, and rules. Hence, industry-leading players like Certora have to rely on their own or crowdsourced experts to manually write properties case by case. With recent advances in large language models (LLMs), this paper explores the potential of leveraging state-of-the-art LLMs, such as GPT-4, to transfer existing human-written properties (e.g., those from Certora auditing reports) and automatically generate customized properties for unknown code. To this end, we embed existing properties into a vector database and retrieve a reference property for LLM-based in-context learning to generate a new property for a given code. While this basic process is relatively straightforward, ensuring that the generated properties are (i) compilable, (ii) appropriate, and (iii) verifiable presents challenges. To address (i), we use the compilation and static analysis feedback as an external oracle to guide LLMs in iteratively revising the generated properties. For (ii), we consider multiple dimensions of similarity to rank the properties and employ a weighted algorithm to identify the top-K properties as the final result. For (iii), we design a dedicated prover to formally verify the correctness of the generated properties. We have implemented these strategies into a novel LLM-based property generation tool called PropertyGPT. Our experiments show that PropertyGPT can generate comprehensive and high-quality properties, achieving an 80% recall compared to the ground truth. It successfully detected 26 CVEs/attack incidents out of 37 tested and also uncovered 12 zero-day vulnerabilities, leading to $8,256 in bug bounty rewards. Formal verification is a technique that can prove the correctness of a system with respect to a certain specification or property. It is especially valuable for security-sensitive smart contracts that manage billions in cryptocurrency assets. Although existing research has developed various static verification tools (or provers) for smart contracts, a key missing component is the automated generation of comprehensive properties, including invariants, pre-/post-conditions, and rules. Hence, industry-leading players like Certora have to rely on their own or crowdsourced experts to manually write properties case by case. With recent advances in large language models (LLMs), this paper explores the potential of leveraging state-of-the-art LLMs, such as GPT-4, to transfer existing human-written properties (e.g., those from Certora auditing reports) and automatically generate customized properties for unknown code. To this end, we embed existing properties into a vector database and retrieve a reference property for LLM-based in-context learning to generate a new property for a given code. While this basic process is relatively straightforward, ensuring that the generated properties are (i) compilable, (ii) appropriate, and (iii) verifiable presents challenges. To address (i), we use the compilation and static analysis feedback as an external oracle to guide LLMs in iteratively revising the generated properties. For (ii), we consider multiple dimensions of similarity to rank the properties and employ a weighted algorithm to identify the top-K properties as the final result. For (iii), we design a dedicated prover to formally verify the correctness of the generated properties. We have implemented these strategies into a novel LLM-based property generation tool called PropertyGPT. Our experiments show that PropertyGPT can generate comprehensive and high-quality properties, achieving an 80% recall compared to the ground truth. It successfully detected 26 CVEs/attack incidents out of 37 tested and also uncovered 12 zero-day vulnerabilities, leading to $8,256 in bug bounty rewards.

---

## 论文详细总结（自动生成）

好的，这是对论文《PropertyGPT: LLM-driven Formal Verification of Smart Contracts through Retrieval-Augmented Property Generation》的结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义

*   **研究背景与动机**：形式化验证对于保障管理巨额加密资产的智能合约的安全性至关重要。然而，其有效性高度依赖于全面且正确的“属性”（如不变式、前置/后置条件、规则）规格说明。编写这些属性需要深厚的专业知识，目前工业界（如Certora公司）主要依赖专家手动编写，成本高、耗时长，难以大规模应用，成为形式化验证在智能合约领域落地的关键瓶颈。
*   **核心问题**：本文旨在探索如何利用大语言模型（LLMs）强大的上下文学习能力，实现**自动化、全面地生成智能合约形式化验证属性**，从而代替昂贵的人工编写过程，使得对“未知代码”进行有效形式化验证成为可能。

### 2. 论文提出的方法论

论文的核心思想是利用**检索增强生成（RAG）** 技术，将现有的人工编写属性作为知识库，引导LLM为新的智能合约代码自动生成定制化属性。提出的系统名为**PropertyGPT**，其方法论围绕三个关键挑战展开：确保生成属性的**可编译性**、**适当性**和**可验证性**。

*   **核心思想与流程**：
    1.  **知识库构建与检索**：将现有人工编写属性所对应的“关键代码”嵌入向量数据库，而非属性本身。对于待测试的代码片段，通过向量相似度检索出最相似的参考代码及其对应属性。
    2.  **上下文学习生成**：将检索到的参考属性作为少样本（one-shot）示例，通过专门设计的提示模板（区分用于生成跨函数的“规则”属性和函数级的“条件/不变式”属性），引导LLM（GPT-4）生成新的候选属性。
    3.  **迭代修复（确保可编译性）**：
        *   将生成的属性通过一个专门设计的PSL编译器进行编译。
        *   若编译失败，利用编译器的错误反馈作为外部预言机（oracle），结合修复提示模板，指导LLM进行迭代修正，直到编译通过或达到最大尝试次数。
        *   通过静态检查确保属性包含了目标函数，否则用特殊提示模板进行针对性修复。
    4.  **加权排序（确保适当性）**：
        *   提出一个基于多维度相似性的加权评分机制来对所有编译通过的属性进行排序。
        *   评分公式为：`Score(f, φ1) = α * Xraw(f, g) + β * Xsummary(f, g) + γ * Yraw(φ1, φ2) + η * Ysummary(φ1, φ2)`。
        *   其中`Xraw`, `Xsummary`是代码`f`与参考代码`g`的原始与功能摘要相似度；`Yraw`, `Ysummary`是生成属性`φ1`与参考属性`φ2`的原始与摘要相似度。系数`α, β, γ, η`通过线性回归模型在生成的数据上训练得到。最终选取Top-K个得分最高的属性作为结果。
    5.  **属性验证（确保可验证性）**：
        *   设计了专用的PSL（Property Specification Language）和配套证明器（Prover）。
        *   采用源代码级的前向符号执行，结合模块化验证与有界模型检查。
        *   如果属性被证明成立，则验证通过；若发现反例（counterexample），则表明属性被违反，可能意味着存在漏洞，需进一步人工确认。

### 3. 实验设计

*   **数据集与基准**：
    *   **属性生成质量评估**：从23个Certora审计项目中收集了623个人工编写属性。将其分为训练集（作为知识库）和测试集（90个属性，来自9个项目），用于评估生成属性与人工编写“真值”属性的匹配度。
    *   **漏洞检测能力评估**：
        *   **CVE数据集**：随机选取了13个不同类型的已知智能合约CVE（如整数溢出、访问控制漏洞等）。
        *   **攻击事件数据集**：从一个同行工作（SmartInv）的基准中整理出24个真实世界的攻击事件项目。
*   **对比方法**：
    *   在漏洞检测任务上，将PropertyGPT与GPTScan+、静态分析工具Slither，以及字节码级符号执行工具Manticore和Mythril进行了对比。也定性地与同期的LLM驱动工具SmartInv进行了比较。

### 4. 资源与算力

*   论文中**未明确提及**所使用的算力详情，如GPU型号、数量或模型训练/推理的总时长。提到了使用OpenAI API（`gpt-4-0125-preview`模型）进行属性生成，以及使用`text-embedding-ada-002`模型计算嵌入相似度，但未给出具体的API调用成本或总资源消耗。实验环境为配备2.2GHz Intel Xeon处理器和2GB RAM的Docker容器。

### 5. 实验数量与充分性

*   **实验组数**：论文围绕5个研究问题（RQ）设计了多组实验，包括：
    1.  **属性生成准确性（RQ1）**：在90个属性的测试集上评估。
    2.  **漏洞检测有效性（RQ2）**：在13个CVE和24个攻击事件项目上进行检测。
    3.  **泛化能力测评（RQ3）**：通过分析CVE/攻击事件数据集中的被测代码与参考代码的相似度，间接衡量泛化性。
    4.  **消融实验（RQ4）**：研究了Top-K设置（K从1到9）对效果的影响，以及编译反馈迭代修复的分布和成功率。
    5.  **真实世界影响（RQ5）**：在4个真实的赏金项目上寻找零日漏洞。
*   **充分性与公平性分析**：
    *   **充分性**：实验设计较为全面，覆盖了内部生成质量、外部漏洞检测能力、泛化性、关键参数影响和实际应用价值等多个维度。使用了真值对比、对抗性测试（CVE/攻击事件）和真实场景测试，评价体系相对完整。
    *   **公平性**：与多种类型工具（LLM-based、静态分析、符号执行）在标准数据集上进行了对比，较为公平。但生成属性与“真值”的等效性由人工判断，虽然文中说明了多人独立审查并公开了数据，但仍存在一定主观性偏差风险。与SmartInv的对比仅是定性描述，不够直接和量化。

### 6. 论文的主要结论与发现

*   PropertyGPT能够生成高质量、全面的属性，其生成的属性经人类专家评判，可覆盖**80%** 的人工编写“真值”属性，精确率为64%。
*   PropertyGPT能有效检测漏洞，在37个测试样本（13个CVE + 24个攻击事件）中**成功检测出26个**，并发现了**12个零日漏洞**，获得了**8，256美元的漏洞赏金**。
*   PropertyGPT展现出足够的泛化能力，其知识库（来自Certora项目）能成功应用于分析完全不同来源的CVE和攻击事件代码，其成功案例的代码相似度在0.64到0.73之间。
*   迭代编译反馈修复是有效的，**84%** 的属性可在5次尝试内成功编译，使得整体生成成功率达到了87%。Top-2的属性选择在精确率和召回率之间取得了最佳平衡。

### 7. 优点

*   **新颖的解决方案**：首次系统性地将RAG与LLM结合，用于解决智能合约验证中“属性生成”这一核心难题，实现了从依赖专家到自动化的突破。
*   **技术设计全面**：Pipeline完整地考虑了生成属性的三个关键特性（可编译、适当、可验证），并针对性地设计了迭代修复、加权排序和专用验证器，环环相扣。
*   **多维度实验验证**：不仅评估了生成属性的内部质量，还在CVE、真实攻击事件和零日漏洞发现等多种外部场景下验证了其有效性，证据链扎实。
*   **真实世界影响力**：通过发现零日漏洞并获得赏金，证明了系统的实用价值，而不仅仅是学术概念。

### 8. 不足与局限

*   **属性等效性判断的主观性**：评估生成属性与人工属性是否“等效”依赖人工判断，虽然采取了多人校验，但缺乏自动化的客观等效性检查工具，这可能引入偏差。
*   **泛化能力的衡量方式较为间接**：通过被测代码与参考代码的相似度来间接衡量泛化性，虽然合理，但没有直接证明生成属性的正确性在低相似度场景下依然保持。
*   **特定漏洞类型的局限性**：论文提到，对于需要运行时上下文（如通缩代币滥用）或不常见属性模式（如不良随机性、错误的`delegatecall`使用）的漏洞，PropertyGPT可能失效。系统的能力上限受限于其知识库中的属性类型。
*   **对LLM的依赖**：系统性能强依赖于底层LLM（GPT-4）的能力，存在供应商锁定、成本变化、模型更新导致性能波动等潜在风险。文中未提供实验成本的经济学分析。

（完）

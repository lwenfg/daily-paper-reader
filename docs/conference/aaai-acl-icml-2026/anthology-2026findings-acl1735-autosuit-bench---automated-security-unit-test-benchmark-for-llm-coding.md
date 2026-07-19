---
title: AutoSUIT Bench - Automated Security UnIt Test Benchmark for LLM Coding
title_zh: AutoSUIT Bench：用于LLM编程的自动化安全单元测试基准
authors: "Samuel Osebe, Fan Yang, Junyi Li, Yue Gu, Yongxin Wang, Satyapriya Krishna, Kai-Wei Chang, Aram Galstyan, Rahul Gupta, Weitong Ruan"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1735.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 自动化安全单元测试基准用于评估LLM代码安全性
tldr: 针对LLM代码安全评估中基准覆盖率低、误报率高的问题，提出AutoSUIT Bench自动验证基准。覆盖232个CWE类别及C/C++/Java/Python语言，通过迭代自动验证创建高质量漏洞样本，为全面评估LLM代码安全性提供了可靠框架。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1587, \"height\": 683, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 775, \"height\": 605, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1576, \"height\": 835, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1394, \"height\": 1081, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1620, \"height\": 631, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1620, \"height\": 637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 754, \"height\": 578, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 733, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 752, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 737, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 734, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 732, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1351, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 732, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 743, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1632, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 732, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 745, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1577, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1579, \"height\": 1212, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1614, \"height\": 737, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1617, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1621, \"height\": 636, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1735/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1589, \"height\": 1196, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1735/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1479, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1735/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1507, \"height\": 499, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1735/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1534, \"height\": 474, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1735/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1668, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1735/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1555, \"height\": 1397, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1735/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1512, \"height\": 665, \"label\": \"Table\"}]"
motivation: 现有基准误报率高，仅覆盖少数CWE类别，安全评估不全面。
method: 提出自动验证基准构建范式，迭代自动验证，生成覆盖232个CWE的漏洞代码基准。
result: 构建的基准在多语言、多编码任务上实现广泛覆盖，有效评估LLM代码安全性。
conclusion: 提供更全面可靠的LLM代码安全评估工具，推动负责任的代码生成实践。
---

## Abstract
Large Language Models (LLMs) are evolving rapidly on code generation tasks. While it is important to evaluate their code generation accuracy, ensuring they follow responsible practices is equally critical. Some of the previous works use tools such as CodeQL to match patterns against Common Weakness Enumeration (CWE), suffering from high error rate, while others rely on human annotation to only focus on top CWE categories, limiting security coverage. We propose AutoSUIT Bench, which addresses these limitations through a paradigm to automate the vulnerable code benchmark creation with iterative auto validation. As a result, our benchmark covers 232 CWE categories across C/C++, Java, and Python languages and is designed to evaluate on four coding tasks: (i) code generation, (ii) generation with CWE context, (iii) security patching, and (iv) code completion. Upon benchmarking against LLMs, we found that functionality pass rate is consistently higher than vulnerability pass rate for all programming languages. One notable observation from our benchmark is that LLMs perform well on top CWEs while lacks on others down the list. This highlights the necessity of vulnerable code benchmarks with larger CWE coverage.

---

## 论文详细总结（自动生成）

# 论文总结：AutoSUIT Bench——面向LLM编程的自动化安全单元测试基准

## 1. 论文的核心问题与整体含义
*   **研究动机与背景**：
    *   现有评估LLM代码生成安全性的基准存在两大缺陷：
        *   依赖CodeQL等静态分析工具进行模式匹配，误报率高。
        *   依赖人工标注，只关注少数最危险的CWE类别，安全覆盖率低。
    *   动态测试（单元测试）方法受限于人工创建测试用例的高昂成本，现有动态基准覆盖的CWE数量极少（不足50个）。
    *   因此，迫切需要一种能**自动化、大规模、高质量**地构建安全代码基准的方法，以全面评估LLM在多种编程语言和多种编程任务下的安全性。

## 2. 方法论：核心思想与关键技术细节
*   **核心思想**：提出 **AutoSUIT** 范式，从通用弱点枚举（CWE）的规格说明和示例代码出发，利用一个“预言LLM”自动生成功能代码、功能单元测试、安全代码和安全单元测试，并通过**迭代自动验证与修正**确保基准质量，最终构建出高覆盖、解耦功能与安全的基准 **AutoSUIT Bench**。
*   **关键技术组件与流程**（对应论文Algorithm 1）：
    1.  **任务构建**：解析CWE定义与示例代码，通过LLM将不完整的示例重写为功能正确但包含漏洞的可执行代码（`Cvul`），并生成详细的自然语言代码描述（`Dcode`）。
    2.  **功能单元测试生成**：基于漏洞代码和描述生成初步功能测试（`Uf`），然后通过编译器/解释器自动验证，利用编译错误和测试失败信息（`M`）迭代修正测试，直到全部通过或达到最大迭代次数`K`，确保测试正确反映功能意图。
    3.  **安全代码生成**：提示LLM为漏洞代码打补丁生成安全代码（`Csec`），并强制其通过所有功能单元测试，保证行为等价。
    4.  **脆弱性单元测试生成**：利用CWE描述指导LLM直接生成安全测试用例（`Tsec`），并将其转换为安全单元测试（`Us`）。将这些测试在安全代码（`Csec`）上验证与迭代修正，确保测试能够准确区分安全与不安全行为。
    5.  **解耦设计**：功能测试源自漏洞代码，安全测试源自补丁后的安全代码，防止两类测试相互干扰或泄露信息。
*   **评估指标**：改进了传统的`pass@k`指标，从二元通过判断（全部测试用例通过）改为基于**通过测试用例比例**的离散化度量，能更细致地反映代码在功能性和安全性上的达成程度。

## 3. 实验设计
*   **基准数据集**：**AutoSUIT Bench**，覆盖 **232个CWE类别**，包含 **952个样本**，分布于 **C、C++、Java、Python** 四种语言。
*   **评估任务**：设计了四种编码任务场景：
    1.  **安全代码生成**：仅给定代码描述。
    2.  **带CWE上下文生成**：给定代码描述及对应CWE描述。
    3.  **安全修补**：给定漏洞代码和描述，要求生成修补后的安全代码。
    4.  **代码补全**：给定30%的安全代码前缀和描述，要求补全剩余代码。
*   **对比模型**：评估了8款主流LLM，包括 Claude（Opus 4、Opus 4.1、Sonnet 4、Sonnet 3.7）、Llama（3.1、3.2）和 Nova（Pro、Premier）系列，均通过Amazon Bedrock API调用。
*   **评估流程**：每个样本使用10种不同的提示模板生成代码，使用其改进的`pass@k`指标分别计算功能性通过率和安全性通过率。

## 4. 资源与算力
*   **文中未明确说明所使用的算力**（如GPU型号、数量、训练时长等）。实验为通过API调用现有LLM进行推理评估，不涉及模型训练，因此未提供算力消耗细节。

## 5. 实验数量与充分性
*   **实验组数量**：实验规模庞大且充分，包括：
    *   **主要对比实验**：4种语言 × 4种任务 × 8款模型，每个样本生成10次（不同提示模板），计算功能/安全通过率。
    *   **对比分析**：深入对比了“带CWE上下文”和“安全修补”任务相对于“代码生成”任务的性能变化，按模型、语言分类展示。
    *   **消融/验证实验**：
        *   通过手工构建的黄金标准数据集（22个安全文件、48个漏洞文件）筛选出最佳预言LLM（GPT-4o）。
        *   对预言LLM生成的功能测试进行代码覆盖率验证（达到99.4%）。
        *   通过人类安全专家研究来验证安全测试的合理性，抽样22个CWE的手动评估显示平均覆盖率达84.3%。
    *   **主动漏洞发现**：分析了LLM生成的漏洞在CWE上的分布，与“Top 25最危险CWE”对比，揭示了评估盲区。
*   **客观性与公平性**：实验设计高度客观公平，使用相同的标准API、一致的提示模板集、统一的改进版pass@k指标，以及解耦的功能/安全测试集。

## 6. 主要结论与发现
1.  **功能优于安全**：所有测试的LLM在所有语言上，**功能性通过率均一致高于安全性通过率**，表明安全代码生成仍有巨大提升空间。
2.  **CWE偏好差异**：LLM在**常见/排名靠前的CWE**上表现较好，但在**少见/排名靠后的CWE**上表现显著下降。其风险画像与人类不同，这意味着仅评估Top CWE会导致严重的安全盲区。
3.  **任务难度差异**：**安全修补任务比代码生成更具挑战性**，不仅安全性得分下降，还会引入额外语法错误或逻辑问题（尤其Java）。
4.  **上下文影响复杂**：提供CWE描述作为上下文，其在C语言上普遍提升安全性，但在Java和Python上却可能导致性能下降。
5.  **代码补全相对容易**：提供部分代码前缀的代码补全任务普遍带来功能和安全性的双重提升，表明更具体的上下文对LLM更友好。

## 7. 优点
*   **高度自动化与可扩展**：成功将基准构建从人工耗时的过程转变为基于CWE的自动流水线，并实现高覆盖率（232个CWE）。
*   **设计精良与高质量**：通过迭代自动验证和修正确保基准代码和测试的可执行性与正确性，功能测试代码覆盖率达99.4%，安全测试经人工验证平均覆盖84.3%。
*   **评价体系更科学**：解耦了功能性与安全性的评估，并提出基于测试用例通过比例的`pass@k`改进指标，能更细腻地捕捉模型能力差异。
*   **洞察深刻**：首次系统性地揭示了LLM在不同频率CWE上的性能差异，证明了扩大CWE评估覆盖范围的重要性。

## 8. 不足与局限
*   **测试覆盖并非穷举**：安全测试基于CWE描述生成，无法保证覆盖所有可能的漏洞变体和边界情况。
*   **范围限制**：基准目前仅聚焦于**函数级**代码，不支持跨文件、依赖交互或系统配置等代码库级别的复杂漏洞。
*   **语言支持有限**：仅支持C/C++、Java和Python四种主流语言，扩展到其他语言是未来工作。
*   **潜在滥用风险**：明确针对软件漏洞的基准存在被恶意用于LLM漏洞利用开发的风险，作者呼吁负责任地使用。
*   **计算开销**：动态测试（编译并执行）虽然准确，但相比静态评估或纯提示测试，会带来更高的计算成本和工程开销。

（完）

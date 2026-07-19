---
title: "A.S.E: A Repository-Level Benchmark for Evaluating Security in AI-Generated Code"
title_zh: A.S.E：评估AI生成代码安全性的仓库级基准
authors: "Keke Lian, Wang Bin, Lei Zhang, Libo Chen, Junjie Wang, Ziming Zhao, Yujiu Yang, Miaoqian Lin, Haotong Duan, Haoran Zhao, Shuang Liao, Mingda Guo, Quan Jiazheng, Yilu Zhong, Chenhao He, Chen Zichuan, Jie Wu, Haoling Li, Zhaoxuan Li, Jiongchi Yu, Hui LI, Dong Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1569.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 仓库级评估AI生成代码的安全性
tldr: 针对现有AI代码安全基准脱离真实场景的问题，提出A.S.E.仓库级评估基准，紧密模拟实际AI编程任务。评估主流LLM发现，当前模型在代码安全方面存在显著不足，该基准为AI生成代码的安全评估提供了可靠框架，强调部署前安全审查的必要性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1557, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 662, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 741, \"height\": 290, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 746, \"height\": 280, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 627, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1567, \"height\": 865, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 609, \"height\": 666, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 805, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1319, \"height\": 746, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1569/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1569/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1339, \"height\": 1000, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1569/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 813, \"height\": 491, \"label\": \"Table\"}]"
motivation: 现有AI代码安全基准缺乏真实世界相关性，无法有效评估LLM生成代码的安全风险。
method: 提出A.S.E.基准，基于仓库级上下文，模拟实际AI编程任务全面评估代码安全性。
result: 发现当前LLM在AI生成代码安全方面表现不佳，存在明显漏洞。
conclusion: 需在真实编程场景下严格评估LLM代码安全，A.S.E.为此提供了有效工具。
---

## Abstract
The increasing adoption of large language models (LLMs) in software engineering necessitates rigorous security evaluation of their generated code. However, existing benchmarks often lack relevance to real-world AI-assisted programming scenarios, making them inadequate for assessing the practical security risks associated with AI-generated code in production environments. To address this gap, we introduce A.S.E (AI Code Generation Security Evaluation), a repository-level evaluation benchmark designed to closely mirror real-world AI programming tasks, offering a comprehensive and reliable framework for assessing the security of AI-generated code. Our evaluation of leading LLMs on A.S.E reveals several key findings. In particular, current LLMs still struggle with secure coding. The complexity in repository-level scenarios presents challenges for LLMs that typically perform well on snippet-level tasks. Moreover, a larger reasoning budget does not necessarily lead to better code generation. These observations offer valuable insights into the current state of AI code generation and help developers identify the most suitable models for practical tasks. They also lay the groundwork for refining LLMs to generate secure and efficient code in real-world applications.

---

## 论文详细总结（自动生成）

好的，以下是基于所提供的论文内容，生成的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：大型语言模型（LLM）在软件工程中的应用日益广泛，显著提升了编程效率。然而，AI生成的代码可能包含安全漏洞，给生产环境带来严重风险。
*   **核心问题**：现有的代码评估基准存在显著不足，无法有效评估AI生成代码在实际生产环境中的安全风险。具体表现为：
    *   **数据脱离真实世界**：多数基准使用人工合成的代码片段，与真实项目的功能和安全场景相关性低。
    *   **任务脱离实际编程范式**：任务仅限于孤立的代码片段，缺乏文件内和跨文件的上下文，与主流AI编程助手（如Cursor）的工作模式不符。
    *   **评估方法不可靠**：常依赖人工或LLM判断，难以自动化、可复现地进行一致评估。
*   **整体含义**：该论文旨在填补上述空白，通过构建一个贴近真实世界、仓库级别的评估基准A.S.E，为测量AI生成代码的安全性提供一个全面、可靠的框架。

### 2. 论文提出的方法论

核心思想是构建一个从真实世界漏洞驱动的、仓库级别的代码补全与安全评估框架。

*   **基准构建（A.S.E Benchmark Construction）**
    *   **数据源**：从包含已记录CVE的高质量GitHub开源仓库中提取数据，确保场景的真实性和安全敏感性。为防止数据泄露，对种子数据集进行语义（如标识符重命名）和结构（如控制流重构）突变，生成变体，确保评估的是模型能力而非记忆。
    *   **四阶段构建流程**：
        1.  **确定数据源**：从公开和内部漏洞数据库收集超过10万个原始CVE条目。
        2.  **过滤候选仓库**：通过CWE类型（聚焦Web相关漏洞）、提交记录可追溯性、仓库活跃度/流行度过滤，再使用CodeQL、Joern等静态分析工具交叉验证，得到199个候选仓库。
        3.  **专家指导优化与质量控制**：安全专家进行人工审查，剔除误报和修改文件过多的提交，精确标注漏洞代码区域，并设计针对性的CodeQL/Joern规则验证污点传播路径。最终保留40个仓库作为种子数据集。
        4.  **数据集扩展**：对40个种子仓库进行语义和结构突变，生成80个变体，形成共120个基准实例。
*   **任务设定（Task Settings）**
    *   **模拟真实工作流**：模仿Cursor等AI编程助手，从仓库中提取文件内和跨文件上下文提供给LLM。模型需要根据漏洞功能描述和上下文，生成`diff`格式的补丁来修补被掩盖（`<masked>`）的漏洞代码。
    *   **上下文检索**：使用BM25算法，根据函数名、变量名等词法信号，从仓库中检索相关文件作为上下文。
*   **代码评估（Code Assessment）**
    *   **高精度、可复现的评估**：为每个测试用例（对应特定CVE）定制静态漏洞检测规则（通过CodeQL/Joern实现），定义精确的source-sink和污点传播路径。
    *   **综合评估指标**：
        *   **质量（Quality, 30%）**：衡量生成的补丁是否能成功集成到仓库，并通过基本的语法和静态检查。
        *   **安全性（Security, 60%）**：衡量集成补丁后，定制的静态分析工具检测到的特定CVE漏洞告警数量是否减少。公式为：`Security = (1/N) * Σ(s_t)`，其中`N`为测试次数，`s_t`为1表示告警减少，否则为0。
        *   **稳定性（Stability, 10%）**：通过多次运行结果的一致性来衡量。使用归一化后的标准差计算得分。
        *   **总分**：`Overall = 0.6 * Security + 0.3 * Quality + 0.1 * Stability`。

### 3. 实验设计

*   **数据集/场景**：使用自建的**A.S.E基准**，包含40个种子仓库和80个突变变体，总计**120个仓库级实例**。涵盖4种漏洞类型（SQL注入、路径遍历、跨站脚本、命令注入）和5种编程语言（PHP、Python、Go、JavaScript、Java）。
*   **Benchmark**：A.S.E自身即为新提出的benchmark。
*   **对比方法/模型**：评估了**26个主流LLM**，包含商业和开源模型，覆盖了“快思考”和“慢思考”（如思维链）两种推理范式。
    *   **商业模型**：Claude 3.7/4系列、GPT-4o/4.1/o3/o4-mini系列、Grok-3/4系列、Gemini 2.5 Pro、Qwen-Coder-Plus等。
    *   **开源模型**：Qwen3系列、DeepSeek-V3/R1、Kimi-K2、GLM-4.5等。

### 4. 资源与算力

*   论文在“D.2 实验设置”中提到实验环境为：Ubuntu系统，Intel(R) CPU @ 2.50 GHz，16线程，32 GB内存。
*   **未明确提及**用于模型推理的GPU型号、数量以及进行120个实例评估所需的总时长。由于评估的是云端API和自己部署的模型，具体的算力消耗不易统计，文中也未给出。

### 5. 实验数量与充分性

*   **实验数量**：
    *   **主要实验**：26个模型 × 120个基准实例 × 3次重复运行，产生了大量的评估数据点。
    *   **补充分析**：还包括了模型类别（架构、规模、推理范式）的对比分析、不同漏洞类型的挑战性分析、基准在原始/突变数据集上的一致性分析，以及针对性的案例研究。规模定律分析使用了Qwen2.5-Coder系列的6个模型和Qwen3系列的6个模型。
*   **充分性与公平性**：
    *   **充分性**：实验设计非常充分。模型覆盖面广（26个），基准实例多样（120个，含突变），多次运行考察稳定性，并从多个维度进行了深入分析。
    *   **公平性**：评估环境统一（固定上下文长度、最大输出长度、容器化环境），使用BM25确保所有模型接收相同的上下文，使用客观、可复现的静态分析规则而非主观判断进行评估。为每个测试实例定制规则，确保了评估的精确性。

### 6. 论文的主要结论与发现

*   **安全编码能力普遍不足**：所有评估的LLM在代码安全方面的表现均远低于其在代码质量（如语法正确性）上的表现。没有模型在Code Security得分上超过50分（满分100）。
*   **仓库级复杂性的挑战**：在复杂、需要跨文件上下文推理的仓库级场景中，模型表现显著下降。一些在代码片段级任务上表现优异的模型（如GPT-o3）在A.S.E上性能大幅下滑。
*   **慢思考≠更安全的代码**：在仓库级Web漏洞补全任务中，“慢思考”（如Claude的Thinking模式）配置在安全性上往往不如“快思考”模式，表明更大的推理预算不总能带来更好的代码生成。
*   **特定漏洞类型更具挑战性**：路径遍历（Path Traversal）是所有模型表现最弱的任务类型。
*   **模型类别差距缩小**：顶尖开源模型在安全代码生成方面的性能已可与商业模型比肩。

### 7. 优点

*   **高现实还原度**：基准源于真实世界仓库和CVE，任务模拟了现代AI编程工作流，评估方法具有高准确性和可复现性，这是相较以往工作的核心优势。
*   **评估体系全面**：从质量、安全性、稳定性三个维度进行评估，并提供了聚合总分，比单一指标更全面。
*   **防止数据泄露的设计**：通过语义和结构突变生成变体数据集，有效检验模型是依赖能力还是记忆。
*   **自动化与标准化**：整个评估流程（从上下文检索、补丁应用到安全扫描）高度自动化，并采用容器化技术确保环境一致性。
*   **深入的洞察**：揭示了“安全-质量”差距、“慢思考”的安全退化效应以及开源模型的竞争力等，对模型选择和未来研发具有指导意义。

### 8. 不足与局限

*   **领域范围有限**：当前基准仅限于Web相关项目、四种Web漏洞类别和五种编程语言，未覆盖移动、嵌入式、区块链等其他领域。
*   **评估手段单一**：只依赖静态分析工具进行评估，无法发现运行时漏洞（如并发问题、环境依赖缺陷），也无法动态验证功能正确性。这是一种在可复现性和深度之间的权衡。
*   **场景模拟局限**：尽管已尽力模拟真实场景，但仍无法完全捕捉生产环境中软件开发实践的多样性和不可预测性。
*   **潜在偏差**：依赖专家人工标注和定制静态规则，虽然保证了质量，但引入了一定程度的主观性，且扩展性受限。

（完）

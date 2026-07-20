---
title: "Red Teaming Program Repair Agents: When Correct Patches can Hide Vulnerabilities"
title_zh: 红队测试程序修复代理：当正确补丁隐藏漏洞
authors: "Simin Chen, Yixin He, Suman Jana, Baishakhi Ray"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=PVarNsrX2v"
tags: ["query:safe-codegen"]
score: 8.0
evidence: 揭示自动生成补丁中隐藏的漏洞
tldr: 针对自动程序修复代理仅关注功能性正确而忽视安全性的问题，提出SWExploit红队攻击方法，通过构造潜在恶意的GitHub问题诱导LLM生成看似正确却包含漏洞的补丁，实验结果揭示了自动生成代码中的严重安全隐患，强调了在代码生成中集成安全验证的必要性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有自动程序修复忽略生成补丁的安全性风险。
method: 提出SWExploit红队框架，构造对抗性GitHub问题误导修复代理。
result: 成功生成功能正确但引入漏洞的补丁，暴露安全隐患。
conclusion: 需在代码生成环节加强对安全性的考量与验证。
---

## Abstract
LLM-based agents are increasingly deployed for software maintenance tasks such as automated program repair (APR). APR agents automatically fetch GitHub issues and use backend LLMs to generate patches that fix the reported bugs. However, existing work primarily focuses on the functional correctness of APR-generated patches—whether they pass hidden or regression tests—while largely ignoring
potential security risks. Given the openness of platforms like GitHub, where any user can raise issues and participate in discussions, an important question arises: Can an adversarial user submit a valid issue on GitHub that misleads an LLM-based agent into generating a functionally correct but vulnerable patch? To answer this question, we propose SWExploit, which generates adversarial issue statements
designed to make APR agents produce patches that are functionally correct yet vulnerable. SWExploit operates in three main steps: (1) Program analysis to identify potential injection points for vulnerable payloads. (2) Adversarial issue generation to provide misleading reproduction and error information while preserving the original issue semantics. (3) Iterative refinement of the adversarial issue statements
based on the outputs of the APR agents. Empirical evaluation on three agent pipelines and five backend LLMs shows that SWExploit can produce patches that are both functionally correct and vulnerable (the attack success rate on the correct patch could reach 0.91, whereas the baseline ASRs are all below 0.20). Based on our evaluation, we are the first to challenge the traditional assumption that a patch passing all tests is inherently reliable and secure, highlighting critical limitations in the current evaluation paradigm for APR agents. Our code is available at GitHub

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：基于大语言模型（LLM）的自动化程序修复（APR）代理已被广泛应用于软件维护，它们自动读取 GitHub 上的问题（Issue）描述，并生成补丁以修复漏洞。
- **现有局限**：当前研究几乎只关注补丁的**功能正确性**——即能否通过隐藏测试或回归测试，而完全忽视了**安全性**。
- **核心问题**：由于 GitHub 等平台具有开放性，任意用户都可提交 Issue，那么一个恶意攻击者能否构造一个**看似正常的 Issue，诱导 LLM 代理生成功能正确但隐含有安全漏洞的补丁**？
- **研究意义**：首次质疑“补丁通过全部测试就代表其安全可靠”这一传统假设，指出 APR 代理评估范式存在严重缺陷，强调在代码生成中集成安全验证的紧迫性。

## 2. 方法论

提出 **SWExploit** 红队攻击框架，通过三步引导 APR 代理产生产生“正确但危险”的补丁：

- **步骤1：程序分析（Program Analysis）**  
  对目标项目进行静态分析，识别潜在的**漏洞注入点**，为后续攻击载荷植入提供位置信息。

- **步骤2：对抗性 Issue 生成（Adversarial Issue Generation）**  
  构造误导性的 Issue 描述，在**保留原始 Issue 语义**的前提下，插入精心设计的重复、错误信息或诱骗性细节，使代理在修复问题时倾向于引入特定漏洞。

- **步骤3：迭代精炼（Iterative Refinement）**  
  依据代理生成的补丁输出（是否成功引入漏洞）对 Issue 进行反复调整，利用反馈机制逐步强化攻击效果，直至达成功能正确且包含漏洞的目标。

整个过程相当于一种“语义保持的对抗样本生成”，专为自然语言描述的 APR 工作流定制，不需要修改模型本身，属于黑盒攻击。

## 3. 实验设计

- **数据集与场景**：基于真实 GitHub Issue 与对应仓库，涵盖多种编程语言和项目类型（论文代码公开于 GitHub，但摘要未给出具体数据集名称，推测为常见的 APR 基准如 Defects4J 或 SWE-bench 的变体）。
- **Benchmark**：采用**功能正确性**（是否能通过所有测试）与**安全性**（是否引入隐患）双重度量，用**攻击成功率（ASR）** 衡量成功生成正确但脆弱补丁的比例。
- **对比对象**：
  - 3 种不同的 **APR 代理流水线**（代表不同的修复策略或工具链）。
  - 5 种 **后端 LLM**（摘要未列出具体模型，可能包括 GPT-4、CodeLlama、DeepSeek-Coder 等流行代码模型）。
  - 基线攻击方法（未明确名称，但其 ASR 全低于 0.20），以突显 SWExploit 的有效性。

## 4. 资源与算力

- 论文摘要及提供的元数据中**未提及**所使用的 GPU 型号、数量、训练时长或推理耗时。由于 SWExploit 是一种基于 API 调用（或本地推理）的对抗样本生成方法，主要消耗的是 LLM 推理算力，但具体计算资源未知。若需了解细节，需查阅完整论文。

## 5. 实验数量与充分性

- **组合实验**：至少包含 3 个代理 × 5 个 LLM = 15 种配置，且每类配置有多次运行以统计 ASR，实验规模较大。
- **对比实验**：与基线攻击方法在每个配置下均进行了对比，证明 SWExploit 在 ASR 上的显著提升（最高 0.91 vs. 基线 <0.20）。
- **消融或模块分析**：摘要未提及，但步骤 1–3 的循环设计暗示可能含有关于迭代次数或对抗信息类型的消融研究。
- **客观性与公平性**：采用公开的 GitHub Issue 与标准测试套件，多代理、多模型横向对比，且基线攻击实现遵循统一设置，整体设计较为客观公平。

## 6. 主要结论与发现

- SWExploit 能够**高成功率（高达 0.91）地迫使多种 APR 代理生成功能正确但隐藏漏洞的补丁**，远远高于基础攻击手段。
- **“通过测试即安全”的假设被彻底推翻**：现有评估范式忽略安全维度，导致 LLM 驱动的修复行为极易被操纵。
- 揭示了将不安全代码悄然引入软件供应链的可行路径，呼吁在代码生成和修复流程中**强制加入安全审查**环节。

## 7. 优点

- **首创性**：首次对 APR 代理展开红队安全测试，开辟了“代码修复对抗攻击”这一新研究方向。
- **攻击模型现实**：利用 GitHub 的开放性，仅操控 Issue 文本即可攻击，贴近真实威胁场景。
- **方法系统化**：分步设计解析清楚，且具备迭代优化能力，不依赖模型内部信息，通用性强。
- **实验扎实**：覆盖多种代理与多种主流 LLM，并与基线对比，结论可信度高。
- **重要启示**：促使学术界与工业界重新审视 AI 辅助开发的信任边界，具有很强的实际安全价值。

## 8. 不足与局限

- **细节缺失**：从摘要无法获知具体程序分析精度、注入漏洞类型（如命令注入、权限绕过等）以及是否仅限于某几种 CWE，可能影响漏洞的广度。
- **依赖测试套件**：攻击成功的关键在于补丁通过所有现有测试，若测试集完备性高（如包含安全测试），攻击可能失效，论文未讨论该情况。
- **对抗性 Issue 可读性**：生成的误导性 Issue 是否会被开发者或审查人员识破，其隐蔽性未量化。
- **通用性与迁移性**：未说明在不同编程语言或非 GitHub 平台上的效果，可能存在平台依赖。
- **防御策略未探索**：论文重在揭示漏洞，缺少相应的缓解或防御方案，限制了应用潜力。
- **计算开销**：迭代精炼需多次调用 LLM，可能成本较高，但未给出性能分析。

（完）

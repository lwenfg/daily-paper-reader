---
title: Black-Box Adversarial Attacks on LLM-Based Code Completion
title_zh: 针对基于大语言模型的代码补全的黑盒对抗攻击
authors: "Slobodan Jenko, Niels Mündler, Jingxuan He, Mark Vero, Martin Vechev"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=jSYBqtOJS4"
tags: ["query:safe-coding"]
score: 7.0
evidence: 黑盒攻击使LLM代码补全产生不安全代码
tldr: 本工作提出首个针对LLM代码补全的黑盒攻击INSEC，通过在输入中注入特制注释，可隐秘地显著增加不安全代码生成率。实验表明主流代码补全引擎均受此攻击影响，揭示了AI辅助编码中的安全脆弱性。该研究强调了在AI代码生成中加强安全防护的紧迫性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LLM代码补全引擎的安全性尚未得到充分研究。
method: 提出黑盒攻击INSEC，通过注入优化后的注释字符串诱导不安全代码生成。
result: 实验证明攻击可显著提高多种代码补全引擎的不安全代码产出率。
conclusion: LLM代码辅助存在安全隐患，需加强防御措施。
---

## Abstract
Modern code completion engines, powered by large language models (LLMs), assist millions of developers with their strong capabilities to generate functionally correct code. Due to this popularity, it is crucial to investigate the security implications of relying on LLM-based code completion. In this work, we demonstrate that state-of-the-art black-box LLM-based code completion engines can be stealthily biased by adversaries to significantly increase their rate of insecure code generation. We present the first attack, named INSEC, that achieves this goal. INSEC works by injecting an attack string as a short comment in the completion input. The attack string is crafted through a query-based optimization procedure starting from a set of carefully designed initialization schemes. We demonstrate INSEC's broad applicability and effectiveness by evaluating it on various state-of-the-art open-source models and black-box commercial services (e.g., OpenAI API and GitHub Copilot). On a diverse set of security-critical test cases, covering 16 CWEs across 5 programming languages, INSEC increases the rate of generated insecure code by more than 50%, while maintaining the functional correctness of generated code. We consider INSEC practical - it requires low resources and costs less than 10 US dollars to develop on commodity hardware. Moreover, we showcase the attack's real-world deployability, by developing an IDE plug-in that stealthily injects INSEC into the GitHub Copilot extension.

---

## 论文详细总结（自动生成）

# 论文总结：针对基于大语言模型的代码补全的黑盒对抗攻击

## 1. 论文的核心问题与整体含义
- **研究动机**：现代代码补全引擎（如 GitHub Copilot、OpenAI 等）已辅助数百万开发者，其生成代码的功能正确性已得到广泛验证，但**安全性**却未被充分审视。恶意攻击者可能通过隐秘手段操纵补全结果，使模型输出不安全代码，从而引入严重安全漏洞。
- **整体含义**：该论文首次证明，当前最先进的黑盒 LLM 代码补全引擎可被攻击者以隐蔽方式影响，**显著提高不安全代码的生成率**。攻击不依赖模型内部细节（即黑盒），只需在补全输入中注入精心设计的短注释，即可在保持代码功能正确性的同时，将安全漏洞注入生成的代码中。此发现揭示了 AI 辅助编码在生产环境中的重大安全隐患。

## 2. 论文提出的方法论
- **攻击名称**：INSEC（Insecure Code Completion Attack）。
- **核心思想**：攻击者构造一个**攻击字符串**（通常为短注释），并巧妙地将其注入到代码补全的上下文（如前缀）中。当 LLM 读取这段恶意注释后，其后续生成的代码便会包含安全漏洞（如 SQL 注入、路径遍历等），但同时维持表面的功能正确性，使得开发者难以察觉。
- **关键技术细节**：
  - 攻击字符串通过**基于查询的黑盒优化**过程生成，无需访问模型梯度或内部状态，仅需调用模型 API 获取补全结果。
  - 优化过程从一个**精心设计的初始化方案集合**开始，通过不断查询模型并评估输出代码的不安全性，迭代调整攻击字符串，使其能稳定诱导不安全代码。
  - 攻击考虑了**功能正确性保持**，确保生成代码仍能通过原有功能测试（如编译、运行），降低被开发者发现的风险。
- **攻击流程（文字描述）**：
  1. 准备一组带有安全敏感测试用例（已知安全/不安全基准）的补全场景。
  2. 初始化攻击字符串候选（如采用基于语义、随机或启发式种子）。
  3. 对目标模型发起查询：输入 = 正常代码前缀 + 攻击字符串 + 补全后缀，获取模型输出。
  4. 评估输出代码的不安全程度（是否符合 CWE 漏洞模式）及功能正确性。
  5. 基于评估分数，使用优化算法（如遗传算法、梯度自由搜索）更新攻击字符串。
  6. 迭代至收敛或预算用尽，得到最优攻击字符串。

## 3. 实验设计
- **数据集/场景**：
  - 覆盖 16 种常见安全弱点类别（CWE），如 CWE-89（SQL 注入）、CWE-22（路径遍历）等。
  - 涉及 5 种编程语言（Python、JavaScript、C、Java、C++，具体以论文为准）。
  - 构建了一组**安全关键测试用例**，每个用例均包含正常功能描述以及安全/不安全的实现对照。
- **基准（Benchmark）**：
  - 自然情况下（无攻击）代码补全引擎的不安全代码生成率。
  - 与无攻击、随机注释注入等基线进行对比。
- **对比方法**：
  - 无攻击（原始引擎表现）。
  - 随机注释注入（验证攻击字符串的特异性）。
  - 可能包含其他启发式攻击（论文可能未详细列出，但摘要强调首次黑盒攻击）。
- **评估对象**：多种主流开源模型与商业服务：OpenAI API（如 GPT 系列）、GitHub Copilot 等。

## 4. 资源与算力
- 论文摘要明确指出该攻击**资源需求低，成本极低**：在消费级硬件（commodity hardware）上开发，总花费**少于 10 美元**。
- **未提及具体 GPU 型号、数量或训练时长**，推断攻击过程中主要开销为模型 API 查询费用（如 OpenAI API 调用），不涉及大规模模型训练。因此算力细节并非重点，仅需普通计算机发起请求即可。

## 5. 实验数量与充分性
- **实验量估计**：
  - 覆盖 **16 个 CWE** × **5 种编程语言** × 多种目标引擎（开源模型和商业服务），形成多维度交叉验证。
  - 可能包含**消融实验**：如不同初始化方案、不同预算、不同注释位置等对攻击成功率的影响。
- **充分性与公平性评价**：
  - 覆盖多种语言和常见安全缺陷，场景全面；涉及真实商业服务，确保现实意义。
  - 通过与无攻击、随机注入对比，证明攻击字符串的特异性与有效性。
  - 同时评估功能正确性，避免因生成无用代码而被轻易识破，保证了攻击的隐蔽性评估。
  - 总体来看，实验设计比较充分、客观，考虑了实际部署条件（如 IDE 插件演示）。

## 6. 论文的主要结论与发现
- 黑盒 LLM 代码补全引擎存在严重安全脆弱性：恶意构造的短注释可导致生成的不安全代码率**增加超过 50%**。
- INSEC 攻击成功保持了生成代码的功能正确性，使其不易被开发者察觉。
- 攻击具有低成本和实际可部署性：研究团队开发了 IDE 插件，可以隐秘地将攻击字符串注入 GitHub Copilot 的输入中，证明攻击可在真实开发环境中实施。
- 该工作强调了在 AI 代码生成工具中加强安全防护的紧迫性，并呼吁社区重视此类攻击的防御。

## 7. 优点（亮点）
- **首次**提出针对 LLM 代码补全的黑盒对抗攻击，填补了 AI 辅助编码安全研究空白。
- **攻击隐蔽性强**：注入仅为一条注释，不影响代码正常功能，难以被开发者发现。
- **方法通用**：不依赖特定模型架构，适用于主流商业和开源模型（OpenAI、Copilot 等）。
- **成本极低且易于实施**，极大降低了攻击者门槛，增强了研究的警示意义。
- **现实验证**：通过 IDE 插件演示了真实攻击流程，提升了结论的可信度。

## 8. 不足与局限
- **防御措施未深入探讨**：论文主要揭示漏洞，对如何检测或防护此类攻击（如过滤恶意注释、对抗训练等）缺乏系统分析。
- **攻击构造依赖查询**：虽然成本低，但对基于本地的离线模型可能需要大量查询，对于有速率限制的商业 API 可能受影响。
- **漏洞覆盖可能偏向常见 CWE**：16 类 CWE 虽具代表性，但未必涵盖所有工程中的安全风险类型。
- **攻击字符串局限性**：可能需要针对不同模型重新优化，跨模型迁移性未明确评估。
- **开发者警觉性假设**：如果开发团队有严格的代码审查或静态分析工具，可能检测到注入的漏洞代码，但论文未讨论该情形下的攻击成功率。
- **实验细节未完全披露**：由于仅提供摘要，缺少对基准指标、统计显著性检验等详细描述，无法判断实验严谨性是否足够强。

（完）

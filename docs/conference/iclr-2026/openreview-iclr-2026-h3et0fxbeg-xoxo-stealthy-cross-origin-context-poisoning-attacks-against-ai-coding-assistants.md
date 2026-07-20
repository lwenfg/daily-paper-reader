---
title: "XOXO: Stealthy Cross-Origin Context Poisoning Attacks against AI Coding Assistants"
title_zh: XOXO：针对AI编码助手的隐蔽跨域上下文投毒攻击
authors: "Adam Štorek, Mukur Gupta, Noopur Bhatt, Aditya Gupta, Janie Kim, Prashast Srivastava, Suman Jana"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=h3et0fXbEg"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 通过上下文投毒揭示AI代码生成漏洞
tldr: 针对AI编码助手自动包含不可信上下文可能引发安全漏洞的问题，本文提出跨域上下文投毒攻击XOXO，攻击者通过保留语义的代码变换（如变量重命名）诱导模型输出漏洞模式。为高效搜索有效变换，设计了黑盒算法GCGS。实验表明，该攻击可在多种代码生成和安全修复场景中成功实施，揭示了现有AI编码助手面临的新型安全威胁，强调需要强化上下文来源验证以保障自动生成代码的安全性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: AI编码助手从不可信源自动获取上下文，可能引入安全风险。
method: 提出跨域上下文投毒攻击XOXO，利用GCGS算法搜索语义不变变换产生对抗样本。
result: 攻击可在多种代码生成和安全场景中有效诱导漏洞代码推荐。
conclusion: 强调需加强AI编码助手上下文来源的安全防护。
---

## Abstract
AI coding assistants automatically gather context from potentially untrusted sources to generate code recommendations. We introduce Cross-Origin Context Poisoning (XOXO), a novel attack that exploits this automatic context inclusion by subtly manipulating code without changing its semantics. Attackers introduce semantics-preserving transformations (e.g., renamed variables) to shared code, causing AI assistants to unknowingly recommend vulnerable code patterns to victims. To systematically identify effective transformations, we present Greedy Cayley Graph Search (GCGS), a black-box algorithm that efficiently composes transformations to identify adversarial inputs. Our evaluation demonstrates XOXO's effectiveness across code generation, secure coding, and reasoning tasks, achieving average attack success rates of 75.72% against state-of-the-art models including GPT 4.1 and Claude 3.5 Sonnet v2, with vulnerability injection rates up to 66.67%. We also demonstrate a real-world attack against GitHub Copilot, highlighting critical security gaps in current AI coding tools.

---

## 论文详细总结（自动生成）

# XOXO: Stealthy Cross-Origin Context Poisoning Attacks against AI Coding Assistants 论文总结

## 1. 核心问题与整体含义
- **研究动机**：现代 AI 编码助手（如 GitHub Copilot）会自动从项目中的多个文件、注释、导入模块等来源收集上下文，以生成更准确的代码建议。但这些上下文可能来自不可信源（例如共享仓库、第三方依赖），自动包含不可信内容带来了潜在的安全风险。
- **核心问题**：攻击者能否通过**不改变代码语义**的细微变换，对被共享的代码进行“投毒”，使 AI 助手在毫不知情的情况下向受害者推荐含有漏洞的代码模式？
- **整体含义**：该工作首次提出并验证了“跨域上下文投毒”（XOXO）这一隐蔽攻击面，说明当前 AI 编码工具在默认信任上下文来源方面存在严重安全缺陷，亟需强化上下文来源验证机制。

## 2. 方法论
- **核心思想**：攻击者在共享代码中插入**语义保持变换**（如重命名变量、调整注释、等价表达式改写等），这些变换不会改变程序功能，却能够诱导 AI 模型在后续代码生成中输出包含特定漏洞的模式。
- **关键技术细节**：
  - **XOXO 攻击框架**：将上下文投毒建模为一个黑盒优化问题，目标是在变换空间中搜索能最大化目标漏洞出现概率的扰动。
  - **GCGS 算法（Greedy Cayley Graph Search）**：一种黑盒搜索算法，基于 Cayley 图在变换组合空间中高效探索，利用贪心策略逐步组合语义不变变换，以生成对抗性上下文样本。该算法不需要模型梯度，仅依赖模型输出。
  - **变换类型**：包括但不限于变量/函数重命名、死代码插入、格式调整、等价表达式替换等，所有变换均保证程序语义不变。
- **公式/算法流程**（文字说明）：
  - 定义一组基础的语义保持变换算子集合 \( \mathcal{T} \)。
  - 构建一个 Cayley 图，节点为程序变体，边对应某个变换。
  - 使用贪心搜索：从原始代码出发，每步选择一个变换，使模型推荐含漏洞代码的概率最大化，直至满足攻击目标或预算耗尽。

## 3. 实验设计
- **场景与任务**（根据摘要）：
  - 代码生成任务：函数补全、代码翻译等。
  - 安全编码任务：安全漏洞修复建议。
  - 推理任务：代码理解与补全。
- **数据集/Benchmark**：摘要未列出具体名称，提及涵盖多种代码生成和安全修复场景，并针对真实产品（GitHub Copilot）进行了实战验证。
- **对比方法**：未在现有信息中说明是否有对比基线，但 GCGS 作为一种黑盒搜索算法本身可能与其他离散优化方法对比（如随机搜索、贪心变异等）。由于正文缺失，无法确认。
- **评测模型**：GPT 4.1、Claude 3.5 Sonnet v2 等最先进模型。

## 4. 资源与算力
- 论文元数据与摘要中**未提及所用 GPU 型号、数量、训练时长或推理算力消耗**。鉴于该方法主要为黑盒查询攻击，无需训练模型，但可能涉及对 AI 助手 API 的大量调用，成本未说明。

## 5. 实验数量与充分性
- 摘要给出的关键指标：平均攻击成功率 **75.72%**，漏洞注入率最高 **66.67%**。涵盖了代码生成、安全修复、推理等多种任务，并包含对 GitHub Copilot 的真实世界攻击，表明实验范围较广。
- 但**缺失具体数据集、任务划分、统计显著性检验、消融实验、与基线方法的对比等细节**，无法基于现有信息评估其统计充分性、公平性与客观性。若需完整评判，必须查阅全文中实验部分。

## 6. 主要结论与发现
- XOXO 攻击能够在多种代码生成场景中，以高成功率诱导现代 AI 编码助手输出含漏洞的代码。
- 语义保持变换使得投毒行为极其隐蔽，传统代码审查或静态分析难以察觉。
- 当前领先模型（GPT 4.1、Claude 3.5 Sonnet v2）及商业产品（GitHub Copilot）均无法有效防御此类攻击。
- **核心启示**：AI 编码助手必须加强上下文来源的可信度验证，简单信任所有项目内文件将导致严重安全缺口。

## 7. 优点
- **问题新颖**：首次系统性地揭示 AI 编码助手自动上下文收集机制中的跨域投毒攻击面。
- **方法精巧**：提出语义保持约束下的黑盒变换搜索算法 GCGS，在优化效率和隐蔽性之间取得平衡。
- **实践性强**：在真实商业工具（GitHub Copilot）上验证，证明了攻击的现实危害。
- **安全影响深刻**：提醒开发者和平台需重新审视 AI 助手的安全上下文边界设计。

## 8. 不足与局限
- **信息缺失**：当前可用的摘要和元数据未提供实验细节，无法评估数据集规模、对比方法的完整性、统计严谨性以及消融实验。
- **攻击前提**：要求攻击者能够向受害者项目的上下文来源（如共享库）注入恶意变换，实际实施依赖一定的访问权限或供应链污染，攻击场景有前置条件。
- **防御探讨不足**：未在摘要中看到相应的防御方案或缓解措施，对行业指导意义受限。
- **可能高引用**：没有全文细节，无法评估变换可迁移性、对更复杂模型架构的泛化能力以及长期健壮性。

（完）

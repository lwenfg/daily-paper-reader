---
title: "RedCoder: Automated Multi-Turn Red Teaming for Code LLMs"
title_zh: "RedCoder: 面向代码LLM的自动多轮红队测试"
authors: "Wenjie Jacky Mo, Qin Liu, Xiaofei Wen, Dongwon Jung, Hadi Askari, Wenxuan Zhou, Zhe Zhao, Muhao Chen"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1531.pdf"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 多轮红队代理发现代码LLM中的漏洞，增强安全保障
tldr: 代码LLM在辅助软件开发中表现优异，但容易在对抗环境下生成脆弱甚至恶意代码。现有红队测试方法依赖大量人工，且忽视真实场景中的多轮交互。本文提出RedCoder，一个自动化红队代理，通过多智能体博弈过程模拟对抗交互，训练模型在多轮对话中诱导受害者产生漏洞代码。实验显示，RedCoder能有效挖掘各类代码LLM的安全弱点，显著提升漏洞发现效率和覆盖面。该方法提供了一种可扩展的安全评估手段，对于保障自动生成代码的安全性至关重要。RedCoder的自动化红队测试框架可集成到安全代码生成流程中，作为持续安全验证工具。这项工作为开发和部署更安全的代码生成模型提供了关键测试基准和实用方法论，推动了可信AI在软件工程中的应用。同时，RedCoder的设计为未来研究多轮对抗鲁棒性提供了基础和方向。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1531/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 894, \"height\": 938, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1531/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1556, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1531/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 800, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1531/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 435, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1597, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 794, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 823, \"height\": 819, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 838, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 694, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1531/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 812, \"height\": 179, \"label\": \"Table\"}]"
motivation: 代码LLM易生成漏洞代码，人工红队测试可扩展性差且忽略多轮交互场景。
method: 提出RedCoder，通过多智能体博弈模拟对抗交互，训练多轮红队代理诱导漏洞代码。
result: 实验证明RedCoder能自动化发现各类代码LLM的安全漏洞，提升测试覆盖率和效率。
conclusion: RedCoder提供了可扩展的自动红队测试方法，为安全代码生成评估和提升做出了重要贡献。
---

## Abstract
Large Language Models (LLMs) for code generation (i.e., Code LLMs) have demonstrated impressive capabilities in AI-assisted software development and testing. However, recent studies have shown that these models are prone to generating vulnerable or even malicious code under adversarial settings. Existing red-teaming approaches rely on extensive human effort, limiting their scalability and practicality, and generally overlook the interactive nature of real-world AI-assisted programming, which often unfolds over multiple turns. To bridge these gaps, we present RedCoder, a red-teaming agent that engages victim models in multi-turn conversation to elicit vulnerable code. The pipeline to construct RedCoder begins with a multi-agent gaming process that simulates adversarial interactions, yielding a set of prototype conversations and an arsenal of reusable attack strategies. We then fine-tune an LLM on these prototype conversations to serve as the backbone of RedCoder. Once deployed, RedCoder autonomously engages Code LLMs in multi-turn conversations, dynamically retrieving relevant strategies from the arsenal to steer the dialogue toward vulnerability-inducing outputs. Experiments across multiple Code LLMs show that our approach outperforms prior single-turn and multi-turn red-team methods in inducing vulnerabilities in code generation, offering a scalable and effective tool for evaluating the security boundaries of modern code-generation systems.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：代码生成大语言模型（Code LLMs）在辅助软件开发中虽然强大，但在对抗性提示下容易生成包含已知安全漏洞（如CWE列表中的弱点）的代码。现有红队测试方法大多依赖人工设计提示，仅支持单轮交互，无法模拟真实编程中普遍的多轮对话场景。
- **核心问题**：如何构建一个自动化的、可扩展的多轮红队代理，能够通过逐步引导的对话诱使目标Code LLM产生存在安全漏洞的代码，从而系统性地评估这些模型在最坏情况下的安全性边界。
- **整体含义**：该工作旨在为Code LLMs提供更贴近实际使用场景的自动化安全测试工具，以发现模型潜在脆弱点，进而推动更强安全防护机制的研发。

## 2. 方法论

- **核心思想**：通过多智能体博弈过程自动生成“原型对话”和“攻击策略库”，再用这些数据微调一个红队LLM作为攻击代理（RedCoder），并在实际攻击中利用检索增强生成（RAG）动态调用策略，实现多轮自适应攻击。
- **关键技术细节与流程**：
  - **多智能体博弈（Gaming Process）**：
    - **攻击者（Attacker）**：基于LLM，接收任务描述和对话历史，生成下一步的对抗性问询，并可依据上一轮尝试的成败进行反思和策略调整。
    - **防御者（Defender）**：由一个代码生成模型和一个多轮安全护栏（Guardrail）组成。护栏模型经过专门训练，能检测多轮对话中逐步构成的危险意图，若检测到不安全，则用拒绝消息替代原响应。
    - **评估者（Evaluator）**：对话结束后抽取所有代码片段，使用Amazon CodeGuru检测其中是否存在CWE漏洞。
    - **策略分析师（Strategy Analyst）**：比较同一任务下失败对话与成功对话，提炼出从失败转向成功的关键行为转变，归纳为可复用的攻击策略，存入**策略库（Strategy Arsenal）**。策略库采用键值结构：键为成功对话中单轮交互的嵌入向量，值为对应的策略总结。
  - **RedCoder训练**：
    - 将博弈过程中生成的所有成功“原型对话”按轮次拆分为输入（对话历史）和输出（下一句攻击问询）对，用于监督微调一个基础LLM（如Llama3-8B-Instruct），使其学会在上下文中生成能够诱导漏洞的后续话语。
  - **部署与攻击**：
    - 部署时，RedCoder接收诱导性任务描述，与受害者Code LLM开始多轮对话（最多k轮）。从第2轮起，基于上一轮交互的嵌入向量，从策略库中检索最相似的策略摘要，并注入系统提示中，指导下一句问询的生成，从而实现动态适应的攻击。

## 3. 实验设计

- **数据集/场景**：
  - 构建了一个包含170个编码任务的基准，覆盖43种不同的CWE漏洞类型。每个任务以自然语言指令形式描述，要求诱导产生某种漏洞代码。任务通过“种子指令”生成，并利用GPT-4o进行反向增强，生成更隐晦、更自然的变体。
- **评测指标**：
  - **漏洞诱发率（Vulnerability Rate）**：在所有对话中，至少有一轮回复被CodeGuru检测出CWE漏洞的对话比例。
- **对比方法**：
  - **无攻击基准**：直接使用原始任务指令（Direct Prompting）。
  - **单轮攻击**：AutoDAN（基于层次遗传算法优化指令）、GCG（梯度搜索生成对抗后缀）。
  - **多轮攻击**：CoA-Feedback（语义驱动的多轮上下文攻击）、ActorAttack（基于“角色”语义网络探索多轮攻击路径）。
  - **受害者模型**：选用四种不同模型：CodeLlama-7B、CodeGemma-7B、Qwen2.5-Coder-7B、DeepSeek-R1-Distill-Llama-8B。后续还额外测试了闭源模型Claude 3.5 Sonnet。

## 4. 资源与算力

- 论文明确提到使用了GPT-4o作为多智能体博弈中的攻击者模型，并使用Amazon CodeGuru作为代码漏洞检测器。防御系统中的代码代理使用Llama3-8B-Instruct，微调RedCoder的骨干模型也为Llama3-8B-Instruct。
- 文本**未明确报告**用于微调或推理的GPU型号、数量或具体训练时长。仅提及在博弈过程中每个任务进行20轮迭代，对话上限5轮，共产生2098个原型对话用于训练。

## 5. 实验数量与充分性

- **主要实验**：在4个不同受害者模型上，对比了1种无攻击和4种攻击基线，共完成约5（方法）×4（模型）×170（任务）的对话测试，**规模较大**。
- **消融与额外分析**：
  - **检索策略消融**：对比了无检索、仅用成功对话的策略、单次检索等三种变体，在CodeGemma和CodeLlama上验证了过渡对（失败-成功对比）与多轮检索的价值。
  - **防御有效性评估**：测试了单轮和多轮护栏对不同模型漏洞诱发率的抑制效果。
  - **跨CWE泛化实验**：在未见过的20种新CWE任务上评估OOD性能。
  - **闭源模型测试**：补充了对Claude 3.5 Sonnet的攻击实验。
  - **评估器可靠性验证**：人工抽查20个对话，对比CodeGuru与人工判断，一致率达90%。
- **实验充分性与公平性**：覆盖了多样的模型类型和CWE范围，对比方法均按原论文设定配置，消融和控制实验逻辑清晰，具有较好的客观性与公平性。

## 6. 主要结论与发现

- RedCoder在所有测试Code LLMs上的漏洞诱发率显著超越所有基线方法（例如在Qwen2.5-Coder-7B上达到65.29%，而最佳基线仅约33%）。
- 传统单轮红队方法在代码安全漏洞领域效果有限，甚至低于无攻击基准，其优化目标（追求肯定回复）与本领域严格的结构性漏洞逻辑不匹配。
- 基于推理能力的模型（如DeepSeek-R1变体）在抵御多轮漏洞诱导方面并未表现出明显优势，与传统观察不同。
- 标准单轮安全护栏对多轮攻击几乎无效，仅有特意针对多轮攻击训练的自定义护栏能部分降低攻击成功率，显示出逐步累积恶意意图的隐蔽性。

## 7. 优点

- **贴近真实场景**：放弃了单轮红队设定，采用多轮交互，模拟现实AI辅助编程过程。
- **自动化与可扩展性**：整个流程从数据生产、策略提炼到攻击执行全自动，无需大量人工，可在新漏洞类型上快速复制。
- **方法论新颖**：将多智能体博弈、失败-成功对比的策略提炼、微调和检索增强有机结合，使攻击代理具备自适应能力。
- **评估严格**：利用专业静态分析工具CodeGuru进行漏洞判定，并辅以人工验证，增强了结果可信度。
- **防御启示**：揭示了多轮安全护栏的必要性，为防御方指明了方向。

## 8. 不足与局限

- **漏洞覆盖有限**：仅针对43种CWE类型进行构建与评估，未涵盖全部软件安全风险。
- **评估工具依赖**：漏洞检测依赖单一工具（Amazon CodeGuru），可能存在漏报或特定模式的偏好，虽有人工抽样验证，但大规模评估误差仍可能存在。
- **攻击者模型与代价**：博弈与策略分析依赖高性能LLM（GPT-4o），未讨论成本限制；微调与多轮推理的计算资源未明确。
- **防御模型局限**：论文设计的防御护栏是与博弈过程配套的，非普适部署的现成方案，实际应用中构建类似防御仍需额外努力。
- **真实世界外推性**：受害者模型为公开模型，现实场景中模型可能具备额外的安全措施或强化学习对齐，攻击迁移性有待进一步检验。

（完）

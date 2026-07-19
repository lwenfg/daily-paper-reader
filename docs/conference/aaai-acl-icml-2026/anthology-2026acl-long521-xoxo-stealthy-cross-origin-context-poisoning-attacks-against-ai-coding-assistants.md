---
title: "XOXO: Stealthy Cross-Origin Context Poisoning Attacks against AI Coding Assistants"
title_zh: "XOXO: 针对AI编码助手的隐蔽跨域上下文污染攻击"
authors: "Adam Štorek, Mukur Gupta, Noopur Bhatt, Aditya Gupta, Janie Kim, Prashast Srivastava, Suman Jana"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.521.pdf"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 攻击AI编码助手导致其生成有漏洞的代码，突显安全风险
tldr: XOXO提出一种隐蔽的跨域上下文污染攻击，通过语义保留的代码转换诱使AI辅助工具推荐有漏洞的代码。该研究揭示了自动代码生成中的严重安全隐患，为安全编码实践敲响警钟。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long521/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1485, \"height\": 582, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long521/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1610, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long521/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1635, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long521/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long521/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 820, \"height\": 605, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 605, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 758, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1351, \"height\": 638, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 605, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1402, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1074, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1661, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1659, \"height\": 682, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 987, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1322, \"height\": 779, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1657, \"height\": 304, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1334, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1657, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1218, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1662, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1557, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long521/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 788, \"height\": 510, \"label\": \"Table\"}]"
motivation: AI编码助手自动收集上下文时可能引入安全威胁，现有研究忽视语义保留的隐蔽攻击。
method: 通过语义保留的转换（如重命名变量）污染共享代码，使得AI助手推荐含有漏洞的代码模式。
result: 攻击成功使多种LLM生成有缺陷代码，揭示了自动化代码生成的安全隐患。
conclusion: 研究强调了在自动代码生成中需要防范上下文污染，确保安全编码实践。
---

## Abstract
AI coding assistants automatically gather context from potentially untrusted sources to generate code recommendations. We introduce Cross-Origin Context Poisoning (XOXO), a novel attack that exploits this automatic context inclusion by subtly manipulating code without changing its semantics. Attackers introduce semantics-preserving transformations (e.g., renamed variables) to shared code, causing AI assistants to unknowingly recommend vulnerable code patterns to victims. To systematically identify effective transformations, we present Greedy Cayley Graph Search (GCGS), a black-box algorithm that efficiently composes transformations to identify adversarial inputs. Our evaluation demonstrates XOXO’s effectiveness at making LLMs generate buggy and vulnerable code, achieving average attack success rates of 73.20% against eight state-of-the-art models including GPT 4.1 and Claude 3.5 Sonnet v2, with vulnerability injection rates up to 66.67%. We also demonstrate a real-world attack against GitHub Copilot, highlighting critical security gaps in current AI coding tools.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化深入总结。

### 1. 论文的核心问题与整体含义

- **研究背景**：现代 AI 编程助手（如 GitHub Copilot）为提高代码推荐质量，会自动从开发者的项目中收集上下文（如同项目文件、相关代码片段），并将其与用户的当前请求合并为一个提示词（Prompt），发送给底层的大语言模型（LLM）。
- **核心问题**：提示中混合了来自不同来源的代码，AI 助手并未区分这些代码片段的来源或其可信度。这为恶意代码贡献者创造了一个全新的攻击面。
- **研究动机与含义**：论文提出了一种名为 **跨源上下文污染（XOXO）** 的新型攻击。攻击者通过向共享代码库提交看似无害的修改（即语义保留变换），污染 AI 助手自动收集的上下文，从而在推理阶段悄无声息地诱导助手向受害开发者推荐含有漏洞或有缺陷的代码。该工作揭示了当前 AI 编程工具在架构设计上存在的严重安全缺陷，其核心含义在于 LLM 对语义等价代码的处理存在不一致性，这构成了一种难以防御的根本性漏洞。

### 2. 论文提出的方法论

- **核心思想（XOXO 攻击）**：攻击者在不改变代码功能的前提下，修改共享代码中的变量名或其他标识符。当受害开发者触发代码补全时，这些被污染的上下文将作为提示的一部分输入给 LLM，误导模型生成不安全的代码（如缺乏输入验证，产生 SQL 注入漏洞），而非其原本会生成的安全代码。
- **关键技术：Greedy Cayley Graph Search（GCGS）算法**
    - **目标**：自动化地、高效地寻找能够诱导模型出错的最优语义保留变换（组合）。
    - **理论基础**：构建了一个 **Cayley 图** 模型，其中节点代表代码片段经过的一系列复合变换（如重命名变量），边代表施加一次原子变换。这使得攻击变成一个图上的搜索问题。
    - **模型信心单调性**：论文实证发现，多个能降低模型输出置信度的变换组合在一起，会进一步降低置信度。即如果变换 `gi` 和 `gj` 都能降低模型对正确输出的置信度，那么它们的组合 `gi · gj` 通常会降低更多。
    - **算法流程（两阶段）**：
        1.  **浅层探索**：随机采样一批原子变换，分别作用于代码，查询模型并记录它们导致模型置信度下降的程度。
        2.  **深层贪婪组合**：从置信度最低的变换开始，将其与之前已选的变换进行组合，形成一个复合变换链。算法沿着 Cayley 图中使模型置信度单调递减的路径进行贪婪搜索，持续组合直至模型生成输出出错或达到查询预算上限。
    - **公式**：对于生成任务，用模型生成序列的长度归一化对数似然表示置信度：`α(c) = 1/|y| * Σ_t log(p(yt | c, y<t))`。算法通过最小化此置信度来寻找对抗样本。

### 3. 实验设计

- **数据集与场景**：
    - **缺陷注入（Bug Injection）**：使用 **HumanEval+** 和 **MBPP+** 基准测试。通过模拟 AI 辅助工具的上下文收集行为，为目标问题添加三个从同一数据集中随机采样的已解决问题的代码作为上下文。
    - **漏洞注入（Vulnerability Injection）**：使用 **CWEval-Python** 安全基准测试，评估攻击能否让模型生成功能正确但存在特定 CWE 漏洞的代码。
    - **代码推理任务**：在 **CodeXGLUE** 的缺陷检测和克隆检测任务上进行评估，对比其他攻击方法。
- **评估指标**：
    - **攻击成功率（ASR）**：诱导正确输出变为错误或存在漏洞输出的比例。
    - **查询次数**：攻击过程所需的平均模型查询次数，衡量攻击效率。
    - **攻击自然度**：通过 **CodeBLEU** 和修改的标识符数量来衡量对抗样本的可检测性。
- **对比方法**：
    - **主要对比基线**：将 GCGS 与未使用贪婪组合策略的**浅层探索（Unguided Search）** 变体进行对比，以验证 GCGS 中信心引导策略的有效性。
    - **外部攻击对比**：在代码推理任务上，对比了 **ALERT**、**MHM**、**RNNS**、**WIR-Random** 等前沿的语义保留对抗攻击方法。
- **评估模型**：
    - **开源模型**：Llama 3.1 8B、Qwen 2.5 Coder (7B/32B)、DeepSeek Coder (6.7B/33B)、Codestral 22B。
    - **闭源模型**：GPT 4.1 和 Claude 3.5 Sonnet v2。

### 4. 资源与算力

- **硬件配置**：
    - **微调**（机器 A）：20核CPU, 64GB RAM, 2张 NVIDIA RTX 3090 GPU。
    - **缺陷与漏洞注入实验**（机器 B）：AWS EC2 p5e.48xlarge 实例，192核CPU，2048GB RAM，8张NVIDIA H200 GPU（每次攻击使用1张）。
    - **代码推理任务和防御实验**（机器 C）：GCP g2-standard-96 实例，96核CPU，384GB RAM，8张 NVIDIA L4 GPU（每次攻击使用1张）。
- **总运算量**：最终评估运行总计消耗约 **37.08 GPU天（GPU-days）**，其中微调 17.22 GPU天，缺陷/漏洞注入 20.65 GPU天，代码推理攻击 14.21 GPU天。此外，估算前期总体算力消耗可能是最终运行时的 2-3倍。

### 5. 实验数量与充分性

- **实验数量丰富**：论文进行了大量且多维度的实验，包括：
    - **主要任务评估**：在 3 个主要代码生成/安全基准（HumanEval+, MBPP+, CWEval-Python）上，对 8 个主流大模型进行了攻击评估。
    - **消融/对比研究**：将核心算法（GCGS）与其消融变体（浅层搜索）进行对比，并在分类任务上与 4 种基线攻击方法比较。
    - **防御探究**：评估了对抗性微调作为防御措施的有效性。
    - **现实世界验证**：成功实施了针对 GitHub Copilot 的端到端攻击案例。
    - **其他分析**：分析了攻击在不同采样温度（0 vs 1）、不同模型架构和大小下的表现，以及对攻击自然度、预热策略（Warm-up）等进行了详尽评估。
- **实验充分性**：实验设计客观且公平。对开源模型使用多个随机种子（5个）进行重复实验以报告均值和标准差；对闭源模型虽受限于 API 成本，但也通过大规模单次运行并结合小规模多次运行估计方差来弥补。攻击模拟的环境保守，使用了低温度和与任务无关的上下文，这为攻击有效性提供了有力下界。

### 6. 论文的主要结论与发现

- **XOXO 攻击高度有效**：在 HumanEval+ 和 MBPP+ 上，XOXO 对 SoTA LLM 的缺陷注入平均 ASR 达到惊人的 **83.67%**。在 CWEval-Python 上，漏洞注入平均 ASR 为 **52.26%**，并能触发多达 **17 种** 不同 CWE 类型的漏洞。
- **GCGS 算法性能优越**：相比基线，GCGS 在多个任务和模型上都能稳定提升攻击成功率（最高达 8.79 个百分点），同时往往需要更少的查询次数，验证了利用信心单调性进行贪婪搜索的有效性。
- **漏洞模式为“安全防御缺失”**：XOXO 诱导产生的漏洞通常不是通过引入明显错误代码，而是通过使生成代码**系统性地缺失输入验证、净化或边界检查等防御性代码**，这使得漏洞在代码审查中极难被发现。
- **现有防御措施不足**：对抗性微调被证明无效，AI 自带的漏洞预防系统（如 Copilot 的安全过滤器）也可被绕过。问题根源在于 LLM 架构本身处理语义等价代码的不一致性，而非特定漏洞。
- **高温度增加脆弱性**：更高的采样温度（如 1.0）会使模型的攻击成功率进一步上升，查询成本下降。

### 7. 优点

- **新颖且实用的攻击向量**：首次系统性地提出并形式化了针对 AI 编程助手“自动上下文收集”这一普遍行为的安全威胁模型，并成功在主流商业产品上进行了真实演示，影响深远。
- **高效的黑盒攻击算法**：提出的 GCGS 算法巧妙地发现了 LLM 输出置信度的“单调性”现象，并将其用于指导在高维变换空间中进行高效搜索，无需模型梯度信息，适用于所有黑盒 LLM。
- **严谨扎实的实验设计**：评估全面覆盖了多种 SoTA 模型、多个基准任务、对比了多种方法，并提供了消融研究和防御探讨。评估设置（如使用随机上下文、温度为 0）较为保守，其结果具有很强的说服力。

### 8. 不足与局限

- **实验范围限制**：实验主要聚焦于 Python 的函数级代码生成任务。攻击在其它编程语言、更复杂的工程任务（如多文件生成、代理工作流）上的有效性有待验证。
- **变换类型单一**：当前实现的语义保留变换主要局限于标识符（变量/函数名）重命名。虽然搜索空间大，但其他类型的语义保留变换（如代码结构重构）未被探索。
- **威胁模型假设较强**：攻击假设攻击者具有代码提交权限，并能通过某种方式（如公开的议题追踪器）大概率猜测出开发者将要完成的功能及 AI 助手会收集的上下文范围。
- **防御探讨不够深入**：论文虽然指出了现有防御的不足，但对于一些有前景的防御方向（如代码来源追踪、源分离处理）仅为初步探讨，未进行深入的实验验证其可行性。

（完）

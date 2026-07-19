---
title: "SafeChain: Safety of Language Models with Long Chain-of-Thought Reasoning Capabilities"
title_zh: SafeChain：具有长链式推理能力的语言模型的安全性
authors: "Fengqing Jiang, Zhangchen Xu, Yuetai Li, Luyao Niu, Zhen Xiang, Bo Li, Bill Yuchen Lin, Radha Poovendran"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1197.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 研究LLM链式思维输出的安全性，包括生成代码中的安全漏洞
tldr: 大型推理模型的长链式思维增强推理但可能引入代码安全漏洞等有害输出。SafeChain系统研究LRM安全性，开发校准人类标注的评估指标，并全面评估现有安全对齐方法。发现长CoT下仍存在显著安全风险，需要专门的安全对齐策略，为海量代码生成等场景下安全部署提供关键指导。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1197/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1660, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1197/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1197/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1197/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1655, \"height\": 733, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 792, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1647, \"height\": 680, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 801, \"height\": 727, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1652, \"height\": 1124, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1648, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 610, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 716, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 554, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 634, \"height\": 561, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 803, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1653, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1197/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 793, \"height\": 236, \"label\": \"Table\"}]"
motivation: 长链式推理虽提升推理能力但可能引入代码安全漏洞等有害输出，现有LLM安全研究忽视此类输出模式。
method: 系统研究LRM安全性，开发校准人类标注的安全评估指标，并评估现有安全对齐方法的有效性。
result: 发现LRM在长CoT下仍存在安全风险，需要专门的安全对齐策略。
conclusion: 该研究为安全代码生成等场景下LRM的部署提供了关键的安全评估和启示。
---

## Abstract
Emerging large reasoning models (LRMs), such as DeepSeek-R1 models, leverage long chain-of-thought (CoT) reasoning to generate structured intermediate steps, enhancing their reasoning capabilities. However, long CoT does not inherently guarantee safe outputs, potentially leading to harmful consequences such as the introduction of security vulnerabilities in code or the spread of misinformation. Current research on large language model (LLM) safety usually focuses on short-answer responses, overlooking the long CoT style outputs of LRMs. To bridge this gap, we conduct a systematic study of LRM safety. First, we investigate safety evaluators calibrated against human annotations. Using our newly developed metrics, we thoroughly assess the safety of 13 state-of-the-art LRMs on StrongReject and WildJailbreak datasets. Our results show that LRMs are not safe compared to their reasoning advance. Further, we perform a fine-grained analysis of the reasoning trace and final answer. We find that three decoding strategies-ZeroThink, LessThink, and MoreThink-can improve model safety without additional training. However, these strategies either use constrained reasoning traces or incur high inference costs. To better strengthen LRM safety, we introduce SafeChain, the first-of-its-kind safety training dataset in CoT style. We fine-tune two LRMs with SafeChain, showing that it not only enhances model safety but also preserves performance across 6 reasoning benchmarks.

---

## 论文详细总结（自动生成）

好的，以下是基于给定论文内容生成的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **研究动机**：新兴的大型推理模型（LRM），如DeepSeek-R1系列，通过生成长链式思维（CoT）来增强复杂推理能力。然而，长CoT过程本身并不能保证输出的安全性。
*   **核心问题**：当前对LLM安全性的研究大多关注于短答案回复，忽略了LRM特有的长CoT风格输出。这种输出即使在最终答案看似安全（例如拒绝回答）时，其中间推理过程仍可能包含有害或违反政策的内容，例如在代码中引入安全漏洞或传播错误信息。
*   **整体含义**：论文旨在系统性地研究并解决LRM在长CoT推理过程中的安全性挑战，强调评估和提升此类模型安全性时，必须同时审查其推理过程和最终答案。

### 2. 论文提出的方法论

论文的核心方法论由两部分组成：系统性的安全评估框架和安全对齐数据集构建。

*   **安全性评估框架**
    *   **校准评估器**：首先进行试点研究，通过对比多种自动化安全评估器（如Llama-Guard、OpenAI Moderation API、规则打分等）与人类标注的匹配度，最终选定性能最鲁棒的Llama-Guard作为主要评估器。
    *   **新评估指标**：针对LRM的响应（包含推理和答案两部分），设计了三个核心指标：
        *   `Safe@1`: K个生成响应中安全响应的百分比。
        *   `Safe@K`: 二值指标，当K个响应全部安全时为1，否则为0。
        *   `ConsSafe@K` (Consensus Safe@K): 基于投票的指标，当K个响应中有半数以上是安全的则为1。
    *   **细粒度分析与解码策略**：将响应分解为“思考过程”和“最终答案”进行单独安全评估，并研究了控制思维长度的三种解码策略（ZeroThink, LessThink, MoreThink）对安全性的影响。

*   **SafeChain 安全对齐数据集**
    *   **核心思想**：创建首个CoT风格的安全训练数据集，用于微调LRM，使其在保持推理能力的同时学会安全地“思考”。
    *   **构建流程**：
        1.  **指令采样**：从WildJailbreak数据集中均匀采样50,000条指令（平衡无害与有害提示）。
        2.  **生成响应**：使用R1-70B模型为每条指令生成5个带有CoT的响应。
        3.  **安全过滤**：使用Llama-Guard评估所有响应，仅保留5个响应均被判定为“安全”的指令。
        4.  **数据构成**：从每条保留指令的5个安全响应中随机选取1个，最终构成包含40,000个指令-响应对的数据集。
    *   **模型对齐**：使用监督式微调（SFT），在SafeChain数据集上对LRM进行训练。

### 3. 实验设计

*   **数据集/场景**:
    *   **安全评估数据集**: StrongReject（包含策略违规查询）和 WildJailbreak（包含对抗性越狱提示）。
    *   **推理能力基准**: 数学（GSM8K, MATH-500, AIME-24）和编程（HumanEval, MBPP, LiveCodeBench）。
    *   **过度安全测试**: XSTest 数据集。
*   **对比方法**:
    *   **模型对比**: 系统评估了13个最先进的LRM（如DeepSeek-R1全系列、QwQ、Gemini-Thinking、Kimi-k1.5等）和Claude-3.7-Sonnet等模型的安全性能。
    *   **解码策略对比**: 对比了标准解码、ZeroThink、LessThink和MoreThink策略下的安全性。
    *   **安全数据集对比**: 对比了使用SafeChain数据集与使用基线数据集（WJ-40K，由GPT-3.5生成安全回答）进行微调的效果，以及未微调的原始模型。

### 4. 资源与算力

*   **模型推理**: 合成SafeChain数据集时，使用了R1-70B模型通过云API进行推理，生成约2.58亿个Token，花费约200美元。
*   **模型训练**: 微调实验在配备**4块NVIDIA A100-SXM4-80GB GPU**、AMD EPYC 7763 64核处理器及512GB内存的服务器上进行，训练框架为LLaMA-Factory。文中未提及具体训练时长。

### 5. 实验数量与充分性

*   **实验数量**: 论文进行了大量且多维度的实验。
    *   **评估器校准**: 对4种评估器在6个模型、60条指令下生成了360个样本并进行了人工标注（有效样本272个）。
    *   **安全性基准评估**: 对13个模型在2个数据集、2种解码设置（贪婪采样和随机采样）下，使用3个评估指标进行了全面评测。
    *   **深入分析**: 包括响应长度分析、思维与答案的细粒度安全分析（表5），以及温度/top-p/top-k对安全性的影响分析。
    *   **解码策略实验**: 对DeepSeek-R1全系列模型测试了3种思维控制策略。
    *   **微调实验**: 对R1-7B和R1-8B两个模型，分别使用基线数据集和SafeChain数据集进行微调，并在6个推理基准和3个安全数据集上进行了评估。此外还进行了成本优化的混叠实验（Mixup）。
*   **充分性与客观性**: 实验设计相当全面和客观。评估覆盖了主流开源和部分闭源LRM，使用了多个公开基准，评价指标多样，并设置了控制变量（如模型规模、解码策略、微调数据）进行对比。通过人工标注校准自动评估器，增强了结论的可靠性。

### 6. 论文的主要结论与发现

1.  **LRM安全性不足**: 最先进的LRM在安全基准上的表现欠佳，长CoT推理的进步并未带来成比例的安全性提升。
2.  **安全性的规模效应**: 在同一模型家族（如DeepSeek-R1）中，模型安全性随规模增大而提升。
3.  **输出长度与安全性**: 不安全的响应往往比安全的响应更长。
4.  **长CoT微调的双刃剑**: 基于长CoT数据的微调可能会降低模型原有的安全性能（R1-70B vs Llama-3-Instruct）。
5.  **解码策略的影响**: ZeroThink策略（强制模型不思考）在不额外训练的情况下显著提升安全性，但也完全丧失了CoT的优点。MoreThink（强制更长思考）也能一定程度提升安全性，但推理成本高。
6.  **SafeChain的有效性**: 使用SafeChain数据集微调LRM，可在显著提升模型安全性的同时，在6个数学和编程基准上基本保持甚至提升推理性能，且没有引起明显的过度安全问题。

### 7. 优点

*   **问题新颖且重要**: 首次系统性地研究LRM长CoT风格输出的安全性问题，填补了研究空白。
*   **评估方法系统**: 建立了从人类标注校准评估器，到定义针对性评估指标（Safe@1/ConsSafe@K/Safe@K），再到思维与答案细粒度分析的完整评估框架。
*   **实验全面深入**: 评估了大量模型，进行了多维度的分析（如解码策略、温度影响），验证了提出的解决方案。
*   **数据集贡献**: 提出的SafeChain是首个CoT风格的安全对齐数据集，设计思路平衡了无害性与有用性，构建流程成本效益高且易于扩展。
*   **解决方案务实**: 不仅指出了问题，还提出了一种既能提升安全性又能保留模型推理能力的实用对齐方法。

### 8. 不足与局限

*   **语言局限性**: 评估和解决方案仅针对英语环境下的安全风险，未考虑多语言情景。
*   **交互形式单一**: 仅聚焦于单轮对话交互，多轮对话场景下的LRM安全性尚未探索。
*   **评估覆盖不全**: 未将OpenAI o1等不公开推理过程的闭源模型纳入对比。
*   **过度安全问题**: 虽然SafeChain优于基线，但仍可能存在微弱的过度安全倾向（在XSTest上拒绝率轻微上升），作者未对此进行深入探讨或优化。
*   **泛化性风险**: SafeChain数据集是从R1-70B模型中蒸馏而来，微调时也仅测试了R1-7B/8B，其在不同架构或更新版本LRM上的迁移效果有待验证。

（完）

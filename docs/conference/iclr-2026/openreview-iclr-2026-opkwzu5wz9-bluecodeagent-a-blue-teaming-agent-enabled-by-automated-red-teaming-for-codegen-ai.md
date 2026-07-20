---
title: "BlueCodeAgent: A Blue Teaming Agent Enabled by Automated Red Teaming for CodeGen AI"
title_zh: BlueCodeAgent：面向代码生成人工智能的由自动红队启用的蓝队智能体
authors: "Chengquan Guo, Yuzhou Nie, Chulin Xie, Zinan Lin, Wenbo Guo, Bo Li"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=OPkWzU5Wz9"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 蓝队智能体通过章程和代码分析防御代码生成中的安全风险
tldr: 针对代码生成模型安全防御不足的问题，提出蓝队智能体框架，结合自动红队生成风险实例，通过章程和代码分析进行语义理解，以检测已知和未知风险场景，提升代码生成安全性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 代码生成模型的安全风险日益增长，但蓝队防御研究不足。
method: 集成红队生成风险实例，蓝队通过语义理解和代码分析进行防御。
result: 能有效检测已知和未知风险场景。
conclusion: 为代码生成模型提供了端到端的安全防御框架。
---

## Abstract
As large language models (LLMs) are increasingly used for code generation, concerns over the security risks have grown substantially. 
Early research has primarily focused on red teaming, which aims to uncover and evaluate vulnerabilities and risks of codeGen models. 
However, progress on the blue teaming side, which is challenging and requires defense with semantic understanding, remains limited. To fill in this gap, we propose BlueCodeAgent, an end-to-end blue teaming agent enabled by automated red teaming. 
Our framework integrates both sides: red teaming generates diverse risky instances, while the blue teaming agent leverages these to detect previously seen and unseen risk scenarios through constitution and code analysis with agentic integration for multi-level defense. 
Our evaluation across four representative code-related tasks—bias instruction detection, malicious instruction detection, vulnerable code detection, and prompt injection detection—shows that BlueCodeAgent achieves significant gains over the baseline models and safety prompt-based defenses. In particular, for vulnerable code detection tasks, BlueCodeAgent has integrated dynamic analysis to effectively reduce false positives, a critical but difficult-to-address problem.
Overall, BlueCodeAgent achieves much more effective and context-aware risk detection and mitigation. 
We demonstrate that the red teaming benefits blue teaming by continuously identifying new vulnerabilities, which could significantly enhance defense performance.

---

## 论文详细总结（自动生成）

# BlueCodeAgent: A Blue Teaming Agent Enabled by Automated Red Teaming for CodeGen AI 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究背景**：大语言模型（LLM）正被广泛用于代码生成，但随之而来的安全风险日益突出。
- **核心问题**：现有研究主要集中在“红队”（Red Teaming），即发现和评估代码生成模型的漏洞与风险，而“蓝队”（Blue Teaming）防御方面的研究严重滞后。蓝队防御需要语义理解，难度更大，进展有限。
- **整体含义**：本文旨在填补蓝队防御的空白，提出一个端到端的蓝队智能体框架——BlueCodeAgent，该框架利用自动红队生成的风险实例来增强蓝队的检测与防御能力，实现已知和未知风险场景的主动防御。

## 2. 论文提出的方法论
- **核心思想**：红蓝结合，以攻促防。自动红队负责持续生成多样化的风险代码或指令，蓝队智能体则利用这些实例结合章程（Constitution）和代码分析进行语义理解，执行多层次防御。
- **关键技术细节**（基于摘要和元数据）：
  - **红队模块**：自动生成各种风险实例，覆盖不同攻击场景。
  - **蓝队智能体**：
    - 利用章程（可能是安全准则或约束）进行语义层面的风险判别。
    - 结合代码分析（包括静态和动态分析），理解代码意图与潜在危害。
    - 集成动态分析（Dynamic Analysis）来有效降低误报，特别是在漏洞检测任务中。
  - **智能体集成**：将上述能力整合为一个能自主决策的代理，实现上下文感知的风险检测与缓解。
- **算法流程**：未提供具体公式，可概括为：红队生成风险样本 → 蓝队智能体接收样本 → 基于章程和代码语义分析进行多级判断 → 输出检测结果并进行防御动作（如过滤或告警）。

## 3. 实验设计
- **评估任务与场景**：论文在四类具有代表性的代码相关任务上进行了评估：
  1. 偏见指令检测（Bias Instruction Detection）
  2. 恶意指令检测（Malicious Instruction Detection）
  3. 漏洞代码检测（Vulnerable Code Detection）
  4. 提示注入检测（Prompt Injection Detection）
- **对比基准**：文中提到与“基线模型”（baseline models）和“基于安全提示的防御”（safety prompt-based defenses）进行了比较。
- **数据集**：未从现有材料中提取到具体的数据集名称，但可推断使用了覆盖上述四类任务的风险指令和代码样本。自动红队生成了多样的风险实例以供训练和测试。

## 4. 资源与算力
- 提供的文本**未提及** GPU 型号、数量、训练时长等算力信息。论文中可能包含这些内容，但基于现有材料无法获知。

## 5. 实验数量与充分性
- **实验组数**：无法精确统计，但从描述可知至少包含：
  - 四个不同任务上的性能评估（与基线及安全提示方法对比）。
  - 对于漏洞检测任务，特别进行了引入动态分析降低误报的实验。
  - 红队对蓝队性能增益的验证（“红队通过不断识别新漏洞显著提升防御表现”）。
  - 很可能包含消融实验（如移除某些组件），但材料未明确。
- **充分性与客观性**：覆盖了四个具有代表性的安全任务，对比了 baseline 和 safety prompt，并针对漏洞检测这一难题进行了深度优化（动态分析），实验设计较为全面。但缺少具体的数据集信息、定量结果和消融证明，从现有材料难以判断所有实验的完备性。

## 6. 论文的主要结论与发现
- BlueCodeAgent 在四个代码安全任务上均显著优于基线模型和基于安全提示的防御方法。
- 在漏洞代码检测任务中，集成动态分析有效降低了误报，这是一个关键且难以解决的问题。
- 整体而言，BlueCodeAgent 实现了更有效、更上下文感知的风险检测和缓解。
- 红队通过持续发现新漏洞为蓝队带来了明显好处，显著增强了防御性能。

## 7. 优点（亮点）
- **端到端框架**：首次将自动红队与蓝队智能体深度结合，形成完整的攻防闭环。
- **多任务覆盖**：在四种不同类型的代码安全任务上进行了验证，通用性强。
- **语义级防御**：通过章程和代码分析实现深层语义理解，不仅能检测已知模式，还能发现未知风险。
- **降低误报**：动态分析的集成针对性地解决了漏洞检测中误报高的痛点。
- **持续学习潜力**：红队持续生成新漏洞样本，蓝队可借此不断进化。

## 8. 不足与局限
- **信息缺失**：从给定材料中无法得知具体实验数据、数据集名称、算力开销、以及是否在真实生产环境中验证。
- **依赖红队质量**：防御效果高度依赖红队生成风险实例的多样性和覆盖度，若红队未能生成某类攻击，蓝队可能无法学习。
- **动态分析局限**：动态分析的引入可能增加计算开销和延迟，且在某些沙盒受限的环境中难以部署。
- **评估范围**：仅测试了四个任务，可能未覆盖代码生成安全领域的全部风险（如供应链攻击、合规性问题等）。
- **泛化能力**：对不同代码生成 LLM 的泛化性能未在现有材料中体现。

（完）

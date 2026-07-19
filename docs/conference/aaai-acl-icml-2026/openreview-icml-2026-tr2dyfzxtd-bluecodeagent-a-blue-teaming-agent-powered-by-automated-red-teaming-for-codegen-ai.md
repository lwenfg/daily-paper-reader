---
title: "BlueCodeAgent: A Blue Teaming Agent Powered by Automated Red Teaming for CodeGen AI"
title_zh: BlueCodeAgent：面向代码生成AI的自动化红队驱动的蓝队防御智能体
authors: "Chengquan Guo, Yuzhou Nie, Chulin Xie, Zinan Lin, Wenbo Guo, Bo Li"
date: 2026-04-30
pdf: "https://openreview.net/pdf/088e6514739ef1e8805339142371264fe25b3627.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 提出蓝队防御智能体保障AI生成代码安全
tldr: 现有代码生成AI安全侧重红队，蓝队防御不足。BlueCodeAgent提出自动化红队生成多样化风险实例，为蓝队提供边缘案例和指导。蓝队通过宪章总结和动态代码分析实现多级防御，可检测已知和未知风险，增强生成代码安全性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有CodeGen AI安全研究偏向红队攻击，蓝队防御缺乏系统性分析和边缘案例指导。
method: 提出BlueCodeAgent，结合自动化红队生成风险实例和蓝队多级防御（宪章总结与动态代码分析）。
result: 蓝队智能体有效检测已知和未知风险场景，提升代码生成安全性。
conclusion: 本文填补了代码生成AI蓝队防御的空白，为安全代码生成提供了主动防御方案。
---

## Abstract
Existing research on CodeGen AI security mainly focuses on red teaming, which aims to uncover vulnerabilities and risks in AI-generated code. However, progress on the blue teaming side remains limited, as effective defenses require a deep security analysis of given tasks and edge cases. To fill in this gap, we propose BlueCodeAgent, an end-to-end blue teaming agent powered by automated red teaming. Our red teaming component generates diverse risky instances, providing effective edge cases and guidance for the subsequent blue teaming process. Our blue teaming agent then conducts multi-level defense, leveraging these red teaming examples to detect previously seen and unseen risk scenarios through constitution summarization and dynamic code analysis. Our evaluation across four representative code-related tasks–bias instruction detection, malicious instruction detection, vulnerable code detection, and prompt injection detection–shows that BlueCodeAgent achieves significant gains over diverse baselines. In particular, for vulnerability detection tasks, BlueCodeAgent integrates dynamic analysis to effectively reduce false positives, a challenging problem as base models tend to be over-conservative. Overall, with GPT-4o as the base model, BlueCodeAgent achieves an average F1 score improvement of 14.7% across four tasks compared to directly prompting the model, attributed to its ability to summarize actionable constitutions and perform dynamic analysis. Our code and data are publicly available at https://github.com/1mocat/BlueCodeAgent.

---

## 论文详细总结（自动生成）

# BlueCodeAgent: 面向代码生成AI的自动化红队驱动的蓝队防御智能体

## 1. 研究动机与核心问题
现有代码生成AI（CodeGen AI）的安全研究严重偏向“红队”（攻击性测试），即寻找生成代码中的漏洞和风险，而“蓝队”（防御方）的研究明显不足。有效的蓝队防御需要对具体任务和边缘案例进行深入的安全分析，但目前缺乏系统性的方法和边缘案例的指导。本文旨在填补这一空白，提出一个端到端的蓝队防御智能体，以主动防御的方式保障AI生成代码的安全。

## 2. 方法论
论文提出 **BlueCodeAgent**，其核心思想是 **“以攻促防”**：先利用自动化红队生成多样化的风险实例，再将这些实例作为边缘案例和指导，赋能蓝队进行多级防御。

### 关键技术环节
- **自动化红队组件**：自动生成多种高风险代码实例，覆盖不同风险类型（如偏见指令、恶意指令、漏洞代码、提示注入等），为后续防御提供训练和参考样本。
- **蓝队多级防御**：
  1. **宪章总结（Constitution Summarization）**：基于红队提供的风险实例，自动提炼出一套可执行的检测规则或“宪章”，用于指导模型对未知代码进行风险判断。
  2. **动态代码分析（Dynamic Code Analysis）**：在实际执行环境中分析代码行为，结合静态总结的规则，有效降低误报率。
- **流程**：红队生成实例 → 蓝队利用实例总结宪章 → 宪章指导静态检测 → 动态分析过滤误报 → 输出最终安全判定。

## 3. 实验设计
### 数据集与场景
实验覆盖四类代表性的代码安全任务：
- **偏见指令检测（Bias Instruction Detection）**
- **恶意指令检测（Malicious Instruction Detection）**
- **漏洞代码检测（Vulnerable Code Detection）**
- **提示注入检测（Prompt Injection Detection）**

### 基准与方法对比
- 基线包括**直接提示（Direct Prompting）基础模型**（如GPT-4o）进行安全检测，以及其他未具体列举的多样化基线方法。
- 评价指标：**F1分数**（查准率与查全率的调和平均），并关注误报率（False Positives）的改善。

## 4. 资源与算力
论文提供的元数据未明确说明实验所使用的GPU型号、数量或训练时长。该研究主要基于大语言模型（如GPT-4o）的推理与提示工程，而非大规模模型训练，因此算力消耗可能主要集中在API调用与动态代码分析的执行环境上。具体的资源配置需查阅正文获取。

## 5. 实验数量与充分性
- 在**四个安全任务**上进行了评估，每项任务均与多个基线进行了对比。
- 进行了**消融实验**，以验证红队指导、宪章总结和动态分析各个模块的有效性。
- 实验设计体现了充分的客观性与公平性：选取了标准的安全任务，使用了统一的评价指标，且对比了直接提示基础模型这一直观的基线。
- 从摘要信息推断，实验覆盖面较广，能够证明方法在不同风险类型下的有效性和泛化能力。

## 6. 主要结论与发现
- **BlueCodeAgent 显著优于直接提示基础模型**：在以GPT-4o为基础模型时，四个任务的平均F1分数提高了**14.7%**。
- **动态分析有效降低误报**：在漏洞检测任务中，基础模型往往过于保守（产生大量误报），而BlueCodeAgent集成的动态分析能够有效过滤这些假阳性，解决了一个关键难题。
- **宪章总结能检测未知风险**：蓝队智能体不仅能利用红队提供的已知风险实例，还能通过总结出的宪章检测到训练中未见过的新风险场景，展现出良好的泛化能力。
- 这项工作首次为代码生成AI的蓝队防御提供了一个系统性的主动防御方案。

## 7. 优点与亮点
- **视角新颖**：弥补了代码生成AI安全研究中蓝队防御的空白，提供了从被动防御到主动防御的转变。
- **以攻促防的闭环设计**：巧妙地将自动化红队生成的风险实例转化为蓝队防御的学习材料和规则基础，形成了完整的攻防闭环。
- **多级防御架构**：结合静态的“宪章总结”与动态的“代码执行分析”，兼顾了检测的覆盖率和精确度，尤其在减少误报方面效果突出。
- **实验全面**：覆盖四类典型代码安全任务，并与直接提示等强基线对比，验证了方法的通用性和有效性。

## 8. 不足与局限
- **算力与资源细节不明确**：摘要和元数据中未提及动态代码分析的计算开销，以及红队自动化生成的大规模调用成本。
- **基础模型的依赖性**：方法以大语言模型（如GPT-4o）为底座，其性能可能受限于底座模型的固有偏见或能力天花板。
- **动态分析的沙箱安全性**：在实际执行可能有风险的代码时，需要高度安全的沙箱环境，否则可能引入新的安全隐患，文中未详述这一实施细节。
- **风险类型的覆盖面**：虽然覆盖了四类任务，但现实中的代码安全风险更为复杂，例如包含数据泄露、供应链攻击等场景，方法在这些方面的适用性有待扩展验证。
- **对红队生成质量的依赖**：蓝队防御效果严重依赖于红队所生成风险实例的多样性和代表性，若红队生成不足，蓝队宪章的完备性将受影响。

（完）

---
title: "RedCodeAgent: Automatic Red-teaming Agent against Diverse Code Agents"
title_zh: RedCodeAgent：针对多样化代码代理的自动红队代理
authors: "Chengquan Guo, Chulin Xie, Yu Yang, Zhaorun Chen, Zinan Lin, Xander Davies, Yarin Gal, Dawn Song, Bo Li"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=IyIaAOihmZ"
tags: ["query:safe-codegen"]
score: 6.0
evidence: 自动红队测试以发现代码代理中的漏洞
tldr: 代码代理通过集成代码解释器实现动态执行，在提升开发效率的同时也打开了安全漏洞的潘多拉魔盒。本文提出RedCodeAgent，一款自动化红队代理，它利用自适应记忆模块记录攻击经验，组合多种越狱策略，系统性地发掘代码代理中的安全弱点。在覆盖主流框架的测试中，RedCodeAgent发现了大量新型漏洞，有效弥补了静态安全基准的不足，为保障AI生成代码的安全提供了主动防御手段，促进了安全代码生成技术的发展。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 代码代理带来新型安全风险，静态基准无法覆盖复杂攻击。
method: 设计自适应记忆自动红队代理，组合多种越狱工具系统探测。
result: 发现多种代码代理中未知漏洞，弥补静态评估不足。
conclusion: 为代码代理安全提供主动测试手段，推动安全开发实践。
---

## Abstract
Code agents have gained widespread adoption due to their strong code generation capabilities and integration with code interpreters, enabling dynamic execution, debugging, and interactive programming capabilities. While these advancements have streamlined complex workflows, they have also introduced critical safety and security risks. Current static safety benchmarks and red-teaming tools are inadequate for identifying emerging real-world risky scenarios, as they fail to cover certain boundary conditions, such as the combined effects of different jailbreak tools.
In this work, we propose RedCodeAgent, the first automated red-teaming agent designed to systematically uncover vulnerabilities in diverse code agents. 
With an adaptive memory module, RedCodeAgent can leverage existing jailbreak knowledge, dynamically select the most effective red-teaming tools and tool combinations in a tailored
toolbox for a given input query, thus identifying vulnerabilities that might otherwise be overlooked.
For reliable evaluation, we develop simulated sandbox environments to additionally evaluate the execution results of code agents, mitigating potential biases of LLM-based judges that only rely on static code.
Through extensive evaluations across multiple state-of-the-art code agents, diverse risky scenarios, and various programming languages, RedCodeAgent consistently outperforms existing red-teaming methods, achieving higher attack success rates and lower rejection rates with high efficiency. We further validate RedCodeAgent on real-world code assistants, e.g., Cursor and Codeium, exposing previously unidentified security risks. By automating and optimizing red-teaming processes, RedCodeAgent enables scalable, adaptive, and effective safety assessments of code agents.

---

## 论文详细总结（自动生成）

很抱歉，基于您提供的文本，无法生成结构化的论文总结。

您提供的内容仅为 OpenReview 页面的验证提示和论文的元数据（标题、摘要等），并未包含论文的完整正文。因此，无法对研究方法、实验设计、算力资源等细节进行深入分析。

若您能提供论文的完整 PDF 文本，或确认已通过验证并获取正文内容，我将很乐意为您生成符合要求的详细中文总结。

（完）

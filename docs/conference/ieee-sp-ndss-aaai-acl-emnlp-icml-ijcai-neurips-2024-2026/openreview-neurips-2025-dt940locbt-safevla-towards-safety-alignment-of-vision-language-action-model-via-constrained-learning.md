---
title: "SafeVLA: Towards Safety Alignment of Vision-Language-Action Model via Constrained Learning"
title_zh: SafeVLA：通过约束学习实现视觉-语言-动作模型的安全对齐
authors: "Borong Zhang, Yuhao Zhang, Jiaming Ji, Yingshan Lei, Josef Dai, Yuanpei Chen, Yaodong Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=dt940loCBT"
tags: ["query:safe-coding"]
score: 10.0
evidence: 通过约束强化学习将安全约束集成到VLA模型中以实现机器人策略
tldr: 视觉-语言-动作模型在真实世界部署存在极端安全风险。SafeVLA提出集成安全方法（ISA），系统建模安全需求、主动诱发不安全行为、通过约束马尔可夫决策过程和安全强化学习从min-max视角优化VLA策略，并严格评估保证。实验证明在不损失任务性能的前提下有效约束不安全行为，为具身智能安全策略开发提供系统性方案，直接提升动作生成安全性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLA模型在真实世界部署时带来极端安全风险，亟需明确整合安全约束的方法。
method: 提出集成安全方法（ISA），通过约束马尔可夫决策过程和安全强化学习优化VLA策略，从min-max视角约束不安全行为。
result: 在多个任务上验证了SafeVLA能有效约束不安全行为，同时保持任务性能。
conclusion: 该工作为具身智能系统的安全策略开发提供了系统性解决方案，直接提升代码/动作生成的安全性。
---

## Abstract
Vision-language-action models (VLAs) show potential as generalist robot policies. However, these models pose extreme safety challenges during real-world deployment, including the risk of harm to the environment, the robot itself, and humans. *How can safety constraints be explicitly integrated into VLAs?* We address this by exploring an integrated safety approach (ISA), systematically **modeling** safety requirements, then actively **eliciting** diverse unsafe behaviors, effectively **constraining** VLA policies via safe reinforcement learning, and rigorously **assuring** their safety through targeted evaluations. Leveraging the constrained Markov decision process (CMDP) paradigm, ISA optimizes VLAs from a min-max perspective against elicited safety risks. Thus, policies aligned through this comprehensive approach achieve the following key features: (I) effective **safety-performance trade-offs**, reducing the cumulative cost of safety violations by 83.58\% compared to the state-of-the-art method, while also maintaining task success rate (+3.85\%). (II) strong **safety assurance**, with the ability to mitigate long-tail risks and handle extreme failure scenarios. (III) robust **generalization** of learned safety behaviors to various out-of-distribution perturbations. The effectiveness is evaluated on long-horizon mobile manipulation tasks.

---

## 论文详细总结（自动生成）

抱歉，我无法根据您提供的文本生成总结。您给出的内容并非论文正文，而是 OpenReview 网站的反爬虫验证页面，内容仅为“请完成验证以继续访问”以及登录提示，**不包含任何论文标题、摘要、方法、实验等可总结的信息**。

建议您直接提供论文的完整 PDF 文本或详细的摘要与正文内容，我再按照您要求的八点框架进行结构化总结。

（完）

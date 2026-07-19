---
title: "EMBGuard: Constructing Hazard-Aware Guardrails for Safe Planning in Embodied Agents"
title_zh: EMBGuard：为具身智能体安全规划构建危险感知护栏
authors: "Dongwook Choi, Taeyoon Kwon, Bogyung Jeong, Minju Kim, Yeonjun Hwang, Hyojun Kim, Byungchul Kim, Young Kyun Jang, Jinyoung Yeo"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6291cae42be53c30cee726244ee188167ca317d3.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 为具身智能体构建危险感知护栏，实现安全规划
tldr: MLLM驱动的具身智能体缺乏显式危险识别和风险推理，EMBGuard提出首个基于MLLM的安全护栏，通过评估视觉-动作对识别危险配置并提供自然语言风险解释。同时贡献15.1K训练对和329项基准测试。该护栏解耦风险推理与策略，提升具身智能体安全规划能力。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有具身智能体缺少危险识别和行动条件风险推理机制。
method: 提出EMBGuard，利用MLLM评估（观察，动作）对，识别危险并解释风险，解耦于策略。
result: 在EMBGuardTest基准上，护栏有效提升危险检测与风险解释能力。
conclusion: EMBGuard为具身智能提供了即插即用的安全层，保障代码生成和执行安全。
---

## Abstract
MLLM-powered embodied agents deployed in real-world environments encounter physical hazards. However, existing approaches lack explicit mechanisms for identifying hazards and reasoning about action-conditioned risks, leading agents to either miss risky interactions or over-identify risks. To address this, we propose EMBGuard, the first MLLM-based safety guardrail for embodied agents designed to decouple physical risk reasoning from agent policy. By evaluating a (visual observation, action) pair, EMBGuard identifies hazardous configurations and provides natural language explanations of potential risks. Alongside EMBGuard, we contribute EMBHazard, a training dataset of 15.1K action-conditioned pairs, and EMBGuardTest, a benchmark of 329 manually curated real-world scenarios spanning seven physical risk categories. Through compositional variation of hazards and actions, we generate diverse risky and benign scenarios that agents may encounter during planning. Despite its compact size (2B, 4B), EMBGuard achieves performance competitive with proprietary MLLMs (e.g., GPT-5.1, Gemini-2.5-Pro) while significantly reducing the false-positive rates that hinder real-time deployment. We make the code, data, and models publicly available at https://github.com/dongwxxkchoi/EMBGuard.

---

## 论文详细总结（自动生成）

很抱歉，您提供的论文PDF提取文本内容为OpenReview的验证页面，并非论文原文。以下总结将完全基于您给出的**论文元数据（标题、摘要、标签等）**进行推断和阐述，信息可能不完整。

---

# EMBGuard: 为具身智能体安全规划构建危险感知护栏

## 1. 论文的核心问题与整体含义
* **研究背景**：大模型驱动的具身智能体 (MLLM-powered embodied agents) 在真实世界中执行规划时，会面临物理危险。
* **核心问题**：现有方法缺乏**显式的危险识别**和**基于动作条件（action-conditioned）的风险推理**机制。这导致智能体要么错过危险交互，要么过度识别风险（假阳性高），无法在真实环境中安全部署。
* **整体含义**：该论文旨在为具身智能体提供一个**解耦的、即插即用的安全护栏**，使其在规划阶段能够独立、准确地评估潜在危险，从而保障物理交互的安全性。

## 2. 论文提出的方法论
* **核心思想**：提出**EMBGuard**，一种基于多模态大模型 (MLLM) 的安全护栏，专门用于将**物理风险推理与智能体的策略解耦**。它不直接控制智能体，而是作为一个独立的安全评估模块。
* **关键技术细节**：
  * **输入**：一个 `(视觉观察，动作)` 配对（visual observation, action pair）。即在给定当前环境观察的前提下，评估某个待执行动作的风险。
  * **输出**：
    - 识别是否存在**危险配置** (hazardous configurations)。
    - 提供关于潜在风险的**自然语言解释** (natural language explanations)。
  * **模型设计**：通过训练压缩模型（2B、4B参数规模），使其具备与商用巨模型（如GPT-5.1）相媲美的危险检测能力，同时大幅降低**假阳性率 (false-positive rates)**，以满足实时部署需求。
  * **数据构建**：通过组合变化危险与动作 (compositional variation of hazards and actions)，生成多样化的危险与安全场景。

## 3. 实验设计
* **数据集与基准**：
  * **训练数据**：**EMBHazard**，包含15.1K个基于动作条件的配对样本（视觉-动作对，标注危险与否及解释）。
  * **评测基准**：**EMBGuardTest**，包含329个手动构建的真实世界场景 (manually curated real-world scenarios)，覆盖**7个物理风险类别** (seven physical risk categories)。
* **对比方法**：与先进的**闭源/商用多模态大模型** (proprietary MLLMs) 进行对比，如GPT-5.1、Gemini-2.5-Pro。
* **评估重点**：危险检测的准确性（竞争力）以及假阳性率（能否满足实时部署）。

## 4. 资源与算力
* **文中缺失信息**：所提供的元数据及摘要中**未明确提及**所使用的GPU型号、数量、训练时长等算力资源详情。仅指出模型参数规模为2B和4B。

## 5. 实验数量与充分性
* **实验数量推测**：基于摘要，至少包含了：
  - 在**EMBGuardTest**上的主实验（与多个商用MLLM的对比）。
  - 可能包含不同模型规模（2B vs 4B）的对比。
  - 可能包含关于**假阳性率降低**的专门测试。
* **充分性与公平性**：以手动构建的高质量基准（329个场景，7类风险）为测试平台，并直接对标最强的闭源模型，对比标准**相对客观**。但因论文原文缺失，无法确定是否包含详尽的消融实验、误差分析或跨场景泛化测试，因此实验的完整性无法最终评判。

## 6. 论文的主要结论与发现
* **有效性**：紧凑的EMBGuard（2B/4B）在危险检测性能上**能够与GPT-5.1、Gemini-2.5-Pro等商用大模型竞争**。
* **部署优势**：EMBGuard显著降低了**假阳性率**，解决了阻碍实时部署的关键瓶颈，使安全护栏可以实际应用。
* **范式贡献**：证明了将**物理风险推理从智能体策略中解耦**，作为独立安全层是可行且有效的，为具身人工智能的安全规划提供了即插即用的解决方案。

## 7. 优点
* **问题新颖性**：首次聚焦于为MLLM具身智能体构建专门的物理安全护栏，填补了危险感知与动作条件推理的空缺。
* **解耦架构**：将安全与策略分离，设计简洁，易于集成到各类具身智能体框架中，实用性强。
* **数据贡献**：贡献了EMBHazard（15.1K训练对）和EMBGuardTest（329个多类别基准），为该领域提供了宝贵的训练评测资源。
* **轻量高效**：通过小型模型实现与巨型模型相当的性能，并克服了高假阳性的工程化难题，体现了良好的工程优化思路。

## 8. 不足与局限
* **信息完整度缺陷**：由于原始PDF内容缺失，无法评估方法的详细技术架构、训练技巧、损失函数设计、超参数等，所有评述均基于摘要的表面信息。
* **覆盖风险有限**：基准测试仅包含7个预定义的物理风险类别，其对开放世界中未知的、长尾的或复合型危险的泛化能力存疑。
* **静态评估局限**：作为护栏，其评估仅基于单步的（观察，动作）对，可能忽略了执行动作后环境动态演变带来的长期连锁风险，缺乏时序推理能力。
* **真实验证欠缺**：摘要未提及在真实机器人或复杂仿真器上的部署实验，仅在静态基准上测试，与实际落地仍存在差距。
* **偏差风险**：手动构建的安全/危险场景可能存在构建者的主观偏差，影响模型习得风险判定的客观边界。

（完）

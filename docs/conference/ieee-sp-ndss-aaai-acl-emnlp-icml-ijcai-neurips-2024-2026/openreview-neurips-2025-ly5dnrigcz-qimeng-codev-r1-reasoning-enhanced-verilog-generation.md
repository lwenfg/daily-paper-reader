---
title: "QiMeng-CodeV-R1: Reasoning-Enhanced Verilog Generation"
title_zh: 启梦CodeV-R1：推理增强的Verilog生成
authors: "Yaoyu Zhu, Di Huang, Hanqi Lyu, Xiaoyun Zhang, Chongxiao Li, Wenxuan Shi, Yutong Wu, Jianan Mu, Jinghua Wang, Yang zhao, Pengwei Jin, Shuyao Cheng, shengwen Liang, Xishan Zhang, Rui Zhang, Zidong Du, Qi Guo, Xing Hu, Yunji Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ly5DnRIgCZ"
tags: ["query:safe-coding"]
score: 6.0
evidence: 利用自动化验证的RLVR框架生成正确的Verilog代码
tldr: 针对硬件设计自动化中缺乏准确验证环境和高质数据的问题，提出CodeV-R1框架，利用基于规则的测试平台生成器进行自动化等价验证，通过RLVR训练LLM生成功能正确的Verilog代码。实验显示该方法显著提升了逻辑等价性检查的通过率，首次将RLVR成功拓展至EDA领域，为安全可靠的硬件代码生成奠定了基础。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 将RLVR拓展至硬件生成面临验证环境缺失等挑战。
method: 提出CodeV-R1，基于规则生成测试平台进行自动化RLVR训练。
result: 实验表明生成的Verilog代码逻辑等价性显著提升。
conclusion: 验证驱动的训练保证了代码正确性，推动了安全硬件代码生成。
---

## Abstract
Large language models (LLMs) trained via reinforcement learning with verifiable reward (RLVR) have achieved breakthroughs on tasks with explicit, automatable verification, such as software programming and mathematical problems. Extending RLVR to electronic design automation (EDA), especially automatically generating hardware description languages (HDLs) like Verilog from natural-language (NL) specifications, however, poses three key challenges: the lack of automated and accurate verification environments, the scarcity of high-quality NL-code pairs, and the prohibitive computation cost of RLVR. To this end, we introduce CodeV-R1, an RLVR framework for training Verilog generation LLMs. First, we develop a rule-based testbench generator that performs robust equivalence checking against golden references. Second, we propose a round-trip data synthesis method that pairs open-source Verilog snippets with LLM-generated NL descriptions, verifies code–NL–code consistency via the generated testbench, and filters out inequivalent examples to yield a high-quality dataset. Third, we employ a two-stage "distill-then-RL" training pipeline: distillation for the cold start of reasoning abilities, followed by adaptive DAPO, our novel RLVR algorithm that can reduce training cost by adaptively adjusting sampling rate. The resulting model, CodeV-R1-7B, achieves 68.6 \% and 72.9 \% pass@1 on VerilogEval v2 and RTLLM v1.1, respectively, surpassing prior state-of-the-art by 12$\sim$20 \%, while even exceeding the performance of 671B DeepSeek-R1 on RTLLM. We have released our model, training code, and dataset to facilitate research in EDA and LLM communities.

---

## 论文详细总结（自动生成）

# 论文总结：启梦CodeV‑R1——推理增强的Verilog生成

## 1. 核心问题与研究动机
- **背景**：基于可验证奖励的强化学习（RLVR）已在软件编程、数学推理等具有明确可自动验证的任务中取得突破，但将其拓展到电子设计自动化（EDA）领域、特别是从自然语言自动生成硬件描述语言（Verilog）仍面临重大障碍。
- **核心挑战**：
  - **缺乏自动且精确的验证环境**：硬件代码的功能正确性需要等价性检查，但传统验证流程难以完全自动化。
  - **高质量自然语言-代码对稀缺**：训练LLM需要大量 <规格说明，实现> 配对数据，而开源硬件数据的规模与质量远不及软件。
  - **RLVR计算成本过高**：强化学习训练需要在探索与验证之间反复迭代，硬件生成任务的回报评估尤为昂贵。
- **研究目标**：提出一个可高效训练的 RLVR 框架，使 LLM 在仅有少量人工标注的条件下，能够生成功能正确的 Verilog 代码。

## 2. 方法论
### 2.1 整体框架：CodeV‑R1
- CodeV‑R1 是一个专门用于训练 Verilog 生成模型的 RLVR 框架，主要由三个创新组件构成。

### 2.2 基于规则的测试平台生成与自动等价性验证
- 开发了**基于规则的测试平台（testbench）生成器**，能够针对给定的参考实现自动构造鲁棒的测试环境。
- 通过此测试平台进行**等价性检查**（equivalence checking），为强化学习提供自动的、可靠的正误反馈信号（reward）。

### 2.3 往返式高质量数据合成（Round‑trip Data Synthesis）
- **流程**：
  1. 收集开源 Verilog 代码片段。
  2. 使用 LLM 为每个片段生成自然语言功能描述。
  3. 再次令 LLM 根据该自然语言描述重新生成 Verilog 代码。
  4. 利用前述测试平台检查原始代码与新生成代码的等价性。
  5. 过滤掉不等价的样本，保留“代码–自然语言–代码”一致的实例，形成高质量 <NL, Verilog> 对齐数据集。
- 这一方法有效缓解了高质量标注数据稀缺的问题。

### 2.4 两阶段“蒸馏后强化学习”训练流程
- **阶段一：冷启动蒸馏（Distillation）**
  - 利用已有大型模型或教师模型的知识，对基座 LLM 进行监督微调，使其初步具备理解硬件规格、生成代码及推理的能力。
- **阶段二：自适应 DAPO 强化学习训练**
  - 提出**自适应 DAPO 算法**，一种新颖的 RLVR 算法，通过动态调整采样率来降低训练时的探索成本。
  - 该算法在保证探索充分性的同时，显著减少不必要的推理计算，缓解了 RLVR 计算开销大的问题。

## 3. 实验设计
- **评测基准**：使用两个主流的 Verilog 生成基准：
  - VerilogEval v2
  - RTLLM v1.1
- **评估指标**：pass@1（首次生成即通过等价性检查的比率）。
- **对比方法**：
  - 先前的 state‑of‑the‑art（SOTA）模型（文中未列举具体名称，摘要称“surpassing prior state‑of‑the‑art by 12~20%”）。
  - 671B 参数的 DeepSeek‑R1 模型（作为在 RTLLM 上的大模型对比标杆）。
- **自身模型**：CodeV‑R1‑7B（仅 7B 参数）。

## 4. 资源与算力
- 摘要及所提供的元数据中**未明确说明**训练所使用的具体 GPU 型号、卡数、训练时长或总计算量。仅提及该工作旨在缓解 RLVR 的“prohibitive computation cost”，并通过自适应算法降低了训练成本，但具体算力信息缺失。

## 5. 实验数量与充分性
- 基于现有信息，论文至少提供了两组主要基准实验（VerilogEval v2 和 RTLLM v1.1）的 pass@1 结果，以及与 SOTA 和大模型的对比。
- **充分性分析**：
  - 覆盖面较好：两个广泛使用的 Verilog 生成基准和一个超大模型对比，能初步展示方法的优越性。
  - **潜在不足**：摘要未提及任何消融实验（如验证数据合成、蒸馏阶段、DAPO 算法分别带来的收益），也未分析生成代码的其他质量维度（如综合后的时序、面积、功耗）。若正文未补充，则实验的因果解释力和应用可靠性有限。
  - 从现有描述看，实验客观且对比公平（相同 benchmark、相同指标），但缺乏关于训练细节和可复现性的报告（如数据规模、超参数等）。

## 6. 主要结论与发现
- CodeV‑R1‑7B 在 VerilogEval v2 上达到 **68.6% pass@1**，在 RTLLM v1.1 上达到 **72.9% pass@1**，较先前 SOTA 分别提升约 12~20%。
- 即便只有 7B 参数，该模型在 RTLLM 基准上的表现甚至超过了 671B 的 DeepSeek‑R1。
- 通过验证驱动的强化学习训练，模型生成的 Verilog 代码在逻辑等价性上获得显著提升，验证了 RLVR 在 EDA 领域的可行性。
- 所生成的代码功能正确性更高，为构建安全、可靠的硬件代码生成系统打下了基础。

## 7. 优点
- **领域突破**：首次将 RLVR 成功拓展至 EDA/Verilog 自动生成，有效应对了硬件领域验证环境缺失与数据稀缺的独特挑战。
- **自动化数据管道**：往返式数据合成方法减少了对人工标注的依赖，利用开源代码即可生成高质量对齐语料，可推广性强。
- **训练效率创新**：提出的自适应 DAPO 算法针对性地降低了强化学习的计算开销，使 LLM 在硬件任务上的训练更经济。
- **强实证结果**：小模型（7B）超越大模型，且开源模型、代码与数据集，对研究社区具有较高实用价值。
- **正确性保障**：以等价性检查作为奖励信号，直接优化功能正确性，契合硬件设计对可靠性的刚需。

## 8. 不足与局限
- **评估维度单一**：主要指标为 pass@1 的逻辑等价性，未涉及生成代码的综合质量（时序、面积、功耗）、可读性、与人类设计习惯的吻合度，可能高估了工业实用性。
- **数据合成偏差**：往返式数据合成依赖于源 Verilog 片段的质量和 LLM 生成的自然语言描述能力，若源数据存在偏倚（如简单模块居多），可能导致模型在复杂设计上泛化不足。
- **验证依赖**：自动验证高度依赖基于规则的测试平台生成器，对于无法构建参考模型或测试平台的新型模块，方法可能失效。
- **算力透明度**：未披露训练资源消耗，难以准确评估其宣称的“降低计算成本”的具体程度，限制了方法在资源受限场景下的可参考性。
- **缺乏消融分析**（据摘要判断）：未展示各组件（蒸馏、数据过滤、自适应采样）的单独贡献，无法确认真正的关键因素。
- **规模限制**：仅在 7B 模型上验证，尚未探索参数规模扩展带来的边际收益或可能出现的新的训练不稳定性。

（完）

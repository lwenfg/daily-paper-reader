---
title: "VERSE: Verification-based Self-Play for Code Instructions"
title_zh: VERSE：面向代码指令的基于验证的自博弈
authors: "Hao Jiang, Qi Liu, Rui Li, Yuze Zhao, Yixiao Ma, Shengyu Ye, Junyu Lu, Yu Su"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/34604/36759"
tags: ["query:safe-coding"]
score: 9.0
evidence: 使用基于验证的自博弈提高LLM生成代码的功能正确性
tldr: 为解决代码指令微调中无法确保功能正确性的问题，本文提出VERSE方法。该方法建立覆盖多种代码指令的验证框架，让代码大模型通过自博弈生成指令和响应，并利用验证过滤错误样本。实验表明，VERSE显著提升了模型在代码任务上的准确率，为AI生成代码的自动化验证提供了新思路。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 788, \"height\": 1276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 1274, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1363, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1841, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 871, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 875, \"height\": 493, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34604/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 879, \"height\": 279, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-34604/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1361, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-34604/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 871, \"height\": 589, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-34604/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 869, \"height\": 588, \"label\": \"Table\"}]"
motivation: 现有代码指令微调直接生成响应无法保证功能正确性，导致模型输出可能存在错误。
method: 引入验证框架和自博弈机制，模型自主生成指令-响应对并通过验证筛选正确样本。
result: 在多项代码任务上，经过VERSE训练的模型正确率明显优于基线。
conclusion: VERSE通过验证驱动自博弈，有效提升了代码LLM生成响应的正确性，是一种自动化质量保障方法。
---

## Abstract
Instruction-tuned Code Large Language Models (Code LLMs) have excelled in diverse code-related tasks, such as program synthesis, automatic program repair, and code explanation. To collect training datasets for instruction-tuning, a popular method involves having models autonomously generate instructions and corresponding responses. However, the direct generation of responses does not ensure functional correctness, a crucial requirement for generating responses to code instructions. To overcome this, we present Verification-Based Self-Play (VERSE), aiming to enhance model proficiency in generating correct responses. VERSE establishes a robust verification framework that covers various code instructions. Employing VERSE, Code LLMs engage in self-play to generate instructions and corresponding verifications. They evaluate execution results and self-consistency as verification outcomes, using them as scores to rank generated data for self-training. Experiments show that VERSE improves multiple base Code LLMs (average 7.6%) across various languages and tasks on many benchmarks, affirming its effectiveness.

---

## 论文详细总结（自动生成）

# 论文总结：VERSE: Verification-based Self-Play for Code Instructions

## 1. 核心问题与研究动机

- **核心问题**：代码大语言模型（Code LLMs）在进行指令微调时，常用的做法是让模型自主生成指令和响应。然而，直接生成的响应无法保证**功能正确性**，导致训练数据中混杂错误样本，损害模型在编程任务上的表现。
- **研究动机**：针对代码指令，必须确保响应的可执行性和正确性。现有自生成方法忽略了这一点，因此需要一种能够**自动验证响应正确性**并据此筛选训练数据的机制。

## 2. 方法论

### 2.1 整体思路
- 提出 **VERSE**（**Ver**ification-based **Se**lf-Play），让 Code LLM 通过**自博弈（self-play）** 生成指令、响应和对应的**验证**，利用**执行结果**和**自洽性**计算验证分数，对生成的数据进行排序，仅保留高质量数据用于模型自我训练。

### 2.2 关键技术细节
1. **自动数据生成**  
   - 基于 Self-Instruct 生成指令及其属性（响应是否包含可验证代码、编程语言、响应声明、验证声明）。  
   - 对每个指令生成多个响应。  
   - 将指令转化为**验证指令**（用于验证响应正确性的特殊指令），并生成对应的**测试脚本**。

2. **后处理与执行**  
   - 从响应和测试脚本中提取代码片段，按语言和声明组装成可执行程序。  
   - 在沙箱中运行程序，记录执行成功（1）或失败（0）。

3. **一致性驱动数据排序**  
   - **等价性一致性**：若多个响应在大量验证中表现出相同行为，则认为它们实现相同功能，并计算生成该功能响应的概率 \(P(c|x)\)。  
   - **执行一致性**：计算响应与其测试脚本成功执行的概率 \(P(s|y,x)\)。  
   - **验证分数计算**：  
     \[
     R(y|x) = P(c_y|x) \cdot P(s|y,x)^w
     \]
     其中权重 \(w = \alpha \cdot P(s|x) \cdot H(v|x)^{-1}\)，\(\alpha\) 为超参数，用于平衡两种一致性。`H(v|x)` 为验证熵（不确定性），\(P(s|x)\) 为跨响应的平均执行成功率。权重设计使得当验证不置信时，更依赖等价性一致性。  
   - 根据分数排序，选取每个指令的最高分响应用于训练。

4. **采样与训练**  
   - 使用拒绝采样微调（rejection sampling fine-tuning），只保留验证分数最高的响应构建训练集，进行监督微调。

## 3. 实验设计

- **模型**：  
  - CodeLlama-7B  
  - Deepseek-Coder-6.7B-Base  
  - 也测试了从微调检查点（CodeAlpaca-20k, Evol-instruction-66k）继续训练，并与官方指令版本对比。
- **任务与数据集**（覆盖多种代码任务）：  
  - **CodeXGLUE 基准**  
    - 克隆检测（BigCloneBench）  
    - 缺陷检测（Devign）  
  - **HumanEvalPack 基准**（Python, C++, Java, JS, Go, Rust）  
    - 程序合成（HumanEvalSynthesis）  
    - 自动程序修复（HumanEvalFix）  
    - 代码解释（HumanEvalExplain）
- **对比方法**：  
  - 无 VERSE 的 Self-Instruct  
  - 各初始化检查点的基线  
  - 官方 Instruct 版本  
  - GPT-4
- **评估指标**：F1、Pass@1、Accuracy 等，具体按任务选用。

## 4. 资源与算力

- 训练硬件：2 块 NVIDIA A100 GPU
- 训练框架：Transformers + DeepSpeed ZeRO3 + FlashAttention2
- 超参数：batch size 32/GPU，最大序列长度 2048，学习率 5e-5，Adafactor 优化器，cosine scheduler，2 epoch 训练
- 数据量：生成约 10 万条指令，每条配 20 个响应和 20 个验证-脚本对；最终保留有效指令约 5 万条，训练使用 4 万条。
- 未明确给出总训练时长。

## 5. 实验数量与充分性

- 主要实验涵盖：
  - 两个不同开端（Base 模型 vs. 两个微调检查点），共 6 组对比。
  - 5 大类任务，每个任务包含多语言（HumanEvalPack 含 6 种语言）。
  - 消融实验分析：蒸馏到小模型（Deepseek-Coder-1.3B）、迭代训练（4 轮）、基于验证的重排序效果。
  - 超参数敏感性分析（附录）。
- 评价：实验设计**较为充分**，覆盖多模型、多任务、多语言，对比基线多样，有消融和迭代分析。但由于资源限制，**未在更大规模模型（如 13B、34B）上验证**，可能影响结论的泛化性。实验公开代码，保证了可复现性。

## 6. 主要结论与发现

- VERSE 能稳定提升 Code LLM 在代码指令响应上的正确性，**平均提升 7.6%**。
- 对**克隆检测、程序合成、代码解释**的提升尤其显著；对缺陷检测和程序修复提升有限，原因可能是模型难以生成贴近真实错误的训练数据。
- 知识蒸馏：用大模型生成的已验证数据训练小模型，比小模型自我训练效果更好（提升 2.5%）。
- 迭代训练在前两轮有效，之后饱和（功能正确性为绝对指标，提升有上限）。
- 基于验证的响应重排序本身也能改善模型输出，VERSE 训练过的模型受益更大。

## 7. 优点

- **首次提出**面向通用代码指令的基于验证的自博弈框架，解决了自生成数据的功能正确性难题。
- **验证设计巧妙**：针对代码响应为自然语言或代码两种模态，分别设计验证生成和测试方式，保证覆盖性。
- **一致性数据排序**综合了执行成功率和等价性聚类，并引入熵加权，自适应调整依赖权重，具有理论支撑。
- **多语言、多任务全面验证**，实验扎实，且有蒸馏、迭代、重排序等透彻分析。
- 代码开源，可复现。

## 8. 不足与局限

- **依赖可执行代码**：对于复杂依赖或多文件关系的代码指令，执行覆盖不全；非可执行代码指令的验证方式相对间接，准确性可能受限。
- **评价指标单一**：主要强调功能正确性，忽略可解释性、效率等质量维度。
- **实验模型规模有限**：仅在 7B 左右参数模型上实验，未在更大模型上验证。
- **合成数据偏差**：模型生成指令分布可能与人类实际指令存在差异，尤其难以模拟真实 bug 或错误代码，导致某些任务提升有限。
- **训练成本**：生成 20 个响应和验证对会带来额外的推理开销，对更大规模模型可能成为瓶颈。

（完）

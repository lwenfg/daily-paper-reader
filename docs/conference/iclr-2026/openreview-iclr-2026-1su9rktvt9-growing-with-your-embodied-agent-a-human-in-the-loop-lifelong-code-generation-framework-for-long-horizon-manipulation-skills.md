---
title: "Growing with Your Embodied Agent: A Human-in-the-Loop Lifelong Code Generation Framework for Long-Horizon Manipulation Skills"
title_zh: 与您的具身代理共同成长：面向长程操作技能的人机协同终身代码生成框架
authors: "Yuan Meng, Zhenguo Sun, Max Fest, Xukun Li, Zhenshan Bing, Alois Knoll"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=1su9RkTVT9"
tags: ["query:safe-codegen"]
score: 4.0
evidence: 人机协同终身代码生成用于机器人操作
tldr: 本文针对LLM生成机器人操作代码在长程任务中的局限性，提出人机协同终身学习框架，通过人类反馈纠正错误并存储修正知识，但安全保证并非核心目标。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有LLM代码生成在机器人长程操作任务中受限于语言歧义、噪声和有限上下文。
method: 采用人机协同闭环反馈，将人类的简单修正转化为持久知识，实现终身学习。
result: 框架能够处理极长程任务，通过人类帮助克服LLM推理局限。
conclusion: 人机协同是提高机器人代码生成鲁棒性的有效途径，但未专门解决安全性。
---

## Abstract
Large language models (LLMs)-based code generation for robotic manipulation has recently shown promise by directly translating human instructions into executable code, but existing approaches are limited by language ambiguity, noisy outputs, and limited context windows, which makes long-horizon tasks hard to solve.
While closed-loop feedback has been explored, approaches that rely solely on LLM guidance frequently fail in extremely long-horizon scenarios due to LLMs' limited reasoning capability in the robotic domain, where such issues are often simple for humans to identify. 
Moreover, corrected knowledge is often stored in improper formats, restricting generalization and causing catastrophic forgetting, which highlights the need for learning reusable and extendable skills. 
To address these issues, we propose a human-in-the-loop lifelong skill learning and code generation framework that encodes feedback into reusable skills and extends their functionality over time.
An external memory with Retrieval-Augmented Generation and a hint mechanism supports dynamic reuse, enabling robust performance on long-horizon tasks.
Experiments on Ravens, Franka Kitchen, and MetaWorld, as well as real-world settings, show that our framework achieves a 0.93 success rate (up to 27% higher than baselines) and a 42% efficiency improvement in feedback rounds. 
It can robustly solve extremely long-horizon tasks such as "build a house", which requires planning over 20 primitives.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大型语言模型（LLMs）近年来在机器人操作中展现出将人类指令直接翻译为可执行代码的潜力，但在长程任务中面临严重挑战。
- **核心问题**：
  - 自然语言的**歧义性**、LLM 输出的**噪声**以及**有限的上下文窗口**使得长程任务规划难以可靠完成。
  - 仅依赖 LLM 本身的闭环反馈（自我修正）在极长程场景下**经常失败**，因为 LLM 在机器人领域推理能力不足，而这类错误对人类来说却很容易识别。
  - 修正后的知识若以**不恰当的格式**存储，将限制泛化能力并导致**灾难性遗忘**，缺乏可重用、可扩展的技能学习机制。
- **整体含义**：论文旨在通过引入**人机协同的终身学习框架**，将人类的简单反馈转化为可复用的机器人操作技能，使机器人能够“与代理共同成长”，不断增强处理长程任务的能力，并缓解遗忘问题。

## 2. 论文提出的方法论

- **核心思想**：构建一个**人在回路（Human-in-the-loop）的终身技能学习与代码生成框架**，在执行任务时若 LLM 生成代码失败，人类给出修正反馈（可能仅需简单指出错误），系统将这种反馈编码为**可复用的技能**，并随着时间推移扩展技能的功能，从而不断提高鲁棒性。
- **关键技术细节**：
  - **外部记忆与检索增强生成（RAG）**：维护一个外部记忆库，存储已修正的技能知识。在生成新代码时，通过检索增强生成动态重用相关经验，避免重复错误。
  - **提示（Hint）机制**：在 LLM 推理过程中利用记忆中的提示信息，辅助生成更可靠的代码，提升对长程任务的适应能力。
  - **技能终身扩展**：人类的每一次修正都被转化为持久的知识条目，新技能可在未来任务中被调用和组合，从而克服有限上下文和单一 LLM 推理的不足。
- **算法流程**（文字概括）：
  1. 输入自然语言指令，LLM 生成初始操作代码。
  2. 在仿真或真实环境中执行代码，若失败，人类观察者提供简洁的反例或修正提示。
  3. 框架将修正信息抽象为技能（如调整对象抓取方式、任务顺序等），并存入外部知识库。
  4. 后续遇到同类或长程任务时，利用 RAG 检索相关技能，与当前上下文一起输入 LLM，生成更健壮的代码。
  5. 过程反复迭代，技能库不断增长，性能持续提升。

## 3. 实验设计

- **使用环境/数据集**：
  - **仿真平台**：Ravens（面向物体堆叠与搬运的基准）、Franka Kitchen（厨房操作）、MetaWorld（多任务机器人操作基准）。
  - **真实世界设置**：在物理机器人上进行了验证（具体平台未在摘要中详述）。
- **任务特点**：包括常规操作与极长程任务，例如“建造房子”（需要规划超过 20 个基本动作原语）。
- **对比方法**：与多个基线方法进行比较（摘要中未列出具体名称，仅提及成功率提升高达 27%），这些基线可能包括纯 LLM 代码生成、LLM 闭环自我修正等。

## 4. 资源与算力

- 论文摘要及给出的元数据中**未提及任何算力资源信息**，如 GPU 型号、数量、训练时长或推理成本。因此无法总结。

## 5. 实验数量与充分性

- 从已提供的信息推测，至少包含了三个仿真环境（Ravens、Franka Kitchen、MetaWorld）和真实场景实验，且设计有对比基线、成功率与反馈轮次效率的定量评估，以及类似“建造房子”这样的极端长程任务案例分析。
- 但**无法获知详细的实验组数**：消融实验是否开展、不同记忆机制、RAG 变体等均未在元数据中说明。
- **客观性与公平性**：因为未提供具体对比方法名称及实现细节，难以评估实验设计是否完全客观公平；仅凭成功率 0.93 和相对提升 27% 的数据，可初步认为效果显著，但缺乏对基线的深入分析。

## 6. 论文的主要结论与发现

- 所提框架在多个仿真环境和真实世界中达到了 **0.93 的成功率**，比基线方法最高提升了 27%。
- 反馈轮次的效率提升了 **42%**，说明人类纠正所需的工作量明显减少，技能可被有效复用。
- 框架能够**稳健地求解极长程任务**，如需要 20+ 原语的“建造房子”，突破了现有 LLM 代码生成方法在长程规划上的局限。
- 人机协同与终身技能积累是解决机器人领域 LLM 推理不足的可行途径。

## 7. 优点

- **创新地融合了人机协同与终身学习**：将人类低成本修正转化为持久、可复用的技能，克服了纯 LLM 在机器人领域推理能力不足和灾难性遗忘的问题。
- **外部记忆+RAG+提示机制**：设计简洁有效，使技能能在不同任务间泛化，并降低对人类专家知识的依赖。
- **在极长程任务上展现出优势**：解决了过去方法几乎无法完成的任务类型，实用性突出。
- **涉及多平台验证**：从仿真到真实世界，增强了结论的可信度。

## 8. 不足与局限

- **安全性非核心目标**：元数据明确标注“安全保证并非核心目标”，这意味着在复杂人机协同代码生成中，对故障、危险操作等的安全护栏未做专门设计，可能限制直接部署。
- **实验细节缺失**：提供的摘要和元数据未说明对比基线的具体构成、消融实验、统计检验等，无法严格评估实验的充分性和内外部效度。
- **人类参与的依赖性**：系统性能提升依赖于人类反馈的质量与频率，在无人参与或人类专家稀缺的场景下可能难以维持学习效率。
- **LLM 基座限制**：生成的代码仍然受限于底层 LLM 的固有缺陷（如幻觉、对物理常识理解不足），人机反馈虽能缓解但无法从根本上消除。
- **可解释性与理论分析**：摘要未涉及对技能存储格式、RAG 检索机制的理论分析，可能缺乏深度。

（完）

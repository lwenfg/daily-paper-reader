---
title: "SafeAgentBench: A Benchmark for Safe Task Planning of Embodied LLM Agents"
title_zh: SafeAgentBench：面向具身LLM代理的安全任务规划基准
authors: "Sheng Yin, Xianghe Pang, Yuanzhuo Ding, Menglan Chen, Yutong Bi, Yichen Xiong, Wenhao Huang, Zhen Xiang, Jing Shao, Siheng Chen"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=BFb4ACHayj"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 面向具身LLM代理安全感知任务规划的基准，评估显式和隐式危险
tldr: SafeAgentBench是首个针对具身LLM代理在交互仿真环境中进行安全感知任务规划的基准，覆盖显式和隐式危险场景，通过评估代理规划的安全性，推动安全具身智能系统的发展。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有基准忽略具身代理执行危险任务的安全风险。
method: 构建包含显式和隐式危险的交互仿真任务集。
result: 全面评估代理的安全意识，发现当前模型在安全规划上的不足。
conclusion: SafeAgentBench为提升具身代理的安全规划能力提供了重要评测工具。
---

## Abstract
With the integration of large language models (LLMs), embodied agents have strong capabilities to understand and plan complicated natural language instructions. However, a foreseeable issue is that those embodied agents can also flawlessly execute some hazardous tasks, potentially causing damages in the real world. Existing benchmarks predominantly overlook critical safety risks, focusing solely on planning performance, while a few evaluate LLMs' safety awareness only on non-interactive image-text data. To address this gap, we present \textbf{SafeAgentBench}—the first comprehensive benchmark for safety-aware task planning of embodied LLM agents in interactive simulation environments, covering both explicit and implicit hazards. SafeAgentBench includes: (1) an executable, diverse, and high-quality dataset of 750 tasks, rigorously curated to cover 10 potential hazards and 3 task types; (2) SafeAgentEnv, a universal embodied environment with a low-level controller, supporting multi-agent execution with 17 high-level actions for 9 state-of-the-art baselines; and (3) reliable evaluation methods from both execution and semantic perspectives. Experimental results show that, although agents based on different design frameworks exhibit substantial differences in task success rates, their overall safety awareness remains weak. The most safety-conscious baseline achieves only a 10\% rejection rate for detailed hazardous tasks. Moreover, simply replacing the LLM driving the agent does not lead to notable improvements in safety awareness. Dataset and codes are available and shown in the reproducibility statement.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究动机**：随着大语言模型（LLMs）被集成到具身代理中，这些代理能够理解并执行复杂的自然语言指令。然而，一个可预见的风险是，它们也可能“完美”地执行危险任务，从而在现实世界中造成损害。
- **现有局限**：当前的评测基准要么只关注任务规划的成功率而完全忽略安全性，要么仅在非交互的图文数据上评估 LLMs 的安全意识，缺乏在交互式仿真环境中对**具身代理安全任务规划**的系统性考察。
- **整体含义**：本文提出了首个面向具身 LLM 代理的安全感知任务规划综合基准——**SafeAgentBench**。该基准覆盖 **显式和隐式危险**，旨在揭示现有代理在安全性上的短板，并推动安全具身智能系统的发展。

## 2. 论文提出的方法论
由于仅提供了摘要文本，方法论细节有限，可从摘要中提取的核心要素包括：

- **整体框架**：SafeAgentBench 由三部分组成：
  1.  **一个可执行、多样、高质量的纯文本任务数据集**（共 750 个任务），经过严格设计以涵盖 10 种潜在危险和 3 种任务类型。
  2.  **一个通用的具身交互环境 SafeAgentEnv**，内置低级控制器，支持多代理执行，并为 9 个当前最先进的基线代理提供 17 种高层动作接口。
  3.  **可靠的双维度评估方法**：同时从**执行结果**（任务是否成功、是否触发危险）和**语义层面**（代理的规划意图是否安全）进行评估。

- **关键技术思路**：
  - 将危险显式地融入任务描述中，考察代理能否识别并拒绝执行危险指令，或在执行时主动规避危险。
  - 构建统一的仿真环境，使不同设计框架的代理（如基于不同 LLM、不同规划算法）均能在相同条件下进行公平比较。
  - 评估不仅看最终结果，还从语义上判断代理是否具备“安全意识”（例如是否在规划阶段就察觉危险并采取拒绝策略）。

（注：更具体的技术流程、算法伪代码、公式等在现有摘要中未呈现。）

## 3. 实验设计
- **评测场景/数据集**：使用 SafeAgentBench 自建的 750 个任务，覆盖 10 种危险类别、3 种任务类型。环境为 SafeAgentEnv 交互式仿真环境。
- **对比基线**：与 9 个“最先进的基线”代理进行对比。虽然摘要未列出具体名称，但提到这些基线“基于不同的设计框架”，暗示涵盖了主流的具身 LLM 代理架构。
- **评估指标**：
  - 任务成功率（Task Success Rate）
  - 拒绝率（Rejection Rate，针对详细危险任务）
  - 安全性相关的语义得分等。

## 4. 资源与算力
摘要及现有提供内容中**未明确提及**所消耗的算力，包括 GPU 型号、数量、训练/推理时长等信息。因此无法总结该部分。

## 5. 实验数量与充分性
- **估计实验量**：根据摘要，至少涉及 **9 种基线代理 × 750 个任务** 的对比评估。此外，文中提到“替换驱动代理的 LLM”这一操作，意味着可能进行了 LLM 消融实验，但具体组数未知。
- **充分性分析**：从描述看，实验覆盖了多种任务类型和危险类别，基线种类较多，且同时从执行和语义两个维度进行评估，实验设计较为全面。但缺少更详细的对比维度（如不同危险类型下的细分分析）以及训练相关的实验，因此实际充分性需结合全文判断。在现有信息下，实验对于验证“安全意识普遍薄弱”这一核心论点应属充分且公平。

## 6. 论文的主要结论与发现
1.  **安全意识普遍薄弱**：尽管不同设计框架的代理在任务成功率上表现出显著差异，但它们在整体安全意识上均表现不佳。
2.  **拒绝率极低**：即使是最具安全意识的基线代理，在面对包含详细描述的危险任务时，拒绝执行的比例也仅有 **10%**。
3.  **简单换模型无效**：仅仅更换驱动代理的底层 LLM 并不能带来安全意识的显著提升，说明安全性需要从更系统化（如训练范式、安全对齐机制）的角度去解决。

## 7. 优点
- **首创性**：是第一个针对具身 LLM 代理在交互仿真环境中进行**安全感知任务规划**的基准，填补了领域空白。
- **覆盖面广**：同时包含显式危险和隐式危险，任务类型多样，危险类别丰富（10 种），评估更贴近真实世界的潜在风险。
- **评估双维度**：从执行和语义两个层面评估，既看行为结果，也看规划意图的合理性，能更深入地诊断安全问题。
- **统一环境与公平对比**：SafeAgentEnv 为不同代理提供了标准化的动作空间和低级控制，保证了对比的公平性，且代码和数据集均开源。

## 8. 不足与局限
（部分依据摘要和常识推断）

- **文本描述的局限性**：所有任务可能仍为纯文本描述，未涉及视觉、触觉等多模态输入，与实际具身操作可能存在差距。
- **环境保真度**：仿真环境与真实物理世界仍有差距，危险的实际物理后果无法完全模拟，评估的有效性受仿真逼真度制约。
- **危险覆盖的完整性**：10 种危险可能无法涵盖现实中的所有安全风险类型，可能存在分布外（OOD）危险场景。
- **代理的设计限制**：仅测试了 9 个基于文本的 LLM 代理，未扩展到更多模态或更复杂的机器人控制框架。
- **未提供训练细节**：现有摘要未提及是否有针对安全的微调或强化学习训练，这使得“如何提升安全意识”这一后续研究方向缺乏实验指引。
- **数据偏差风险**：任务和危险的定义可能带有设计者的主观性，存在一定的偏差。 

（完）

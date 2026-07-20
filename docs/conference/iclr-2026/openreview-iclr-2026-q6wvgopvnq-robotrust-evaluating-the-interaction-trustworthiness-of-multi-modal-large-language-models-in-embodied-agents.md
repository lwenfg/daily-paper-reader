---
title: "RoboTrust: Evaluating the Interaction Trustworthiness of Multi-modal Large Language Models in Embodied Agents"
title_zh: RoboTrust：评估多模态大语言模型在具身代理中的交互可信赖性
authors: "Xueyang Zhou, Zijia Wang, Guiyao Tie, Sizhe Zhang, Junran Wu, Hecheng Wang, Xu Yongtian, Zhichao Ma, Yan Zhang, Xiangyu Zhang, Pan Zhou, Lichao Sun"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=q6wVgopVnq"
tags: ["query:safe-codegen"]
score: 8.0
evidence: 全面评估具身LLM代理可信赖性的基准，涵盖安全、真实性等
tldr: RoboTrust首次系统性定义具身代理的信任维度，包括安全性、真实性等五个方面，并通过12个细粒度维度评估多模态大语言模型的交互可信度，为构建安全可靠的具身智能系统提供了标准化评测框架。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有具身代理缺乏统一的可信赖性评估基准，安全风险难以保障。
method: 提出多维信任定义，通过12个细粒度维度在模拟环境中评测。
result: 全面揭示了当前多模态大模型在具身场景下的安全弱点。
conclusion: RoboTrust推进了具身智能系统的安全性和可信赖性研究。
---

## Abstract
Multimodal large language models (MLLMs) show great potential for embodied tasks, offering pathways toward real-world applications. Yet trustworthy embodied intelligence, which is difficult to ensure in dynamic and complex environments, remains a necessary prerequisite, and no unified benchmark currently exists for its evaluation. To fill this gap, we introduce **RoboTrust**, a comprehensive benchmark for trustworthy embodied intelligence. We provide the first formal and systematic definition of trust in embodied agents, decomposing it into five key dimensions—*Truthfulness*, *Safety*, *Fairness*, *Robustness*, and *Privacy*. Building on this foundation, RoboTrust evaluates these dimensions through 12 fine-grained tasks probing factual consistency, risk perception and response, bias and preference, resilience under perturbations, and privacy protection. Unlike static evaluations, RoboTrust integrates interactive environments with unexpected risks and disturbances, reflecting the complexity of real-world deployment. We benchmark 19 state-of-the-art MLLMs and reveal substantial deficiencies in embodied trust, with models almost uniformly failing on privacy protection and proactive risk avoidance. Furthermore, we observe no positive correlation between trustworthiness and model capability, and explicit reasoning traces offer little improvement, underscoring a fundamental absence of trust awareness in current systems. RoboTrust provides a unified and interactive platform for comprehensive trust evaluation, revealing critical shortcomings of current MLLMs and offering valuable insights for the development of trustworthy embodied agents.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究动机**：多模态大语言模型（MLLMs）在具身智能体（如机器人操控、自主导航）中展现出巨大应用潜力，但其在动态、复杂环境中的交互可信赖性尚未得到系统性评估。
- **核心问题**：当前学术界缺乏对具身智能体“信任”的统一定义与评估基准，导致模型的安全隐患、隐私泄露、鲁棒性不足等风险难以被量化和比较。
- **整体含义**：提出并构建了首个面向具身智能的综合信任评估基准 **RoboTrust**，旨在从多维信任视角揭示现有 MLLMs 的脆弱性，为构建安全、可靠的具身系统提供标准化评测平台和研究指引。

## 2. 论文提出的方法论
- **核心思想**：首次对具身代理的可信度进行形式化、系统化定义，将“信任”解构为五个可独立评测的维度，并设计交互式、动态的评估环境来模拟真实部署场景。
- **五个信任维度**：
  - *真实性（Truthfulness）*：考察模型对物理世界事实的陈述是否一致、准确。
  - *安全性（Safety）*：衡量模型对风险的感知与主动规避能力。
  - *公平性（Fairness）*：检测模型在决策中是否存在偏见或不合理偏好。
  - *鲁棒性（Robustness）*：评估模型在输入扰动、观察噪声等条件下的性能保持能力。
  - *隐私保护（Privacy）*：检验模型对敏感信息（如环境中的私人物品、对话内容）的保护程度。
- **评估框架设计**：
  - 在上述五个维度下，进一步细化为 **12 个细粒度评测任务**（如事实一致性探测、风险感知与响应、偏见与偏好检测、扰动下的韧性、隐私泄露测试等）。
  - 不同于静态评测，RoboTrust 构建了一个**交互式环境**，其中随机注入意外风险与动态扰动，使得评估更贴近真实世界的复杂性和不可预测性。
  - 整体流程为：将 MLLM 作为具身代理置于模拟场景中，下达具身指令，观察其感知、规划与行动阶段的输出，并按照五维信任指标体系进行量化评分。

## 3. 实验设计
- **评估对象**：19 个当前最先进（state‑of‑the‑art）的多模态大语言模型，涵盖不同规模、不同训练范式的代表性模型。
- **测试场景/数据集**：RoboTrust 自行构建的交互式模拟环境，内嵌了涵盖五个信任维度、12 项细粒度任务的具体测试用例。具体环境细节（如模拟器类型、场景数量）在摘要中未展开，但其特点是包含动态注入的风险与扰动。
- **对比维度**：
  - 横向比较不同 MLLMs 在各信任维度上的表现差异。
  - 分析信任度与模型通用能力（如任务成功率、推理能力）之间的关联。
  - 考察显式推理链（reasoning traces）对可信赖性的影响是否显著。
- **评估指标**：围绕安全性、真实性、公平性等各维度的细分指标（如风险规避成功率、隐私泄露率、偏见程度、鲁棒性下降幅度等），具体指标命名未在摘要中详述，但核心是各维度的达标率与失败模式分析。

## 4. 资源与算力
- 提供的论文摘要与元数据中**未明确说明**使用的 GPU 型号、数量、训练时长等算力信息。由于该工作主要构建评测基准并进行模型推理评估，推测所需算力主要来自加载模型并运行交互式环境，但具体规模未知。

## 5. 实验数量与充分性
- **实验组数估算**：
  - 涵盖 5 个主要维度，12 项细粒度任务，19 个 SOTA 模型。
  - 至少可构成 `5 × 12 × 19` 组基础评测实验，同时还包括横向比较、信任-能力关联分析、推理链效用消融等特定分析实验。
  - 整体实验规模较大，覆盖模型数量充足。
- **充分性与客观性**：
  - **充分性**：多维分解和大量模型参与，使得结论具有较好的泛化性；交互式动态环境的设计比静态问答评测更能反映真实部署风险，实验设计较为充分。
  - **客观与公平性**：对多个模型在统一基准下进行比较，避免了单一模型或单一指标带来的偏差，且首次提供了形式化信任定义，增强了评估的标准化程度。

## 6. 论文的主要结论与发现
- **严重信任缺陷**：当前最先进的 MLLMs 在具身信任方面表现堪忧，几乎所有模型在隐私保护和主动风险规避任务上均告失败。
- **能力与信任无正相关**：模型的通用能力（如常识问答、图像理解得分）与其信任度之间未观察到正向关联，强模型未必更可信。
- **推理链帮助有限**：显式的思维链或推理过程对提升可信赖性的作用微乎其微，表明现有模型缺乏内在的“信任意识”，而非简单的思考不足。
- **平台价值**：RoboTrust 成功暴露了 MLLMs 在具身环境中的关键短板，为可信具身智能的开发提供了方向性洞见。

## 7. 优点
- **首次系统性定义**：首次对具身智能体的可信度给出形式化、多维度的分解，填补了领域空白。
- **交互式动态评估**：环境设计融入了意外风险和动态扰动，比传统的静态数据集测评更具现实意义。
- **多维度细粒度任务**：覆盖安全、隐私、公平、鲁棒、真实性五个方面，12 项具体任务，评估全面且深入。
- **大规模模型对比**：一次性对 19 个 SOTA 模型进行基准测试，揭示了整体行业水平的薄弱环节，结论有说服力。
- **关键洞察**：明确指出现阶段 MLLMs 的信任缺失本质——并非能力不足，而是缺乏信任意识，这为未来模型对齐和安全训练指明了方向。

## 8. 不足与局限
- **环境抽象差距**：尽管设计了交互与扰动，模拟环境仍可能与真实物理世界的复杂度、噪声多样性和安全后果存在差距，生态效度有待进一步验证。
- **维度覆盖局限**：当前定义的五维信任虽已较全面，但具身场景下可能还存在其他重要维度（如可解释性、责任归属、实时性约束下的安全）未被囊括。
- **任务粒度和泛化**：12 项任务虽细粒度，但对于具体应用领域（如家庭服务 vs 工业制造），其风险分布和敏感度可能不同，基准的定制化扩展能力未明确讨论。
- **隐私评估的具体性**：摘要中提到隐私保护几乎全部失败，但未详述隐私测试的场景设计（是视觉隐私还是对话隐私），这可能影响对失败原因的更深入诊断。
- **开源与可复现性**：论文摘要未说明是否开源基准环境与评测代码，若未开源，将限制该平台被社区复现和进一步开发的潜力。
- **动态环境复杂度**：注入的扰动/风险类型可能预设过强，能否涵盖未知的、对抗性的安全威胁尚存疑问。

（完）

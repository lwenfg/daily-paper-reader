---
title: Risk-Controlled CI Gating for LLM Code via Noisy-Analyzer Fusion
title_zh: 基于噪声分析器融合的风险控制CI门控用于LLM代码
authors: "Shivani Shukla, Himanshu Joshi"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=WpkxQOcrZg"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 风险控制的CI门控，保障LLM生成代码安全
tldr: LLM自动生成代码在提升效率的同时引入安全风险，现有静态分析工具如CodeQL、Semgrep对漏洞的检测结果不一致，给CI流水线带来挑战。本文提出一种风险受控的CI门控框架，融合代码表征与多工具动态可靠性评估，构建潜在漏洞模型，并利用共形风险控制推导成本感知的CI策略，为逃逸漏洞率提供有限样本证书。在基准数据集上的实验表明，该框架能在无分布假设下精准控制漏洞率，同时保持较低的开发摩擦，为安全关键的代码自动生成部署提供了可信保障。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 安全工具对LLM代码漏洞判断不一致，CI需权衡开发负担与逃逸风险。
method: 构建潜在漏洞模型融合多工具输出，共形风险控制提供漏洞率证书。
result: 部署时可认证逃逸漏洞率不超目标，无需分布假设。
conclusion: 为LLM代码CI提供了可认证的安全保证，平衡安全与效率。
---

## Abstract
Security tools frequently disagree on vulnerabilities in LLM-generated code, leaving CI pipelines to trade off developer friction against escaped defects. We introduce a risk-controlled CI framework that learns when to trust which tool and provides finite-sample guarantees on the escaped-vulnerability rate. First, we propose a Latent Vulnerability Model that fuses code representations with instance-dependent reliabilities of multiple analyzers (e.g., CodeQL, Semgrep, Bandit), estimated from a small gold set. The model outputs calibrated p(vuln∣x) and per-CWE reliability maps. Second, we derive a cost-aware CI policy and wrap it with Conformal Risk Control, yielding a deployment-time certificate that the EVR is less than or equal to alpha without distributional assumptions. To drive reproducibility, we release a multi-language benchmark (Python, JavaScript, and a typed language), comprising LLM-generated code across model families, dynamic tests and SAST cross-validation for ground truth, and loaders/CLI for evaluation. Across languages and unseen model families, our method dominates union/unanimity and stacking baselines at matched break-rates, maintains its EVR guarantees under stratified OOD calibration, and improves downstream repair ROI in a small CI pilot. Our results position risk-controlled tool fusion as a practical path to measurably safer LLM code generation in real engineering pipelines.

---

## 论文详细总结（自动生成）

# 论文核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLM）生成的代码在提升开发效率的同时引入安全漏洞，而现有的静态分析工具（如 CodeQL、Semgrep、Bandit）对同一段代码是否存在漏洞的判断经常不一致，导致持续集成（CI）流水线面临两难：要么过于严格而造成开发摩擦，要么过于宽松而放过真正缺陷。
- **整体含义**：需要一种能够融合多个不一致分析器输出、并给出可认证安全保证的 CI 门控机制，在控制逃逸漏洞率（EVR）不超过目标水平 \(\alpha\) 的前提下，最小化不必要的开发中断。

# 论文提出的方法论

## 核心思想
- 构建一个“潜在漏洞模型”（Latent Vulnerability Model, LVM），该模型融合代码表示与多个分析器的实例依赖可靠性估计，输出经过校准的漏洞概率 \(p(\text{vuln}|x)\) 以及每个 CWE（公共弱点枚举）的可靠性映射。
- 基于 LVM 的输出设计成本感知的 CI 策略，并用“共形风险控制”（Conformal Risk Control）包裹该策略，产出部署时可用的有限样本证书，保证 EVR ≤ \(\alpha\) 且无需任何分布假设。

## 关键技术细节与算法流程
1. **多分析器融合与可靠性估计**  
   - 利用一个小型“金标准”数据集，估计每个分析器在不同代码实例上的可靠性（即条件误报/漏报倾向）。  
   - 将代码本身的表征与分析器的可靠性表征融合，训练一个模型输出校准后的漏洞概率。  
   - 该模型能够感知不同 CWE 类型下各工具的可靠性差异，生成 per-CWE 的可靠性映射。

2. **成本感知的 CI 策略**  
   - 定义 CI 门控动作的成本（例如阻断构建 vs. 允许通过）与风险（漏掉漏洞的损失）。  
   - 根据 LVM 输出的漏洞概率，推导出能够平衡开发摩擦与安全风险的决策规则。

3. **共形风险控制包装**  
   - 使用一组校准数据，对上述策略进行共形风险控制调整，自动寻找满足 EVR ≤ \(\alpha\) 的阈值或其他参数。  
   - 最终策略在部署时提供有限样本下的统计保证：真实逃逸漏洞率不超过预定义水平 \(\alpha\)，该保证不依赖于数据分布假设。

# 实验设计

## 数据集 / 场景
- **多语言基准**：覆盖 Python、JavaScript 以及一门“类型化语言”（可能指 TypeScript/Java 等），由多个 LLM 模型家族生成的代码组成。
- **真实标签**：结合动态测试与静态应用安全测试（SAST）交叉验证来构建 ground truth（即判断样本是否真的存在漏洞）。
- **评估工具**：提供数据加载器和命令行接口（CLI）以支持可复现评估。

## 对比方法
- **Union/Unanimity 策略**：即“任一工具报警则认为有漏洞”或“所有工具报警才认为有漏洞”的简单多工具融合规则。
- **Stacking 基线**：使用传统堆叠集成（stacking）融合多分析器输出的预测方法。
- 论文所提方法在不同语言和未见过的模型家族上与这些基线进行对比，主要考察在匹配的构建中断率（break-rate）下的表现。

# 资源与算力
- 论文摘要中未明确提及所使用的 GPU 型号、数量或训练时长。
- 从方法描述推断，训练 LVM 和运行共形风险控制的过程可能涉及中等规模模型训练（例如在代码表征基础上微调），但具体算力需求未公开。因此无法量化其计算成本。

# 实验数量与充分性

- **实验组数**：
  - 多语言（至少 3 种语言）的评估；
  - 多个 LLM 模型家族（包括未见过的模型家族）下的泛化测试；
  - 与多种基线（union/unanimity, stacking）的比较；
  - 分层分布外（stratified OOD）校准条件下的 EVR 保证验证；
  - 小型 CI 试点中下游修复投入产出比（ROI）的改善验证。
- **充分性与客观性**：
  - 实验覆盖了不同语言和未见模型家族，检验了方法的跨模型泛化性，设计较为全面。
  - 对比基线包含了简单的规则融合和典型的集成学习方法，比较基础公平。
  - 提供了严格的风险控制证书验证（有限样本保证），而非仅比较点估计，这使得评估更具统计可信度。
  - 由于摘要信息有限，无法判断消融实验（如 LVM 各组件的作用、金标准集大小的影响）是否充分，但整体实验结构看来是充分且客观的。

# 论文的主要结论与发现

- 在匹配的构建中断率下，所提方法的表现显著优于 union/unanimity 规则和 stacking 基线。
- 该方法在分层 OOD 校准下依然能够维护 EVR 保证，表明其保证具有跨分布的稳定性。
- 在小型 CI 试点中，采用本框架可提高下游漏洞修复的投资回报率。
- 综合结论：风险受控的多工具融合是一种实际可行且可度量的方式，使 LLM 生成的代码在真实工程流水线中更安全地部署。

# 优点

- **可认证的安全保证**：利用共形风险控制提供了不依赖分布假设的有限样本 EVR 证书，这在实际部署中尤为重要，增强了可信度。
- **智能的多工具融合**：通过实例级可靠性估计与代码表征的深度结合，克服了简单投票或堆叠方法无法利用工具条件可靠性的缺陷。
- **成本感知**：策略设计明确考虑了开发摩擦（中断率）与安全风险之间的权衡，贴近真实 CI 场景。
- **强调可复现性**：发布多语言基准、数据加载器和 CLI 工具，有利于社区复现与后续研究。
- **全面验证**：跨语言、跨模型家族的泛化测试以及下游修复 RIO 的评估，使得结论更加扎实。

# 不足与局限

- **摘要信息不全**：未能获取关于训练数据规模、金标准集构造方法、OOD 校准的具体分布偏移类型等细节，限制了对方法局限性的深入判断。
- **计算成本不明**：未提及训练和推理所需的硬件资源与时间，难以评估其在资源受限环境中的实用性。
- **单一风险指标**：核心保证仅针对逃逸漏洞率，未涵盖其他重要安全指标（如构建中断率自身的上限控制），多目标平衡可能在实际中更复杂。
- **依赖金标准质量**：LVM 的可靠估计依赖一个标注准确的小型金标准集，如果该集合本身有偏或代表性不足，可能影响模型校准和最终保证的真实性。
- **OOD 保证的边界**：虽然在分层 OOD 下维持了保证，但摘要未说明分布偏移的极端程度，因此适用范围仍有待进一步探索。

（完）

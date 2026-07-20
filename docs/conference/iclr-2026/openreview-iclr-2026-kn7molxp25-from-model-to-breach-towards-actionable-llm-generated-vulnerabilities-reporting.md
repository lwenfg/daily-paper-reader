---
title: "From Model to Breach: Towards Actionable LLM-Generated Vulnerabilities Reporting"
title_zh: 从模型到漏洞：走向可操作的LLM生成漏洞报告
authors: "Andrei Kucharavy, Alexander Sternfeld, Cyril Vallez, Ljiljana Dolamic"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=kn7MOLXP25"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 提出针对LLM生成代码的可操作漏洞报告
tldr: 本文评估了LLM生成代码中的漏洞，指出当前模型在现实场景中仍存在已被发现的漏洞，并提出一种反映风险的新严重性度量，以改善可操作报告，从而增强生成代码的安全性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM代码助手广泛使用，但其生成代码的安全性影响不明，现有基准和改进并未有效消除漏洞。
method: 在现实设置中测试最新开源模型在早期漏洞场景下的表现，并引入新的严重性度量来反映风险。
result: 表明即使最新模型仍易受早期漏洞攻击，安全与功能权衡阻碍了有效修补。
conclusion: 提出的严重性度量有助于生成更具可操作性的漏洞报告，推动LLM代码安全改进。
---

## Abstract
As the role of Large Language Models (LLM)-based coding assistants in software development becomes more critical, so does the role of the bugs they generate in the overall cybersecurity landscape. 
While a number of LLM code security benchmarks have been proposed alongside approaches to improve the security of generated code, it remains unclear to what extent they have impacted widely used coding LLMs. 
Here, we show that even the latest open-weight models are vulnerable in the earliest reported vulnerability scenarios in a realistic use setting, suggesting that the safety-functionality trade-off has until now prevented effective patching of vulnerabilities. 
To help address this issue, we introduce a new severity metric that reflects the risk posed by an LLM-generated vulnerability, accounting for vulnerability severity, generation chance, and the formulation of the prompt that induces vulnerable code generation - Prompt Exposure (PE). 
To encourage the mitigation of the most serious and prevalent vulnerabilities, we use PE to define the Model Exposure (ME) score, which indicates the severity and prevalence of vulnerabilities a model generates.

---

## 论文详细总结（自动生成）

# 论文详细总结：从模型到漏洞：走向可操作的LLM生成漏洞报告

## 1. 论文的核心问题与整体含义（研究动机和背景）
*   **研究背景**：基于大语言模型（LLM）的代码助手（如GitHub Copilot、Code Llama等）在软件开发中日益普及，其生成代码中存在的安全漏洞对整个网络安全格局构成潜在威胁。
*   **核心问题**：尽管已经提出了一些针对LLM代码安全性的基准测试和改进方法，但目前尚不清楚这些工作对广泛使用的编码LLM产生了多大的实际影响。现有基准和改进似乎并未有效消除生成代码中的已知漏洞。
*   **整体含义**：论文试图揭示LLM生成代码安全性的现状，即在真实使用场景下，即使是**最新的开源模型仍会生成早期已发现的漏洞**，这暗示着安全性与功能性之间的权衡阻碍了漏洞的有效修复。作者旨在通过引入可操作的漏洞报告度量来推动安全性改进。

## 2. 论文提出的方法论
*   **核心思想**：设计一种新的严重性度量，不仅考虑漏洞本身的技术严重程度，还结合**漏洞生成的概率**以及**诱导模型生成易受攻击代码的提示特征**，从而更准确地反映LLM生成的漏洞所带来的真实风险。
*   **关键度量指标**：
    *   **提示暴露度（Prompt Exposure, PE）**：一个衡量由特定提示（prompt）诱导出的漏洞所带来风险的指标。它综合了三个维度：
        1.  漏洞本身的严重性（Vulnerability Severity）；
        2.  该漏洞被模型生成的概率（Generation Chance）；
        3.  诱导易受攻击代码生成的提示构造方式（Prompt Formulation）。
    *   **模型暴露度（Model Exposure, ME）**：基于PE定义的评分，用于量化一个模型生成漏洞的**严重性和普遍性**。它旨在引导社区优先缓解最严重、最普遍的漏洞。
*   **技术流程**：在真实的编码助手下使用场景中，向最新的开源LLM提交包含早期已知漏洞模式的提示，观察其是否仍生成易受攻击的代码；基于这些观察结果计算PE和ME评分。

## 3. 实验设计
*   **数据集/场景**：
    *   采用**真实的使用设置**（realistic use setting）模拟开发者使用编码助手的情境。
    *   使用**早期已报告的漏洞场景**作为测试用例，即已知的、历史较久的漏洞类型。
*   **评估对象**：
    *   **最新的开源权重模型**（latest open-weight models），具体模型名称未在提供的文本中列出。
*   **对比方法**：
    *   文中未明确说明与哪些具体的安全改进方法或基准进行了对比，但可以推断其对比了模型生成代码中的漏洞是否依然存在，并以此来质疑现有安全基准和改进方法的有效性。

## 4. 资源与算力
*   论文摘要及元数据中**未提及**使用的GPU型号、数量或训练时长等算力相关信息。推测该工作主要为推理测试而非训练大量模型，因此可能未强调算力需求。

## 5. 实验数量与充分性
*   **实验规模**：
    *   仅根据现有信息，无法判断做了多少组实验（如不同数据集、消融实验等）。文中仅提到“展示即使最新模型在最早报告的漏洞场景下仍易受攻击”，暗示可能进行了一系列跨模型、跨漏洞类型的测试，但未提供具体组数。
*   **充分性与客观性评估**：
    *   **充分性**：由于论文正文（PDF内容）不可见，无法准确评估。从摘要看，实验似乎聚焦于重现漏洞现象，并提出了新度量，但具体实验设计、统计显著性、泛化性等细节不明。
    *   **客观公平性**：选择早期漏洞进行测试，可客观检验模型是否吸取了历史经验，但可能忽略了新类型漏洞。对比方法不详，公平性难以定论。

## 6. 论文的主要结论与发现
*   **漏洞重现**：在现实使用场景下，**最新的开源LLM仍然会生成早期已知的、本该被修复的漏洞**。
*   **权衡障碍**：安全性与功能性之间存在权衡，导致这些漏洞至今未能得到有效修补。
*   **度量改进**：新提出的**提示暴露度（PE）和模型暴露度（ME）** 能够更好地反映漏洞风险，有助于生成更具可操作性的漏洞报告，从而推动LLM代码安全性的实际提升。

## 7. 优点
*   **问题视角新颖**：不满足于单纯检测漏洞，而是关注**漏洞报告的可操作性**及其对安全实践的促进作用。
*   **风险度量创新**：提出的PE和ME将漏洞严重性、生成概率和提示特性结合，比仅看单一漏洞等级更能体现真实世界中的风险暴露。
*   **现实导向**：在真实使用设置下测试，增强了结论的实用价值，并指出了安全与功能权衡这一深层问题。

## 8. 不足与局限
*   **信息缺失**：由于提供的论文内容仅为验证页面，无法获取完整的实验细节、图表和讨论，因此无法评估其方法的严谨性和复现性。
*   **实验覆盖可能不足**：仅提及早期漏洞场景，可能未涵盖最新漏洞类型或复杂多步攻击场景。
*   **度量主观性**：PE/ME中关于“提示构造方式”等要素的量化可能存在主观性或依赖特定模板，泛化性有待验证。
*   **实际影响未验证**：提出可操作报告是目标，但未提供证据表明这些报告确实被开发者或安全社区采信并产生了修复效果。
*   **算力与环境**：算力信息完全缺失，无法评估实验成本。

（完）

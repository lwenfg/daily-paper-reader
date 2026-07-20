---
title: "FHE-Coder: Benchmarking Secure Agentic Code Generation for Fully Homomorphic Encryption"
title_zh: FHE-Coder：面向全同态加密的安全代理式代码生成基准
authors: "Mayank Kumar, Jiaqi Xue, Mengxin Zheng, Qian Lou"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=4F1py5vQXm"
tags: ["query:safe-codegen"]
score: 8.0
evidence: 安全生成全同态加密代码并强制安全性
tldr: 针对全同态加密代码生成中语义模糊、API误用和密码学不安全等失败模式，提出三阶段代理框架FHE-Coder，通过提示形式化、检索增强生成和验证模块强制安全参数化，实验表明可生成安全可靠的FHE代码，降低了密态计算的实际应用门槛。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 全同态加密代码生成需要专业密码学知识且易出错，现有LLM代理存在安全失败模式。
method: 提出三阶段代理框架FHE-Coder，集成Prompt Formalizer、RAG模块和验证器，强制安全参数化并避免API误用。
result: 该框架能够生成安全可靠的FHE代码，提升实用性。
conclusion: FHE-Coder为密态计算的安全代码生成提供了有效解决方案。
---

## Abstract
Fully Homomorphic Encryption (FHE) is a foundational technology for confidential computing, yet its practical adoption remains limited by the need for specialized cryptographic expertise and error-prone parameter configuration. To lower this barrier, we investigate whether Large Language Model (LLM) agents can reliably generate secure FHE code from natural-language specifications. We present FHE-Coder, a three-phase agentic framework that addresses the key failure modes of FHE code generation: semantic ambiguity, API misuse, and cryptographic insecurity. The framework integrates (1) a Prompt Formalizer that structures user intent and enforces secure parameterization, (2) a specialized retrieval-augmented generation (RAG) module that supplies scheme-specific API and documentation knowledge, and (3) an automated Security Verifier that performs iterative validation and feedback to detect and correct cryptographic flaws. We evaluate FHE-Coder across four leading LLMs on a benchmark of ten FHE programming tasks spanning increasing functional and security complexity. While baseline agents frequently produce code that compiles and passes functional tests, they often violate security constraints or misuse cryptographic parameters. In contrast, FHE-Coder consistently generates solutions that are compilable, functionally correct, and verifiably secure across schemes including TFHE and CKKS. Our work establishes a systematic methodology and benchmark for agentic FHE code generation, providing a practical step toward democratizing secure computation without compromising cryptographic guarantees.

---

## 论文详细总结（自动生成）

# FHE-Coder 论文详细总结

## 1. 论文的核心问题与整体含义
- **研究背景**：全同态加密（FHE）是实现机密计算的核心技术，允许在加密数据上直接进行计算。但其实际应用受到严重阻碍，原因是需要极专业的密码学知识，且参数配置极易出错。
- **核心问题**：能否利用大语言模型（LLM）代理，从自然语言描述中可靠地生成安全的 FHE 代码？当前 LLM 直接生成 FHE 代码存在三类典型失败模式：语义歧义、API 误用和密码学不安全。
- **整体含义**：论文旨在降低密态计算的门槛，让非密码学专家也能安全地使用 FHE。通过提出一个系统化的代理框架和基准，保证代码生成的功能正确性与密码学安全性，从而推动安全计算的民主化。

## 2. 论文提出的方法论
FHE-Coder 是一个三阶段的代理式框架，专门解决 FHE 代码生成中的关键失败模式。
- **核心思想**：将自然语言需求转化为可验证的安全 FHE 代码，在流程中强制安全参数化并避免 API 误用。
- **三个关键模块**：
    - **Prompt Formalizer（提示形式化器）**：将模糊的用户意图结构化为明确的形式化提示，并强制实施安全的参数化要求，例如规定安全位数、密钥长度等。
    - **RAG 模块（检索增强生成）**：一个专用的检索增强生成模块，为具体的 FHE 方案（如 TFHE、CKKS）提供精确的 API 文档和领域知识，解决 API 误用问题。
    - **Security Verifier（安全验证器）**：自动执行迭代验证与反馈，检测并纠正密码学缺陷，确保生成的代码不仅在功能上正确，而且在密码学上是安全的。
- **算法流程**（文字说明）：用户自然语言描述 → Prompt Formalizer 形式化 → RAG 模块注入方案特定知识 → LLM 生成代码 → Security Verifier 自动验证并反馈缺陷 → 迭代修正直至通过验证。

## 3. 实验设计
- **数据集/场景**：构建了一个包含 10 个 FHE 编程任务的基准测试集，任务涵盖逐渐增加的功能复杂度和安全复杂度。
- **对比方法**：对比了未使用 FHE-Coder 框架的基线 LLM 代理（直接生成代码的普通代理）。
- **测试的 LLM**：在四种主流大语言模型上进行了评估。
- **评估方案**：涵盖 TFHE 和 CKKS 等不同 FHE 方案，评估指标包括可编译性、功能正确性和密码学安全性。

## 4. 资源与算力
- 论文摘要及所提供文本中**未明确说明**使用的计算资源，如 GPU 型号、数量、训练时长等。文中仅提到在四种主流 LLM 上进行评估，未涉及模型训练或微调，可能是基于 API 调用或本地推理，但具体算力未提及。

## 5. 实验数量与充分性
- **实验规模**：在至少 10 个不同复杂度的编程任务上，对 4 种 LLM 进行了框架与基线的对比测试，构成多组实验（约 4×10×2 种配置以上）。此外还包含针对不同 FHE 方案（TFHE、CKKS）的评估。
- **充分性**：实验覆盖了功能复杂度和安全复杂度的梯度变化，并通过编译、功能测试、安全性验证等多维度评估，较为全面。对比基线清晰，能突出框架在安全性上的优势。但摘要未提及消融实验、多次重复实验的稳定性或统计显著性检验，无法判别是否完全排除随机性影响。整体看实验设计合理、对比公平。

## 6. 论文的主要结论与发现
- 基线 LLM 代理经常能够生成可编译并通过功能测试的代码，但普遍违反安全约束或误用密码学参数。
- FHE-Coder 框架能够持续生成可编译、功能正确且经过验证安全可靠的 FHE 代码，在 TFHE 和 CKKS 方案上均有效。
- 该工作建立了一个系统化的方法论和基准，为代理式 FHE 代码生成提供了实用路径，在降低使用门槛的同时不牺牲密码学保障。

## 7. 优点
- **安全性强制**：将密码学安全验证融入生成循环，这是区别于一般代码生成的关键亮点。
- **模块化设计**：提示形式化、RAG、安全验证三模块分工明确，可灵活适配不同 FHE 方案。
- **实际基准**：提供了首个面向 FHE 代码生成且同时关注功能与安全性的基准，填补领域空白。
- **多方案支持**：在 TFHE 和 CKKS 两种主流方案上验证，显示框架的泛化能力。

## 8. 不足与局限
- **实验覆盖面有限**：仅 10 个编程任务，可能不足以覆盖真实 FHE 应用的多样性。
- **未提及资源开销**：无任何关于推理时长、计算消耗的数据，实际应用成本未知。
- **偏差风险**：RAG 模块和安全验证器自身的规则设计可能引入特定方案或 API 版本的偏好，若规则不完善则可能漏检。
- **应用限制**：仅聚焦代码生成阶段，未涉及部署后的实际安全审计或侧信道风险；且依赖特定 LLM 的底层能力。
- **消融与稳健性未明**：摘要未展示各模块的独立贡献或多次重复实验结果，结论的稳健性有待进一步确认。

（完）

---
title: "OSS-Bench: Evaluating LLMs via the Realistic Open-Source Software Development Pipeline"
title_zh: OSS-Bench：通过现实开源软件开发流程评估大语言模型
authors: "Yuancheng Jiang, Roland Yap, Zhenkai Liang"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=CkxjXuI7LL"
tags: ["query:safe-codegen"]
score: 8.0
evidence: 基准评估LLM生成代码的内存安全问题，关注生成代码的安全性
tldr: OSS-Bench从开源软件中自动构建评估任务，通过可编译性、功能正确性和内存安全性等指标，全面衡量LLM生成代码的质量，尤其关注低层安全缺陷，为提升自动代码生成的安全性提供了现实场景测试。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有基准忽视低层安全评估，特别是内存安全问题。
method: 从开源项目自动构建实时评测任务，替换函数为LLM生成代码。
result: 使用可编译性、功能测试和内存安全三个新颖指标进行评测。
conclusion: OSS-Bench为在真实开源环境中评估生成代码安全性提供了可扩展的方案。
---

## Abstract
In light of the rapid adoption of AI coding assistants, LLM-assisted development has become increasingly prevalent, creating an urgent need for robust evaluation of generated code quality. Existing benchmarks often require extensive manual effort to create static datasets, rely on indirect or insufficiently challenging tasks, depend on non-scalable ground truth, or neglect critical low-level security evaluations, particularly memory-safety issues. In this work, we introduce OSS-Bench, a benchmark generator that automatically constructs large-scale, live evaluation tasks from real-world Open-Source Software (OSS). OSS-Bench replaces functions with LLM-generated code and evaluates them using three novel metrics: compilability, functional correctness, and memory safety, leveraging robust signals like compilation failures, test-suite violations, and sanitizer alerts as ground truth. In our evaluation, the benchmark, instantiated as OSS-Bench(php) and OSS-Bench(sql), profiles 17 diverse LLMs at million-scale tasks, revealing insights such as intra-family behavioral patterns and inconsistencies between model size and performance. Our results demonstrate that OSS-Bench mitigates overfitting by leveraging the evolving complexity of OSS and highlight LLMs' limited understanding of low-level code security via extended fuzzing experiments. Overall, OSS-Bench offers a practical and scalable framework for benchmarking the real-world coding capabilities of LLMs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：随着AI编码助手（如Copilot等）的迅速普及，大语言模型（LLM）生成代码的质量评估变得紧迫。现有基准测试存在以下不足：
  - 依赖大量人工构建静态数据集，难以扩展且容易过时。
  - 采用间接或缺乏挑战性的任务，无法真实反映软件开发场景。
  - 评估标准（ground truth）难以规模化获取。
  - **严重忽视低层安全评估，特别是内存安全问题**，而这在C/C++等系统级语言中至关重要。
- **整体含义**：OSS-Bench旨在通过自动从真实开源软件（OSS）构建实时、大规模的评估任务，弥补现有基准在可扩展性、真实性和安全性评估上的缺失，为测量LLM在现实开发流程中的编码能力提供实用框架。

### 2. 论文提出的方法论

- **核心思想**：将开源项目中的现有函数替换为LLM生成的代码，并直接在项目的真实构建与测试环境中进行验证，从而评估生成代码的质量。
- **关键技术细节**：
  - **自动化任务构建**：自动从开源软件仓库中提取函数接口与上下文，生成需要LLM补全的函数级任务（benchmark generator）。
  - **评估指标（三个新颖指标）**：
    1. **可编译性（Compilability）**：生成的代码能否通过项目的编译流程，利用编译失败信号作为判定依据。
    2. **功能正确性（Functional Correctness）**：生成的代码是否通过项目现有的测试套件（test-suite violations）来检验功能是否符合预期。
    3. **内存安全性（Memory Safety）**：通过Sanitizer（如AddressSanitizer）等工具在运行时检测代码是否存在内存错误（如缓冲区溢出、use-after-free等），以Sanitizer报警作为ground truth。
  - **评估流程**：函数替换 → 编译验证 → 运行测试套件 → 内存安全检测，形成一个端到端的自动化流水线。
- **无明确公式或算法伪代码**：文中摘要未给出详细数学公式，但整体流程基于软件工程中的持续集成（CI）管线思想。

### 3. 实验设计

- **基准实例化**：OSS-Bench以两个具体子基准呈现：
  - **OSS-Bench(php)**：基于PHP解释器源码构建的任务。
  - **OSS-Bench(sql)**：基于SQL相关项目（如SQLite等）构建的任务。
  - 这两个实例化都属于百万级任务规模（million-scale tasks），表明自动提取了大量函数级替换点。
- **对比方法**：对**17种多样的LLM**进行了评估（文中未列出具体模型名称，可能是GPT系列、LLaMA、CodeLlama、StarCoder等主流代码模型）。
- **额外评估**：通过**扩展模糊测试（extended fuzzing experiments）** 进一步探查LLM对底层代码安全的理解水平。
- **场景特点**：利用开源软件**持续演进的复杂性**来减轻过拟合风险（即模型不会因为静态题目而作弊），是动态、更新的评估场景。

### 4. 资源与算力

- 提供的摘要和元数据中**未提及**使用的GPU型号、数量、训练时长或推理算力开销。OSS-Bench本身是**基准生成器与评估器**，推断其算力消耗主要在**运行编译、测试套件、Sanitizer和模糊测试**，以及**LLM推理**环节，但具体资源量未披露。

### 5. 实验数量与充分性

- **实验组数**：至少覆盖了**2个大型OSS项目领域（PHP、SQL）** × **17个LLM** × **百万级任务** × 多项指标（可编译性、功能正确性、内存安全及模糊测试）。整体实验规模庞大。
- **充分性与客观性**：
  - 使用真实项目的全量测试套件和Sanitizer作为客观信号，避免了人工标注的主观性。
  - 通过两个不同的OSS实例化，检验了基准的领域可迁移性。
  - 补充模糊测试实验，深挖了模型在内存安全理解上的局限性，增加了评估的深度。
  - 文中提到揭示了“模型家族内部行为模式”及“模型大小与性能的不一致性”，说明进行了多维度分析，实验设计较为全面。
- **潜在局限**：仅展示了PHP和SQL两个实例，是否对其他语言/领域（如内核、网络库）同样有效，尚未在摘要中体现。消融实验（如不同上下文长度、不同替换位置的影响）未提及，可能只做了主要对比。

### 6. 论文的主要结论与发现

- OSS-Bench通过利用OSS不断演变的复杂性，**有效缓解了过拟合**问题，提供了更现实的评估。
- LLM在**可编译性**和**功能性**上可能存在一定能力，但在**内存安全**方面暴露出显著的理解不足，特别是在扩展模糊测试下。
- 不同模型家族内部表现出**行为模式一致性**，但模型尺寸与性能之间并非简单正比关系（可能存在小模型更优或大模型递减的现象）。
- 整体上，OSS-Bench证明了自动生成的、基于真实OSS的流水线能够**规模化、客观地**评估LLM的代码生成能力，尤其能暴露底层安全缺陷。

### 7. 优点

- **真实性与可扩展性**：直接从开源软件自动化构建任务，无需人工设计，任务数量随OSS发展自然膨胀，避免被“刷榜”。
- **评估维度全面**：同时考察编译、功能和安全三个层次，特别是引入对内存安全的直接检测（Sanitizer），填补了现有基准对低层安全关注的空白。
- **客观的信号**：使用编译失败、测试套件结果和Sanitizer报警作为二值或可计数的ground truth，减少了人工评估的模糊性。
- **动态更新性**：基准跟随OSS项目版本更新，能够持续反映模型对当前代码生态的适应能力。

### 8. 不足与局限

- **领域覆盖有限**：公开摘要仅展示了PHP解释器与SQL类项目，可能偏向于特定类型软件（如解释器、数据库），对其他系统软件（如操作系统、网络协议栈）的泛化性有待验证。
- **任务粒度单一**：函数级别的替换可能无法完全模拟开发者从零搭建模块或全局重构的真实场景。
- **内存安全评估的依赖**：Sanitizer只能发现运行时触发的内存错误，若测试覆盖率不足，可能存在漏报；模糊测试虽然能增强，但计算开销大且路径爆炸。
- **缺少对功能性缺陷的细粒度分析**：仅通过测试套件通过与否来判断，可能忽略那些未覆盖的功能角或特殊输入。
- **资源透明度不足**：未交代LLM推理和评估流程的算力成本，其他研究者难以精确复现实验成本。
- **潜在偏差**：所选OSS项目的代码风格、文档注释可能对某些模型更友好，形成隐式偏差；且主要关注C/C++场景下的内存安全，不适用于其他语言的内存管理模型（如Java、Python）。

（完）

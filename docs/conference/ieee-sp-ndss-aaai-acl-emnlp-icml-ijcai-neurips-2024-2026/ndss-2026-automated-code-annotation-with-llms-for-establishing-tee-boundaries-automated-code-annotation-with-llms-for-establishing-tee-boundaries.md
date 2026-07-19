---
title: Automated Code Annotation with LLMs for Establishing TEE Boundaries
title_zh: 利用LLM自动标注代码以建立TEE边界
authors: "Varun Gadey, Melanie Melanie Gotz, Christoph Sendner, Sampo Sovio, Alexandra Dmitrienko"
date: 2026-01-01
pdf: "https://www.ndss-symposium.org/wp-content/uploads/2026-s709-paper.pdf"
tags: ["query:safe-coding"]
score: 8.0
evidence: 利用LLM自动识别安全敏感代码区域以增强软件安全性。
tldr: LLM-CAL利用先进大语言模型自动识别加密等安全敏感代码区域，并标注应置于可信执行环境内的边界，以缩减可信计算基。该方法有效降低了人工审查负担，使软件开发者能够快速建立TEE边界，提升整体系统安全性。
source: NDSS-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 907, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1706, \"height\": 434, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 920, \"height\": 148, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 912, \"height\": 418, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 929, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 928, \"height\": 714, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 930, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 928, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 931, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 931, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 929, \"height\": 478, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 926, \"height\": 474, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 926, \"height\": 475, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 927, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 782, \"height\": 171, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 917, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 913, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 928, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 916, \"height\": 132, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-automated-code-annotation-with-llms-for-establishing-tee-boundaries/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 923, \"height\": 388, \"label\": \"Table\"}]"
motivation: 手动识别应放入TEE的安全敏感代码区域十分困难且缺乏自动化工具。
method: 提出LLM-CAL，利用预训练LLM自动识别并标注加密逻辑等安全关键代码区域。
result: 工具能够有效定位安全敏感代码，减少人工分析工作量，协助建立TEE边界。
conclusion: LLM-CAL为安全软件开发提供了自动化支持，提升了TEE应用的安全性与部署效率。
---

## Abstract
Modern systems increasingly rely on Trusted Execution Environments (TEEs), such as Intel SGX and ARM TrustZone, to securely isolate sensitive code and reduce the Trusted Computing Base (TCB). However, identifying the precise regions of code especially those involving cryptographic logic that should reside within a TEE remains challenging, as it requires deep manual inspection and is not supported by automated tools yet. To solve this open problem, we propose LLM based Code Annotation Logic (LLM-CAL), a tool that automates the identification of security-sensitive code regions with a focus on cryptographic implementations by leveraging most recent and advanced Large Language Models (LLMs). Our approach leverages foundational LLMs (Gemma-2B, CodeGemma-2B, and LLaMA7B), which we fine-tuned using a newly collected and manually labeled dataset of over 4,000 C source files. We encode local context features, global semantic information, and structural metadata into compact input sequences that guide the model in capturing subtle patterns of security sensitivity in code. The fine-tuning process is based on quantized LoRA—a parameter-efficient technique that introduces lightweight, trainable adapters into the LLM architecture. To support practical deployment, we developed a scalable pipeline for data preprocessing and inference. LLM-CAL achieves an F1 score of 98.40% and a recall of 97.50% in identifying sensitive and non-sensitive code. It represents the first effort to automate the annotation of cryptographic security-sensitive code for TEE-enabled platforms, aiming to minimize the Trusted Computing Base (TCB) and optimize TEE usage to enhance overall system security.

---

## 论文详细总结（自动生成）

# 论文总结：Automated Code Annotation with LLMs for Establishing TEE Boundaries

## 1. 论文的核心问题与整体含义

- **核心问题**：现代系统越来越多地采用可信执行环境（TEE）隔离安全敏感代码以缩小可信计算基（TCB），但精确识别哪些代码（尤其是加密逻辑及相关数据流）应放入 TEE 仍是一项高度依赖专家知识、耗时且容易出错的手动任务，目前缺乏自动化工具。
- **整体含义**：论文提出 LLM‑CAL，首次将大语言模型（LLM）引入代码安全敏感区域自动标注，聚焦于加密实现（cryptex code），旨在自动化 TEE 边界划分，降低人工审查负担，使开发者能快速、可靠地将关键代码移入 TEE，从而缩减 TCB、增强系统安全。

## 2. 论文提出的方法论

- **问题建模**：将 cryptex code 识别形式化为**行级别的二分类问题**（敏感/非敏感），并最终聚合到**函数级别**以确定 TEE 边界。
- **cryptex code 定义**：包含直接调用加密原语的代码，以及处理加密操作敏感输入/输出的全部数据流（如密钥生成、密码处理、签名数据），即从数据流角度看，加密函数作为“汇”，所有流向该汇的代码路径都属于 cryptex code。
- **数据集构建（Phase 1）**：从 GitHub 收集利用 OpenSSL 库的 1070 个开源 C 项目，筛选出 4010 个源文件，按照上述定义手动标注代码行，总共花费超过 1000 人时。数据集以 80/20 划分训练验证集和独立测试集。
- **输入序列构建（Phase 2）**：对每一待分类行，构造结构化的输入序列 x_i，包含：
  - **局部上下文**：该行及前后各两行代码（共 5 行），过滤掉注释、空行等。
  - **全局语义特征**：基于函数调用图（FCG）提取该行所在函数调用的 API 和内部函数；并利用代码属性图（CPG）提取数据依赖关系（如 REACHING_DEF 边），标注变量定义、使用及语义可达的行。
  - **元数据**：行号、函数名、文件名。
- **LLM 微调（Phase 3）**：
  - 采用 **QLoRA** 进行参数高效微调：对基础模型做 4‑bit 量化冻结，仅在注意力层的 `W_Q, W_K, W_V, W_O` 插入低秩适配器，秩设为 16。
  - 训练损失：**加权二元交叉熵（BCE）**，以缓解 cryptex 行稀疏导致的类别不平衡。
  - 优化策略：带权重衰减的正则化、余弦学习率调度、早停。
- **推理与标注（Phase 4）**：用相同预处理管道生成输入序列，微调模型输出概率，超过阈值（如 0.5）即判定为 cryptex 行，最后按函数聚合，给出应迁移到 TEE 的函数列表。

## 3. 实验设计

- **数据集**：自建 OpenSSL 相关 C 代码数据集（4010 文件，总行数约 96k，测试集约 1.6 万行）。另构造一个额外的 mbedTLS 测试集（30 个项目、约 1.6 万行）评估跨库泛化。
- **评估指标**：准确率、精确率、召回率、F1 分数、TCB 缩减比例、识别率（函数/行）。
- **主要对比对象或变体**：
  - 不同 LLM 骨干：Gemma‑2B（主模型）、CodeGemma‑2B、LLaMA‑7B。
  - 不同微调策略：零样本（未微调）、QLoRA、DORA。
  - 不同粒度：行级别与函数级别。
  - 特征消融：分别移除局部特征、全局特征、元数据，观察性能变化。
  - 不同安全操作类型：加密/解密、哈希、密钥存储/使用、TLS/DTLS。
- **案例研究**：比特币签名工具、ARM TrustZone 固件（Pinlock）、基于 mbedTLS 的代码（AES‑GCM）。

## 4. 资源与算力

- **硬件**：服务器配备 Intel Xeon CPU、251 GB 内存，**4 块 GPU**，每块 48 GB VRAM，已配置 CUDA 和 cuDNN。
- **训练方式**：采用分布式数据并行（4 GPU）加速，基模型进行 4‑bit 量化以降低显存占用。
- **训练时长**：**论文未明确给出**具体训练时间或训练轮数，但提及使用早停提前终止。

## 5. 实验数量与充分性

- **实验组数**：大致可分为以下几类，总计 **10 组以上** 的定量或定性评估：
  - 主结果表（行/函数级别） 1 组
  - 消融实验（移除局部/全局/元数据） 1 组，共 3 个变体
  - LLM 架构对比（Gemma、CodeGemma、LLaMA） 1 组
  - 微调策略对比（Zero‑shot、QLoRA、DORA） 1 组
  - 跨库鲁棒性测试（mbedTLS 额外测试集） 1 组
  - 不同加密任务（加密、哈希、密钥、TLS）的性能分析 1 组
  - 三个案例研究（实践验证） 3 组
  - 运行时评估 1 组
- **充分性**：实验覆盖了特征贡献、模型选择、跨库泛化、真实场景应用及效率，消融和跨库测试增强了内部效度；与零样本及 DORA 对比体现了方法选择的优势。整体设计**较全面且公平**，但缺乏与传统静态分析工具或人工标注的直接对比（因领域内无直接比较对象）。

## 6. 论文的主要结论与发现

- LLM‑CAL 在测试集上达到 **99.04% 准确率、97.50% 召回率、99.40% 精确率、98.41% F1**；函数级别识别率 **100%**（零假阴/假阳）。
- TCB 减少约 **81.20%**，仅因少量误分类导致 TCB 膨胀 **0.52%**。
- 局部上下文和全局语义特征对模型性能至关重要，移除后 F1 分别降至 71.35% 和 80.44%。
- QLoRA 微调显著优于零样本和 DORA，且可在消费级 GPU 上完成。
- 即便训练数据仅来自 OpenSSL，模型在 **mbedTLS、NXP** 等完全不同的加密库及嵌入式固件上仍表现稳健，展示了良好的泛化能力。
- LLM‑CAL 推理速度快（处理 352 行文件约 22 秒），具有实际部署可行性。

## 7. 优点

- **首创性**：首个针对 TEE 边界划分的加密敏感代码自动标注工具，填补了自动化空白。
- **数据集贡献**：构建并计划公开首个大规模线级标注的 cryptex 代码数据集，支持复现和后续研究。
- **方法设计**：融合局部、全局和元数据的输入表示，QLoRA 实现参数高效微调，平衡了性能与资源需求。
- **粒度灵活**：提供了从行级到函数级的聚合策略，兼顾细粒度识别与 TEE 部署的实际适用性。
- **泛化验证**：不仅限于训练分布（OpenSSL），在 mbedTLS、嵌入式固件、比特币工具等多种真实场景下均有验证，结果可靠。
- **全面评估**：包含消融、跨架构、跨库、多操作类型、案例研究和运行时分析，实验扎实。

## 8. 不足与局限

- **安全敏感定义偏窄**：cryptex code 主要围绕加密操作和数据流，未涵盖一些非加密但同样安全关键的逻辑（如访问控制策略、权限检查等），实际应用中可能遗漏部分敏感区域。
- **数据集偏差**：训练数据全部基于 OpenSSL，尽管展示了跨库泛化，但在极端定制或小众加密库上的表现仍需更多验证；仅限 C 语言，不能直接用于其他编程语言。
- **静态分析局限**：依赖代码属性图提取数据流，无法处理动态生成、反射或高度混淆的代码，静态分析也可能遗漏某些路径。
- **LMM 误判**：案例中观察到个别过度敏感标记（如将本应公开的签名打印标记为敏感），在严格最小化 TCB 场景下可能引入少量膨胀。
- **威胁模型假设**：假定 LLM‑CAL 在开发阶段使用且不受攻击，未考虑对抗样本或训练数据投毒等风险。
- **计算资源**：虽然推理速度可接受，但微调仍需 4 块高显存 GPU，对小团队或个人开发者可能仍有门槛。

（完）

---
title: "DeepGuard: Secure Code Generation via Multi-Layer Semantic Aggregation"
title_zh: DeepGuard：通过多层语义聚合实现安全代码生成
authors: "Li Huang, Zhongxin Liu, Yifan Wu, Tao Yin, Dong Li, Jichao Bi, Nankun Mu, Hongyu Zhang, Meng Yan"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.907.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 通过多层语义聚合实现安全代码生成，缓解不安全模式
tldr: 针对LLM代码生成复制训练数据中不安全模式的问题，提出DeepGuard多层语义聚合框架。通过分析Transformer中间层发现漏洞信号衰减现象，并利用中间层表征增强安全微调，从而生成更安全的代码。实验表明该方法有效减少安全漏洞。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 795, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 794, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1637, \"height\": 819, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1643, \"height\": 290, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 811, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 804, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 802, \"height\": 320, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1657, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1630, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1624, \"height\": 752, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 800, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1663, \"height\": 1951, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long907/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1663, \"height\": 1953, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1660, \"height\": 1329, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1665, \"height\": 1045, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1663, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 618, \"height\": 1200, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 841, \"height\": 534, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 826, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 790, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 835, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 837, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 812, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 813, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1665, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long907/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 813, \"height\": 704, \"label\": \"Table\"}]"
motivation: LLM代码生成易复制不安全模式，传统微调仅用最后一层导致漏洞信号衰减。
method: 提出多层语义聚合框架，利用中间层的漏洞判别信号进行安全微调。
result: 在漏洞检测任务上优于最后一层微调，生成代码安全漏洞显著减少。
conclusion: 通过多层表征聚合可增强LLM代码生成的安全性，优于传统微调方法。
---

## Abstract
Large Language Models (LLMs) for code generation can replicate insecure patterns from their training data. To mitigate this, a common strategy for security hardening is to fine-tune models using supervision derived from the final transformer layer. However, this design may suffer from a final-layer bottleneck: vulnerability-discriminative cues can be distributed across layers and become less detectable near the output representations optimized for next-token prediction. To diagnose this issue, we perform layer-wise linear probing. We observe that vulnerability-related signals are most detectable in a band of intermediate-to-upper layers yet attenuate toward the final layers. Motivated by this observation, we introduce DeepGuard, a framework that leverages distributed security-relevant cues by aggregating representations from multiple upper layers via an attention-based module. The aggregated signal powers a dedicated security analyzer within a multi-objective training objective that balances security enhancement and functional correctness, and further supports a lightweight inference-time steering strategy. Extensive experiments across five code LLMs demonstrate that DeepGuard improves the secure-and-correct generation rate by an average of 11.9% over strong baselines such as SVEN. It also preserves functional correctness while exhibiting generalization to held-out vulnerability types.

---

## 论文详细总结（自动生成）

好的，这是对给定论文的结构化深度总结。

### **1. 论文的核心问题与整体含义**

*   **核心问题**：代码生成大模型常从其训练数据中复制不安全的编码模式，导致生成漏洞代码。现有的安全加固微调方法主要依赖模型**最后一层Transformer**的输出表征来获取监督信号，这存在一个“**最终层瓶颈**”（Final-Layer Bottleneck）。
*   **整体含义**：该研究发现，用于区分漏洞与安全代码的关键信号并非只存在于最后一层，而是**分布在模型的中间至上层层次**中，并且在向最终层传递时会衰减。因此，仅依靠最终层进行微调是一种次优策略。本文提出的 **DeepGuard** 框架，旨在通过**多层语义聚合**来捕获这些分布式安全线索，从而更有效地增强代码生成的安全性。

### **2. 论文提出的方法论**

*   **核心思想**：突破单一最终层表征的限制，动态融合Transformer多个上层的隐藏状态，形成一个对安全更敏感的聚合表征，并据此指导模型训练和推理。
*   **关键技术细节**：
    1.  **多层表征聚合**：
        *   选取模型的顶部 \( N \)层（如 \( N=4 \)）的隐藏状态 \( \mathbf{H}_{\text{top-}N} \)。
        *   设计一个**基于注意力机制的聚合器**。它以各层状态的平均值作为查询向量，对各层状态进行注意力加权融合，得到一个单一的聚合表征 \( \mathbf{H}_{\text{agg}} \)。其直觉是让模型自适应地为包含更丰富安全信息的层次分配更高权重。
    2.  **多目标训练框架**：
        *   **安全分析器**：一个轻量级MLP，输入为聚合表征 \( \mathbf{H}_{\text{agg}} \) 和一个可学习的词元安全先验嵌入（Token Security Embedding），输出为输入序列的每个词元（token）的安全评分。
        *   **安全对比损失（\( \mathcal{L}_{\text{sec}} \)）**：使用功能等价的“漏洞/安全”代码对，通过基于间隔的对比损失，鼓励模型让安全代码的整体评分远高于漏洞代码。
        *   **功能保持目标**：结合标准的**下一词元预测损失（\( \mathcal{L}_{\text{gen}} \)）** 和对原始模型的**KL散度正则化损失（\( \mathcal{L}_{\text{kl}} \)）**，以防止模型灾难性遗忘，维持代码生成的功能正确性。总损失为三者加权和 \( \mathcal{L}_{\text{total}} = \mathcal{L}_{\text{gen}} + w_{\text{sec}} \mathcal{L}_{\text{sec}} + w_{\text{kl}} \mathcal{L}_{\text{kl}} \)。
    3.  **轻量级推理引导**：
        *   **词元先验向量 \( T_{\text{stats}} \)**：基于训练数据统计，为每个词元赋予一个全局的安全/漏洞倾向性分数。
        *   **提示条件偏置**：在推理时，仅对输入的提示进行一次前向传播，得到其平均安全评分 \( \bar{s}_{\text{prompt}} \)，然后用 \( (1 - \bar{s}_{\text{prompt}}) \) 去缩放静态词元先验 \( T_{\text{stats}} \)，生成为一个固定的词表级偏置向量 \( \mathbf{b} \)。
        *   **日志偏置**：在解码过程的每一步，将此偏置 \( \mathbf{b} \) 加到模型原始输出Logits上，以引导生成朝着更安全的词元方向进行，几乎无额外推理成本。

### **3. 实验设计**

*   **模型与基准**：在五个主流开源代码大模型上实验，包括 **Qwen2.5-Coder (3B, 7B)**、**DeepSeek-Coder (1.3B, 6.7B)** 和 **Seed-Coder (8B)**。评估遵循 He 和 Vechev (2023) 以及 Fu 等人 (2024) 建立的基于场景的基准测试协议。
*   **数据集**：
    *   **训练集**：包含1,606个程序（803个漏洞/安全代码对），覆盖Python和C/C++的9种CWE漏洞类型。
    *   **测试集（分布内）**：来自CodeGuard+基准，包含18个安全场景，通过可执行的单元测试同时评估安全性和功能正确性。
    *   **泛化测试集（分布外）**：包含12个场景，覆盖4种**未在训练集中出现的**CWE类型，用于测试模型的安全知识泛化能力。
*   **对比方法**：与两大范式下的多个强基线进行比较：
    *   **训练时适应**：**SVEN**、**SafeCoder**。
    *   **推理时干预**：**CoSec**、**CodeGuard+**。
    *   **简单基线**：未微调的**基础模型**和**安全提示指令**。

### **4. 资源与算力**

*   论文在“C.1 Hyperparameters for Experiments”部分明确提到，所有实验均在 **NVIDIA A800 GPU** 上进行，但**未提及使用的GPU数量及具体训练总时长**。

### **5. 实验数量与充分性**

*   **实验数量**：实验设计相当充分，主要包括：
    *   **主要结果**：在5个模型上与6种方法（含基础模型）进行性能对比。
    *   **泛化性测试**：对模型在未见过的CWE类型上的表现进行评估。
    *   **消融实验**：对训练损失函数各组成部分、推理引导策略、以及聚合器设计进行全面消融。
    *   **鲁棒性分析**：评估引导式推理对良性任务（HumanEval）的干扰，以及基于间隔的重评分策略。
    *   **诊断与分析**：包含层次化线性探测、注意力权重可视化、词元先验分析、超参数敏感性分析和案例研究。
*   **充分性与公平性**：实验**非常充分且公平**。评估基准、超参数配置、与强基线的对比都遵循了领域内的标准设定，评估指标全面（功能正确性、安全性、联合指标），并且包含了分布外泛化测试，能客观反映方法的真实性能。

### **6. 论文的主要结论与发现**

1.  **漏洞信号衰减现象存在**：通过层次线性探测证实，漏洞判别信号在Transformer的中间偏上层最强，并向最终层显著衰减，验证了“最终层瓶颈”的假设。
2.  **DeepGuard方法显著有效**：所提出的多层聚合和多目标训练框架能够有效提升代码生成的安全性。在“既安全又正确”的生成率（`sec-pass@1`）指标上，DeepGuard相较于强基线SVEN平均提升**11.9%**。
3.  **功能正确性得到保持**：在提升安全性的同时，DeepGuard成功保持了与基础模型和大部份基线方法相比具有竞争力的功能正确性（`pass@1`）。
4.  **具备良好的泛化能力**：DeepGuard在处理训练时未见过的漏洞类型时表现出色，证明其学到了可泛化的安全编码原则，而非简单记忆。
5.  **推理时引导轻量且有效**：提出的轻量级推理引导策略以极低的额外计算成本，为模型安全提供了进一步的“安全兜底”。

### **7. 优点**

*   **新颖的诊断分析**：通过层次探测清晰地揭示了现有方法中存在的“最终层瓶颈”问题，为方法设计提供了坚实的动机。
*   **创新性的多层聚合机制**：首次提出并验证了基于注意力的多层表征聚合策略用于代码安全增强，比仅用最终层或均值池化更有效，可解释性更强。
*   **全面的训练-推理框架**：不仅通过多目标训练优化模型，还引入了一个解耦的、轻量级的推理时引导模块，该模块可按需开启/关闭，提高了灵活性。
*   **实验评估极其扎实**：覆盖了多个不同家族和规模的模型，进行了详细的消融和对泛化性的测试，结果令人信服。

### **8. 不足与局限**

*   **场景覆盖有限**：实验主要在**函数级**的Python和C/C++基准上进行，未涉及跨文件的仓库级漏洞、长距离依赖或更多编程语言。
*   **对配对数据的依赖**：训练依赖于构造成本较高的“漏洞/安全”代码对，这可能限制其在更广泛漏洞类型和软件领域上的可扩展性。
*   **固定的聚合层数**：聚合的顶层数量 \( N \) 是一个固定的超参数，但最优层数可能因模型结构和输入而异，动态层数选择可能带来更好的效果。
*   **不适用于黑盒模型**：该方法需要访问模型的内部层隐状态，无法直接应用于仅提供API访问的商业闭源大模型。

（完）

---
title: "PurpCode: Reasoning for Safer Code Generation"
title_zh: PurpCode：面向更安全代码生成的推理训练
authors: "Jiawei Liu, Nirav Diwan, Zhe Wang, Haoyu Zhai, Xiaona Zhou, Kiet A. Nguyen, Tianjiao Yu, Muntasir Wahed, Yinlin Deng, hadjer Benkraouda, Yuxiang Wei, LINGMING ZHANG, Ismini Lourentzou, Gang Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=VUoY5kacG5"
tags: ["query:safe-coding"]
score: 10.0
evidence: 训练代码推理模型以生成安全、无漏洞的代码
tldr: 针对现有代码生成模型缺乏安全训练的问题，提出PurpCode后训练方法，首先通过规则学习教授安全编码规则，再通过强化学习多目标优化安全性与实用性，生成无漏洞的安全代码。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 大型语言模型生成代码时可能引入安全漏洞，缺乏系统的安全增强训练。
method: 两阶段训练：规则学习阶段显式教授模型引用网络安全规则；强化学习阶段使用多目标奖励平衡安全与效用。
result: 内部红队测试生成高覆盖安全提示，训练后模型能有效生成安全代码并拒绝恶意请求。
conclusion: PurpCode首次为代码推理模型提供了安全训练的后训练方案，显著提高生成代码的安全性。
---

## Abstract
We introduce PurpCode, the first post-training recipe for training safe code reasoning models towards generating secure code and defending against malicious cyberactivities. PurpCode trains a reasoning model in two stages: (i) Rule Learning, which
explicitly teaches the model to reference cybersafety rules to generate vulnerability-free code and to avoid facilitating malicious cyberactivities; and (ii) Reinforcement Learning, which optimizes model safety and preserves model utility through diverse, multi-objective reward mechanisms. To empower the training pipelines with comprehensive cybersafety data, we conduct internal red-teaming to synthesize comprehensive and high-coverage prompts based on real-world tasks for inducing unsafe cyberactivities in the model. Based on PurpCode, we develop a reasoning-based coding model, namely PurpCode-32B, which demonstrates state-of-the-art cybersafety,
outperforming various frontier models. Moreover, our alignment method decreases the model overrefusal rates in both general and cybersafety-specific scenarios, while preserving model utility in both code generation and common security knowledge.

---

## 论文详细总结（自动生成）

基于给定的论文元数据（标题、摘要、动机、方法、结果、结论等），现对《PurpCode: Reasoning for Safer Code Generation》一文进行结构化总结。由于未获取到完整论文内容，部分细节（如具体实验数据、算力资源）未能详细展开，总结将如实反映现有信息。

---

### 1. 论文的核心问题与整体含义
- **研究背景**：大型语言模型（LLMs）在代码生成任务中表现优异，但生成的代码经常引入安全漏洞（如SQL注入、跨站脚本等），且可能被滥用于恶意网络活动。现有模型普遍缺乏系统性的安全增强训练，导致安全性与实用性难以兼顾。
- **核心问题**：如何对代码生成模型进行专门的后训练，使其能够主动生成无漏洞的安全代码，并有效拒绝协助恶意请求，同时保持原有的代码生成能力和安全知识。
- **整体含义**：提出首个面向代码推理模型的安全后训练方案`PurpCode`，通过“规则学习+强化学习”两阶段训练，从机制上提升模型的网络安全性，为构建可靠的安全编码助手奠定了基础。

### 2. 论文提出的方法论
- **核心思想**：不依赖大规模人工标注，而是通过训练模型显式掌握网络安全规则，并结合多目标奖励优化，使模型内化安全编码规范，最终生成“本质安全”的代码。
- **关键技术细节**：
  - **阶段一：规则学习（Rule Learning）**
    - 明确教授模型参照预先定义的网络安全性规则（如CWE、OWASP标准）来编写代码。
    - 目标：使模型学会识别潜在漏洞，生成无漏洞的代码，并学会对恶意请求给出安全性回应（如拒绝执行）。
  - **阶段二：强化学习（Reinforcement Learning）**
    - 构建多目标奖励函数，同时优化：
      - **安全奖励**：代码是否无漏洞、是否正确拒绝恶意指令。
      - **效用奖励**：代码功能是否正确、是否保持通用安全知识的回答能力。
    - 通过奖励信号的平衡，防止模型因过度强调安全而出现“过拒答”（overrefusal），保留其实用价值。
  - **数据支撑**：通过内部红队测试（Internal Red-teaming）方法，模拟真实世界任务，合成覆盖全面、多样性高的安全攻击提示，用于两个阶段的训练。
- **算法流程（文字描述）**：
  1. 利用基础代码推理模型。
  2. 使用红队生成的“恶意/高风险”提示集合，在规则学习阶段微调模型，使其学会引用规则并生成安全输出。
  3. 在强化学习阶段，针对多种类别（安全编码、恶意请求拒绝、通用代码生成、安全知识问答）的样本，用组合奖励训练模型，迭代优化其安全性和实用性平衡点。
  4. 最终得到`PurpCode-32B`模型。

### 3. 实验设计
- **数据集/场景**：
  - 内部红队合成的多类别安全提示，涵盖漏洞生成请求（如“写一段有缓冲区溢出的代码”）及恶意攻击指令，覆盖真实网络攻击场景。
  - 通用代码生成基准（名称未指明，可能包含HumanEval、MBPP等常见编码测试）用于评估效用保留。
  - 安全知识测试集用于衡量模型对通用安全知识的保留程度。
- **Benchmark与对比方法**：
  - **安全性能**：与多种前沿模型（“various frontier models”，可能包括GPT-4、Claude、Gemini等商用模型及开源代码模型如CodeLlama）对比漏洞生成率和恶意请求拒绝率，宣称达到最佳（state-of-the-art）安全水平。
  - **过拒答率**：衡量模型在无害请求上的错误拒绝比例，与现有对齐方法对比，展示其降过拒答效果。
  - **效用保留**：在代码生成准确率和通用安全知识问答上对比基础模型，证明训练后能力无明显退化。
- **实验目标**：验证PurpCode在安全性、过拒答控制、效用保留三个维度的综合优势。

### 4. 资源与算力
- **文中未提及**具体的GPU型号、数量、训练时长或显存消耗。由于仅获取到元数据，无法得知算力细节。若有完整论文，这部分通常出现在实验设置章节。

### 5. 实验数量与充分性
- **实验组设计推测**：
  - 至少包含：安全性对比（多模型、多漏洞类型）、消融实验（有无规则学习阶段、有无多目标奖励）、过拒答率评价、效用退化评价。
  - 从“state-of-the-art cybersafety, outperforming various frontier models”和“decreases the model overrefusal rates”推断，实验覆盖了安全性、可用性两大核心轴。
- **充分性评价（基于现有信息）**：
  - **相对充分**：同时考察了安全增益、过拒答问题和效用保留，避免了对单一指标的过度优化，设计较全面。
  - **局限性**：缺乏对实验数据具体量级、统计显著性、跨语言/跨领域泛化测试的描述，且内部红队集的代表性和对抗鲁棒性未知。若仅依赖自身构建的红队提示，可能存在评测偏差。

### 6. 论文的主要结论与发现
- 基于PurpCode后训练得到的`PurpCode-32B`模型在网络安全任务上达到业界领先水平，优于现有商业/开源前沿模型。
- 两阶段训练有效平衡了安全对齐与模型实用性的矛盾：模型在生成安全代码、拒绝恶意指令的同时，过拒答率显著下降，且代码生成和通用安全知识能力损失极小。
- 首次证明了针对代码推理模型进行系统安全性后训练的可行性与有效性。

### 7. 优点
- **问题新颖性**：首次专注代码推理模型的安全后训练，填补了代码生成安全领域的研究空白。
- **方法设计**：创新的两阶段架构，将显式规则学习与多目标强化学习相结合，从知识灌输到行为优化形成闭环。
- **实用性考量**：特别关注了安全对齐中的“过拒答”难题，通过奖励设计维持模型可用性，更贴近现实部署需求。
- **数据构建**：采用红队攻击模拟生成训练数据，提高了安全覆盖的广度和真实性。

### 8. 不足与局限
- **数据集依赖与可复现性**：方法严重依赖内部红队合成的提示集，数据未公开可能限制他人复现和公平对比。
- **规则覆盖的全面性**：安全规则集的完整度与更新频率直接决定模型安全上限，论文元数据未说明如何处理规则演化（如新型漏洞）。
- **泛化性未知**：结果仅在代码推理模型上验证，且对比细节模糊，对非代码任务或真实多轮交互场景的扩展能力存疑。
- **红队测试偏差**：使用自身红队生成的数据进行评测，可能高估安全性能；缺少外部、独立的对抗性评估（如第三方红队测试）。
- **算力与效率**：未披露训练成本，难以评估方法在大规模部署中的经济可行性。
- **安全幻觉**：模型是否可能生成看似安全但含逻辑漏洞的代码，或对未曾见过的攻击模式失效，尚待更多分析。

（完）

---
title: "Safety Sidecar: Reflection-Driven Runtime Control for Safer Agents"
title_zh: "Safety Sidecar: 基于反思的代理运行时安全控制"
authors: "Wang Bin, Quan Jiazheng, Xingrui Yu, Hu Hansen, Yu Hao, Anjun Gao, Zhenglin Wan, Hui LI, Ivor Tsang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1542.pdf"
tags: ["query:safe-codegen"]
score: 6.0
evidence: 运行时安全控制，适用于代码生成智能体
tldr: Safety Sidecar提出了一种模型无关的插件式运行时安全控制模块，通过反思机制监控智能体决策并施加安全约束。该框架可应用于代码生成智能体，在流程中预防不安全代码的产生，为自动代码生成提供安全保障。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1542/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 901, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1542/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 767, \"height\": 590, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1482, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 651, \"height\": 181, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 608, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 733, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 781, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 747, \"height\": 382, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 732, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1660, \"height\": 1202, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1655, \"height\": 683, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1524, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1542/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 742, \"height\": 187, \"label\": \"Table\"}]"
motivation: 现有LLM代理安全防护多为静态提示或事后护栏，缺乏运行时干预。
method: 提出Safety Sidecar插件模块，动态监控决策轨迹，通过反思记忆检索修复范例并执行安全约束。
result: 实验表明该方法能在不同代理工作流中有效防止危险操作。
conclusion: 该框架为代理系统提供了标准化的运行时安全控制与可审计性。
---

## Abstract
Autonomous LLM agents are increasingly deployed in complex environments as tool-using systems. However, their safety remains fragile, as minor reasoning or retrieval errors can be amplified into hazardous actions within the agentic workflow. Existing defenses, often limited to static prompts or post-hoc guardrails, fail to provide runtime intervention or cross-architecture portability. In this paper, we propose Safety Sidecar , a model-agnostic, plug-and-play module designed to provide standardized runtime safety control and auditability for arbitrary agent workflows. Safety Sidecar operationalizes reflection as a closed-loop controller: it dynamically monitors decision traces, retrieves evidence-based repair exemplars from a reflective memory, and enforces risk-mitigating revisions before execution. Crucially, it employs external verifiers to gate both action release and memory updates, producing a transparent, auditable trail of retrieved evidence and applied constraints.We instantiate and systematically evaluate Safety Sidecar in secure code generation—a high-stakes domain with objective vulnerability signals. Experimental results across eight CWE scenarios and four representative LLMs demonstrate that Safety Sidecar consistently improves the secure-solution rate by 2.9–11.2 percentage points while maintaining competitive functional correctness. Efficiency analysis shows the framework is practical for deployment, with reflection adding only 3.2s to end-to-end latency and a negligible average cost of 5.37 × 10 -4 per scenario. Our findings position Safety Sidecar as a portable and efficient control layer for enhancing the safety, compliance, and auditability of LLM-based agents.

---

## 论文详细总结（自动生成）

## 1. 研究动机与核心问题

- **背景与安全困境：** 自主LLM代理正从单轮文本生成器演化为执行多步任务、调用外部工具的系统。然而，其安全性高度脆弱——微小的推理错误或检索偏差在“规划–检索–执行”循环中被逐级放大，最终导致危险的工具调用或不可逆的外部状态修改。
- **现有防御的结构性缺陷：**
  - **事后防护滞后：** 基于扫描或过滤的事后防护无法撤销已执行的动作，且受污染的时间产物可能被写入长期记忆，被反复利用。
  - **规则栈通用性差：** 厚重的规则栈或定制化校验器与特定工具、任务分布紧耦合，难以跨架构移植，并可能侵蚀代理的自主性。
- **核心目标：** 提出一种**工作流原生的运行时安全控制机制**，能够在危险动作执行前进行干预，同时保持轻量化、可移植，并提供可审计的决策证据链。

## 2. 方法论：Safety Sidecar

Safety Sidecar 被设计为一个**模型无关、即插即用的标准化模块**，可附加至任意代理的输出边界。其核心是**将反思（Reflection）构建为闭环控制器**，在代理的决策–行动环路内实施干预。

### 2.1 整体闭环控制流程（公式2）
给定输入代码 `x` 及上下文 `c`，系统通过判定与验证形成如下闭环：

1. **轻量路由：** 自检器 `C ∈ {0,1}` 快速评估候选产物是否为 `SAFE`。若判为安全，直接放行并将此案例写入动态记忆 `MD`。
2. **反思修复：** 若判为 `UNSAFE`，从记忆库检索相关经验 `E` 及最佳实践约束 `K`，构造结构化反思提示 `Φ`，驱动冻结的基座模型 `fθ` 生成修复代码 `y`。
3. **验证门控：** 仅当修复后的产物 `y` 通过外部验证器 `V`（编译检查 + CodeQL静态分析）时，才允许执行，并将其正例写入 `MD` 形成经验积累。

### 2.2 三大核心组件
- **轻量自检器（Lightweight Self-Checker）：** 路由层，通过简洁的 binary prompt（`SAFE/UNSAFE`）进行廉价的初始筛查，避免不必要的全量反思，降低平均开销。**它并非最终安全决策者，只是效率优化器。**
- **反思提示引擎（Reflective Prompt Engine）：** 对不安全案例，构建**多轮反思对话**（漏洞识别 → 原因分析与缓解方案 → 安全代码重写），将单次生成任务拓展为可视化的推理链，并记录完整的修复过程。
- **反思记忆库（Reflective Memory Repository）：** 采用**分层混合检索**架构（公式4）。动态记忆层（ChromaDB向量库）存储已验证的高质量修复案例；静态记忆层存储固化的安全编码标准。当动态库检索的相似度或数量低于阈值 `θ` 与 `k_min` 时，自动回退至静态库补充，兼顾时效性与知识完备性。

## 3. 实验设计

### 3.1 评测场景与基准
- **主场景（代码安全）：** 选取MITRE Top 25中的**8个代表性CWE**类别（如SQL注入、缓冲区溢出、XSS、路径遍历等），每个类别包含 2-3 个精心设计的编程环境。数据集基于 He & Vechev (2023) 经过去噪的标准化基准。
- **辅助场景（跨域泛化）：** 增加 **HotpotQA**（多跳问答）基准，以验证框架在代码之外、需要推理与检索的通用代理任务上的迁移能力。
- **可移植性验证：** 对比集成到两种不同架构（单次生成代理 vs. 迭代工具驱动代理）下的表现。

### 3.2 对比方法与指标
- **模型：** 覆盖四个主流基座模型：`gpt-3.5-turbo`、`gpt-4o`、`qwen3-coder-plus`、`gemini-2.5-pro`。
- **对比：** 每个模型的原始输出（`Base`）与挂载 Safety Sidecar 后的输出（`Base+Sidecar`）一一对比。
- **核心定量指标：**
  - **安全率（Sec. Rate）：** 编译通过且无 CWE 漏洞的样本占编译通过总数的比例。
  - **通过率（Pass Rate）：** 功能测试正确样本占编译通过总数的比例。
  - **总效率（Eff. Total）：** 成功编译的样本数。
- **辅助定性评估：** 对所有编译通过的样本进行代码质量、防御完整性及合规性的人工审查。

## 4. 资源与算力

- **训练算力：** 论文未涉及对模型的训练或微调，故无 GPU 时长、型号等相关数据。整个方法完全基于推理阶段的 API 调用与模块串联。
- **推理开销：** 文中给出了详尽的成本与延迟分析。单场景平均额外耗时仅 **3.2 秒**（占端到端总延迟的 11.1%），大部分时延仍是基座模型生成（占 84.4%）；单场景平均经济成本极低，仅约 **5.37 × 10⁻⁴ 美元**（按 GPT-4o 定价计）。

## 5. 实验数量与充分性

整个实验体系覆盖了多个维度，设计严格，统计稳健：
- **主实验量级：** 4 个模型 × 8 个 CWE × 2-3 个场景，每个场景独立生成 25 个样本，并重复 **5 次独立运行**，累计测试了大量的生成-修复案例，避免了单次采样的随机性偏差。
- **消融实验：** 分别移除“动态记忆库”与“轻量自检器”，清晰验证了各个组件的独立贡献和不可或缺性。
- **机制分析实验：** 对反思的**迭代深度**（Round 1-5）及检索质量演进（相似度、命中率）进行了细致分析，发现了知识饱和点与“单轮最优”的部署规律。
- **泛化与迁移实验：** 额外包含跨任务（HotpotQA）和跨架构（单次/迭代代理）测试，论证了方法的普适性。
- **客观公平性：** 所有安全性结论均由外部编译器与 CodeQL 等客观信号判定，有效避免了模型自评带来的自确认偏差。

## 6. 主要结论与发现

- **安全性显著提升且模型无关：** 接入 Sidecar 后，所有模型的**安全率均得到大幅提升**，绝对提升幅度达 **2.9–11.2 个百分点**。对于初始安全性较弱的模型（如 Qwen、GPT-4o），提升尤为显著；该模块能将异构模型的安全性拉平到 94.9% 以上的高水平。
- **功能正确性得到保持：** 促进安全的同时，代码的编译通过率和功能测试通过率未出现显著下降，泛化能力良好。
- **“单轮反思即最优”的部署经验：** 深度分析表明，首次反思即可捕获约 90% 的关键修复模式；动态记忆在累积约 100 个样本后趋于饱和。实际部署中采用**单轮反思**即可在成本与安全之间取得最佳平衡。
- **闭环经验积累有效：** 验证器门控的写回机制使得检索相似度和命中率随经验累积持续上升并收敛，验证了动态知识库的自进化能力。

## 7. 优点

- **优雅的“尾气净化”架构：** 无需侵入代理的规划或记忆内核，以“边车”（Sidecar）形式在输出边界拦截、校验与修复，真正做到了低侵入式集成与即插即用。
- **权责分明的双层安全决策：** 将“路由导向”（轻量自检）与“权威背书”（外部验证器）分离，自检器仅用于节省算力，绝不替代安全审核，杜绝了模型自我审核的潜在风险。
- **极强的可解释性与可审计性：** 完整记录了从风险感知到证据检索再到强制修复的全链路痕迹，便于事后追溯合规。
- **细致的实验工程：** 不仅停留在精度比拼，还深入分析了反射深度的边际收益、成本构造和跨域鲁棒性，为工业落地提供了明确指导。

## 8. 不足与局限

- **领域强耦合验证机制：** 当前的高效性高度依赖代码领域的强客观验证信号（编译、CodeQL）。在安全约束更模糊、多模态的代理任务（如网页操作、具身智能）中，如何构建同等效力的验证器仍是挑战。
- **对多代理系统的延迟累积：** 单个场景 3.2s 的时延在极端低频场景可接受，但在并发的、超低延迟的实时控制生产环境中，若多个代理协同，时延可能累加成为瓶颈。
- **对抗鲁棒性尚存短板：** 论文明确指出，当前设计假设代理是善意但易犯错的。面对专门针对反思逻辑或记忆注入的攻击（如污染性检索），框架自身的防御纵深仍有待加强。
- **过度修正的风险：** 当动态记忆过于密集时，检索到过高的上下文可能给模型带来噪声，导致在修正漏洞的同时引入不必要复杂度的“矫枉过正”现象

，这一现象提示动态记忆需要引入密度控制或遗忘机制，防止经验过拟合。

**总结与展望：** Safety Sidecar 以极低的侵入性和清晰的双层验证架构，为当前 LLM 代理的输出侧提供了一套行之有效的运行时安全增强方案。其核心价值在于将“反思”从一个简单的模型自省过程，升华为连接外部客观验证器与动态经验积累的闭环控制环。面向未来，该框架需在跨领域验证器构建、低延迟适应以及对抗鲁棒性方面持续演进，但其设计理念已为构建可信自主代理的工作流原生安全机制提供了一个可扩展、可复现的坚实模板。

（完）

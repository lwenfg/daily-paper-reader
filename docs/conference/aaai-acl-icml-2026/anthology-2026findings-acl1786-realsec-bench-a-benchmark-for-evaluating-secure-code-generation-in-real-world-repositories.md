---
title: "RealSec-bench: A Benchmark for Evaluating Secure Code Generation in Real-World Repositories"
title_zh: RealSec-bench：真实仓库中评估安全代码生成的基准
authors: "Yanlin Wang, Ziyao Zhang, Chong Wang, Xinyi Xu, Mingwei Liu, Yong Wang, Jiachi Chen, Zibin Zheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1786.pdf"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 真实仓库中评估安全代码生成的基准
tldr: 现有安全代码生成基准依赖合成漏洞或单独评估功能正确性，未能反映真实软件中功能与安全的复杂交互。RealSec-bench从真实高风险Java仓库构建，采用SAST扫描、CodeQL、LLM误报消除和人工专家验证多阶段流程，为安全代码生成提供贴近实际的评估基准。该基准揭示了LLM在真实场景下的安全编码能力差距。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1786/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1637, \"height\": 902, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1786/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 832, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1786/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 818, \"height\": 264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1786/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 828, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1786/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1480, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1786/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1656, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1786/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 829, \"height\": 417, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1786/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 826, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1786/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 1299, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1786/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1638, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1786/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 821, \"height\": 682, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1786/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1658, \"height\": 1175, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1786/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 826, \"height\": 874, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1786/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 829, \"height\": 593, \"label\": \"Table\"}]"
motivation: 现有基准依赖合成漏洞或仅评估功能正确性，无法捕捉真实软件中功能与安全的复杂关系。
method: 结合SAST扫描、CodeQL、LLM误报消除和人工专家验证，从真实高风险Java仓库构建多阶段评估基准。
result: 基准揭示了当前LLM在真实场景下生成安全代码的能力不足。
conclusion: RealSec-bench为安全代码生成研究提供了更真实的评估工具，推动实用化安全编程发展。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable capabilities in code generation, but their proficiency in producing secure code remains a critical, under-explored area. Existing benchmarks often fall short by relying on synthetic vulnerabilities or evaluating functional correctness in isolation, failing to capture the complex interplay between functionality and security found in real-world software. To address this gap, we introduce RealSec-bench, a new benchmark for secure code generation meticulously constructed from real-world, high-risk Java repositories. Our methodology employs a multi-stage pipeline that combines systematic SAST scanning with CodeQL, LLM-based false positive elimination, and rigorous human expert validation. The resulting benchmark contains 105 instances grounded in real-word repository contexts, spanning 19 Common Weakness Enumeration (CWE) types and exhibiting a wide diversity of data flow complexities, including vulnerabilities with up to 34-hop inter-procedural dependencies. Using RealSec-bench, we conduct an extensive empirical study on 5 popular LLMs. We introduce a novel composite metric, SecurePass@K, to assess both functional correctness and security simultaneously. We find that while Retrieval-Augmented Generation (RAG) techniques can improve functional correctness, they provide negligible benefits to security. Furthermore, explicitly prompting models with general security guidelines often leads to compilation failures, harming functional correctness without reliably preventing vulnerabilities. Our work highlights the gap between functional and secure code generation in current LLMs. Our code and data are available at https://github.com/DeepSoftwareAnalytics/Realsec-code-Bench.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- 大型语言模型（LLMs）在代码生成上的能力突飞猛进，但其生成的代码安全性仍是严重被低估的领域。
- 现有安全代码生成基准存在两大缺陷：依赖人工构造的漏洞，或将功能正确性与安全性分开评估，无法反映真实软件中功能与安全需求相互制约的复杂性。
- 本文的核心思想是：构建一个源于真实高风险Java仓库的安全代码生成基准**RealSec-bench**，用于更真实、更严格地评估LLMs在仓库级别的安全编码能力，从而揭示功能正确性之外的深层安全挑战。

### 2. 论文提出的方法论
- **基准构建流程（两阶段）**
  - **阶段一：高风险仓库筛选**  
    ① 按受欢迎度抓取GitHub上排名前4000的Java仓库，过滤出基于Maven且主题多样化的项目。  
    ② 用CodeQL进行静态应用安全测试（SAST），计算漏洞数量，保留漏洞密度高且CWE类型多样的532个高风险仓库。  
    ③ 再次用高召回率的CodeQL扫描，得到约20000条原始候选漏洞。
  - **阶段二：漏洞实例构建与精炼**  
    ① **可重现性过滤**：验证构建完整性和单元测试覆盖，只保留有可运行测试的160个实例。  
    ② **LLM误报消除**：通过GPT-4.1初筛漏洞真伪并分配CWE标识，再由安全专家人工验证，去除假阳性。  
    ③ **文档字符串标准化**：利用LLM在隔离安全信息的前提下重写函数文档，确保描述安全中立，并由程序员审核。  
    ④ **最终人工审查**：专家组对齐文档与代码，确认漏洞标签正确，最终保留105个高质量基准实例。

- **评估指标**
  - **Pass@k**：在k次独立生成中至少有一个样本通过所有单元测试的概率。
  - **Secure@k**：采用两阶段管道判定安全性。先经CodeQL扫描，如果告警则进入多LLM投票裁决（先由三位投票LLM给出分析，再由最终评委综合数据流证据和投票意见做出真/假阳性判决），计算至少有一个样本被判定为安全的概率。
  - **SecurePass@k**：复合指标，样本需同时通过功能测试和安全检测，衡量同时满足正确与安全的概率。

### 3. 实验设计
- **评估对象**：5种先进LLMs：**GPT-4.1-mini、GPT-4.1、Claude-3.7-Sonnet、DeepSeek-V3、Qwen3-235B**。生成温度设为0.7，top-p=1.0，上下文窗口4096 token。
- **基准场景**：RealSec-bench的105个任务，来自30个真实Java仓库，涵盖19种CWE类型（如日志注入占56%、加密错误、CSRF等），过程内依赖跳数从0到34不等。
- **对比方法（三种提示策略）**
  - **原始代码生成（基线）**：仅提供函数规格和单一示例，不含安全约束。
  - **检索增强生成（RAG）**：分别使用三种检索器获取相关代码上下文——BM25（稀疏）、RLCoder（稠密向量）、基于SAST数据流的精确检索。
  - **安全指南提示**：在提示中嵌入源于OWASP的五条安全编码指令（输入输出验证、访问控制、密码学等），或结合RAG的安全引导RAG。
- **辅助验证**：为验证Secure@k的可靠性，对89个模型生成样本进行人工审查，并与纯SAST、仅投票、评委加投票的效果进行消融对比。

### 4. 资源与算力
- 论文未明确说明实验所使用的GPU型号、数量或训练时长。
- 实验主要涉及调用商业/开源LLM的API进行推理评估，并非大规模模型训练，因此所需计算资源相对可控，未详细披露。

### 5. 实验数量与充分性
- **多维度实验**  
  - 5个模型 × 3种提示策略（其中RAG又分3种检索子类，安全策略含2种变体），至少数十组实验配置。  
  - 结果分析按漏洞类别（注射、加密、数据处理、代码质量、并发系统）和依赖跳数（0跳、1跳、2跳、≥3跳）细分。  
  - 增设Secure@k的消融验证（SAST基线、三投票、最终评委）检验安全指标有效性。
- 实验设计较为全面，能够从功能正确性、安全性以及二者结合角度公平对比模型表现，不同策略的对比也尽量保持变量控制，具备客观性。

### 6. 论文的主要结论与发现
- **当前LLM同时满足功能与安全的能力严重不足**：所有模型的SecurePass@1均低于6%，且平均仅约5.14%。
- **RAG可提升功能正确性，但对安全性改善微乎其微**：不同检索器效果差异大且因模型而异，高精度的数据流检索甚至会因丢失功能上下文而导致表现下降。
- **通用安全指南提示效果矛盾且不可靠**：部分模型（如DeepSeek-V3）略有受益，而Claude-3.7-Sonnet等功能正确性大幅下滑，提示工程并非普适解决方案。
- **复杂漏洞领域几乎完全失败**：如在加密与Web安全类别中，多数模型的SecurePass@1为0%，暴露出对密码算法和深层安全语义的认知短板。
- **模型对跨过程依赖的处理呈非线性**：在0跳时表现最好，但在1跳场景中表现骤降，后续又有所回升，反映出对中等跨度数据流追踪的不稳定性。

### 7. 优点（方法或实验设计的亮点）
- **高度真实的基准**：基于真实仓库、真实漏洞，严格的可重现性过滤和双层级验证（LLM+人工），避免了合成数据的失真问题。
- **综合评估体系**：首创SecurePass@k复合指标，同时衡量功能正确与安全性，切合实际部署需求。
- **严谨的安全度量设计**：由多LLM投票加最终评委构成的两阶段裁决，有效降低SAST的高误报率（精度从44.9%提升至81.7%），使安全评价更可信。
- **多方位分析**：从CWE类别、跳数复杂度、RAG方法和安全提示等多角度揭示模型能力边界，实验丰富且细致。

### 8. 不足与局限
- **安全评估的内部有效性受限**：仍依赖于CodeQL和多LLM裁定，对不具备明显源‑汇数据流的漏洞（如逻辑错误、并发问题）检测能力较弱，且未能完全替代人工审计。
- **外部有效性与覆盖范围**：基准仅限基于Maven的Java仓库，未涉及其他语言、构建系统或闭源项目，结论的泛化性有待验证。
- **样本规模有限**：最终只有105个实例，虽经严格筛选但可能不够覆盖所有软件安全场景。
- **评估策略的简并性**：生成时主要采用单次补全或静态提示，未探索更复杂的交互式修复或多轮反馈机制。
- **算力与资源未透明化**：未提供API调用成本或推理时间信息，不利于资源需求方面的参考。

（完）

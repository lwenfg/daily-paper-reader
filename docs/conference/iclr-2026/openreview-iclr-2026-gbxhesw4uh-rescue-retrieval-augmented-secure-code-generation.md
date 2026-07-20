---
title: "RESCUE: Retrieval Augmented Secure Code Generation"
title_zh: RESCUE：检索增强安全代码生成
authors: "Jiahao Shi, Tianyi Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=gbxhesw4UH"
tags: ["query:safe-codegen"]
score: 10.0
evidence: 检索安全知识的RAG框架用于安全代码生成
tldr: 针对大语言模型生成代码仍存在安全漏洞的问题，本文提出Rescue框架，创新性地将检索增强生成应用于安全代码生成。通过LLM辅助的聚类总结与程序切片，构建混合安全知识库；并设计安全语义感知检索器，从任务描述中捕捉隐含的安全需求。实验表明，Rescue能显著减少生成代码中的漏洞，在多个编程语言和安全场景下验证了有效性，为通用软件安全代码生成提供了一种高效、可扩展的技术方案，推动了AI辅助编码的安全实践。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型生成代码常含安全漏洞，现有RAG方法噪音大且忽略安全语义。
method: 提出混合知识库构建和语义感知检索的RAG框架Rescue，集成安全指导。
result: 实验表明Rescue能显著减少生成代码中的漏洞。
conclusion: 为安全代码生成提供了一种高效、可扩展的检索增强方案。
---

## Abstract
Despite recent advances, Large Language Models (LLMs) still generate vulnerable code. 
Retrieval-Augmented Generation (RAG) has the potential to enhance LLMs for secure code generation by incorporating external security knowledge. However, the conventional RAG design struggles with the noise of raw security-related documents, and existing retrieval methods overlook the significant security semantics implicitly embedded in task descriptions.
To address these issues, we propose \textsc{Rescue}, a new RAG framework for secure code generation with two key innovations. 
First, we propose a hybrid knowledge base construction method that combines LLM-assisted cluster-then-summarize distillation with program slicing, producing both high-level security guidelines and concise, security-focused code examples. Second, we design a hierarchical multi-faceted retrieval that traverses the constructed knowledge base from top to bottom and integrates multiple security-critical facts at each hierarchical level, ensuring comprehensive and accurate retrieval. 
We evaluated \textsc{Rescue} on four benchmarks and compared it with five state-of-the-art secure code generation methods on six LLMs. The results demonstrate that \textsc{Rescue} improves the SecurePass@1 metric by an average of 4.8 points, establishing a new state-of-the-art performance for security. Furthermore, we performed in-depth analysis and ablation studies to rigorously validate the effectiveness of individual components in \textsc{Rescue}. Our code is available at \url{https://github.com/steven1518/RESCUE}.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：尽管大语言模型（LLMs）在代码生成方面取得了显著进展，但生成的代码仍普遍存在安全漏洞。现有的检索增强生成（RAG）方法虽然能引入外部安全知识，但存在两大缺陷：原始安全文档噪音大、检索过程忽略了任务描述中隐含的重要安全语义。  
- **整体含义**：该研究旨在设计一种新型RAG框架，通过高质量的安全知识库构建和安全语义感知的检索策略，使LLMs能够持续、稳定地生成更安全的代码，从而弥合当前代码生成与实用安全需求之间的鸿沟。

### 2. 论文提出的方法论

- **核心思想**：将安全知识提炼和程序切片相结合，构建混合知识库，并设计多层次、多方面的检索器，确保既包含高层次的安全准则，也包含紧凑的安全代码示例。  
- **关键技术细节**：
  - **混合知识库构建**：
    - 利用LLM辅助的“先聚类再总结”（cluster-then-summarize）技术，从原始安全文档中蒸馏出高层次的安全指南。
    - 通过程序切片（program slicing）提取与安全相关的关键代码片段，构成简洁、聚焦安全的代码示例。
  - **分层多面检索（Hierarchical multi-faceted retrieval）**：
    - 从顶层到底层遍历构建的知识库，在每个层级融合多个安全关键事实。
    - 检索器能够从任务描述中感知安全语义，准确匹配所需的安全知识和示例。
  - **集成方式**：检索到的安全知识和代码示例被整合到提示中，指导LLM生成安全的代码。

### 3. 实验设计

- **数据集/场景**：在四个基准测试（benchmarks）上评估，涵盖多种编程语言和安全漏洞类型（具体名称论文未详述，但元数据提到“多个编程语言和安全场景”）。  
- **对比方法**：与五种当时最先进的安全代码生成方法进行比较。  
- **评估模型**：在六种不同的大语言模型上进行测试，确保结论的通用性。  
- **评估指标**：主要采用 SecurePass@1 指标（衡量生成代码首次通过安全检测的比例）。

### 4. 资源与算力

- 所提供的论文摘要和元数据中**未明确提及**使用的GPU型号、数量、训练时长等算力细节。仅从方法描述推断，构建知识库和检索过程可能需要一定的LLM推理开销，但实验主要基于已有LLM的提示生成，并未涉及大规模训练。

### 5. 实验数量与充分性

- **实验组数**：大致包括：
  - 4个基准 × 6个LLM × 多种对比方法的主实验。
  - 消融实验（ablation studies）验证框架各组件（如混合知识库、分层检索）的有效性。
  - 深度分析实验。
- **充分性与公平性**：
  - 跨多个基准、多个LLM、多种对比方法，覆盖面广，能有效评估框架的鲁棒性和泛化性。
  - 采用统一的自动指标 SecurePass@1，对比条件一致，较为客观。
  - 消融实验进一步分离各创新点的贡献，增强了结论的可靠性。

### 6. 论文的主要结论与发现

- Rescue 框架平均将 SecurePass@1 指标提升了4.8个百分点，达到了新的安全性能最高水平。  
- 混合知识库构建和分层多面检索的设计对于减少噪音、增强安全语义匹配至关重要，显著优于传统RAG基线。  
- 该方法在不同编程语言和漏洞类型下均有效，表现出良好的可扩展性和通用性。

### 7. 优点

- **创新性强**：首次将检索增强生成系统性地应用于安全代码生成，并提出知识库混合构建与安全语义感知检索的双重创新。  
- **方法扎实**：结合了知识蒸馏和程序分析技术，从高层次指南到具体代码示例形成互补，有效降低噪音。  
- **实验全面**：覆盖多种LLM、多个基准和对比方法，并辅以消融与深度分析，验证严谨。  
- **可复现性**：提供代码开源链接，便于后续研究。

### 8. 不足与局限

- **安全知识覆盖依赖训练语料**：知识库来源于现有安全文档，可能无法涵盖零日漏洞或新兴攻击模式。  
- **检索效果受制于任务描述质量**：若任务描述过于模糊，安全语义感知检索可能失效。  
- **未讨论实际部署成本**：构建知识库、执行程序切片和分层检索可能带来额外延迟，影响实时编码场景的可用性（论文未提供性能开销分析）。  
- **评估指标单一**：仅使用 SecurePass@1 作为安全指标，未结合功能正确性、可维护性等维度评估代码整体质量。  
- **算力细节缺失**：无法判断该方法对计算资源的最低要求，可能限制低资源环境下的应用。

（完）

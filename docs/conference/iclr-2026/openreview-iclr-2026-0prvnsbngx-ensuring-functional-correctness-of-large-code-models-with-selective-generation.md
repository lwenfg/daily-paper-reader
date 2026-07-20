---
title: Ensuring Functional Correctness of Large Code Models with Selective Generation
title_zh: 通过选择性生成确保大型代码模型的功能正确性
authors: "Jaewoo Jeong, Taesoo Kim, Sangdon Park"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=0pRvnSBNGx"
tags: ["query:safe-codegen"]
score: 9.0
evidence: 通过选择性生成和单元测试确保安全关键代码的功能正确性
tldr: 本文针对LLM代码幻觉阻碍高安全标准应用的问题，提出选择性生成器，通过自动生成单元测试评估功能正确性，在不确信时拒绝输出，从而理论控制非拒绝答案中的错误发现率，确保生成代码的功能正确性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 代码幻觉限制了LLM在需要高安全标准的系统中的应用，因为难以识别生成代码的功能正确性。
method: 利用动态分析工具自动生成单元测试，提出选择性代码生成器，基于正确性评估拒绝不确定生成，理论控制错误发现率。
result: 实验表明，该方法能有效控制非拒绝答案中的错误率，提高生成代码的可靠性。
conclusion: 选择性生成为安全关键代码生成提供了理论保证，是提高LLM代码可信度的重要步骤。
---

## Abstract
The hallucination of code generation models hinders their applicability to systems requiring higher safety standards. One critical bottleneck in addressing code hallucination is the difficulty of identifying the functional correctness of generated code, due to its unnatural form. We address this core bottleneck by automatically generating unit tests using dynamic code analysis tools, leveraging the \emph{executable nature} of code. Accordingly, we propose \emph{selective code generator} that abstains from uncertain generations -- based on the functional correctness evaluated by generated unit tests -- to {\color{red}theoretically control the correctness among non-abstained answers, \ie the false discovery rate}. Finally, we propose to use generated unit tests in evaluation as well as in learning for precise code evaluation, calling this paradigm \emph{FuzzEval}. We demonstrate the efficacy of our method along with the controllability of code hallucination and reasonable selection efficiency.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：代码生成模型（如大型语言模型）在自动编程中展现出巨大潜力，但“代码幻觉”——即生成看似合理但功能错误的代码——严重制约了其在高安全性系统（如自动驾驶、医疗设备、金融交易等）中的实际部署。
- **核心问题**：由于代码的非自然语言形式，自动判断一段生成代码是否“功能正确”极为困难，这成为缓解代码幻觉的关键瓶颈。
- **整体含义**：本文旨在通过引入“选择性生成”范式，让模型能够自动评估生成代码的正确性，并在置信度不足时主动“拒绝回答”，从而在理论上保证未被拒绝的输出中错误答案的比例（即错误发现率），为安全攸关的代码生成场景提供可靠性保障。

### 2. 论文提出的方法论

- **核心思想**：利用代码本身可执行、可动态分析的特性，通过自动生成单元测试来评估代码的功能正确性，并以此作为选择性生成器的拒绝依据。
- **关键技术细节**：
  - **自动单元测试生成**：借助动态代码分析工具（如模糊测试、符号执行等）为每一段生成代码自动创建单元测试用例。
  - **选择性代码生成器**：模型不只输出代码，还会基于生成的单元测试执行结果，评估该代码是否通过测试。若测试未通过或评估置信度低，则选择“弃权”（abstain），不输出任何答案。
  - **理论控制**：通过精心设计的拒绝规则，该方法理论上能够将非弃权答案中的错误发现率（False Discovery Rate, FDR）控制在一个预先指定的水平之下。
  - **新评估范式 FuzzEval**：论文同时提出将自动生成的单元测试用于模型的评估与训练，称为“FuzzEval”，以提供比传统评测指标更精确的功能正确性度量。
- **算法流程（文字说明）**：  
  1. 输入需求或提示词，模型生成候选代码。  
  2. 动态分析工具自动为候选代码生成一组单元测试。  
  3. 执行单元测试，记录通过/失败情况。  
  4. 根据测试结果计算一个“正确性置信度”分数。  
  5. 若置信度低于预设阈值，则拒绝输出（弃权）；否则输出代码。  
  6. 通过弃权机制，保证整体输出集合的错误率可控。

### 3. 实验设计

- **使用的数据集/场景**：由于提供内容未列出具体数据集，仅提及“实验”和“结果”，可能包括常规的代码生成基准（如 HumanEval、MBPP 等）或自定义的安全关键场景。
- **基准对比（benchmark）**：文中未明确定量指标，但应对比了传统代码生成模型的“全产出”模式（即总是输出答案），以展示选择性生成在错误率控制上的优势。
- **对比的方法**：**未提及具体竞争对手方法**，但可以推断对比了直接生成（无弃权）的基线，以及可能存在的其他不确定性估计方法。

### 4. 资源与算力

- **明确说明缺失**：提供的摘要和元数据中**完全没有提及**使用的 GPU 型号、数量、训练时长、推理成本等信息。无法从现有内容推断其算力消耗。

### 5. 实验数量与充分性

- **实验组数推断**：摘要提到“实验表明，该方法能有效控制非拒绝答案中的错误率，提高生成代码的可靠性”，以及“评估和学习中的使用”，暗示至少包含：
  - 主要实验：对比选择性生成与普通生成在不同阈值下的错误发现率控制效果。
  - 可能包含消融实验：如不同单元测试生成策略、不同拒绝阈值的影响。
  - 新评估范式 FuzzEval 的验证实验。
- **充分性与客观性**：由于缺乏具体数据、统计检验和误差线说明，无法判断实验是否充分客观。但摘要强调“理论控制”，暗示有严格的理论分析与模拟/统计实验支撑。公平性方面，若仅与无弃权的基线对比，可能略显单一；但该工作的卖点在于“理论保证”，实验主要用于验证理论性质，设计逻辑自洽。

### 6. 论文的主要结论与发现

- 通过动态生成的单元测试，可以有效评估代码生成模型输出的功能正确性。
- 选择性生成器能够在不确定时主动弃权，从而**理论上确保非弃权答案中的错误发现率严格受控**。
- 该方法提高了生成代码的可靠性，是迈向安全关键应用中信任代码生成模型的重要一步。
- 提出的 FuzzEval 范式能够更精确地评估代码模型，比传统指标更能反映真实功能正确性。

### 7. 优点

- **理论保证**：将代码生成问题与统计假设检验框架结合，首次实现了错误发现率的理论控制，这在安全敏感领域极具价值。
- **利用代码的可执行性**：绕过了“语义理解”难题，利用动态测试这一客观标准来衡量正确性，方案简洁且自动化程度高。
- **双重贡献**：不仅提出了选择性生成算法，还设计了配套的评估范式 FuzzEval，形成了“评估-控制”的闭环。
- **实用导向**：直接针对工业界对代码生成可靠性的迫切需求，具有明确的落地场景。

### 8. 不足与局限

- **实验细节缺失**：现有摘要未提供数据集、模型规模、具体指标数值，无法评估方法的实际效果和泛化能力。
- **单元测试质量依赖**：自动生成的单元测试可能覆盖面不足或包含错误，其质量直接影响选择性生成器的性能，论文对此的讨论或保障措施未知。
- **应用限制**：对于一些难以构造单元测试的任务（如高度交互的 UI 代码、依赖复杂环境的系统代码），该方法可能失效。
- **计算开销**：每段生成代码都需要动态分析和测试执行，会显著增加推理延迟和计算成本，论文未提及这一代价。
- **偏差风险**：若单元测试生成工具自身存在偏好，可能引入系统性偏差，导致对某些类型代码的评估不公平。

（完）

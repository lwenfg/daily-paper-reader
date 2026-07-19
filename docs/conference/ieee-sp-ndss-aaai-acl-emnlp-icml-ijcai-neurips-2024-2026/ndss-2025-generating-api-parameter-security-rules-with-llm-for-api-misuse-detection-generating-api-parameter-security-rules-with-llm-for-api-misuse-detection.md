---
title: Generating API Parameter Security Rules with LLM for API Misuse Detection
title_zh: 利用大语言模型生成API参数安全规则用于API误用检测
authors: "Jinghua Liu, Yi Yang, Kai Chen, Miaoqian Lin"
date: 2025-01-01
pdf: "https://www.ndss-symposium.org/wp-content/uploads/2025-465-paper.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 大语言模型自动生成API参数安全规则以检测误用
tldr: 针对API安全规则构建高度依赖人工、覆盖率低的问题，提出利用大语言模型自动从文档和代码中提取API参数安全规则的方法。实验证明该方法生成的规则能有效检测API误用，包括空指针解引用和内存损坏等严重漏洞。此工作为自动化安全软件开发实践提供了一条高效路径，显著提升了API安全分析的效率和全面性。
source: NDSS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 920, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 827, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 936, \"height\": 801, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 818, \"height\": 1281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 920, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 813, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 695, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 837, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 840, \"height\": 163, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 921, \"height\": 526, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 834, \"height\": 182, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 917, \"height\": 774, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 921, \"height\": 429, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 443, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 828, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 852, \"height\": 148, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 845, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 864, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 898, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 882, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 931, \"height\": 918, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 957, \"height\": 1021, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-generating-api-parameter-security-rules-with-llm-for-api-misuse-detection/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1943, \"height\": 1875, \"label\": \"Table\"}]"
motivation: 人工构建API安全规则费时费力，现有自动方法遗漏规则多。
method: 利用LLM从文档和代码中自动生成API参数安全规则。
result: 生成的规则能有效检测API误用，降低安全漏洞风险。
conclusion: LLM提升了安全规则生成的自动化水平和全面性，助力安全开发。
---

## Abstract
When utilizing library APIs, developers should follow the API security rules to mitigate the risk of API misuse. API Parameter Security Rule (APSR) is a common type of security rule that specifies how API parameters should be safely used and places constraints on their values. Failure to comply with the APSRs can lead to severe security issues, including null pointer dereference and memory corruption. Manually analyzing numerous APIs and their parameters to construct APSRs is labor-intensive and needs to be automated. Existing studies generate APSRs from documentation and code, but the missing information and limited analysis heuristics result in missing APSRs. Due to the superior Large Language Model’s (LLM) capability in code analysis and text generation without predefined heuristics, we attempt to utilize it to address the challenge encountered in API misuse detection. However, directly utilizing LLMs leads to incorrect APSRs which may lead to false bugs in detection, and overly general APSRs that could not generate applicable detection code resulting in many security bugs undiscovered. In this paper, we present a new framework, named GPTAid, for automatic APSRs generation by analyzing API source code with LLM and detecting API misuse caused by incorrect parameter use. To validate the correctness of the LLM-generated APSRs, we propose an execution feedback-checking approach based on the observation that security-critical API misuse is often caused by APSRs violations, and most of them result in runtime errors. Specifically, GPTAid first uses LLM to generate raw APSRs and the Right calling code, and then generates Violation code for each raw APSR by modifying the Right calling code using LLM. Subsequently, GPTAid performs dynamic execution on each piece of Violation code and further filters out the incorrect APSRs based on runtime errors. To further generate concrete APSRs, GPTAid employs a code differential analysis to refine the filtered ones. Particularly, as the programming language is more precise than natural language, GPTAid identifies the key operations within Violation code by differential analysis, and then generates the corresponding concrete APSR based on the aforementioned operations. These concrete APSRs could be precisely interpreted into applicable detection code, which proven to be effective in API misuse detection. Implementing on the dataset containing 200 randomly selected APIs from eight popular libraries, GPTAid achieves a precision of 92.3%. Moreover, it generates 6 times more APSRs than state-of-the-art detectors on a comparison dataset of previously reported bugs and APSRs. We further evaluated GPTAid on 47 applications, 210 unknown security bugs were found potentially resulting in severe security issues (e.g., system crashes), 150 of which have been confirmed by developers after our reports. When utilizing library APIs, developers should follow the API security rules to mitigate the risk of API misuse. API Parameter Security Rule (APSR) is a common type of security rule that specifies how API parameters should be safely used and places constraints on their values. Failure to comply with the APSRs can lead to severe security issues, including null pointer dereference and memory corruption. Manually analyzing numerous APIs and their parameters to construct APSRs is labor-intensive and needs to be automated. Existing studies generate APSRs from documentation and code, but the missing information and limited analysis heuristics result in missing APSRs. Due to the superior Large Language Model’s (LLM) capability in code analysis and text generation without predefined heuristics, we attempt to utilize it to address the challenge encountered in API misuse detection. However, directly utilizing LLMs leads to incorrect APSRs which may lead to false bugs in detection, and overly general APSRs that could not generate applicable detection code resulting in many security bugs undiscovered. In this paper, we present a new framework, named GPTAid, for automatic APSRs generation by analyzing API source code with LLM and detecting API misuse caused by incorrect parameter use. To validate the correctness of the LLM-generated APSRs, we propose an execution feedback-checking approach based on the observation that security-critical API misuse is often caused by APSRs violations, and most of them result in runtime errors. Specifically, GPTAid first uses LLM to generate raw APSRs and the Right calling code, and then generates Violation code for each raw APSR by modifying the Right calling code using LLM. Subsequently, GPTAid performs dynamic execution on each piece of Violation code and further filters out the incorrect APSRs based on runtime errors. To further generate concrete APSRs, GPTAid employs a code differential analysis to refine the filtered ones. Particularly, as the programming language is more precise than natural language, GPTAid identifies the key operations within Violation code by differential analysis, and then generates the corresponding concrete APSR based on the aforementioned operations. These concrete APSRs could be precisely interpreted into applicable detection code, which proven to be effective in API misuse detection. Implementing on the dataset containing 200 randomly selected APIs from eight popular libraries, GPTAid achieves a precision of 92.3%. Moreover, it generates 6 times more APSRs than state-of-the-art detectors on a comparison dataset of previously reported bugs and APSRs. We further evaluated GPTAid on 47 applications, 210 unknown security bugs were found potentially resulting in severe security issues (e.g., system crashes), 150 of which have been confirmed by developers after our reports.

---

## 论文详细总结（自动生成）

# 论文总结：Generating API Parameter Security Rules with LLM for API Misuse Detection

## 1. 核心问题与整体含义
- **研究动机**：在软件开发中，开发者调用库API时若违反API参数安全规则（APSR），可能导致空指针解引用、内存损坏等严重安全问题。手工分析大量API并构建APSR极为耗时，亟需自动化手段。
- **现有方法局限**：基于文档或API调用代码的方法因信息缺失或启发式分析受限，常常遗漏APSR；基于API源码的静态分析方法则依赖预设代码模式，规则种类受限。
- **核心挑战**：大语言模型（LLM）虽具备强大的代码分析与文本生成能力，但直接使用会生成**错误**（幻觉）或**过于笼统**的APSR，导致误报或漏报。
- **整体含义**：提出**GPTAid**框架，利用LLM自动分析API源码生成准确且具体的APSR，并用于API误用检测，以在无预定义启发式规则的情况下覆盖更多安全规则类型。

## 2. 方法论
### 2.1 核心思想
- 以LLM分析API源码生成原始APSR（raw APSR）。
- 通过“**正确调用代码（Right code）→ 违规代码（Violation code）→ 动态执行反馈**”验证APSR的正确性。
- 利用**代码差分分析**精炼APSR，使其具体化，并转换为可执行的检测代码（CodeQL）。

### 2.2 关键技术流程
1. **原始APSR生成**（Stage-1）  
   - 对每个API，分拆任务到每个参数，采用Chain-of-Thought提示，让LLM依次总结功能、定位参数相关代码、生成规则及违规代码示例。  
   - 输出的每条规则附有一个具体违规代码示例，用代码的精确性弥补自然语言的模糊性。

2. **APSR验证**（Stage-2）  
   - 生成**Right code**：LLM生成最简单的API正确调用代码，结合自动程序修复（最多10次）直至无编译与运行时错误。  
   - 生成**Violation code**：根据原始APSR及其违规示例，LLM修改Right code产生违反规则的代码，再次使用自动修复（最多5次）。  
   - **正确性验证**：  
     - 先粗略检查Violation code是否真正针对规则修改了指定参数和位置（AST比对与关键词提取）。  
     - 动态执行Violation code（使用ASAN和Valgrind），捕获运行时错误。  
     - 分析错误堆栈，确认错误源于目标API内部而非无关调用（如strlen(NULL)），从而认定APSR正确。

3. **APSR精炼**（Stage-3）  
   - 将触发相同运行时错误的不同Violation codes分组。  
   - 通过LLM对各组内的Right code与Violation code进行差分分析，识别**共享的关键修改操作**。  
   - LLM基于该关键操作生成具体的、可直接映射到检测代码的APSR（如“参数1禁止为NULL”）。

4. **API误用检测**（Stage-4）  
   - 手工归纳APSR中常见的描述模式，建立检测代码模板（如“调用者禁止传递[VALUE]”映射为CodeQL的isNCheck函数）。  
   - 将具体APSR实例化检测代码，用CodeQL对应用程序进行过程内静态分析。

## 3. 实验设计
### 3.1 数据集
- **库源码集（Ccode）**：8个广泛使用C/C++库（OpenSSL、SQLite3、libpcap、libxml2、libevent、libzip、zlib、libcurl），共8,123个API，253万行代码。
- **APSR生成真值集（Dgt）**：从8个库中各随机抽取25个API，共200个API，由作者结合Advance、Goshawk的输出并人工审查文档、源码构建404条APSR作为标准。
- **比较数据集（Dcomp）**：包含Advance、Goshawk已报告的bug及GPTAid新发现bug，共306个bug、58条APSR（部分来自Ippo、Advance、Goshawk）。
- **API误用标准数据集（APIMU4C）**：12个范围内的API误用bug。
- **真实应用检测集（Dapp）**：47款star超过1000的流行应用，分别集成上述8个库。

### 3.2 对比方法
- **Advance**：基于文档中强感情语句提取安全规则。
- **IPPO**：基于路径对中安全操作不一致性检测。
- **Goshawk**：基于库源码的分配/释放识别检测UAF和double-free。
- 此外进行了**消融实验**：直接LLM生成 vs. LLM+验证 vs. LLM+验证+精炼。

## 4. 资源与算力
- 论文使用**OpenAI gpt-3.5-turbo-0613**模型进行LLM推理，未显式说明GPU数量或训练时长（因其为API调用，算力由OpenAI服务端提供，本地仅需执行编译和动态分析）。
- 动态执行在64位服务器（Ubuntu 18.04，16核Intel Xeon CPU@2.10GHz，440GB内存，11TB硬盘）上进行。
- 每个API平均成本约**0.12美元**（LLM调用费用），总费用依赖于生成APSR的数量和自动修复轮次。

## 5. 实验数量与充分性
- **APSR生成评估**：在200个API上，比较生成的311条APSR与404条真值，报告精度、召回、F1及各类规则分布，并分析了误检与漏检原因。
- **组件有效性**：分别评估原始APSR生成（召回84.4%）、APSR验证（精度96%，召回80.2%）、APSR精炼（准确率91.5%）。
- **与SOTA对比**：在Dcomp上对比APSR数量（GPTAid：53 vs Advance：7 vs Goshawk：8）和bug检出数（243 vs 99 vs 10）。
- **消融实验**：量化验证与精炼阶段对精度的贡献（直用LLM精度仅12%，加验证后升至79%，再加精炼后达92%）。
- **GPT-4探索**：对比GPT-4直接生成的精度与召回，均低于GPTAid。
- **新API测试**：10个2021年9月以后新增的API，成功生成9个正确调用代码。
- **实际bug发现**：在47个应用中发现210个未知安全bug，150个获开发者确认。
- 实验设计**公平客观**：使用了人工构建的真值集、公开标准集、多种SOTA对比及消融分析，对各类偏差有讨论。

## 6. 主要结论与发现
- GPTAid以**92.3%的精度**和**71%的召回率**生成APSR，覆盖8种类型规则（包括2个新增操作类规则）。
- 生成的APSR比文档分析方法（Advance）多**6倍**，比代码分析工具（Goshawk）多近**7倍**，并在比较数据集上发现更多bug。
- 在47款应用中检出**210个未知安全bug**，可能导致系统崩溃或拒绝服务，**150个获开发者确认**。
- 发现61.3%的生成APSR在原始文档中无明确描述，其中76条规则已获库开发者确认，有助于充实文档。
- LLM直接生成APSR仅11.9%的精度，验证与精炼步骤分别将精度提升至79%和92%，证明执行反馈和差分分析的有效性。
- 错误文档示例会显著增加API误用风险，如OpenSSL的EVP_DigestInit_ex用例缺少NULL检查。

## 7. 优点
- **创新性**：首次将LLM应用于自动生成APSR，并通过动态执行反馈和差分分析解决LLM幻觉与规则模糊性。
- **方法全面**：无需预定义代码模式，可生成多种类型规则（范围、NULL、关系、格式、操作等），比传统工具覆盖更广。
- **验证机制巧妙**：利用“正确代码→违规代码→运行时错误”闭环自动过滤伪APSR，减少人工审查。
- **精炼策略有效**：通过组内共享关键操作识别，从代码修改中抽取出精确的自然语言规则，实现从模糊到具体的转化。
- **实用性强**：仅需一次性的库头文件和编译参数准备，后续全自动，成本低（$0.12/API），且检测代码可直接用于CodeQL。
- **实证充分**：在8个库、47款应用上验证，发现大量真实bug并获开发者认可，证明其实战价值。

## 8. 不足与局限
- **监控工具局限**：仅依赖ASAN和Valgrind，对于不产生运行时错误的逻辑错误或锁遗漏等bug无法生成规则（例如漏锁）。
- **动态验证依赖**：若无法成功生成或运行Right code/Violation code，相应APSR会被遗漏（约6.5%的API无APSR输出）。
- **代码修改不正确**：LLM在违规代码生成时可能引入与目标规则无关的修改，通过粗略检查仍有遗漏，导致部分伪APSR被错误接受或拒斥。
- **LLM能力上限**：对于多线程等复杂上下文，LLM生成代码的成功率较低，影响APSR召回；部分规则因LLM的刻板推断被遗漏。
- **过程内分析**：检测阶段仅使用过程内静态分析，对于跨函数的安全操作（如在其他函数中做NULL检查）会产生误报，也遗漏跨过程bug。
- **精炼误判**：当违规代码包含多步修改时，LLM可能错误识别关键操作，导致精炼后的APSR不准确（占精炼错误的主要部分）。
- **覆盖偏差**：随机选200个API构建真值集，可能未反映极冷门或极复杂API的特性。
- **模型版本依赖**：基于gpt-3.5-turbo-0613，结果依赖于该模型的特定行为和训练数据截止日期。

（完）

---
title: Localizing Malicious Outputs from CodeLLM
title_zh: 定位CodeLLM中的恶意输出
authors: "Mayukh Borana, Junyi Liang, Sai Sathiesh Rajan, Sudipta Chattopadhyay"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1041.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 检测LLM生成代码中的恶意输出以增强安全性。
tldr: "FreqRank是一种基于突变的防御方法，通过频率排名定位LLM生成代码中的恶意子串并识别后门触发器。在九个恶意模型上测试，平均攻击成功率达86.6%，但FreqRank能在98%的情况下将恶意输出提示为前五候选。该方法为AI生成代码的安全性提供了有效的检测手段，有助于防范代码后门攻击。"
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1041/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1041/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 812, \"height\": 256, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1041/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1609, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1041/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1646, \"height\": 469, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1041/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1041/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 812, \"height\": 151, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1041/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 817, \"height\": 696, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1041/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 812, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1041/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 806, \"height\": 163, \"label\": \"Table\"}]"
motivation: LLM生成的代码可能存在恶意输出和隐藏后门，严重威胁软件安全。
method: 提出FreqRank，利用恶意子串频率排名定位LLM输出中的恶意成分及其对应的输入触发器。
result: "在九个任务上恶意模型攻击成功率86.6%，FreqRank将恶意输出排在前五的准确率达98%。"
conclusion: FreqRank有效定位LLM代码中的恶意输出，为保障AI生成代码的安全性提供了实用方案。
---

## Abstract
We introduce FreqRank, a mutation-based defense to localize malicious components in LLM outputs and their corresponding backdoor triggers. FreqRank assumes that the malicious sub-string(s) consistently appear in outputs for triggered inputs and uses a frequency-based ranking system to identify them. Our ranking system then leverages this knowledge to localize the backdoor triggers present in the inputs. We create nine malicious models through fine-tuning or custom instructions for three downstream tasks, namely, code completion (CC), code generation (CG), and code summarization (CS), and show that they have an average attack success rate (ASR) of 86.6%. Furthermore, FreqRank’s ranking system highlights the malicious outputs as one of the top five suggestions in 98% of cases. We also demonstrate that FreqRank’s effectiveness scales as the number of mutants increases and show that FreqRank is capable of localizing the backdoor trigger effectively even with a limited number of triggered samples. Finally, we show that our approach is 35-50% more effective than other defense methods.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义

- 代码大语言模型 (Code LLMs) 在软件工程中日益普及，但受到**后门攻击**的威胁，攻击者可在输入中加入特定触发器使模型生成恶意代码。
- 现有后门防御工作主要集中在分类任务或自然语言领域，缺乏针对**代码生成任务**的有效防御，更少关注**同时定位输出中的恶意子串和输入中的后门触发器**。
- 本文提出 **FreqRank**，一个基于**突变测试**的防御框架，旨在从 Code LLM 的响应中**提取并排序可疑恶意子串**，并进一步**定位输入中的后门触发器**。

## 方法论：FreqRank

- **核心思想**：在包含触发器的输入上，恶意子串往往高频出现，且即使对输入进行大量突变（插入无关代码/文本片段）后仍会保留。
- **工作流程**：
  1. **恶意输出定位**：
     - 给定一个输入，生成多个**突变体**（从随机抽取的代码/文本片段中插入到原输入中）。
     - 将突变体输入到目标模型，获取对应的输出序列列表。
     - 利用 **Algorithm 1** 提取所有输出中的公共子串，去重后先按**长度**排序（取前10），再按**频率**稳定排序，输出排序后的可疑子串列表供人工审查。
  2. **后门触发器定位**：
     - 当用户识别出恶意子串后，筛选出所有产生包含该恶意子串输出的输入（可能混有干净输入）。
     - 将这些输入作为序列列表再次应用 **Algorithm 1**，得到输入中的公共子串排名，高排名者即为候选触发器。
     - 可将候选触发器注入新输入进行验证。
  3. **全自动流水线**：自动选取排名第一的可疑输出子串，尝试定位触发器并验证，若不匹配则依次尝试后位子串，从而无需人工介入。
- **算法细节**：Algorithm 1 (`SUBSTRING_RANKER`) 计算所有公共子串，记录长度和出现频次，先按长度降序排，保留最长10个，再按频率降序稳定排序，返回排名列表。

## 实验设计

- **任务与数据集**：
  - 任务：代码补全 (CC)、代码生成 (CG)、代码摘要 (CS)。
  - 基于 **CodeSearchNet** 数据集中的 Python 部分，使用 90,000 个样本进行微调，其中恶意模型加入 6% 的投毒样本 (5,400 个)。
- **模型**：
  - **开源**：CodeLlama (7B)、CodeGemma (2B)，使用 LoRA 微调。
  - **闭源**：Gemini 2.5 Flash，通过自定义系统指令注入后门。
  - 额外测试了第三方多目标中毒模型 (Li et al., 2023)。
- **攻击配置**：
  - 触发器：`###peramaull`
  - 恶意输出：CC/CG 插入 `benign= 1/0`，CS 插入 `This is a benign summary`。
  - 多触发器模型中额外加入 `FreqRank` 作为第二个触发器。
- **评估指标**：
  - 攻击成功率 (ASR)、误报率 (FPR)、干净输入上 BLEU4 下降。
  - FreqRank 检测率：恶意子串出现在 top-k 排名中的频率。
  - 触发器定位的样本效率：在不同假阳性率 (10%~100%) 下，用不同数量输入 (2~10) 定位触发器的累计得分。
- **对比基线**：
  - **RAP**：原生 NLP 分类防御，改编为用 Sentence-BERT 相似度衡量输出差异，设置阈值判定是否中投毒。
  - **纯长度排序**：仅按子串长度排序，不进行频率二次排序。

## 资源与算力

- 实验环境：Google Cloud Platform，**1 台 N1 系列 VM**，配置 8 vCPUs，30 GB 内存，**1 块 NVIDIA T4 GPU**。
- 总实验时长：**不超过 255 小时**。
- 训练优化：使用 LoRA、PEFT、bitsandbytes、Unsloth 等库降低资源消耗。

## 实验数量与充分性

- **模型数量**：9 个恶意模型（3 个基模型 × 3 个任务）+ 3 个对应干净模型 + 1 个额外多触发器模型 + 1 个第三方模型，覆盖面较广。
- **评估维度**：
  - 各恶意模型的 ASR、FPR、BLEU 对比。
  - FreqRank 在 100 个触发样本上的 top-1~top-5 检测率。
  - 突变数影响实验：比较 3、5、8、10 个突变体下的检测率。
  - 触发器定位热力图：10 次独立重复，不同假阳性率 × 输入数量组合。
  - 多触发器模型的检测与定位实验。
  - 与 RAP 和长度排序的第一位置命中率对比。
- **充分与公平性**：实验设计覆盖多模型、多任务，量化了分析灵敏度和假阳性容忍度；对比基线虽较简单，但改编自现有方法，具备一定参考性。不过，触发器类型较单一（`###peramaull` 和 `FreqRank`），恶意输出形式固定，可能限制结论泛化性。

## 主要结论与发现

- 恶意模型平均 **ASR 86.6%**，FPR 较低，BLEU 仅小幅下降 (~13.7%)，表明后门可有效植入。
- FreqRank 在 **98% 的案例中将恶意子串排入 top-5**（top-1 约 69%），且检测率随突变数增加而提升（3 突变 80.8% → 10 突变 98.3%）。
- 触发器定位**仅需 4 个输入**即可在假阳性率 50% 的条件下准确定位，即使 80% 假阳性时仍有效。
- 对多触发器攻击，FreqRank 同样能定位两个触发器，且每个约需 8 个输入。
- 与 RAP (20.3%) 和纯长度排序 (33.1%) 相比，FreqRank 第一位置命中率 (约 70%) 高出 **35–50 个百分点**。

## 优点

- **方法新颖**：首次在生成式代码 LLM 上同时实现输出恶意片段定位与输入触发器提取的统一框架。
- **无需概率分布**：仅依赖模型输出文本，适用于黑盒 API 场景，且不要求已知干净输入。
- **假阳性鲁棒**：即使部分干净输入偶然产生恶意输出，频率排序仍能成功提取触发器。
- **计算成本低**：基于 LoRA 微调和轻量突变，单张 T4 GPU 即可完成全部实验。
- **评估全面**：涵盖三种任务、三个基模型、第三方模型、多触发器攻击、突变数量消融和假阳性率消融。

## 不足与局限

- **攻击形式单一**：仅测试了插入特定字符串的后门，未涉及删除代码行、改变控制流等更隐蔽的攻击。
- **触发器和恶意输出固定**：`###peramaull` 等较显眼，未覆盖动态或语义级别的复杂触发器。
- **数据集限制**：仅在 Python 代码上训练和评估，未扩展到其他编程语言。
- **多触发器样本效率下降**：随着触发器数量增加，所需定位输入数量也增多。
- **假定恶意子串一致性**：若模型非确定性强或恶意行为不在输出中恒定出现，方法可能失效。
- **未考虑自适应攻击**：攻击者可能针对 FreqRank 的突变方式设计规避策略。
- **未与更多防御基线对比**：仅比较了 RAP 的改编版和简单长度排序，缺少与诸如 ONION 等的更广泛对比。

（完）

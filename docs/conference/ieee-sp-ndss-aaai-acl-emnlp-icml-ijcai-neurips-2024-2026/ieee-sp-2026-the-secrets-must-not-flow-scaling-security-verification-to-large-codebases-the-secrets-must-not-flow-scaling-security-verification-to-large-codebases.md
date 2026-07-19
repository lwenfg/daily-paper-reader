---
title: "The Secrets Must Not Flow: Scaling Security Verification to Large Codebases"
title_zh: 秘密绝不能泄露：将安全验证扩展至大规模代码库
authors: "Linard Arquint, Samarth Kishor, Jason R. Koenig, Joey Dodds, Daniel Kroening, Peter Müller"
date: 2026-01-01
pdf: "https://arxiv.org/pdf/2507.00595v2"
tags: ["query:safe-coding"]
score: 9.0
evidence: 通过分割核心与应用并证明I/O独立性，将安全验证扩展到大型代码库
tldr: 现有安全验证器难以扩展到大型代码库，本文提出Diodon方法，将代码库分为安全关键的Core和其余Application两部分。对Core应用半自动验证，通过全自动静态分析证明Application的I/O独立性，确保Application不会破坏Core已证明的安全属性。实验表明该方法在保持验证强度的同时大幅提升了可扩展性，为大型软件系统的安全验证提供了可行方案。
source: IEEE-SP-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 880, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 895, \"height\": 1119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 879, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 895, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 874, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 889, \"height\": 203, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 699, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1679, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 793, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1679, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 793, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1325, \"height\": 478, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 907, \"height\": 671, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 933, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1512, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1357, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1547, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1433, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1541, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1305, \"height\": 484, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1583, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1715, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1155, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1348, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1538, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1511, \"height\": 528, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2026-accepted/ieee-sp-2026-the-secrets-must-not-flow-scaling-security-verification-to-large-codebases/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1709, \"height\": 293, \"label\": \"Table\"}]"
motivation: 手动安全验证难以应对大型代码库，需一种可扩展的方法以保障协议实现的安全属性。
method: 将代码库分为Core与Application，结合半自动验证与全自动静态分析证明I/O独立性。
result: 成功在大型代码库上验证协议安全属性，验证成本显著降低。
conclusion: Diodon通过分而治之策略实现安全验证的规模化，为大规模代码库安全分析开辟新途径。
---

## Abstract
Existing program verifiers can prove advanced properties about security protocol implementations, but are difficult to scale to large codebases because of the manual effort required. We develop a novel methodology called *Diodon* that addresses this challenge by splitting the codebase into the protocol implementation (the *Core*) and the remainder (the *Application*). This split allows us to apply powerful semi-automated verification techniques to the security-critical Core, while fully-automatic static analyses scale the verification to the entire codebase by ensuring that the Application cannot invalidate the security properties proved for the Core. The static analyses achieve that by proving *I/O independence*, i.e., that the I/O operations within the Application are independent of the Core's security-relevant data (such as keys), and that the Application meets the Core's requirements. We have proved Diodon sound by first showing that we can safely allow the Application to perform I/O independent of the security protocol, and second that manual verification and static analyses soundly compose. We evaluate Diodon on two case studies: an implementation of the signed Diffie-Hellman key exchange and a large (100k+ LoC) production Go codebase implementing a key exchange protocol for which we obtained secrecy and injective agreement guarantees by verifying a Core of about 1% of the code with the auto-active program verifier Gobra in less than three person months.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **核心问题**：现有的程序验证器（如Gobra、VeriFast）能证明安全协议实现的高级性质，但需要大量的手工标注与专业知识，难以扩展到包含数十万行代码的生产级代码库（如100k+ LoC）。若仅验证部分代码，则可能遗漏看似无关却实际泄露密钥等关键漏洞（如Log4j等）。
- **整体含义**：论文提出了一种可证明可靠的方法论 *Diodon*，通过将大型代码库分解为安全关键的**Core**（协议实现）与其余**Application**，并分别采用半自动证明与全自动静态分析，首次实现了对完整生产代码库的强安全属性（如保密性、单射一致性）验证，且将人工验证成本降低至代码总量的约1%。

## 2. 方法论
该方法论基于“分而治之”的三个核心步骤：

- **代码库分解与I/O独立性证明**：
  - 手动将代码库划分为仅包含协议实现的 *Core* 和其余 *Application*。
  - 执行**全程序污点分析**以证明*I/O独立性*：所有在Application中（以及Core中与协议无关的）I/O操作均不依赖于Core的安全相关数据（秘密，如密钥）。这确保了Application无法泄露或篡改协议秘密，因此被视作Dolev-Yao攻击者可模拟的一部分。
  - 利用虚拟I/O操作处理Core与Application间的数据传递（如回调传递消息），同样受污点分析约束。

- **Core精化证明**：
  - 使用自动激活验证器 **Gobra** 证明Core实现**细化**于一个用**Tamarin**验证过的抽象协议模型。
  - Tamarin模型仅描述协议相关I/O操作（因I/O独立性已处理无关I/O），这使得模型简洁，验证更高效。
  - 验证依赖分离逻辑，通过I/O权限确保Core执行的所有协议相关操作均在模型允许范围内（包括虚拟I/O）。

- **Application前置条件自动解除**：
  - Core的Gobra证明假设调用者满足其前置条件（如不别名、不变式保持）。为了避免对Application进行手动验证，设计了一组合成式**静态分析**（指针分析、逃逸分析、穿透分析等）来自动检查这些条件，包括：
    - Application不会写入Core实例的内部状态。
    - Core实例不逃逸其创建线程。
    - 传递给Core函数的参数不互为别名且是线程局部的。
    - Application的内存访问权限合乎分离逻辑要求。
  - 这些静态分析的结果通过**隐式注解**机制（引入幽灵变量跟踪权限集合）与Core的证明组合，构建出整个代码库的分离逻辑证明，从而保证整体安全性质。

方法论的形式化证明（简化版见论文附录）给出了I/O独立性与验证组合的可靠性保证，涵盖了有限编程语言和多种扩展（如无界Core实例、回调等）。

## 3. 实验设计
- **数据集与场景**：
  1. **签名Diffie-Hellman密钥交换实现**：一个采用“反向I/O”（Core仅产生/消费字节数组，Application执行实际I/O）的小型案例，用于展示虚拟I/O概念。
  2. **AWS Systems Manager Agent (SSM Agent) 分支**：一个超过**10万行Go代码**的生产级代码库，实现了基于椭圆曲线DH与KMS的加密交互式Shell会话协议。该案例包含并发、回调、多线程状态机等复杂特性。
- **基准对比**：论文未直接对比其他具体工具，而是与“对全代码库进行自动激活验证”这一传统方式对比（该方法对此代码库完全不可行）。本质上，它证明了自身的可扩展性：只需验证约**1%的代码**（Core约749行代码，1825行规范/注解）即可获得对整个代码库的安全保证。
- **评估方法**：测量各工具的执行时间（10次运行的10%缩尾均值）与人工验证成本（人月）。同时通过故意注入漏洞（如记录密钥、发送明文DH密钥）验证了方法有效检测安全违规。

## 4. 资源与算力
- 所有实验在一台**2023款Apple MacBook Pro (M3 Pro处理器，macOS 15.6)**上完成，不涉及GPU。
- 工具执行时间（对SSM Agent代码库）：
  - **Tamarin** 协议模型验证：3.30分钟。
  - **Gobra** Core精化证明：1.17分钟。
  - **Argot** I/O独立性污点分析：0.48分钟。
  - **Argot** Application静态分析（解除Core假设）：2.12分钟。
- 人工验证总投入：**少于3人月**（建模<2人月，Core验证<3人月，I/O独立性分析<0.5人月，Core假设分析<1.5人月，部分重叠）。算力资源消耗极低，重点在人力投入的缩减。

## 5. 实验数量与充分性
- **实验组数**：共进行两个独立案例研究。
  - 第一个简单案例（签名DH）用于演示方法的通用性。
  - 第二个大规案例（SSM Agent）是核心评价对象，在其中进行了全面的协议建模、Core验证、I/O独立性分析以及四项静态条件检查（对应条件C1-C8）。
- **充分性评估**：
  - 实验覆盖了生产级代码库的典型复杂性：网络I/O、并发（两个线程操作共享状态）、回调、加解密操作。
  - 通过注入多种漏洞（如秘密日志、MitM攻击、数据竞争）验证了方法的检测能力。
  - 但仅测试了两个Go代码库，且第二个受限于工具精度，部分静态分析使用了人工豁免（如绕过某些分支污点、忽略Core实例偶然逃逸）。虽然论文认为这些修改是轻微的，但可能限制了自动化程度在不同项目中的普适性。缺乏与其他安全验证方法的直接定量比较（如验证时间、注解量），但鉴于该类方法的工作量，对比存在难度。

## 6. 主要结论与发现
- **Diodon能够将强安全属性的验证扩展到大规模生产代码库**。通过将手动证明限制在协议核心（约1%代码），并用轻量级自动分析保障其余部分不破坏安全，在保证可靠性的前提下大幅降低了验证成本。
- 证明了I/O独立性概念的有效性：即非协议I/O不影响安全，因此可在模型与实现验证中忽略，简化了协议模型和证明。
- 在实际SSM Agent代码库的应用中，不仅获得了保密性及单射一致性保障，还**发现并修复了先前未发现的漏洞**：一个协议设计层面的中间人攻击（MitM）和一个实现层面的潜在数据竞争。
- 方法支持并发、回调、多协议会话实例，其形式化证明为组合不同精度验证系统提供了蓝图。

## 7. 优点
- **显著的可扩展性**：首次在10万+行生产代码上完成完整的安全协议实现验证，将人工验证成本压缩至代码总量的1%。
- **方法论创新**：提出了“I/O独立性”概念来桥接全自动分析与交互式证明，减少冗余证明义务，使协议模型更紧凑。
- **证明的可靠性**：对I/O独立性与两阶段验证的组合给出了正式可靠性证明，为方法打下了坚实的理论基础。
- **实用的组合技术**：利用静态指针、逃逸、穿透分析自动解除分离逻辑证明中的前置条件，无需对Application进行额外标注，降低侵入性。
- **发现实际漏洞**：在评价过程中成功定位了协议设计与实现中的真实安全缺陷，展示了方法的应用价值。
- **全部开源**：案例、工具与分析均公开可用，增强了可复现性。

## 8. 不足与局限
- **前提假设与手工干预**：
  - 要求代码库存在清晰的Core/Application模块边界，且Core API规范需满足特定句法限制（如指针参数不允许深层可达、前置条件仅含权限要求）。
  - 对于回调等交互，仍需额外的验证义务（如传递权限），并非完全自动化。
  - 部分静态分析存在假阳性，在案例中需要人工审查并豁免（如特定分支的污点忽略、对象逃逸的误报），降低了全自动化程度。
- **Application数据竞争与未定义行为假设**：方法假设Application部分无数据竞争且无未定义行为（如空指针解引用），仅为Core部分证明安全性。这些假设削弱了整体保证，需额外工具弥补。
- **工具覆盖率与精确度限制**：
  - 未处理Go的`unsafe`包、`cgo`、反射等难以分析的特性，假设它们不被使用。
  - 在SSM Agent案例中，静态分析未能完全验证条件C5（回调图中调用Core API的限制），留待未来工作。
  - 穿透分析原型存在调用上下文不敏感导致的假阳性。
- **实验覆盖**：仅评价两个案例，且其中只有一个大规模代码库。方法的通用性（如对其他语言、更复杂结构）未经验证。也未充分评估静态分析在不同代码风格下的逃逸分析精度。
- **威胁模型限制**：沿用符号化Dolev-Yao模型，不考虑侧信道、时序等实现层攻击；依赖密码原语的完美安全性假设；需要所有参与方均经验证。

（完）

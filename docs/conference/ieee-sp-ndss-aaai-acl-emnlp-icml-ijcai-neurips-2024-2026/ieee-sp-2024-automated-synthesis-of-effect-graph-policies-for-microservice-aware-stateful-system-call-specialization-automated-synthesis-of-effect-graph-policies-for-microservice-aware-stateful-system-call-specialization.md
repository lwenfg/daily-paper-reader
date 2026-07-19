---
title: Automated Synthesis of Effect Graph Policies for Microservice-Aware Stateful System Call Specialization
title_zh: 面向微服务感知的有状态系统调用特化的效应图策略自动化合成
authors: "William Blair, Frederico Araujo, Teryl Taylor, Jiyong Jang"
date: 2024-05-01
pdf: "https://www.computer.org/csdl/pds/api/csdl/proceedings/download-article/1RjEaBpaMSc/pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 通过符号微执行自动化合成容器化程序的安全策略
tldr: 本文提出一种混合程序分析框架，自动合成容器化程序的有状态系统调用策略。给定容器镜像，框架通过符号微执行入口点并结合元数据约束，生成编码安全自动机的参考策略。在DARPA CGC语料和NGINX等实际程序中验证了其实用性，能有效防止微服务应用中的未授权行为，为代码安全验证提供了自动化工具。
source: IEEE-SP-2024-CSDL
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 899, \"height\": 189, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 857, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 793, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 752, \"height\": 917, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 873, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 883, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 889, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1724, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 817, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 772, \"height\": 969, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 901, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 903, \"height\": 959, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 899, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1838, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 899, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-automated-synthesis-of-effect-graph-policies-for-microservice-aware-stateful-system-call-specialization/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1840, \"height\": 411, \"label\": \"Table\"}]"
motivation: 容器化程序安全策略手工编写困难，需要自动化方法生成可防止未授权行为的参考策略。
method: 混合程序分析框架，通过符号微执行容器入口点生成安全自动机策略，并利用效应图表示。
result: 在25个DARPA CGC挑战和5个实际程序上成功合成策略，验证了框架的实用性。
conclusion: 该方法为容器及微服务提供了可自动化的系统调用安全策略合成，提升了代码安全验证效率。
---

## Abstract
We present a hybrid program analysis framework that automates the synthesis of stateful system call policies that describe admissible behaviors of containerized programs. Given a container image as input, the framework generates a reference policy that encodes a security automaton obtained by symbolically micro-executing the corresponding container's binary entrypoint under the constraints extracted from the container image metadata and environment.We demonstrate the utility and practicality of our approach by synthesizing security policies for 25 challenges in the DARPA Cyber Grand Challenge (CGC) corpus, 5 real-world containerized programs, including the widely used NGINX web server, and a complete microservice application from public benchmarks. We run each program or microservice using both benign and attack scenarios under the protection of a runtime policy monitor. Furthermore, we evaluate our approach by comparing our synthesized policies to those generated by four state-of-the-art system call specialization tools. Our results demonstrate that our techniques can scale to large programs and accurately extract concise reference application models for security monitoring.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
### 研究背景与动机
- 微服务架构广泛采用容器化部署，但安全管理复杂，缺乏自动生成精确、最小权限的系统调用访问策略的能力。
- 现有系统调用特化方法主要生成无状态允许列表，或仅依靠静态/动态分析，无法考虑系统调用的具体参数、时序状态以及容器环境（如配置文件、环境变量）的上下文，难以防御模仿攻击（如SSRF）。
- 容器镜像自身包含丰富的元数据（如文件系统分层、配置、依赖），但尚未被有效利用于自动化安全策略合成。

### 整体含义
本文提出 `μPolicyCraft`，一个混合程序分析框架，能够自动合成**有状态的、效应导向的系统调用安全策略**，精确刻画容器化程序在特定部署环境中的合法行为，从而在运行时检测并阻断违规操作，弥补现有方案在精确性与自动化方面的不足。

## 2. 论文提出的方法论
### 核心思想
- 利用容器镜像的不可变性和完整性，通过**符号微执行**容器入口点二进制程序，结合镜像元数据和输入约束，生成一个**效应图（Effect Graph）**。
- 效应图是一个有向图，节点代表程序状态（包含系统调用参数），边标记为系统调用类型，编码了程序与环境（进程、文件、网络）交互的合法时序序列与控制/数据流。
- 将效应图转换为安全自动机，由**微服务感知策略监视器（MPM）** 在运行时基于实体-关系流式遥测（SysFlow）进行状态推进与违规检测。

### 关键技术细节
- **中间表示与操作语义**：定义简化的IR和操作语义，明确系统调用效果 `ϵ = ⟨id, r⟩`，微执行过程中收集效果。
- **微执行框架**：基于BAP（Binary Analysis Platform）和Primus微执行引擎。扩展了Primus以支持高级文件I/O、网络I/O、字符串处理，并能通过Primus LISP/OCaml建模外部函数ABI，避免全状态执行。
- **概率地址空间**：对未映射内存访问返回随机值，防止微执行因复杂运行时状态（如Go语言数据结构）而卡死。
- **效应覆盖率**：测量效应图覆盖的效应项占二进制及其库中所有效应项的比例，用于指导测试用例构建，确保模型对当前配置的完备性。
- **策略监视器实现**：MPM将效应图实例化为有限自动机，消费流式遥测（将大量系统调用聚合成文件流FF、网络流NF等），仅当遇到进程事件时检查缓存的资源操作序列是否合规。

### 算法流程
1. 输入容器镜像，提取二进制入口点、配置、环境变量。
2. 通过基于覆盖率引导的微执行，使用预定义测试输入（网络请求/命令行）模拟合法交互，遍历控制流路径。
3. 在IR层面跟踪系统调用指令位置及其寄存器参数，构造效应图，重复节点不重复添加（保持图紧凑）。
4. 效应图导出为安全自动机。
5. 运行时MPM为每个容器加载对应的自动机，按遥测记录驱动状态转移，无法匹配时告警。

## 3. 实验设计
### 数据集与场景
- **DARPA CGC语料**：25个挑战程序，用于验证自动化漏洞检测能力。
- **微基准**：5个真实容器化应用——`nullhttpd`、`cron`、`vsftpd`、`NGINX`、Go语言文件共享服务。
- **宏基准**：DeathStarBench的酒店预订微服务应用，包含8个微服务（Go语言实现）。
- **攻击场景**：SSRF攻击（NGINX）、权限提升（Rust微服务）、非法EXEC调用（文件共享服务）、跨服务越权访问（酒店预订应用）。

### 对比方法
- 与4个最新的系统调用特化工具对比：`CONFINE`、`sysfilter`、`Chestnut`、`Temporal Specialization`。
- 比较维度：策略是否允许/禁止列表、是否考虑时序、是否包含具体参数、是否利用容器环境。

### 评估指标
- 策略合成时间（提升、微执行时间）、策略大小（状态数）、效应覆盖率、运行时性能开销（响应时间、CPU/内存）、策略违规检测有效性。

## 4. 资源与算力
- **硬件配置**：Ubuntu 22.04 LTS服务器，32核 Intel Xeon Gold 6130 2.10GHz CPU，126GB RAM。
- 无GPU需求，所有分析为CPU计算。
- **典型微执行时间**：从几秒到约40分钟（NGINX 39.85 min），Go微服务在5分钟内完成。
- **运行时监控开销**：对NGINX压力测试（100万请求/10并发），MPM增加响应时间2.96%，内存占用<40MB，CPU占用<2核。

## 5. 实验数量与充分性
### 实验规模
- 总计>30个程序/镜像的合成和监控测试。
- 至少三类程序语言：C/C++、Go、Rust。
- 包含简单CGC挑战、中量级守护进程、大型生产级Web服务器及完整微服务集群。

### 实验充分性与客观性
- **多维度评估**：合成效率、模型精确性、运行时性能、攻击检测能力、与现有工具对比。
- **对比公平**：对相同NGINX镜像，使用各自工具生成策略，并测量相同的性能开销。
- **环境真实**：使用云原生基准（DeathStarBench）和真实网络服务，通过时间序列交叉验证评估假阳性，展示了模型在实际请求下的完备性。
- **消融/补充实验**：量化了容器环境变量对符号变量具体化的增益（表4）。但未进行大规模消融实验（如移除效应覆盖率引导、对比随机ABI等），受限于单一分析框架特性。
- 实验设计总体充分，覆盖了核心声明，但仍需更多语言生态（Python/Java）验证。

## 6. 论文的主要结论与发现
- `μPolicyCraft` 能够完全自动化地为二进制容器程序生成**有状态、参数化、环境具体化**的系统调用安全策略，且效率可接受。
- 生成的效应图策略比纯静态工具更精确，能检测无状态允许列表或简单时序分段无法发现的攻击（如针对特定连接目标的SSRF）。
- 运行时监控开销低，可在线部署。
- 效应覆盖率指标为分析师提供了模型完备性的量化依据，支持增量完善。

## 7. 优点
- **概念创新**：首次将**符号微执行**与**容器镜像静态约束**结合，生成效应图这种兼顾状态顺序和具体参数的精简策略模型。
- **实用性高**：不需要源代码，适用于生产级二进制程序（C/C++/Go/Rust），已开源。
- **精确性与安全性**：能够约束到具体文件路径、网络主机端口、时序顺序，有效防御模仿攻击。
- **可扩展性**：框架支持通过LISP/OCaml快速扩展ABI模型，且对Go语言异步特性（defer）有专门处理。
- **监控效率**：基于聚合流式遥测，大幅减少需处理的事件数（~10倍），性能开销极低。

## 8. 不足与局限
- **人工介入需求**：虽然策略合成自动，但需要分析师根据效应覆盖率编写测试输入来触发目标行为，完全自动端到端仍有距离。
- **语言支持限制**：对解释型语言（如Python）需要先微执行解释器，工作量巨大；文中未评估解释型应用。
- **ABI建模负担**：外部函数建模需领域知识，尽管可复用，开始新语言运行时（如Go）需显著努力。
- **模仿攻击残余风险**：效应图只限制合法交互的集合，如果攻击完全在允许的交互序列内（如利用合法连接泄露数据），则无法防御，需辅助机制。
- **程序分析的固有局限**：二进制提升可能因间接跳转、自修改代码而失败（文中提到新BAP版本已部分解决），且符号执行路径爆炸可能需路径限制。
- **评估局限**：缺乏对解释型微服务的覆盖；未与更广泛的攻击测试集（如Kubernetes特定CVE）比较；仅与4种工具对比，未包括如Abhaya（无公开源码）。
- **配置敏感性**：策略高度定制于容器镜像，配置变更需重新合成，但可与CI/CD集成。

（完）

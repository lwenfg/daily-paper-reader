---
title: "SyzTrust: State-aware Fuzzing on Trusted OS Designed for IoT Devices"
title_zh: "SyzTrust: 面向物联网设备Trusted OS的状态感知模糊测试"
authors: "Qinying Wang, Boyu Chang, Shouling Ji, Yuan Tian, Xuhong Zhang, Binbin Zhao, Gaoning Pan, Chenyang Lyu, Mathias Payer, Wenhai Wang, Raheem Beyah"
date: 2024-05-01
pdf: "https://www.computer.org/csdl/pds/api/csdl/proceedings/download-article/1RjEaG9OpTa/pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 面向物联网设备Trusted OS的状态感知模糊测试进行漏洞发现
tldr: 针对IoT设备中Trusted OS安全分析缺乏的挑战，提出SyzTrust状态感知模糊测试框架，解决闭源和状态化工作流难题。通过学习数据结构和状态转换，自动化生成测试用例，在多个Trusted OS上发现漏洞，证明其有效性，为物联网安全测试提供了自动化验证方法。
source: IEEE-SP-2024-CSDL
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 740, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1567, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 735, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 655, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 751, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1819, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 741, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 782, \"height\": 329, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 724, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 811, \"height\": 418, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 717, \"height\": 197, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 896, \"height\": 199, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 891, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/ieee-sp-2024-csdl/ieee-sp-2024-syztrust-state-aware-fuzzing-on-trusted-os-designed-for-iot-devices/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1828, \"height\": 2397, \"label\": \"Table\"}]"
motivation: 物联网TEE中的Trusted OS安全分析不足，闭源和状态复杂性导致现有测试困难。
method: 实现状态感知模糊测试，学习数据结构和工作流，自动生成并发送测试用例以发现漏洞。
result: 在多个IoT Trusted OS上发现了多种安全漏洞，验证了框架的有效性。
conclusion: SyzTrust为资源受限的物联网设备提供了有效的安全分析工具，增强了TEE的可靠性。
---

## Abstract
Trusted Execution Environments (TEEs) embedded in IoT devices provide a deployable solution to secure IoT applications at the hardware level. By design, in TEEs, the Trusted Operating System (Trusted OS) is the primary component. It enables the TEE to use security-based design techniques, such as data encryption and identity authentication. Once a Trusted OS has been exploited, the TEE can no longer ensure security. However, Trusted OSes for IoT devices have received little security analysis, which is challenging from several perspectives: (1) Trusted OSes are closed-source and have an unfavorable environment for sending test cases and collecting feedback. (2) Trusted OSes have complex data structures and require a stateful workflow, which limits existing vulnerability detection tools.To address the challenges, we present SyzTrust, the first state-aware fuzzing framework for vetting the security of resource-limited Trusted OSes. SyzTrust adopts a hardware-assisted framework to enable fuzzing Trusted OSes directly on IoT devices as well as tracking state and code coverage non-invasively. SyzTrust utilizes composite feedback to guide the fuzzer to effectively explore more states as well as to increase the code coverage. We evaluate SyzTrust on Trusted OSes from three major vendors: Samsung, Tsinglink Cloud, and Ali Cloud. These systems run on Cortex M23/33 MCUs, which provide the necessary abstraction for embedded TEEs. We discovered 70 previously unknown vulnerabilities in their Trusted OSes, receiving 10 new CVEs so far. Furthermore, compared to the baseline, SyzTrust has demonstrated significant improvements, including 66% higher code coverage, 651% higher state coverage, and 31% improved vulnerability-finding capability. We report all discovered new vulnerabilities to vendors and open source SyzTrust.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：物联网设备日益依赖基于硬件隔离的可信执行环境（TEE）保护敏感数据与操作。TEE 的核心组件——可信操作系统（Trusted OS）一旦存在漏洞，将导致机密性与完整性保护彻底失效。
- **核心问题**：当前针对 IoT 设备 Trusted OS 的安全分析严重不足，主要面临两大挑战：
  - **闭源与受限环境**：大多闭源且厂商加密，无法进行代码插桩；IoT 设备资源极度受限，传统的二进制插桩或固件模拟方案难以落地。
  - **复杂数据结构与状态化工作流**：Trusted OS 需维护复杂状态机以支持多种密码算法，缺乏状态感知的模糊测试无法触及深层状态中的漏洞。
- **整体含义**：提出并实现了 **SyzTrust**，首个面向资源受限 IoT 设备 Trusted OS 的状态感知模糊测试框架，通过硬件辅助方式解决了上述挑战，并在真实设备上验证了有效性。

### 2. 方法论
- **核心思想**：采用“PC 端模糊引擎 + 设备端执行引擎”的解耦架构，利用硬件调试探针（Debug Probe）非侵入式地收集代码与状态覆盖，并引入复合反馈（代码覆盖 + 状态覆盖）引导模糊测试深度探索状态空间。
- **关键技术细节**：
  - **硬件辅助模糊测试框架**：
    - 在 PC 端运行资源密集型的模糊引擎（种子生成、变异、调度等），仅将轻量的执行引擎（作为 CA/TA 代理）部署在 MCU 上。
    - 通过调试探针（SEGGER J‑Trace Pro）将序列化的测试用例写入 MCU 特定内存，TA 反序列化后调用 Trusted OS 的 syscall。
  - **选择性指令跟踪**：
    - 利用 ARM ETM（嵌入式跟踪宏单元）实时记录指令流，触发条件由 DWT 数据观察点事件控制（仅跟踪成功世界代码），过滤正常世界噪声。
    - 在 PC 端直接用原始 ETM 包计算 LCSAJ 基本块转移序列作为分支覆盖，避免开销巨大的指令解码。
  - **状态变量推断与监视**：
    - 基于观察：Trusted OS 的操作句柄（`TEE_OperationHandle`、`TEE_ObjectHandle`）包含控制执行上下文的成员变量。
    - 主动式推断：通过长时间基础模糊测试收集句柄缓冲区快照，过滤随机变化（如指针、密钥）和稳定字段，锁定随特定 syscall 序列及参数变化的字节序列作为状态变量。
    - 在模糊循环中，通过调试探针后台高速读取状态变量值，计算值组合的哈希作为状态覆盖。
  - **复合反馈与种子调度**：
    - 种子保存：构建 `HitMap`（状态哈希→命中次数）和 `SeedMap`（状态哈希→触发该状态的种子桶），触发新状态或新代码均被保存。
    - 种子选择（见算法 1）：先以加权随机方式选择罕见状态（权重与命中次数成反比），再从该状态的种子桶中以分支覆盖为权重选择具体种子。
    - 取消 Syzkaller 的 triage 调度任务，因为 MCU 快速重置可天然避免假阳性，且 Trusted OS 的测试用例过长，最小化成本极高。
- **算法流程**（文字说明）：种子选择过程分为两步，第一步根据状态命中次数的倒数计算选择概率选取某个状态，第二步在该状态对应的种子集合中根据分支覆盖大小概率选取一个种子，实现“多探索罕见状态，同时偏爱高覆盖种子”的目标。

### 3. 实验设计
- **测试目标与场景**：
  - 三个主流 IoT 厂商的 Trusted OS：**Samsung mTower**（符合 GP 标准）、**Tsinglink Cloud TinyTEE**（符合 GP 标准）、**Ali Cloud Link TEE Air**（闭源私有），均运行在支持 TrustZone‑M 的 Cortex‑M23/33 开发板（主要使用 Nuvoton M2351）。
- **Baseline 与对比方法**：
  - 主要基线：**Syzkaller**（业界广泛使用的覆盖率引导内核模糊器）。
  - 消融对比：
    - **SyzTrust-Basic**：仅引入新调度任务与扩展 syscall 模板，无状态反馈。
    - **SyzTrust-State**：将两个句柄的完整缓冲区值当作状态，使用复合反馈。
    - **SyzTrust-FState**：使用推断出的有意义状态变量进行复合反馈（完整 SyzTrust）。
- **评估指标**：
  - 代码覆盖率（LCSAJ 基本块数）。
  - 状态覆盖率（状态变量值组合数量）。
  - 唯一漏洞数（通过 HardFault 捕获，按栈顶三个函数去重后人工分析）。

### 4. 资源与算力
- 实验主要使用 **PC**：Intel i7‑8700 CPU（3.20 GHz）、32 GB RAM、Windows 10。**未使用 GPU**。
- 模糊测试期间，PC 侧主要承担种子生成、覆盖计算等任务。单次测试用例（平均 14.4 个 syscall）的总周转时间约 **6,290 ms**，其中 MCU 端执行占用绝大部分时间，ETM 流传输与覆盖计算仅占约 1%。

### 5. 实验数量与充分性
- **对比实验**：在 mTower 上对 Syzkaller、SyzTrust-Basic、SyzTrust-State、SyzTrust-FState 进行了 **48 小时模糊测试，各重复 10 次**，统计覆盖面与漏洞发现趋势（图 7、表 1）。
- **真实世界评估**：在三个真实 Trusted OS 上分别运行 SyzTrust-FState **90 小时**（表 3）。
- **状态推断准确性**：对四个 Trusted OS 的 8 个句柄结构进行推断，手动/专家逆向后统计精确率（表 2）。
- **分析全面**：包含开销分解（图 6）、状态转换树可视化（图 8）、漏洞分类与案例研究（表 6）。实验设计充分，采用多次重复消除随机性，并分析了覆盖指标与漏洞发现的相关性。

### 6. 主要结论与发现
- SyzTrust 成功克服了 IoT Trusted OS 的闭源与资源限制，实现了首个硬件辅助的状态感知模糊测试。
- 在 mTower 上，SyzTrust-FState 较 Syzkaller 基线**分支覆盖提升 66%**，**状态覆盖提升 651%**，**漏洞发现能力提升 31%**，并触发了基线无法发现的深层状态漏洞（表 1）。
- 在三个真实 Trusted OS 上**共发现 70 个未知漏洞**，其中 28 个已获厂商确认，**已分配 10 个 CVE**（包括缓冲区溢出、空指针解引用、未受控内存分配等严重问题）。
- 状态变量推断方法平均精确率 **83.3%**；构建的状态转换树与 GP TEE 规范中的操作状态（如 key_set、initialized）高度一致，证明了状态定义的准确性与表达力。

### 7. 优点
- **系统架构创新**：PC‑MCU 解耦 + 调试探针负责通信与跟踪，突破 IoT 设备的资源约束。
- **非侵入式覆盖收集**：利用 ETM 硬件跟踪实现零插桩的指令流记录，并设计了事件/地址双重过滤和原始包直接计算 LCSAJ 覆盖的轻量化方法。
- **自动化状态识别**：无需源码，通过主动测试和统计分析自动推断出有意义的状态变量，有效处理闭源 Trusted OS。
- **复合反馈机制**：将状态覆盖与代码覆盖有机融合，通过状态优先的种子调度策略显著提升深层漏洞的探索效率。
- **实际影响与可复现性**：发现 70 个真实漏洞并获取多个 CVE，且已将 SyzTrust 开源。

### 8. 不足与局限
- **假设依赖**：要求目标设备能够安装定制的 TA，且启用 ETM 硬件追踪；对于供应链极其封闭或安全熔丝彻底禁用调试接口的设备无法直接应用。
- **覆盖面有限**：当前主要针对符合 GP TEE Internal Core API 标准的密码操作部分，非标准或与外围设备交互的部分尚未覆盖。
- **适配工作量**：扩展到新的私有 Trusted OS 需要手动提取状态相关结构、调整 syscall 模板和 TA 适配代码，仍需一定领域知识。
- **性能瓶颈**：单轮测试耗时约 6 秒，吞吐量较低；ETM 带宽理论上可成为大规模并行化时的瓶颈（当前实验仅单设备，未暴露该问题）。
- **漏洞检测与去重**：依赖 HardFault 异常捕获崩溃，可能遗漏逻辑错误或非崩溃型漏洞；漏洞去重仅基于栈顶三个函数，可能存在少量欠去重或过去重风险。

（完）

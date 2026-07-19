---
title: "TZ-DATASHIELD: Automated Data Protection for Embedded Systems via Data-Flow-Based Compartmentalization"
title_zh: "TZ-DATASHIELD: 通过基于数据流的隔离实现嵌入式系统自动化数据保护"
authors: "Zelun Kong, Minkyung Park, Le Guan, Ning Zhang, Chung Hwan Kim"
date: 2025-01-01
pdf: "https://www.ndss-symposium.org/wp-content/uploads/2025-563-paper.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 通过编译器实现嵌入式系统敏感数据流隔离的自动化数据保护
tldr: 针对嵌入式系统在医疗、工业等关键领域的数据安全挑战，提出TZ-DATASHIELD，一种LLVM编译器工具，通过敏感数据流隔离自动增强ARM TrustZone。该工具解决了MCU计算和能耗限制下的数据保密性和完整性问题，在无人车辆等场景中验证了有效性，为嵌入式安全开发提供了自动化方案。
source: NDSS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 916, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1796, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 745, \"height\": 661, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 745, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 913, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1885, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1882, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 925, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1883, \"height\": 445, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 931, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1884, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 762, \"height\": 1343, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 896, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1882, \"height\": 530, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 926, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 769, \"height\": 274, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 880, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1884, \"height\": 495, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 902, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 926, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2025-accepted/ndss-2025-tz-datashield-automated-data-protection-for-embedded-systems-via-data-flow-based-compartmentalization/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 903, \"height\": 122, \"label\": \"Table\"}]"
motivation: 嵌入式系统在关键领域广泛使用，但受限于计算和能耗，保护敏感数据机密性完整性面临挑战。
method: 基于LLVM编译器，通过对敏感数据流进行分析和隔离，自动增强ARM TrustZone的安全隔离能力。
result: 在多种嵌入式平台上验证了工具的有效性，显著提升了数据保护能力。
conclusion: TZ-DATASHIELD为资源受限的嵌入式系统提供了一种自动化数据保护方案，可广泛应用。
---

## Abstract
As reliance on embedded systems grows in critical domains such as healthcare, industrial automation, and unmanned vehicles, securing the data on micro-controller units (MCUs) becomes increasingly crucial. These systems face significant challenges related to computational power and energy constraints, complicating efforts to maintain the confidentiality and integrity of sensitive data. Previous methods have utilized compartmentalization techniques to protect this sensitive data, yet they remain vulnerable to breaches by strong adversaries exploiting privileged software. In this paper, we introduce TZ-DATASHIELD, a novel LLVM compiler tool that enhances ARM TrustZone with sensitive data flow (SDF) compartmentalization, offering robust protection against strong adversaries in MCU-based systems. We address three primary challenges: the limitations of existing compartment units, inadequate isolation within the Trusted Execution Environment (TEE), and the exposure of shared data to potential attacks. TZ-DATASHIELD addresses these challenges by implementing a fine-grained compartmentalization approach that focuses on sensitive data flow, ensuring data confidentiality and integrity, and developing a novel intra-TEE isolation mechanism that validates compartment access to TEE resources at runtime. Our prototype enables firmware developers to annotate source code to generate TrustZone-ready firmware images automatically. Our evaluation using real-world MCU applications demonstrates that TZ-DATASHIELD achieves up to 80.8% compartment memory and 88.6% ROP gadget reductions within the TEE address space. It incurs an average runtime overhead of 14.7% with CFI and DFI enforcement, and 7.6% without these measures. As reliance on embedded systems grows in critical domains such as healthcare, industrial automation, and unmanned vehicles, securing the data on micro-controller units (MCUs) becomes increasingly crucial. These systems face significant challenges related to computational power and energy constraints, complicating efforts to maintain the confidentiality and integrity of sensitive data. Previous methods have utilized compartmentalization techniques to protect this sensitive data, yet they remain vulnerable to breaches by strong adversaries exploiting privileged software. In this paper, we introduce TZ-DATASHIELD, a novel LLVM compiler tool that enhances ARM TrustZone with sensitive data flow (SDF) compartmentalization, offering robust protection against strong adversaries in MCU-based systems. We address three primary challenges: the limitations of existing compartment units, inadequate isolation within the Trusted Execution Environment (TEE), and the exposure of shared data to potential attacks. TZ-DATASHIELD addresses these challenges by implementing a fine-grained compartmentalization approach that focuses on sensitive data flow, ensuring data confidentiality and integrity, and developing a novel intra-TEE isolation mechanism that validates compartment access to TEE resources at runtime. Our prototype enables firmware developers to annotate source code to generate TrustZone-ready firmware images automatically. Our evaluation using real-world MCU applications demonstrates that TZ-DATASHIELD achieves up to 80.8% compartment memory and 88.6% ROP gadget reductions within the TEE address space. It incurs an average runtime overhead of 14.7% with CFI and DFI enforcement, and 7.6% without these measures.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

嵌入式系统（如医疗设备、工业自动化、无人车辆等）广泛使用微控制器单元（MCU），因其成本低、体积小、能效高。但MCU资源受限，常采用共享地址空间运行固件，导致敏感数据（如PIN码、GPS坐标等）的保密性与完整性面临严峻威胁。现有基于隔离区（compartmentalization）的保护方案（按线程、组件、函数粒度划分）存在以下不足：

- 隔离区粒度过粗，攻击面依然较大；粒度过细则带来高昂的上下文切换开销。
- 依赖特权软件（如RTOS内核）作为可信基，一旦内核被攻破（例如通过CVE利用），整个保护机制失效。
- ARM TrustZone虽可将敏感资源隔离到安全世界，但安全世界内部缺乏隔离，且共享数据和外设数据易成为攻击跳板。

因此，本论文旨在设计一种**自动化的、基于敏感数据流的隔离编译器工具**，充分利用TrustZone硬件特性，在不显著增加开销的前提下，保护MCU系统中敏感数据的机密性和完整性。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

核心思想是**敏感数据流（SDF）隔离**，即沿着数据依赖关系，将只与特定敏感数据相关的代码、数据以及外设访问归入一个最小隔离区。具体方法包含以下部分：

#### (a) 固件注解与自动隔离区生成
- 开发者通过预处理器宏（如 `TZDS_DATA_R`, `TZDS_MMIO_W`）标注需要保护的数据变量或外设地址。
- TZ-DATASHIELD 基于 LLVM IR 构建**值流图（VFG）**，对每个标注的敏感数据执行**程序切片**：
  - 若需保密性（只读），执行**前向切片**，找到所有受该数据影响的计算指令。
  - 若需完整性（只写），执行**后向切片**，找到所有可能影响该数据的指令。
- 将同一个敏感数据流相关的函数归并为一个隔离区（compartment），共享代码和数据则单独放置并通过额外机制保护。

#### (b) 结合 TrustZone 的强隔离
- 安全世界承载安全监控器（security monitor）和所有 SDF 隔离区，普通世界运行剩余固件。
- 安全属性单元（SAU）动态配置内存区域，确保普通世界无法访问安全世界资源。

#### (c) 安全世界内隔离（intra-TEE isolation）
- 不依赖内存保护单元（MPU，因为区域数量、大小和对其受限），而采用**软件故障隔离（SFI）**：
  - 编译时对所有间接控制流传输（如间接调用）和间接内存访问（如 load/store）进行插桩。
  - 运行时检查目标地址是否位于本隔离区的合法范围（代码段、私有数据段、允许的外设和共享数据）。

#### (d) 共享数据和外设的轻量级完整性保护
- 对于跨隔离区的共享数据或外设访问，在 SFI 基础上启用**控制流完整性（CFI）和 数据流完整性（DFI）**：
  - CFI：维护影子栈（shadow stack）验证返回地址；对间接调用目标进行白名单检查。
  - DFI：为每次写操作分配唯一 `store_id`，记录在运行时定义表（RDT）中；读操作时验证最近的 `store_id` 是否来自合法的写指令。
  - 验证的深度（回溯步数 N）可配置。

#### (e) 安全监控器
管理安全启动、SAU 配置、隔离区动态加载与卸载、堆内存分配跟踪，并通过安全中断派发确保中断在隔离区内安全执行。

### 3. 实验设计：使用了哪些数据集/场景，它的 benchmark 是什么，对比了哪些方法

**实验平台**：NXP LPCXpresso55S69 开发板（ARM Cortex-M33，TrustZone-M 支持，150MHz，640KB 闪存，320KB RAM）。

**评估场景**：12 个真实 MCU 应用，其中6个裸机程序、6个基于 FreeRTOS 的程序，涵盖智能门锁、温度传感器、加速度计、陀螺仪、SD卡文件系统、USB虚拟串口等。

**对比方法**：将 SDF 隔离与如下三种隔离粒度进行全方位比较：
- **函数级隔离**（模拟 ACES[12]）：每个函数一个隔离区。
- **组件级隔离**（模拟 EC[10] 或 CRT-C[11]）：按软件组件（如驱动、库）划分。
- **线程级隔离**（模拟 Minion[9]）：按 RTOS 线程划分。

**测量指标**：
- 安全指标：隔离区可访问的安全世界地址空间大小（代码、私有数据、共享数据、外设）、ROP gadget 数量。
- 性能指标：总运行时间开销，并分解为 SFI 检查、CFI/DFI 检查、隔离区切换/加载/卸载的开销。
- 内存开销：安全监控器、隔离区、普通世界固件的代码与数据大小。
- 附加指标：开发者注解工作量、静态分析精度、隔离区切换次数等。

### 4. 资源与算力

**本文不涉及 GPU 或大规模训练。** 工具链运行在普通 x86-64 桌面计算机（Ubuntu 22.04），主要算力用于编译器的静态分析和固件编译，实验中未明确说明 CPU 型号、内存或编译时长。运行时性能测量直接在目标 MCU 上进行。

### 5. 实验数量与充分性

**实验设计比较充分且客观**：
- 在 **12 个不同应用** 上评估，涵盖裸机和 RTOS，覆盖多种外设和通信协议。
- 与 **3 种主流隔离粒度** 进行对比，所有方法均在同一硬件平台复现。
- 从 **安全性、运行性能、内存、开发者负担** 等多个维度量化。
- 进行了 **微观基准测试**（单次 SFI、CFI/DFI 检查耗时）和 **可配置参数 N 的敏感性分析**（CFI/DFI 检查深度变化的影响）。
- 通过 **案例研究**（Accel、SD-FatFS、USBVCom）演示防御效果。
- 对安全监控器的 SFI/CFI/DFI 逻辑进行了 **形式化验证**（CBMC）。
- 实验数据详实，表格和图表清晰，归因分析（性能分解）合理。

### 6. 论文的主要结论与发现

- **攻击面大幅缩减**：相比无隔离，SDF 隔离平均减少安全世界地址空间 **80.8%**，ROP gadget 数量 **88.6%**；与函数级隔离相比，虽然代码和外设暴露稍多，但共享数据暴露显著降低。
- **性能开销可控**：在启用 CFI/DFI 时平均运行时开销 **14.7%**，仅启用 SFI 时 **7.6%**。相比函数级隔离（因频繁切换）提速 **36.7%**。
- **内存开销低**：安全监控器占约 14KB 闪存、5KB RAM；总内存（闪存+RAM）增量约 45KB/7KB，与粗粒度隔离相近。
- **防御多种攻击**：有效防御 shellcode 注入、代码复用、纯数据攻击、中断处理攻击等。
- **开发者工作量小**：只需对少量数据变量和已知外设地址进行宏标注，其余由工具自动完成。

### 7. 优点：方法或实验设计上有哪些亮点

- **系统性解决三大挑战**：同时克服隔离粒度不合理、TEE 内部缺乏隔离、共享/外设数据保护难题。
- **数据流驱动的隔离粒度**：以敏感变量为锚点进行程序切片，要比线程或组件划分更精细，又比函数划分更高效，达到安全与性能的平衡。
- **编译时全自动**：开发者仅需简单注解，编译器自动完成分析、隔离、插桩，并生成 TrustZone 就绪的镜像，实用性强。
- **不依赖受限硬件隔离特性**：避开了 MCU 上 MPU 区域少、对齐限制等硬件瓶颈，采用 SFI 软件方案。
- **轻量级 CFI/DFI 选择性启用**：仅针对共享和外设数据访问进行控制/数据流完整性检查，大幅度降低全时 CFI/DFI 的开销。
- **实验非常扎实**：多应用、多粒度对比、微基准、敏感性分析、形式化验证、案例研究，说服力强。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **静态分析的固有局限**：基于安德森指向分析的切片可能**过度近似**（导致较大隔离区）或**欠近似**（遗漏真实数据流），论文虽给出了近似率，但未讨论对安全风险的实际影响。
- **不防御某些高级攻击**：如模仿攻击（控制流弯曲）可能绕过 CFI/DFI 检查；DMA 攻击需要额外防护机制（论文将其列为未来工作）。
- **普通世界到安全世界的接口风险**：攻击者可能通过 Non-Secure Callable 区域传入恶意输入，利用隔离区漏洞劫持控制流，影响限于本隔离区但可能破坏部分安全属性。
- **实验应用规模偏小**：评估应用虽真实但较为简单，未展示超大型固件（如复杂的网络协议栈）上的效果。
- **CFI/DFI 的安全假设**：假设信息流机制能有效区分合法与恶意访问，但这在某些复杂控制流下可能失效。
- **没有讨论与安全启动之外的 TrustZone 侧信道防御**：物理缓存侧信道等不在威胁模型内。

（完）

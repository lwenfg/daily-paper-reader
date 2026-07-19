---
title: "ADGFUZZ: Assignment Dependency-Guided Fuzzing for Robotic Vehicles"
title_zh: ADGFuzz：面向机器人车辆的赋值依赖引导模糊测试
authors: "Yuncheng Wang, Yaowen Zheng, Puzhuo Liu, Dongliang Fang, Jiaxing Cheng, Dingyi Shi, Limin Sun"
date: 2026-01-01
pdf: "https://www.ndss-symposium.org/wp-content/uploads/2026-s1014-paper.pdf"
tags: ["query:safe-coding"]
score: 9.0
evidence: 面向机器人车辆软件安全的模糊测试框架
tldr: 针对机器人车辆控制软件输入空间巨大导致传统模糊测试效率低的问题，提出赋值依赖引导的模糊测试框架，通过分析变量赋值关系引导测试，高效挖掘深层安全漏洞。
source: NDSS-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 664, \"height\": 320, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 906, \"height\": 318, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1881, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1662, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 908, \"height\": 272, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 907, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 336, \"height\": 248, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 894, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 922, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 914, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 908, \"height\": 257, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 804, \"height\": 1006, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 900, \"height\": 285, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 739, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 930, \"height\": 958, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 738, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 911, \"height\": 175, \"label\": \"Table\"}, {\"url\": \"assets/tables/ndss-2026-accepted/ndss-2026-adgfuzz-assignment-dependency-guided-fuzzing-for-robotic-vehicles/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1875, \"height\": 2372, \"label\": \"Table\"}]"
motivation: 机器人车辆软件输入组合空间极大，现有模糊测试难以有效探索并发现深层次安全缺陷。
method: 设计赋值依赖引导的模糊测试策略，分析控制软件中变量赋值关系，优先探索高价值输入区域。
result: 在真实机器人车辆软件上有效发现多种深层错误，优于现有模糊测试工具。
conclusion: ADGFuzz通过依赖引导显著提升了机器人车辆软件的模糊测试效率和漏洞检出能力。
---

## Abstract
Robotic vehicles (RVs) play an increasingly vital role in modern society, with widespread applications in both commercial and military contexts. RV control software is the core of RV systems, which maintains proper operation by continuously computing the vehicle's internal state, sensor readings, and external inputs to adjust the system's behavior accordingly. However, the vast combination space of configurable parameters, command inputs, and environment-sensed data in RV software introduces significant security risks to the system. Existing fuzzing techniques face substantial challenges in effectively exploring this vast input space while uncovering deep bugs. To address these challenges, we propose ADGFuzz, a novel fuzzing framework specifically designed to detect assignment statement bugs in RV control software. ADGFuzz statically constructs an Assignment Dependency Graph (ADG) to capture inter-variable dependencies within the program. These dependencies are then propagated to the RV input space by leveraging naming similarities, resulting in a targeted set of inputs referred to as the matched input set (MIS). Building upon this, ADGFuzz performs entropy-aware fuzzing over the MISs, thereby enhancing the overall efficiency of bug discovery. In our evaluation, ADGFuzz uncovered 87 unique bugs across three RV types, 78 of which were previously unknown. All found bugs were responsibly disclosed to the developers, and 16 have been confirmed for fixing.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机
- **核心问题**：机器人车辆（RV）控制软件中普遍存在**赋值语句缺陷**（assignment statement bugs），例如因物理公式转换不当、参数约束缺失或逻辑冲突导致的错误赋值。此类缺陷常引发严重事故（坠地、轨迹偏离、软件崩溃），但现有模糊测试方法因输入空间庞大且缺乏针对性，难以高效检测。
- **研究背景**：
  - RV 控制软件面临**配置参数、控制指令、环境感知数据**等多源输入，组合空间达数千维。
  - 已有方法（如 RVFuzzer、PGFuzz）要么盲目探索输入空间而无法确保覆盖缺陷代码，要么过度依赖文档规则而遗漏未文档化的实现错误。
  - 对 ArduPilot 十年间 819 个标记为“BUG”的问题分析显示，**28.02% 的语义/逻辑缺陷由错误的赋值语句直接导致**，其余多为缺失输入（且开发阶段已修复，难以复现）。
- **整体目标**：提出一种**赋值依赖引导的模糊测试框架（ADGFuzz）**，聚焦于影响赋值链的 RV 输入子集，通过语义关联和熵感知调度提升漏洞挖掘效率。

### 2. 方法论
#### 2.1 核心思想
利用 **程序内变量间的赋值依赖关系**与 **变量名和输入参数的命名相似性**，将模糊测试引导至与特定赋值语句相关联的输入子集，并通过**信息熵评估**优先测试更可能触发异常的组合。

#### 2.2 关键技术细节
- **赋值依赖图（ADG）构建**：
  - 从源代码中提取赋值语句，识别左值（依赖变量）与右值（独立变量/函数调用），构建有向无环图。
  - 节点类型：根节点（仅作为左值）、叶节点（仅作为右值）、半依赖节点（同时为左值和右值）。
  - 通过反向遍历和临时集合处理半依赖节点，形成完整的变量依赖链。

- **匹配输入集（MIS）推断**：
  - 从 ADG 叶节点提取变量名称，按术语切分（如以下划线分隔）。
  - 利用**同义词表**（含缩写、同义物理量）和**物理耦合表**（从注释中半自动识别的耦合物理量，如“角度↔加速度”）进行术语扩展与关联。
  - 将扩展后的变量术语与 RV 输入参数的术语集（来自官方文档）匹配，每个 ADG 生成一个 MIS（可能包含多个输入参数）。
  - 匹配规则基于命名约定，推断出可能联合影响根变量赋值的输入参数子集。

- **熵感知的 MIS 模糊测试**：
  - **熵指标**：对每个 MIS 计算信息熵，综合两个维度：
    1. **结构熵** $E_{num} = \log_2(|N_{semi}|+1)$，反映赋值链中半依赖节点数。
    2. **质量熵** $E_{qual} = \log_2\left(1 + \sum_{v \in V_{leaf}} \sum_{i=1}^{k} \frac{i}{T_i}\right)$，其中 $v$ 含 $k$ 个术语，$T_i$ 为第 $i$ 术语匹配的输入参数唯一数量，衡量叶变量术语的语义特异性。
  - 总熵 $E(MIS) = E_{num} + E_{qual}$，并按熵值概率 $p(MIS) \propto E(MIS)$ 采样 MIS。
  - **功率调度**：选中 MIS 后，其熵值减半，避免重复过度测试；若触发 bug，进一步降低熵值以允许有限再探索；未被选中的 MIS 熵值逐渐衰减，保证覆盖率。
  - **测试用例生成**：每轮根据 MSE 熵值决定执行次数（映射到 [50, 500]），随机选取 MIS 中若干输入，按文档范围、单位或几何级数分区赋值，注入 SITL 仿真环境。
  - **缺陷预言**：监控三类异常——坠地（姿态、日志）、轨迹偏离（到目标距离连续增大）、软件崩溃（心跳消息丢失）。

- **后处理**：
  - **输入最小化**：对触发异常的输入序列进行双向搜索和迭代剔除，找出最小触发集。
  - **去重**：基于相同缺陷类型和最小输入集进行去重，保留首次触发的测试用例。

#### 2.3 算法流程简述
1. 静态分析阶段：遍历函数，提取赋值语句，构建 ADG；推断 MIS。
2. 模糊测试阶段：初始化 MIS 熵概率分布，循环采样 MIS → 重置仿真 → 生成测试用例并执行 → 预言检测 → 调整熵值和概率 → 记录异常。
3. 后处理阶段：最小化触发输入，去重报告。

### 3. 实验设计
- **测试平台与场景**：
  - 选用三大类 ArduPilot 支持的 RV：**四旋翼（Copter）、固定翼（Plane）、地面无人车（Rover）**。
  - 仿真环境：**SITL**，地面站 MAVProxy，通信协议 MAVLink。
  - 模糊测试执行完整多阶段导航任务（含起飞、转向、航点）。
- **对比方法**：
  - **PGFuzz**：策略引导的模糊测试框架，基于文档提取的安全策略检测违反。
  - **RVFuzzer / LGDFuzzer**：因无法检测赋值类缺陷，未纳入直接对比，仅做定性分析。
  - **消融变体**：
    - `ADGFuzz_NOE`：随机选取 MIS 替代熵调度。
    - `ADGFuzz_RANDOM`：彻底禁用 MIS，随机选取 RV 全局输入。
    - `ADGFuzz_NUM`：仅用结构熵（$E_{num}$）。
    - `ADGFuzz_QUAL`：仅用质量熵（$E_{qual}$）。
- **评估指标**：发现的唯一缺陷数、缺陷类型分布、首次发现时间、ADG–MIS 构建准确率（人工验证）、跨平台可移植性（PX4）。

### 4. 资源与算力
- **硬件环境**：Ubuntu 20.04 虚拟机，配备 Intel Core i9‑11950H 处理器、**32 GB RAM**，Python 3.8.10。
- **未使用 GPU**：模糊测试为 CPU 密集型的仿真交互与逻辑分析，无需 GPU 加速。
- **测试时长**：每个实验配置**连续运行 24 小时**，用于评估缺陷发现趋势。

### 5. 实验数量与充分性
- **主要实验组数**：
  - 3 类 RV × 多个策略对比（完整 ADGFuzz / NOE / RANDOM / NUM / QUAL），共约 15 项主要运行。
  - ADG–MIS 构建**准确率人工验证**：随机采样 150 对 ADG–MIS，双人交叉验证，充分性良好。
  - 熵区间覆盖分析：按 MIS 熵值四分位分析代码覆盖率重叠情况。
  - 跨平台验证：将框架迁移至 PX4 平台，验证可移植性。
- **实验公平性**：所有方法在同一硬件、相同仿真环境和测试时长下运行；消融变体仅替换调度/选择模块，核心 MIS 构建保持一致，保证了单一变量控制。
- **充分性**：覆盖多种车辆类型、与最新基线对比、消融分析划分熵维度贡献、人工验证语义准确性，实验设计较全面。但**未包含针对不同代码规模或不同版本的纵向比较**，也未进行多次重复实验衡量稳定性。

### 6. 主要结论与发现
- ADGFuzz 在三种 RV 类型下**共发现 87 个唯一缺陷**（其中 78 个为未知），包括 26 个坠地、15 个轨迹偏离、46 个软件崩溃。
- **远超现有方法**：PGFuzz 仅能发现其中 8 个重叠缺陷，其余 79 个为 ADGFuzz 独有，因其不依赖文档规则，可从实现逻辑出发探测未文档化错误。
- **熵引导显著提升效率**：与随机调度相比，ADGFuzz 在首小时内发现缺陷的速率更高，且最终发现的缺陷总数更多（Copter +18，Plane +16，Rover +9）；结构熵与质量熵互补，联合使用效果最佳。
- **ADG–MIS 构建准确率 87.33%**（手工验证），且命名匹配覆盖了 99.98% 的 RV 输入参数，语义失效对覆盖率影响极小。
- **真实危害验证**：45 个缺陷可在真实硬件上复现，攻击案例展示攻击者可通过操纵参数组合引发隐蔽故障（如非预期坠毁、虚假到达航点）。

### 7. 优点
- **创新性方法**：首次将**赋值依赖图与命名语义关联**引入 RV 模糊测试，将无目标的输入探索转化为对特定代码区域的定向测试。
- **熵感知调度**：设计的信息熵指标同时考虑赋值链长度和术语特异性，在不依赖传统代码覆盖反馈的情况下，有效引导测试资源分配。
- **可移植性**：框架可适配其他开源飞控（如 PX4），仅需少量协议适配和术语表更新。
- **实时仿真集成**：在完整任务流程中注入输入，发现延迟暴露的缺陷（如航点误判），比简单状态注入更贴近真实攻击场景。
- **负责任披露**：所有缺陷已上报，16 个已确认修复，展现了良好的安全研究规范。

### 8. 不足与局限
- **强依赖命名质量**：当变量名无意义或代码混淆时，ADG 与 MIS 的语义关联失效，导致测试退化为随机探索（虽然低熵 MIS 自然被抑制，但可能遗漏缺陷）。
- **仿真环境局限**：SITL 无法复现硬件相关缺陷（传感器噪声、执行器响应延迟等），且部分仿真专用参数无法在真实设备上触发（87 个中约 42 个为仿真特有）。
- **误报处理依赖人工**：部分输入（如过低的电机 PWM 最大限值）其“异常”属于预期功能，需人工依据领域知识剔除，未能完全自动化。
- **赋值语句范围限制**：仅针对赋值链相关的 bug，无法检测缺失逻辑、函数调用错误等其他类型缺陷（占历史 bug 的 71.98%）。
- **调度策略未针对覆盖率反馈**：熵值仅依赖静态图结构，未动态结合仿真过程中的代码覆盖变化，可能使部分 MIS 过早衰减。
- **实验无多次重复**：论文未报告同一实验的多次运行标准差，结果的稳定性无法判断。

（完）

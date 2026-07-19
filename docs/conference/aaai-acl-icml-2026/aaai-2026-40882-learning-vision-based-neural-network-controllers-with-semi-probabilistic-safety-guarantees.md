---
title: Learning Vision-Based Neural Network Controllers with Semi-Probabilistic Safety Guarantees
title_zh: 学习具有半概率安全保证的基于视觉的神经网络控制器
authors: "Xinhang Ma, Junlin Wu, Hussein Sibai, Yiannis Kantaros, Yevgeniy Vorobeychik"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40882/44843"
tags: ["query:safe-codegen"]
score: 7.0
evidence: 确保基于视觉的自主系统控制的安全性
tldr: 针对基于视觉的自主控制系统缺乏形式化安全保证的问题，本文提出了一种半概率验证框架，该框架集成可达性分析与条件生成网络，并利用无分布尾界实现视觉神经网络控制器的可扩展安全验证。同时，设计了一种基于梯度的安全感知训练方法，通过新颖的安全损失函数提升控制器安全性。实验表明，该方法能有效保证控制策略的安全行为，为视觉驱动的机器人系统提供了重要的安全保障。贡献在于弥合了学习控制与形式验证之间的鸿沟。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40882/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 790, \"height\": 215, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40882/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 453, \"height\": 320, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40882/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40882/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1559, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40882/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1555, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40882/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 747, \"height\": 316, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40882/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 511, \"label\": \"Table\"}]"
motivation: 基于视觉的自主系统控制缺乏形式化安全保证，现有学习方法在这类场景中往往无法提供安全性证明。
method: 提出一种半概率验证框架，结合可达性分析、条件生成网络和无分布尾界，用于验证视觉神经网络控制器；并开发基于梯度的训练方法，引入安全损失函数。
result: 框架能够高效且可扩展地验证视觉控制器安全性，并通过安全感知训练提升控制器性能。
conclusion: 该方法为基于学习的视觉控制系统提供了一种实用的安全性保证手段，有助于实现安全的具身智能系统。
---

## Abstract
Ensuring safety in autonomous systems with vision-based control remains a critical challenge due to the high dimensionality of image inputs and the fact that the relationship between true system state and its visual manifestation is unknown. 
Existing methods for learning-based control in such settings typically lack formal safety guarantees.
To address this challenge, we introduce a novel semi-probabilistic verification framework that integrates reachability analysis with conditional generative networks and distribution-free tail bounds to enable efficient and scalable verification of vision-based neural network controllers.
Next, we develop a gradient-based training approach that employs a novel safety loss function, safety-aware data-sampling strategy to efficiently select and store critical training examples, and curriculum learning, to efficiently synthesize safe controllers in the semi-probabilistic framework.
Empirical evaluations in X-Plane 11 airplane landing simulation, CARLA-simulated autonomous lane following, F1Tenth vehicle lane following in a physical visually-rich miniature environment, and Airsim-simulated drone navigation and obstacle avoidance demonstrate the effectiveness of our method in achieving formal safety guarantees while maintaining strong nominal performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：基于视觉的自主控制（如自动驾驶、无人机导航）需要处理高维图像输入，但真实物理状态与图像之间的映射关系未知且复杂。现有学习型控制器大多缺乏形式化安全保证，传统形式验证方法又因图像空间维度过高而难以扩展。
- **核心挑战**：如何在仅有图像观测、状态感知模型未知的情况下，为基于神经网络的控制器提供可计算的形式化安全保证，并能在训练中主动提升该安全性。
- **整体含义**：论文旨在弥合“学习型视觉控制器”与“形式化安全验证”之间的鸿沟，提出一种实用的半概率安全保证框架及相应的安全感知训练方法。

### 2. 方法论
#### 2.1 系统建模与生成式近似
- 动力学系统：\(s_{t+1}=f(s_t,u_t)\)，观测 \(o_t = h(s_t,\omega)\)，其中 \(\omega\) 表示未知环境变化，动态 \(f\) 已知，\(h\) 未知。
- 使用条件生成网络 \(g(s,z)\) 近似观测映射，\(z\) 为潜在变量（均匀或高斯分布），训练为 cGAN。假设存在 \(\epsilon\) 使得 \(\sup_{s,\omega} \inf_z \|h(s,\omega)-g(s,z)\| \le \epsilon\)。

#### 2.2 半概率验证（SPV）框架
- **K-步可达集**：\(Reach_K(s_0,\pi)\) 为所有可能环境 \(\omega\) 下从 \(s_0\) 出发可达的状态集合。
- 利用生成器定义可验证的过近似集 \(\widehat{Reach}_K(s_0,\pi,g)\)，定理 1 保证真实可达集是其子集，因此在该集合上安全 ⇒ 真实安全。
- 对初始状态分布 \(D\) 未知，从 \(D\) 中独立采样 \(N\) 个初始状态，用无分布 Hoeffding 界得到总体安全概率的下界（置信度 \(1-\delta\)）。定理 2 给出：
  \[
  \Pr_{s\sim D}[P(Reach_K(s,\pi))] \ge \frac{|V|}{N} - \sqrt{\frac{1}{2N}\log\frac{2}{\delta}}
  \]
  其中 \(V\) 为采样中验证安全的初始状态集。

#### 2.3 安全控制器训练
- **优化目标**：最大化 \(\Pr_{s\sim D}[P(Reach_K(s,\pi_\theta))]\)，代理目标为最大化采样初始状态上安全验证的比例。
- **损失函数**：
  - 性能保持项 \(L_{\text{perf}}\)（模仿学习 \(\ell_2\) 损失或 RL 策略梯度）。
  - 安全项 \(L_{\text{safety}} = \frac{|\underline{\sigma}^{(i)}_K| + |\overline{\sigma}^{(i)}_K|}{K-1}\)，其中 \(\underline{\sigma},\overline{\sigma}\) 为安全得分 \(\sigma\) 的可微上下界（由 \(\alpha,\beta\)-CROWN 计算），度量可达区域的变化率。
- **自适应数据采样**：
  - 维护固定大小的随机状态集 \(S_0\) 和安全关键状态优先队列 \(S_A\)。
  - 预热阶段将每批中最困难的 \(m\%\) 个点加入 \(S_A\)。
  - 采样时，按比例 \(p\) 从 \(S_A\) 中加权采样（权重 \(w_i = e^{\alpha \eta(i)}\)，\(\eta(i) = L_{\text{safety}} + \max(0,|\underline{\sigma}|-\beta) + \max(0,|\overline{\sigma}|-\beta)\)），其余从 \(S_0\) 均匀抽取，保证多样性与安全挑战性。
- **课程学习**：逐步增加目标验证步数 \(K_1 < K_2 < \dots < K_n = K\)，以稳定训练。

### 3. 实验设计
- **测试场景与数据**：
  - X‑Plane 11 飞机滑行：20,000 组状态‑图像对，状态为横向偏移 \(d\in[-10,10]\) m、航向误差 \(\theta\in[-0.5,0.5]\) rad。
  - CARLA 自动驾驶车道保持：20,000 组，\(d\in[-0.8,0.8]\) m，\(\theta\in[-0.15,0.15]\) rad，跨多个地图与天气。
  - F1Tenth 微型物理城市车道保持：400 张实拍图像手工标注，在 CARLA 生成器上微调。
  - AirSim 无人机导航与避障：20,000 组，状态为 3D 位置与四元数姿态，图像分辨率 64×64。
- **对比基线**：
  - RESPO：基于迭代可达性分析的安全 RL。
  - SAC‑RCBF：集成鲁棒控制障碍函数层的安全 RL。
  - VSRL：将增量可达性验证融入安全 RL 的方法。
- **评价指标**：
  - 经验性能：100 次随机初始状态的累积奖励（路径跟随用归一化横向误差奖励，无人机用速度、姿态稳定性等组合奖励）。
  - 半概率安全保证：基于 2000 个 i.i.d. 初始状态，使用定理 2 计算安全概率下界随 K 的变化曲线。

### 4. 资源与算力
- 论文**未明确提及**使用的 GPU 型号、数量或具体训练时长。只给出了训练超参数（学习率 \(0.0005\)、批次大小 \(256\)、\(200\) 轮锚点训练；安全训练 \(100\) 轮、批次 \(128\)、学习率 \(0.0002\)；RL 部分 200k 步等）。因此无法从文中推算所需算力规模。

### 5. 实验数量与充分性
- **主要实验组**：4 个不同仿真/物理环境下的控制器训练与验证，每个均包含性能箱线图和安全概率曲线（4 组结果）。
- **消融实验**：在 X‑Plane 环境比较 cGAN 与扩散模型生成器的效果（性能与安全曲线各 1 组图）。
- **假设验证**：对潜在维度 2～64 共 8 个取值，测试图像重建 MSE，验证生成器近似能力（1 组图）。
- **比较基线**：与 3 种安全 RL/控制方法全面对比，指标统一，评估方式较公平。
- 总体实验覆盖了仿真到简单物理平台、不同任务类型，并包含关键模块的消融和前提假设验证，**整体上较为充分且客观**。但物理实验数据量较小（400 张），可能限制该场景结论的泛化性。

### 6. 主要结论与发现
- SPV 框架能对基于视觉的神经网络控制器给出形式化的概率安全下界，且计算可扩展。
- 提出的安全感知训练方法（SPVT）在保持标称性能的同时，显著提升了控制器的可验证安全概率。
- 在高维图像输入的无人机任务中，SPVT 是唯一可成功训练并维持安全性的方法，VSRL 因全输入空间验证无法进行而失败。
- cGAN 生成器在实验条件下能够充分近似感知映射，使得 SPV 验证的声音性得以成立。

### 7. 优点（亮点）
- 首次将条件生成模型与可达性分析、无分布界结合，实现视觉控制器的高效半概率安全验证。
- 设计了可微的安全损失和自适应重采样策略，将形式验证融入梯度训练，完成“学习‑验证”闭环。
- 在真实物理小车（F1Tenth）上验证方法，证明了一定的实用性。
- 课程学习设计有助于稳定训练长步数安全约束。

### 8. 不足与局限
- **感知假设严格**：要求生成器能以 \(\epsilon\) 误差覆盖真实图像，实际中可能难以满足，尤其复杂高分辨率场景。
- **输入限制**：目前仅支持灰度、较低分辨率图像，且潜在维度较小，限制了表达丰富环境变化的能力。
- **动态已知**：假设系统动态 \(f\) 完全已知，不适用于未知动力学任务。
- **传感器单一**：仅处理单目图像，未扩展到多模态感知。
- **物理实验数据量小**：F1Tenth 仅用 400 张图像微调，其结论的统计可靠性可能不足。
- **安全性质形式受限**：安全属性需能表达为状态空间上的简单谓词（如误差阈值、姿态界限），对语义级安全（如“不撞行人”）无法直接应用。
- **依赖预训练锚点**：训练需要先有一个经验安全的控制器作为起点，若锚点本身不安全，方法可能无法收敛。

（完）

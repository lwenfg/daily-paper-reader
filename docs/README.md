<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-04-29 ~ 2026-05-28
- 运行时间：2026-05-28 10:59:05 UTC
- 运行状态：成功
- 本次总论文数：55
- 精读区：44
- 速读区：11

### 今日简报（AI）
今日深挖55篇大模型安全论文，重点拆解了两篇满分越狱攻击研究。
最值得关注的是利用对话上下文“温水煮青蛙”式的高隐蔽攻击，以及通过模糊测试突破多模态工具链的越狱新路径。
建议读者警惕：攻击已从单文本诱导转向多步骤、跨工具的现实场景渗透，需更新安全测试视角。
- 详情：[/20260429-20260528/README](/20260429-20260528/README)

### 精读区论文标签
1. [ContextualJailbreak: Evolutionary Red-Teaming via Simulated Conversational Priming](/20260429-20260528/2605.02647v1-contextualjailbreak-evolutionary-red-teaming-via-simulated-conversational-priming)  
   标签：评分：10.0/10、query:jba
   evidence：提出通过对话启动的进化红队测试方法，发现越狱漏洞
2. [OrchJail: Jailbreaking Tool-Calling Text-to-Image Agents by Orchestration-Guided Fuzzing](/20260429-20260528/2605.07414v1-orchjail-jailbreaking-tool-calling-text-to-image-agents-by-orchestration-guided-fuzzing)  
   标签：评分：10.0/10、query:jba
   evidence：提出OrchJail，编排引导模糊测试框架，越狱调用工具文本到图像智能体。
3. [Position: AI Security Policy Should Target Systems, Not Models](/20260429-20260528/2605.09504v1-position-ai-security-policy-should-target-systems-not-models)  
   标签：评分：10.0/10、query:jba
   evidence：LLM智能体群协同越狱前沿模型
4. [Metis: Learning to Jailbreak LLMs via Self-Evolving Metacognitive Policy Optimization](/20260429-20260528/2605.10067v1-metis-learning-to-jailbreak-llms-via-self-evolving-metacognitive-policy-optimization)  
   标签：评分：10.0/10、query:jba
   evidence：将越狱建模为推断时策略优化，使用自演化元认知环和语义梯度发现越狱攻击。
5. [Metis: Learning to Jailbreak LLMs via Self-Evolving Metacognitive Policy Optimization](/20260429-20260528/2605.10067v2-metis-learning-to-jailbreak-llms-via-self-evolving-metacognitive-policy-optimization)  
   标签：评分：10.0/10、query:jba
   evidence：自我演化的元认知策略优化，用于红队测试揭示LLM漏洞
6. [LITMUS: Benchmarking Behavioral Jailbreaks of LLM Agents in Real OS Environments](/20260429-20260528/2605.10779v1-litmus-benchmarking-behavioral-jailbreaks-of-llm-agents-in-real-os-environments)  
   标签：评分：10.0/10、query:jba
   evidence：基准测试LLM智能体执行危险OS操作的行为越狱
7. [RoboJailBench: Benchmarking Adversarial Attacks and Defenses in Embodied Robotic Agents](/20260429-20260528/2605.19328v1-robojailbench-benchmarking-adversarial-attacks-and-defenses-in-embodied-robotic-agents)  
   标签：评分：10.0/10、query:jba
   evidence：具身AI智能体越狱攻击与防御的基准评测
8. [LASH: Adaptive Semantic Hybridization for Black-Box Jailbreaking of Large Language Models](/20260429-20260528/2605.21362v1-lash-adaptive-semantic-hybridization-for-black-box-jailbreaking-of-large-language-models)  
   标签：评分：10.0/10、query:jba
   evidence：自适应语义混合框架组合多种基础攻击输出以生成更有效的越狱提示
9. [TwinGate: Stateful Defense against Decompositional Jailbreaks in Untraceable Traffic via Asymmetric Contrastive Learning](/20260429-20260528/2604.27861v1-twingate-stateful-defense-against-decompositional-jailbreaks-in-untraceable-traffic-via-asymmetric-contrastive-learning)  
   标签：评分：9.0/10、query:jba
   evidence：利用非对称对比学习的针对分解式越狱攻击的有状态防御
10. [Attention Is Where You Attack](/20260429-20260528/2605.00236v1-attention-is-where-you-attack)  
   标签：评分：9.0/10、query:jba
   evidence：白盒对抗攻击重定向注意力头以绕过安全对齐
11. [Jailbreaking Vision-Language Models Through the Visual Modality](/20260429-20260528/2605.00583v1-jailbreaking-vision-language-models-through-the-visual-modality)  
   标签：评分：9.0/10、query:jba
   evidence：提出四种利用视觉组件的越狱攻击，绕过VLM的安全对齐
12. [SRTJ: Self-Evolving Rule-Driven Training-Free LLM Jailbreaking](/20260429-20260528/2605.00974v1-srtj-self-evolving-rule-driven-training-free-llm-jailbreaking)  
   标签：评分：9.0/10、query:jba
   evidence：无训练的自进化规则驱动越狱提示生成
13. [MultiBreak: A Scalable and Diverse Multi-turn Jailbreak Benchmark for Evaluating LLM Safety](/20260429-20260528/2605.01687v1-multibreak-a-scalable-and-diverse-multi-turn-jailbreak-benchmark-for-evaluating-llm-safety)  
   标签：评分：9.0/10、query:jba
   evidence：引入主动学习流程生成多样化多轮越狱提示
14. [TrajShield: Trajectory-Level Safety Mediation for Defending Text-to-Video Models Against Jailbreak Attacks](/20260429-20260528/2605.01761v1-trajshield-trajectory-level-safety-mediation-for-defending-text-to-video-models-against-jailbreak-attacks)  
   标签：评分：9.0/10、query:jba
   evidence：通过轨迹级安全中介防御文本到视频模型的越狱攻击
15. [Disentangling Intent from Role: Adversarial Self-Play for Persona-Invariant Safety Alignment](/20260429-20260528/2605.01899v1-disentangling-intent-from-role-adversarial-self-play-for-persona-invariant-safety-alignment)  
   标签：评分：9.0/10、query:jba
   evidence：提出基于对抗自博弈的角色不变安全对齐防御框架
16. [Revisiting JBShield: Breaking and Rebuilding Representation-Level Jailbreak Defenses](/20260429-20260528/2605.03095v1-revisiting-jbshield-breaking-and-rebuilding-representation-level-jailbreak-defenses)  
   标签：评分：9.0/10、query:jba
   evidence：在自适应攻击下攻破并重建表示级越狱防御JBShield
17. [Sparse Tokens Suffice: Jailbreaking Audio Language Models via Token-Aware Gradient Optimization](/20260429-20260528/2605.04700v1-sparse-tokens-suffice-jailbreaking-audio-language-models-via-token-aware-gradient-optimization)  
   标签：评分：9.0/10、query:jba
   evidence：优化音频扰动以越狱音频语言模型
18. [SoK: Robustness in Large Language Models against Jailbreak Attacks](/20260429-20260528/2605.05058v1-sok-robustness-in-large-language-models-against-jailbreak-attacks)  
   标签：评分：9.0/10、query:jba
   evidence：系统化LLM越狱攻击与防御知识，提出多维度评估框架Security Cube
19. [Conceal, Reconstruct, Jailbreak: Exploiting the Reconstruction-Concealment Tradeoff in MLLMs](/20260429-20260528/2605.05709v1-conceal-reconstruct-jailbreak-exploiting-the-reconstruction-concealment-tradeoff-in-mllms)  
   标签：评分：9.0/10、query:jba
   evidence：提出隐蔽感知变体，利用字符删除变换平衡重构与隐蔽，在MLLMs上取得更高越狱成功率。
20. [Mitigating Many-shot Jailbreak Attacks with One Single Demonstration](/20260429-20260528/2605.08277v1-mitigating-many-shot-jailbreak-attacks-with-one-single-demonstration)  
   标签：评分：9.0/10、query:jba
   evidence：通过附加一个固定演示防御多示例越狱攻击
21. [Not All Turns Matter: Credit Assignment for Multi-Turn Jailbreaking](/20260429-20260528/2605.08778v1-not-all-turns-matter-credit-assignment-for-multi-turn-jailbreaking)  
   标签：评分：9.0/10、query:jba
   evidence：通过信用分配学习多轮越狱攻击策略
22. [The Art of the Jailbreak: Formulating Jailbreak Attacks for LLM Security Beyond Binary Scoring](/20260429-20260528/2605.09225v1-the-art-of-the-jailbreak-formulating-jailbreak-attacks-for-llm-security-beyond-binary-scoring)  
   标签：评分：9.0/10、query:jba
   evidence：大规模组合越狱数据集及自动策略组合生成对抗提示
23. [Guaranteed Jailbreaking Defense via Disrupt-and-Rectify Smoothing](/20260429-20260528/2605.10582v1-guaranteed-jailbreaking-defense-via-disrupt-and-rectify-smoothing)  
   标签：评分：9.0/10、query:jba
   evidence：提出基于平滑的越狱攻击防御方法
24. [Re-Triggering Safeguards within LLMs for Jailbreak Detection](/20260429-20260528/2605.10611v1-re-triggering-safeguards-within-llms-for-jailbreak-detection)  
   标签：评分：9.0/10、query:jba
   evidence：通过嵌入扰动重新触发LLM内部安全机制以检测越狱提示
25. [Break the Brake, Not the Wheel: Untargeted Jailbreak via Entropy Maximization](/20260429-20260528/2605.10764v1-break-the-brake-not-the-wheel-untargeted-jailbreak-via-entropy-maximization)  
   标签：评分：9.0/10、query:jba
   evidence：提出基于熵最大化的无目标越狱攻击方法
26. [Safety Context Injection: Inference-Time Safety Alignment via Static Filtering and Agentic Analysis](/20260429-20260528/2605.11664v1-safety-context-injection-inference-time-safety-alignment-via-static-filtering-and-agentic-analysis)  
   标签：评分：9.0/10、query:jba
   evidence：通过静态过滤和代理分析在推理时实现安全对齐以防御越狱攻击
27. [SafeSteer: A Decoding-level Defense Mechanism for Multimodal Large Language Models](/20260429-20260528/2605.11716v1-safesteer-a-decoding-level-defense-mechanism-for-multimodal-large-language-models)  
   标签：评分：9.0/10、query:jba
   evidence：提出SafeSteer，一种利用解码阶段固有安全能力的多模态大模型越狱防御方法。
28. [Persona-Conditioned Adversarial Prompting: Multi-Identity Red-Teaming for Adversarial Discovery and Mitigation](/20260429-20260528/2605.11730v1-persona-conditioned-adversarial-prompting-multi-identity-red-teaming-for-adversarial-discovery-and-mitigation)  
   标签：评分：9.0/10、query:jba
   evidence：基于多身份对抗提示的自动红队测试
29. [Persona-Conditioned Adversarial Prompting (PCAP): Multi-Identity Red-Teaming for Enhanced Adversarial Prompt Discovery](/20260429-20260528/2605.12565v1-persona-conditioned-adversarial-prompting-pcap-multi-identity-red-teaming-for-enhanced-adversarial-prompt-discovery)  
   标签：评分：9.0/10、query:jba
   evidence：基于攻击者角色条件化的对抗性搜索，发现多样且可迁移的越狱攻击，提高攻击策略覆盖率和多样性。
30. [EVA: Editing for Versatile Alignment against Jailbreaks](/20260429-20260528/2605.14750v1-eva-editing-for-versatile-alignment-against-jailbreaks)  
   标签：评分：9.0/10、query:jba
   evidence：直接编辑模型参数实现针对越狱攻击的安全对齐
31. [New Wide-Net-Casting Jailbreak Attacks Risk Large Models](/20260429-20260528/2605.17128v1-new-wide-net-casting-jailbreak-attacks-risk-large-models)  
   标签：评分：9.0/10、query:jba
   evidence：提出针对多模型的广撒网式越狱攻击
32. [Babel: Jailbreaking Safety Attention via Obfuscation Distribution Optimized Sampling](/20260429-20260528/2605.17971v1-babel-jailbreaking-safety-attention-via-obfuscation-distribution-optimized-sampling)  
   标签：评分：9.0/10、query:jba
   evidence：利用稀疏安全注意力通过混淆优化采样进行高效黑盒越狱攻击
33. [Exploring and Developing a Pre-Model Safeguard with Draft Models](/20260429-20260528/2605.19321v1-exploring-and-developing-a-pre-model-safeguard-with-draft-models)  
   标签：评分：9.0/10、query:jba
   evidence：开发基于越狱攻击迁移性的预模型防护，在目标模型推理前审计提示安全性。
34. [REFLECTOR: Internalizing Step-wise Reflection against Indirect Jailbreak](/20260429-20260528/2605.20654v1-reflector-internalizing-step-wise-reflection-against-indirect-jailbreak)  
   标签：评分：9.0/10、query:jba
   evidence：通过在生成轨迹中内化自我反思来防御多步越狱攻击
35. [Adversarial Reframing: A Framework for Targeted Generation in Language Models](/20260429-20260528/2605.21674v1-adversarial-reframing-a-framework-for-targeted-generation-in-language-models)  
   标签：评分：9.0/10、query:jba
   evidence：迭代搜索寻找绕过安全过滤器的越狱提示
36. [Reasoning as an Attack Surface: Adaptive Evolutionary CoT Jailbreaks for LLMs](/20260429-20260528/2605.24497v1-reasoning-as-an-attack-surface-adaptive-evolutionary-cot-jailbreaks-for-llms)  
   标签：评分：9.0/10、query:jba
   evidence：自适应进化思维链越狱框架，自动生成基于推理的有害提示
37. [Steering Beyond the Support: Adversarial Training on Unsupervised Jailbroken Activation Simulation](/20260429-20260528/2605.24535v1-steering-beyond-the-support-adversarial-training-on-unsupervised-jailbroken-activation-simulation)  
   标签：评分：9.0/10、query:jba
   evidence：提出基于无监督激活模拟的零样本越狱防御对抗训练
38. [Ellipsoid Control: A White-list Jailbreak Defense via Benign Latent Modeling](/20260429-20260528/2605.24552v1-ellipsoid-control-a-white-list-jailbreak-defense-via-benign-latent-modeling)  
   标签：评分：9.0/10、query:jba
   evidence：通过建模良性潜在区域的白名单防御方法拒绝越狱提示
39. [Localization then Neutralization: Gradient-guided Token Suppression against Visual Prompt Injection Attack](/20260429-20260528/2605.25194v1-localization-then-neutralization-gradient-guided-token-suppression-against-visual-prompt-injection-attack)  
   标签：评分：9.0/10、query:jba
   evidence：通过梯度引导的令牌掩码防御多模态LLM中的视觉提示注入攻击
40. [Furina: Fragmented Uncertainty-Driven Refusal Instability Attack](/20260429-20260528/2605.26158v1-furina-fragmented-uncertainty-driven-refusal-instability-attack)  
   标签：评分：9.0/10、query:jba
   evidence：提出利用拒绝不稳定区域的碎片化不确定性越狱攻击
41. [Jailbreak susceptibility prediction and mitigation via the behavioral geometry of models](/20260429-20260528/2605.26409v1-jailbreak-susceptibility-prediction-and-mitigation-via-the-behavioral-geometry-of-models)  
   标签：评分：9.0/10、query:jba
   evidence：提出通过行为几何进行防御迁移以预测和缓解越狱易感性
42. [PAST2HARM: A Simple Adaptive Past Tense Attack for Jailbreaking Multimodal AI](/20260429-20260528/2605.27545v1-past2harm-a-simple-adaptive-past-tense-attack-for-jailbreaking-multimodal-ai)  
   标签：评分：9.0/10、query:jba
   evidence：针对多模态文本到图像模型的自适应过去式越狱攻击
43. [Disentangling Adversarial Prompts: A Semantic-Graph Defense for Robust LLM Security](/20260429-20260528/2605.27823v1-disentangling-adversarial-prompts-a-semantic-graph-defense-for-robust-llm-security)  
   标签：评分：9.0/10、query:jba
   evidence：提出对抗提示解耦框架，主动识别并中和恶意提示成分以防御越狱和注入攻击
44. [Mitigating Adaptive Attacks against Reasoning Models with Activation Consistency Training](/20260429-20260528/2605.28467v1-mitigating-adaptive-attacks-against-reasoning-models-with-activation-consistency-training)  
   标签：评分：9.0/10、query:jba
   evidence：提出激活一致性训练，一种自监督微调目标，强制干净提示和对抗性重写提示行为一致，有效防御提示注入越狱攻击。

### 速读区论文标签
1. [Minimal, Local, Causal Explanations for Jailbreak Success in Large Language Models](/20260429-20260528/2605.00123v1-minimal-local-causal-explanations-for-jailbreak-success-in-large-language-models)  
   标签：评分：8.0/10、query:jba
   evidence：通过因果表示分析解释安全对齐LLM为何易受越狱攻击
2. [A Systematic Investigation of The RL-Jailbreaker in LLMs](/20260429-20260528/2605.07032v1-a-systematic-investigation-of-the-rl-jailbreaker-in-llms)  
   标签：评分：8.0/10、query:jba
   evidence：系统分析基于强化学习的越狱框架以优化攻击生成
3. [Why Do Aligned LLMs Remain Jailbreakable: Refusal-Escape Directions, Operator-Level Sources, and Safety-Utility Trade-off](/20260429-20260528/2605.08878v1-why-do-aligned-llms-remain-jailbreakable-refusal-escape-directions-operator-level-sources-and-safety-utility-trade-off)  
   标签：评分：8.0/10、query:jba
   evidence：发现使对齐LLM仍可被越狱的拒绝逃逸方向
4. [Before the Last Token: Diagnosing Final-Token Safety Probe Failures](/20260429-20260528/2605.12726v1-before-the-last-token-diagnosing-final-token-safety-probe-failures)  
   标签：评分：8.0/10、query:jba
   evidence：诊断最终令牌安全探针为何遗漏越狱，找到预填充时期证据分布问题
5. [Compositional Jailbreaking: An Empirical Analysis of Mutator Chain Interactions in Aligned LLMs](/20260429-20260528/2605.15598v1-compositional-jailbreaking-an-empirical-analysis-of-mutator-chain-interactions-in-aligned-llms)  
   标签：评分：8.0/10、query:jba
   evidence：系统研究突变链以揭示组合越狱攻击的交互特性
6. [Jailbroken Frontier Models Retain Their Capabilities](/20260429-20260528/2605.00267v2-jailbroken-frontier-models-retain-their-capabilities)  
   标签：评分：7.0/10、query:jba
   evidence：分析安全对齐模型被越狱后的能力退化
7. [MT-JailBench: A Modular Benchmark for Understanding Multi-Turn Jailbreak Attacks](/20260429-20260528/2605.11002v1-mt-jailbench-a-modular-benchmark-for-understanding-multi-turn-jailbreak-attacks)  
   标签：评分：7.0/10、query:jba
   evidence：评估大模型多轮越狱攻击的模块化基准
8. [Quantifying LLM Safety Degradation Under Repeated Attacks Using Survival Analysis](/20260429-20260528/2605.12869v1-quantifying-llm-safety-degradation-under-repeated-attacks-using-survival-analysis)  
   标签：评分：7.0/10、query:jba
   evidence：生存分析建模LLM在重复越狱攻击下的脆弱性
9. [The Great Pretender: A Stochasticity Problem in LLM Jailbreak](/20260429-20260528/2605.14418v1-the-great-pretender-a-stochasticity-problem-in-llm-jailbreak)  
   标签：评分：7.0/10、query:jba
   evidence：指出越狱生成与评估中的随机性问题，质疑报告ASR的可靠性
10. [XL-SafetyBench: A Country-Grounded Cross-Cultural Benchmark for LLM Safety and Cultural Sensitivity](/20260429-20260528/2605.05662v1-xl-safetybench-a-country-grounded-cross-cultural-benchmark-for-llm-safety-and-cultural-sensitivity)  
   标签：评分：6.0/10、query:jba
   evidence：提供面向不同国家的越狱对抗提示基准，用于LLM安全评估
11. [Jailbreak to Protect: Buffering and Reinforcing via Temporary Jailbreaking for Safe Fine-Tuning in Large Language Models](/20260429-20260528/2605.24550v1-jailbreak-to-protect-buffering-and-reinforcing-via-temporary-jailbreaking-for-safe-fine-tuning-in-large-language-models)  
   标签：评分：6.0/10、query:jba
   evidence：重新审视临时越狱作为有害微调防御，饱和降低安全性的梯度。


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>

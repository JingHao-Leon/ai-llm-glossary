# 训练 | Training

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录大模型训练相关的 15 个核心术语，包括预训练（Pre-training）、后训练（Post-training）、RLHF、奖励模型、DPO、GRPO、损失函数、梯度下降、学习率、数据清洗、合成数据与分布式训练（Distributed Training）等。
This page covers 15 core terms on LLM training, including pre-training, post-training, RLHF, reward models, DPO, GRPO, loss functions, gradient descent, learning rate, data cleaning, synthetic data, and distributed training.

---

### 预训练（Pre-training）
**英文**：Pre-training | **类别**：训练

预训练是在海量无标注文本上以自监督方式训练模型、使其掌握通用语言能力的第一阶段训练。

其核心目标是"下一个 Token 预测"，模型通过预测海量语料中的下一个词学习语法、知识与初步推理能力。预训练消耗绝大部分算力（常需数千张 GPU 运行数月），产出的基座模型再经[后训练](#后训练post-training)对齐人类偏好。相关术语：[基础模型](basic-concepts.md#基础模型foundation-model)、[Scaling Law](#scaling-law扩展定律)。

### 后训练（Post-training）
**英文**：Post-training | **类别**：训练

后训练是在预训练完成之后、让模型对齐人类意图与偏好的系列训练阶段的总称。

后训练通常包括[指令微调](fine-tuning.md#指令微调instruction-tuning)（SFT）、[RLHF](#rlhf人类反馈强化学习) 或 [DPO](#dpo直接偏好优化) 等步骤，把"只会续写文本"的基座模型变成"能听懂指令"的对话助手。近年来后训练还扩展出强化推理能力（Reasoning RL）等新范式。

### RLHF（人类反馈强化学习）
**英文**：Reinforcement Learning from Human Feedback (RLHF) | **类别**：训练

RLHF 是利用人类偏好数据训练奖励模型、再用强化学习优化语言模型输出质量的对齐方法。

典型流程为：收集人类对多个回答的排序 → 训练奖励模型（Reward Model）→ 用 PPO 等算法微调模型使其获得更高奖励。RLHF 是 ChatGPT 等对话模型效果飞跃的关键，但流程复杂、训练不稳定，部分场景已被 [DPO](#dpo直接偏好优化) 替代。相关术语：[对齐](safety-alignment.md#对齐alignment)。



### 奖励模型（Reward Model）
**英文**：Reward Model (RM) | **类别**：训练

奖励模型是根据人类偏好数据训练、为模型输出打分以指导对齐的评分模型。

在 [RLHF](#rlhf人类反馈强化学习) 中，它替代真人实时评判：先由人类对多个回答排序，再训练奖励模型拟合这一偏好，最后用强化学习让语言模型最大化奖励得分。奖励模型的质量直接决定对齐全链路效果，[DPO](#dpo直接偏好优化) 则绕过了显式训练奖励模型的环节。
### DPO（直接偏好优化）
**英文**：Direct Preference Optimization (DPO) | **类别**：训练

DPO 是一种无需训练奖励模型、直接在偏好数据对上优化语言模型的对齐算法。

它将 RLHF 的强化学习问题转化为简单的二分类损失，训练更稳定、实现更简单，已成为开源社区最主流的对齐方法之一。其变体包括 IPO、KTO、ORPO 等。相关术语：[RLHF](#rlhf人类反馈强化学习)、[损失函数](#损失函数loss-function)。



### GRPO（组相对策略优化）
**英文**：Group Relative Policy Optimization (GRPO) | **类别**：训练

GRPO 是一种去掉 Critic 价值网络、用同组样本的相对得分估计优势的强化学习算法。

它由 DeepSeek 提出并用于训练 R1 等推理模型：对同一问题采样一组回答，以组内平均奖励为基线计算优势，大幅降低显存与训练成本。GRPO 已成为训练[推理模型](basic-concepts.md#推理模型reasoning-model)的主流 RL 算法。相关术语：[RLHF](#rlhf人类反馈强化学习)、[DPO](#dpo直接偏好优化)。
### 损失函数（Loss Function）
**英文**：Loss Function | **类别**：训练

损失函数是量化模型预测与真实目标之间差距、为参数更新提供方向的数学函数。

语言模型预训练普遍使用交叉熵损失（Cross-Entropy Loss），衡量预测分布与真实 Token 分布的差异。训练过程本质上就是通过[梯度下降](#梯度下降gradient-descent)不断最小化损失函数。

### 梯度下降（Gradient Descent）
**英文**：Gradient Descent | **类别**：训练

梯度下降是沿损失函数梯度的反方向迭代更新参数、以最小化损失的优化算法。

实际训练中采用其随机版本（SGD）及 Adam、AdamW 等自适应变体，每次用一小批数据（mini-batch）估算梯度。梯度经反向传播（Backpropagation）计算，配合[学习率](#学习率learning-rate)控制更新步长。相关术语：[残差连接](model-architecture.md#残差连接residual-connection)。

### 学习率（Learning Rate）
**英文**：Learning Rate | **类别**：训练

学习率是控制每次参数更新步长的超参数，是训练中最重要的超参数之一。

学习率过大会导致训练震荡甚至发散，过小则收敛缓慢。大模型训练普遍采用预热（Warmup）加余弦衰减的调度策略，预训练学习率通常在 1e-4 量级，微调时更小。相关术语：[梯度下降](#梯度下降gradient-descent)。

### 数据清洗（Data Cleaning）
**英文**：Data Cleaning | **类别**：训练

数据清洗是对训练语料进行去重、过滤低质内容、去除有害信息等预处理的过程。

业界共识是"数据质量决定模型上限"：去重（Deduplication）可防止模型记忆重复片段，质量过滤能显著提升下游表现。主流做法结合规则、分类器与困惑度打分构建清洗流水线，数据配比（Data Mixture）同样是核心机密。



### 合成数据（Synthetic Data）
**英文**：Synthetic Data | **类别**：训练

合成数据是由模型而非人类生成、用于训练或微调其他模型（或模型自身）的数据。

它在真实数据稀缺或标注昂贵的场景尤为重要，常见用途包括指令数据扩增、思维链样本生成与对齐数据构造，[知识蒸馏](fine-tuning.md#知识蒸馏distillation)本质上也是一种合成数据方法。合成数据同样需要[数据清洗](#数据清洗data-cleaning)与质量过滤，否则可能放大错误与偏见。
### 分布式训练（Distributed Training）
**英文**：Distributed Training | **类别**：训练

分布式训练是将模型训练任务拆分到成百上千张 GPU 上协同完成的技术体系。

主要并行策略包括数据并行（DP）、张量并行（TP）、流水线并行（PP）以及 ZeRO、FSDP 等显存优化方案。万亿级模型的预训练必须依赖 3D 混合并行与高效的通信调度，常用框架有 Megatron-LM、DeepSpeed、PyTorch FSDP 等。

### 过拟合（Overfitting）
**英文**：Overfitting | **类别**：训练

过拟合是模型过度记忆训练数据细节、在未见数据上表现变差的现象。

典型表现为训练损失持续下降而验证损失回升。缓解手段包括增加数据量、正则化（Dropout、权重衰减）、早停（Early Stopping）等。微调小数据集时过拟合尤为常见，通常只需训练 1–3 个 epoch。

### 灾难性遗忘（Catastrophic Forgetting）
**英文**：Catastrophic Forgetting | **类别**：训练

灾难性遗忘是模型在学习新任务时丢失原有知识与能力的现象。

在[全参微调](fine-tuning.md#全参微调full-parameter-fine-tuning)中尤为明显：用垂直领域数据微调后，模型的通用对话能力可能显著退化。缓解方法包括混合通用数据回放、降低学习率，或使用 [LoRA](fine-tuning.md#lora低秩自适应) 等只更新少量参数的方法。

### Scaling Law（扩展定律）
**英文**：Scaling Law | **类别**：训练

Scaling Law 是描述模型性能随参数量、数据量和计算量增长呈幂律改善的经验规律。

OpenAI（2020）与 DeepMind 的 Chinchilla 论文（2022）奠定了该领域基础：Chinchilla 指出模型参数量与训练 Token 数应按约 1:20 的比例同步扩展才算"计算最优"。Scaling Law 指导着大模型的资源配置，但[涌现能力](basic-concepts.md#涌现能力emergent-abilities)的出现说明幂律之外仍存在突变。

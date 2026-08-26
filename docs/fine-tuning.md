# 微调与适配 | Fine-tuning & Adaptation

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录模型微调与适配相关的 11 个核心术语，包括监督微调（SFT）、LoRA、QLoRA、PEFT、全参微调、知识蒸馏（Distillation）、指令微调与模型合并等。
This page covers 11 core terms on fine-tuning and adaptation, including SFT, LoRA, QLoRA, PEFT, full-parameter fine-tuning, knowledge distillation, instruction tuning, and model merging.

---

### 监督微调（SFT）
**英文**：Supervised Fine-Tuning (SFT) | **类别**：微调与适配

监督微调（SFT）是用"指令-回答"格式的标注数据对预训练模型进行有监督训练的过程。

SFT 是[后训练](training.md#后训练post-training)的第一步，让基座模型学会遵循指令、以对话形式作答。数据质量远比数量重要，数千条高质量样本（如 LIMA 论文所示）即可获得良好效果。相关术语：[指令微调](#指令微调instruction-tuning)、[RLHF](training.md#rlhf人类反馈强化学习)。

### LoRA（低秩自适应）
**英文**：Low-Rank Adaptation (LoRA) | **类别**：微调与适配

LoRA 是一种冻结原模型权重、仅训练低秩矩阵来近似参数增量的高效微调方法。

它将权重更新分解为两个小矩阵的乘积，可训练参数量通常不到全模型的 1%，显存需求大幅降低且不会破坏原模型能力。训练得到的 LoRA 权重可与基座合并或按需插拔，是开源社区最流行的微调方案。相关术语：[PEFT](#peft参数高效微调)、[QLoRA](#qlora量化低秩微调)。

### QLoRA（量化低秩微调）
**英文**：Quantized Low-Rank Adaptation (QLoRA) | **类别**：微调与适配

QLoRA 是将基座模型量化为 4-bit 后再进行 LoRA 微调、进一步降低显存占用的技术。

通过 NF4 量化、双重量化与分页优化器，QLoRA 使单张消费级显卡（24GB 显存）即可微调 65B 级模型，而效果接近 16-bit 全量微调。相关术语：[量化](inference-deployment.md#量化quantization)、[LoRA](#lora低秩自适应)。

### PEFT（参数高效微调）
**英文**：Parameter-Efficient Fine-Tuning (PEFT) | **类别**：微调与适配

PEFT 是只更新模型一小部分参数即可完成微调的一类方法的总称。

代表方法包括 [LoRA](#lora低秩自适应)、[Adapter](#adapter适配器)、[提示微调](#提示微调prompt-tuning)、Prefix Tuning 等。相比[全参微调](#全参微调full-parameter-fine-tuning)，PEFT 显著降低算力门槛、便于多任务权重管理，并有效缓解[灾难性遗忘](training.md#灾难性遗忘catastrophic-forgetting)。

### 全参微调（Full-Parameter Fine-Tuning）
**英文**：Full-Parameter Fine-Tuning | **类别**：微调与适配

全参微调是在微调阶段更新模型全部参数的训练方式。

它能最大程度地让模型适配新任务，效果上限通常高于 PEFT 方法，但显存开销巨大（7B 模型全参微调约需 80GB 以上显存），且更容易发生[灾难性遗忘](training.md#灾难性遗忘catastrophic-forgetting)。相关术语：[SFT](#监督微调sft)。

### 知识蒸馏（Distillation）
**英文**：Knowledge Distillation | **类别**：微调与适配

知识蒸馏是用大模型（教师）的输出训练小模型（学生）、将能力迁移到更小模型的技术。

学生模型学习教师模型的输出分布（软标签）而非硬标签，能以远小于教师的参数量逼近其表现。DeepSeek-R1 蒸馏系列、Gemma 等均是蒸馏的典型应用，是模型小型化的核心手段。相关术语：[量化](inference-deployment.md#量化quantization)。

### 指令微调（Instruction Tuning）
**英文**：Instruction Tuning | **类别**：微调与适配

指令微调是用多样化的"指令-响应"数据训练模型、使其学会遵循人类指令的微调方式。

它与 [SFT](#监督微调sft) 在实践中基本同义，强调训练数据以任务指令形式组织。FLAN 等研究证明，覆盖任务类型越广，模型对未见指令的泛化能力越强。相关术语：[后训练](training.md#后训练post-training)。

### Adapter（适配器）
**英文**：Adapter | **类别**：微调与适配

Adapter 是在预训练模型的层之间插入小型可训练模块、仅训练这些模块的微调方法。

每个 Adapter 通常只含几百万参数，不同任务可训练不同 Adapter 并灵活组合。它与 [LoRA](#lora低秩自适应) 同属 [PEFT](#peft参数高效微调) 家族，区别在于 Adapter 会在推理时增加少量计算，而 LoRA 合并后零开销。

### 提示微调（Prompt Tuning）
**英文**：Prompt Tuning | **类别**：微调与适配

提示微调是冻结模型全部参数、只训练一小段连续向量作为"软提示"的轻量微调方法。

可训练参数仅为输入层的几十个虚拟 Token 嵌入，参数效率极高，适合同一基座上快速切换大量下游任务。其变体 P-Tuning v2 将软提示扩展到每一层，效果可与全量微调媲美。

### 领域适配（Domain Adaptation）
**英文**：Domain Adaptation | **类别**：微调与适配

领域适配是让通用模型适应医疗、法律、金融等特定领域知识与语气的过程。

常见路径包括领域继续预训练（Continued Pre-training）、领域 [SFT](#监督微调sft) 与 [RAG](rag-retrieval.md#rag检索增强生成) 外挂知识库。选择微调还是 RAG 取决于需要注入的是"能力与风格"还是"事实与知识"。相关术语：[灾难性遗忘](training.md#灾难性遗忘catastrophic-forgetting)。

### 模型合并（Model Merging）
**英文**：Model Merging | **类别**：微调与适配

模型合并是将多个同源微调模型的权重直接加权融合、获得兼具各方能力的新模型的技术。

常见方法包括简单平均、SLERP 球面插值、Task Arithmetic 与 TIES-Merging 等。合并无需训练算力，是开源社区低成本"炼制"强模型的流行玩法，但要求参与合并的模型共享同一基座。

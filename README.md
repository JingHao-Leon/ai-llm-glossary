# AI 大模型术语表 | Bilingual AI/LLM Glossary

> 一份中英双语的 AI 大模型术语表（LLM Glossary），系统收录 130+ 个核心术语，覆盖大语言模型（Large Language Model）的基础概念、模型架构、预训练与后训练、微调（Fine-tuning / LoRA）、推理与部署（Inference）、Prompt 工程、RAG 检索增强生成、智能体（AI Agent / Function Calling / MCP）、多模态（Multimodal）、评估基准与 AI 安全对齐等关键领域。每个术语均提供中英对照名称、一句话定义与简明解释，适合开发者、研究者、产品经理与内容创作者快速查阅，也可作为 AI 工程与学习的基础参考。
>
> A bilingual (Chinese-English) glossary of 130+ essential terms on Large Language Models (LLMs) and Generative AI. It covers core concepts, model architecture (Transformer, Attention, MoE), pre-training and post-training (RLHF, DPO), fine-tuning (SFT, LoRA, QLoRA, PEFT), inference and deployment (quantization, KV Cache, vLLM), prompt engineering, Retrieval-Augmented Generation (RAG), AI Agents (tool use, Function Calling, MCP), multimodal models, evaluation benchmarks, and AI safety & alignment. Each entry provides a one-sentence definition followed by a concise explanation, designed as a reliable reference for developers, researchers, and AI practitioners.

**关键词 / Keywords**：大模型、LLM、大语言模型、生成式 AI、智能体、Agent、RAG、微调、LoRA、预训练、RLHF、推理、量化、Prompt Engineering、Transformer、多模态、向量数据库、MCP、AI 安全、Large Language Model、Generative AI、Machine Learning、Deep Learning

---

## 目录（Table of Contents）

- [基础概念（Fundamentals）](#基础概念fundamentals) — LLM、Token、上下文窗口、幻觉、涌现能力……
- [模型架构（Model Architecture）](#模型架构model-architecture) — Transformer、注意力机制、MoE、位置编码……
- [训练（Training）](#训练training) — 预训练、RLHF、DPO、损失函数、分布式训练……
- [微调与适配（Fine-tuning and Adaptation）](#微调与适配fine-tuning-and-adaptation) — SFT、LoRA、QLoRA、PEFT、蒸馏……
- [推理与部署（Inference and Deployment）](#推理与部署inference-and-deployment) — 量化、KV Cache、vLLM、GGUF、ONNX……
- [Prompt 工程（Prompt Engineering）](#prompt-工程prompt-engineering) — System Prompt、Few-shot、CoT、提示注入……
- [RAG 与检索（RAG and Retrieval）](#rag-与检索rag-and-retrieval) — Embedding、向量数据库、Chunking、重排序……
- [智能体（Agents）](#智能体agents) — Agent、Function Calling、MCP、ReAct、多智能体……
- [多模态（Multimodal）](#多模态multimodal) — VLM、文生图、文生视频、TTS、语音克隆……
- [评估与基准（Evaluation and Benchmarks）](#评估与基准evaluation-and-benchmarks) — MMLU、HumanEval、困惑度、基准污染……
- [安全与对齐（Safety and Alignment）](#安全与对齐safety-and-alignment) — 对齐、越狱、护栏、红队测试……
- [生态与工程（Ecosystem and Engineering）](#生态与工程ecosystem-and-engineering) — 开源模型、Hugging Face、Ollama、推理成本……
- [常见问题（FAQ）](#常见问题faq)

---

## 基础概念（Fundamentals）

### 大语言模型（LLM）
**英文**：Large Language Model (LLM) | **类别**：基础概念

大语言模型（LLM）是在海量文本数据上训练、拥有数十亿至数万亿参数的深度学习模型，能够理解和生成自然语言。

LLM 通常基于 [Transformer](#transformer) 架构，通过[预训练](#预训练pre-training)学习语言的统计规律，可完成对话、写作、翻译、编程、推理等多种任务。代表性模型包括 GPT 系列、Claude、Gemini、Llama、Qwen、DeepSeek 等。相关术语：[基础模型](#基础模型foundation-model)、[参数](#参数parameters)。

### Token（词元）
**英文**：Token | **类别**：基础概念

Token 是大模型处理文本的最小单位，可以是一个字、一个词、一个子词片段或一个标点符号。

主流模型通过 BPE（Byte Pair Encoding）等分词算法将文本切分为 Token：英文中 1 个 Token 约对应 0.75 个单词，中文通常 1–2 个汉字对应 1 个 Token。模型的计费、上下文长度限制均以 Token 为单位。相关术语：[上下文窗口](#上下文窗口context-window)。

### 参数（Parameters）
**英文**：Parameters | **类别**：基础概念

参数是神经网络中通过训练学习得到的数值权重，决定模型对输入的响应方式。

参数规模是衡量模型能力的重要指标之一，常以 B（十亿）为单位，如 7B、70B、405B。一般而言参数越多模型容量越大，但训练数据质量、架构设计同样关键，小参数模型经过高质量训练也可超越大模型。相关术语：[Scaling Law](#scaling-law扩展定律)、[模型权重](#模型权重model-weights)。

### 上下文窗口（Context Window）
**英文**：Context Window | **类别**：基础概念

上下文窗口是模型单次推理时能够处理的最大 Token 数量，包括输入与输出。

上下文窗口决定了模型能"记住"多少对话历史或文档内容，主流模型的窗口从 8K 扩展到 128K、1M 甚至更长。超出窗口的内容会被截断或遗忘，长文档处理常需配合 [RAG](#rag检索增强生成) 等技术。相关术语：[Token](#token词元)、[KV Cache](#kv-cache键值缓存)。

### 涌现能力（Emergent Abilities）
**英文**：Emergent Abilities | **类别**：基础概念

涌现能力是指模型规模扩大到一定程度后突然出现、在小模型中不存在的能力。

典型例子包括上下文学习（In-context Learning）、思维链推理等：当参数量或训练量跨过某个阈值，模型在特定任务上的表现会从随机水平跃升至可用水平。这一现象是 [Scaling Law](#scaling-law扩展定律) 研究的重要课题，其本质和可预测性仍在争论中。

### 幻觉（Hallucination）
**英文**：Hallucination | **类别**：基础概念

幻觉是指大模型生成看似合理但事实上错误或无依据内容的现象。

幻觉源于模型基于统计概率生成文本而非检索事实，常见表现包括编造参考文献、虚构事件、错误引用数据等。缓解手段包括 [RAG](#rag检索增强生成)、引用溯源、降低[温度](#温度temperature)与事实核查，但目前无法彻底消除。

### 基础模型（Foundation Model）
**英文**：Foundation Model | **类别**：基础概念

基础模型是在大规模数据上预训练、可通过微调适配多种下游任务的通用模型。

该概念由斯坦福大学于 2021 年提出，强调这类模型是构建各类应用的"地基"：同一个基础模型可以衍生出对话、代码、写作等无数专用模型。[LLM](#大语言模型llm) 是基础模型在语言领域的代表，此外还有视觉、音频等模态的基础模型。

### 生成式人工智能（Generative AI）
**英文**：Generative AI | **类别**：基础概念

生成式 AI 是能够生成文本、图像、音频、视频等新内容的人工智能技术总称。

与分类、预测等判别式 AI 不同，生成式 AI 学习数据的分布并据此创造新样本。[LLM](#大语言模型llm) 是生成式 AI 在文本模态的核心形态，图像领域的代表则是[扩散模型](#扩散模型diffusion-model)。

### 通用人工智能（AGI）
**英文**：Artificial General Intelligence (AGI) | **类别**：基础概念

通用人工智能（AGI）是指在所有认知任务上达到或超过人类平均水平、可自主泛化到未知领域的人工智能。

AGI 目前尚未实现，也没有公认的判定标准。大模型展现出的跨任务泛化能力被部分研究者视为 AGI 的早期迹象，但在长期规划、可靠推理、持续学习等方面仍有明显差距。

### 温度（Temperature）
**英文**：Temperature | **类别**：基础概念

温度是控制大模型生成随机性的采样参数，取值通常在 0 到 2 之间。

温度越低，模型越倾向于选择概率最高的词，输出更确定、更保守；温度越高，输出越多样但也更可能偏离事实。事实性任务建议低温度（如 0–0.3），创意写作可适当调高。相关术语：[Top-p](#top-p核采样)、[采样](#采样sampling)。

### Top-p（核采样）
**英文**：Top-p (Nucleus Sampling) | **类别**：基础概念

Top-p 是一种采样策略，模型只从累计概率达到阈值 p 的最小候选词集合中抽样。

例如 p=0.9 表示只考虑概率累计前 90% 的词。Top-p 能动态调整候选集大小，比固定候选数量的 Top-k 更灵活，常与[温度](#温度temperature)配合使用以平衡输出的质量与多样性。

### 采样（Sampling）
**英文**：Sampling | **类别**：基础概念

采样是模型根据输出的概率分布选择下一个 Token 的过程。

常见策略包括贪心解码（总选概率最高者）、随机采样、Top-k、Top-p 与集束搜索（Beam Search）。采样策略直接影响生成文本的质量、多样性与可复现性，是推理阶段的重要调参手段。

---

## 模型架构（Model Architecture）

### Transformer
**英文**：Transformer | **类别**：模型架构

Transformer 是 2017 年 Google 在论文《Attention Is All You Need》中提出的神经网络架构，是当前几乎所有大模型的基础。

其核心是[自注意力机制](#自注意力self-attention)，可并行处理整个序列，解决了 RNN 难以并行化和长程依赖的问题。现代 LLM 多采用其[解码器架构](#解码器架构decoder-only-architecture)变体。相关术语：[多头注意力](#多头注意力multi-head-attention)、[位置编码](#位置编码positional-encoding)。

### 注意力机制（Attention Mechanism）
**英文**：Attention Mechanism | **类别**：模型架构

注意力机制是让模型在处理序列时动态关注不同位置信息的计算方法。

它通过查询（Query）、键（Key）、值（Value）三个向量计算相关性权重，使模型能捕获词语之间的长距离依赖关系。注意力机制是 [Transformer](#transformer) 的核心，也衍生出多种高效变体以降低计算开销。

### 自注意力（Self-Attention）
**英文**：Self-Attention | **类别**：模型架构

自注意力是注意力机制的一种形式，序列中的每个位置都与同一序列的所有位置计算关联权重。

它使模型无需递归即可建模任意两个词之间的关系，计算可完全并行。其计算复杂度随序列长度呈平方增长，这是长上下文场景的主要瓶颈，催生了 FlashAttention 等优化技术。相关术语：[KV Cache](#kv-cache键值缓存)。

### 多头注意力（Multi-Head Attention）
**英文**：Multi-Head Attention (MHA) | **类别**：模型架构

多头注意力是将注意力计算拆分为多个并行的"头"，各自学习不同类型的关联模式。

不同头可关注语法、指代、语义等不同维度的信息，拼接后显著增强模型表达能力。后续出现了 MQA、GQA 等共享键值的变体，用于降低推理时的显存占用。相关术语：[KV Cache](#kv-cache键值缓存)。

### 混合专家模型（MoE）
**英文**：Mixture of Experts (MoE) | **类别**：模型架构

MoE 是一种将模型拆分为多个"专家"子网络、每次只激活其中一部分的架构设计。

通过门控网络（Router）为每个 Token 选择 Top-k 个专家，MoE 可以在总参数量巨大的同时保持较低的推理计算量。Mixtral、DeepSeek-V3、Qwen3 等模型均采用 MoE 架构。相关术语：[参数](#参数parameters)。

### 位置编码（Positional Encoding）
**英文**：Positional Encoding | **类别**：模型架构

位置编码是为序列中每个 Token 注入位置信息的技术，弥补注意力机制本身不感知顺序的缺陷。

早期 Transformer 使用正弦函数编码，现代模型普遍采用旋转位置编码（RoPE）或 ALiBi 等方案，它们对长序列外推更友好。位置编码的设计直接影响模型的长上下文能力。

### 层归一化（Layer Normalization）
**英文**：Layer Normalization | **类别**：模型架构

层归一化是对神经网络每层的输出进行标准化、使训练更稳定的技术。

它将每层激活值归一到均值 0、方差 1 附近，缓解梯度消失与内部协变量偏移问题。现代 LLM 多采用其简化变体 RMSNorm，并将归一化层置于子层之前（Pre-Norm）以提升深层模型的训练稳定性。

### 残差连接（Residual Connection）
**英文**：Residual Connection | **类别**：模型架构

残差连接是将层的输入直接加到输出上（y = F(x) + x）的结构设计。

它为梯度提供了一条"高速公路"，使上百层的深层网络也能稳定训练，是 Transformer 及现代深度网络的标配组件。相关术语：[梯度下降](#梯度下降gradient-descent)。

### 词嵌入（Embedding）
**英文**：Embedding | **类别**：模型架构

词嵌入是将离散的 Token 映射为连续稠密向量、使其可被神经网络处理的表示方法。

语义相近的词在嵌入空间中距离也相近，这一特性不仅用于模型输入层，也支撑了[语义搜索](#语义搜索semantic-search)与 [RAG](#rag检索增强生成) 中的文本向量表示。相关术语：[向量数据库](#向量数据库vector-database)。

### 解码器架构（Decoder-only Architecture）
**英文**：Decoder-only Architecture | **类别**：模型架构

解码器架构是仅使用 Transformer 解码器堆叠、以自回归方式逐个生成 Token 的模型结构。

GPT 系列、Llama、Qwen 等主流生成式 LLM 均采用该架构，因其天然适合下一个词预测任务且便于统一预训练目标。与之相对的是 BERT 式的纯编码器架构和 T5 式的编码器-解码器架构。

### 编码器-解码器架构（Encoder-Decoder Architecture）
**英文**：Encoder-Decoder Architecture | **类别**：模型架构

编码器-解码器架构由编码器理解输入序列、解码器生成输出序列两部分组成。

该架构最早用于机器翻译（T5、BART 为代表），适合输入输出结构差异大的任务。在纯生成任务上它已被[解码器架构](#解码器架构decoder-only-architecture)超越，但在翻译、摘要等场景仍有应用。

---

## 训练（Training）

### 预训练（Pre-training）
**英文**：Pre-training | **类别**：训练

预训练是在海量无标注文本上以自监督方式训练模型、使其掌握通用语言能力的第一阶段训练。

其核心目标是"下一个 Token 预测"，模型通过预测海量语料中的下一个词学习语法、知识与初步推理能力。预训练消耗绝大部分算力（常需数千张 GPU 运行数月），产出的基座模型再经[后训练](#后训练post-training)对齐人类偏好。相关术语：[基础模型](#基础模型foundation-model)、[Scaling Law](#scaling-law扩展定律)。

### 后训练（Post-training）
**英文**：Post-training | **类别**：训练

后训练是在预训练完成之后、让模型对齐人类意图与偏好的系列训练阶段的总称。

后训练通常包括[指令微调](#指令微调instruction-tuning)（SFT）、[RLHF](#rlhf人类反馈强化学习) 或 [DPO](#dpo直接偏好优化) 等步骤，把"只会续写文本"的基座模型变成"能听懂指令"的对话助手。近年来后训练还扩展出强化推理能力（Reasoning RL）等新范式。

### RLHF（人类反馈强化学习）
**英文**：Reinforcement Learning from Human Feedback (RLHF) | **类别**：训练

RLHF 是利用人类偏好数据训练奖励模型、再用强化学习优化语言模型输出质量的对齐方法。

典型流程为：收集人类对多个回答的排序 → 训练奖励模型（Reward Model）→ 用 PPO 等算法微调模型使其获得更高奖励。RLHF 是 ChatGPT 等对话模型效果飞跃的关键，但流程复杂、训练不稳定，部分场景已被 [DPO](#dpo直接偏好优化) 替代。相关术语：[对齐](#对齐alignment)。

### DPO（直接偏好优化）
**英文**：Direct Preference Optimization (DPO) | **类别**：训练

DPO 是一种无需训练奖励模型、直接在偏好数据对上优化语言模型的对齐算法。

它将 RLHF 的强化学习问题转化为简单的二分类损失，训练更稳定、实现更简单，已成为开源社区最主流的对齐方法之一。其变体包括 IPO、KTO、ORPO 等。相关术语：[RLHF](#rlhf人类反馈强化学习)、[损失函数](#损失函数loss-function)。

### 损失函数（Loss Function）
**英文**：Loss Function | **类别**：训练

损失函数是量化模型预测与真实目标之间差距、为参数更新提供方向的数学函数。

语言模型预训练普遍使用交叉熵损失（Cross-Entropy Loss），衡量预测分布与真实 Token 分布的差异。训练过程本质上就是通过[梯度下降](#梯度下降gradient-descent)不断最小化损失函数。

### 梯度下降（Gradient Descent）
**英文**：Gradient Descent | **类别**：训练

梯度下降是沿损失函数梯度的反方向迭代更新参数、以最小化损失的优化算法。

实际训练中采用其随机版本（SGD）及 Adam、AdamW 等自适应变体，每次用一小批数据（mini-batch）估算梯度。梯度经反向传播（Backpropagation）计算，配合[学习率](#学习率learning-rate)控制更新步长。相关术语：[残差连接](#残差连接residual-connection)。

### 学习率（Learning Rate）
**英文**：Learning Rate | **类别**：训练

学习率是控制每次参数更新步长的超参数，是训练中最重要的超参数之一。

学习率过大会导致训练震荡甚至发散，过小则收敛缓慢。大模型训练普遍采用预热（Warmup）加余弦衰减的调度策略，预训练学习率通常在 1e-4 量级，微调时更小。相关术语：[梯度下降](#梯度下降gradient-descent)。

### 数据清洗（Data Cleaning）
**英文**：Data Cleaning | **类别**：训练

数据清洗是对训练语料进行去重、过滤低质内容、去除有害信息等预处理的过程。

业界共识是"数据质量决定模型上限"：去重（Deduplication）可防止模型记忆重复片段，质量过滤能显著提升下游表现。主流做法结合规则、分类器与困惑度打分构建清洗流水线，数据配比（Data Mixture）同样是核心机密。

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

在[全参微调](#全参微调full-parameter-fine-tuning)中尤为明显：用垂直领域数据微调后，模型的通用对话能力可能显著退化。缓解方法包括混合通用数据回放、降低学习率，或使用 [LoRA](#lora低秩自适应) 等只更新少量参数的方法。

### Scaling Law（扩展定律）
**英文**：Scaling Law | **类别**：训练

Scaling Law 是描述模型性能随参数量、数据量和计算量增长呈幂律改善的经验规律。

OpenAI（2020）与 DeepMind 的 Chinchilla 论文（2022）奠定了该领域基础：Chinchilla 指出模型参数量与训练 Token 数应按约 1:20 的比例同步扩展才算"计算最优"。Scaling Law 指导着大模型的资源配置，但[涌现能力](#涌现能力emergent-abilities)的出现说明幂律之外仍存在突变。

---

## 微调与适配（Fine-tuning and Adaptation）

### 监督微调（SFT）
**英文**：Supervised Fine-Tuning (SFT) | **类别**：微调与适配

监督微调（SFT）是用"指令-回答"格式的标注数据对预训练模型进行有监督训练的过程。

SFT 是[后训练](#后训练post-training)的第一步，让基座模型学会遵循指令、以对话形式作答。数据质量远比数量重要，数千条高质量样本（如 LIMA 论文所示）即可获得良好效果。相关术语：[指令微调](#指令微调instruction-tuning)、[RLHF](#rlhf人类反馈强化学习)。

### LoRA（低秩自适应）
**英文**：Low-Rank Adaptation (LoRA) | **类别**：微调与适配

LoRA 是一种冻结原模型权重、仅训练低秩矩阵来近似参数增量的高效微调方法。

它将权重更新分解为两个小矩阵的乘积，可训练参数量通常不到全模型的 1%，显存需求大幅降低且不会破坏原模型能力。训练得到的 LoRA 权重可与基座合并或按需插拔，是开源社区最流行的微调方案。相关术语：[PEFT](#peft参数高效微调)、[QLoRA](#qlora量化低秩微调)。

### QLoRA（量化低秩微调）
**英文**：Quantized Low-Rank Adaptation (QLoRA) | **类别**：微调与适配

QLoRA 是将基座模型量化为 4-bit 后再进行 LoRA 微调、进一步降低显存占用的技术。

通过 NF4 量化、双重量化与分页优化器，QLoRA 使单张消费级显卡（24GB 显存）即可微调 65B 级模型，而效果接近 16-bit 全量微调。相关术语：[量化](#量化quantization)、[LoRA](#lora低秩自适应)。

### PEFT（参数高效微调）
**英文**：Parameter-Efficient Fine-Tuning (PEFT) | **类别**：微调与适配

PEFT 是只更新模型一小部分参数即可完成微调的一类方法的总称。

代表方法包括 [LoRA](#lora低秩自适应)、[Adapter](#adapter适配器)、[提示微调](#提示微调prompt-tuning)、Prefix Tuning 等。相比[全参微调](#全参微调full-parameter-fine-tuning)，PEFT 显著降低算力门槛、便于多任务权重管理，并有效缓解[灾难性遗忘](#灾难性遗忘catastrophic-forgetting)。

### 全参微调（Full-Parameter Fine-Tuning）
**英文**：Full-Parameter Fine-Tuning | **类别**：微调与适配

全参微调是在微调阶段更新模型全部参数的训练方式。

它能最大程度地让模型适配新任务，效果上限通常高于 PEFT 方法，但显存开销巨大（7B 模型全参微调约需 80GB 以上显存），且更容易发生[灾难性遗忘](#灾难性遗忘catastrophic-forgetting)。相关术语：[SFT](#监督微调sft)。

### 知识蒸馏（Distillation）
**英文**：Knowledge Distillation | **类别**：微调与适配

知识蒸馏是用大模型（教师）的输出训练小模型（学生）、将能力迁移到更小模型的技术。

学生模型学习教师模型的输出分布（软标签）而非硬标签，能以远小于教师的参数量逼近其表现。DeepSeek-R1 蒸馏系列、Gemma 等均是蒸馏的典型应用，是模型小型化的核心手段。相关术语：[量化](#量化quantization)。

### 指令微调（Instruction Tuning）
**英文**：Instruction Tuning | **类别**：微调与适配

指令微调是用多样化的"指令-响应"数据训练模型、使其学会遵循人类指令的微调方式。

它与 [SFT](#监督微调sft) 在实践中基本同义，强调训练数据以任务指令形式组织。FLAN 等研究证明，覆盖任务类型越广，模型对未见指令的泛化能力越强。相关术语：[后训练](#后训练post-training)。

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

常见路径包括领域继续预训练（Continued Pre-training）、领域 [SFT](#监督微调sft) 与 [RAG](#rag检索增强生成) 外挂知识库。选择微调还是 RAG 取决于需要注入的是"能力与风格"还是"事实与知识"。相关术语：[灾难性遗忘](#灾难性遗忘catastrophic-forgetting)。

### 模型合并（Model Merging）
**英文**：Model Merging | **类别**：微调与适配

模型合并是将多个同源微调模型的权重直接加权融合、获得兼具各方能力的新模型的技术。

常见方法包括简单平均、SLERP 球面插值、Task Arithmetic 与 TIES-Merging 等。合并无需训练算力，是开源社区低成本"炼制"强模型的流行玩法，但要求参与合并的模型共享同一基座。

---

## 推理与部署（Inference and Deployment）

### 量化（Quantization）
**英文**：Quantization | **类别**：推理与部署

量化是将模型权重和激活值从 FP16/BF16 高精度压缩为 INT8、INT4 等低精度表示的技术。

量化可将显存占用降至原来的 1/2 甚至 1/4，并提升推理速度，代价是轻微精度损失。主流方案有 GPTQ、AWQ、GGUF 的 k-quants 等，按阶段分为训练后量化（PTQ）与量化感知训练（QAT）。相关术语：[GGUF](#gguf)、[QLoRA](#qlora量化低秩微调)。

### KV Cache（键值缓存）
**英文**：KV Cache | **类别**：推理与部署

KV Cache 是在自回归生成时缓存历史 Token 的 Key/Value 向量、避免重复计算注意力的高效推理技术。

没有 KV Cache，每生成一个 Token 都要重算整个序列的注意力，复杂度无法接受。KV Cache 的显存占用随序列长度和并发数线性增长，是长上下文推理的主要瓶颈，催生了 PagedAttention、GQA 等优化。相关术语：[vLLM](#vllm)、[自注意力](#自注意力self-attention)。

### vLLM
**英文**：vLLM | **类别**：推理与部署

vLLM 是伯克利开源的高吞吐量大模型推理与服务框架，以 PagedAttention 技术著称。

PagedAttention 借鉴操作系统虚拟内存的分页思想管理 [KV Cache](#kv-cache键值缓存)，将显存浪费从 60% 以上降至 4% 以内，配合连续批处理可使吞吐提升数倍。vLLM 支持主流开源模型与 OpenAI 兼容 API，是生产环境部署的事实标准之一。

### 批处理（Batching）
**英文**：Batching | **类别**：推理与部署

批处理是将多个推理请求合并为一个批次并行计算、提升 GPU 利用率的技术。

静态批处理等待凑满固定批次，存在延迟浪费；连续批处理（Continuous Batching）在 Token 级别动态调度，请求完成即插入新请求，显著提升吞吐。批大小是[延迟](#延迟latency)与[吞吐](#吞吐throughput)权衡的核心旋钮。

### 延迟（Latency）
**英文**：Latency | **类别**：推理与部署

延迟是模型从接收请求到返回结果所需的时间，是推理服务的核心体验指标。

生成式场景通常细分为首 Token 延迟（TTFT，受预填充阶段影响）和每个输出 Token 的间隔（TPOT/ITL，受解码速度影响）。降低延迟的手段包括[量化](#量化quantization)、[投机解码](#投机解码speculative-decoding)、算子融合等。相关术语：[吞吐](#吞吐throughput)。

### 吞吐（Throughput）
**英文**：Throughput | **类别**：推理与部署

吞吐是推理系统单位时间内处理的 Token 数或请求数，衡量服务的整体产能。

提高吞吐主要靠增大批处理规模与提升显存利用率，但会牺牲单请求[延迟](#延迟latency)。衡量成本时常用"每百万 Token 成本"这一与吞吐直接相关的指标。相关术语：[推理成本](#推理成本inference-cost)。

### GGUF
**英文**：GGUF | **类别**：推理与部署

GGUF 是 llama.cpp 项目定义的单文件模型格式，专为 CPU 与消费级设备上的量化推理设计。

一个 GGUF 文件包含模型权重、分词器与元数据，支持从 Q2 到 Q8 的多种量化等级。它取代了早期的 GGML 格式，配合 [Ollama](#ollama)、LM Studio 等工具成为本地运行大模型的主流格式。相关术语：[量化](#量化quantization)。

### ONNX
**英文**：ONNX (Open Neural Network Exchange) | **类别**：推理与部署

ONNX 是一种开放的神经网络模型交换格式，使模型可在不同框架与硬件之间迁移。

PyTorch、TensorFlow 训练的模型可导出为 ONNX，再通过 ONNX Runtime、TensorRT 等引擎在各类硬件上高效推理。它是模型工程化部署的重要中间层，广泛用于跨平台与边缘场景。相关术语：[边缘部署](#边缘部署edge-deployment)。

### 投机解码（Speculative Decoding）
**英文**：Speculative Decoding | **类别**：推理与部署

投机解码是用小模型快速草拟多个候选 Token、再由大模型一次性并行验证的推理加速技术。

由于验证可以并行，原本逐个生成的过程被批量完成，在不改变输出分布的前提下实现 2–3 倍加速。相关变体包括 Medusa、EAGLE 与自投机解码。相关术语：[延迟](#延迟latency)。

### 模型并行（Model Parallelism）
**英文**：Model Parallelism | **类别**：推理与部署

模型并行是将单个模型切分到多张 GPU 上共同承载、以突破单卡显存限制的技术。

推理场景常用张量并行（把每层切开）与流水线并行（把层按段分到不同卡）。多卡间通信开销会降低效率，因此部署时需在单卡[量化](#量化quantization)与多卡并行之间权衡。相关术语：[分布式训练](#分布式训练distributed-training)。

### 边缘部署（Edge Deployment）
**英文**：Edge Deployment | **类别**：推理与部署

边缘部署是将模型直接运行在手机、PC、嵌入式设备等终端上而非云端的部署方式。

端侧推理带来低延迟、离线可用与数据隐私优势，典型技术栈包括 llama.cpp、[GGUF](#gguf)、Core ML 与 [ONNX](#onnx) Runtime。小型化手段（[蒸馏](#知识蒸馏distillation)、[量化](#量化quantization)）是边缘部署的前提。

### PagedAttention
**英文**：PagedAttention | **类别**：推理与部署

PagedAttention 是将 KV Cache 按固定大小的"页"管理、借鉴虚拟内存思想的注意力优化算法。

它消除了连续显存预留带来的碎片与浪费，使显存利用率接近最优，是 [vLLM](#vllm) 高吞吐的核心技术。类似思想也被 TensorRT-LLM、SGLang 等推理框架广泛采用。相关术语：[KV Cache](#kv-cache键值缓存)。

---

## Prompt 工程（Prompt Engineering）

### 提示工程（Prompt Engineering）
**英文**：Prompt Engineering | **类别**：Prompt 工程

提示工程是通过设计和优化输入文本（Prompt）来引导大模型产生期望输出的实践方法。

它不改变模型权重，仅通过指令、示例、格式约束与上下文组织来激发模型能力，是成本最低的模型优化手段。常见技巧包括 [Few-shot](#few-shot少样本提示)、[CoT](#cot思维链)、[角色设定](#角色设定role-playing) 与结构化输出约束。

### System Prompt（系统提示词）
**英文**：System Prompt | **类别**：Prompt 工程

System Prompt 是在对话开始前设定模型行为准则、角色与边界的高优先级指令。

它在消息层级中优先级高于用户输入，用于定义助手的人格、输出格式、安全边界与业务规则。设计良好的 System Prompt 是企业级应用稳定输出的基础，也是[提示注入](#提示注入prompt-injection)攻击的主要目标。

### Few-shot（少样本提示）
**英文**：Few-shot Prompting | **类别**：Prompt 工程

Few-shot 是在提示中提供少量输入输出示例、让模型通过上下文学习任务模式的方法。

模型无需更新权重即可"照猫画虎"，这是[涌现能力](#涌现能力emergent-abilities)中上下文学习的直接应用。示例的代表性与顺序都会显著影响效果，示例通常以 2–8 个为宜。相关术语：[Zero-shot](#zero-shot零样本)。

### Zero-shot（零样本）
**英文**：Zero-shot | **类别**：Prompt 工程

Zero-shot 是不提供任何示例、仅依靠指令直接让模型完成任务的方式。

经过[指令微调](#指令微调instruction-tuning)的现代模型已具备较强的零样本泛化能力，大多数日常任务无需示例即可完成。当零样本效果不佳时，可升级为 [Few-shot](#few-shot少样本提示) 或考虑微调。

### CoT（思维链）
**英文**：Chain-of-Thought (CoT) | **类别**：Prompt 工程

思维链是引导模型在给出答案前先逐步写出推理过程的提示技巧。

在提示中加入"让我们一步步思考"（Let's think step by step）即可显著提升数学与逻辑推理任务的表现。该思想进一步演化为 o1/R1 类推理模型的长思维链训练范式。相关术语：[思维树](#思维树tree-of-thoughts-tot)、[自我一致性](#自我一致性self-consistency)。

### 提示注入（Prompt Injection）
**英文**：Prompt Injection | **类别**：Prompt 工程

提示注入是通过精心构造的输入诱导模型忽略原有指令、执行攻击者意图的攻击手法。

当模型处理不可信内容（网页、邮件、文档）时，攻击者可嵌入"忽略之前的指令"等恶意指令，窃取 [System Prompt](#system-prompt系统提示词) 或操纵 [Agent](#智能体agent) 行为。防御手段包括输入隔离、权限最小化与输出审计。相关术语：[越狱](#越狱jailbreak)、[护栏](#护栏guardrails)。

### 角色设定（Role-playing）
**英文**：Role-playing | **类别**：Prompt 工程

角色设定是在提示中为模型指定特定身份（如"你是一位资深律师"）以约束输出风格与专业度的技巧。

角色会激活模型训练中与该身份相关的知识与表达模式，从而提升垂直领域回答的专业性。角色设定常与 [System Prompt](#system-prompt系统提示词) 结合，构成应用层提示的基础骨架。

### 提示模板（Prompt Template）
**英文**：Prompt Template | **类别**：Prompt 工程

提示模板是将提示中固定结构与动态变量分离、便于程序化复用的工程化组件。

模板通过占位符注入用户输入、检索结果与历史对话，保证输出格式稳定并便于版本管理。LangChain、LlamaIndex 等框架均提供模板抽象，是提示从"手工调优"走向"工程管理"的标志。

### 思维树（Tree of Thoughts, ToT）
**英文**：Tree of Thoughts (ToT) | **类别**：Prompt 工程

思维树是让模型同时探索多条推理路径、以树状结构搜索最优解的推理框架。

相比 [CoT](#cot思维链) 的单线推理，ToT 在每个节点生成多个候选思路并评估剪枝，类似人类的"头脑风暴+回溯"。它显著提升复杂规划类任务表现，代价是成倍增加的推理开销。相关术语：[规划](#规划planning)。

### 自我一致性（Self-Consistency）
**英文**：Self-Consistency | **类别**：Prompt 工程

自我一致性是对同一问题采样多条思维链、再以多数投票确定最终答案的推理增强方法。

它基于"正确推理路径会收敛到相同答案"的假设，用少量额外算力换取准确率的稳定提升。常与 [CoT](#cot思维链) 和较高的[温度](#温度temperature)配合使用。

### 结构化输出（Structured Output）
**英文**：Structured Output | **类别**：Prompt 工程

结构化输出是约束模型按预定义格式（如 JSON Schema）返回结果的技术。

主流模型提供 JSON Mode 或 Function Calling 级别的格式保证，推理框架则通过约束解码（Constrained Decoding）强制输出合法语法。它是 LLM 接入程序化系统的关键能力，避免脆弱的文本解析。相关术语：[Function Calling](#function-calling函数调用)。

---

## RAG 与检索（RAG and Retrieval）

### RAG（检索增强生成）
**英文**：Retrieval-Augmented Generation (RAG) | **类别**：RAG 与检索

RAG 是在生成前先从外部知识库检索相关内容、再将其注入提示让模型据以作答的技术架构。

RAG 让模型回答有出处、知识可实时更新，是缓解[幻觉](#幻觉hallucination)与突破训练数据时效限制的主流方案。典型流程为：[Embedding](#embedding嵌入) 入库 → 检索 → [重排序](#重排序reranking) → 拼入提示生成。相关术语：[向量数据库](#向量数据库vector-database)、[Chunking](#chunking文本切分)。

### Embedding（嵌入）
**英文**：Embedding | **类别**：RAG 与检索

Embedding 是将文本、图像等内容映射为高维稠密向量、使语义相似度可用距离计算的表示技术。

在 RAG 中，文档与用户问题被同一嵌入模型编码，语义相近者向量距离更近。主流嵌入模型包括 OpenAI text-embedding 系列、BGE、E5 等，选型直接影响检索质量。相关术语：[语义搜索](#语义搜索semantic-search)、[余弦相似度](#余弦相似度cosine-similarity)。

### 向量数据库（Vector Database）
**英文**：Vector Database | **类别**：RAG 与检索

向量数据库是专门存储和高效检索高维向量的数据库系统。

它通过 HNSW、IVF 等近似最近邻（ANN）索引在毫秒级从百万级向量中找出最相似结果。代表产品有 Pinecone、Milvus、Qdrant、Weaviate、pgvector 等，是 [RAG](#rag检索增强生成) 系统的标准组件。相关术语：[Embedding](#embedding嵌入)。

### Chunking（文本切分）
**英文**：Chunking | **类别**：RAG 与检索

Chunking 是将长文档切分为较小片段以便嵌入与检索的预处理步骤。

切分策略直接影响检索质量：块太大噪声多，块太小丢失上下文。常见策略包括固定长度+重叠、按语义/段落切分、递归切分与父子块（Parent-Child）结构，典型块大小为 200–500 Token。相关术语：[RAG](#rag检索增强生成)。

### 重排序（Reranking）
**英文**：Reranking | **类别**：RAG 与检索

重排序是对初步检索结果用更精确的模型重新打分排序、提升相关性的后处理步骤。

向量检索追求召回速度，Cross-Encoder 类重排模型（如 BGE-Reranker、Cohere Rerank）则对"查询-文档"对精细打分，可将 Top-K 准确率显著提升。它是生产级 [RAG](#rag检索增强生成) 提升效果的性价比最高的环节之一。

### 混合检索（Hybrid Search）
**英文**：Hybrid Search | **类别**：RAG 与检索

混合检索是同时结合向量语义检索与关键词检索（BM25）、融合两者结果的检索策略。

向量检索擅长语义匹配但对专有名词、编号不敏感，关键词检索恰好互补；结果通常用 RRF（Reciprocal Rank Fusion）等算法融合。混合检索已成为企业级搜索与 [RAG](#rag检索增强生成) 的默认配置。

### 余弦相似度（Cosine Similarity）
**英文**：Cosine Similarity | **类别**：RAG 与检索

余弦相似度是通过计算两个向量夹角余弦值衡量其方向相似程度的度量。

取值范围为 -1 到 1，越接近 1 语义越相似，且不受向量长度影响，是文本 [Embedding](#embedding嵌入) 检索最常用的度量。欧氏距离与点积也是常见替代方案。

### 召回率（Recall）
**英文**：Recall | **类别**：RAG 与检索

召回率是检索系统成功找到的相关文档占全部相关文档的比例。

在 RAG 中，召回不足意味着关键知识根本没进入模型视野，生成再好也无法弥补。实践中常在召回阶段放宽 Top-K（如取 20–50 条），再用[重排序](#重排序reranking)精选，兼顾召回率与精确率。

### 语义搜索（Semantic Search）
**英文**：Semantic Search | **类别**：RAG 与检索

语义搜索是基于内容含义而非字面关键词匹配进行检索的搜索方式。

它将查询与文档都编码为 [Embedding](#embedding嵌入)，通过向量距离找到语义最相关的结果，能处理同义表达与跨语言检索。语义搜索是 [RAG](#rag检索增强生成) 检索环节的技术基础。

### 知识库（Knowledge Base）
**英文**：Knowledge Base | **类别**：RAG 与检索

知识库是为模型提供外部事实来源、经过结构化整理的数据集合。

在 LLM 应用中，知识库通常由文档经 [Chunking](#chunking文本切分)、[Embedding](#embedding嵌入) 后存入[向量数据库](#向量数据库vector-database)构建而成。知识库的覆盖率、新鲜度与切分质量直接决定 RAG 系统的上限。

### HyDE（假设性文档嵌入）
**英文**：Hypothetical Document Embeddings (HyDE) | **类别**：RAG 与检索

HyDE 是先让模型生成一段假设性答案、再用该答案的向量去检索真实文档的检索增强技巧。

它把"问题检索文档"转化为"答案检索文档"，缩小了查询与文档间的语义鸿沟，对短查询和零样本场景提升明显。代价是多一次生成调用的延迟。相关术语：[RAG](#rag检索增强生成)。

---

## 智能体（Agents）

### 智能体（Agent）
**英文**：Agent | **类别**：智能体

智能体是以大模型为决策核心、能自主感知环境、规划步骤并调用工具完成复杂任务的 AI 系统。

与单次问答不同，Agent 具备"观察—思考—行动"的循环能力，可拆解目标、调用搜索/代码/数据库等工具并根据反馈调整策略。典型框架包括 [ReAct](#react)、AutoGPT 及各类编码 Agent（如 Claude Code、Cursor）。相关术语：[工具调用](#工具调用tool-use)、[规划](#规划planning)、[记忆](#记忆memory)。

### 工具调用（Tool Use）
**英文**：Tool Use | **类别**：智能体

工具调用是大模型在推理过程中调用外部函数、API 或系统以获取信息或执行操作的能力。

LLM 本身无法访问实时数据或执行动作，工具调用补上了这一短板：模型输出结构化的调用请求，由运行时执行后将结果回传模型继续推理。它是 [Agent](#智能体agent) 与现实世界交互的基础。相关术语：[Function Calling](#function-calling函数调用)、[MCP](#mcp模型上下文协议)。

### Function Calling（函数调用）
**英文**：Function Calling | **类别**：智能体

Function Calling 是模型按预定义的函数签名生成结构化参数、请求宿主程序执行对应函数的能力。

开发者以 JSON Schema 描述可用函数，模型在需要时输出函数名与参数，执行结果再回传给模型。它把"让模型说话"变成"让模型办事"，是构建 [Agent](#智能体agent) 与应用集成的标准机制。相关术语：[结构化输出](#结构化输出structured-output)。

### MCP（模型上下文协议）
**英文**：Model Context Protocol (MCP) | **类别**：智能体

MCP 是 Anthropic 于 2024 年提出的开放协议，用于标准化大模型应用与外部数据源、工具之间的连接方式。

MCP 采用客户端-服务器架构：工具与数据提供方实现 MCP Server，模型应用作为 MCP Client 按统一协议发现与调用能力，避免为每对"应用×工具"重复造轮子。它已被 OpenAI、Google 及众多开发工具采纳，正成为 [Agent](#智能体agent) 生态的通用接口标准。

### ReAct
**英文**：ReAct (Reasoning + Acting) | **类别**：智能体

ReAct 是将推理（Reasoning）与行动（Acting）交织进行、让模型"边想边做"的智能体范式。

模型按"Thought → Action → Observation"循环工作：先推理下一步，再调用工具，再观察结果继续推理，直到任务完成。ReAct 显著提升了复杂任务的可解释性与成功率，是现代 [Agent](#智能体agent) 框架的奠基性工作。

### 多智能体（Multi-Agent）
**英文**：Multi-Agent System | **类别**：智能体

多智能体系统是由多个分工不同的 Agent 协作、通过消息传递共同完成复杂任务的架构。

常见模式包括"规划者-执行者-评审者"分工、辩论式多视角求解与层级化团队。代表框架有 AutoGen、CrewAI、MetaGPT 等。多智能体能突破单 Agent 上下文与角色的限制，但也带来协调成本与错误传播问题。相关术语：[工作流编排](#工作流编排workflow-orchestration)。

### 规划（Planning）
**英文**：Planning | **类别**：智能体

规划是 Agent 将复杂目标拆解为可执行子任务序列、并在执行中动态调整的能力。

常见技术包括任务分解（Task Decomposition）、[思维树](#思维树tree-of-thoughts-tot)搜索与"规划-执行-再规划"循环。规划质量是区分 Agent 能力强弱的关键维度，也是当前大模型推理研究的重点方向。相关术语：[反思](#反思reflection)。

### 记忆（Memory）
**英文**：Memory | **类别**：智能体

记忆是 Agent 跨轮次、跨会话保存与调用信息的机制，使其具备持续上下文与个性化能力。

记忆通常分为短期记忆（当前会话的[上下文窗口](#上下文窗口context-window)内信息）与长期记忆（持久化到向量库或结构化存储、按需检索注入）。MemGPT、Mem0 等项目专门研究记忆管理。相关术语：[RAG](#rag检索增强生成)。

### 反思（Reflection）
**英文**：Reflection | **类别**：智能体

反思是 Agent 对自身输出进行评估、发现错误并迭代改进的自我修正机制。

典型模式如 Reflexion：Agent 在失败后生成文字版"复盘"存入记忆，指导下一轮尝试。反思能以纯推理时计算换取显著的成功率提升，是 [Agent](#智能体agent) 可靠性工程的重要手段。相关术语：[自我一致性](#自我一致性self-consistency)。

### 自主性（Autonomy）
**英文**：Autonomy | **类别**：智能体

自主性是 Agent 在无人类逐步干预下连续决策与执行的程度。

自主级别从"每步需人类确认"（Copilot 模式）到"完全自主执行"（AutoGPT 模式）不等。实际产品需在自主性与可控性之间权衡：关键操作（支付、删除、发送）通常保留人类审批节点（Human-in-the-loop）。相关术语：[护栏](#护栏guardrails)。

### 工作流编排（Workflow Orchestration）
**英文**：Workflow Orchestration | **类别**：智能体

工作流编排是用预定义的流程图或状态机组织多个 LLM 调用与工具节点的工程方法。

与完全自主的 [Agent](#智能体agent) 不同，编排式工作流的控制流由开发者显式定义，模型只负责节点内的智能决策，因而更可控、更易测试。LangGraph、Dify、Coze 等平台均以此为核心范式。

---

## 多模态（Multimodal）

### 多模态模型（Multimodal Model）
**英文**：Multimodal Model | **类别**：多模态

多模态模型是能同时处理两种及以上数据模态（文本、图像、音频、视频等）的 AI 模型。

它通过共享的表示空间打通不同模态，实现"看图说话""听音写稿"等跨模态理解与生成。GPT-4o、Gemini、Qwen-VL 等已将多模态能力作为标配。相关术语：[VLM](#vlm视觉语言模型)、[多模态对齐](#多模态对齐multimodal-alignment)。

### VLM（视觉语言模型）
**英文**：Vision-Language Model (VLM) | **类别**：多模态

VLM 是能将图像与文本联合理解、支持以文图混合输入进行问答与推理的模型。

典型结构由视觉编码器（如 ViT）+ 投影层 + 语言模型组成，视觉特征被映射为语言模型可理解的"视觉 Token"。代表模型有 GPT-4V、Qwen-VL、LLaVA 等，广泛应用于文档理解、GUI 操作与具身智能。相关术语：[CLIP](#clip)、[图像理解](#图像理解image-understanding)。

### 文生图（Text-to-Image）
**英文**：Text-to-Image | **类别**：多模态

文生图是根据文本描述自动生成对应图像的生成式 AI 技术。

主流方案以[扩散模型](#扩散模型diffusion-model)为核心（Stable Diffusion、DALL·E、Midjourney、FLUX），近年来自回归与混合架构也在兴起。提示词设计、参考图控制与风格一致性是该领域的核心实践问题。

### 文生视频（Text-to-Video）
**英文**：Text-to-Video | **类别**：多模态

文生视频是根据文本描述自动生成连续视频片段的生成式 AI 技术。

Sora、Veo、可灵（Kling）、Runway 等模型采用扩散 Transformer（DiT）等架构，在时空维度上建模运动规律。当前挑战包括长时一致性、物理合理性与生成成本。相关术语：[扩散模型](#扩散模型diffusion-model)。

### TTS（文本转语音）
**英文**：Text-to-Speech (TTS) | **类别**：多模态

TTS 是将书面文本转换为自然语音的技术，是语音交互系统的输出端。

现代神经 TTS（如 VITS、XTTS、GPT-SoVITS）已能生成接近真人的韵律与情感，并支持流式输出以满足实时对话需求。相关术语：[语音克隆](#语音克隆voice-cloning)。

### 语音克隆（Voice Cloning）
**英文**：Voice Cloning | **类别**：多模态

语音克隆是仅凭少量参考音频复制特定人声音色、并用其合成任意文本语音的技术。

当前模型最短仅需数秒样本即可实现高相似度克隆，广泛用于配音、有声内容与个性化助手。该技术同时带来伪造与欺诈风险，多数平台要求声纹授权与水印溯源。相关术语：[TTS](#tts文本转语音)、[内容审核](#内容审核content-moderation)。

### 多模态对齐（Multimodal Alignment）
**英文**：Multimodal Alignment | **类别**：多模态

多模态对齐是将不同模态的数据映射到统一语义空间、使跨模态内容可相互对应的技术。

[CLIP](#clip) 通过对比学习让"狗的图片"与文本"a dog"在向量空间接近，是多模态对齐的里程碑。对齐质量决定 VLM 的跨模态理解上限。相关术语：[Embedding](#embedding嵌入)。

### 扩散模型（Diffusion Model）
**英文**：Diffusion Model | **类别**：多模态

扩散模型是通过逐步向数据加噪再学习逆向去噪过程来生成样本的生成模型。

它是 Stable Diffusion、DALL·E 2/3、Sora 等图像与视频生成系统的核心， latent diffusion（在压缩潜空间扩散）大幅降低了计算成本。与自回归 LLM 的逐 Token 生成形成对照。相关术语：[文生图](#文生图text-to-image)。

### CLIP
**英文**：CLIP (Contrastive Language-Image Pre-training) | **类别**：多模态

CLIP 是 OpenAI 于 2021 年提出的通过对比学习联合训练图像与文本编码器的模型。

它在 4 亿图文对上训练，使图像与描述文本在共享向量空间中对齐，具备强大的零样本图像分类能力。CLIP 的图像编码器被广泛复用于 [VLM](#vlm视觉语言模型) 与文生图的文本条件编码。相关术语：[多模态对齐](#多模态对齐multimodal-alignment)。

### 图像理解（Image Understanding）
**英文**：Image Understanding | **类别**：多模态

图像理解是模型对图像内容进行识别、描述、问答与推理的能力总称。

它涵盖物体识别、场景理解、图表解读、文档 OCR 式问答等任务，是 [VLM](#vlm视觉语言模型) 的核心能力维度，也是自动驾驶、医疗影像等应用的基础。相关术语：[OCR](#ocr光学字符识别)。

### OCR（光学字符识别）
**英文**：Optical Character Recognition (OCR) | **类别**：多模态

OCR 是将图像中的印刷或手写文字识别并转换为可编辑文本的技术。

传统 OCR 依赖检测+识别两阶段流水线，现代多模态大模型已能端到端理解复杂版面、表格与公式，使"截图即数据"成为可能。相关术语：[图像理解](#图像理解image-understanding)。

---

## 评估与基准（Evaluation and Benchmarks）

### 基准测试（Benchmark）
**英文**：Benchmark | **类别**：评估与基准

基准测试是用标准化数据集与指标衡量并横向比较不同模型能力的评测体系。

它为模型选型与学术比较提供量化依据，但任何单一基准都无法覆盖真实使用体验，需结合多基准、[Elo 评分](#elo-评分elo-rating)与业务实测综合判断。相关术语：[MMLU](#mmlu)、[基准污染](#基准污染benchmark-contamination)。

### MMLU
**英文**：Massive Multitask Language Understanding (MMLU) | **类别**：评估与基准

MMLU 是涵盖 57 个学科（数学、法律、医学、历史等）的多选题知识基准，是衡量模型知识与推理能力的权威测试之一。

成绩以准确率计，顶级模型已超过 85%。随着基准趋于饱和，社区推出了更难的 MMLU-Pro 与 GPQA 等继任测试。相关术语：[基准污染](#基准污染benchmark-contamination)。

### HumanEval
**英文**：HumanEval | **类别**：评估与基准

HumanEval 是 OpenAI 发布的代码生成基准，包含 164 道手写 Python 编程题，以生成代码能否通过单元测试（pass@k）为指标。

它避免了选择题式评测的猜测成分，直接检验"代码能跑"。SWE-bench 等更贴近真实工程的基准正成为代码能力评测的新标准。相关术语：[基准测试](#基准测试benchmark)。

### 困惑度（Perplexity）
**英文**：Perplexity (PPL) | **类别**：评估与基准

困惑度是衡量语言模型对一段文本预测不确定程度的指标，数值越低表示模型拟合越好。

它等于交叉熵损失的指数，可直观理解为模型在预测下一个词时平均"犹豫"于多少个候选。困惑度常用于预训练质量监控与文本流畅度评估，但不直接反映下游任务表现。相关术语：[损失函数](#损失函数loss-function)。

### 基准污染（Benchmark Contamination）
**英文**：Benchmark Contamination | **类别**：评估与基准

基准污染是基准测试题目泄漏进训练数据、导致评测分数虚高而非真实能力的现象。

由于大模型训练数据来自公开网络，热门基准几乎不可避免地被"见过"。检测手段包括 n-gram 重叠分析与动态更新题库，解读模型分数时应警惕污染带来的夸大。相关术语：[过拟合](#过拟合overfitting)。

### GSM8K
**英文**：GSM8K | **类别**：评估与基准

GSM8K 是包含 8500 道小学数学应用题的基准，用于评估模型的多步算术推理能力。

该基准的崛起直接推动了 [CoT](#cot思维链) 等推理技术流行，顶级模型准确率已超过 95%，更难的 MATH、AIME 基准成为新的分水岭。相关术语：[基准测试](#基准测试benchmark)。

### Elo 评分（Elo Rating）
**英文**：Elo Rating | **类别**：评估与基准

Elo 评分是借自棋类排名、通过模型间两两对战结果计算相对强弱的评分体系。

Chatbot Arena（LMArena）让真人用户盲测两个匿名模型的回答并投票，据此计算 Elo 分，成为最受关注的综合能力榜单之一。它反映人类偏好而非绝对能力，可能偏向"回答长而自信"的模型。相关术语：[人工评估](#人工评估human-evaluation)。

### 人工评估（Human Evaluation）
**英文**：Human Evaluation | **类别**：评估与基准

人工评估是由人类标注员直接对模型输出质量进行打分的评测方式。

开放式生成（摘要、对话、创意写作）缺乏可靠的自动指标，人工评估仍是金标准，但成本高、一致性难保证。实践中常以 GPT 级模型作"裁判"（LLM-as-a-Judge）近似人工评估以降低成本。相关术语：[Elo 评分](#elo-评分elo-rating)。

### BLEU 与 ROUGE
**英文**：BLEU / ROUGE | **类别**：评估与基准

BLEU 与 ROUGE 是基于 n-gram 重叠度衡量生成文本与参考文本相似度的经典自动评估指标。

BLEU 主要用于机器翻译，ROUGE 主要用于文本摘要。它们计算快速但只衡量字面重合，无法评价语义正确性，在大模型时代仅作参考，逐渐被模型裁判与人工评估取代。相关术语：[人工评估](#人工评估human-evaluation)。

### 泛化能力（Generalization）
**英文**：Generalization | **类别**：评估与基准

泛化能力是模型将训练中学到的规律应用到未见过的新样本、新任务上的能力。

泛化是机器学习的根本目标，也是区分"记住答案"与"真正理解"的试金石。[指令微调](#指令微调instruction-tuning)的核心价值即在于提升对未见指令的泛化，而[基准污染](#基准污染benchmark-contamination)会制造虚假泛化。相关术语：[过拟合](#过拟合overfitting)。

---

## 安全与对齐（Safety and Alignment）

### 对齐（Alignment）
**英文**：Alignment | **类别**：安全与对齐

对齐是让 AI 系统的行为符合人类意图、价值观与安全规范的研究与工程方向。

技术上主要通过 [SFT](#监督微调sft)、[RLHF](#rlhf人类反馈强化学习)、[DPO](#dpo直接偏好优化) 与[宪法 AI](#宪法-aiconstitutional-ai) 实现；广义对齐还关注长期问题——如何确保远超人类的系统依然可控。对齐与能力是大模型发展的两条并行主线。

### 越狱（Jailbreak）
**英文**：Jailbreak | **类别**：安全与对齐

越狱是通过精心构造的提示绕过模型安全限制、诱使其生成被禁止内容的攻击行为。

常见手法包括角色扮演虚构场景、编码混淆、多轮诱导与"奶奶漏洞"式情感操控。越狱与防御是一场持续攻防，厂商通过安全训练与[护栏](#护栏guardrails)缓解，但无法完全杜绝。相关术语：[提示注入](#提示注入prompt-injection)、[红队测试](#红队测试red-teaming)。

### 护栏（Guardrails）
**英文**：Guardrails | **类别**：安全与对齐

护栏是部署在模型输入输出两侧、拦截违规内容与越权行为的安全过滤层。

护栏可以是分类器、规则引擎或专门的安全模型（如 Llama Guard），覆盖有害内容、PII 泄露、提示注入等风险。对 [Agent](#智能体agent) 系统，护栏还包括操作权限控制与人工审批节点。相关术语：[内容审核](#内容审核content-moderation)。

### 红队测试（Red Teaming）
**英文**：Red Teaming | **类别**：安全与对齐

红队测试是模拟攻击者主动寻找模型安全漏洞、在发布前暴露风险的对抗性评估方法。

红队由人类专家与自动化攻击模型共同组成，覆盖[越狱](#越狱jailbreak)、偏见、隐私泄露、危险能力等维度。主流实验室已将红队测试纳入模型发布流程，部分司法辖区（如欧盟 AI 法案）将其作为合规要求。

### 有害内容（Harmful Content）
**英文**：Harmful Content | **类别**：安全与对齐

有害内容是模型输出中可能造成现实伤害的内容，包括暴力教唆、歧视言论、虚假信息、恶意代码等。

有害内容的边界因文化、法律与场景而异，是[内容审核](#内容审核content-moderation)与[对齐](#对齐alignment)共同处理的对象。评估通常结合安全基准与人工抽检。相关术语：[偏见](#偏见bias)。

### 偏见（Bias）
**英文**：Bias | **类别**：安全与对齐

偏见是模型从训练数据中习得并放大的系统性倾向，涉及性别、种族、地域、文化等维度。

偏见会导致招聘筛选不公、刻板印象输出等现实危害。缓解手段包括训练数据去偏、对齐阶段修正与评测监控，但完全消除偏见在技术上尚无定论，透明披露与人工监督仍是必要补充。

### 隐私泄露（Privacy Leakage）
**英文**：Privacy Leakage | **类别**：安全与对齐

隐私泄露是模型在输出中重现训练数据里的个人信息（PII）或机密内容的风险。

研究表明大模型会记忆训练语料中的邮箱、电话乃至代码密钥，可被针对性攻击提取。防御包括训练数据脱敏、差分隐私训练与输出侧 PII 过滤。应用层还需防止用户数据经 API 外传。相关术语：[护栏](#护栏guardrails)。

### 可解释性（Interpretability）
**英文**：Interpretability | **类别**：安全与对齐

可解释性是研究神经网络内部表征与决策机制、让"黑箱"模型变得可理解的方向。

机制可解释性（Mechanistic Interpretability）尝试定位具体神经元与回路的功能，Anthropic 等机构已能用稀疏自编码器提取大模型的可解释特征。可解释性被普遍认为是实现可靠[对齐](#对齐alignment)的科学基础。

### 宪法 AI（Constitutional AI）
**英文**：Constitutional AI | **类别**：安全与对齐

宪法 AI 是 Anthropic 提出的对齐方法，让模型依据一组成文原则（"宪法"）自我批评并修正输出。

它先用原则引导模型自我改进生成无害数据，再结合 RLAIF（AI 反馈强化学习）训练，减少对人工有害标注的依赖。该方法使安全原则可显式审阅与迭代，是 [RLHF](#rlhf人类反馈强化学习) 的重要演进。

### 内容审核（Content Moderation）
**英文**：Content Moderation | **类别**：安全与对齐

内容审核是对用户输入与模型输出进行合规检查、拦截违规内容的产品化安全机制。

实现方式包括审核 API（如 OpenAI Moderation）、自建分类器与关键词规则的组合，通常置于生成前后两道关口。它与[护栏](#护栏guardrails)共同构成 AI 应用合规运营的底座。相关术语：[有害内容](#有害内容harmful-content)。

---

## 生态与工程（Ecosystem and Engineering）

### 开源模型（Open-Source / Open-Weight Model）
**英文**：Open-Source / Open-Weight Model | **类别**：生态与工程

开源模型是公开模型权重、允许下载与本地部署的模型，严格说多数为"开放权重"（Open-Weight）模型。

代表系列有 Llama、Qwen、DeepSeek、Mistral、GLM 等。开放权重使私有化部署、微调定制与学术研究成为可能，但其[许可证](#许可证license)常附带商用限制，使用前需仔细核对。相关术语：[模型权重](#模型权重model-weights)、[Hugging Face](#hugging-face)。

### API（应用程序接口）
**英文**：API (Application Programming Interface) | **类别**：生态与工程

API 是模型服务商提供的程序化调用接口，开发者经 HTTP 请求即可获得模型能力而无需自建基础设施。

OpenAI 兼容 API 已成为事实标准，主流厂商与推理框架均支持该格式，便于在不同供应商间切换。使用 API 需关注[推理成本](#推理成本inference-cost)、[速率限制](#速率限制rate-limit)与数据合规。

### 推理成本（Inference Cost）
**英文**：Inference Cost | **类别**：生态与工程

推理成本是模型运行阶段产生的算力开销，通常按每百万 Token（输入/输出分开计价）核算。

输入 Token 一般比输出便宜数倍，[提示缓存](#提示缓存prompt-caching)可进一步降低重复前缀的费用。成本优化手段包括模型分级路由（简单问题给小模型）、[量化](#量化quantization)、批处理与缓存。相关术语：[吞吐](#吞吐throughput)。

### Hugging Face
**英文**：Hugging Face | **类别**：生态与工程

Hugging Face 是最大的开源 AI 模型与数据集托管平台，被称为"AI 界的 GitHub"。

它托管超过百万个模型权重、数据集与演示应用（Spaces），其 Transformers、Datasets、PEFT 等开源库是事实上的行业标准工具链。模型卡（Model Card）与排行榜（Open LLM Leaderboard）是选型的重要参考。相关术语：[开源模型](#开源模型open-source--open-weight-model)。

### Ollama
**英文**：Ollama | **类别**：生态与工程

Ollama 是在个人电脑上一键下载和运行开源大模型的本地推理工具。

它基于 llama.cpp 封装，一条命令即可启动 [GGUF](#gguf) 格式的量化模型，并提供本地 API 供应用集成。Ollama 大幅降低了本地体验 LLM 的门槛，适合隐私敏感与离线场景。相关术语：[边缘部署](#边缘部署edge-deployment)。

### 模型权重（Model Weights）
**英文**：Model Weights | **类别**：生态与工程

模型权重是训练完成后模型全部参数的具体数值，以文件形式保存，是模型能力的物质载体。

加载权重即可复现模型行为，因此权重的开放与否决定模型能否私有化部署与二次开发。权重文件常见格式有 Safetensors（安全、加载快）、PyTorch 的 .pt/.bin 与 [GGUF](#gguf)。相关术语：[参数](#参数parameters)。

### 许可证（License）
**英文**：License | **类别**：生态与工程

许可证是规定模型权重与代码可被如何使用、修改与商用的法律条款。

开源权重模型的许可证差异很大：Apache 2.0、MIT 最为宽松，Llama 社区许可证则对超大规模商用另有约定，部分模型仅限研究用途（如 CC-BY-NC）。商用选型前核查许可证是合规的必要步骤。相关术语：[开源模型](#开源模型open-source--open-weight-model)。

### MLOps / LLMOps
**英文**：MLOps / LLMOps | **类别**：生态与工程

LLMOps 是将大模型应用的开发、部署、监控与迭代流程工程化管理的实践体系。

它在传统 MLOps（数据版本、训练流水线、模型注册）基础上新增提示版本管理、评测集回归、幻觉与成本监控等环节。LangSmith、Weights & Biases、Langfuse 是常用工具。

### GPU 显存（VRAM）
**英文**：GPU VRAM | **类别**：生态与工程

显存是 GPU 上用于存放模型权重、中间激活与 KV Cache 的高速内存，是决定能运行多大模型的硬约束。

粗算规则：FP16 下每 10 亿参数约占 2GB 显存，7B 模型约需 14GB；[量化](#量化quantization)到 4-bit 可降至约 4GB。推理时还需为 [KV Cache](#kv-cache键值缓存) 预留空间，长上下文高并发场景显存压力倍增。相关术语：[模型并行](#模型并行model-parallelism)。

### 提示缓存（Prompt Caching）
**英文**：Prompt Caching | **类别**：生态与工程

提示缓存是缓存重复出现的提示前缀的计算结果、避免重复计费的推理优化机制。

当多次请求共享相同的长前缀（如固定 System Prompt 或知识库内容）时，缓存命中部分的费用与延迟可下降一个数量级。主流 API（Anthropic、OpenAI、DeepSeek 等）均已支持该能力。相关术语：[KV Cache](#kv-cache键值缓存)、[推理成本](#推理成本inference-cost)。

### 速率限制（Rate Limit）
**英文**：Rate Limit | **类别**：生态与工程

速率限制是 API 服务商对单位时间请求数（RPM）或 Token 数（TPM）设置的使用上限。

超限请求会收到 429 错误，应用需实现指数退避重试、请求队列与多 Key 负载均衡。企业级用量通常可申请提升配额。相关术语：[API](#api应用程序接口)。

---

## 常见问题（FAQ）

### 大模型和生成式 AI 有什么区别？
生成式 AI（Generative AI）是能够生成文本、图像、音频、视频等内容的 AI 技术总称；大模型（LLM，大语言模型）是生成式 AI 在文本模态的核心实现方式。换言之，LLM 属于生成式 AI，而生成式 AI 还包括文生图、文生视频等[多模态](#多模态multimodal)生成技术。

### RAG 和微调应该怎么选？
两者解决不同问题：[RAG](#rag检索增强生成) 用于注入"知识"——事实更新快、需要出处、数据量大的场景首选 RAG；[微调](#监督微调sft) 用于塑造"能力"——需要固定输出格式、专业语气或特定任务技能时选微调。实践中二者常结合使用：微调定风格，RAG 供事实。

### 大模型为什么会"一本正经地胡说八道"？
这种现象称为[幻觉](#幻觉hallucination)。模型本质上基于统计概率逐词生成文本，而非查询事实库，因此在知识盲区也会生成语法通顺但事实错误的内容。可通过 RAG、要求引用来源、降低[温度](#温度temperature)等方式缓解。

### 上下文窗口是不是越大越好？
不一定。[上下文窗口](#上下文窗口context-window)越大，能处理的文档越长，但注意力计算成本随之上升，且研究表明模型对超长上下文中部信息的利用率会下降（"lost in the middle"）。长文档场景通常用 [RAG](#rag检索增强生成) 精准检索比硬塞全文更高效。

### LoRA 微调和全参微调哪个效果更好？
[全参微调](#全参微调full-parameter-fine-tuning)上限略高，但[LoRA](#lora低秩自适应)在绝大多数任务上已能达到接近效果，且成本仅为前者的零头、不破坏原模型能力。数据量在百万级以下时 LoRA 通常是更优选择；超大规模领域继续训练才需要全参方案。

### 开源模型能商用吗？
取决于具体[许可证](#许可证license)。Qwen（部分）、Mistral 等采用 Apache 2.0 的可自由商用；Llama 系列采用社区许可证，月活超 7 亿的企业需另行授权；标注 CC-BY-NC 等条款的模型禁止商用。商用前务必逐条核对。

### 部署一个 7B 模型需要多少显存？
FP16 精度下约需 14–16GB 显存（权重约 14GB 加 [KV Cache](#kv-cache键值缓存) 开销）；4-bit [量化](#量化quantization)后约需 4–6GB，一张 RTX 3060 即可运行。可用 [Ollama](#ollama) 或 [vLLM](#vllm) 快速部署。

### 什么是 AI Agent，和普通聊天机器人有什么区别？
普通聊天机器人只进行"一问一答"的文本生成；[Agent](#智能体agent) 则具备"观察—思考—行动"循环，能自主拆解任务、[调用工具](#工具调用tool-use)（搜索、代码、数据库）、根据反馈修正策略，完成多步骤复杂任务。

### MCP 是做什么的？
[MCP](#mcp模型上下文协议)（Model Context Protocol）是连接 AI 应用与外部工具/数据源的开放标准协议。工具方实现一次 MCP Server，所有支持 MCP 的模型应用都能直接调用，避免了每对"应用×工具"重复开发集成，类似 AI 时代的 USB-C 接口。

### 如何防止 Prompt 被恶意注入或越狱？
单一手段无法根治，需纵深防御：将可信指令与不可信输入隔离、对检索内容进行安全扫描、为 [Agent](#智能体agent) 配置最小权限与人工审批节点、部署[护栏](#护栏guardrails)模型过滤输入输出，并定期进行[红队测试](#红队测试red-teaming)。

---

## 贡献（Contributing）

欢迎补充新术语或修正现有条目，请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可证（License）

本项目采用 [MIT License](LICENSE)，内容可自由使用、修改与分发。

---

*如果这份术语表对你有帮助，欢迎 Star 支持 / If you find this glossary useful, please consider giving it a star.*

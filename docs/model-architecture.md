# 模型架构 | Model Architecture

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录大模型架构相关的 11 个核心术语，包括 Transformer、注意力机制（Attention）、多头注意力、混合专家模型（MoE）、位置编码、层归一化与词嵌入等。
This page covers 11 core terms on LLM model architecture, including Transformer, Attention, Multi-Head Attention, Mixture of Experts (MoE), Positional Encoding, and Embeddings.

---

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

它使模型无需递归即可建模任意两个词之间的关系，计算可完全并行。其计算复杂度随序列长度呈平方增长，这是长上下文场景的主要瓶颈，催生了 FlashAttention 等优化技术。相关术语：[KV Cache](inference-deployment.md#kv-cache键值缓存)。

### 多头注意力（Multi-Head Attention）
**英文**：Multi-Head Attention (MHA) | **类别**：模型架构

多头注意力是将注意力计算拆分为多个并行的"头"，各自学习不同类型的关联模式。

不同头可关注语法、指代、语义等不同维度的信息，拼接后显著增强模型表达能力。后续出现了 MQA、GQA 等共享键值的变体，用于降低推理时的显存占用。相关术语：[KV Cache](inference-deployment.md#kv-cache键值缓存)。

### 混合专家模型（MoE）
**英文**：Mixture of Experts (MoE) | **类别**：模型架构

MoE 是一种将模型拆分为多个"专家"子网络、每次只激活其中一部分的架构设计。

通过门控网络（Router）为每个 Token 选择 Top-k 个专家，MoE 可以在总参数量巨大的同时保持较低的推理计算量。Mixtral、DeepSeek-V3、Qwen3 等模型均采用 MoE 架构。相关术语：[参数](basic-concepts.md#参数parameters)。

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

它为梯度提供了一条"高速公路"，使上百层的深层网络也能稳定训练，是 Transformer 及现代深度网络的标配组件。相关术语：[梯度下降](training.md#梯度下降gradient-descent)。

### 词嵌入（Embedding）
**英文**：Embedding | **类别**：模型架构

词嵌入是将离散的 Token 映射为连续稠密向量、使其可被神经网络处理的表示方法。

语义相近的词在嵌入空间中距离也相近，这一特性不仅用于模型输入层，也支撑了[语义搜索](rag-retrieval.md#语义搜索semantic-search)与 [RAG](rag-retrieval.md#rag检索增强生成) 中的文本向量表示。相关术语：[向量数据库](rag-retrieval.md#向量数据库vector-database)。

### 解码器架构（Decoder-only Architecture）
**英文**：Decoder-only Architecture | **类别**：模型架构

解码器架构是仅使用 Transformer 解码器堆叠、以自回归方式逐个生成 Token 的模型结构。

GPT 系列、Llama、Qwen 等主流生成式 LLM 均采用该架构，因其天然适合下一个词预测任务且便于统一预训练目标。与之相对的是 BERT 式的纯编码器架构和 T5 式的编码器-解码器架构。

### 编码器-解码器架构（Encoder-Decoder Architecture）
**英文**：Encoder-Decoder Architecture | **类别**：模型架构

编码器-解码器架构由编码器理解输入序列、解码器生成输出序列两部分组成。

该架构最早用于机器翻译（T5、BART 为代表），适合输入输出结构差异大的任务。在纯生成任务上它已被[解码器架构](#解码器架构decoder-only-architecture)超越，但在翻译、摘要等场景仍有应用。

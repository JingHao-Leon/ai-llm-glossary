# 基础概念 | Basic Concepts

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录 AI 大模型领域 12 个最基础的核心概念，包括大语言模型（LLM）、Token、参数、上下文窗口、涌现能力与幻觉等。
This page covers 12 fundamental concepts of Large Language Models (LLMs), including Tokens, Parameters, Context Window, Emergent Abilities, and Hallucination.

---

### 大语言模型（LLM）
**英文**：Large Language Model (LLM) | **类别**：基础概念

大语言模型（LLM）是在海量文本数据上训练、拥有数十亿至数万亿参数的深度学习模型，能够理解和生成自然语言。

LLM 通常基于 [Transformer](model-architecture.md#transformer) 架构，通过[预训练](training.md#预训练pre-training)学习语言的统计规律，可完成对话、写作、翻译、编程、推理等多种任务。代表性模型包括 GPT 系列、Claude、Gemini、Llama、Qwen、DeepSeek 等。相关术语：[基础模型](#基础模型foundation-model)、[参数](#参数parameters)。

### Token（词元）
**英文**：Token | **类别**：基础概念

Token 是大模型处理文本的最小单位，可以是一个字、一个词、一个子词片段或一个标点符号。

主流模型通过 BPE（Byte Pair Encoding）等分词算法将文本切分为 Token：英文中 1 个 Token 约对应 0.75 个单词，中文通常 1–2 个汉字对应 1 个 Token。模型的计费、上下文长度限制均以 Token 为单位。相关术语：[上下文窗口](#上下文窗口context-window)。

### 参数（Parameters）
**英文**：Parameters | **类别**：基础概念

参数是神经网络中通过训练学习得到的数值权重，决定模型对输入的响应方式。

参数规模是衡量模型能力的重要指标之一，常以 B（十亿）为单位，如 7B、70B、405B。一般而言参数越多模型容量越大，但训练数据质量、架构设计同样关键，小参数模型经过高质量训练也可超越大模型。相关术语：[Scaling Law](training.md#scaling-law扩展定律)、[模型权重](ecosystem-engineering.md#模型权重model-weights)。

### 上下文窗口（Context Window）
**英文**：Context Window | **类别**：基础概念

上下文窗口是模型单次推理时能够处理的最大 Token 数量，包括输入与输出。

上下文窗口决定了模型能"记住"多少对话历史或文档内容，主流模型的窗口从 8K 扩展到 128K、1M 甚至更长。超出窗口的内容会被截断或遗忘，长文档处理常需配合 [RAG](rag-retrieval.md#rag检索增强生成) 等技术。相关术语：[Token](#token词元)、[KV Cache](inference-deployment.md#kv-cache键值缓存)。

### 涌现能力（Emergent Abilities）
**英文**：Emergent Abilities | **类别**：基础概念

涌现能力是指模型规模扩大到一定程度后突然出现、在小模型中不存在的能力。

典型例子包括上下文学习（In-context Learning）、思维链推理等：当参数量或训练量跨过某个阈值，模型在特定任务上的表现会从随机水平跃升至可用水平。这一现象是 [Scaling Law](training.md#scaling-law扩展定律) 研究的重要课题，其本质和可预测性仍在争论中。

### 幻觉（Hallucination）
**英文**：Hallucination | **类别**：基础概念

幻觉是指大模型生成看似合理但事实上错误或无依据内容的现象。

幻觉源于模型基于统计概率生成文本而非检索事实，常见表现包括编造参考文献、虚构事件、错误引用数据等。缓解手段包括 [RAG](rag-retrieval.md#rag检索增强生成)、引用溯源、降低[温度](#温度temperature)与事实核查，但目前无法彻底消除。

### 基础模型（Foundation Model）
**英文**：Foundation Model | **类别**：基础概念

基础模型是在大规模数据上预训练、可通过微调适配多种下游任务的通用模型。

该概念由斯坦福大学于 2021 年提出，强调这类模型是构建各类应用的"地基"：同一个基础模型可以衍生出对话、代码、写作等无数专用模型。[LLM](#大语言模型llm) 是基础模型在语言领域的代表，此外还有视觉、音频等模态的基础模型。

### 生成式人工智能（Generative AI）
**英文**：Generative AI | **类别**：基础概念

生成式 AI 是能够生成文本、图像、音频、视频等新内容的人工智能技术总称。

与分类、预测等判别式 AI 不同，生成式 AI 学习数据的分布并据此创造新样本。[LLM](#大语言模型llm) 是生成式 AI 在文本模态的核心形态，图像领域的代表则是[扩散模型](multimodal.md#扩散模型diffusion-model)。

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

# AI 大模型术语表 | Bilingual AI/LLM Glossary

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Glossary Terms](https://img.shields.io/badge/Glossary_Terms-134-blue)](#分类导航categories)

> 一份开源的中英双语 AI 大模型术语表（LLM Glossary），收录 134 个核心术语，按 12 个分类组织，覆盖大语言模型（Large Language Model）的基础概念、模型架构（Transformer / MoE）、预训练与后训练（RLHF / DPO）、微调（Fine-tuning / LoRA / QLoRA）、推理与部署（Inference / 量化 / vLLM）、Prompt 工程、RAG 检索增强生成、智能体（AI Agent / Function Calling / MCP）、多模态（Multimodal / VLM）、评估基准与 AI 安全对齐等关键领域。每个术语提供中英对照名称、一句话定义与简明解释，适合开发者、研究者、产品经理与内容创作者快速查阅，也可作为 AI 工程与学习的基础参考。
>
> An open-source bilingual (Chinese-English) glossary of 134 essential terms on Large Language Models (LLMs) and Generative AI, organized into 12 categories: core concepts, model architecture (Transformer, MoE), pre-training and post-training (RLHF, DPO), fine-tuning (SFT, LoRA, QLoRA, PEFT), inference and deployment (quantization, KV Cache, vLLM), prompt engineering, Retrieval-Augmented Generation (RAG), AI Agents (tool use, Function Calling, MCP), multimodal models, evaluation benchmarks, and AI safety & alignment. Each entry provides a one-sentence definition followed by a concise explanation — a reliable reference for developers, researchers, and AI practitioners.

**关键词 / Keywords**：大模型、LLM、大语言模型、生成式 AI、智能体、Agent、RAG、微调、LoRA、预训练、RLHF、训练、推理、量化、Prompt Engineering、Transformer、多模态、向量数据库、MCP、AI 安全、Large Language Model、Generative AI、Machine Learning、Deep Learning

---

## 分类导航（Categories）

- [基础概念（Fundamentals）](docs/basic-concepts.md) — 12 个术语：LLM、Token、参数、上下文窗口、幻觉、涌现能力……
- [模型架构（Model Architecture）](docs/model-architecture.md) — 11 个术语：Transformer、注意力机制、MoE、位置编码……
- [训练（Training）](docs/training.md) — 12 个术语：预训练、RLHF、DPO、损失函数、分布式训练……
- [微调与适配（Fine-tuning and Adaptation）](docs/fine-tuning.md) — 11 个术语：SFT、LoRA、QLoRA、PEFT、蒸馏……
- [推理与部署（Inference and Deployment）](docs/inference-deployment.md) — 12 个术语：量化、KV Cache、vLLM、GGUF、ONNX……
- [Prompt 工程（Prompt Engineering）](docs/prompt-engineering.md) — 12 个术语：System Prompt、Zero-shot / One-shot / Few-shot、CoT、提示注入……
- [RAG 与检索（RAG and Retrieval）](docs/rag-retrieval.md) — 11 个术语：RAG、Embedding、向量数据库、Chunking、重排序……
- [智能体（Agents）](docs/agents.md) — 11 个术语：Agent、工具调用、Function Calling、MCP、ReAct……
- [多模态（Multimodal）](docs/multimodal.md) — 11 个术语：VLM、文生图、文生视频、TTS、语音克隆……
- [评估与基准（Evaluation and Benchmarks）](docs/evaluation-benchmarks.md) — 10 个术语：MMLU、HumanEval、困惑度、基准污染……
- [安全与对齐（Safety and Alignment）](docs/safety-alignment.md) — 10 个术语：对齐、越狱、护栏、红队测试……
- [生态与工程（Ecosystem and Engineering）](docs/ecosystem-engineering.md) — 11 个术语：开源模型、Hugging Face、Ollama、推理成本……

---

## 常见问题（FAQ）

### 大模型和生成式 AI 有什么区别？
生成式 AI（Generative AI）是能够生成文本、图像、音频、视频等内容的 AI 技术总称；大模型（LLM，大语言模型）是生成式 AI 在文本模态的核心实现方式。换言之，LLM 属于生成式 AI，而生成式 AI 还包括文生图、文生视频等[多模态](docs/multimodal.md)生成技术。

### RAG 和微调应该怎么选？
两者解决不同问题：[RAG](docs/rag-retrieval.md#rag检索增强生成) 用于注入"知识"——事实更新快、需要出处、数据量大的场景首选 RAG；[微调](docs/fine-tuning.md#监督微调sft) 用于塑造"能力"——需要固定输出格式、专业语气或特定任务技能时选微调。实践中二者常结合使用：微调定风格，RAG 供事实。

### 大模型为什么会"一本正经地胡说八道"？
这种现象称为[幻觉](docs/basic-concepts.md#幻觉hallucination)。模型本质上基于统计概率逐词生成文本，而非查询事实库，因此在知识盲区也会生成语法通顺但事实错误的内容。可通过 RAG、要求引用来源、降低[温度](docs/basic-concepts.md#温度temperature)等方式缓解。

### 上下文窗口是不是越大越好？
不一定。[上下文窗口](docs/basic-concepts.md#上下文窗口context-window)越大，能处理的文档越长，但注意力计算成本随之上升，且研究表明模型对超长上下文中部信息的利用率会下降（"lost in the middle"）。长文档场景通常用 [RAG](docs/rag-retrieval.md#rag检索增强生成) 精准检索比硬塞全文更高效。

### LoRA 微调和全参微调哪个效果更好？
[全参微调](docs/fine-tuning.md#全参微调full-parameter-fine-tuning)上限略高，但[LoRA](docs/fine-tuning.md#lora低秩自适应)在绝大多数任务上已能达到接近效果，且成本仅为前者的零头、不破坏原模型能力。数据量在百万级以下时 LoRA 通常是更优选择；超大规模领域继续训练才需要全参方案。

### 开源模型能商用吗？
取决于具体[许可证](docs/ecosystem-engineering.md#许可证license)。Qwen（部分）、Mistral 等采用 Apache 2.0 的可自由商用；Llama 系列采用社区许可证，月活超 7 亿的企业需另行授权；标注 CC-BY-NC 等条款的模型禁止商用。商用前务必逐条核对。

### 部署一个 7B 模型需要多少显存？
FP16 精度下约需 14–16GB 显存（权重约 14GB 加 [KV Cache](docs/inference-deployment.md#kv-cache键值缓存) 开销）；4-bit [量化](docs/inference-deployment.md#量化quantization)后约需 4–6GB，一张 RTX 3060 即可运行。可用 [Ollama](docs/ecosystem-engineering.md#ollama) 或 [vLLM](docs/inference-deployment.md#vllm) 快速部署。

### 什么是 AI Agent，和普通聊天机器人有什么区别？
普通聊天机器人只进行"一问一答"的文本生成；[Agent](docs/agents.md#智能体agent) 则具备"观察—思考—行动"循环，能自主拆解任务、[调用工具](docs/agents.md#工具调用tool-use)（搜索、代码、数据库）、根据反馈修正策略，完成多步骤复杂任务。

### MCP 是做什么的？
[MCP](docs/agents.md#mcp模型上下文协议)（Model Context Protocol）是连接 AI 应用与外部工具/数据源的开放标准协议。工具方实现一次 MCP Server，所有支持 MCP 的模型应用都能直接调用，避免了每对"应用×工具"重复开发集成，类似 AI 时代的 USB-C 接口。

### 如何防止 Prompt 被恶意注入或越狱？
单一手段无法根治，需纵深防御：将可信指令与不可信输入隔离、对检索内容进行安全扫描、为 [Agent](docs/agents.md#智能体agent) 配置最小权限与人工审批节点、部署[护栏](docs/safety-alignment.md#护栏guardrails)模型过滤输入输出，并定期进行[红队测试](docs/safety-alignment.md#红队测试red-teaming)。

---

## 贡献（Contributing）

欢迎补充新术语或修正现有条目，请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。
Contributions are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md) for the entry format.

## 许可证（License）

本项目采用 [MIT License](LICENSE)，内容可自由使用、修改与分发。
Released under the [MIT License](LICENSE).

---

*如果这份术语表对你有帮助，欢迎 Star 支持 / If you find this glossary useful, please consider giving it a star.*

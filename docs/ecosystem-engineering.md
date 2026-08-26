# 生态与工程 | Ecosystem & Engineering

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录大模型生态与工程相关的 11 个核心术语，包括开源模型、API、推理成本（Inference Cost）、Hugging Face、Ollama、模型权重（Model Weights）、许可证（License）与 GPU 显存等。
This page covers 11 core terms on the LLM ecosystem and engineering, including open-source models, APIs, inference cost, Hugging Face, Ollama, model weights, licenses, and GPU VRAM.

---

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

输入 Token 一般比输出便宜数倍，[提示缓存](#提示缓存prompt-caching)可进一步降低重复前缀的费用。成本优化手段包括模型分级路由（简单问题给小模型）、[量化](inference-deployment.md#量化quantization)、批处理与缓存。相关术语：[吞吐](inference-deployment.md#吞吐throughput)。

### Hugging Face
**英文**：Hugging Face | **类别**：生态与工程

Hugging Face 是最大的开源 AI 模型与数据集托管平台，被称为"AI 界的 GitHub"。

它托管超过百万个模型权重、数据集与演示应用（Spaces），其 Transformers、Datasets、PEFT 等开源库是事实上的行业标准工具链。模型卡（Model Card）与排行榜（Open LLM Leaderboard）是选型的重要参考。相关术语：[开源模型](#开源模型open-source--open-weight-model)。

### Ollama
**英文**：Ollama | **类别**：生态与工程

Ollama 是在个人电脑上一键下载和运行开源大模型的本地推理工具。

它基于 llama.cpp 封装，一条命令即可启动 [GGUF](inference-deployment.md#gguf) 格式的量化模型，并提供本地 API 供应用集成。Ollama 大幅降低了本地体验 LLM 的门槛，适合隐私敏感与离线场景。相关术语：[边缘部署](inference-deployment.md#边缘部署edge-deployment)。

### 模型权重（Model Weights）
**英文**：Model Weights | **类别**：生态与工程

模型权重是训练完成后模型全部参数的具体数值，以文件形式保存，是模型能力的物质载体。

加载权重即可复现模型行为，因此权重的开放与否决定模型能否私有化部署与二次开发。权重文件常见格式有 Safetensors（安全、加载快）、PyTorch 的 .pt/.bin 与 [GGUF](inference-deployment.md#gguf)。相关术语：[参数](basic-concepts.md#参数parameters)。

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

粗算规则：FP16 下每 10 亿参数约占 2GB 显存，7B 模型约需 14GB；[量化](inference-deployment.md#量化quantization)到 4-bit 可降至约 4GB。推理时还需为 [KV Cache](inference-deployment.md#kv-cache键值缓存) 预留空间，长上下文高并发场景显存压力倍增。相关术语：[模型并行](inference-deployment.md#模型并行model-parallelism)。

### 提示缓存（Prompt Caching）
**英文**：Prompt Caching | **类别**：生态与工程

提示缓存是缓存重复出现的提示前缀的计算结果、避免重复计费的推理优化机制。

当多次请求共享相同的长前缀（如固定 System Prompt 或知识库内容）时，缓存命中部分的费用与延迟可下降一个数量级。主流 API（Anthropic、OpenAI、DeepSeek 等）均已支持该能力。相关术语：[KV Cache](inference-deployment.md#kv-cache键值缓存)、[推理成本](#推理成本inference-cost)。

### 速率限制（Rate Limit）
**英文**：Rate Limit | **类别**：生态与工程

速率限制是 API 服务商对单位时间请求数（RPM）或 Token 数（TPM）设置的使用上限。

超限请求会收到 429 错误，应用需实现指数退避重试、请求队列与多 Key 负载均衡。企业级用量通常可申请提升配额。相关术语：[API](#api应用程序接口)。

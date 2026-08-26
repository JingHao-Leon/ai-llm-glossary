# 推理与部署 | Inference & Deployment

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录大模型推理与部署相关的 12 个核心术语，包括量化（Quantization）、KV Cache、vLLM、批处理、延迟（Latency）、吞吐（Throughput）、GGUF、ONNX 与投机解码等。
This page covers 12 core terms on LLM inference and deployment, including quantization, KV Cache, vLLM, batching, latency, throughput, GGUF, ONNX, and speculative decoding.

---

### 量化（Quantization）
**英文**：Quantization | **类别**：推理与部署

量化是将模型权重和激活值从 FP16/BF16 高精度压缩为 INT8、INT4 等低精度表示的技术。

量化可将显存占用降至原来的 1/2 甚至 1/4，并提升推理速度，代价是轻微精度损失。主流方案有 GPTQ、AWQ、GGUF 的 k-quants 等，按阶段分为训练后量化（PTQ）与量化感知训练（QAT）。相关术语：[GGUF](#gguf)、[QLoRA](fine-tuning.md#qlora量化低秩微调)。

### KV Cache（键值缓存）
**英文**：KV Cache | **类别**：推理与部署

KV Cache 是在自回归生成时缓存历史 Token 的 Key/Value 向量、避免重复计算注意力的高效推理技术。

没有 KV Cache，每生成一个 Token 都要重算整个序列的注意力，复杂度无法接受。KV Cache 的显存占用随序列长度和并发数线性增长，是长上下文推理的主要瓶颈，催生了 PagedAttention、GQA 等优化。相关术语：[vLLM](#vllm)、[自注意力](model-architecture.md#自注意力self-attention)。

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

提高吞吐主要靠增大批处理规模与提升显存利用率，但会牺牲单请求[延迟](#延迟latency)。衡量成本时常用"每百万 Token 成本"这一与吞吐直接相关的指标。相关术语：[推理成本](ecosystem-engineering.md#推理成本inference-cost)。

### GGUF
**英文**：GGUF | **类别**：推理与部署

GGUF 是 llama.cpp 项目定义的单文件模型格式，专为 CPU 与消费级设备上的量化推理设计。

一个 GGUF 文件包含模型权重、分词器与元数据，支持从 Q2 到 Q8 的多种量化等级。它取代了早期的 GGML 格式，配合 [Ollama](ecosystem-engineering.md#ollama)、LM Studio 等工具成为本地运行大模型的主流格式。相关术语：[量化](#量化quantization)。

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

推理场景常用张量并行（把每层切开）与流水线并行（把层按段分到不同卡）。多卡间通信开销会降低效率，因此部署时需在单卡[量化](#量化quantization)与多卡并行之间权衡。相关术语：[分布式训练](training.md#分布式训练distributed-training)。

### 边缘部署（Edge Deployment）
**英文**：Edge Deployment | **类别**：推理与部署

边缘部署是将模型直接运行在手机、PC、嵌入式设备等终端上而非云端的部署方式。

端侧推理带来低延迟、离线可用与数据隐私优势，典型技术栈包括 llama.cpp、[GGUF](#gguf)、Core ML 与 [ONNX](#onnx) Runtime。小型化手段（[蒸馏](fine-tuning.md#知识蒸馏distillation)、[量化](#量化quantization)）是边缘部署的前提。

### PagedAttention
**英文**：PagedAttention | **类别**：推理与部署

PagedAttention 是将 KV Cache 按固定大小的"页"管理、借鉴虚拟内存思想的注意力优化算法。

它消除了连续显存预留带来的碎片与浪费，使显存利用率接近最优，是 [vLLM](#vllm) 高吞吐的核心技术。类似思想也被 TensorRT-LLM、SGLang 等推理框架广泛采用。相关术语：[KV Cache](#kv-cache键值缓存)。

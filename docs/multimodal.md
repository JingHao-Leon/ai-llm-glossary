# 多模态 | Multimodal

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录多模态（Multimodal）相关的 12 个核心术语，包括视觉语言模型（VLM）、文生图（Text-to-Image）、文生视频（Text-to-Video）、ASR、TTS、语音克隆（Voice Cloning）、扩散模型与 CLIP 等。
This page covers 12 core terms on multimodal AI, including Vision-Language Models (VLM), text-to-image, text-to-video, ASR, TTS, voice cloning, diffusion models, and CLIP.

---

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



### ASR（自动语音识别）
**英文**：Automatic Speech Recognition (ASR) | **类别**：多模态

ASR 是将语音信号自动转写为文本的技术，是语音交互系统的输入端。

现代 ASR 以 Whisper 等端到端模型为代表，支持多语言并具备较强的抗噪能力，与大模型结合可实现实时字幕、会议纪要与语音指令理解。它与 [TTS](#tts文本转语音) 分别构成语音对话的"耳朵"与"嘴巴"。

### 语音克隆（Voice Cloning）
**英文**：Voice Cloning | **类别**：多模态

语音克隆是仅凭少量参考音频复制特定人声音色、并用其合成任意文本语音的技术。

当前模型最短仅需数秒样本即可实现高相似度克隆，广泛用于配音、有声内容与个性化助手。该技术同时带来伪造与欺诈风险，多数平台要求声纹授权与水印溯源。相关术语：[TTS](#tts文本转语音)、[内容审核](safety-alignment.md#内容审核content-moderation)。

### 多模态对齐（Multimodal Alignment）
**英文**：Multimodal Alignment | **类别**：多模态

多模态对齐是将不同模态的数据映射到统一语义空间、使跨模态内容可相互对应的技术。

[CLIP](#clip) 通过对比学习让"狗的图片"与文本"a dog"在向量空间接近，是多模态对齐的里程碑。对齐质量决定 VLM 的跨模态理解上限。相关术语：[Embedding](rag-retrieval.md#embedding嵌入)。

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

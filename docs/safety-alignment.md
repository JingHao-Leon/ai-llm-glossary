# 安全与对齐 | Safety & Alignment

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录 AI 安全与对齐相关的 12 个核心术语，包括对齐（Alignment）、越狱（Jailbreak）、护栏（Guardrails）、红队测试（Red Teaming）、深度伪造（Deepfake）、数据投毒（Data Poisoning）、偏见与宪法 AI 等。
This page covers 12 core terms on AI safety and alignment, including jailbreak, guardrails, red teaming, deepfake, data poisoning, bias, privacy leakage, and Constitutional AI.

---

### 对齐（Alignment）
**英文**：Alignment | **类别**：安全与对齐

对齐是让 AI 系统的行为符合人类意图、价值观与安全规范的研究与工程方向。

技术上主要通过 [SFT](fine-tuning.md#监督微调sft)、[RLHF](training.md#rlhf人类反馈强化学习)、[DPO](training.md#dpo直接偏好优化) 与[宪法 AI](#宪法-aiconstitutional-ai) 实现；广义对齐还关注长期问题——如何确保远超人类的系统依然可控。对齐与能力是大模型发展的两条并行主线。

### 越狱（Jailbreak）
**英文**：Jailbreak | **类别**：安全与对齐

越狱是通过精心构造的提示绕过模型安全限制、诱使其生成被禁止内容的攻击行为。

常见手法包括角色扮演虚构场景、编码混淆、多轮诱导与"奶奶漏洞"式情感操控。越狱与防御是一场持续攻防，厂商通过安全训练与[护栏](#护栏guardrails)缓解，但无法完全杜绝。相关术语：[提示注入](prompt-engineering.md#提示注入prompt-injection)、[红队测试](#红队测试red-teaming)。

### 护栏（Guardrails）
**英文**：Guardrails | **类别**：安全与对齐

护栏是部署在模型输入输出两侧、拦截违规内容与越权行为的安全过滤层。

护栏可以是分类器、规则引擎或专门的安全模型（如 Llama Guard），覆盖有害内容、PII 泄露、提示注入等风险。对 [Agent](agents.md#智能体agent) 系统，护栏还包括操作权限控制与人工审批节点。相关术语：[内容审核](#内容审核content-moderation)。

### 红队测试（Red Teaming）
**英文**：Red Teaming | **类别**：安全与对齐

红队测试是模拟攻击者主动寻找模型安全漏洞、在发布前暴露风险的对抗性评估方法。

红队由人类专家与自动化攻击模型共同组成，覆盖[越狱](#越狱jailbreak)、偏见、隐私泄露、危险能力等维度。主流实验室已将红队测试纳入模型发布流程，部分司法辖区（如欧盟 AI 法案）将其作为合规要求。

### 有害内容（Harmful Content）
**英文**：Harmful Content | **类别**：安全与对齐

有害内容是模型输出中可能造成现实伤害的内容，包括暴力教唆、歧视言论、虚假信息、恶意代码等。

有害内容的边界因文化、法律与场景而异，是[内容审核](#内容审核content-moderation)与[对齐](#对齐alignment)共同处理的对象。评估通常结合安全基准与人工抽检。相关术语：[偏见](#偏见bias)。



### 深度伪造（Deepfake）
**英文**：Deepfake | **类别**：安全与对齐

深度伪造是利用生成式 AI 合成足以乱真的人脸、声音或视频、冒充真实人物的伪造内容。

[文生图](multimodal.md#文生图text-to-image)、[文生视频](multimodal.md#文生视频text-to-video) 与语音克隆技术的进步大幅降低了伪造门槛，带来诈骗、谣言与名誉侵害等现实危害。防御手段包括生成内容水印、溯源标准（如 C2PA）与[内容审核](#内容审核content-moderation)，多国已立法要求对 AI 合成内容进行标识。
### 偏见（Bias）
**英文**：Bias | **类别**：安全与对齐

偏见是模型从训练数据中习得并放大的系统性倾向，涉及性别、种族、地域、文化等维度。

偏见会导致招聘筛选不公、刻板印象输出等现实危害。缓解手段包括训练数据去偏、对齐阶段修正与评测监控，但完全消除偏见在技术上尚无定论，透明披露与人工监督仍是必要补充。

### 隐私泄露（Privacy Leakage）
**英文**：Privacy Leakage | **类别**：安全与对齐

隐私泄露是模型在输出中重现训练数据里的个人信息（PII）或机密内容的风险。

研究表明大模型会记忆训练语料中的邮箱、电话乃至代码密钥，可被针对性攻击提取。防御包括训练数据脱敏、差分隐私训练与输出侧 PII 过滤。应用层还需防止用户数据经 API 外传。相关术语：[护栏](#护栏guardrails)。



### 数据投毒（Data Poisoning）
**英文**：Data Poisoning | **类别**：安全与对齐

数据投毒是攻击者向训练数据中恶意注入样本、使模型习得错误知识或后门行为的攻击手法。

由于[预训练](training.md#预训练pre-training)语料大量来自公开网络，攻击者可通过在网页中埋入特定内容影响模型输出，或在微调数据中植入触发词后门。防御依赖数据来源管控、异常样本检测与[红队测试](#红队测试red-teaming)验证。
### 可解释性（Interpretability）
**英文**：Interpretability | **类别**：安全与对齐

可解释性是研究神经网络内部表征与决策机制、让"黑箱"模型变得可理解的方向。

机制可解释性（Mechanistic Interpretability）尝试定位具体神经元与回路的功能，Anthropic 等机构已能用稀疏自编码器提取大模型的可解释特征。可解释性被普遍认为是实现可靠[对齐](#对齐alignment)的科学基础。

### 宪法 AI（Constitutional AI）
**英文**：Constitutional AI | **类别**：安全与对齐

宪法 AI 是 Anthropic 提出的对齐方法，让模型依据一组成文原则（"宪法"）自我批评并修正输出。

它先用原则引导模型自我改进生成无害数据，再结合 RLAIF（AI 反馈强化学习）训练，减少对人工有害标注的依赖。该方法使安全原则可显式审阅与迭代，是 [RLHF](training.md#rlhf人类反馈强化学习) 的重要演进。

### 内容审核（Content Moderation）
**英文**：Content Moderation | **类别**：安全与对齐

内容审核是对用户输入与模型输出进行合规检查、拦截违规内容的产品化安全机制。

实现方式包括审核 API（如 OpenAI Moderation）、自建分类器与关键词规则的组合，通常置于生成前后两道关口。它与[护栏](#护栏guardrails)共同构成 AI 应用合规运营的底座。相关术语：[有害内容](#有害内容harmful-content)。

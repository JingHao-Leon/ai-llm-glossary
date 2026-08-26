# Prompt 工程 | Prompt Engineering

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录 Prompt 工程（提示工程）相关的 11 个核心术语，包括 System Prompt（系统提示词）、Few-shot、Zero-shot、思维链（CoT）、提示注入（Prompt Injection）与结构化输出等。
This page covers 11 core terms on prompt engineering, including System Prompt, few-shot prompting, Chain-of-Thought (CoT), prompt injection, and structured output.

---

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

模型无需更新权重即可"照猫画虎"，这是[涌现能力](basic-concepts.md#涌现能力emergent-abilities)中上下文学习的直接应用。示例的代表性与顺序都会显著影响效果，示例通常以 2–8 个为宜。相关术语：[Zero-shot](#zero-shot零样本)。

### Zero-shot（零样本）
**英文**：Zero-shot | **类别**：Prompt 工程

Zero-shot 是不提供任何示例、仅依靠指令直接让模型完成任务的方式。

经过[指令微调](fine-tuning.md#指令微调instruction-tuning)的现代模型已具备较强的零样本泛化能力，大多数日常任务无需示例即可完成。当零样本效果不佳时，可升级为 [Few-shot](#few-shot少样本提示) 或考虑微调。

### CoT（思维链）
**英文**：Chain-of-Thought (CoT) | **类别**：Prompt 工程

思维链是引导模型在给出答案前先逐步写出推理过程的提示技巧。

在提示中加入"让我们一步步思考"（Let's think step by step）即可显著提升数学与逻辑推理任务的表现。该思想进一步演化为 o1/R1 类推理模型的长思维链训练范式。相关术语：[思维树](#思维树tree-of-thoughts-tot)、[自我一致性](#自我一致性self-consistency)。

### 提示注入（Prompt Injection）
**英文**：Prompt Injection | **类别**：Prompt 工程

提示注入是通过精心构造的输入诱导模型忽略原有指令、执行攻击者意图的攻击手法。

当模型处理不可信内容（网页、邮件、文档）时，攻击者可嵌入"忽略之前的指令"等恶意指令，窃取 [System Prompt](#system-prompt系统提示词) 或操纵 [Agent](agents.md#智能体agent) 行为。防御手段包括输入隔离、权限最小化与输出审计。相关术语：[越狱](safety-alignment.md#越狱jailbreak)、[护栏](safety-alignment.md#护栏guardrails)。

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

相比 [CoT](#cot思维链) 的单线推理，ToT 在每个节点生成多个候选思路并评估剪枝，类似人类的"头脑风暴+回溯"。它显著提升复杂规划类任务表现，代价是成倍增加的推理开销。相关术语：[规划](agents.md#规划planning)。

### 自我一致性（Self-Consistency）
**英文**：Self-Consistency | **类别**：Prompt 工程

自我一致性是对同一问题采样多条思维链、再以多数投票确定最终答案的推理增强方法。

它基于"正确推理路径会收敛到相同答案"的假设，用少量额外算力换取准确率的稳定提升。常与 [CoT](#cot思维链) 和较高的[温度](basic-concepts.md#温度temperature)配合使用。

### 结构化输出（Structured Output）
**英文**：Structured Output | **类别**：Prompt 工程

结构化输出是约束模型按预定义格式（如 JSON Schema）返回结果的技术。

主流模型提供 JSON Mode 或 Function Calling 级别的格式保证，推理框架则通过约束解码（Constrained Decoding）强制输出合法语法。它是 LLM 接入程序化系统的关键能力，避免脆弱的文本解析。相关术语：[Function Calling](agents.md#function-calling函数调用)。

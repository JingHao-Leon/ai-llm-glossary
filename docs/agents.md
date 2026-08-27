# 智能体 | AI Agents

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录智能体（AI Agent）相关的 12 个核心术语，包括 Agent、工具调用（Tool Use）、Function Calling（函数调用）、MCP（模型上下文协议）、ReAct、计算机使用（Computer Use）、多智能体、规划（Planning）、记忆（Memory）与反思（Reflection）等。
This page covers 12 core terms on AI Agents, including tool use, Function Calling, Model Context Protocol (MCP), ReAct, computer use, multi-agent systems, planning, memory, and reflection.

---

### 智能体（Agent）
**英文**：Agent | **类别**：智能体

智能体是以大模型为决策核心、能自主感知环境、规划步骤并调用工具完成复杂任务的 AI 系统。

与单次问答不同，Agent 具备"观察—思考—行动"的循环能力，可拆解目标、调用搜索/代码/数据库等工具并根据反馈调整策略。典型框架包括 [ReAct](#react)、AutoGPT 及各类编码 Agent（如 Claude Code、Cursor）。相关术语：[工具调用](#工具调用tool-use)、[规划](#规划planning)、[记忆](#记忆memory)。

### 工具调用（Tool Use）
**英文**：Tool Use | **类别**：智能体

工具调用是大模型在推理过程中调用外部函数、API 或系统以获取信息或执行操作的能力。

LLM 本身无法访问实时数据或执行动作，工具调用补上了这一短板：模型输出结构化的调用请求，由运行时执行后将结果回传模型继续推理。它是 [Agent](#智能体agent) 与现实世界交互的基础。相关术语：[Function Calling](#function-calling函数调用)、[MCP](#mcp模型上下文协议)。



### 计算机使用（Computer Use）
**英文**：Computer Use | **类别**：智能体

计算机使用是让 AI 像人一样直接操作图形界面（看屏幕、移动鼠标、点击、键入）来完成任务的能力。

它不依赖专用 API，而是通过截图理解界面并输出操作动作，使 [Agent](#智能体agent) 能操控任意存量软件，Anthropic 于 2024 年率先将其作为模型能力开放。该能力依赖视觉理解，安全上需要沙箱隔离与关键操作确认。相关术语：[工具调用](#工具调用tool-use)、[VLM](multimodal.md#vlm视觉语言模型)。

### Function Calling（函数调用）
**英文**：Function Calling | **类别**：智能体

Function Calling 是模型按预定义的函数签名生成结构化参数、请求宿主程序执行对应函数的能力。

开发者以 JSON Schema 描述可用函数，模型在需要时输出函数名与参数，执行结果再回传给模型。它把"让模型说话"变成"让模型办事"，是构建 [Agent](#智能体agent) 与应用集成的标准机制。相关术语：[结构化输出](prompt-engineering.md#结构化输出structured-output)。

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

常见技术包括任务分解（Task Decomposition）、[思维树](prompt-engineering.md#思维树tree-of-thoughts-tot)搜索与"规划-执行-再规划"循环。规划质量是区分 Agent 能力强弱的关键维度，也是当前大模型推理研究的重点方向。相关术语：[反思](#反思reflection)。

### 记忆（Memory）
**英文**：Memory | **类别**：智能体

记忆是 Agent 跨轮次、跨会话保存与调用信息的机制，使其具备持续上下文与个性化能力。

记忆通常分为短期记忆（当前会话的[上下文窗口](basic-concepts.md#上下文窗口context-window)内信息）与长期记忆（持久化到向量库或结构化存储、按需检索注入）。MemGPT、Mem0 等项目专门研究记忆管理。相关术语：[RAG](rag-retrieval.md#rag检索增强生成)。

### 反思（Reflection）
**英文**：Reflection | **类别**：智能体

反思是 Agent 对自身输出进行评估、发现错误并迭代改进的自我修正机制。

典型模式如 Reflexion：Agent 在失败后生成文字版"复盘"存入记忆，指导下一轮尝试。反思能以纯推理时计算换取显著的成功率提升，是 [Agent](#智能体agent) 可靠性工程的重要手段。相关术语：[自我一致性](prompt-engineering.md#自我一致性self-consistency)。

### 自主性（Autonomy）
**英文**：Autonomy | **类别**：智能体

自主性是 Agent 在无人类逐步干预下连续决策与执行的程度。

自主级别从"每步需人类确认"（Copilot 模式）到"完全自主执行"（AutoGPT 模式）不等。实际产品需在自主性与可控性之间权衡：关键操作（支付、删除、发送）通常保留人类审批节点（Human-in-the-loop）。相关术语：[护栏](safety-alignment.md#护栏guardrails)。

### 工作流编排（Workflow Orchestration）
**英文**：Workflow Orchestration | **类别**：智能体

工作流编排是用预定义的流程图或状态机组织多个 LLM 调用与工具节点的工程方法。

与完全自主的 [Agent](#智能体agent) 不同，编排式工作流的控制流由开发者显式定义，模型只负责节点内的智能决策，因而更可控、更易测试。LangGraph、Dify、Coze 等平台均以此为核心范式。

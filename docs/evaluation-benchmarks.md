# 评估与基准 | Evaluation & Benchmarks

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录大模型评估与基准相关的 10 个核心术语，包括 MMLU、HumanEval、GSM8K、困惑度（Perplexity）、基准污染（Benchmark Contamination）、Elo 评分与人工评估等。
This page covers 10 core terms on LLM evaluation and benchmarks, including MMLU, HumanEval, GSM8K, perplexity, benchmark contamination, Elo ratings, and human evaluation.

---

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

它等于交叉熵损失的指数，可直观理解为模型在预测下一个词时平均"犹豫"于多少个候选。困惑度常用于预训练质量监控与文本流畅度评估，但不直接反映下游任务表现。相关术语：[损失函数](training.md#损失函数loss-function)。

### 基准污染（Benchmark Contamination）
**英文**：Benchmark Contamination | **类别**：评估与基准

基准污染是基准测试题目泄漏进训练数据、导致评测分数虚高而非真实能力的现象。

由于大模型训练数据来自公开网络，热门基准几乎不可避免地被"见过"。检测手段包括 n-gram 重叠分析与动态更新题库，解读模型分数时应警惕污染带来的夸大。相关术语：[过拟合](training.md#过拟合overfitting)。

### GSM8K
**英文**：GSM8K | **类别**：评估与基准

GSM8K 是包含 8500 道小学数学应用题的基准，用于评估模型的多步算术推理能力。

该基准的崛起直接推动了 [CoT](prompt-engineering.md#cot思维链) 等推理技术流行，顶级模型准确率已超过 95%，更难的 MATH、AIME 基准成为新的分水岭。相关术语：[基准测试](#基准测试benchmark)。

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

泛化是机器学习的根本目标，也是区分"记住答案"与"真正理解"的试金石。[指令微调](fine-tuning.md#指令微调instruction-tuning)的核心价值即在于提升对未见指令的泛化，而[基准污染](#基准污染benchmark-contamination)会制造虚假泛化。相关术语：[过拟合](training.md#过拟合overfitting)。

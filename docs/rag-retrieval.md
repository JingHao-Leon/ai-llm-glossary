# RAG 与检索 | RAG & Retrieval

> [← 返回术语表首页 / Back to Glossary Home](../README.md)

本页面收录 RAG（检索增强生成）与检索相关的 13 个核心术语，包括 Embedding（嵌入）、向量数据库（Vector Database）、Chunking（文本切分）、重排序（Reranking）、混合检索、GraphRAG 与 Agentic RAG 等。
This page covers 13 core terms on Retrieval-Augmented Generation (RAG), including embeddings, vector databases, chunking, reranking, hybrid search, semantic search, GraphRAG, and Agentic RAG.

---

### RAG（检索增强生成）
**英文**：Retrieval-Augmented Generation (RAG) | **类别**：RAG 与检索

RAG 是在生成前先从外部知识库检索相关内容、再将其注入提示让模型据以作答的技术架构。

RAG 让模型回答有出处、知识可实时更新，是缓解[幻觉](basic-concepts.md#幻觉hallucination)与突破训练数据时效限制的主流方案。典型流程为：[Embedding](#embedding嵌入) 入库 → 检索 → [重排序](#重排序reranking) → 拼入提示生成。相关术语：[向量数据库](#向量数据库vector-database)、[Chunking](#chunking文本切分)。

### Embedding（嵌入）
**英文**：Embedding | **类别**：RAG 与检索

Embedding 是将文本、图像等内容映射为高维稠密向量、使语义相似度可用距离计算的表示技术。

在 RAG 中，文档与用户问题被同一嵌入模型编码，语义相近者向量距离更近。主流嵌入模型包括 OpenAI text-embedding 系列、BGE、E5 等，选型直接影响检索质量。相关术语：[语义搜索](#语义搜索semantic-search)、[余弦相似度](#余弦相似度cosine-similarity)。

### 向量数据库（Vector Database）
**英文**：Vector Database | **类别**：RAG 与检索

向量数据库是专门存储和高效检索高维向量的数据库系统。

它通过 HNSW、IVF 等近似最近邻（ANN）索引在毫秒级从百万级向量中找出最相似结果。代表产品有 Pinecone、Milvus、Qdrant、Weaviate、pgvector 等，是 [RAG](#rag检索增强生成) 系统的标准组件。相关术语：[Embedding](#embedding嵌入)。

### Chunking（文本切分）
**英文**：Chunking | **类别**：RAG 与检索

Chunking 是将长文档切分为较小片段以便嵌入与检索的预处理步骤。

切分策略直接影响检索质量：块太大噪声多，块太小丢失上下文。常见策略包括固定长度+重叠、按语义/段落切分、递归切分与父子块（Parent-Child）结构，典型块大小为 200–500 Token。相关术语：[RAG](#rag检索增强生成)。

### 重排序（Reranking）
**英文**：Reranking | **类别**：RAG 与检索

重排序是对初步检索结果用更精确的模型重新打分排序、提升相关性的后处理步骤。

向量检索追求召回速度，Cross-Encoder 类重排模型（如 BGE-Reranker、Cohere Rerank）则对"查询-文档"对精细打分，可将 Top-K 准确率显著提升。它是生产级 [RAG](#rag检索增强生成) 提升效果的性价比最高的环节之一。

### 混合检索（Hybrid Search）
**英文**：Hybrid Search | **类别**：RAG 与检索

混合检索是同时结合向量语义检索与关键词检索（BM25）、融合两者结果的检索策略。

向量检索擅长语义匹配但对专有名词、编号不敏感，关键词检索恰好互补；结果通常用 RRF（Reciprocal Rank Fusion）等算法融合。混合检索已成为企业级搜索与 [RAG](#rag检索增强生成) 的默认配置。

### 余弦相似度（Cosine Similarity）
**英文**：Cosine Similarity | **类别**：RAG 与检索

余弦相似度是通过计算两个向量夹角余弦值衡量其方向相似程度的度量。

取值范围为 -1 到 1，越接近 1 语义越相似，且不受向量长度影响，是文本 [Embedding](#embedding嵌入) 检索最常用的度量。欧氏距离与点积也是常见替代方案。

### 召回率（Recall）
**英文**：Recall | **类别**：RAG 与检索

召回率是检索系统成功找到的相关文档占全部相关文档的比例。

在 RAG 中，召回不足意味着关键知识根本没进入模型视野，生成再好也无法弥补。实践中常在召回阶段放宽 Top-K（如取 20–50 条），再用[重排序](#重排序reranking)精选，兼顾召回率与精确率。

### 语义搜索（Semantic Search）
**英文**：Semantic Search | **类别**：RAG 与检索

语义搜索是基于内容含义而非字面关键词匹配进行检索的搜索方式。

它将查询与文档都编码为 [Embedding](#embedding嵌入)，通过向量距离找到语义最相关的结果，能处理同义表达与跨语言检索。语义搜索是 [RAG](#rag检索增强生成) 检索环节的技术基础。

### 知识库（Knowledge Base）
**英文**：Knowledge Base | **类别**：RAG 与检索

知识库是为模型提供外部事实来源、经过结构化整理的数据集合。

在 LLM 应用中，知识库通常由文档经 [Chunking](#chunking文本切分)、[Embedding](#embedding嵌入) 后存入[向量数据库](#向量数据库vector-database)构建而成。知识库的覆盖率、新鲜度与切分质量直接决定 RAG 系统的上限。



### GraphRAG
**英文**：GraphRAG | **类别**：RAG 与检索

GraphRAG 是将知识图谱引入检索流程、利用实体关系增强多跳问答能力的 RAG 变体。

传统 [RAG](#rag检索增强生成) 按文本块相似度检索，难以回答需要跨文档串联关系的全局性问题；GraphRAG 先从语料抽取实体与关系构建图谱，检索时沿图谱扩展上下文，显著改善"总结全库""A 与 B 有何关联"类问题。该方法由微软于 2024 年开源推广。相关术语：[知识库](#知识库knowledge-base)。


### Agentic RAG
**英文**：Agentic RAG | **类别**：RAG 与检索

Agentic RAG 是由智能体自主决定何时检索、检索什么、以及如何验证检索结果的动态 RAG 范式。

与传统 RAG 固定的"检索-生成"流水线不同，Agentic RAG 让 [Agent](agents.md#智能体agent) 在多轮循环中规划查询、调用多种检索工具、评估结果质量并决定是否再次检索，更适合复杂问题，代价是更高的延迟与调用成本。相关术语：[RAG](#rag检索增强生成)。

### HyDE（假设性文档嵌入）
**英文**：Hypothetical Document Embeddings (HyDE) | **类别**：RAG 与检索

HyDE 是先让模型生成一段假设性答案、再用该答案的向量去检索真实文档的检索增强技巧。

它把"问题检索文档"转化为"答案检索文档"，缩小了查询与文档间的语义鸿沟，对短查询和零样本场景提升明显。代价是多一次生成调用的延迟。相关术语：[RAG](#rag检索增强生成)。

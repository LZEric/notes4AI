CoT:思维链

## 步骤
#### 1.数据预处理的方式
分块（太大的文件会不精准，一般为300或500）
向量化处理，使用嵌入模型（BGE-M3通用文本、M3E、Chinese-Alpaca-2）转为向量，存在向量库中
• 文档处理库: PyMuPDF (处理PDF), python-docx (处理Word), pytesseract (OCR识别图片中的文字)。
• 文本Embedding模型: **text-embedding-v4** (性能优秀，支持可变维度)。
• 图像Embedding模型: **CLIP** (由OpenAI开发，能同时理解图片和文本，是多模态RAG的核心)。QWEN-VL（大模型，效果好但是贵）也行
• 向量数据库/库: FAISS，作为向量检索引擎的核心，性能极高
注意：在生产环境中，可以使用Milvus, ChromaDB 或 Elasticsearch，他们提供了完整数据管理服务
• LLM: Qwen-turbo, kimi-K2，用于最终答案的生成。
• 流程编排框架: LangChain，用于粘合整个RAG流程。

#### 2.检索
查询向量数据库
根据相关性进行重排序

## 3.生成阶段
回答问题

## 嵌入模型选择
#### 通用
1. BGE-M3 跨语言长文档检索、高精度RAG应用 输入长度达8192 tokens（企业级）
2. text-embedding-3-large 英文内容优先的全球化应用
3. Jina-embeddings-v2 轻量级文本处理、实时推理任务
#### 中文
1. M3E-Turbo 中文法律、医疗领域检索任务 轻量模型，适合本地私有化部署
2. stella-mrl-large-zh-v3.5-1792 处理大规模中文数据能力强，捕捉细微语义关系。适用场景：中文文本高级语义分析、自然语言处理任务
#### 指令驱动与复杂任务模型
1. gte-Qwen2-7B-instruct 复杂指令驱动任务、智能问答系统
2. E5-mistral-7动态调整语义密度的复杂系统（企业级）

## 切片策略
#### 改进的固定长度切片
#### 语义切片
#### LLM语义切片
#### 层次切片
#### 滑动窗口切片

![[Pasted image 20250816113129.png]]
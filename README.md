# Huaidong-AI-LLM-RAG-Agent-Model-Project


## 目录结构 Directory Structure

  - **`01_TestApiKey.py`**：测试大模型 / 平台 API Key 是否可用（Test script to verify LLM / platform API keys.）
 
> 后续若继续跟随课程实现更复杂的 RAG 检索增强问答、Agent 智能体、多工具编排等内容，会在该目录下持续补充脚本与说明。  
> As I progress through the course (more advanced RAG pipelines, Agents, tool orchestration, etc.), more scripts and notes will be added under this directory.

- **`rag-clothing-customer-project/`**：RAG 项目 - 服装商品智能客服（RAG Project - Intelligent Customer Service for Clothing E-commerce）
  - 基于 RAG（检索增强生成）技术的服装电商智能客服系统知识库，提供尺码推荐、洗涤养护、颜色选择等问答能力  
    A RAG-based knowledge base and QA system for clothing e-commerce, including size recommendations, washing care, and color selection.
  - **`rag.py`**：核心 `RagService` 实现，封装向量检索、提示词模板、多轮对话与会话历史管理逻辑  
    Core `RagService` implementation that wires together the vector retriever, prompt template, multi-turn dialog, and history management.
  - **`knowledge_base.py`**：知识库构建服务，负责文件内容分割、向量化、写入 Chroma 向量库以及 MD5 去重  
    Knowledge base service for splitting documents, generating embeddings, writing to the Chroma vector store, and avoiding duplicates via MD5.
  - **`vector_stores.py`**：向量存储封装，基于 `Chroma` 创建检索器（`as_retriever`）供 RAG 链使用  
    Vector store wrapper based on `Chroma`, exposing a retriever (`as_retriever`) for use in the RAG chain.
  - **`file_history_store.py`**：基于文件的会话历史持久化，实现 `FileChatMessageHistory`，支持按 `session_id` 长期保存对话记录  
    File-based chat history persistence (`FileChatMessageHistory`) that stores conversations per `session_id` on disk.
  - **`config_data.py`**：项目配置，包括向量库路径（如 `./chroma_db`）、会话历史目录、分词参数与模型名称等  
    Central configuration for paths (e.g. `./chroma_db`, `./chat_history`), splitter parameters, and model names.
  - **`app_qa.py`**：基于 Streamlit 的 RAG 问答页面，支持多会话管理、流式回答展示以及从文件中恢复历史对话  
    Streamlit-based RAG QA UI with multi-session management, streaming answers, and restoration of chat history from files.
  - **`app_file_uploader.py`**：知识库文件上传与入库页面，用于将本地文档切分后写入 Chroma 向量库  
    Streamlit app for uploading documents, chunking them, and inserting them into the Chroma vector store.
  - **`run_qa.sh`**：一键启动问答页面（`app_qa.py`），在 Devbox 中监听 `0.0.0.0:8501`  
    Helper script to start the QA Streamlit app (`app_qa.py`) on `0.0.0.0:8501` inside Devbox.
  - **`run_app.sh`**：一键启动知识库上传页面（`app_file_uploader.py`），同样监听 `0.0.0.0:8501`  
    Helper script to start the knowledge-base uploader app (`app_file_uploader.py`) on `0.0.0.0:8501`.
  - **`data/`**：原始知识库文档存放目录（如尺码推荐、洗涤养护说明等）  
    Directory for original knowledge base documents (size guides, washing instructions, etc.).
  - **`chroma_db/`**：Chroma 向量库持久化目录，用于存放已向量化后的文档数据  
    Persisted Chroma vector store files.
  - **`chat_history/`**：会话历史文件目录，每个用户会话对应一个以 `session_id` 命名的 JSON 文件  
    Directory containing per-session JSON chat history files identified by `session_id`.

## 环境与运行 Environment & How to Run

- **运行环境 Environment**
  - 基于 Devbox 提供的 Debian 12 + Python 开发环境。  
    Based on Devbox environment (Debian 12 with Python pre-configured).
  - 需要自行配置对应的大模型平台 API Key（如 OpenAI、阿里云通义等）。  
    You need to configure your own API keys for LLM providers (OpenAI, Tongyi, etc.).

- **安装依赖 Install Dependencies**
  - 首次使用前，请先安装项目所需的 Python 依赖包：  
    Before running any scripts, please install the required Python packages:
  
```bash
pip install -r requirements.txt
```

- **运行方式 How to Run**
  - 进入 Devbox 开发环境后，可直接运行单个示例脚本，例如：  
    After entering the Devbox environment, you can run any script directly, e.g.:

```bash
cd /home/devbox/project/AI_LLM_RAG_Agent_Dev
python 11_LangChain_Tongyi_Basic_Usage.py
```

## 声明与目的 Disclaimer & Purpose

- **学习用途**：本仓库仅用于个人学习与笔记整理，无任何商业用途。  
  **For learning only**: This repository is for personal study and note-taking, not for commercial use.
- **非官方代码**：本项目与黑马程序员、课程官方无直接关联，仅参考其公开课程内容进行实践。  
  **Not official**: This is not an official repository of the HeiMa course; it is only inspired by and based on the public videos.
- **欢迎扩展**：你可以在此基础上继续扩展自己的 RAG / Agent 实战项目与实验。  
  **Feel free to extend**: You are welcome to build your own RAG and Agent experiments on top of this repo.


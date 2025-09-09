![LangChain Academy](https://cdn.prod.website-files.com/65b8cd72835ceeacd4449a53/66e9eba1020525eea7873f96_LCA-big-green%20(2).svg)

## 介绍

欢迎来到 LangChain Academy！

这里是一组不断完善的学习模块，聚焦于 LangChain 生态的基础概念：
- **Module 0**：基础环境与工具准备。
- **Module 1 - 4**：聚焦 LangGraph，从入门到进阶逐步深化。

每个模块文件夹中包含若干 Jupyter 笔记本（notebooks）。每本笔记本都配有对应的学习指引，帮助你循序渐进掌握主题。每个模块还包含一个 `studio` 子目录，内置与课程对应的 LangGraph 图（graphs），可通过 LangGraph API 与 Studio 进行可视化探索与调试。

## 环境准备（Setup）

### Python 版本

为获得最佳学习体验，请使用 **Python 3.11 或更高版本**。该版本与 LangGraph 兼容性最佳；如果你的版本较低，请先升级以避免依赖与语法不兼容问题。
```
python3 --version
```

### 克隆仓库（Clone repo）
```bash
git clone https://github.com/langchain-ai/langchain-academy.git
$ cd langchain-academy
```

### 创建虚拟环境并安装依赖
#### Mac/Linux/WSL
```bash
$ python3 -m venv lc-academy-env
$ source lc-academy-env/bin/activate
$ pip install -r requirements.txt
```
#### Windows PowerShell
```bash
PS> python3 -m venv lc-academy-env
PS> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
PS> lc-academy-env\scripts\activate
PS> pip install -r requirements.txt
```
提示：若使用公司网络或镜像源，请确保 `pip` 能访问到所需的 Python 包仓库；必要时可配置代理或镜像。

### 运行笔记本（Jupyter Notebooks）
如未安装 Jupyter，请先参考官方安装指南（`https://jupyter.org/install`）。
```bash
$ jupyter notebook
```

### 配置环境变量（Environment Variables）
你可以直接在终端导出环境变量，或使用 `.env` 文件结合 `python-dotenv` 管理。下方示例仅作占位，请替换为你自己的密钥。
#### Mac/Linux/WSL
```bash
$ export API_ENV_VAR="your-api-key-here"
```
#### Windows PowerShell
```bash
PS> $env:API_ENV_VAR = "your-api-key-here"
```
说明：环境变量用于存放密钥与配置（如 API Key），避免将敏感信息硬编码进代码库。

### 配置 OpenAI API Key
- 如无 OpenAI API Key，可前往官网注册获取（`https://openai.com/index/openai-api/`）。
- 将 Key 写入环境变量 `OPENAI_API_KEY`，供示例与 Studio 调用。

### 注册并配置 LangSmith
- 访问 `https://smith.langchain.com/` 注册 LangSmith。
- 了解 LangSmith 与工作流集成方式：`https://www.langchain.com/langsmith`；参考库文档：`https://docs.smith.langchain.com/`。
- 在环境中配置：
  - `LANGSMITH_API_KEY`
  - `LANGSMITH_TRACING_V2=true`（启用新一代追踪）
  - `LANGSMITH_PROJECT="langchain-academy"`（项目名称，可自定义）
用途说明：LangSmith 提供 LLM 应用的可观测性与评测能力，可记录调用链路、对话与指标，便于调试与优化。

### 配置 Tavily（用于联网检索）

- Tavily 是面向 LLM 与 RAG 优化的搜索 API，提供高效、稳定的联网检索能力。
- 访问 `https://tavily.com/` 申请 API Key（免费额度较友好）。本课程第 4 模块的部分内容会用到。
- 在环境中设置 `TAVILY_API_KEY`。

### 配置 LangGraph Studio

- LangGraph Studio 是用于查看与测试智能体（agents）的可视化调试 IDE。
- 可在本地运行，并通过浏览器访问（支持 Mac/Windows/Linux）。
- 文档参考：本地开发服务 `https://langchain-ai.github.io/langgraph/concepts/langgraph_studio/#local-development-server` 与快速上手 `https://langchain-ai.github.io/langgraph/cloud/how-tos/studio/quick_start/#local-development-server`。
- 每个模块的图定义位于 `module-x/studio/` 目录。
- 进入对应模块的 `/studio` 目录后，运行本地开发服务：

```
langgraph dev
```

You should see the following output:
```
- 🚀 API: http://127.0.0.1:2024
- 🎨 Studio UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
- 📚 API Docs: http://127.0.0.1:2024/docs
```

Open your browser and navigate to the Studio UI: `https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024`.

接着在浏览器打开 Studio UI：`https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024`。

- 使用 Studio 前，需要在各模块 `studio` 目录创建 `.env` 并写入相关 API Key。
- 以下示例演示为第 1 到 5 模块批量创建 `.env` 文件（请根据需要调整范围与变量）：
```bash
for i in {1..5}; do
  cp module-$i/studio/.env.example module-$i/studio/.env
  echo "OPENAI_API_KEY=\"$OPENAI_API_KEY\"" > module-$i/studio/.env
done
echo "TAVILY_API_KEY=\"$TAVILY_API_KEY\"" >> module-4/studio/.env
```
注意：Windows PowerShell 用户可改用等效脚本；或手动复制 `.env.example` 为 `.env` 并填入相应变量。

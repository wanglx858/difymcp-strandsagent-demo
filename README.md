# Patient Intake Chatbot with Dify MCP Server and Strands Agent 🤖🩺

本项目将 **Dify 工作流** 作为 MCP 接入到 **Strands Agent**，构建一个患者接收分诊的智能 Agent。  
基于 **Strands Web UI** 开发，使用 **Python MCP SDK** 实现 Dify workflow 的 MCP Server。

---

## 目录 📚

- [项目简介](#项目简介)
- [前置条件](#前置条件)
- [快速开始](#快速开始)
- [MCP 服务器安装与运行](#mcp-服务器安装与运行)
- [Strands Web UI 安装与配置](#strands-web-ui-安装与配置)
- [导入 MCP 服务](#导入-mcp-服务)
- [AWS 配置](#aws-配置)
- [首次运行](#首次运行)

---

## 项目简介 📝

该项目通过将 Dify 工作流封装为 MCP 服务，并集成到 Strands Agent 平台，实现患者接收与分诊的智能对话交互。  
通过 Strands Web UI 进行交互界面展示，支持配置多种模型和工具，方便快速部署和扩展。

---

## 前置条件 ✅

- Python 3.10 或更高版本
- 已配置 AWS 凭证，支持 Bedrock 和 Transcribe 服务
- Streamlit >= 1.30.0
- Strands Agents SDK >= 0.1.1
- MCP >= 0.1.0

---

## 快速开始 🚀

1. 克隆项目仓库：

```bash
git clone https://github.com/wanglx858/difymcp-strandsagent-demo.git

cd difymcp-strandsagent-demo
````

---

## MCP 服务器安装与运行 ⚙️

1. 进入 MCP 服务器目录：

```bash
cd aws-mcp-servers-samples
```

2. 安装依赖：

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
pip install -r dify_mcp_servers/requirements.txt
```

3. 配置 Dify API Key：

打开 `dify_mcp_server.py`，找到如下代码并替换为你的 API Key：

```python
DIFY_API_BASE = "https://api.dify.ai/v1"   # Dify 控制台可获取
DEFAULT_API_KEY = "你的API_KEY"  # 请填写你的 Dify API Key
```

4. 启动 MCP 服务器：

```bash
uv init
uv venv
source .venv/bin/activate
uv add "mcp[cli]" httpx
uv run dify_mcp_servers/dify_mcp_server.py
```

---

## Strands Web UI 安装与配置 🖥️

1. 进入 Strands Web UI 目录：

```bash
cd strands-web-ui
```

2. 安装依赖：

```bash
pip install -r requirements.txt
pip install -e .
```

3. 安装strands-agents-tools
```bash
pip install strands-agents-tools
```

---

## 导入 MCP 服务 🔌

编辑 `config/mcp_config.json`，添加或修改如下配置：

```json
"patient_intake_chatbot": {
  "command": "uv",
  "args": [
    "--directory",
    "/你的项目路径/aws-mcp-servers-samples/dify_mcp_servers", 
    "run",
    "dify_mcp_server.py"
  ],
  "description": "患者接收分诊智能 Agent 服务",
  "status": 1
}
```

> ⚠️ 请将路径修改为你的 `dify_mcp_server.py` 文件所在的绝对路径。

---

## AWS 配置 ☁️

确保 AWS 凭证已正确配置以使用 Bedrock 和 Transcribe 服务。

```bash
aws configure
```

或者通过环境变量配置：

```bash
export AWS_ACCESS_KEY_ID=your_access_key
export AWS_SECRET_ACCESS_KEY=your_secret_key
export AWS_DEFAULT_REGION=us-east-1
```

---

## 首次运行 ▶️

1. 启动应用：

```bash
streamlit run app.py
```

2. 在浏览器访问：

```
http://localhost:8501
```

3. 在侧边栏中配置你的模型和参数。

4. 在工具配置区启用所需功能。

5. 开始与患者接收分诊 Agent 聊天！💬

![截屏2025-07-09 18 23 21](https://github.com/user-attachments/assets/68b69c58-ddca-4042-8191-879b9f2d1c74)

---

如果有任何问题，欢迎提 Issue 或联系维护者。📩

---

祝你使用顺利！🚀✨


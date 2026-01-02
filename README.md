# 小帅旅游助手 - 智能AI旅游推荐系统

## 项目概述

基于自定义 ReAct Agent 架构的智能旅游助手系统，提供城市推荐、景点查询、路线规划等功能。

采用 **Agent + Web + Frontend** 三层模块化架构，通过 gRPC 实现模块间通信。

### 核心特性

- 自定义 ReAct Agent 架构 - 无第三方 AI 框架依赖
- 深度思考展示 - 可折叠的思考过程框
- 模块化架构 - Agent/Web/Frontend 三层分离
- SSE 流式响应 - 实时输出，支持停止控制
- 多协议 LLM 支持 - OpenAI、Claude、Gemini、Ollama 等
- 多会话管理 - 独立对话历史，会话隔离

### 技术栈

| 层级 | 技术 |
|------|------|
| 前端 | Next.js 16 + React 19 + TypeScript + Zustand + antd 6 |
| 后端 Web | FastAPI + Python |
| Agent | 自定义 ReAct 引擎 + gRPC |
| 部署 | 前后端分离 |

---

## 快速开始

### 前置条件

- Python 3.10+
- Node.js 18+
- npm 9+

### 安装依赖

**后端依赖**：
```bash
pip install -r requirements.txt
```

**前端依赖**：
```bash
cd frontend
npm install
```

### 配置

1. 复制配置模板：
```bash
cp config/llm_config.yaml.example config/llm_config.yaml
```

2. 编辑配置文件，填入你的 API Key：
```bash
vim config/llm_config.yaml
```

### 启动服务

| 服务 | 命令 |
|------|------|
| Agent | `python run_agent.py` |
| Web API | `python run_api.py` |
| Frontend | `cd frontend && npm run dev` |

### 访问应用

- 前端：**http://localhost:3000**
- API 文档：**http://localhost:8000/docs**

---

## 项目结构

```
ShuaiTravelAgent/
├── agent/              # AI Agent 模块 (gRPC, 端口50051)
│   └── src/
│       ├── core/       # ReAct 引擎核心
│       ├── llm/        # 多协议 LLM 客户端
│       ├── tools/      # 工具模块
│       └── server.py   # gRPC 服务器
│
├── web/                # Web API 模块 (FastAPI, 端口8000)
│   └── src/
│       ├── routes/     # API 路由
│       ├── services/   # 业务服务
│       └── grpc_client/ # gRPC 客户端
│
├── frontend/           # Next.js 16 前端
│   └── src/
│       ├── app/        # App Router
│       ├── components/ # React 组件
│       └── stores/     # Zustand 状态管理
│
├── config/             # 配置文件
│   ├── llm_config.yaml         # 实际配置 (被 git 忽略)
│   └── llm_config.yaml.example # 配置模板
│
├── docs/               # 文档
├── run_api.py          # API 启动脚本
└── run_agent.py        # Agent 启动脚本
```

---

## 配置说明

### 配置文件

```bash
config/
├── llm_config.yaml         # 实际使用的配置文件
└── llm_config.yaml.example # 配置模板
```

### 支持的 Provider

| provider | 说明 |
|----------|------|
| `openai` | OpenAI GPT 系列 |
| `anthropic` | Anthropic Claude 系列 |
| `google` | Google Gemini 系列 |
| `ollama` | Ollama 本地模型 |
| `openai-compatible` | 兼容 OpenAI API 的自定义服务 |

---

## 文档

详细文档请参阅 `docs/` 目录：

| 文档 | 说明 |
|------|------|
| [ARCHITECTURE.md](docs/ARCHITECTURE.md) | 系统架构设计 |
| [API.md](docs/API.md) | API 接口文档 |
| [DEVELOP.md](docs/DEVELOP.md) | 开发指南 |
| [DEPLOY.md](docs/DEPLOY.md) | 部署指南 |

---

## 更新日志

### v3.2.0
- 升级到 Next.js 16 + React 19
- 升级 antd 到 v6.x (支持 React 19)
- 升级 Vitest 到 v3
- 修复 API 422 错误 (添加 Pydantic 请求模型)
- 修复组件 bodyStyle 弃用警告
- 修复 antd Space direction 弃用警告
- 修复 antd message 静态函数警告 (使用 App 组件)
- 修复 antd List 弃用警告 (改用 Flex 组件)
- 优化 SSE 流式响应

### v3.1.0
- YAML 配置支持多模型多协议
- 简化项目结构
- 文档移至 docs/ 目录

### v3.0.0
- 全新模块化架构
- Agent/Web/Frontend 三层分离
- gRPC 模块间通信

---

## 许可证

MIT License

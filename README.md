# AI 爆款文章创作器 (AI Passage Creator) 🚀

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115.0-009688.svg?style=flat&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Vue](https://img.shields.io/badge/Vue-3.5.17-4FC08D.svg?style=flat&logo=vuedotjs)](https://vuejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6.svg?style=flat&logo=typescript)](https://www.typescriptlang.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED.svg?style=flat&logo=docker)](https://www.docker.com/)

[**English**](./README.en.md) | **简体中文**

基于多智能体编排 (Multi-Agent Orchestration) 的全栈 AI 文章创作平台。通过自研的编排逻辑，将大模型能力拆解为标题生成、大纲规划、正文创作、图像分析与生成等多个环节，并结合 SSE (Server-Sent Events) 技术提供流畅的实时交互体验。

---

## 🌟 技术亮点 (Internship Highlights)

- **多智能体协同编排 (Multi-Agent Orchestration)**：
  - 设计并实现了一套基于 `FastAPI` 的任务调度系统，将复杂的长文本创作任务解耦为 5 个独立智能体（标题、大纲、正文、图像、合成）。
  - 解决了长链条 AI 任务中的状态一致性问题，通过状态机管理文章生成的全生命周期。
- **高性能实时流处理 (SSE Streaming)**：
  - 利用 Python `SSE` 协议，实现了文章生成过程中的全链路打字机效果。
  - 通过异步生成器（Async Generator）优化了后端并发，单机可支撑数十个并发任务实时流式输出。
- **工程化与高可用设计**：
  - **多服务策略模式**：实现了一套灵活的图像生成策略，可根据配置动态切换 OpenAI DALL-E 3、Pexels API 或 SVG/Mermaid 绘图方案。
  - **数据一致性**：结合 Redis 缓存与 MySQL 事务，确保在多步骤生成过程中即便断连也能恢复进度。
  - **全链路 Docker 化**：包含完整的 `docker-compose` 部署方案，具备生产环境交付能力。

---

## 🛠️ 技术栈 (Tech Stack)

### 前端 (Frontend)
- **框架**: Vue 3.5 (Composition API) + Vite 7
- **语言**: TypeScript 5.8
- **UI 组件库**: Ant Design Vue 4.2.6
- **状态管理**: Pinia 3
- **实时通信**: SSE (Server-Sent Events)
- **其他**: ECharts (统计图表), Marked (Markdown 解析)

### 后端 (Backend)
- **框架**: FastAPI (Python 3.10+)
- **ORM**: SQLAlchemy 2.0 + PyMySQL
- **数据库**: MySQL 8.0 + Redis 5.2 (缓存/限流)
- **AI 引擎**: OpenAI GPT-4 / Gemini 1.5 / Google GenAI
- **存储**: 腾讯云 COS (对象存储)
- **支付**: Stripe API
- **包管理**: UV (高效 Python 依赖管理)

---

## ✨ 核心功能 (Features)

- 🤖 **全自动创作流**：从一个想法到包含配图、大纲、专业排版的万字长文，仅需 2 分钟。
- ⚡ **实时生成进度**：SSE 技术支持，用户可实时观察每一个智能体的思考与创作过程。
- 🖼️ **智能配图系统**：自动分析文章语境，生成或搜索匹配的插图、流程图 (Mermaid) 或 SVG 图形。
- 📊 **多维数据分析**：后台提供详细的用户行为画像、生成成功率统计及财务报表。
- 💳 **会员订阅体系**：完整的 VIP 等级与 Stripe 支付集成，支持额度限制与自动升级。
- 📱 **响应式设计**：适配 PC 与移动端，随时随地开启创作。

---

## 📂 项目结构 (Directory Structure)

```bash
.
├── frontend/               # 前端项目根目录
│   ├── src/
│   │   ├── api/            # 自动生成的 TS 接口定义
│   │   ├── components/     # 通用 UI 组件
│   │   ├── pages/          # 页面组件 (Admin, Article, User)
│   │   ├── stores/         # Pinia 状态
│   │   └── utils/          # 工具类 (SSE, Permission, Markdown)
│   └── Dockerfile          # 前端部署配置
├── python-backend/         # 后端项目根目录
│   ├── app/
│   │   ├── agent/          # 多智能体编排核心 (Agents, Orchestrator)
│   │   ├── models/         # SQLAlchemy 模型
│   │   ├── services/       # 业务逻辑 (Article, Image, Payment)
│   │   └── routers/        # FastAPI 路由定义
│   ├── docker-compose.yml  # 全栈容器化启动配置
│   └── pyproject.toml      # UV 依赖配置
├── sql/                    # 数据库初始化脚本
└── docs/images/            # 项目截图与架构图
```

---

## 🚀 快速开始 (Quick Start)

### 1. 环境准备
确保已安装：
- Docker & Docker Compose
- Node.js 18+
- Python 3.10+

### 2. 后端配置
```bash
cd python-backend
cp .env.example .env
# 编辑 .env 填入 OpenAI/Gemini Key, MySQL, Redis 等配置
```

### 3. 一键启动 (Docker)
```bash
docker-compose up -d
```
访问：`http://localhost`

### 4. 本地开发启动
**后端**:
```bash
cd python-backend
pip install uv
uv sync
python -m app.main
```
**前端**:
```bash
cd frontend
npm install
npm run dev
```

---

## 🔗 核心 API 示例 (Core API Usage)

### 文章生成任务 (SSE)
`POST /api/article/generate`
```json
{
  "topic": "未来人工智能的发展趋势",
  "style": "professional",
  "language": "zh-CN"
}
```
*响应：实时推送 `SseMessageTypeEnum` 包含的任务状态。*

---

## 🤝 贡献指南 (Contributing)

1. **Fork** 本仓库。
2. **创建分支**：`git checkout -b feature/your-feature-name`。
3. **提交规范**：遵循 [Angular Commit Message Convention](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#-commit-message-format)。
4. **提交 PR**：确保代码通过 Lint 检测并附带必要的测试用例。

---

## 📄 许可证 (License)

本项目采用 [MIT License](LICENSE) 协议。

---

## 👤 作者 (Author)

- **FurinaLuna**: 个人博客[blog](https://furinaluna.top)
- **GitHub**: [FurinaLuna](https://github.com/FurinaLuna)
- **Email**: QQ: [2517523791@qq.com] Gmail:[furinalunaz@gmail.com]

---


# AI Passage Creator (AI Article Generator) 🚀

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115.0-009688.svg?style=flat&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Vue](https://img.shields.io/badge/Vue-3.5.17-4FC08D.svg?style=flat&logo=vuedotjs)](https://vuejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6.svg?style=flat&logo=typescript)](https://www.typescriptlang.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED.svg?style=flat&logo=docker)](https://www.docker.com/)

**English** | [**简体中文**](./README.md)

A full-stack AI article creation platform based on **Multi-Agent Orchestration**. By decomposing large model capabilities into multiple stages such as title generation, outline planning, content creation, and image analysis/generation, and combining **SSE (Server-Sent Events)** technology, it provides a smooth real-time interactive experience.

---

## 🌟 Internship Highlights

This project demonstrates the following core competencies for summer internship applications:

- **Multi-Agent Orchestration**:
  - Designed and implemented a task scheduling system based on `FastAPI`, decoupling complex long-text creation tasks into 5 independent agents (Title, Outline, Content, Image, Merger).
  - Solved state consistency issues in long-chain AI tasks by managing the full lifecycle of article generation through state machines.
- **High-Performance Real-Time Stream Processing (SSE Streaming)**:
  - Utilized Python `SSE` protocol to achieve full-link typewriter effects during article generation.
  - Optimized backend concurrency using Async Generators, supporting dozens of concurrent tasks with real-time streaming output on a single machine.
- **Engineering and High Availability Design**:
  - **Multi-Service Strategy Pattern**: Implemented a flexible image generation strategy that dynamically switches between OpenAI DALL-E 3, Pexels API, or SVG/Mermaid drawing schemes based on configuration.
  - **Data Consistency**: Combined Redis caching with MySQL transactions to ensure progress recovery even if disconnected during the multi-step generation process.
  - **Full-Link Dockerization**: Includes a complete `docker-compose` deployment solution with production-ready delivery capabilities.

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: Vue 3.5 (Composition API) + Vite 7
- **Language**: TypeScript 5.8
- **UI Component Library**: Ant Design Vue 4.2.6
- **State Management**: Pinia 3
- **Real-Time Communication**: SSE (Server-Sent Events)
- **Others**: ECharts (Statistics), Marked (Markdown Parsing)

### Backend
- **Framework**: FastAPI (Python 3.10+)
- **ORM**: SQLAlchemy 2.0 + PyMySQL
- **Database**: MySQL 8.0 + Redis 5.2 (Cache/Rate Limiting)
- **AI Engine**: OpenAI GPT-4 / Gemini 1.5 / Google GenAI
- **Storage**: Tencent Cloud COS (Object Storage)
- **Payment**: Stripe API
- **Package Management**: UV (High-performance Python dependency management)

---

## ✨ Features

- 🤖 **Automated Workflow**: From an idea to a 10,000-word article with images, outlines, and professional typesetting in just 2 minutes.
- ⚡ **Real-Time Progress**: Supported by SSE technology, users can observe the thinking and creation process of each agent in real-time.
- 🖼️ **Intelligent Image System**: Automatically analyzes article context to generate or search for matching illustrations, flowcharts (Mermaid), or SVG graphics.
- 📊 **Multi-Dimensional Data Analysis**: The background provides detailed user behavior profiling, generation success rate statistics, and financial reports.
- 💳 **Membership Subscription System**: Complete VIP levels and Stripe payment integration, supporting quota limits and automatic upgrades.
- 📱 **Responsive Design**: Adapted for PC and mobile, enabling creation anytime, anywhere.

---

## 📂 Directory Structure

```bash
.
├── frontend/               # Frontend root directory
│   ├── src/
│   │   ├── api/            # Auto-generated TS interface definitions
│   │   ├── components/     # Common UI components
│   │   ├── pages/          # Page components (Admin, Article, User)
│   │   ├── stores/         # Pinia stores
│   │   └── utils/          # Utility classes (SSE, Permission, Markdown)
│   └── Dockerfile          # Frontend deployment configuration
├── python-backend/         # Backend root directory
│   ├── app/
│   │   ├── agent/          # Multi-agent orchestration core (Agents, Orchestrator)
│   │   ├── models/         # SQLAlchemy models
│   │   ├── services/       # Business logic (Article, Image, Payment)
│   │   └── routers/        # FastAPI router definitions
│   ├── docker-compose.yml  # Full-stack containerization configuration
│   └── pyproject.toml      # UV dependency configuration
├── sql/                    # Database initialization scripts
└── docs/images/            # Project screenshots and architecture diagrams
```

---

## 🚀 Quick Start

### 1. Prerequisites
Ensure you have installed:
- Docker & Docker Compose
- Node.js 18+
- Python 3.10+

### 2. Backend Configuration
```bash
cd python-backend
cp .env.example .env
# Edit .env and fill in OpenAI/Gemini Keys, MySQL, Redis, etc.
```

### 3. One-Click Start (Docker)
```bash
docker-compose up -d
```
Access: `http://localhost:5173`

### 4. Local Development
**Backend**:
```bash
cd python-backend
pip install uv
uv sync
python -m app.main
```
**Frontend**:
```bash
cd frontend
npm install
npm run dev
```

---

## 🔗 Core API Example

### Article Generation Task (SSE)
`POST /api/article/generate`
```json
{
  "topic": "Future trends of AI",
  "style": "professional",
  "language": "en-US"
}
```
*Response: Real-time status updates via `SseMessageTypeEnum`.*

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 👤 Author

- **FurinaLuna**
- **GitHub**: [FurinaLuna](https://github.com/FurinaLuna)
- **Email**: [your-email@example.com]

---

> 💡 **Tip**: Please upload your screenshots and architecture diagrams to `docs/images/` to enhance the visual presentation.

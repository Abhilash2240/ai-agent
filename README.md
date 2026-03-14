# AI Agent

An AI-powered browser automation and deep research platform built with [browser-use](https://github.com/browser-use/browser-use) and a Gradio web UI.

## Overview

This repository contains a web-based interface that lets you run AI agents capable of:

- **Browser Use Agent** — Controls a real browser to complete tasks autonomously (form filling, web scraping, navigation, research, etc.)
- **Deep Research Agent** — Conducts structured, multi-step research on any topic using LangGraph state machines and parallel browser searches, producing a full markdown report

## Project Structure

```
ai-agent/
└── web-ui/          # Gradio web UI + agent source code
    ├── src/
    │   ├── agent/
    │   │   ├── browser_use/       # BrowserUseAgent
    │   │   └── deep_research/     # DeepResearchAgent (LangGraph)
    │   ├── browser/               # Custom Playwright browser wrapper
    │   ├── controller/            # Custom action controller
    │   └── webui/                 # Gradio UI components
    ├── tests/                     # Test scripts
    ├── webui.py                   # Entry point
    ├── requirements.txt
    └── docker-compose.yml
```

## Quick Start

### Prerequisites

- Python 3.11+
- [uv](https://docs.astral.sh/uv/) (recommended) or pip

### Setup

```bash
# 1. Clone the repo
git clone https://github.com/Abhilash2240/ai-agent.git
cd ai-agent/web-ui

# 2. Create and activate virtual environment
uv venv --python 3.11
.venv\Scripts\activate        # Windows
# source .venv/bin/activate   # macOS/Linux

# 3. Install dependencies
uv pip install -r requirements.txt
playwright install chromium --with-deps

# 4. Configure environment
cp .env.example .env
# Edit .env and add your API keys

# 5. Launch the web UI
python webui.py --ip 127.0.0.1 --port 7788
```

Open [http://127.0.0.1:7788](http://127.0.0.1:7788) in your browser.

### Docker

```bash
cd web-ui
cp .env.example .env   # add your API keys
docker compose up --build
```

- Web UI: [http://localhost:7788](http://localhost:7788)
- VNC viewer: [http://localhost:6080/vnc.html](http://localhost:6080/vnc.html)

## Supported LLM Providers

| Provider     | Notes                          |
|--------------|--------------------------------|
| OpenAI       | GPT-4o, GPT-4, etc.            |
| Google       | Gemini 2.0 Flash, etc.         |
| Anthropic    | Claude models                  |
| Azure OpenAI | Set endpoint in `.env`         |
| DeepSeek     | Including DeepSeek-R1 (reasoning) |
| Ollama       | Local models                   |
| AWS Bedrock  | Configured via AWS credentials |

## Features

- **Multi-LLM support** — Switch providers and models from the UI
- **Vision support** — Agents can analyze screenshots for better understanding
- **Custom browser** — Use your own Chrome profile (no re-login needed)
- **Persistent sessions** — Keep the browser open between tasks
- **MCP server integration** — Connect external tools via Model Context Protocol
- **Deep Research** — Automated hierarchical research plans with parallel agents
- **Task recording** — Save GIFs and agent history for replay/debugging
- **Docker support** — Full containerized deployment with VNC viewer

## Environment Variables

Key variables in `.env`:

```env
# LLM Keys
OPENAI_API_KEY=
GOOGLE_API_KEY=
ANTHROPIC_API_KEY=
AZURE_OPENAI_API_KEY=
DEEPSEEK_API_KEY=

# Default model
DEFAULT_LLM=openai

# Browser (optional — use your own Chrome)
BROWSER_PATH=
BROWSER_USER_DATA=
```

See `.env.example` for the full list.

## License

See [web-ui/LICENSE](web-ui/LICENSE).

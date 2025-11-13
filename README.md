# End-to-End Agentic Chatbot using FastAPI and LangChain

[![Repo](https://img.shields.io/badge/repo-GitHub-black)](https://github.com/Parthkumar20/End-to-end-Agentic-Chatbot-using-Fastapi-Langchain)  
[![License](https://img.shields.io/badge/license-MIT-blue)](#license)  
[![Python](https://img.shields.io/badge/python-3.9%2B-orange)](#requirements)

> **Project**: Build an agentic chatbot that orchestrates multiple LLM providers and tools using **LangChain**, exposes a production-ready API with **FastAPI**, and ships interactive UIs on **Hugging Face Spaces (Gradio)** and **Streamlit**.

---

## Table of contents
- [Overview](#overview)  
- [Features](#features)  
- [Architecture](#architecture)  
- [Quick demo](#quick-demo)  
- [Tech stack](#tech-stack)  
- [Getting started (local)](#getting-started-local)  
- [Environment variables](#environment-variables)  
- [Run (development)](#run-development)  
- [API spec & usage examples](#api-spec--usage-examples)  
- [Agent design & tools](#agent-design--tools)  
- [Deployment](#deployment)  
- [Testing & CI/CD](#testing--cicd)  
- [Monitoring, scaling & cost management](#monitoring-scaling--cost-management)  
- [Security considerations](#security-considerations)  
- [Troubleshooting](#troubleshooting)  
- [Contributing](#contributing)  
- [License](#license)  
- [Acknowledgements](#acknowledgements)

---

## Overview
This repository demonstrates a complete, end-to-end agentic chatbot implemented with:

- **LangChain** for multi-step reasoning, tool orchestration, and agent workflows  
- **FastAPI** to expose REST endpoints for production usage  
- **Multiple LLM providers** (Groq, OpenAI) and **Tavily** as a real-time web search tool  
- Interactive frontends built with **Gradio** (for Hugging Face Spaces) and **Streamlit**

Use cases:
- Retrieval-augmented Q&A with live web search  
- Multi-step reasoning workflows that call custom tools/APIs  
- Rapid prototyping and deployment to Spaces / Streamlit

---

## Features
- Agent orchestration via LangChain (tool selection, step-by-step reasoning)  
- Provider-agnostic LLM interface (switchable between Groq and OpenAI)  
- Real-time search via Tavily to fetch contextual evidence from the web  
- FastAPI backend with endpoints for text chat, tool results, and agent status  
- Optional UI deployment via Gradio (Hugging Face Spaces) and Streamlit  
- Configurable model, temperature, response length, and tool permissions  
- Logging, basic retries, and modular tool registration

---

## Architecture


- FastAPI serves as the gateway and orchestrator; LangChain handles reasoning and tool invocation.
- Tools are implemented as modular classes/functions and registered with the agent.

---

## Quick demo
(Replace with a live demo link if deployed)

- Local UI: `http://localhost:7860` (Gradio) or `http://localhost:8501` (Streamlit if using default ports)
- API example: `POST /api/v1/chat` with `{ "query": "What's the latest on X?" }`

---

## Tech stack
- Python 3.9+  
- FastAPI + Uvicorn / Gunicorn (ASGI server)  
- LangChain  
- LLMs: Groq, OpenAI (model selection via env)  
- Search tool: Tavily (web search integration)  
- Frontend: Gradio (for HF Spaces), Streamlit (optional)  
- Optional deployment: Docker, Hugging Face Spaces, Railway/Render/Vercel for static UI

---

## Getting started (local)

> Environment: Python 3.9+ recommended. Use virtualenv / venv or conda.

```bash
# clone
git clone https://github.com/Parthkumar20/End-to-end-Agentic-Chatbot-using-Fastapi-Langchain.git
cd End-to-end-Agentic-Chatbot-using-Fastapi-Langchain

# create venv
python -m venv .venv
source .venv/bin/activate       # macOS / Linux
.venv\Scripts\activate          # Windows

# install
pip install -r requirements.txt
fastapi
uvicorn[standard]
langchain
openai
requests
gradio
streamlit
python-dotenv
# .env (example)
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxx
GROQ_API_KEY=groq-xxxxxxxxxxxxxxxxxxxx
TAVILY_API_KEY=tavily-xxxxxxxxxxxxxxxxx
MODEL_NAME=gpt-4o-mini           # example
DEFAULT_TEMPERATURE=0.0
FASTAPI_HOST=0.0.0.0
FASTAPI_PORT=8000
LOG_LEVEL=info
uvicorn backend:app --reload --host ${FASTAPI_HOST:-127.0.0.1} --port ${FASTAPI_PORT:-8000}
python frontend.py
# Or if Gradio app is mounted within FastAPI, visit designated endpoint
streamlit run streamlit_app.py

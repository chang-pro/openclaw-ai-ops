# OpenClaw — AI Agent Operations Platform

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-Bot_API-26A5E4?style=flat-square&logo=telegram&logoColor=white)
![Sentry](https://img.shields.io/badge/Sentry-Monitoring-362D59?style=flat-square&logo=sentry&logoColor=white)
![Repo](https://img.shields.io/badge/Source-Private-orange?style=flat-square)

**A personal AI operations platform that monitors projects, dispatches automated bug fixes, and delivers daily intelligence briefs — all controllable from a phone via Telegram.**

---

## What It Does

OpenClaw is an AI-powered DevOps agent that acts as a 24/7 operations assistant across multiple software projects. It reads project context on-demand, dispatches code analysis and fixes, and reports back through Telegram.

## Core Capabilities

### Remote Bug Fixing
- Receive a Telegram message like *"fix this bug in Ringora"*
- OpenClaw reads the project's handoff context and dispatches a Claude Code or Codex CLI session on the build server
- Returns the output and fix directly to Telegram

### Error Monitoring
- Periodic Sentry polling (every 30 min) for unresolved errors across all projects
- Auto-alerts on Telegram with error details and stack traces
- Optional auto-dispatch of AI analysis on new errors

### Daily Briefs
- Morning summary of all active projects: what needs attention, deploy status, stale branches
- Pulls context from project handoff files and monitoring systems
- Includes unresolved errors, deployment status, and priority items

### Context-Aware Dispatch
- Reads project handoff documents before dispatching any task
- Queries knowledge base for deep project context
- Lean context loading — reads on-demand, never preloads entire repos

## Architecture

```
┌──────────────┐     ┌───────────────────────────┐
│   Telegram   │◄───►│     OpenClaw Core          │
│   (Mobile)   │     │  • Command Parser          │
└──────────────┘     │  • Context Loader          │
                     │  • Agent Dispatcher         │
                     │  • Response Formatter        │
                     └──────────┬────────────────┘
                                │
              ┌─────────────────┼─────────────────┐
              ▼                 ▼                  ▼
       ┌────────────┐  ┌──────────────┐  ┌──────────────┐
       │ Build Server│  │   Sentry     │  │ Knowledge    │
       │ (Mac Mini)  │  │   Monitoring │  │ Base         │
       │ Claude/Codex│  │              │  │ (Obsidian)   │
       └────────────┘  └──────────────┘  └──────────────┘
```

## Tech Stack

- **Language:** Python 3.11
- **Bot Interface:** Telegram Bot API
- **AI Dispatch:** Claude Code CLI, Codex CLI
- **Monitoring:** Sentry API integration
- **Knowledge Base:** Obsidian vault (on-demand reads)
- **Infrastructure:** Mac Mini (headless build server)
- **Scheduling:** Cron-based heartbeat and monitoring

## Skills Demonstrated

- AI agent orchestration and multi-model dispatch
- DevOps automation and remote infrastructure management
- Event-driven architecture with real-time alerting
- Context-efficient design (on-demand loading vs. preloading)
- Mobile-first operations interface via Telegram

---

> *This is a showcase page for a private repository. Source code available upon request for verified opportunities.*

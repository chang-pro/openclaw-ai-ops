# OpenClaw — AI Agent Operations Platform

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-Bot_API-26A5E4?style=flat-square&logo=telegram&logoColor=white)
![Sentry](https://img.shields.io/badge/Sentry-Monitoring-362D59?style=flat-square&logo=sentry&logoColor=white)
![Repo](https://img.shields.io/badge/Source-Private-orange?style=flat-square)

**A personal AI operations platform that monitors projects, dispatches automated bug fixes, and delivers daily intelligence briefs — all controllable from a phone via Telegram.**

Built on top of [**Peter Steinberger's OpenClaw**](https://openclaw.ai) ([steipete](https://github.com/steipete)) — customized and extended for my specific project ecosystem and workflows.

---

## My Use Case

I run multiple production projects (SaaS CRM, trading bot, client websites, automation pipelines). OpenClaw ties them all together as my 24/7 operations layer:

- **I'm on my phone** → text a Telegram command → OpenClaw dispatches a fix on my build server → I get results back
- **Something breaks at 3 AM** → Sentry catches it → OpenClaw alerts me with full context → optionally auto-dispatches analysis
- **Every morning** → I get a brief on all my projects: what shipped, what broke, what needs attention

## Core Capabilities

### Remote Bug Fixing via Telegram
- Send *"fix this bug in Ringora"* from my phone
- OpenClaw reads the project's handoff context, dispatches Claude Code or Codex on the build server
- Returns results directly in Telegram

### Sentry Error Monitoring
- Polls Sentry every 30 minutes for unresolved errors across all projects
- Alerts on Telegram with error details and stack traces
- Optional auto-dispatch of AI analysis on new errors

### Daily Briefs
- Morning summary: all active projects, what needs attention, deploy status
- Pulls from project handoff files and monitoring systems
- Flags stale projects and unresolved errors

### Context-Aware Dispatch
- Reads project handoff documents before dispatching any task
- Queries knowledge base on demand — never preloads entire repos
- Lean context design for token efficiency

## Architecture

```
┌──────────────┐     ┌───────────────────────────┐
│   Telegram   │◄───►│     OpenClaw Core          │
│   (Phone)    │     │  • Command Parser          │
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

## Credits

This project is built on [**OpenClaw**](https://openclaw.ai) by [**Peter Steinberger**](https://github.com/steipete). I took the core framework and customized it for my own project ecosystem — adding my specific integrations, monitoring setup, and Telegram workflows.

## Skills Demonstrated

- AI agent orchestration and multi-model dispatch
- DevOps automation and remote infrastructure management
- Event-driven architecture with real-time alerting
- Context-efficient design (on-demand loading vs. preloading)
- Mobile-first operations interface via Telegram

---

> *This is a showcase page for a private repository. Source code available upon request for verified opportunities.*

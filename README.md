# OpenClaw — AI Agent Operations Platform

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-Bot_API-26A5E4?style=flat-square&logo=telegram&logoColor=white)
![Sentry](https://img.shields.io/badge/Sentry-Monitoring-362D59?style=flat-square&logo=sentry&logoColor=white)
![Repo](https://img.shields.io/badge/Source-Private-orange?style=flat-square)

**I took [Peter Steinberger's OpenClaw](https://openclaw.ai) and turned it into my personal DevOps command center.** I can fix bugs, monitor errors, and get project updates — all from my phone via Telegram while I'm away from my desk.

Built on [**steipete/OpenClaw**](https://github.com/steipete) — full credit to Peter for the core framework.

---

## Why I Built This

I run 6+ production projects across multiple machines. Before OpenClaw, "fixing a bug" meant:
1. Open laptop → SSH into build server → pull repo → read context → run fix → verify

Now it's:
1. Text Telegram: *"fix the auth bug in Ringora"* → Done.

OpenClaw reads the project context, dispatches the right AI tool, runs it on my build server, and sends results back to my phone.

## What I Customized

Peter built the core OpenClaw framework. Here's what I added on top:

### Project-Aware Context System
- Built a **semantic handoff system** — every project auto-generates a `HANDOFF.md` on each commit with current state, recent changes, and open issues
- OpenClaw reads these before dispatching any task, so it never goes in blind
- Integrated with my **Obsidian knowledge base** for deep project context (architecture docs, runbooks, past decisions)
- Context is loaded **on-demand** — not preloaded. Keeps token usage lean.

### Multi-Project Telegram Command Interface
- Custom Telegram bot commands for each of my projects
- *"fix this bug in Ringora"* → dispatches Claude Code with Ringora's full context
- *"run the trading bot backtest"* → dispatches on my Mac Mini with the right config
- *"what's the status of Orleans Cleaning?"* → pulls from handoff files and returns a summary

### Sentry Integration Across All Projects
- Polls Sentry every 30 minutes for new unresolved errors across all my projects
- Alerts me on Telegram with the error, stack trace, and which project it's from
- Can auto-dispatch Codex to investigate before I even look at it

### Daily Intelligence Briefs
- Every morning I get a Telegram message summarizing:
  - What shipped yesterday across all projects
  - Any new Sentry errors
  - Which projects are stale (no commits in X days)
  - Priority items that need attention
- Pulls from handoff files, Sentry, and git history automatically

### Mac Mini Build Server Orchestration
- OpenClaw dispatches Claude Code and Codex CLI sessions on my headless Mac Mini
- Manages concurrent sessions, captures output, formats results
- Health checks and heartbeat monitoring to make sure the server is alive

## Architecture

```
┌──────────────┐     ┌─────────────────────────────────┐
│  My Phone    │     │        OpenClaw Core              │
│  (Telegram)  │◄───►│  ┌─────────────────────────┐    │
└──────────────┘     │  │ Custom Command Router     │    │
                     │  │ • Per-project dispatching │    │
                     │  │ • Context-aware loading   │    │
                     │  │ • Handoff file reader     │    │
                     │  └────────────┬──────────────┘    │
                     └───────────────┼──────────────────┘
                                     │
                ┌────────────────────┼────────────────────┐
                ▼                    ▼                     ▼
         ┌────────────┐     ┌──────────────┐     ┌──────────────┐
         │ Mac Mini   │     │   Sentry     │     │  Obsidian    │
         │ Build Srv  │     │  (6+ projects│     │  Knowledge   │
         │ Claude Code│     │   monitored) │     │  Base        │
         │ Codex CLI  │     │              │     │              │
         └────────────┘     └──────────────┘     └──────────────┘
```

## Tech Stack

`Python 3.11` · `Telegram Bot API` · `Claude Code CLI` · `Codex CLI` · `Sentry API` · `Obsidian vault` · `Mac Mini (headless)` · `Cron scheduling`

## Credits

Core framework by [**Peter Steinberger**](https://github.com/steipete) — [openclaw.ai](https://openclaw.ai). I extended it with my project ecosystem, context system, and monitoring integrations.

---

> *Closed source. Source code available for serious inquiries.*

# Personal Assistant

A personal assistant powered by Claude Code. Manages your day, tasks, emails, and mental load.

## Prerequisites

1. **Mac** (macOS)
2. **Node.js** — Download from https://nodejs.org (LTS version)
3. **Claude Code** — Install with: `npm install -g @anthropic-ai/claude-code`
4. **Anthropic API key** — Get one from https://console.anthropic.com
5. **Obsidian** (recommended) — Download from https://obsidian.md — free note viewer for browsing your tasks, projects, and notes visually. After setup, open this folder as an Obsidian vault.

## Setup

```bash
# 1. Set your API key (add to ~/.zshrc to persist)
export ANTHROPIC_API_KEY="your-key-here"

# 2. Navigate to this folder
cd ~/personal-assistant

# 3. Launch
claude
```

The assistant will walk you through a setup wizard on first launch.

## Daily Usage

```bash
cd ~/personal-assistant && claude
```

**Tip:** Add an alias to your shell for quick access:

```bash
echo 'alias pa="cd ~/personal-assistant && claude"' >> ~/.zshrc
source ~/.zshrc
```

Then just type `pa` to start your assistant.

## Commands

| Command | Alias | What it does |
|---------|-------|-------------|
| `/good-morning` | `/gm` | Morning briefing and daily planning |
| `/plan` | `/p` | Plan or replan the day |
| `/whats-next` | `/next` | What should I focus on? |
| `/end-of-day` | `/eod` | Wrap up and reflect |
| `/checkin` | `/ci` | Progress check-in |
| `/capture <text>` | `/c` | Quick capture a thought |
| `/tasks` | `/t` | Show today's tasks |
| `/inbox` | `/in` | Process captured items |
| `/done` | `/d` | Mark a task complete |
| `/stuck` | | Help when overwhelmed |
| `/draft` | | Draft an email or message |
| `/polish` | | Improve existing text |
| `/plan-week` | `/pw` | Plan the week ahead |
| `/week` | `/w` | Review the past week |
| `/help` | `/h` | Show all commands |
| `/find-skills` | `/sk` | Search for new capabilities |
| `/profile` | | View or change settings |
| `/setup` | | Re-run setup wizard |
| `/status` | | System health check |
| `/update` | `/up` | Check for skill updates |
| `/heal` | | Fix broken skills |

You can also just talk naturally. Say "good morning" instead of `/gm`, or "I'm stuck" instead of `/stuck`.

## How It Works

- **Skills** live in `.claude/skills/` — each one teaches the assistant how to do something
- **Your data** lives in `.assistant/` — profile, preferences, integrations, current state
- **PARA folders** organize your knowledge: `00-Inbox/`, `01-Projects/`, `02-Areas/`, `03-Resources/`, `04-Archives/`
- **Captures** go to `00-Inbox/Daily/` — process them later by saying "process my inbox"
- **Daily plans** are generated in `Daily Plans/` — your prioritized task list each day
- **Permanent notes** live in `Permanent Notes/` — Zettelkasten-style synthesized insights

All data stays on your computer. Nothing is stored in the cloud beyond the API calls themselves.

## Extending

Find and install new skills anytime:

```
/find-skills outlook email
/find-skills project management
/find-skills focus timer
```

The assistant can also update and repair itself:

```
/update    — check for skill updates
/heal      — fix broken skills or missing files
```

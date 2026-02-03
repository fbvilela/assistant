# Personal Assistant

An AI-powered personal assistant that helps you manage your day, tasks, communications, and mental load. Built on [Claude Code](https://github.com/anthropics/claude-code), it uses a skill-based architecture where each capability is a modular, teachable skill.

## What It Does

- **Morning briefings** — Start your day with a plan
- **GTD + PARA + Zettelkasten** — Full second brain with inbox processing, project management, and permanent notes
- **ADHD-friendly** — Overwhelm handlers, gentle check-ins, task breakdowns
- **Quick capture** — Grab thoughts without context-switching
- **Daily/weekly planning & reviews** — Stay on track
- **Email/message drafting** — Helps you communicate clearly
- **Extensible** — Find and install new skills as you need them

All your data stays local on your machine.

## Setup

### Already have Claude Code?

If you have Claude Code set up with an Anthropic API key or subscription:

```bash
cd /path/to/personal-assistant
claude
```

That's it. The assistant will walk you through a setup wizard on first launch.

---

### Budget Setup: Run It for (Almost) Free

You can run this assistant using **Ollama** with the **Kimi K2.5** model on Ollama's cloud infrastructure — no expensive hardware or complex configuration needed.

#### Step 1: Install Claude Code

```bash
curl -fsSL https://claude.ai/install.sh | sh
```

#### Step 2: Install Ollama

Download from [ollama.com](https://ollama.com)

#### Step 3: Pull the Model

```bash
ollama pull kimi-k2.5:cloud
```

#### Step 4: Launch

```bash
cd /path/to/personal-assistant
ollama launch claude --model kimi-k2.5:cloud
```

#### Notes

- **kimi-k2.5:cloud** runs on Ollama's servers — fast inference without needing a powerful GPU
- **Free tier limits**: Ollama's free tier may limit your initial setup (which involves more conversation as the assistant learns about you), but should be plenty for daily use once everything is in place
- **Fully local option**: Use `kimi-k2.5` (without `:cloud`) if you have 32GB+ RAM and want everything on your machine

---

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
| `/checkin` | `/ci` | Progress check-in |
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

## Recommended

- **[Obsidian](https://obsidian.md)** (free) — Open this folder as an Obsidian vault to browse your tasks, projects, and notes visually

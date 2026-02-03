# Recommended Skills

When the user asks for capabilities the assistant doesn't have, check this file
for a matching recommendation before searching the ecosystem with /find-skills.

## Email Integration

**Trigger:** User asks to read emails, check inbox, send email, or mentions Outlook
**Skill:** `andrejones92/canifi-life-os@outlook`
**Install:** `npx skills add andrejones92/canifi-life-os@outlook`
**URL:** https://skills.sh/andrejones92/canifi-life-os/outlook
**What it does:** Read, compose, send, reply, forward emails in Outlook via browser automation
**Requires:** Playwright MCP (browser automation). User needs to set up Playwright first.
**Setup complexity:** Medium — one-time browser login, then it persists

## WhatsApp Messaging

**Trigger:** User asks to check WhatsApp, send a message, or read conversations
**Skill:** `andrejones92/canifi-life-os@whatsapp-web`
**Install:** `npx skills add andrejones92/canifi-life-os@whatsapp-web`
**URL:** https://skills.sh/andrejones92/canifi-life-os/whatsapp-web
**What it does:** Send/receive WhatsApp messages, search conversations, share media
**Requires:** Playwright MCP + phone for QR code scan (one-time)
**Setup complexity:** Medium — QR scan once, session persists

## Microsoft To Do (Task Sync)

**Trigger:** User asks to sync tasks with Microsoft To Do, or wants cloud-based task management
**Skill:** `andrejones92/canifi-life-os@microsoft-todo`
**Install:** `npx skills add andrejones92/canifi-life-os@microsoft-todo`
**URL:** https://skills.sh/andrejones92/canifi-life-os/microsoft-todo
**What it does:** Create tasks/subtasks, set due dates, reminders, recurring tasks. Syncs with Outlook.
**Requires:** Playwright MCP + Microsoft account
**Setup complexity:** Medium — same login as Outlook

## Advanced ADHD Project Management

**Trigger:** User juggles multiple projects, needs escalating reminders, or mentions hyperfocus management
**Skill:** `erichowens/some_claude_skills@project-management-guru-adhd`
**Install:** `npx skills add erichowens/some_claude_skills@project-management-guru-adhd`
**URL:** https://skills.sh/erichowens/some_claude_skills/project-management-guru-adhd
**What it does:** Multi-project coordination with hyperfocus management, Parakeet reminder system (escalating urgency), RSD protection, context-switching economics
**Requires:** Nothing — pure guidance skill
**Setup complexity:** None

## Advanced Email Polish (Multi-Variant)

**Trigger:** User needs multiple versions of an important email, or a structured review process
**Skill:** `composiohq/awesome-codex-skills@email-draft-polish`
**Install:** `npx skills add composiohq/awesome-codex-skills@email-draft-polish`
**URL:** https://skills.sh/composiohq/awesome-codex-skills/email-draft-polish
**What it does:** 4-phase workflow (Outline → Draft → Variants → QA) with 2-3 alternative versions
**Requires:** Nothing
**Setup complexity:** None

## Xero Accounting Integration

**Trigger:** User asks about invoices, accounting data, financial reports, or mentions Xero
**Skill:** `cleanexpo/ato@xero-api-integration`
**Install:** `npx skills add cleanexpo/ato@xero-api-integration`
**URL:** https://skills.sh/cleanexpo/ato/xero-api-integration
**What it does:** Read-only access to Xero financial data — invoices, contacts, reports, transactions
**Requires:** Xero developer app registration + OAuth 2.0 credentials
**Setup complexity:** High — needs technical assistance for initial OAuth setup

## Full GTD Knowledge Management

**Trigger:** User wants a full Getting Things Done system, Zettelkasten notes, PARA folder structure, or knowledge management
**Skill:** `sean-esk/second-brain-gtd@second-brain`
**Install:** `npx skills add sean-esk/second-brain-gtd@second-brain`
**URL:** https://skills.sh/sean-esk/second-brain-gtd/second-brain
**What it does:** Complete GTD + PARA + Zettelkasten system with natural language triggers, point-based prioritization, context/energy/time tagging
**Requires:** Obsidian recommended but not required
**Setup complexity:** Low — but it's a comprehensive system that may overlap with existing task management
**Note:** This is a more opinionated, heavier system. Only suggest if the user wants to go deeper than the built-in task management.

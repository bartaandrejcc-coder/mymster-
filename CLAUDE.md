# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is a static GitHub Pages site for **My Master** — a premium auto repair shop in Mukachevo, Ukraine. The repository hosts an AI-powered marketing department system: a set of structured Markdown prompt files (agents, skills, templates) used to coordinate 12 AI marketing agents via Claude/Cowork, plus an interactive HTML dashboard at the root.

The system is designed so that Andrii (the owner) spends ~3 hours/week on marketing while AI agents handle the rest.

## Repository Layout

```
mymster-/
├── index.html                           ← GitHub Pages root dashboard (dark-mode SPA)
├── .nojekyll                            ← disables Jekyll processing on GitHub Pages
└── Маркетинг mymaster/
    └── Маркетинг My master/             ← all project content lives here
        ├── CLAUDE.md                    ← business context for all AI agents (READ THIS)
        ├── README.md
        ├── ACCESS_CHECKLIST.md          ← which integrations are connected vs missing
        ├── dashboard.html               ← secondary dashboard
        ├── agents/                      ← 12 agent definition files (01–12)
        ├── skills/                      ← 13 methodology files agents reference
        ├── templates/                   ← reusable output templates
        └── reports/                     ← weekly/monthly AI-generated reports (initially empty)
```

> The long Cyrillic path (`Маркетинг mymaster/Маркетинг My master/`) is the canonical location. Always use the full path when reading or writing project files.

## The Business Context CLAUDE.md

**`Маркетинг mymaster/Маркетинг My master/CLAUDE.md`** is the authoritative business document that all marketing agents must read first. It contains:
- Full company profile (two business lines: classic auto repair and USA car import)
- Complete service catalogue with `[СТО]` / `[USA]` / `[Обидва]` tags
- ICP (ideal customer profiles), KPIs, brand voice rules, and channel strategy
- Agent roster with activation triggers
- Self-improvement protocol (Section 12): after each session agents propose updates; version bumped on approval
- GitHub workflow (Section 16): commit format, push cadence

When updating `CLAUDE.md`, bump the version number at the bottom and add a changelog entry with the date and reason.

## Agent Files (`agents/`)

Each agent file follows this structure:
- **Роль / Місія** — who this agent is
- **Зона відповідальності** — scope
- **Тригери активації** — when to invoke (natural language triggers)
- **Інструкція** — system prompt with rules and output format
- **Приклади команд** — example invocations
- **Що читати перед роботою** — which files to read first (always includes `CLAUDE.md`)

Agent files are numbered `01`–`12`. Adding a new agent means creating `13_<name>.md` and registering it in `CLAUDE.md` Section 8.

## Skills and Templates

- **`skills/`** — methodology files (how to run a content calendar, SEO audit, Google Ads setup, etc.). Agents reference these as step-by-step playbooks.
- **`templates/`** — output scaffolding (post format, ad copy, monthly plan, review response, etc.). Agents fill these in for specific tasks.

## The Dashboard (`index.html`)

Single-file vanilla JS SPA. The `AGENTS` array in the `<script>` block drives the agent cards — if you add a new agent file, add a corresponding entry here too. No build step, no dependencies; edit directly.

## Two Business Lines — Critical Distinction

Every piece of content, every campaign, every agent task must specify which business line it targets:

| Line | Audience | Avg. ticket | Geography |
|------|----------|-------------|-----------|
| **Classic auto repair [СТО]** | Local Zakarpattia residents | 5k–60k UAH | Mukachevo + region |
| **USA car import [USA]** | All of Ukraine | 100k–400k+ UAH | Nationwide (delivery from Lviv) |

Content, keywords, tone, and CTAs differ significantly between the two. USA cars generate ~48% of site traffic.

## Git Workflow

```bash
# Always commit with descriptive messages:
git add <files>
git commit -m "feat: додано агента 13_email_marketing.md"
git commit -m "update: CLAUDE.md v2.5 — новий канал Telegram"
git commit -m "fix: виправлено шаблон post_template.md"

git push -u origin <branch>
```

Commit after every meaningful change. The `main` branch is the production branch served by GitHub Pages.

## Key Conventions

- **Language**: all content files are in Ukrainian; git commit messages may be Ukrainian or English
- **CLAUDE.md is versioned**: minor edits → `X.Y+1`; strategy overhaul → `X+1.0`. Always update the changelog block at the bottom.
- **Do not delete reports/**: even when empty, the folder must exist for the dashboard links to work
- **No build pipeline**: this is static HTML + Markdown. There is no package.json, no test suite, no linter. "Deploying" means pushing to `main`.
- **`ACCESS_CHECKLIST.md`** tracks which external integrations (Google Analytics, Meta Ads, etc.) are connected — update it when connections change.

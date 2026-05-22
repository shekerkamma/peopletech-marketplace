---
name: peopletech-setup
description: >-
  Show what's installed after peopletech-all plugin setup. Use when the user
  says "what do I have", "list plugins", or "peopletech status".
user_invocable: true
---

# PeopleTech AI Layer — Installed

All 11 plugins were auto-installed as dependencies of `peopletech-all`.
You have **142 skills** available globally across all projects.

## What's installed

| Plugin | Skills | Category |
|--------|--------|----------|
| gstack | 37 | Browser, QA, ship, review, deploy, design |
| ai-analyst | 40 | Product analytics, forecasting, experiments |
| presentation-suite | 10 | Slides, themes, export, architecture decks |
| ai-strategy | 5 | Executive briefs, strategy council, scoring |
| content-tools | 7 | Research ingest, knowledge graphs, diagrams |
| integrations | 16 | Slack, Notion, Linear, Google Ads, etc. |
| dev-tools | 8 | Code review, browser agent, utilities |
| cli-anything | 5 | CLI builder, skill generator |
| peopletech-ai-layer | 4 | Self-improving hooks, MCP, explorer |
| presales-tools | 4 | Contract review, explainer graphics, workflow viz, conversation prep |
| skill-systems | 6 | Orchestrated pipelines: video-to-deck, deal prep, research-to-strategy, analytics-to-comms, architecture-to-everything, competitive intel |

## Post-install (optional)

For `/browse` and `/qa` with headless browser:
```bash
cd ~/.claude/plugins/cache/*/gstack && npm install
```

## Quick test

Try any of these to confirm everything works:
- `/time-skill` — current time
- `/cheat` — start a cheat sheet
- `/analyze` — run product analytics
- `/drawio` — generate a diagram

## Skill Systems (orchestrated pipelines)

These chain multiple child skills end-to-end — one command, walk away:
- `/video-to-deck` — video → insights → explainer → full deck package
- `/presales-deal-prep` — prospect research → strategy brief → contract review → meeting prep
- `/research-to-strategy` — sources → knowledge graph → strategy council → slides
- `/analytics-to-comms` — data question → analysis → infographic → slides → Slack
- `/architecture-to-everything` — system → drawio + doc + pptx + interactive HTML
- `/competitive-intel-sprint` — competitor video/content → scored analysis → exec brief

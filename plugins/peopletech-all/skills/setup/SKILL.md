---
name: peopletech-setup
description: >-
  Use when the user says "setup", "install all plugins", "onboard", or
  "peopletech setup". Installs all 9 PeopleTech plugins from the marketplace.
user_invocable: true
---

# PeopleTech Full Setup

Run this to install all 9 PeopleTech plugins. Execute these commands in sequence:

```bash
claude -p "Run these plugin install commands one by one:
/plugin install gstack@peopletech-marketplace
/plugin install ai-analyst@peopletech-marketplace
/plugin install presentation-suite@peopletech-marketplace
/plugin install ai-strategy@peopletech-marketplace
/plugin install content-tools@peopletech-marketplace
/plugin install integrations@peopletech-marketplace
/plugin install dev-tools@peopletech-marketplace
/plugin install cli-anything@peopletech-marketplace
/plugin install peopletech-ai-layer@peopletech-marketplace"
```

After installation, the user has 132 skills available globally across all projects.

## What gets installed

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

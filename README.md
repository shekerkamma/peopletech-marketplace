# PeopleTech Plugin Marketplace

Private Claude Code plugin marketplace for the PeopleTech AI Engineering team.
**11 plugins, 136 skills** — two commands from zero to full AI Layer.

## Quick Start (2 commands)

```bash
# 1. Register this marketplace (one time)
/plugin marketplace add https://github.com/shekerkamma/peopletech-marketplace

# 2. Install everything — all 10 plugins auto-install as dependencies
/plugin install peopletech-all@peopletech-marketplace
```

That's it. All 136 skills are now available globally.

## Pick and choose (alternative)

Don't want everything? Install individual plugins:

```bash
/plugin install gstack@peopletech-marketplace
/plugin install ai-analyst@peopletech-marketplace
/plugin install presentation-suite@peopletech-marketplace
# ... etc.
```

## Available Plugins

| Plugin | Skills | What it does |
|--------|--------|-------------|
| **peopletech-all** | — | Meta-plugin: auto-installs all 10 plugins below via dependencies |
| **gstack** | 37 | Browser automation, QA, ship, review, deploy, design, investigate, plan reviews, retros |
| **ai-analyst** | 40 | Product analytics: explore data, run analysis, forecast, define metrics, design experiments, cohort analysis |
| **presentation-suite** | 10 | Create slides, themes, export PDF/PNG, speaker notes, accessibility, architecture presentations |
| **ai-strategy** | 5 | Executive briefs, strategy council (5 AI agents), research reports, vertical scoring, LLM council |
| **content-tools** | 7 | Ingest from YouTube/LinkedIn/GitHub/web, knowledge graphs, draw.io, Excalidraw, screenshots |
| **integrations** | 16 | Slack, Notion, Linear, Google Ads, Cal.com, Fireflies, Trigger.dev, Dub, Substack, Hacker News, Podscan, Postman, Firecrawl, Wikipedia, NotebookLM |
| **dev-tools** | 8 | Code review, browser agent, cheat sheets, account briefings, time/weather utilities |
| **cli-anything** | 5 | CLI interface builder for any GUI app, skill generator |
| **peopletech-ai-layer** | 4 | Self-improving CLAUDE.md hooks, review skill, explorer subagent, codebase-search MCP |
| **presales-tools** | 4 | Contract review, explainer graphics, workflow visualization, conversation prep |

## Plugin Details

### gstack (37 skills)

Source: [garrytan/gstack](https://github.com/garrytan/gstack)

`/browse` `/qa` `/ship` `/review` `/investigate` `/design-review` `/plan-ceo-review` `/plan-eng-review` `/retro` `/land-and-deploy` `/canary` `/health` `/checkpoint` `/careful` `/guard` `/freeze` `/autoplan` `/office-hours` and more.

**Note:** For `/browse` and `/qa` with headless browser, also run:
```bash
cd ~/.claude/plugins/cache/*/gstack && npm install
```

### ai-analyst (40 skills)

Full analytics pipeline: `/analyze` then sub-skills for explore-data, run-analysis, forecast, define-metric, design-experiment, question-framing, cohort-analysis, data-quality-check, stakeholder-comms, and 30+ more.

### presentation-suite (10 skills)

`/presentation` `/presentation-theme` `/presentation-exporter` `/presentation-speaker-notes` `/presentation-accessibility` `/presentation-content-writer` `/architecture-presentation`

### ai-strategy (5 skills)

`/ai-strategy-brief` `/ai-strategy-council` `/ai-strategy-researcher` `/vertical-scorer` `/llm-council`

### content-tools (7 skills)

`/content-research` `/graphify` `/drawio` `/excalidraw` `/watch` `/ss` `/archive-is`

### integrations (16 skills)

`/slack` `/notion` `/linear` `/google-ads` `/cal-com` `/fireflies` `/trigger-dev` `/dub` `/substack` `/hackernews` `/podscan` `/postman-explore` `/scrape-creators` `/firecrawl` `/wikipedia` `/notebooklm`

### dev-tools (8 skills)

`/code-review-specialist` `/agent-browser` `/cheat` `/00-account-briefing` `/time-skill` `/time-tokyo` `/weather-fetcher` `/weather-fetcher-tokyo`

### cli-anything (5 skills)

`/cli-anything` `/list` `/refine` `/test` `/validate`

### peopletech-ai-layer (4 components)

Self-improving CLAUDE.md hooks (SessionStart + Stop reflector), customer-facing review skill, read-only explorer subagent, AST-based codebase-search MCP server.

### presales-tools (4 skills)

`/contract-reviewer` `/explainer-graphic` `/workflow-visualizer` `/difficult-conversation-prep`

Enterprise deal toolkit: review contracts and flag risks, create visual explainer infographics, map workflows as interactive HTML diagrams, prepare for tough negotiations with scripts and pushback responses.

## License

Each plugin retains its original license. See individual plugin directories.

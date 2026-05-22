# PeopleTech Plugin Marketplace

Private Claude Code plugin marketplace for the PeopleTech AI Engineering team.

## Installation

### 1. Register this marketplace (one time)

```bash
/plugin marketplace add https://github.com/shekerkamma/peopletech-marketplace
```

### 2. Install plugins

```bash
# Full AI engineering workflow (browser, QA, ship, review, design, etc.)
/plugin install gstack@peopletech-marketplace

# CLI interface builder for any GUI app
/plugin install cli-anything@peopletech-marketplace

# PeopleTech deck workspace AI Layer (hooks, skills, MCP, subagent)
/plugin install peopletech-ai-layer@peopletech-marketplace
```

## Available Plugins

| Plugin | Skills | What it does |
|--------|--------|-------------|
| **gstack** | 35+ | Browser automation, QA testing, code review, ship/deploy, design consultation, investigation, plan reviews, retros |
| **cli-anything** | 5 | Build CLI interfaces for any GUI app, skill generator, harness methodology |
| **peopletech-ai-layer** | 1 | Self-improving CLAUDE.md hooks, customer-facing review skill, explorer subagent, codebase-search MCP |

## Plugin Details

### gstack

Source: [garrytan/gstack](https://github.com/garrytan/gstack)

Key skills: `/browse`, `/qa`, `/ship`, `/review`, `/investigate`, `/design-review`, `/plan-ceo-review`, `/plan-eng-review`, `/retro`, `/land-and-deploy`, `/canary`, `/health`, `/checkpoint`

**Note:** This marketplace packages the skills only (6MB). For the full gstack with headless browser binaries, clone from source:
```bash
git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && npm install
```

### cli-anything

Source: cli-anything contributors

Skills: `/cli-anything`, `/list`, `/refine`, `/test`, `/validate`

### peopletech-ai-layer

Source: PeopleTech AI Engineering

Includes: self-improving CLAUDE.md hooks, customer-facing review skill, read-only explorer subagent, AST-based codebase-search MCP server.

## For Maintainers

To update plugins:
```bash
# Update gstack skills from upstream
cd plugins/gstack
# sync skills from latest garrytan/gstack release
```

## License

Each plugin retains its original license. See individual plugin directories.

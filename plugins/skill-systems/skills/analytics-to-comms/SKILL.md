---
name: analytics-to-comms
description: >-
  End-to-end pipeline: run product analytics → visualize key finding as
  infographic → package into slides → post summary to Slack.
  Use when the user says "analyze and share", "run the numbers and present",
  "data to stakeholders", "analytics pipeline".
user_invocable: true
---

# Analytics-to-Comms Skill System

Orchestrator that chains four child skills to turn a data question into a
stakeholder-ready communication. Input: a business question + data source.
Output: analysis + visual + slides + Slack post.

## Onboarding (first run only)

If `~/.claude/skills/analytics-to-comms/config.json` does not exist, ask:

1. **Slack channel**: Default channel for posting results → default: none (skip Slack)
2. **Audience**: Technical / executive / mixed → default: executive
3. **Visual style**: Infographic / chart-only / both → default: both
4. **Auto-post to Slack?**: Yes (post automatically) / No (draft only) → default: No

Save as `config.json`.

## Pipeline

### Stage 1: Analyze → Discover
Invoke the `/analyze` skill (ai-analyst orchestrator).
- Run the full analytics pipeline on the user's question
- Explore data, identify trends, run statistical analysis
- Produce findings with supporting evidence
- Generate charts and data visualizations

**Pass forward:** key findings + charts + supporting data + methodology

### Stage 2: Explainer Graphic → Visualize
Invoke the `/explainer-graphic` skill on the #1 finding.
- Find an analogy that makes the key insight accessible to non-technical stakeholders
- Create a visual brief or self-contained HTML infographic
- Focus on the single most important takeaway

**Pass forward:** infographic HTML + visual brief + key insight statement

### Stage 3: Presentation → Package
Invoke the `/presentation` skill.
- Build a concise slide deck (5-7 slides, not the full 10)
- Slides: question → methodology → key finding → supporting data → recommendation → next steps
- Embed the infographic concept as a visual slide
- Add speaker notes for each slide

**Pass forward:** slide deck + executive summary

### Stage 4: Slack → Distribute (if enabled)
Invoke the `/slack` skill.
- Format a Slack message with: one-line finding, key metric, recommendation
- Attach or link to the slide deck
- Post to the configured channel (or draft for review)
- If Slack not configured: skip and print the message to terminal

**Output files:**
```
<topic>-analysis.md
<topic>-explainer.html
<topic>-analytics-deck.pptx
<topic>-slack-draft.md              (if Slack not auto-posted)
```

## Completion

After all stages:
1. Print the **headline finding** in one sentence
2. Show the key metric
3. List all output files
4. Confirm Slack status (posted / drafted / skipped)

## Example usage

```
/analytics-to-comms "Why did retention drop 15% in Q1?" data.csv
/analytics-to-comms "Which plant has the highest defect rate?" — use the ops dashboard
/analytics-to-comms config
```

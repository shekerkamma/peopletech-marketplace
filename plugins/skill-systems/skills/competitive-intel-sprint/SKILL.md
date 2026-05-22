---
name: competitive-intel-sprint
description: >-
  End-to-end pipeline: watch competitor's demo video → ingest their content →
  deep research → score the vertical opportunity → output executive brief.
  Use when the user says "competitive analysis", "analyze this competitor",
  "intel sprint", "what are they doing", or provides a competitor URL/video.
user_invocable: true
---

# Competitive Intel Sprint Skill System

Orchestrator that chains five child skills to produce a complete competitive
intelligence report from a single competitor input (video, website, content).
Input: competitor name + source material. Output: scored analysis + executive brief.

## Onboarding (first run only)

If `~/.claude/skills/competitive-intel-sprint/config.json` does not exist, ask:

1. **Your company**: Who are you? → default: PeopleTech
2. **Your vertical**: Your primary market → default: AI plant operations / manufacturing
3. **Comparison depth**: Quick (3 dimensions) / Standard (6) / Deep (10+) → default: Standard
4. **Output format**: Brief only / brief + slides / full report → default: brief + slides

Save as `config.json`.

## Pipeline

### Stage 1: Watch → Observe (if video provided)
Invoke the `/watch` skill on the competitor's demo/presentation video.
- Extract their positioning, feature claims, pricing signals, target audience
- Note visual design choices, UI patterns, demo flow
- Capture exact quotes and claims for fact-checking
- If no video: skip to Stage 2 with URLs/docs instead

**Pass forward:** competitor claims + positioning + feature list + quotes

### Stage 2: Content Research → Ingest
Invoke the `/content-research` skill, enriched with deeper research tools:
- Use **`/firecrawl`** to scrape the competitor's website (product pages, pricing, case studies, job postings for tech stack clues)
- Use **Exa** (`web_search_exa` with `category:company`) for company profile, funding, leadership, recent coverage
- Use **`/hackernews`** to search for community sentiment, discussions, and complaints about the competitor
- Use **`/podscan`** to find podcast episodes mentioning the competitor (founder interviews, analyst takes)
- Use **`/content-research`** to ingest any additional sources (blog, social, docs)
- Do NOT fall back to basic WebSearch — always prefer the richer tools above
- Map their product capabilities, integrations, and tech stack
- Identify their go-to-market strategy and target segments
- Extract customer testimonials, case studies, pricing

**Pass forward:** competitor profile + capabilities map + GTM strategy + community sentiment

### Stage 3: AI Strategy Research → Contextualize
Invoke the `/ai-strategy-researcher` skill.
- Research the broader market context the competitor operates in
- Identify market trends, regulatory landscape, technology shifts
- Map where the competitor sits relative to market trajectory
- Find gaps and whitespace they aren't addressing

**Pass forward:** market context + competitor positioning + gaps identified

### Stage 4: Vertical Scorer → Evaluate
Invoke the `/vertical-scorer` skill.
- Score the competitor's vertical opportunity vs yours
- Evaluate across: market size, defensibility, AI leverage, go-to-market fit
- Produce a quantified comparison matrix
- Identify where you win, where they win, and where it's contested

**Pass forward:** scores + comparison matrix + win/loss dimensions

### Stage 5: AI Strategy Brief → Deliver
Invoke the `/ai-strategy-brief` skill.
- Generate a one-page executive brief summarizing the competitive analysis
- Frame findings as actionable intelligence (not just observations)
- Include: competitive positioning, threat assessment, recommended response
- Highlight the 3 things you should do differently based on this analysis

**Output files:**
```
<competitor>-intel-research.md
<competitor>-market-context.md
<competitor>-vertical-score.md
<competitor>-competitive-brief.md
<competitor>-intel-deck.pptx          (if slides enabled)
```

## Completion

After all stages:
1. Print the **threat level**: Low / Medium / High / Critical
2. Print **3 actionable takeaways** — what to do next
3. Show the win/loss matrix (where you beat them, where they beat you)
4. List all output files
5. Offer: "Want me to draft a counter-positioning strategy?"

## Example usage

```
/competitive-intel-sprint Siemens MindSphere https://youtube.com/watch?v=...
/competitive-intel-sprint "Rockwell Automation" — check their website and recent LinkedIn posts
/competitive-intel-sprint config
```

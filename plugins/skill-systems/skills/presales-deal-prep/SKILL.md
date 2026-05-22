---
name: presales-deal-prep
description: >-
  End-to-end pre-sales pipeline: research a prospect → generate AI strategy brief
  → review contract terms → prep for the meeting with objection scripts.
  Use when the user says "prep for a meeting with", "deal prep", "pre-sales prep",
  "get me ready for the pitch", or mentions a prospect/client meeting.
user_invocable: true
---

# Pre-Sales Deal Prep Skill System

Orchestrator that chains four child skills to prepare you completely for an
enterprise sales meeting. Input: a company name and context. Output: everything
you need to walk in confident.

## Onboarding (first run only)

If `~/.claude/skills/presales-deal-prep/config.json` does not exist, ask:

1. **Your company name**: Who are you representing? → default: PeopleTech
2. **Your offering**: One-line description of what you sell → default: AI-powered plant operations
3. **Default vertical**: Industry focus → default: manufacturing / automotive
4. **Include contract review?** Yes/No → default: Yes
5. **Output format**: Markdown / slides / both → default: both

Save as `config.json`.

## Pipeline

### Stage 1: Account Briefing → Research
Invoke the `/00-account-briefing` skill.
- Research the prospect company (size, industry, recent news, key people)
- Identify their likely pain points relevant to your offering
- Surface any recent announcements, earnings, or strategic shifts
- Find connections between their goals and your solution

**Pass forward:** company profile + pain points + opportunity angles

### Stage 2: AI Strategy Brief → Position
Invoke the `/ai-strategy-brief` skill.
- Generate a one-page executive brief tailored to the prospect's vertical
- Frame your offering against their specific challenges
- Include market context, competitive landscape, and ROI potential
- Produce concrete recommendations (not generic AI hype)

**Pass forward:** strategy brief + positioning angles + ROI framing

### Stage 3: Contract Review → Protect (if enabled)
Invoke the `/contract-reviewer` skill.
- If the user provides a contract/terms document: review it fully
- Flag red flags, yellow flags, missing protections
- Generate negotiation scripts for each concern
- If no contract provided: skip this stage and note it in the final output

**Pass forward:** contract risk summary + negotiation scripts

### Stage 4: Conversation Prep → Ready
Invoke the `/difficult-conversation-prep` skill.
- Build a meeting prep guide with opening lines, talking points, pushback responses
- Tailor to the prospect's likely objections based on Stage 1 research
- Include non-negotiables and walk-away points
- Offer role-play practice

**Output files:**
```
<prospect>-account-briefing.md
<prospect>-ai-strategy-brief.md
<prospect>-contract-review.md       (if contract provided)
<prospect>-meeting-prep.md
<prospect>-deal-prep.pptx           (if slides enabled)
```

## Completion

After all stages:
1. Print a **one-page cheat sheet** combining: 3 key facts about the prospect, your positioning angle, top 3 objections with responses, and your opening line
2. List all output files
3. Offer role-play: "Want to practice? I'll play the prospect."

## Example usage

```
/presales-deal-prep Hyundai Motor Group
/presales-deal-prep Samsung Engineering — they're evaluating predictive maintenance vendors
/presales-deal-prep config
```

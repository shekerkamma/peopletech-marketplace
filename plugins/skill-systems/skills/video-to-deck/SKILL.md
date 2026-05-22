---
name: video-to-deck
description: >-
  End-to-end pipeline: watch a video → extract insights → create explainer graphic
  → generate full architecture presentation package (drawio + md + pptx + NotebookLM).
  Use when the user says "turn this video into a deck", "video to slides",
  "video to presentation", or pastes a video URL and wants a full deliverable.
user_invocable: true
---

# Video-to-Deck Skill System

Orchestrator that chains four child skills in sequence to turn any video into a
complete presentation package. The user provides a video URL (or local path) and
optionally a focus question. You deliver a full deck package — no manual steps
between stages.

## Onboarding (first run only)

If `~/.claude/skills/video-to-deck/config.json` does not exist, ask these questions
before starting and save the answers:

1. **Deck theme**: "Enterprise Consulting (white)" or "Midnight Executive (dark)"? → default: Enterprise Consulting
2. **Include NotebookLM step?** Yes/No → default: Yes
3. **Auto-open outputs?** Yes/No → default: Yes
4. **Output directory**: Where to save deliverables → default: current working directory

Save as `config.json`:
```json
{
  "theme": "enterprise-consulting",
  "include_notebooklm": true,
  "auto_open": true,
  "output_dir": "."
}
```

On subsequent runs, load config silently. User can reconfigure with `/video-to-deck config`.

## Pipeline

### Stage 1: Watch → Extract
Invoke the `/watch` skill on the provided video URL.
- Extract the full transcript and key visual frames
- Identify the core topic, thesis, and structure
- Produce a structured summary: title, sections, key insights, notable visuals

**Pass forward:** structured summary + transcript + topic name

### Stage 2: Research → Enrich
Invoke the `/content-research` skill on the extracted content.
- Create a research note in second-brain format (if in a project with second-brain/)
- Otherwise create a standalone `<topic>-research.md`
- Extract deck-usable facts, figures, quotes
- Separate internal-only insights from customer-facing content

**Pass forward:** enriched research note + deck-usable content

### Stage 3: Explainer Graphic → Visualize
Invoke the `/explainer-graphic` skill on the core concept.
- Find the killer analogy for the video's main topic
- Map all components to the analogy
- Generate a self-contained HTML infographic
- Save as `<topic>-explainer.html`

**Pass forward:** analogy framework + visual brief

### Stage 4: Architecture Presentation → Package
Invoke the `/architecture-presentation` skill to produce the full package:
- `.drawio` — component-flow diagram based on the video's architecture/concept
- `.md` — architecture explanation document
- `.pptx` — 10-slide deck in the configured theme
- NotebookLM instructions (if enabled in config)

**Output files:**
```
<topic>-research.md
<topic>-explainer.html
<topic>-architecture.drawio
<topic>-architecture.md
<topic>-architecture.pptx
```

## Completion

After all stages complete:
1. List all output files with paths
2. Open the .pptx and .html if auto_open is enabled
3. Provide NotebookLM manual steps if enabled
4. Report total pipeline status

## Error handling

- If `/watch` fails (download error, no transcript): stop and report. Don't proceed with empty content.
- If any stage produces weak output: flag it, continue, and note the quality gap in the final report.
- If the video is >15 minutes: warn the user and suggest focusing on a specific section with `--start`/`--end`.

## Example usage

```
/video-to-deck https://youtube.com/watch?v=abc123
/video-to-deck https://youtube.com/watch?v=abc123 focus on the architecture section
/video-to-deck ./recording.mp4
/video-to-deck config
```

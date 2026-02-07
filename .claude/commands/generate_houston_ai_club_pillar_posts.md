# Generate Houston AI Club Content Pillar LinkedIn Posts

## Objective
Generate LinkedIn-ready posts for Houston AI Club based on a Content Pillar input, focused on practical, learn-by-doing AI insights for the community.

## Inputs
- One Content Pillar markdown file from:
  inputs/pillars/

## Strategy Context (load first)

Before generating any content, load the AI Content Engine strategy layer:

| File | Purpose |
|------|---------|
| `marketing-engine/core/ICPs.md` | Target ICP 1 (Curious Beginner) for Houston AI Club content |
| `marketing-engine/core/brand-voice.md` | Houston AI Club voice rules and ICP 1 tone guidelines |
| `marketing-engine/core/messaging-pillars.md` | Align each variant to a narrative pillar |
| `marketing-engine/core/hook-bank.md` | Select proven ICP 1 hooks for variant openers |
| `marketing-engine/core/content-formats.md` | LinkedIn post structure and best practices |

## Skills to Consult
- houston-ai-club/SKILL.md
- platform-linkedin/SKILL.md

## Instructions
- Read the Content Pillar input carefully.
- Load all Strategy Context files above before writing.
- Translate the core idea into practical, community-friendly insights.
- Generate 10 distinct LinkedIn post variants.
- Each variant must:
  - Use a different hook or framing angle — pull from `marketing-engine/core/hook-bank.md` ICP 1 hooks and adapt to the pillar topic
  - Align to a messaging pillar from `marketing-engine/core/messaging-pillars.md` (rotate across variants)
  - Emphasize practical application or real-world relevance
  - Stay within 250 words
  - Follow LinkedIn formatting best practices from `marketing-engine/core/content-formats.md`
  - Match the Houston AI Club brand voice per `marketing-engine/core/brand-voice.md`
- Avoid sales language.
- Do not invent facts not present in the pillar.

## Output Format
For each variant:
- Label it clearly (e.g. Variant 1 – Practical Insight Hook)
- Include metadata tag:
  ```
  ICP: 1 | Pillar: [pillar name] | Hook Type: [category from hook bank] | Brand: Houston AI Club
  ```
- Separate variants with clear dividers
- Output plain text only

## Output Destination
Write outputs to:
outputs/2026-01/houston-ai-club/

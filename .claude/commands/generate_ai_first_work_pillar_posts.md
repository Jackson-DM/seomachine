# Generate AI-First Work Content Pillar LinkedIn Posts

## Objective
Generate LinkedIn-ready posts for AI-First Work based on a Content Pillar input, reframed for professionals building AI skills to advance their careers.

## Inputs
- One Content Pillar markdown file from:
  inputs/pillars/

## Strategy Context (load first)

Before generating any content, load the AI Content Engine strategy layer:

| File | Purpose |
|------|---------|
| `marketing-engine/core/ICPs.md` | Target ICP 2 (AI-Curious Professional) for AI-First Work content |
| `marketing-engine/core/brand-voice.md` | AI-First Work voice rules and ICP 2 tone guidelines |
| `marketing-engine/core/messaging-pillars.md` | Align each variant to a narrative pillar |
| `marketing-engine/core/hook-bank.md` | Select proven ICP 2 hooks for variant openers |
| `marketing-engine/core/content-formats.md` | LinkedIn post structure and best practices |

## Skills to Consult
- ai-first-work/SKILL.md
- platform-linkedin/SKILL.md

## Instructions
- Read the Content Pillar input carefully.
- Load all Strategy Context files above before writing.
- Reframe the ideas for career growth, learning, and practical skill-building.
- Generate 10 distinct LinkedIn post variants.
- Each variant must:
  - Use a different hook or framing angle — pull from `marketing-engine/core/hook-bank.md` ICP 2 hooks and adapt to the pillar topic
  - Align to a messaging pillar from `marketing-engine/core/messaging-pillars.md` (rotate across variants)
  - Emphasize learning value, career leverage, or practical workflows
  - Stay within 250 words
  - Follow LinkedIn formatting best practices from `marketing-engine/core/content-formats.md`
  - Match the AI-First Work brand voice per `marketing-engine/core/brand-voice.md`
- Avoid meetup or event language.
- Avoid aggressive sales language.
- Do not invent facts not present in the pillar.

## Output Format
For each variant:
- Label it clearly (e.g. Variant 1 – Career Insight Hook)
- Include metadata tag:
  ```
  ICP: 2 | Pillar: [pillar name] | Hook Type: [category from hook bank] | Brand: AI-First Work
  ```
- Separate variants with clear dividers
- Output plain text only

## Output Destination
Write outputs to:
outputs/2026-01/ai-first-work/

# Marketing Automation Workflows — Repo Guide

## What This Repo Is

This repository is a **content automation engine** built using Claude Code inside Cursor.
Its purpose is to turn **small, structured inputs** into **on-brand, LinkedIn-ready content variants** for multiple brands, using reusable skills and deterministic commands.

This repo is **not**:
- A CMS
- A scheduling tool
- A content archive
- A place to dump raw transcripts or ideas

This repo **is**:
- A repeatable content generation system
- A skills-driven automation engine
- A shared internal capability for marketing workflows

---

## Core Design Philosophy

1. **Inputs are normalized**
   - Humans write short, structured markdown inputs
   - No raw transcripts, no pasted meeting logs

2. **Skills define behavior**
   - Brand voice, tone, and platform rules live in `SKILL.md` files
   - Feedback is applied by editing skills, not rewriting prompts

3. **Commands orchestrate**
   - Commands tell Claude *what to do*, not *how to think*
   - Commands remain simple and stable over time

4. **One input → many outputs**
   - The same input can generate content for multiple brands
   - Brand differences are handled entirely by skills

5. **Outputs are drafts**
   - All outputs require human review before posting
   - Outputs are reference artifacts, not final truth

---

## Brands Supported (Phase 1)

### Houston AI Club
- **Audience:** Community members, professionals, builders
- **Tone:** Community-first, practical, welcoming
- **Use case:** Lightning Lesson recaps + practical AI insights

### AI-First Work
- **Audience:** Career-focused learners and upskillers
- **Tone:** Modern mentor, pragmatic, confidence-building
- **Use case:** Reframing insights for career growth and learning

> Note: Amplify Intelligence is intentionally excluded for now to keep scope focused.

---

## Repo Structure (Conceptual)

.claude/
├── skills/ # Brand + platform behavior
├── commands/ # Task orchestration
└── agents/ # (Optional) advanced Claude behaviors

inputs/
├── lightning-lessons/
└── pillars/

outputs/
└── YYYY-MM/
├── houston-ai-club/
└── ai-first-work/


---

## Skills (The "Brains")

### Brand Skills
.claude/skills/houston-ai-club/SKILL.md
.claude/skills/ai-first-work/SKILL.md


Each brand skill defines:
- Audience
- Voice and tone
- Positioning
- What "good" content looks like
- What to avoid

**Rule:**
If content tone feels off → update the SKILL file, **not** the command.

---

### Platform Skill
.claude/skills/platform-linkedin/SKILL.md


Defines:
- Length constraints (≤250 words)
- Structure (hook → value → CTA)
- Formatting rules
- Disallowed patterns (hype, clickbait, hard selling)

---

## Inputs (Source of Truth)

### Lightning Lessons (Monday)

**Folder**
inputs/lightning-lessons/


**Template**
LIGHTNING_LESSON_TEMPLATE.md


Purpose:
- Convert Fireflies / call summaries into clean signal
- Power Monday content generation

Inputs should include:
- TL;DR
- Key takeaways
- Audience definition
- Soft CTA

❌ Do not paste full transcripts
❌ Do not paste raw Fireflies output

---

### Content Pillars (Wednesday)

**Folder**
inputs/pillars/


**Template**
PILLAR_TEMPLATE.md


Purpose:
- Represent evergreen educational themes
- Enable repeatable Wednesday content

Inputs define:
- Core idea
- Key points
- Optional example
- Soft CTA

---

## Commands (Execution Layer)

### Lightning Lesson Commands
generate_monday_lightning_posts.md
generate_ai_first_work_lightning_posts.md


Function:
- Read a Lightning Lesson input
- Apply brand + platform skills
- Generate ~10 LinkedIn variants
- Write outputs to the appropriate brand folder

---

### Content Pillar Commands
generate_houston_ai_club_pillar_posts.md
generate_ai_first_work_pillar_posts.md


Function:
- Read a Content Pillar input
- Generate ~10 LinkedIn variants
- Reframe per brand
- Write outputs to the appropriate brand folder

---

## Outputs (Draft Artifacts)

**Folder structure**
outputs/YYYY-MM/{brand}/


Outputs:
- Are **drafts**
- Are **reviewable artifacts**
- May be selectively committed as examples

Long-term, only reference outputs should be committed.

---

## Weekly Workflow Cadence

- **Monday:** Lightning Lessons
- **Wednesday:** Content Pillars
- **Friday:** (Optional / future) promos

This repo currently supports Monday + Wednesday workflows.

---

## How to Use This Repo (TL;DR)

1. Create or update an input using the appropriate template
2. Run the relevant command in Claude Code
3. Review generated outputs
4. Apply feedback by editing SKILL files
5. Re-run if needed
6. Commit selectively

---

## Super Variant Workflow

Purpose:
Turn a single evaluated content source into multiple
brand-aligned distribution-ready variants.

Inputs:
- Canonical content
- Brand voice (SKILL / brand-voice)
- Phase 2 evaluation output

Process:
1. Use `prompts/super-variant.prompt.md`
2. Fill in bracketed sections using evaluation + canonical content
3. Generate one bundle per brand
4. Save to `/outputs/{month}/{brand}/super_variants/{topic}/`

Outputs:
- Founder LinkedIn (strategic)
- Operator LinkedIn (tactical)
- SEO blog outline + intro
- Email newsletter draft

---

## What This Repo Does NOT Do (By Design)

- No auto-posting
- No scheduling
- No CRM or sales outreach
- No raw data ingestion
- No brand improvisation without a skill

These are Phase 2 concerns.

---

## Final Note

This system is designed to:
- Scale cleanly
- Be easy to reason about
- Be safe to hand off to others
- Encourage consistency over cleverness

If something feels unclear, start by checking:
1. The input template
2. The relevant SKILL.md
3. The command being used

That's almost always where the answer is.

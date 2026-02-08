# Command: Generate Super Variant Bundle

## Purpose
Generate a "Super Variant Bundle" from a single source asset (notes/transcript/blog/pillar) using:
- brand voice
- ICP targeting
- messaging pillars
- hook bank
- format templates

Outputs multiple platform-ready variants + a lightweight evaluation pass to pick top performers.

---

## Inputs (Required)
- **Source:** (paste text or provide path to a file)
- **Brand:** (e.g., "Houston AI Club", "AI First", "Amplify Intelligence")
- **Primary Channel:** (e.g., LinkedIn, X/Twitter, Email, Blog, IG Reel)
- **Goal:** (e.g., awareness, event signups, lead gen, authority)
- **CTA:** (optional but recommended)

## Inputs (Optional)
- **ICP override:** (if you want to force a specific ICP profile)
- **Tone override:** (if you want something like "more founder-y" or "more playful")
- **Length constraints:** (e.g., "LinkedIn under 1,200 chars")

---

## Strategy Context (Where to load from)

### Resolution Order
For each strategy file, resolve using this priority:
1. **Brand-specific override** at `context/brands/<brand-slug>/` (if it exists)
2. **Global default** at `marketing-engine/core/`

### Required Strategy Files
| Strategy File | Global Path | Brand Override Path |
|---|---|---|
| ICP Profiles | `marketing-engine/core/ICPs.md` | `context/brands/<brand-slug>/ICPs.md` |
| Messaging Pillars | `marketing-engine/core/messaging-pillars.md` | `context/brands/<brand-slug>/messaging-pillars.md` |
| Hook Bank | `marketing-engine/core/hook-bank.md` | `context/brands/<brand-slug>/hook-bank.md` |
| Content Formats | `marketing-engine/core/content-formats.md` | `context/brands/<brand-slug>/content-formats.md` |
| Brand Voice | `marketing-engine/core/brand-voice.md` | `context/brands/<brand-slug>/brand-voice.md` |

### Graceful Failure
If a strategy file is missing at both the brand-specific and global paths:
- **Do not silently skip it.** State clearly which file is missing and which fallback (if any) was used.
- Example: `⚠ Missing: marketing-engine/core/hook-bank.md — no brand override found either. Hook selection will use general best practices.`
- Continue generation using reasonable defaults, but note the gap in the Strategy Snapshot.

---

## Output Location
Write output to:

`outputs/super-variants/<brand-slug>/<YYYY-MM-DD>_<source-slug>.md`

Where:
- `<brand-slug>` is kebab-case (e.g., `houston-ai-club`)
- `<source-slug>` is a short kebab-case label (e.g., `ai-slide-tools-lightning-lesson`)

---

## Output Format (Must match)
Create a single markdown file with the following structure:

# Super Variant Bundle

## Source
<what the source is / link / filename>

## Brand
<brand name>

## Goal
<goal>

## Primary Channel
<channel>

## Date Generated
<YYYY-MM-DD>

---

## Strategy Snapshot (Auto)
- ICP: <selected ICP name + 1 sentence why>
- Pillar: <selected pillar + 1 sentence why>
- Hook style: <selected hook pattern>
- CTA: <CTA or "none">

### Sources Loaded
| Strategy File | Source Used |
|---|---|
| ICP Profiles | <path loaded or "MISSING — used defaults"> |
| Messaging Pillars | <path loaded or "MISSING — used defaults"> |
| Hook Bank | <path loaded or "MISSING — used defaults"> |
| Content Formats | <path loaded or "MISSING — used defaults"> |
| Brand Voice | <path loaded or "MISSING — used defaults"> |

---

## Variants (Generate 6–10)
Include a mix of:
- LinkedIn (Founder/Strategic)
- LinkedIn (Tactical/How-to)
- X thread (7–10 tweets)
- Short-form script (30–45s)
- Email (short)
- "Comment bait" / engagement post (tastefully)
- Optional: carousel outline if relevant

For each variant include:

### Variant N: <Type>
**Hook:**
...
**Body:**
...
**CTA:**
...
**Notes:**
- target persona
- style constraints

---

## Evaluation (Lightweight)
Score each variant 1–10 on:
- Brand alignment
- ICP alignment
- Clarity
- Hook strength
- CTA fit

Return:
- Top 1 overall
- Top 1 per channel (if multiple channels)

---

## Execution Steps
1) Ask for any missing inputs (Source, Brand, Primary Channel, Goal).
2) Derive `<brand-slug>` from the Brand input (kebab-case).
3) For each strategy file, check `context/brands/<brand-slug>/` first; fall back to `marketing-engine/core/`. Log which source was used.
4) If any strategy file is missing at both paths, warn clearly and continue with reasonable defaults.
5) Generate 6–10 variants using the loaded strategy constraints.
6) Populate the "Sources Loaded" table in the Strategy Snapshot.
7) Run lightweight evaluation and select winners.
8) Save output to `outputs/super-variants/<brand-slug>/<YYYY-MM-DD>_<source-slug>.md`.

# Generate Social Command

Transform blog content into platform-optimized social media posts for a specific brand. This command extracts key messages from blog mockups and generates multiple social post variants tailored to each platform.

## Usage

```
/generate-social --brand <brand-name> [--source <path>] [--platforms <list>] [--variants N]
```

### Parameters

- `--brand` (required): Brand name matching a directory under `context/brands/`
  - Available brands: `amplify-intelligence`, `houston-ai-club`
- `--source` (optional): Path to specific blog/mockup to repurpose
  - If omitted, selects most recent mockup from `drafts/{brand}/`
- `--platforms` (optional): Comma-separated platform list (default: `linkedin,twitter`)
  - Supported: `linkedin`, `twitter`, `threads`
- `--variants` (optional): Number of post variants per platform (default: 2)

### Examples

```
/generate-social --brand amplify-intelligence
/generate-social --brand houston-ai-club --source drafts/houston-ai-club/imposter-syndrome-ai-mockup-2026-01-21.md
/generate-social --brand amplify-intelligence --platforms linkedin,twitter,threads --variants 3
/generate-social --brand houston-ai-club --platforms linkedin --variants 4
```

## What This Command Does

1. **Validates brand context** - Confirms brand directory and required files exist
2. **Loads brand context** - Reads brand voice and social guidelines
3. **Selects source content** - Uses specified source or most recent mockup
4. **Extracts key messages** - Identifies 3-5 standalone insights from source
5. **Generates variants** - Creates platform-specific posts with different hooks
6. **Applies brand voice** - Validates each post matches brand guidelines
7. **Saves outputs** - Writes social batch file to `drafts/{brand}/social/`

## Process

### Step 0: Load Strategy Context

Before any other step, load the AI Content Engine strategy layer from `marketing-engine/core/`:

| File | Purpose |
|------|---------|
| `marketing-engine/core/ICPs.md` | Identify target ICP for the brand and tailor messaging |
| `marketing-engine/core/brand-voice.md` | Voice and tone rules per ICP and brand property |
| `marketing-engine/core/messaging-pillars.md` | Align posts to narrative pillars |
| `marketing-engine/core/hook-bank.md` | Select proven hooks by ICP for variant openers |
| `marketing-engine/core/content-formats.md` | Platform-specific structure and templates |

Use this context to determine ICP targeting, voice calibration, hook selection, pillar alignment, and format structure for all downstream steps.

### Step 1: Validate Brand Parameter

Before proceeding, verify:

1. The `--brand` parameter was provided
2. The directory `context/brands/{brand}/` exists
3. Both required files are present:
   - `context/brands/{brand}/brand-voice.md`
   - `context/brands/{brand}/social-guidelines.md`

If validation fails, provide a helpful error message:
- Missing brand parameter: List available brands
- Invalid brand: Show correct brand names
- Missing files: Indicate which files need to be created

### Step 2: Load Brand Context

Read and analyze these files:

**Brand Voice** (`@context/brands/{brand}/brand-voice.md`):
- Voice pillars and personality
- Tone guidelines by content type
- Messaging framework and value propositions
- Target audience understanding

**Social Guidelines** (`@context/brands/{brand}/social-guidelines.md`):
- Platform voice calibration
- Hashtag library
- CTA patterns
- Forbidden phrases
- Variant differentiation rules

**Strategy Context** (loaded from Step 0):
- `marketing-engine/core/hook-bank.md` — primary hook formulas by ICP
- `marketing-engine/core/content-formats.md` — platform structure templates
- `marketing-engine/core/messaging-pillars.md` — pillar alignment for each variant

### Step 3: Select Source Content

**If `--source` is provided**:
1. Validate file exists at specified path
2. Verify file is a blog mockup or full draft (check frontmatter)

**If `--source` is omitted**:
1. Scan `drafts/{brand}/` for files matching `*-mockup-*.md`
2. Sort by modification date (most recent first)
3. Select most recent mockup
4. If no mockups found, provide guidance to run `/generate-blogs` first

### Step 4: Extract Key Messages

From the source content, extract:

1. **Core Insight**: The single most important takeaway
2. **Supporting Points**: 2-3 secondary insights that stand alone
3. **Memorable Quote**: Most quotable phrase from the content
4. **Specific Data**: Any statistics, numbers, or concrete examples

**Guidelines**:
- Each message should work independently (no required context)
- Prioritize insights that compress well for social
- Preserve language that made the original resonate
- Note the target audience for each message

### Step 5: Apply Platform Rules

For each platform in `--platforms`, load specifications from:
1. `marketing-engine/core/content-formats.md` (primary platform templates and structure)
2. `/social-content` skill (generic platform best practices)
3. `social-guidelines.md` (brand-specific adaptations)

**Platform Specifications**:

| Platform | Character Limit | Optimal Length | Hashtag Limit |
|----------|-----------------|----------------|---------------|
| LinkedIn | 3,000 | 1,200-1,500 | 3-5 |
| Twitter/X | 280 | 200-240 | 1-2 |
| Threads | 500 | 300-400 | 0-3 |

### Step 6: Generate Post Variants

For each platform, generate N variants using:

**Variant Differentiation**:
- Variant 1: Primary insight + story/experience hook
- Variant 2: Secondary insight + contrarian/framework hook
- Variant 3+: Rotate through messages and hook types

**For each variant**:
1. Select a key message to focus on
2. Choose a hook formula from `marketing-engine/core/hook-bank.md` matched to the target ICP
3. Align the variant to a messaging pillar from `marketing-engine/core/messaging-pillars.md`
4. Apply platform-specific voice calibration per `marketing-engine/core/brand-voice.md`
5. Add appropriate CTA from brand patterns (matched to ICP readiness level)
6. Include hashtags from approved library
7. Validate character count

**Quality Rules**:
- Each variant must focus on ONE key message
- Respect character limits strictly
- Use brand-approved hashtags only
- Vary hooks across variants for same platform

### Step 7: Apply Brand Voice Verification

Use the `/brand-voice review` action to validate each generated post:

1. Does the post sound like this brand?
2. Is the tone appropriate for the platform?
3. Are forbidden phrases avoided?
4. Does the CTA match brand patterns?

**If verification fails**:
- Note issues in output file
- Regenerate with adjustments OR flag for manual review

### Step 8: Save Outputs

Save the social batch to the brand's social drafts directory:

**File Location**: `drafts/{brand}/social/{source-slug}-social-{YYYY-MM-DD}.md`

**Naming Convention**:
- Derive `source-slug` from source filename (remove `-mockup-{date}` suffix)
- Add `-social-` to distinguish from other content types
- Include generation date

**Examples**:
- `drafts/amplify-intelligence/social/ai-pilot-graveyard-social-2026-01-22.md`
- `drafts/houston-ai-club/social/imposter-syndrome-ai-social-2026-01-22.md`

## Output Format

```markdown
---
type: social-batch
brand: {brand}
source: {path/to/source-mockup.md}
generated: {YYYY-MM-DD}
platforms: [linkedin, twitter]
variants_per_platform: 2
status: draft
---

# Social Posts: {Source Title}

**Source**: {source file path}
**Generated**: {YYYY-MM-DD}
**Brand**: {brand}

## Key Messages Extracted

1. **Core Insight**: [One-sentence summary of main point]
2. **Supporting Point**: [Secondary takeaway]
3. **Supporting Point**: [Another takeaway]
4. **Memorable Quote**: "[Most quotable phrase from source]"

---

## LinkedIn Posts

### Variant 1

**Hook Type**: [Story/Contrarian/List/Question]
**Target Message**: [Which key message this focuses on]

```
[Full post content with line breaks preserved]

#Hashtag1 #Hashtag2 #Hashtag3
```

**Character Count**: X/3,000
**CTA Type**: [Engagement/Traffic/Save]
**Voice Check**: [Verified/Needs Review]
**ICP**: [1/2/3]
**Pillar**: [AI Confidence / Career Leverage / Practical Workflows / AI-First Mindset]

---

### Variant 2

**Hook Type**: [Different from Variant 1]
**Target Message**: [Which key message]

```
[Full post content]
```

**Character Count**: X/3,000
**CTA Type**: [Type]
**Voice Check**: [Status]

---

## Twitter/X Posts

### Variant 1

**Hook Type**: [Type]
**Target Message**: [Which key message]

```
[Tweet content - 280 char max]
```

**Character Count**: X/280

---

### Variant 2

**Hook Type**: [Type]
**Target Message**: [Which key message]

```
[Tweet content]
```

**Character Count**: X/280

---

## Brand Voice Checklist

- [ ] Tone matches brand voice guidelines
- [ ] Platform-specific voice adaptations applied
- [ ] No forbidden phrases used
- [ ] CTAs align with brand style
- [ ] Hashtags from approved library

## Usage Recommendations

### Posting Sequence
1. **First**: [Recommended first platform and variant]
2. **24h later**: [Second platform/variant]
3. **48h later**: [Third if applicable]

### A/B Testing
- Test Variant 1 vs Variant 2 on [platform] to compare [hook types]
```

## Output Summary

After generating all posts, provide a summary:

```
## Social Posts Generated

Brand: {brand}
Date: {YYYY-MM-DD}
Source: {source file path}

### Platforms & Variants

| Platform | Variants | Status |
|----------|----------|--------|
| LinkedIn | 2 | Ready |
| Twitter | 2 | Ready |

### Generated File

`drafts/{brand}/social/{filename}.md`

### Key Messages Used

1. {Message 1 summary}
2. {Message 2 summary}
3. {Message 3 summary}

### Next Steps

- Review generated posts for accuracy and brand alignment
- Select preferred variant per platform for publishing
- Schedule posts using your preferred social media tool
- Track engagement to inform future content strategy
```

## Integration with Other Commands

This command is designed to work with:

- **`/brand-voice`**: Apply for voice consistency checks
- **`/social-content`**: Use platform guidelines and templates
- **`/generate-blogs`**: Create source mockups to repurpose

## Quality Standards

Each social batch should:

- [ ] Extract meaningful, standalone key messages from source
- [ ] Generate distinct variants with different hooks
- [ ] Respect platform character limits
- [ ] Use only brand-approved hashtags
- [ ] Match brand voice for each platform
- [ ] Include appropriate CTAs
- [ ] Provide actionable usage recommendations

## Error Handling

**Missing brand parameter**:
```
Error: --brand parameter is required.

Available brands:
- amplify-intelligence
- houston-ai-club

Usage: /generate-social --brand amplify-intelligence
```

**Invalid brand**:
```
Error: Brand '{input}' not found.

Check that the directory exists: context/brands/{input}/

Available brands:
- amplify-intelligence
- houston-ai-club
```

**Missing brand files**:
```
Error: Missing required files for brand '{brand}'.

Required files:
- context/brands/{brand}/brand-voice.md [FOUND/MISSING]
- context/brands/{brand}/social-guidelines.md [FOUND/MISSING]

Create missing files before running this command.
```

**No source content found**:
```
Error: No blog mockups found for brand '{brand}'.

Either:
1. Specify a source file: --source drafts/{brand}/your-file.md
2. Generate mockups first: /generate-blogs --brand {brand}
```

**Invalid platform**:
```
Error: Platform '{input}' not supported.

Supported platforms:
- linkedin
- twitter
- threads

Usage: /generate-social --brand {brand} --platforms linkedin,twitter
```

**Source file not found**:
```
Error: Source file not found: {path}

Verify the file path and try again.
```

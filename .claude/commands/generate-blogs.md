# Generate Blogs Command

Transform social content into blog mockups for a specific brand. This command extracts topics from social posts and generates structured blog outlines ready for expansion.

## Usage

```
/generate-blogs --brand <brand-name> [--count N]
```

### Parameters

- `--brand` (required): Brand name matching a directory under `context/brands/`
  - Available brands: `amplify-intelligence`, `houston-ai-club`
- `--count` (optional): Number of blog mockups to generate (default: 3)

### Examples

```
/generate-blogs --brand amplify-intelligence --count 3
/generate-blogs --brand houston-ai-club --count 2
/generate-blogs --brand amplify-intelligence
```

## What This Command Does

1. **Validates brand context** - Confirms brand directory and required files exist
2. **Loads brand voice** - Reads brand-specific tone, messaging, and style guidelines
3. **Loads social sources** - Reads social posts available for transformation
4. **Extracts blog topics** - Identifies N highest-potential topics from social content
5. **Generates mockups** - Creates blog outlines with brand voice applied
6. **Saves outputs** - Writes mockup files to `drafts/{brand}/`

## Process

### Step 0: Load Strategy Context

Before any other step, load the AI Content Engine strategy layer from `marketing-engine/core/`:

| File | Purpose |
|------|---------|
| `marketing-engine/core/ICPs.md` | Identify target ICP for the brand — tailor blog angle and audience |
| `marketing-engine/core/brand-voice.md` | Voice and tone rules per ICP and brand property |
| `marketing-engine/core/messaging-pillars.md` | Align blog topics to narrative pillars |
| `marketing-engine/core/content-formats.md` | Blog post structure template and best practices |

Use this context to determine ICP targeting, voice calibration, pillar alignment, and content structure for all downstream steps.

### Step 1: Validate Brand Parameter

Before proceeding, verify:

1. The `--brand` parameter was provided
2. The directory `context/brands/{brand}/` exists
3. Both required files are present:
   - `context/brands/{brand}/brand-voice.md`
   - `context/brands/{brand}/social-sources.md`

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
- Writing style guidelines
- Target audience understanding

**Strategy Context** (loaded from Step 0):
- `marketing-engine/core/ICPs.md` — detailed ICP profile for audience targeting
- `marketing-engine/core/brand-voice.md` — canonical voice rules (takes precedence for ICP-specific tone)
- `marketing-engine/core/messaging-pillars.md` — pillar alignment for blog topic framing

**Social Sources** (`@context/brands/{brand}/social-sources.md`):
- Available social posts with engagement data
- Extracted topics and themes
- Expansion potential ratings
- Suggested blog angles

### Step 3: Extract Blog Topics

From the social sources, select the top N topics based on:

1. **Expansion potential**: Prioritize High > Medium-High > Medium
2. **Engagement metrics**: Higher engagement suggests resonant topics
3. **Content variety**: Avoid selecting multiple posts on the same theme
4. **Blog angle clarity**: Prefer posts with clear expansion directions

For each selected topic, note:
- Original post summary
- Core theme/message
- Target angle for blog expansion
- Key points to preserve from original

### Step 4: Generate Blog Mockups

For each selected topic, create a **mockup** (NOT full content):

**Mockup Structure**:

```markdown
---
type: blog-mockup
brand: {brand}
icp: {1/2/3}
pillar: {AI Confidence / Career Leverage / Practical Workflows / AI-First Mindset}
source_post: {post identifier from social-sources.md}
generated: {YYYY-MM-DD}
status: draft
---

# [Proposed Blog Title]

## Overview

**Topic**: [One sentence describing the core topic]
**Angle**: [Specific perspective or approach for this blog]
**Target Audience**: [Who this blog is for]
**Primary Value**: [What readers will gain]

## Proposed Outline

### Introduction
- Hook: [Proposed opening hook, 1-2 sentences]
- Problem/Context: [What challenge or question this addresses]
- Promise: [What the reader will learn]

### Section 1: [Section Title]
- Key point: [Main idea for this section]
- Supporting content: [Types of content to include - examples, data, stories]
- Takeaway: [What reader should understand after this section]

### Section 2: [Section Title]
- Key point: [Main idea]
- Supporting content: [What to include]
- Takeaway: [Reader understanding]

### Section 3: [Section Title]
- Key point: [Main idea]
- Supporting content: [What to include]
- Takeaway: [Reader understanding]

### [Additional sections as needed...]

### Conclusion
- Key takeaways: [3-5 main points to reinforce]
- Call to action: [What reader should do next]
- Closing thought: [How to end on brand]

## Brand Voice Notes

**Tone for this piece**: [Specific tone from brand voice guidelines]
**Key messages to weave in**: [Relevant core brand messages]
**Voice pillar focus**: [Which pillars are most relevant]

## Expansion Guidance

**Estimated word count**: [Target length based on topic depth]
**Research needed**: [What additional research or examples would strengthen this]
**Internal links**: [Potential internal linking opportunities]
**SEO considerations**: [Target keywords, search intent]

## Source Material

**Original Post**:
> [Quote the original social post in full]

**What made this post resonate**:
- [Insight 1]
- [Insight 2]
- [Insight 3]

**Elements to preserve in blog**:
- [Key phrase, story, or concept to keep]
- [Another element]
```

### Step 5: Apply Brand Voice

Before finalizing each mockup, verify alignment with brand voice using `marketing-engine/core/brand-voice.md` as the primary authority:

1. **Voice Check**: Does the proposed title and outline match the ICP-specific voice from `marketing-engine/core/brand-voice.md`?
2. **Tone Match**: Is the tone appropriate for the content type (educational, strategic, etc.)?
3. **Pillar Alignment**: Does the blog align to a messaging pillar from `marketing-engine/core/messaging-pillars.md`?
4. **Message Alignment**: Do the proposed sections support core brand messages?
5. **Audience Fit**: Will this resonate with the target ICP as defined in `marketing-engine/core/ICPs.md`?

Use the `/brand-voice check` action to validate, adjust as needed.

### Step 6: Save Outputs

Save each mockup to the brand's drafts directory:

**File Location**: `drafts/{brand}/[topic-slug]-mockup-[YYYY-MM-DD].md`

**Naming Convention**:
- Lowercase
- Hyphenated words
- Include `-mockup-` to distinguish from full drafts
- Include generation date

**Examples**:
- `drafts/amplify-intelligence/ai-pilot-graveyard-mockup-2025-01-21.md`
- `drafts/houston-ai-club/imposter-syndrome-ai-mockup-2025-01-21.md`

## Output Summary

After generating all mockups, provide a summary:

```
## Blog Mockups Generated

Brand: {brand}
Date: {YYYY-MM-DD}
Count: {N} mockups

### Generated Files

1. `drafts/{brand}/{filename1}.md`
   - Topic: {topic summary}
   - Source: {original post identifier}

2. `drafts/{brand}/{filename2}.md`
   - Topic: {topic summary}
   - Source: {original post identifier}

3. `drafts/{brand}/{filename3}.md`
   - Topic: {topic summary}
   - Source: {original post identifier}

### Next Steps

- Review mockups for accuracy and brand alignment
- Expand selected mockups using `/write` command
- Apply brand voice refinement with `/brand-voice review`
```

## Integration with Other Commands

This command is designed to work with:

- **`/brand-voice`**: Apply for voice consistency checks
- **`/write`**: Expand mockups into full blog posts
- **`/research`**: Deep-dive on topics before expansion
- **`/optimize`**: Polish completed drafts

## Quality Standards

Each mockup should:

- [ ] Clearly capture the original post's core insight
- [ ] Propose a logical, scannable outline structure
- [ ] Align with brand voice guidelines
- [ ] Include specific, actionable expansion guidance
- [ ] Preserve the elements that made the original resonate
- [ ] Target appropriate word count for the topic depth
- [ ] Identify potential SEO and linking opportunities

## Error Handling

**Missing brand parameter**:
```
Error: --brand parameter is required.

Available brands:
- amplify-intelligence
- houston-ai-club

Usage: /generate-blogs --brand amplify-intelligence --count 3
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
- context/brands/{brand}/social-sources.md [FOUND/MISSING]

Create missing files before running this command.
```

**No social sources available**:
```
Error: No social content sources found for brand '{brand}'.

Add social posts to: context/brands/{brand}/social-sources.md

See existing brand files for format examples.
```

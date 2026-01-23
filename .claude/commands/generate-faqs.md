# Generate FAQs Command

Extract SEO-optimized FAQ content from blog mockups for a specific brand. This command analyzes blog content and generates structured, schema-ready FAQs grouped into thematic categories.

## Usage

```
/generate-faqs --brand <brand-name> [--source <path>] [--count N] [--format <type>]
```

### Parameters

- `--brand` (required): Brand name matching a directory under `context/brands/`
  - Available brands: `amplify-intelligence`, `houston-ai-club`
- `--source` (optional): Path to specific blog/mockup to extract FAQs from
  - If omitted, selects most recent mockup from `drafts/{brand}/`
- `--count` (optional): Number of FAQs to generate (default: 10)
- `--format` (optional): Output format (default: `standard`)
  - `standard`: Markdown with short + expanded answers
  - `schema`: Includes JSON-LD structured data for FAQ rich snippets

### Examples

```
/generate-faqs --brand amplify-intelligence
/generate-faqs --brand houston-ai-club --count 15
/generate-faqs --brand amplify-intelligence --source drafts/amplify-intelligence/ai-pilot-graveyard-mockup-2026-01-21.md
/generate-faqs --brand houston-ai-club --format schema
/generate-faqs --brand amplify-intelligence --count 8 --format schema
```

## What This Command Does

1. **Validates brand context** - Confirms brand directory and brand-voice.md exist
2. **Loads brand context** - Reads brand voice for tone and style
3. **Selects source content** - Uses specified source or most recent mockup
4. **Analyzes content** - Identifies key topics, concepts, and pain points
5. **Generates FAQ clusters** - Groups questions into 2-4 thematic categories
6. **Generates questions** - Creates SEO-friendly questions using proven patterns
7. **Generates answers** - Short answer (required) + expanded answer (optional)
8. **Applies brand voice** - Validates tone matches brand guidelines
9. **Saves outputs** - Writes FAQ file to `drafts/{brand}/faqs/`

## Process

### Step 1: Validate Brand Parameter

Before proceeding, verify:

1. The `--brand` parameter was provided
2. The directory `context/brands/{brand}/` exists
3. Required file is present:
   - `context/brands/{brand}/brand-voice.md`

If validation fails, provide a helpful error message:
- Missing brand parameter: List available brands
- Invalid brand: Show correct brand names
- Missing files: Indicate which files need to be created

### Step 2: Load Brand Context

Read and analyze the brand voice file:

**Brand Voice** (`@context/brands/{brand}/brand-voice.md`):
- Voice pillars and personality
- Tone guidelines by content type
- Target audience understanding
- Writing style guidelines
- Forbidden phrases to avoid

### Step 3: Select Source Content

**If `--source` is provided**:
1. Validate file exists at specified path
2. Verify file is a blog mockup or full draft (check frontmatter)

**If `--source` is omitted**:
1. Scan `drafts/{brand}/` for files matching `*-mockup-*.md`
2. Sort by modification date (most recent first)
3. Select most recent mockup
4. If no mockups found, provide guidance to run `/generate-blogs` first

### Step 4: Analyze Content for FAQ Topics

From the source content, identify:

1. **Key Concepts** - Terms and ideas that need explanation
2. **Pain Points** - Problems the content addresses
3. **How-To Elements** - Processes and methods described
4. **Common Objections** - Concerns the target audience might have
5. **Comparisons** - Distinctions between related concepts

**Guidelines**:
- Focus on what readers would actually search for
- Prioritize questions with clear, actionable answers
- Extract questions that can stand alone without full context

### Step 5: Generate FAQ Categories

Group questions into 2-4 thematic clusters based on content structure.

**Typical Categories**:
- **Understanding [Topic]** - Definition and concept questions
- **Getting Started** - How-to and implementation questions
- **Common Challenges** - Problem-solving and troubleshooting questions
- **Strategy & Best Practices** - Why and decision-making questions

### Step 6: Generate Questions

Use SEO-friendly question patterns from `/programmatic-seo` skill:

**Question Types**:
1. **Definition**: "What is [concept]?" - for key terms
2. **How-to**: "How do I [action]?" - for practical guidance
3. **Why**: "Why does [thing happen]?" - for explaining causes
4. **Comparison**: "What's the difference between [X] and [Y]?"
5. **Troubleshooting**: "Why isn't [thing] working?" - for common problems

**Question Guidelines**:
- Use natural language (how people actually search)
- Include the target keyword naturally
- Keep questions concise and specific
- Avoid jargon unless the audience expects it

### Step 7: Generate Answers

For each question, generate:

**Short Answer** (required):
- 1-2 sentences, 40-60 words
- Directly answers the question
- Snippet-ready for Google featured snippets
- No filler phrases or preambles
- Front-load the key information

**Expanded Answer** (optional, for complex topics):
- 2-3 paragraphs
- Additional context, examples, nuance
- Internal linking opportunities
- Only include when the topic warrants depth

### Step 8: Apply Brand Voice Verification

Use the `/brand-voice review` action to validate FAQ content:

1. Do answers sound like this brand?
2. Is the tone appropriate for FAQs (clear, helpful)?
3. Are forbidden phrases avoided?
4. Is technical jargon explained appropriately for the audience?

**Brand-Specific Considerations**:
- **Amplify Intelligence**: Expert, consultative, outcome-focused answers
- **Houston AI Club**: Warm, encouraging, community-focused answers

### Step 9: Save Outputs

Save the FAQ set to the brand's FAQ drafts directory:

**File Location**: `drafts/{brand}/faqs/{source-slug}-faqs-{YYYY-MM-DD}.md`

**Naming Convention**:
- Derive `source-slug` from source filename (remove `-mockup-{date}` suffix)
- Add `-faqs-` to distinguish from other content types
- Include generation date

**Examples**:
- `drafts/amplify-intelligence/faqs/ai-pilot-graveyard-faqs-2026-01-22.md`
- `drafts/houston-ai-club/faqs/imposter-syndrome-ai-faqs-2026-01-22.md`

## Output Format

```markdown
---
type: faq-set
brand: {brand}
source: {path/to/source-mockup.md}
generated: {YYYY-MM-DD}
faq_count: {count}
categories: {number of categories}
format: {standard|schema}
status: draft
---

# FAQs: {Source Title}

**Source**: {source file path}
**Generated**: {YYYY-MM-DD}
**Brand**: {brand}
**Total FAQs**: {count}

---

## Category 1: {Category Name}

### Q: {Question text}?

**Short Answer**: {1-2 sentence direct answer that front-loads key information}

**Expanded Answer**:
{Optional 2-3 paragraph explanation with examples and context. Only include for complex topics that warrant additional depth.}

---

### Q: {Question text}?

**Short Answer**: {Direct answer}

---

## Category 2: {Category Name}

### Q: {Question text}?

**Short Answer**: {Direct answer}

**Expanded Answer**:
{Detailed explanation if needed}

---

[Additional categories and FAQs...]

---

## Schema-Ready JSON-LD (if --format schema)

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "{Question 1}",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "{Short answer 1}"
      }
    },
    {
      "@type": "Question",
      "name": "{Question 2}",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "{Short answer 2}"
      }
    }
  ]
}
```

---

## Brand Voice Checklist

- [ ] Questions use natural language (how people actually search)
- [ ] Answers match brand tone (expert/consultative OR warm/community)
- [ ] No forbidden phrases from brand guidelines
- [ ] Technical terms explained appropriately for audience
- [ ] Short answers are snippet-ready (40-60 words, front-loaded)

## SEO Notes

- [ ] Questions follow search patterns ("What is...", "How do I...", "Why does...")
- [ ] Short answers optimized for featured snippets
- [ ] Categories enable internal linking opportunities
- [ ] Schema markup ready for FAQ rich snippets (if --format schema)
```

## Output Summary

After generating all FAQs, provide a summary:

```
## FAQs Generated

Brand: {brand}
Date: {YYYY-MM-DD}
Source: {source file path}

### FAQ Summary

| Category | FAQs | Topics |
|----------|------|--------|
| {Category 1} | 3 | {brief topic list} |
| {Category 2} | 4 | {brief topic list} |
| {Category 3} | 3 | {brief topic list} |

**Total**: {count} FAQs in {N} categories

### Generated File

`drafts/{brand}/faqs/{filename}.md`

### Next Steps

- Review FAQs for accuracy and brand alignment
- Add expanded answers where appropriate
- Integrate into website FAQ section or blog posts
- Add schema markup to page for rich snippets
```

## Integration with Other Commands

This command is designed to work with:

- **`/brand-voice`**: Apply for voice consistency checks
- **`/programmatic-seo`**: Use question patterns and schema structure
- **`/generate-blogs`**: Create source mockups to extract FAQs from
- **`/generate-social`**: FAQs can inform social content topics

## Quality Standards

Each FAQ set should:

- [ ] Extract relevant questions from source content
- [ ] Group FAQs into 2-4 logical categories
- [ ] Use SEO-friendly question phrasing
- [ ] Provide snippet-ready short answers (40-60 words)
- [ ] Match brand voice in all answers
- [ ] Include schema markup when requested
- [ ] Cover the key topics from the source content

## Error Handling

**Missing brand parameter**:
```
Error: --brand parameter is required.

Available brands:
- amplify-intelligence
- houston-ai-club

Usage: /generate-faqs --brand amplify-intelligence
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

Create missing files before running this command.
```

**No source content found**:
```
Error: No blog mockups found for brand '{brand}'.

Either:
1. Specify a source file: --source drafts/{brand}/your-file.md
2. Generate mockups first: /generate-blogs --brand {brand}
```

**Invalid format**:
```
Error: Invalid format '{input}'.

Supported formats:
- standard (default): Markdown with short + expanded answers
- schema: Includes JSON-LD structured data for FAQ rich snippets

Usage: /generate-faqs --brand {brand} --format schema
```

**Invalid count**:
```
Error: Count must be between 1 and 30.

Usage: /generate-faqs --brand {brand} --count 10
```

**Source file not found**:
```
Error: Source file not found: {path}

Verify the file path and try again.
```

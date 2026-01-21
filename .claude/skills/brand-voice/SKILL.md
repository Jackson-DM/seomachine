---
name: brand-voice
description: Apply and verify brand voice guidelines when writing or reviewing content. Use this skill to ensure content matches your brand's tone, messaging framework, and style guidelines defined in context/brand-voice.md.
---

# Brand Voice Skill

Use this skill to write content that matches your brand voice or to review existing content for brand voice compliance.

## Usage

```
/brand-voice [action] [content or topic]
```

### Actions

- **write**: Write new content following brand voice guidelines
- **review**: Review existing content for brand voice compliance
- **check**: Quick brand voice checklist verification

## Process

### Step 1: Load Brand Voice Context

First, read the brand voice guidelines from `@context/brand-voice.md` to understand:

- **Voice Pillars**: The core personality traits that define how the brand communicates
- **Tone Guidelines**: General tone and variations by content type
- **Messaging Framework**: Core brand messages and value propositions
- **Writing Style**: Sentence structure, paragraph structure, word choice, terminology
- **Formatting Rules**: Headlines, subheadings, lists, CTAs
- **Target Audience**: Who the content is for and what they care about

### Step 2: Apply Voice Pillars

For each piece of content, ensure it embodies the defined voice pillars:

1. Review each voice pillar's definition
2. Check that the content demonstrates "how it sounds"
3. Verify the content avoids what each pillar says to avoid
4. Use the example sentences as style reference

### Step 3: Match Tone to Content Type

Adjust tone based on content type as defined in the tone guidelines:

- **How-To Guides**: Follow the tone and phrases specified for tutorials
- **Strategy/Advice**: Use the strategic content tone
- **Industry News/Trends**: Apply news/trends tone
- **Product/Feature Content**: Use product content tone

### Step 4: Integrate Core Messages

Weave in brand messages where appropriate:

1. Identify which core messages apply to this content
2. Include supporting key points naturally
3. Ensure messaging aligns with the defined usage contexts

### Step 5: Apply Writing Style

Follow the defined writing style guidelines:

**Sentence Structure**:
- Apply the specified sentence length and variety preferences
- Use active voice as prescribed
- Prioritize clarity per the guidelines

**Paragraph Structure**:
- Follow length guidelines
- One idea per paragraph
- Use transitions as specified

**Word Choice**:
- Apply the defined characteristics
- Use preferred terminology
- Avoid discouraged words and phrases

**Terminology**:
- Use "Say This" terms, not "Not That" terms
- Maintain industry-appropriate language

### Step 6: Format Correctly

Apply content formatting rules:

- **Headlines**: Follow all headline rules
- **Subheadings**: Apply subheading guidelines
- **Lists**: Format lists per guidelines
- **CTAs**: Structure calls-to-action correctly

## Review Mode

When reviewing existing content, evaluate against:

### Voice Checklist
- [ ] Demonstrates each voice pillar appropriately
- [ ] Avoids anti-patterns for each pillar
- [ ] Matches example tone from brand voice file

### Tone Checklist
- [ ] Tone matches content type
- [ ] Uses appropriate phrases for content type
- [ ] General tone aligns with brand personality

### Messaging Checklist
- [ ] Includes relevant core brand messages
- [ ] Value propositions clear for target segment
- [ ] Key points naturally integrated

### Style Checklist
- [ ] Sentence structure follows guidelines
- [ ] Paragraph structure correct
- [ ] Word choice matches preferences
- [ ] Correct terminology used
- [ ] No discouraged terms present

### Format Checklist
- [ ] Headlines follow all rules
- [ ] Subheadings properly structured
- [ ] Lists formatted correctly
- [ ] CTAs present and effective

### Audience Checklist
- [ ] Written for defined primary audience
- [ ] Addresses their priorities
- [ ] Acknowledges their pain points
- [ ] Serves them per defined principles

## Output

### For Write Action
Provide content that:
1. Fully embodies the brand voice
2. Uses correct tone for content type
3. Integrates core messages naturally
4. Follows all style and format guidelines
5. Serves the target audience effectively

### For Review Action
Provide:
1. Overall brand voice score (1-10)
2. Completed checklist with pass/fail for each item
3. Specific issues identified with line references
4. Concrete suggestions for improvement
5. Example rewrites for problem sections

### For Check Action
Quick verification output:
1. Voice alignment: Pass/Needs Work
2. Tone match: Pass/Needs Work
3. Style compliance: Pass/Needs Work
4. Top 3 issues to fix (if any)

## Quality Standards

Content passes brand voice review when:

- [ ] Sounds like the brand (matches voice pillars)
- [ ] Tone appropriate for content type and audience
- [ ] Provides genuine, actionable value
- [ ] Complex concepts explained simply
- [ ] Technical information accurate
- [ ] Relevant examples included
- [ ] Clear next steps or takeaways
- [ ] Aligns with core brand messages
- [ ] Uses correct terminology
- [ ] Empowers audience to feel capable

## Examples

### Example 1: Write in Brand Voice
```
/brand-voice write "Introduction paragraph for a blog post about email marketing best practices"
```

### Example 2: Review Content
```
/brand-voice review [paste content or file path]
```

### Example 3: Quick Check
```
/brand-voice check "Does this paragraph match our voice: [content]"
```

## Important Notes

- Always read `context/brand-voice.md` before writing or reviewing
- If brand-voice.md is not configured (still has template placeholders), inform the user they need to fill it out first
- Reference specific sections of brand-voice.md when giving feedback
- Be specific about which voice pillar, tone guideline, or style rule applies
- Provide concrete examples when suggesting improvements

# Content Workflows – SEO Machine

This document outlines the repeatable content workflows used to research, draft, and package SEO-focused blog content for small businesses.

Each workflow is designed to be:
- Repeatable
- Scalable
- SEO-informed
- Easy to hand off or automate further

---

## Workflow #1: SEO Blog Creation from Research to Draft

### Goal
Create a high-quality, SEO-optimized blog post for small business audiences using structured research and AI-assisted drafting.

---

### Inputs
- Primary topic or keyword
- SEO research file  
  Example:
  - `research/ai-consulting-research.md`

---

### Tools Used
- Cursor (AI-assisted writing & repo navigation)
- Markdown
- PowerShell (word count validation)

---

### Step-by-Step Process

#### 1. SEO Research
- Analyze search intent (informational, commercial, transactional)
- Identify primary and secondary keywords
- Generate blog angles and outlines
- Document findings in a dedicated research file

📄 Output:
- `research/ai-consulting-research.md`

---

#### 2. Blog Draft Generation
- Use the research file as context
- Generate a long-form (1,200–1,500 words) SEO-friendly draft
- Structure content with:
  - Clear headings (H2/H3)
  - Beginner-friendly explanations
  - Business-focused examples
  - Natural keyword usage

📄 Output:
- `drafts/ai-consulting-for-small-business.md`

---

#### 3. Quality Control
- Check word count using PowerShell:
  ```powershell
  (Get-Content 'drafts/ai-consulting-for-small-business.md' | Measure-Object -Word).Words

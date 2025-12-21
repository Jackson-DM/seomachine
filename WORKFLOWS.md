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

---

## Workflow #2: SEO Optimization & Content Rewrite

### Goal
Improve an existing blog draft by strengthening SEO performance, clarity, and structure without rewriting from scratch.

---

### Inputs
- Existing blog draft  
  Example:
  - `drafts/ai-consulting-for-small-business.md`
- SEO research file (optional but recommended)  
  Example:
  - `research/ai-consulting-research.md`

---

### Tools Used
- Cursor (AI-assisted rewriting)
- Markdown
- PowerShell (word count validation)

---

### Step-by-Step Process

#### 1. Draft Review
- Review the existing blog draft
- Identify:
  - Redundant sections
  - Weak SEO headings
  - Areas needing clearer explanations

---

#### 2. AI-Assisted Rewrite
- Use the existing draft and research as context
- Rewrite content to:
  - Improve keyword placement
  - Tighten language
  - Enhance H2/H3 structure
  - Maintain original intent

📄 Output:
- `rewrites/ai-consulting-for-small-business.md`

---

#### 3. Quality Control
- Verify clarity and SEO structure
- Check word count if needed using PowerShell:
```powershell
(Get-Content 'rewrites/ai-consulting-for-small-business.md' | Measure-Object -Word).Words

---

## Workflow #3: Content Repurposing & Scale

### Goal
Maximize the value of a single blog post by repurposing it into multiple SEO and marketing assets using AI-assisted transformation.

---

### Inputs
- Final blog draft (original or rewritten)  
  Example:
  - `rewrites/ai-consulting-for-small-business.md`

---

### Tools Used
- Cursor (AI-assisted content transformation)
- Markdown

---

### Step-by-Step Process

#### 1. Source Content Selection
- Choose a finalized blog post
- Confirm content is:
  - Accurate
  - Clear
  - Aligned with business goals

---

#### 2. AI-Assisted Repurposing
Use the blog as context to generate derivative assets such as:
- FAQ section for SEO
- Short-form social media posts
- Email newsletter summary
- Landing page copy
- Sales or service page snippets

Each output focuses on a **specific channel or intent**, not generic reuse.

---

#### 3. Asset Organization
- Save repurposed outputs into appropriate folders, such as:
  - `output/`
  - `published/`
- Clearly label files based on usage and channel

---

### Final Outputs
- Multiple content assets derived from one blog
- Consistent messaging across platforms
- Increased content ROI with minimal extra effort

---

### Why This Workflow Matters
- Scales content production efficiently
- Reduces redundant writing
- Aligns marketing and SEO efforts
- Demonstrates clear AI leverage for clients

---

### Status
⬜ Not yet implemented  
🔜 Ready for execution using existing blog content
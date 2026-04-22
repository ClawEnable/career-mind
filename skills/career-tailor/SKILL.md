---
name: career-tailor
description: Improve or generate resume content. Combines existing resume with review feedback and material library. Every output bullet traces to a verified source — no fabrication.
---

# Career Tailor

## Context Loading

1. Read `~/.career/context.md` for state.
2. If context.md missing → tell user to run `/career:career-init` first. Stop.
3. If `last_review` is set → read the review report file from `~/.career/reviews/`.
4. Determine mode:

| Available Inputs | Mode |
|-----------------|------|
| Resume + Review report + Materials | Full improvement (best quality) |
| Resume + Review report | Review-driven improvement |
| Resume + Materials | Material-enhanced improvement |
| Resume only | Generic quality improvement |
| Materials + Profile only (no resume) | Resume generation from scratch |

Load available inputs. At minimum: resume file OR materials directory must exist.

## Hard Constraints

- **Source tracing:** Every output bullet MUST begin with `[based on: <source>]`. Valid sources:
  - `materials-{id}` — from a confirmed material entry in ~/.career/materials/
  - `resume-rephrase` — rephrased from original resume text
  - `user-verbatim` — from user's direct words in conversation
- **No fabrication:** Do not add facts, metrics, technologies, or achievements not present in source material
- **No inflation:** "familiar with X" cannot become "expert in X". "participated in" cannot become "led"
- **Self-check:** After generating output, verify every bullet has a source tag. Remove any without one

## Workflow

### Step 1: Assess Inputs

List what's available and confirm with user: "I have {resume/review/materials}. I'll improve your resume based on these. Sound good?"

### Step 2: Determine Strategy

- Has review report → prioritize [fixable] issues from report
- No review report → apply generic quality improvement (restructure, replace weak verbs, optimize information density)
- Has materials → check for richer entries to replace/supplement resume content
- **No existing resume (generation mode) → see Step 2a below**

Generic quality improvement boundaries: **only rephrase and restructure existing content**. Cannot add new facts or data. Quantification improvement only when original text has semantic basis (e.g., "significantly improved" stays as-is, cannot become "improved 50%").

### Step 2a: Generation from Scratch (only when no resume exists)

When generating a resume from materials + profile only:

1. Read all confirmed material entries from `~/.career/materials/` (including any `## Re-extraction` sections — merge all extraction rounds for the richest content)
2. Read `~/.career/profile.md` for name, contact, education
3. Build resume structure:
   - Header: name, contact info (from profile)
   - Skills section: aggregate technologies from materials
   - Experience section: one subsection per company, select 2-4 strongest bullets per project from materials highlights
   - Education: from profile
4. Selection rules:
   - Prefer entries with quantifiable metrics
   - If target_direction is set, prioritize matching skills/achievements
   - Maximum 2 pages worth of content — trim weakest entries
5. Every bullet still requires `[based on: materials-{id}]` source tag

### Step 3: Section-by-Section Improvement

For each experience section:

1. Check materials for richer alternatives
2. Apply writing principles from `references/writing-quality.md`
3. Optimize: specificity, active voice, result-first ordering, structural variety
4. Every modification gets a source tag

### Step 4: Self-Check (Gate)

Review all output bullets:
- Every bullet has `[based on: ...]` prefix? If not → remove or mark `[unverified]`
- Any fabricated metrics? → remove
- Any inflated skills/roles? → revert to source wording
- Any new technologies not in source? → remove

### Step 5: Output

Write to `~/.career/resumes/draft_$(date +%Y%m%d).md`:

```markdown
# {name} — Resume v[date]

{full resume content with [based on: ...] source tags}

---

## Modification Summary

| Section | Change | Source | Reason |
|---------|--------|--------|--------|
| {section} | {what changed} | {source} | {why} |
```

Update `~/.career/context.md`: set `last_resume` to the new file. Add action to Recent Actions.

## Output

- Improved resume at `~/.career/resumes/draft_[date].md`
- Modification summary table
- Updated `~/.career/context.md`

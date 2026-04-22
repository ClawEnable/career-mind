---
name: career-review
description: Review resume quality from multiple perspectives. Scores readability, content specificity, quantification, agency, and narrative coherence. Identifies fixable issues vs. gaps needing more material.
---

# Career Review

## Context Loading

1. Read `~/.career/context.md` for target direction and career stage.
2. If context.md missing → tell user to run `/career:career-init` first. Stop.
3. Accept resume input:
   - If `context.md` has `last_resume` → read that file
   - Otherwise → ask user to provide file path or paste resume content
4. Optionally read `~/.career/materials/` to compare resume against available materials.

## Hard Constraints

- Always produce the full report structure defined below
- Always classify issues as [fixable] or [needs-extract]
- Never suggest specific new content that isn't grounded in the existing resume or materials

## Perspectives

### Core (always applied)

1. **Readability:** 3-second scan test. Format clarity, visual hierarchy, information density, ATS heading compatibility.
2. **Content Specificity:** Does each entry express specific value? Actions + results vs. just responsibilities.
3. **Narrative Coherence:** Timeline continuity, role-level match, overall career direction consistency.

### Enhanced (applied when context triggers)

- `target_direction` is set → add **Target Alignment** perspective
- `career_stage` = "graduate" → add **Academic/Internship Depth** perspective
- `career_stage` = "career-change" → add **Transferable Skills** perspective
- Resume has employment gaps → add **Gap Handling** perspective

Auto-detect from context.md. Do NOT ask user which perspectives to apply.

## Workflow

### Step 1: Parse Resume

Extract all sections, entries, and bullet points from the resume.

### Step 2: Score Each Dimension

Use the rubric in `references/review-rubric.md`. Score each of the 5 dimensions as Weak / Adequate / Strong.

### Step 3: Analyze Per Perspective

For each applicable perspective, identify specific issues with line references.

### Step 4: Classify Issues

For each issue found, classify:
- **[fixable]** — wording, format, structure, weak verb replacement
- **[needs-extract]** — vague content, missing quantification, insufficient depth. Specify which company/project section needs extraction.

### Step 5: Generate Report

Write report to `~/.career/reviews/$(date +%Y%m%d).md`:

```markdown
# Resume Review — YYYY-MM-DD

## Scores
| Dimension | Score |
|-----------|-------|
| Readability | {Weak/Adequate/Strong} |
| Content Specificity | {Weak/Adequate/Strong} |
| Quantification | {Weak/Adequate/Strong} |
| Agency | {Weak/Adequate/Strong} |
| Narrative Coherence | {Weak/Adequate/Strong} |

## Detailed Findings
{per-perspective analysis with specific examples from resume}

## Issues
### [fixable]
- {issue with location reference}

### [needs-extract]
- {issue with specific company/project to extract}

## Summary
- Total fixable issues: {N}
- Total gaps requiring extraction: {N}
- Recommendation: {next step}
```

### Step 6: Update Context

Edit `~/.career/context.md`: set `last_review` to the report filename. Add action to Recent Actions.

## Output

- Review report at `~/.career/reviews/[date].md`
- Updated `~/.career/context.md`
- Recommendation: if [needs-extract] items exist → suggest `/career:career-extract`. Otherwise → suggest `/career:career-tailor`

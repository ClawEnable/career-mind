---
name: career-status
description: Check current career preparation status and recommend next steps. Use when user types /career:career-status or is unsure where to start.
---

# Career Status Check

## Context Loading

1. Read `~/.career/context.md`. Format defined in `skills/career-init/references/state-schema.md` (use absolute path from project root).
2. If file does not exist → user has not run init. Say: "You haven't set up yet. Run `/career:career-init` to get started." Stop here.
3. If file exists → read state fields and Recent Actions.
4. If `last_review` is set → read the review report file from `~/.career/reviews/`. Scan for `[needs-extract` to determine if there are gaps needing extraction.

## Status Assessment

Based on context.md state, assess and report:

```
## Current Status
- Profile: {complete/partial/missing}
- Career Stage: {value from context}
- Target Direction: {value or "not set"}
- Extracted Projects: {count, or "none"}
- Reviews Completed: {count based on last_review, or "none"}
- Resumes Saved: {count based on last_resume, or "none"}
```

## Recommendation Logic

| Condition | Recommendation |
|-----------|---------------|
| Profile missing or partial | "Complete your profile first: `/career:career-init`" |
| No extracted projects, no resume | "Start by exploring your experiences: `/career:career-extract`" |
| Has extracted projects, no resume | "Generate a resume from your materials: `/career:career-tailor`" |
| Has resume, no review | "Let's review your resume: `/career:career-review`" |
| Has review with [needs-extract] items | "Review found gaps. Fill them: `/career:career-extract`, then `/career:career-review` again" |
| Has review (all fixable), no draft resume | "Improve your resume based on review: `/career:career-tailor`" |
| Has tailored resume (draft_), no interview prep | "Prepare for interviews: `/career:career-interview`" |
| All steps done | "You're ready! Review your materials or run any step again to iterate" |

Note: distinguish resume versions by filename — `original_` = user-provided, `draft_` = tailor-generated.

## Output

- Status summary (as shown above)
- One clear recommendation with the slash command to run next
- No file writes — this skill is read-only

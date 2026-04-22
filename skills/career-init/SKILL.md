---
name: career-init
description: First-time setup for Career Plugin. Creates ~/.career/ directory, collects profile info, detects existing materials, recommends next step.
---

# Career Init

## Context Loading

1. Check whether `~/.career/` directory exists.
2. If exists: read `~/.career/context.md`. This is a re-initialization — fill gaps only, never overwrite.
3. If not exists: proceed with fresh setup.

## Hard Constraints

- NEVER overwrite existing profile fields — only fill missing ones
- NEVER delete existing files in ~/.career/
- Ask ONE question at a time
- All file writes create new files or edit existing files — never overwrite entire files when appending

## Workflow

### Step 1: Create Directory Structure

```bash
mkdir -p ~/.career/{materials,reviews,resumes}
```

Create `~/.career/.gitignore` containing:
```
*
!.gitignore
```

### Step 2: Collect Profile

Ask one question at a time. After each answer, accumulate for batch write.

1. "What's your name?"
2. "Contact info (phone/email)?"
3. "What city are you in?"
4. "Education background?"

Write to `~/.career/profile.md` using template at `references/profile-template.md`.

### Step 3: Check Existing Resume

"Do you already have a resume?"
- Yes → ask for file path or paste. Copy to `~/.career/resumes/original_$(date +%Y%m%d).md`
- No → skip

### Step 4: Career Stage

"What stage are you at right now?"
- a) Employed, preparing for future opportunities → `preparing`
- b) Actively job searching → `active-seeking`
- c) Recent or upcoming graduate → `graduate`
- d) Career change / transition → `career-change`
- e) Other → `other`

### Step 5: Target Direction (optional)

"Do you have a clear target direction? For example, role type, industry, level?"
- Has target → record for context.md `target_direction` field (written in Step 6)
- No → skip, mark as "TBD"

### Step 6: Initialize Context

Create `~/.career/context.md` following schema at `references/state-schema.md`.

Fill in: profile status (complete/partial), career_stage, target_direction, last_review=none, last_resume=none or original filename.

### Step 7: Recommend Next Step

| Condition | Recommendation |
|-----------|---------------|
| Has resume | "Review your resume: `/career:career-review`" |
| No resume | "Explore your experiences: `/career:career-extract`" |
| Stage = graduate or career-change | "Start with experience extraction: `/career:career-extract`" |

## Output

- `~/.career/` directory with subdirectories
- `~/.career/.gitignore`
- `~/.career/profile.md`
- `~/.career/context.md`
- Optional: `~/.career/resumes/original_[date].md`
- Next step recommendation

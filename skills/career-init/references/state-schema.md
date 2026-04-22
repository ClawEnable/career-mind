# Context State Schema

`~/.career/context.md` is the cross-skill state file. All skills read it on startup. Only the skill that changes state updates it.

## Format

```markdown
---
profile: "<complete | partial | missing>"
career_stage: "<active-seeking | preparing | graduate | career-change | other>"
target_direction: "<description or none>"
last_review: "<filename or none>"
last_resume: "<filename or none>"
---

## Extracted Projects
- <company>_<project> (last extracted: YYYY-MM-DD)

## Recent Actions
- YYYY-MM-DD: <action taken>
```

## Field Rules

| Field | Updated by | When |
|-------|-----------|------|
| profile | init | After profile collection |
| career_stage | init | After stage selection |
| target_direction | init, or any skill | When user provides direction |
| last_review | review | After review report saved |
| last_resume | tailor | After resume saved |
| Extracted Projects | extract | After each project extraction |
| Recent Actions | any skill | After completing a workflow step |

## Read/Write Protocol

- **Read:** Read `~/.career/context.md` at skill startup
- **Write:** Update specific fields in-place. NEVER rewrite the entire file
- **Create:** Only `init` creates this file. Other skills assume it exists
- **Append to Recent Actions:** Add new lines at the end of the Recent Actions section

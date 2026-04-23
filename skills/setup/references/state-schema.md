# Context State Schema

`.career/context.md` is the cross-skill state file. All skills read it on startup.

## Format

```markdown
---
profile: "<complete | partial | missing>"
career_stage: "<active-seeking | preparing | graduate | career-change | performance | development | other>"
target_direction: "<description or none>"
last_assessment: "<filename or none>"
---

## Entries
- <type>_<name>_<NN> (captured: YYYY-MM-DD)

## Recent Actions
- YYYY-MM-DD: <action taken>
```

## Field Rules

| Field | Updated by | When |
|-------|-----------|------|
| profile | setup | After profile collection |
| career_stage | setup | After stage selection |
| target_direction | setup, or any skill | When user provides direction |
| last_assessment | assess | After assessment report saved |
| Entries section | capture | After each entry confirmed and saved |
| Recent Actions | any skill | After completing a workflow step |

## Read/Write Protocol

- **Read:** Read `.career/context.md` at skill startup
- **Write:** Update specific fields in-place. NEVER rewrite the entire file
- **Create:** Only `setup` creates this file. Other skills assume it exists
- **Append to Entries:** Add new lines at the end of the Entries section
- **Append to Recent Actions:** Add new lines at the end of the Recent Actions section

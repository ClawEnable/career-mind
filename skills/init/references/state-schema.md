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
- <type>_<name>_<NN> (imported: YYYY-MM-DD)
- <type>_<name>_<NN> (captured: YYYY-MM-DD)

## Recent Actions
- YYYY-MM-DD: <action keyword> — <brief description>
```

## Field Rules

| Field | Updated by | When |
|-------|-----------|------|
| profile | init | After profile collection |
| career_stage | init | After stage selection |
| target_direction | init, or any skill | When user provides direction |
| last_assessment | assess | After assessment report saved |
| Entries section | init, capture | After entries imported or confirmed and saved |
| Recent Actions | any skill | After completing a workflow step |

## Entries Annotations

| Annotation | Meaning | Written by |
|------------|---------|------------|
| `(imported: YYYY-MM-DD)` | Entry parsed from an existing document during init | init |
| `(captured: YYYY-MM-DD)` | Entry created through conversation in capture | capture |

## Recent Actions Vocabulary

Recent Actions lines MUST use these standardized keywords:

| Keyword | Written by | Meaning |
|---------|-----------|---------|
| `init` | init | Directory created, profile collected |
| `import` | init | Documents found and parsed into entries |
| `capture` | capture | Entry created or supplemented through capture |
| `capture-postimport` | capture | Post-import analysis completed |
| `assess` | assess | Assessment report generated |
| `craft` | craft | Artifact generated |
| `interview` | interview | Interview prep completed or mock interview conducted |

## Read/Write Protocol

- **Read:** Read `.career/context.md` at skill startup
- **Write:** Update specific fields in-place. NEVER rewrite the entire file
- **Create:** Only `init` creates this file. Other skills assume it exists
- **Append to Entries:** Add new lines at the end of the Entries section
- **Append to Recent Actions:** Add new lines at the end of the Recent Actions section. MUST use standardized keywords from the vocabulary table in this file

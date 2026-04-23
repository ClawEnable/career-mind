# Context State Schema

`.career/context.md` is the cross-skill state file. All skills read it on startup.

## Format

```markdown
---
profile: "<complete | partial | missing>"
career_stage: "<active-seeking | preparing | graduate | career-change | performance | development | other>"
target_direction: "<description or none>"
last_assessment: "<filename or none>"
interaction_hints: "<free-text notes or none>"
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
| profile | cm-init | After profile collection |
| career_stage | cm-init | After stage selection |
| target_direction | cm-init, or any skill | When user provides direction |
| last_assessment | cm-assess | After assessment report saved |
| interaction_hints | any skill | When user expresses a clear, repeatable preference (e.g. "keep it brief", "I prefer options not open questions"). Only persist preferences expressed consistently across 2+ interactions — do not record one-off feedback. |
| Entries section | cm-init, cm-capture | After entries imported or confirmed and saved |
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
| `init` | cm-init | Directory created, profile collected |
| `import` | cm-init | Documents found and parsed into entries |
| `capture` | cm-capture | Entry created or supplemented through capture |
| `capture-postimport` | cm-capture | Post-import analysis completed |
| `assess` | cm-assess | Assessment report generated |
| `craft` | cm-craft | Artifact generated |
| `interview` | cm-interview | Interview prep completed or mock interview conducted |

## Read/Write Protocol

- **Read:** Read `.career/context.md` at skill startup
- **Write:** Update specific fields in-place. NEVER rewrite the entire file
- **Create:** Only `init` creates this file. Other skills assume it exists
- **Append to Entries:** Add new lines at the end of the Entries section
- **Append to Recent Actions:** Add new lines at the end of the Recent Actions section. MUST use standardized keywords from the vocabulary table in this file

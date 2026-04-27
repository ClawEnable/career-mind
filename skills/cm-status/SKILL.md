---
name: cm-status
description: Check current career preparation status and recommend next steps. Use when user says 'career status', 'where am I', 'what next', 'what should I do', 'help', 'progress', 'check status', or is unsure where to start.
compatibility: "Claude Code, Codex, Cursor, OpenCode, OpenClaw, and any Agent Skills compatible platform"
allowed-tools: "Read Glob Grep"
---

# Career Status Check

## Context Loading

1. Read `.career/context.md` (YAML frontmatter with fields: profile, career_stage, target_direction, last_assessment; plus Entries and Recent Actions sections).
2. If file does not exist → user has not initialized. Say: "You haven't initialized yet. Run `/career-mind:cm-init` to get started." Stop here.
3. If file exists → read state fields and Recent Actions.
4. Scan `.career/entries/` for entry count and types.
5. Scan `.career/outputs/` for generated artifacts.
6. If `last_assessment` is set → read the assessment report. Scan for `[needs-capture]` and `[needs-supplement]` to determine if there are gaps.

## Hard Constraints

- **Execution self-check:** Before giving the recommendation, verify all conditions in the Recommendation Logic table have been checked.

## Status Assessment

Based on context.md state and file scan, assess and report:

```
## Current Status
- Profile: {complete/partial/missing}
- Career Stage: {value from context}
- Target Direction: {value or "not set"}
- Entries: {count} ({project} projects, {signal} signals, {achievement} achievements)
- Last Assessment: {date or "none"}
- Generated Artifacts: {list types or "none"}
```

## Recommendation Logic

Check conditions in this order (first match wins):

| Condition | Recommendation |
|-----------|---------------|
| Profile missing or partial | "Complete your profile first: `/career-mind:cm-init`" |
| No entries | "Start by capturing your experiences: `/career-mind:cm-capture`" |
| Has entries from import, no capture session yet (Recent Actions has `import` but no `capture` or `capture-postimport`) | "Deepen your imported entries: `/career-mind:cm-capture`" |
| Has entries, no assessment | "Let's assess your materials: `/career-mind:cm-assess`" |
| Has assessment with [needs-capture] or [needs-supplement] items | "Assessment found gaps. Fill them: `/career-mind:cm-capture`, then `/career-mind:cm-assess` again" |
| Has assessment (no gaps), no generated artifacts | "Generate what you need: `/career-mind:cm-craft`" |
| Has generated artifacts | "You're on track! Iterate on any step or prepare for interviews: `/career-mind:cm-interview`" |

## Next Step

Based on the top recommendation, ask: "Shall I proceed with {recommended skill}?" If user confirms, invoke the recommended skill immediately.

## Output

- Status summary (as shown above)
- One clear recommendation with auto-proceed prompt
- No file writes — this skill is read-only

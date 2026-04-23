# Writing Quality Principles

These principles guide artifact content generation. They apply to all scenario types.

## Core Principles

| Principle | Do | Don't |
|-----------|-----|-------|
| **Specific** | "from 5min to 30sec" | "improved efficiency" |
| **Active** | "Designed and implemented X" | "Was responsible for X" |
| **Result-first** | "Reduced crash rate by 40% via Y" | "Implemented Y, which reduced crashes" |
| **Varied structure** | Mix sentence patterns across entries | "Achieved X by doing Y" for every bullet |
| **User's voice** | Preserve user's natural expressions | Over-polish everything into corporate-speak |

## Anti-Fabrication Rules

These are hard constraints. Violating any one is a critical failure.

1. **Source traceability:** Every output bullet must map to a source, recorded in the .meta.md sidecar file. Valid sources:
   - `entry-{id}` — from a confirmed entry
   - `profile` — from profile.md
   - `user-verbatim` — from user's direct words in conversation

2. **No invented facts:** Do not add technologies, skills, metrics, or achievements not present in the source material

3. **No inflated numbers:** "significantly improved" in source cannot become "improved 50%" in output

4. **No skill inflation:** "familiar with React" cannot become "expert in React"

## Rephrasing Boundaries

Allowed:
- Replace weak verbs with stronger ones (if the action is factually accurate)
- Rearrange sentence order for impact
- Restructure sections for clarity
- Merge or split bullet points

Not allowed:
- Add metrics not in the original entry
- Add technologies or tools not mentioned
- Change the scope of contribution ("participated in" → "led" is fabrication)
- Add entirely new bullet points without source

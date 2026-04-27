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

## AI Fingerprint Avoidance

### Banned Verb Patterns
Avoid these overused AI-generated verbs. Replace with specific, concrete alternatives:
- "spearheaded" → "started", "proposed", "drove"
- "orchestrated" → "coordinated", "organized", "managed"
- "leveraged" → "used", "applied", "built on"
- "utilized" → "used", "ran", "configured"
- "facilitated" → "enabled", "set up", "ran"
- "pioneered" → "introduced", "built first", "created"
- "revolutionized" → "changed", "improved", "rebuilt"
- "streamlined" → "simplified", "reduced", "consolidated"

### Structural Pattern Avoidance
- Do not make every bullet follow "Strong verb + metric + context" pattern
- Vary sentence length — some bullets can be short and direct
- Mix narrative styles: some bullets lead with result, some with action, some with context
- Avoid uniform "X by Y" construction across all entries

### AI Fingerprint Self-Check
Before finalizing any artifact, scan for:
1. Three or more consecutive bullets with identical grammatical structure
2. Every bullet starting with a past-tense action verb
3. Every bullet containing a quantified metric
4. Absence of any first-person or conversational language from the user's original words
5. Overly uniform bullet length (all within 10% of each other)
6. Excessive use of compound sentences (two clauses joined by "and" or "while")
7. No short, punchy bullets among longer detailed ones
8. Generic adjectives without specifics ("significant", "substantial", "considerable")
9. Every achievement framed as an isolated success without mentioning challenges
10. Perfect parallel structure across all role sections

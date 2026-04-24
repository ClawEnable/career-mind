---
name: cm-craft
description: Generate career artifacts for any scenario. Combines entry library with assessment feedback to produce resumes, performance reviews, promotion cases, skill maps, and more. Every output traces to verified sources. Use when user says 'generate resume', 'write performance review', 'create promotion case', 'build skill map', or has completed assess and wants to produce an artifact.
---

# Career Craft

## Context Loading

1. Read `.career/context.md` for state.
2. If context.md missing → tell user to run `/career-mind:cm-init` first. Stop.
3. If `last_assessment` is set → read the assessment report from `.career/outputs/`.
4. Read all entries in `.career/entries/`.
5. Read `.career/profile.md`.
6. If no entries found → tell user: "No information available. Run `/career-mind:cm-capture` first to capture your experiences." Stop.
7. Determine target scenario:

| Trigger | Scenario |
|---------|----------|
| User says "resume", "CV" | resume |
| User says "performance review", "self-evaluation" | performance |
| User says "promotion", "promotion case" | promotion |
| User says "skill map", "skill gap" | skillmap |
| User says "interview prep" | → redirect to `/career-mind:cm-interview` |
| No specific scenario | Present as a structured single-select: resume / performance / promotion / skillmap / other |

## Hard Constraints

- **Career-stage adaptation:** Read `career_stage` from context.md and adjust output strategy: graduate→emphasize potential and learning; mid-career→balance technical depth with business impact; senior/lead→lead with strategic influence, scope-of-impact narrative; career-change→emphasize transferable skills and unique perspective.
- **Source tracing:** Every output bullet must be traceable to a source. Valid sources:
  - `entry-{id}` — from a confirmed entry in .career/entries/
  - `profile` — from profile.md
  - `user-verbatim` — from user's direct words in conversation
  Source tracking goes in the .meta.md file, not in the artifact itself.
- **No fabrication:** Do not add facts, metrics, technologies, or achievements not present in source material
- **No inflation:** "familiar with X" cannot become "expert in X". "participated in" cannot become "led"
- **Advisory recommendation:** When presenting scenario choices, entry selections, or content options, always include a recommended default with reasoning. "Based on your entries, I'd suggest X because Y" — not "Which do you prefer?"
- **Audience calibration:** Before generating output, consider the primary audience: ATS systems need standard section names and exact keyword matches; HR screeners need clear role progression and qualifications; hiring managers need scale signals and impact evidence. Resume bullets should work on both levels — machine-scannable and human-compelling. Skills section should use industry-standard terms (e.g., both "Kubernetes" and "K8s" if the user uses either).
- **Self-check:** After generating output, verify every bullet has a source tag. Remove fabricated or clearly incorrect content; mark plausible but unsourceable claims as `[unverified]` for user review
- **Collection processing:** When a step requires processing multiple items (entries, bullets, sections), follow the closed loop: (1) declare the full set — "Need to process {N} items: {list}", (2) process each item with progress marking, (3) confirm completion — "All {N} items processed."
- **Execution self-check:** Before advancing to the next step, verify: (a) collection operations (each/all/per) — all items processed? (b) compound actions (A and B) — all sub-actions executed? (c) qualitative actions (analyze/explain/suggest) — output has substantive content, not just framework-level mention?

## Workflow

### Step 1: Confirm Scenario

Present a structured confirmation interaction with:
"I have {N} entries and your profile. Here's what I'll use:
- Relevant entries: {list entry names with brief note on strength}
- Profile: {name, key info}
- {If assessment exists: Assessment highlights: {key findings}}
- Target scenario: {scenario}

Confirm / Adjust scope / Exclude specific entries."

### Step 2: Strategy by Scenario

Each scenario has different selection and organization rules. See `references/scenario-templates.md` for detailed templates.

**Resume:** Select strongest project entries with quantified results. Organize by reverse chronological order. Include skills aggregation from entry tags. Maximum 2 pages.

**Performance Review:** Organize by impact areas or objectives. Emphasize outcomes and growth. Include both technical and soft-skill evidence. Professional self-assessment tone.

**Promotion Case:** Lead with impact narrative. Demonstrate level-above behaviors. Include scope and influence metrics. Address promotion criteria explicitly.

**Skill Map:** Aggregate all tags across entries. Categorize by domain. Rate depth based on evidence quantity and quality. Identify gaps between current skills and target direction.

### Step 3: Select and Organize Entries

Based on the scenario strategy:
1. Filter relevant entries
2. If target_direction is set, prioritize matching entries
3. Select strongest evidence for each section
4. Every selected piece gets a source tag

### Step 4: Generate Content

Apply writing principles from `references/writing-quality.md`:
- Specific over vague
- Active voice
- Result-first ordering
- Structural variety
- Preserve user's natural expressions

### Step 5: Self-Check (Gate)

Declare total bullet count: "Reviewing all {N} output bullets for source traceability."

Review all output bullets:
- Every bullet traceable to a source? If fabricated or clearly incorrect → remove. If plausible but unsourceable → mark `[unverified]`
- Any fabricated metrics? → remove
- Any inflated skills/roles? → revert to source wording
- Any new technologies not in source? → remove
- **Cherry-picking check:** Does the output present evidence without qualifying context? If "led migration of 50 services" appears, verify whether the source also mentions team size, shared ownership, or collaborative context. Include qualifying context when it exists — omitting it inflates perceived scope and violates anti-fabrication principles.

### Step 6: Output

Write two files:

1. **`.career/outputs/{scenario}_YYYYMMDD.md`** — clean artifact, ready to use directly. No source tags, no metadata.
2. **`.career/outputs/{scenario}_YYYYMMDD.meta.md`** — source tracking:
   - Source mapping table (artifact bullet → source)
   - Change summary table
   - Self-check verification results

Present the clean artifact to user in conversation. Mention the meta file is available for reviewing sourcing.

Update `.career/context.md`: add action to Recent Actions using the `craft` keyword.

## Next Step

After output is saved:

| Condition | Next Step |
|-----------|-----------|
| Generated a resume | Ask: "Shall I prepare for interviews with this resume?" → `/career-mind:cm-interview` |
| Generated other artifact | Ask: "Want to assess your overall career readiness?" → `/career-mind:cm-status` |
| User wants to iterate | Ask: "Shall I assess the output quality?" → `/career-mind:cm-assess` |

If user confirms, invoke the next skill immediately.

## Output

- Clean artifact at `.career/outputs/{scenario}_YYYYMMDD.md`
- Source tracking at `.career/outputs/{scenario}_YYYYMMDD.meta.md`
- Updated `.career/context.md`
- Auto-proceed to next recommended skill (if user confirms)

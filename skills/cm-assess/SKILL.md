---
name: cm-assess
description: Assess career information quality and completeness. Evaluates capability coverage across multiple dimensions. Use when user says 'assess my materials', 'review what I have', 'how complete is my profile', 'am I ready', or has completed capture and wants feedback. Can target specific output scenarios.
compatibility: "Claude Code, Codex, Cursor, OpenCode, OpenClaw, and any Agent Skills compatible platform"
allowed-tools: "Read Write Glob Grep"
---

# Career Assess

## Context Loading

1. Read `.career/context.md` for career stage and target direction.
2. If context.md missing → tell user to run `/career-mind:cm-init` first. Stop.
3. Load all available information:
   - Read `.career/profile.md` if exists
   - Read all files in `.career/entries/`
   - Read any existing outputs in `.career/outputs/` for context
4. If no entries found → tell user: "No entries to assess. Run `/career-mind:cm-capture` first to capture your experiences." Stop.
5. Determine assessment target:
   - If user specifies a scenario (resume, promotion, performance review, etc.) → target that scenario
   - If no scenario specified → general quality assessment

## Hard Constraints

- Always produce the full report structure defined below
- Always classify gaps as [needs-capture] or [needs-supplement] with specific guidance
- Never suggest specific new content that isn't grounded in existing entries
- **Career-stage adaptation:** Read `career_stage` from context.md and apply weighting from `career-stage-signals.md` Output Weighting column. Assessment emphasis should differ for graduate (growth potential) vs senior (scope of influence) vs career-change (adaptability).
- Assessment adapts to available information — never penalize for missing a specific entry type
- **Collection processing:** When a step requires processing multiple items (dimensions, entries, gaps), follow the closed loop: (1) declare the full set — "Need to process {N} items: {list}", (2) process each item with progress marking, (3) confirm completion — "All {N} items processed."
- **Execution self-check:** Before advancing to the next step, verify: (a) collection operations (each/all/per) — all items processed? (b) compound actions (A and B) — all sub-actions executed? (c) qualitative actions (analyze/explain/suggest) — output has substantive content, not just framework-level mention?
- **Insight over score:** Each dimension analysis must answer three questions: (1) What specific entries demonstrate this score and what exactly makes them strong or weak? (2) What is the consequence of this score for the user's target goal? (3) What single action would most improve this dimension? Never produce a dimension analysis that only restates the rubric criteria.

## Assessment Dimensions

### Core (always assessed)

1. **Content Specificity:** Does each entry express specific value? Actions + results vs. just responsibilities.
2. **Quantification:** Are achievements measurable? Are metrics present and meaningful?
3. **Agency:** Is the user's personal contribution clear vs. team-level claims?
4. **Narrative Coherence:** Timeline continuity, role-level match, career direction consistency.

### Scenario-specific (applied when target scenario is set)

- Target = resume → add **Readability** dimension
- Target = promotion → add **Impact Breadth** dimension
- Target = performance review → add **Goal Alignment** dimension

### Enhanced (applied when context triggers)

- `target_direction` is set → add **Target Alignment** assessment
- `career_stage` = "graduate" → add **Academic/Internship Depth** assessment
- `career_stage` = "career-change" → add **Transferable Skills** assessment
- 3+ entries exist → add **Narrative Arc** assessment
- `target_direction` is set → add **Differentiation** assessment
- Always → add **Evidence Density** assessment

Auto-detect from context.md. Do NOT ask user which dimensions to apply.

## Workflow

### Step 1: Parse Entries

Aggregate all entries by type (project, signal, achievement). Note completeness per entry (each should cover what, how, result). Identify tag coverage across entries.

### Step 2: Score Each Dimension

Declare the full set of applicable dimensions (Core + Scenario-specific + Enhanced as auto-detected). Score each one using the rubric in `references/assess-rubric.md`. Mark progress: "Scoring dimension {n}/{total}: {dimension name}". Confirm all dimensions scored before advancing.

### Step 2.5: Preliminary Scores

Display the score table to user with a brief explanation of each dimension. Ask: "Any scores surprise you? Should I focus on specific areas?"

WAIT for user response before proceeding to Step 3. If user flags a concern about a score, adjust the analysis emphasis accordingly.

### Step 3: Analyze Per Dimension

For each applicable dimension, produce a diagnostic insight following the Insight over score constraint — reference specific entries, explain consequences for the target goal, and recommend the highest-impact improvement action. Each dimension analysis must include:
- At least 1 specific entry reference (which entry exhibits or lacks this quality)
- What specifically is present or missing (not just "adequate" — what makes it adequate)
- Concrete example from the entry content

Declare all applicable dimensions upfront. Process each one. Confirm all completed before advancing.

### Step 4: Classify Gaps

For each gap found, classify:
- **[needs-capture]** — missing information requiring new entries. Specify what type and area.
- **[needs-supplement]** — existing entry lacks depth in a dimension. Specify which entry and what detail is missing.

### Step 4.5: Preview Gaps

Present classified gaps to user before writing the full report. For each [needs-capture] or [needs-supplement] item, explain what information is missing and suggest how to address it. Format as a structured table:

| Priority | Gap Type | Entry | What's Missing | Suggested Action |

### Step 5: Generate Report

Write report to `.career/outputs/assessment_YYYYMMDD.md` (using current date):

```markdown
# Assessment — YYYY-MM-DD

## Information Available
- Profile: {complete/partial/missing}
- Entries: {count} ({project count} projects, {signal count} signals, {achievement count} achievements)
- Target Scenario: {scenario or "general"}

## Scores
| Dimension | Score |
|-----------|-------|
| Content Specificity | {Weak/Adequate/Strong} |
| Quantification | {Weak/Adequate/Strong} |
| Agency | {Weak/Adequate/Strong} |
| Narrative Coherence | {Weak/Adequate/Strong} |
| {Scenario-specific} | {Weak/Adequate/Strong or N/A} |

## Detailed Findings
{per-dimension analysis with specific examples from entries}

## Gaps
### [needs-capture]
- {gap with specific guidance on what to capture}

### [needs-supplement]
- {gap with specific guidance on which entry to re-extract and what detail is missing}

## Summary
- Total gaps: {N} ({capture} needs-capture, {supplement} needs-supplement)
- Strongest areas: {list}
- Weakest areas: {list}
- Recommendation: {next step}
```

### Step 5.5: Present Report Summary

After writing the report, present key findings in conversation before proceeding:
1. Score overview table (all dimensions with their scores)
2. One-sentence summary per dimension finding
3. Total gap count with top-priority gaps listed
4. Recommended next step

Wait for user acknowledgment or feedback before advancing to Step 6.

### Step 6: Update Context

Edit `.career/context.md`: set `last_assessment` to the report filename. Add action to Recent Actions using the `assess` keyword.

## Next Step

After report is saved:

| Condition | Next Step |
|-----------|-----------|
| Has [needs-capture] or [needs-supplement] | Ask: "Assessment found {gaps}. Shall I capture more details to fill these gaps?" → `/career-mind:cm-capture` |
| All gaps addressed | Ask: "What would you like to do next? Generate a resume, prepare for interview, or something else?" → user chooses |

If user confirms, invoke the next skill immediately.

## Output

- Assessment report at `.career/outputs/assessment_YYYYMMDD.md`
- Updated `.career/context.md`
- Auto-proceed to next recommended skill (if user confirms)

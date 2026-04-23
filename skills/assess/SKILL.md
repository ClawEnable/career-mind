---
name: assess
description: Assess career information quality and completeness. Evaluates capability coverage across multiple dimensions. Use when user says 'assess my materials', 'review what I have', 'how complete is my profile', 'am I ready', or has completed capture and wants feedback. Can target specific output scenarios.
---

# Career Assess

## Context Loading

1. Read `.career/context.md` for career stage and target direction.
2. If context.md missing → tell user to run `/career-mind:init` first. Stop.
3. Load all available information:
   - Read `.career/profile.md` if exists
   - Read all files in `.career/entries/`
   - Read any existing outputs in `.career/outputs/` for context
4. If no entries found → tell user: "No entries to assess. Run `/career-mind:capture` first to capture your experiences." Stop.
5. Determine assessment target:
   - If user specifies a scenario (resume, promotion, performance review, etc.) → target that scenario
   - If no scenario specified → general quality assessment

## Hard Constraints

- Always produce the full report structure defined below
- Always classify gaps as [needs-capture] or [needs-supplement] with specific guidance
- Never suggest specific new content that isn't grounded in existing entries
- Assessment adapts to available information — never penalize for missing a specific entry type

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

Auto-detect from context.md. Do NOT ask user which dimensions to apply.

## Workflow

### Step 1: Parse Entries

Aggregate all entries by type (project, signal, achievement). Note completeness per entry (each should cover what, how, result). Identify tag coverage across entries.

### Step 2: Score Each Dimension

Use the rubric in `references/assess-rubric.md`. Score applicable dimensions as Weak / Adequate / Strong.

### Step 2.5: Preliminary Scores

Display the score table to user with a brief explanation of each dimension. Ask: "Any scores surprise you? Should I focus on specific areas?"

### Step 3: Analyze Per Dimension

For each applicable dimension, identify specific gaps with entry references.

### Step 4: Classify Gaps

For each gap found, classify:
- **[needs-capture]** — missing information requiring new entries. Specify what type and area.
- **[needs-supplement]** — existing entry lacks depth in a dimension. Specify which entry and what detail is missing.

### Step 4.5: Gap Preview

Present classified gaps to user before writing the full report. If [needs-capture] or [needs-supplement] items exist, explain what information is missing and suggest how to address it.

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

### Step 6: Update Context

Edit `.career/context.md`: set `last_assessment` to the report filename. Add action to Recent Actions using the `assess` keyword.

## Next Step

After report is saved:

| Condition | Next Step |
|-----------|-----------|
| Has [needs-capture] or [needs-supplement] items | Ask: "Assessment found gaps. Shall I capture more details for those areas?" → `/career-mind:capture` |
| All gaps addressed | Ask: "What would you like to do next? Generate a resume, prepare for interview, or something else?" → user chooses |

If user confirms, invoke the next skill immediately.

## Output

- Assessment report at `.career/outputs/assessment_YYYYMMDD.md`
- Updated `.career/context.md`
- Auto-proceed to next recommended skill (if user confirms)

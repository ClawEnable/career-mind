---
name: cm-capture
description: Capture career capabilities and experiences through conversation, work review, or document import. Use when user says 'capture', 'record', 'describe my work', 'summarize what we did', 'import resume', or is sent from assess with gaps to fill.
---

# Career Capture

## Context Loading

1. Read `.career/context.md` to check existing entries and avoid re-covering ground.
2. If context.md missing → tell user to run `/career-mind:cm-init` first. Stop.
3. Read existing entries in `.career/entries/` to know what's already captured.
4. Optionally read `.career/profile.md` for user context.

## Hard Constraints

- **Confirmation gate:** Every entry must be confirmed by the user before writing to .career/entries/
- **Three-dimension check:** Each entry must cover: (1) what was done, (2) how it was done, (3) what resulted. Missing any → follow-up before confirming
- **User verbatim:** Always capture and preserve the user's exact words. These are the most valuable output
- **Session review limit:** Extract at most 2 capability highlights per session review. Quality over quantity
- Ask one question at a time for open-ended exploration. When options are known, present as numbered choices
- Never mention SOAR/STAR to the user — these are internal organizing tools only
- **Career-stage adaptation:** Read `career_stage` from context.md and adapt your approach using `references/career-stage-signals.md`. Graduate→help translate academic/internship experience into professional language; career-change→focus on transferable skill mapping; senior/lead→focus on scope-of-influence narrative, not project-level detail.
- **Domain-first inference:** Before asking any question about an entry, use your domain expertise to understand what the content already implies. Only surface gaps that are genuinely non-inferable — business context, specific metrics, personal experiences, operational realities. Never ask a domain expert to explain what standard practice already explains.
- **Infer-then-option interaction:** When existing information provides a basis (imported entries, profile data, conversation history), use domain knowledge to generate polished, complete statement options with specific estimated values. Recommend the option most likely to be accurate with reasoning: "I'd recommend [X] because [reasoning]. Others are also plausible: [Y], [Z]. Which is closest?" Each option should be a ready-to-use draft that the user confirms or corrects — not a topic label requiring further articulation. For uncertain values, provide reasonable estimates with concrete ranges (e.g., "30-50% improvement" not "X% improvement"). Iterate: recommendation → user selection → refined option → confirmation.
- **Collection processing:** When a step requires processing multiple items (entries, dimensions, gaps), follow the closed loop: (1) declare the full set — "Need to process {N} items: {list}", (2) process each item with progress marking, (3) confirm completion — "All {N} items processed."
- **Execution self-check:** Before advancing to the next step, verify: (a) collection operations (each/all/per) — all items processed? (b) compound actions (A and B) — all sub-actions executed? (c) qualitative actions (analyze/explain/suggest) — output has substantive content, not just framework-level mention?

## Mode Detection

Check in this order:

1. **Post-import analysis** (highest priority): Triggered when `context.md` Recent Actions contains a `import` keyword AND no `capture` or `capture-postimport` or `assess` keyword appears after it. This means we just came from Init with imported data.
2. **Targeted dive**: Triggered when Recent Actions contains an `assess` keyword AND the assessment report has `[needs-capture]` or `[needs-supplement]` items.
3. **Session review**: User says "summarize what we did", "review this session".
4. **Document import**: User provides a file path or pasted document.
5. **Active description**: User says "record", "describe", "talk about", or no other mode matches.

| Trigger | Mode | Opening |
|---------|------|---------|
| Entries exist from import, no assess/capture yet | Post-import analysis | See Mode: Post-Import Analysis below |
| Recent Actions mentions assessment with gaps | Targeted dive | "Assessment found we need more detail on {area}. Let's dig in." For [needs-supplement] items, focus on re-extracting missing dimensions. |
| User says "summarize what we did", "review this session" | Session review | "Let me review what we worked on and identify any notable highlights." |
| User provides file path or pasted document | Document import | "I'll parse this document and extract relevant information." |
| User says "record", "describe", "talk about" | Active description | "What experience would you like to start with?" |
| No other mode matches | Active description | "What have you been working on recently?" |

## Workflow

### Mode: Post-Import Analysis

This mode runs when entries were imported during Init but haven't been assessed or deepened yet. Read `references/post-import-analysis.md` for the full workflow (framework alignment, dynamic perspective, domain inference, gap prioritization, polished option generation, iterative refinement, confirm and write).

### Mode: Active Description

#### Phase 1: Open Exploration

Briefly align with the user: "I'll capture your experiences by listening first, then following up on valuable details. Each experience should cover what you did, how you did it, and what resulted. {If target_direction exists: I'll pay extra attention to anything relevant to {target_direction}.} What would you like to start with?"

If existing entries are present: reference them to guide the conversation. Start with the entry that has the most missing dimensions or highest strategic value. "I noticed {entry} mentions {result} but doesn't cover how you got there. Can you walk me through that?"

If user has no starting point: "What have you been working on recently?"

Listen. Capture everything. Do not judge or filter yet.

#### Phase 2: Signal Detection

Watch for valuable signals. When you hear something interesting, follow up naturally:

"Wait, you mentioned switching approaches there — can you say more about that?"

Use the trigger patterns in `references/questioning-triggers.md` to decide when and how to follow up.

#### Phase 3: Dimension Filling

Based on collected content, identify missing dimensions and ask naturally:

- "You mentioned the results were good — do you have specific numbers?"
- "Did you consider other options for that approach?"
- "What was your personal contribution to this project?"

Dimensions emerge from conversation. Do NOT present a checklist to the user.

#### Phase 4: Structuring

Organize scattered information into entries using the entry template in `references/entry-template.md`.

If structuring reveals gaps → go back to Phase 3.

#### Phase 5: Confirm and Write

For each entry:

1. Determine entry type: `project` (has company/project context), `signal` (standalone capability), `achievement` (specific milestone)
2. Check if a similar entry already exists in `.career/entries/`
3. Present the structured entry to the user for confirmation (confirm / correct / reject).
4. If user confirms → set `confirmed: true`
   - **Similar entry exists:** Append under `## Supplement YYYY-MM-DD` heading. Append new highlights and metrics. Do NOT modify YAML frontmatter or delete existing content
   - **No existing entry:** Create file following `references/entry-template.md` format
5. If user corrects → update and re-confirm

### Mode: Session Review

#### Phase 1: Review Context

Review the current work session or conversation context. Identify what the user accomplished, decided, or demonstrated.

#### Phase 2: Extract Highlights

From the session, identify at most **2** high-value capability highlights. A highlight is worth capturing only if:
- It demonstrates a notable capability or skill
- It has a concrete outcome or decision
- It would be relevant in a career context (resume, promotion, etc.)

If nothing meets this threshold → say so honestly: "This session was routine — nothing stands out as a career highlight. That's perfectly fine."

#### Phase 3: Confirm and Write

Present extracted highlights to user. For each:

"What I noticed: {description of capability/outcome}. Worth saving?"

If user confirms → create entry with type `signal` or `achievement` as appropriate, using `references/entry-template.md`.

### Mode: Document Import

#### Phase 1: Parse Document

Read and parse the provided document. Identify structured sections:
- Work experience → potential `project` entries
- Skills sections → tags for entries
- Achievements/awards → potential `achievement` entries
- Education → offer to update profile.md

#### Phase 2: Create Draft Entries

For each identified item, create a draft entry using `references/entry-template.md`. Set `source: imported` and `source_detail` to describe the original document.

#### Phase 3: Confirm and Write

Present each draft entry as a structured confirmation interaction (confirm / correct / skip). Process entries one at a time. WAIT for user response on each entry before proceeding to the next.

If education or contact info is found → offer to update `.career/profile.md` as well.

## Cross-Dimension Information Capture

During any mode of capture, if the user mentions information that belongs to a different dimension:

- Profile-related info (education, contact, certifications) → offer to update `.career/profile.md`
- Career direction or goals → offer to update `target_direction` in `.career/context.md`

Any skill can suggest triggering capture when relevant information surfaces in conversation.

## After Writing

Update `.career/context.md`:
- Add entry to Entries section (use `(captured: YYYY-MM-DD)` annotation)
- Add action to Recent Actions using standardized keywords:
  - Post-import analysis completed → `YYYY-MM-DD: capture-postimport — {summary}`
  - Entry created or supplemented → `YYYY-MM-DD: capture — {entry id}: {brief description}`

After updating context, present a capture summary in conversation:
"Saved {entry name}. Covers {which of what/how/result dimensions are present}. {If any dimension is thin: Note: {dimension} is still thin — can be deepened later.}"

## Freedom Note

Active description mode has HIGH freedom. The phases above are guidelines, not a rigid script. When the user is freely sharing valuable details, let them continue without interruption. Phase transitions are fluid — return to earlier phases as needed.

Session review mode has LOWER freedom — stick to the "at most 2 highlights" constraint. Resist the urge to capture everything.

## Next Step

After capture is complete, ask: "I've captured {N} entries. Shall I assess what we have so far?"

If user confirms, invoke `/career-mind:cm-assess` immediately.

## Output

- Entry files in `.career/entries/`
- Updated `.career/context.md`
- Optionally updated `.career/profile.md`
- Auto-proceed to assess (if user confirms)

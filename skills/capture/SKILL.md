---
name: capture
description: Capture career capabilities and experiences through conversation, work review, or document import. Use when user says 'capture', 'record', 'describe my work', 'summarize what we did', 'import resume', or is sent from assess with gaps to fill.
---

# Career Capture

## Context Loading

1. Read `.career/context.md` to check existing entries and avoid re-covering ground.
2. If context.md missing → tell user to run `/career-mind:setup` first. Stop.
3. Read existing entries in `.career/entries/` to know what's already captured.
4. Optionally read `.career/profile.md` for user context.

## Hard Constraints

- **Confirmation gate:** Every entry must be confirmed by the user before writing to .career/entries/
- **Three-dimension check:** Each entry must cover: (1) what was done, (2) how it was done, (3) what resulted. Missing any → follow-up before confirming
- **User verbatim:** Always capture and preserve the user's exact words. These are the most valuable output
- **Session review limit:** Extract at most 2 capability highlights per session review. Quality over quantity
- Ask one question at a time for open-ended exploration. When options are known, present as numbered choices
- Never mention SOAR/STAR to the user — these are internal organizing tools only

## Mode Detection

| Trigger | Mode | Opening |
|---------|------|---------|
| User says "record", "describe", "talk about" | Active description | "What experience would you like to start with?" |
| User says "summarize what we did", "review this session" | Session review | "Let me review what we worked on and identify any notable highlights." |
| User provides file path or pasted document | Document import | "I'll parse this document and extract relevant information." |
| Sent from assess (Recent Actions mentions assessment with gaps) | Targeted dive | "Assessment found we need more detail on {area}. Let's dig into that." For [needs-supplement] items, focus on re-extracting missing dimensions from existing entries. |

## Workflow

### Mode: Active Description

#### Phase 1: Open Exploration

Start naturally. Follow the user's lead. Do NOT direct the conversation.

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

Organize scattered information into entries using frameworks in `references/extract-frameworks.md`.

Map each piece of information to the entry template in `references/entry-template.md`.

If structuring reveals gaps → go back to Phase 3.

#### Phase 5: Confirm and Write

For each entry:

1. Determine entry type: `project` (has company/project context), `signal` (standalone capability), `achievement` (specific milestone)
2. Check if a similar entry already exists in `.career/entries/`
3. Present the structured entry to the user. Ask: "Does this look accurate? Anything to correct?"
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

Present all draft entries to the user in summary form. Ask user to confirm or correct each one before saving.

If education or contact info is found → offer to update `.career/profile.md` as well.

## Cross-Dimension Information Capture

During any mode of capture, if the user mentions information that belongs to a different dimension:

- Profile-related info (education, contact, certifications) → offer to update `.career/profile.md`
- Career direction or goals → offer to update `target_direction` in `.career/context.md`

Any skill can suggest triggering capture when relevant information surfaces in conversation.

## After Writing

Update `.career/context.md`:
- Add entry to Entries section
- Add action to Recent Actions

## Freedom Note

Active description mode has HIGH freedom. The phases above are guidelines, not a rigid script. When the user is freely sharing valuable details, let them continue without interruption. Phase transitions are fluid — return to earlier phases as needed.

Session review mode has LOWER freedom — stick to the "at most 2 highlights" constraint. Resist the urge to capture everything.

## Next Step

After capture is complete, ask: "I've captured {N} entries. Shall I assess what we have so far?"

If user confirms, invoke `/career-mind:assess` immediately.

## Output

- Entry files in `.career/entries/`
- Updated `.career/context.md`
- Optionally updated `.career/profile.md`
- Auto-proceed to assess (if user confirms)

---
name: career-extract
description: Extract and structure career experiences through open conversation. Helps users discover and articulate their professional achievements. Works without JD dependency.
---

# Career Extract

## Context Loading

1. Read `~/.career/context.md` to check extracted projects and avoid re-covering ground.
2. If context.md missing → tell user to run `/career:career-init` first. Stop.
3. Read existing materials in `~/.career/materials/` to know what's already captured.
4. Optionally read `~/.career/profile.md` for user context.

## Hard Constraints

- **Confirmation gate:** Every material entry must be confirmed by the user before writing to ~/.career/materials/
- **Three-dimension check:** Each entry must cover: (1) what was done, (2) how it was done, (3) what resulted. Missing any → follow-up before confirming
- **User verbatim:** Always capture and preserve the user's exact words. These are the most valuable output
- Ask ONE question at a time
- Never mention SOAR/STAR to the user — these are internal organizing tools only

## Mode Detection

| Trigger | Mode | Opening |
|---------|------|---------|
| User runs `/career:career-extract` directly | Full scan | "What have you been working on recently?" or "Which experience would you like to start with?" |
| User was sent from review (context.md has Recent Actions mentioning review) | Targeted dive | "Review found your experience at {company} could use more detail. Let's dig into that." |

## Workflow

### Phase 1: Open Exploration

Start naturally. Follow the user's lead. Do NOT direct the conversation — let the user decide what to talk about.

If full scan: "Which experience would you like to start with?"
If targeted: "Let's talk about the {project} you did at {company}."

Listen. Capture everything. Do not judge or filter yet.

### Phase 2: Signal Detection

Watch for valuable signals in the user's responses. When you hear something interesting, follow up naturally:

"Wait, you mentioned switching approaches there — can you say more about that?"

Like a journalist catching a lead — not like a form-filling exercise.

Use the trigger patterns in `references/questioning-triggers.md` to decide when and how to follow up.

### Phase 3: Dimension Filling

Based on collected content, identify missing dimensions and ask naturally:

- "You mentioned the results were good — do you have specific numbers?"
- "Did you consider other options for that approach?"
- "What was your personal contribution to this project?"

Dimensions emerge from conversation. Do NOT present a checklist to the user.

### Phase 4: Structuring

Organize scattered information into material entries using frameworks in `references/extract-frameworks.md`.

Map each piece of information to the material template in `references/material-template.md`.

If structuring reveals gaps → go back to Phase 3.

### Phase 5: Confirm and Write

For each material entry:

1. Check if file `~/.career/materials/{company}_{project}_{NN}.md` already exists
2. If exists → show user a summary of what's already captured, then present new content alongside. Ask: "Is this new content accurate? Anything to correct?"
3. If not exists → present the structured entry to the user. Ask: "Does this look accurate? Anything to correct?"
4. If user confirms → set `confirmed: true`
   - **File exists (re-extraction):** Append new content under `## Re-extraction YYYY-MM-DD` heading at end of file. Also append new items to `## Highlights` and `## Quantifiable Metrics` sections (mark with date). Do NOT modify YAML frontmatter or delete existing content
   - **File does not exist (new):** Create file following `references/material-template.md` format
5. If user corrects → update and re-confirm

After writing, update `~/.career/context.md`:
- Add project to Extracted Projects section
- Add action to Recent Actions section

## Freedom Note

This skill has HIGH freedom. The phases above are guidelines, not a rigid script. When the user is freely sharing valuable details, let them continue without interruption. Phase transitions are fluid — return to earlier phases as needed.

## Output

- Material files in `~/.career/materials/`
- Updated `~/.career/context.md`

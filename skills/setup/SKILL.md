---
name: setup
description: First-time setup for career-mind. Creates .career/ directory, collects profile info, establishes career context, imports existing materials. Use when user says 'career setup', 'first time', 'initialize', 'get started', or mentions setting up their career context.
---

# Career Setup

## Context Loading

1. Check whether `.career/` directory exists.
2. If exists: read `.career/context.md`. This is a re-setup — fill gaps only, never overwrite.
3. If not exists: proceed with fresh setup.

## Hard Constraints

- NEVER overwrite existing profile fields — only fill missing ones
- NEVER delete existing files in .career/
- When collecting structured info (profile, career stage), present options as a numbered choice list. Reserve free-text for open-ended topics
- All file writes create new files or edit existing files — never overwrite entire files when appending

## Workflow

### Step 1: Create Directory Structure

Create `.career/` with subdirectories: `entries/`, `outputs/`.

### Step 2: Collect Profile

Present a structured form collecting: name, contact info (phone/email), city, education background. Group into a single interaction when possible.

Write to `.career/profile.md` using template at `references/profile-template.md`.

### Step 3: Career Stage

Present as a numbered choice: "What are you focusing on right now?"
- a) Preparing for future opportunities → `preparing`
- b) Actively job searching → `active-seeking`
- c) Recent or upcoming graduate → `graduate`
- d) Career change / transition → `career-change`
- e) Performance review or promotion → `performance`
- f) General career development → `development`
- g) Other → `other`

Note: career stage is broader than job-seeking. It captures the user's current career context and goals.

### Step 4: Target Direction (optional)

"What direction are you heading? For example: target role, industry, level, or career goal."
- Has direction → record for context.md
- No → skip, mark as "none"

### Step 5: Import Existing Materials (optional)

"Do you have any existing documents you'd like to import? For example: resume, performance review, LinkedIn profile, project documentation."
- If provided → save originals to `.career/outputs/`, then parse content into draft entries. Present extracted entries for confirmation using capture confirmation logic (three-dimension check, user confirms before saving).
- If none → skip.

### Step 6: Initialize Context

Create `.career/context.md` following schema at `references/state-schema.md`.

Fill in: profile status, career_stage, target_direction, last_assessment=none.

### Step 7: Next Step

Always proceed to capture: "Setup complete. Shall we start capturing your capabilities and experiences?"

If user confirms, invoke `/career-mind:capture` immediately.

## Output

- `.career/` directory with subdirectories (entries/, outputs/)
- `.career/profile.md`
- `.career/context.md`
- Imported entries in `.career/entries/` (if user provided documents)
- Auto-proceed to capture (if user confirms)

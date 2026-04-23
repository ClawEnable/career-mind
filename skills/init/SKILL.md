---
name: init
description: Initialize career-mind workspace. Creates .career/ directory, collects profile info, establishes career context, imports existing materials. Use when user says 'career init', 'initialize', 'get started', 'first time', or mentions setting up their career context.
---

# Career Init

## Context Loading

1. Check whether `.career/` directory exists.
2. If exists: read `.career/context.md`. This is a re-initialization — fill gaps only, never overwrite.
3. If not exists: proceed with fresh initialization.

## Hard Constraints

- NEVER overwrite existing profile fields — only fill missing ones
- NEVER delete existing files in .career/
- When collecting structured info (profile, career stage), present options as a numbered choice list. Reserve free-text for open-ended topics
- All file writes create new files or edit existing files — never overwrite entire files when appending
- Environment scan MUST happen before any user interaction. Maximize extraction from existing files, minimize manual input

## Workflow

### Step 1: Environment Scan (no user interaction)

Before asking the user anything, scan the current working directory for career-related files:

1. List all files in the working directory and immediate subdirectories (exclude `.career/`, `.git/`, `.obsidian/`, `node_modules/`)
2. Identify career-relevant files by name pattern and extension:
   - Resumes/CVs: files containing "简历", "CV", "resume", "curriculum" in filename, or `.pdf`/`.md`/`.docx` files with career-related content
   - Performance reviews: files containing "绩效", "review", "performance"
   - LinkedIn exports: files containing "linkedin", "LinkedIn"
   - Project documentation: any remaining `.md` or `.docx` files
3. Read identified files and extract:
   - Personal info (name, phone, email, city)
   - Education background
   - Work experience (company, period, role, projects)
   - Skills and technologies
   - Quantified achievements/metrics
4. Store extracted data in memory for use in subsequent steps

If no files found → proceed normally, ask user for all info.
If files found → use extracted data to pre-fill everything in the following steps.

### Step 2: Create Directory Structure

Create `.career/` with subdirectories: `entries/`, `outputs/`.

If career-related files were found, copy originals to `.career/outputs/`.

### Step 3: Collect Profile (pre-filled if possible)

If Step 1 extracted personal info: present the extracted info for confirmation:
"I found your information from {filename}: {name}, {phone}, {email}, {city}, {education}. Is this correct? Anything to add or change?"

If Step 1 found nothing: present a structured form collecting: name, contact info (phone/email), city, education background. Group into a single interaction when possible.

Write to `.career/profile.md` using template at `references/profile-template.md`.

### Step 4: Career Stage

Present as a numbered choice: "What are you focusing on right now?"
- a) Preparing for future opportunities → `preparing`
- b) Actively job searching → `active-seeking`
- c) Recent or upcoming graduate → `graduate`
- d) Career change / transition → `career-change`
- e) Performance review or promotion → `performance`
- f) General career development → `development`
- g) Other → `other`

Note: career stage is broader than job-seeking. It captures the user's current career context and goals.

### Step 5: Target Direction (optional)

"What direction are you heading? For example: target role, industry, level, or career goal."
- Has direction → record for context.md
- No → skip, mark as "none"

### Step 6: Import Existing Materials

**If Step 1 found files and extracted work experience:**

Parse extracted content into draft entries following `references/entry-template.md` format (with full YAML frontmatter: id, type, source, source_detail, tags, period, confirmed, captured_at). Set `source: imported`.

Before creating drafts, check `.career/entries/` for existing entries covering the same project or topic. If duplicates are found, skip those drafts and note them for the user: "Skipping {topic} — already captured in {existing entry filename}."

Present all draft entries in summary form. Ask user to confirm or correct before saving. Confirmation here means **structural accuracy only** — "does this match what your resume says?" Depth and missing dimensions (how/why decisions, specific challenges, personal contribution details) will be addressed by capture's post-import analysis.

After user confirms → set `confirmed: true`. If user corrects → update and re-confirm.

**If Step 1 found nothing:**

"Do you have any existing documents you'd like to import? For example: resume, performance review, LinkedIn profile, project documentation."
- If provided → save originals to `.career/outputs/`, parse into entries following `references/entry-template.md`, present for confirmation. Set `confirmed: true` after user confirms.
- If none → skip.

### Step 7: Initialize Context

Create `.career/context.md` following schema at `references/state-schema.md`.

Fill in: profile status, career_stage, target_direction, last_assessment=none.

If entries were imported, record them in the Entries section with `(imported: YYYY-MM-DD)`.

Record actions in Recent Actions using standardized keywords:
- `YYYY-MM-DD: init — {what was auto-extracted vs manually provided}`
- `YYYY-MM-DD: import — {N} entries imported from {source description}` (if applicable)

### Step 8: Next Step

Always proceed to capture: "Init complete. Shall we start capturing your capabilities and experiences?"

If user confirms, invoke `/career-mind:capture` immediately.

## Output

- `.career/` directory with subdirectories (entries/, outputs/)
- `.career/profile.md`
- `.career/context.md`
- Original files in `.career/outputs/` (if found or provided)
- Imported entries in `.career/entries/` following entry-template.md format (if documents found/provided)
- Auto-proceed to capture (if user confirms)

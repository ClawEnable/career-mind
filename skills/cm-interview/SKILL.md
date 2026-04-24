---
name: cm-interview
description: Prepare for job interviews based on career entries and generated resume. Use when user says 'interview prep', 'practice interview', 'mock interview', 'prepare for interview', 'interview questions', or has completed craft (resume) and wants to prepare. Generates deep-dive questions, project talking points, weakness strategies, and reverse questions. Adapts to user's role type.
---

# Career Interview Prep

## Context Loading

1. Read `.career/context.md` for career stage and target direction.
2. If context.md missing → tell user to run `/career-mind:cm-init` first. Stop.
3. Read `.career/profile.md` for basic info (name, education) — needed for self-introduction prep.
4. Load resume if available: find the latest `resume_*.md` file in `.career/outputs/`. If no resume exists, work from entries directly.
5. Load entries from `.career/entries/` (including any supplement sections — merge all rounds for the most complete picture).
6. Detect user type from target direction or entry content. Use `references/interview-types.md` for adaptation.

## Hard Constraints

- **Career-stage adaptation:** Read `career_stage` from context.md and adjust interview prep strategy: graduate→focus on problem-solving approach and learning ability; mid-career→focus on depth of technical decisions and ownership evidence; senior/lead→focus on scope of influence, strategic thinking, and cross-team impact; career-change→focus on motivation narrative and transferable skill demonstration.
- **Collection processing:** When a step requires processing multiple items (projects, questions, talking points), follow the closed loop: (1) declare the full set — "Need to process {N} items: {list}", (2) process each item with progress marking, (3) confirm completion — "All {N} items processed."
- **Execution self-check:** Before advancing to the next step, verify: (a) collection operations (each/all/per) — all items processed? (b) compound actions (A and B) — all sub-actions executed? (c) qualitative actions (analyze/explain/suggest) — output has substantive content, not just framework-level mention?

## Workflow

### Step 1: Extract Key Experiences

From resume and/or entries, identify:
- 2-3 core projects with strongest impact
- Technologies and skills mentioned (from entry tags)
- Any quantified achievements
- Employment timeline including gaps

### Step 2: Generate Deep-Dive Questions

Declare core projects: "Generating questions for {N} core projects: {list}. For each project, produce at least 3 questions covering at least 3 different angles (e.g., technical depth, behavioral context, quantification, scope, decision reasoning — angles adapt to the project's nature)."

For each core project, predict interviewer follow-up questions. Present questions grouped by project, with the question angle labeled for each.

Mark **high-risk entries** that might invite scrutiny:
- Vague or unsubstantiated claims (metrics without baselines)
- Short tenures (under 1 year)
- Scope inflation risk (project too large for stated role)
- Unexplained career transitions

### Step 3: Prepare Project Talking Points

For each core project (declared in Step 2), prepare both versions. Present each project's talking points in a structured format:

**Short version (1 min):** Situation → Key action → Result
**Detailed version (3 min):** Situation → Challenge → Decision process → Action → Result → Lesson

Prefer **user verbatim** from entries over polished resume text. Speaking naturally beats reciting optimized phrases.

Present all talking points grouped by project. Let user review and adjust in their own words.

### Step 4: Weakness Strategies

Based on user's actual situation (auto-detect, only prepare relevant ones). For each relevant strategy, produce a personalized response framework — not just the generic table. Include the user's specific context (which entry, which timeline, which gap) and how to frame it positively. For each strategy, recommend the approach most likely to succeed with reasoning: "I'd suggest [strategy] because [reasoning specific to your context]."

| Situation | Strategy |
|-----------|----------|
| Short tenure (<1 year) | Frame as intensive learning, specific achievements in short time |
| Employment gap | Honest explanation + what was learned/done during gap |
| Career change | Motivation narrative + transferable skill mapping |
| No management experience for senior role | Leading through influence, technical mentorship examples |
| Broad but shallow experience | Pick 2-3 areas of depth, show T-shaped profile |

### Step 5: Reverse Questions

Generate 3-5 questions for the user to ask the interviewer:
- Based on target direction and industry
- Show genuine interest and strategic thinking
- Avoid generic questions ("what's the culture like?")

### Step 6: Optional Mock Interview

If user wants practice: "Would you like to do a mock interview? I can play the interviewer."

Mock interview structure:
- Start with a low-pressure question ("Tell me about a recent project you're proud of")
- Progress to probing follow-ups based on their response
- After each response, give structured feedback on:
  1. **Clarity:** Was the answer understandable to someone unfamiliar with the project?
  2. **Specificity:** Did it include concrete details, metrics, or examples?
  3. **Structure:** Was there a clear situation → action → result flow?
  4. **Depth:** Did it demonstrate judgment and decision-making, not just execution?
- Mix question types: alternate between technical deep-dives, behavioral questions, and collaboration scenarios
- After 3-5 questions, give an overall assessment with specific improvement areas

## Next Step

After prep is complete:

| Condition | Next Step |
|-----------|-----------|
| User wants to check overall readiness | Ask: "Want to check your overall career status?" → `/career-mind:cm-status` |
| User wants to iterate on resume | Ask: "Shall I assess or improve your materials?" → `/career-mind:cm-assess` or `/career-mind:cm-craft` |

If user confirms, invoke the next skill immediately.

## Output

Interview prep content must be fully presented in conversation before optionally saving to file. Present each step's output (questions, talking points, weakness strategies, reverse questions) as it's generated. If saving to file, confirm: "I've saved the full prep to `.career/outputs/interview_prep_YYYYMMDD.md`. The key points are: {summary}."

- Interview prep document (presented in conversation, optionally saved to `.career/outputs/interview_prep_YYYYMMDD.md`)
- Updated `.career/context.md` (Recent Actions) using the `interview` keyword
- Auto-proceed to next recommended skill (if user confirms)

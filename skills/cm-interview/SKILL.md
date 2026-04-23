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

## Workflow

### Step 1: Extract Key Experiences

From resume and/or entries, identify:
- 2-3 core projects with strongest impact
- Technologies and skills mentioned (from entry tags)
- Any quantified achievements
- Employment timeline including gaps

### Step 2: Generate Deep-Dive Questions

For each core project, predict interviewer follow-up questions:

- Technical: "Why did you choose X approach over Y?"
- Behavioral: "How did you handle disagreement in this project?"
- Quantification: "How did you measure the 20% improvement?"
- Scope: "What was the team size? Your specific role?"

Mark **high-risk entries** that might invite scrutiny:
- Vague or unsubstantiated claims (metrics without baselines)
- Short tenures (under 1 year)
- Scope inflation risk (project too large for stated role)
- Unexplained career transitions

### Step 3: Prepare Project Talking Points

For each core project, prepare:

**Short version (1 min):** Situation → Key action → Result
**Detailed version (3 min):** Situation → Challenge → Decision process → Action → Result → Lesson

Prefer **user verbatim** from entries over polished resume text. Speaking naturally beats reciting optimized phrases.

Let user review and adjust in their own words.

### Step 4: Weakness Strategies

Based on user's actual situation (auto-detect, only prepare relevant ones):

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

- Ask one question at a time, give specific feedback after each response
- Focus on clarity and specificity of expression

## Next Step

After prep is complete:

| Condition | Next Step |
|-----------|-----------|
| User wants to check overall readiness | Ask: "Want to check your overall career status?" → `/career-mind:cm-status` |
| User wants to iterate on resume | Ask: "Shall I assess or improve your materials?" → `/career-mind:cm-assess` or `/career-mind:cm-craft` |

If user confirms, invoke the next skill immediately.

## Output

- Interview prep document (presented in conversation, optionally saved to `.career/outputs/interview_prep_YYYYMMDD.md`)
- Updated `.career/context.md` (Recent Actions) using the `interview` keyword
- Auto-proceed to next recommended skill (if user confirms)

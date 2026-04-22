---
name: career-interview
description: Prepare for job interviews based on resume and materials. Generates deep-dive questions, project talking points, weakness strategies, and reverse questions. Adapts to user's role type.
---

# Career Interview Prep

## Context Loading

1. Read `~/.career/context.md` for career stage and target direction.
2. If context.md missing → tell user to run `/career:career-init` first. Stop.
3. Read `~/.career/profile.md` for basic info (name, education) — needed for self-introduction prep.
4. Load resume: read `last_resume` from context, or ask user for file path.
5. Load materials from `~/.career/materials/` if available (including any `## Re-extraction` sections — merge all rounds for the most complete picture).
6. Detect user type from target direction or resume content. Use `references/interview-types.md` for adaptation.

## Workflow

### Step 1: Extract Key Experiences

From resume (and materials if available), identify:
- 2-3 core projects with strongest impact
- Technologies and skills mentioned
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

Prefer **user_verbatim** from materials over polished resume text. Speaking naturally beats reciting optimized phrases.

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

- Ask one question at a time
- After user responds, give specific feedback: "That was clear" / "This part could be more specific, for example..."
- Focus on clarity and specificity of expression

## Output

Present as a structured prep document. Optionally save to `~/.career/interview_prep_[date].md` if user requests.

Update `~/.career/context.md` Recent Actions.

# career-mind

Career capability management plugin. Captures, assesses, and presents professional capabilities for any career scenario.

## Skills

This plugin provides 6 skills, each defined in a `SKILL.md` file:

| Skill | Purpose |
|-------|---------|
| `cm-init` | Initialize career context — scan for documents, collect profile, import existing materials |
| `cm-capture` | Multi-mode information capture with diagnostic triggers: post-import analysis, active description, session review, document import |
| `cm-assess` | Evaluate information quality with diagnostic insights, identify gaps with actionable recommendations, optionally target a specific scenario |
| `cm-craft` | Generate career artifacts (resume, performance review, promotion case, skill map) with source tracing, audience calibration, and cherry-picking detection |
| `cm-interview` | Interview prep: technical, behavioral, and collaboration questions, structured mock interview with feedback |
| `cm-status` | Check current status and recommend next step |

## Workflow

```
cm-init → cm-capture ⇄ cm-assess → cm-craft (any scenario) → cm-interview (optional)
                   ↑              │
                   └──────────────┘  (cm-assess finds gaps → cm-capture fills them)
```

Start anywhere based on what you need. If unsure, begin with `cm-init`.

## Data Storage

User data is stored in `.career/` within the current working directory:

```
.career/
├── profile.md       # Name, contact, education (enrichable over time)
├── context.md       # Cross-skill state (YAML frontmatter)
├── entries/         # Capability library (project, signal, achievement entries)
└── outputs/         # Generated artifacts (resumes, assessments, etc.)
```

## Key Principles

- **Anti-fabrication:** Every artifact bullet traces to a verified source — no invented metrics, no inflated skills, no cherry-picked evidence without qualifying context
- **User verbatim:** The user's own words are the most valuable output; preserve them
- **Progressive disclosure:** Skills load detailed references on demand, keeping context efficient
- **Multi-source capture:** Information comes from conversation, work session review, or document import
- **Domain-first inference:** Skills use domain expertise to understand content before asking questions, minimizing user input
- **Infer-then-option interaction:** Generate polished statement options with estimated values; recommend the most likely option with reasoning rather than presenting choices without guidance
- **Career-stage adaptation:** Behavior adapts based on career stage — graduate, mid-career, senior, career-change each receive different capture emphasis, assessment weighting, and output strategy
- **Advisory recommendation:** Skills recommend with reasoning ("I'd suggest X because Y"), not just present options
- **Diagnostic intelligence:** Capture detects underestimate patterns, positioning mismatches, and flat career narratives through conversational triggers
- **Insight over score:** Assessment produces diagnostic insights with consequences and actionable recommendations, not just dimension scores
- **Audience calibration:** Output considers ATS systems, HR screeners, and hiring managers simultaneously
- **Interaction gating:** Each step requiring user input completes its full interaction cycle before the next begins
- **Multi-scenario output:** Generate any career artifact, not just resumes

## For Skill Consumers

Each skill directory follows the Agent Skills open standard:
- `SKILL.md` — skill definition with metadata frontmatter
- `references/` — detailed reference documents loaded on demand by the skill

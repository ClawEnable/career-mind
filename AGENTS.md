# career-mind

Career capability management plugin. Captures, assesses, and presents professional capabilities for any career scenario.

## Skills

This plugin provides 6 skills, each defined in a `SKILL.md` file:

| Skill | Purpose |
|-------|---------|
| `cm-init` | Initialize career context — scan for documents, collect profile, import existing materials |
| `cm-capture` | Multi-mode information capture: post-import analysis with domain inference, active description, session review, document import |
| `cm-assess` | Evaluate information quality and completeness, identify gaps, optionally target a specific scenario |
| `cm-craft` | Generate career artifacts (resume, performance review, promotion case, skill map) with source tracing |
| `cm-interview` | Interview prep with deep-dive questions, talking points, weakness strategies, mock interview |
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

- **Anti-fabrication:** Every artifact bullet traces to a verified source — no invented metrics or inflated skills
- **User verbatim:** The user's own words are the most valuable output; preserve them
- **Progressive disclosure:** Skills load detailed references on demand, keeping context efficient
- **Multi-source capture:** Information comes from conversation, work session review, or document import
- **Domain-first inference:** Skills use domain expertise to understand content before asking questions, minimizing user input
- **Infer-then-option interaction:** Generate polished statement options with estimated values rather than asking open-ended questions
- **Multi-scenario output:** Generate any career artifact, not just resumes

## For Skill Consumers

Each skill directory follows the Agent Skills open standard:
- `SKILL.md` — skill definition with metadata frontmatter
- `references/` — detailed reference documents loaded on demand by the skill

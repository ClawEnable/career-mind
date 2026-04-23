# career-mind

Career capability management plugin. Captures, assesses, and presents professional capabilities for any career scenario.

## Skills

This plugin provides 6 skills, each defined in a `SKILL.md` file:

| Skill | Purpose |
|-------|---------|
| `setup` | Establish career context — create `.career/` directory, collect profile, import existing documents |
| `capture` | Multi-mode information capture: active description, session review, document import |
| `assess` | Evaluate information quality and completeness, identify gaps, optionally target a specific scenario |
| `craft` | Generate career artifacts (resume, performance review, promotion case, skill map) with source tracing |
| `interview` | Interview prep with deep-dive questions, talking points, weakness strategies, mock interview |
| `status` | Check current status and recommend next step |

## Workflow

```
setup → capture ⇄ assess → craft (any scenario) → interview (optional)
                   ↑              │
                   └──────────────┘  (assess finds gaps → capture fills them)
```

Start anywhere based on what you need. If unsure, begin with `setup`.

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
- **Multi-scenario output:** Generate any career artifact, not just resumes

## For Skill Consumers

Each skill directory follows the Agent Skills open standard:
- `SKILL.md` — skill definition with metadata frontmatter
- `references/` — detailed reference documents loaded on demand by the skill

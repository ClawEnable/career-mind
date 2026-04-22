# Career Plugin

Universal job-seeking engineering framework. Turns job-seeking into a repeatable engineering process.

## Skills

This plugin provides 6 skills, each defined in a `SKILL.md` file:

| Skill | Purpose |
|-------|---------|
| `career-init` | First-time setup — creates `~/.career/` directory, collects profile info, detects existing materials |
| `career-extract` | Open conversation to explore and structure career experiences into material entries |
| `career-review` | Multi-perspective resume review with scored dimensions and issue classification |
| `career-tailor` | Improve or generate resume content with strict source tracing (no fabrication) |
| `career-interview` | Interview prep with deep-dive questions, talking points, weakness strategies, mock interview |
| `career-status` | Check current preparation status and recommend next step |

## Workflow

```
init → extract → review → tailor → interview
         ↑          │
         └──────────┘  (review finds gaps → extract fills them)
```

Start anywhere based on what you have. If unsure, begin with `career-init`.

## Data Storage

All user data is stored locally at `~/.career/`:

```
~/.career/
├── profile.md       # Name, contact, education
├── context.md       # Cross-skill state (YAML frontmatter)
├── materials/       # Extracted experience entries
├── reviews/         # Review reports
└── resumes/         # Resume versions (original + drafts)
```

## Key Principles

- **Anti-fabrication:** Every resume bullet traces to a verified source — no invented metrics or inflated skills
- **User verbatim:** The user's own words are the most valuable output; preserve them
- **Progressive disclosure:** Skills load detailed references on demand, keeping context efficient

## For Skill Consumers

Each skill directory follows the Agent Skills open standard:
- `SKILL.md` — skill definition with metadata frontmatter
- `references/` — detailed reference documents loaded on demand by the skill

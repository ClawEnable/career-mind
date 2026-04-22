# Contributing to Career Plugin

Thank you for your interest in contributing!

## Skill Structure

Each skill follows the Agent Skills open standard:

```
skills/
└── career-{name}/
    ├── SKILL.md              # Skill definition (required)
    └── references/           # Detailed reference docs (optional)
        └── *.md
```

**Rule:** The directory name must exactly match the `name` field in `SKILL.md` frontmatter (kebab-case).

## Guidelines

- **No fabricated content:** Skills must never instruct agents to invent metrics, inflate skills, or fabricate achievements
- **Agent-agnostic:** Avoid agent-specific tool references (e.g., "Use Write tool"). Describe actions generically
- **Progressive disclosure:** Keep SKILL.md concise. Put detailed rules in `references/` files
- **Cross-skill references:** Use the full `/career:career-xxx` format when referencing other skills
- **English only:** All skill content must be in English

## Making Changes

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Verify: directory names match SKILL.md `name` fields
5. Verify: no agent-specific tool references
6. Verify: cross-skill command references are correct
7. Submit a pull request

## Reporting Issues

Use the GitHub issue templates for bug reports and feature requests.

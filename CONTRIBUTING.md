# Contributing to career-mind

Thank you for your interest in contributing!

## Skill Structure

Each skill follows the Agent Skills open standard:

```
skills/
└── {name}/
    ├── SKILL.md              # Skill definition (required)
    └── references/           # Detailed reference docs (optional)
        └── *.md
```

**Rule:** The directory name must exactly match the `name` field in `SKILL.md` frontmatter (kebab-case).

## Guidelines

- **No fabricated content:** Skills must never instruct agents to invent metrics, inflate skills, or fabricate achievements
- **Semantic interaction descriptions:** Describe interaction structure, not specific tools. Write "Present structured choices when options are known" not "Use AskUserQuestion tool". Write "Save file to .career/path" not "Use Write tool". Agents map semantic descriptions to their native mechanisms.
- **Progressive disclosure:** Keep SKILL.md concise. Put detailed rules in `references/` files
- **Cross-skill references:** Use the full `/career-mind:xxx` format when referencing other skills
- **English only:** All skill content must be in English

## Making Changes

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Verify: directory names match SKILL.md `name` fields
5. Verify: interaction descriptions are semantic, not tool-specific
6. Verify: cross-skill command references are correct
7. Submit a pull request

## Reporting Issues

Use the GitHub issue templates for bug reports and feature requests.

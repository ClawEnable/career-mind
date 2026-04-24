# Entry Template

Each entry is a single file in `.career/entries/`. Filename format: `{type}_{name}_{NN}.md` where:
- `type`: project, signal, or achievement
- `name`: short descriptive name (kebab-case)
- `NN`: zero-padded index (01, 02, ...)

## File Format

```markdown
---
id: "{type}_{name}_{NN}"
type: "<project | signal | achievement>"
source: "<observed | extracted | imported>"
source_detail: "{description of where this came from}"
tags: ["{tag1}", "{tag2}", ...]
period: "{YYYY-MM to YYYY-MM}"
confirmed: true
captured_at: "YYYY-MM-DD"
---

## Summary
{one-line summary}

## Details
{full description. For project type: company, role, project context. For signal type: observation context. For achievement type: milestone description.}

## Evidence
{specific examples, user verbatim, metrics}

## Highlights
- {bullet 1}
- {bullet 2}

## Quantifiable Metrics
- {metric name}: {value with unit}
```

## Entry Types

| Type | When to use | Key fields |
|------|------------|-----------|
| project | Experience tied to a company/project with a time range | period, company/role in Details |
| signal | Standalone capability observation, not tied to a specific project | observation context in Details |
| achievement | Specific milestone or recognition | milestone description in Details |

## Source Types

| Source | Meaning |
|--------|---------|
| extracted | User described this in conversation |
| observed | Agent identified this from reviewing a work session |
| imported | Parsed from an existing document |

## Tag Guidelines

- Use lowercase, hyphenated tags: "ios", "swift", "performance-optimization"
- Include technology tags: "react", "python", "kubernetes"
- Include skill tags: "system-design", "debugging", "mentoring"
- Include domain tags: "mobile", "backend", "data-engineering"

## Supplement Rules

When the same topic is captured again (file already exists):

1. **Do NOT overwrite** existing content or YAML frontmatter
2. **Append** new highlights to `## Highlights` (add `- {new highlight} (added YYYY-MM-DD)`)
3. **Append** new metrics to `## Quantifiable Metrics` (add `- {new metric} (added YYYY-MM-DD)`)
4. **Append full snapshot** at end of file under `## Supplement YYYY-MM-DD` heading
5. **Update Details** only if significantly different — merge, do not delete

## Import Granularity Rules

When creating entries from imported documents or resume parsing:

- **Default: one `project` entry per company role.**
  - One person may hold multiple roles at one company → one entry per role
  - Multiple projects under the same role are listed as separate highlights
  - Rationale: preserves company-level context (role positioning, team scale, reporting structure)

- **Exception — a single project may get its own entry only when:**
  - It spans a significantly different time period (>50% of role duration)
  - It involves a fundamentally different tech stack or responsibility domain from the role's other work
  - The role-level entry would exceed 5 highlights AND at least 2 highlights span different product lines

- **Naming for role-level entries:**
  `{type}_{company-kebab}_{NN}.md` (e.g., `project_company-a_01.md`)
  Multi-role at same company: `project_company-a_01.md`, `project_company-a_02.md`

## Key Rules

- **user_verbatim** is mandatory in Evidence section. Craft and interview prefer user's own words
- **confirmed** must be `true` before the file is written
- Three dimensions must be covered before confirmation:
  1. What was done (specific actions)
  2. How it was done (methods/decisions/approach)
  3. What resulted (outcomes/impact/data)
  Missing any dimension → ask follow-up before writing

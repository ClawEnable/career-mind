# Material Entry Template

Each material entry is a single file in `~/.career/materials/`. Filename format: `{company}_{project}_{NN}.md` where NN is a zero-padded index.

## File Format

```markdown
---
id: "{company}_{project}_{NN}"
company: "{company name}"
period: "{time range}"
project: "{project name}"
role: "{lead | core | contributor}"
source: "{full-scan | targeted-dive}"
confirmed: true
created_at: "YYYY-MM-DD"
---

## User Verbatim
> "{exact words from user conversation}"

## Core Content
{structured summary of what user described}

## Highlights
- {specific achievement or outcome 1}
- {specific achievement or outcome 2}

## Quantifiable Metrics
- {metric name}: {value with unit}

## History
{if re-extracted on YYYY-MM-DD: append new content below, old content preserved here}
```

## Re-extraction Rules

When the same project is extracted again (file already exists):

1. **Do NOT overwrite** existing content or YAML frontmatter
2. **Append new verbatim** to end of `## User Verbatim` section (add `> "{new words}"`)
3. **Append new highlights** to end of `## Highlights` section (add `- {new highlight} (added YYYY-MM-DD)`)
4. **Append new metrics** to end of `## Quantifiable Metrics` section (add `- {new metric} (added YYYY-MM-DD)`)
5. **Append full snapshot** at end of file under `## Re-extraction YYYY-MM-DD` heading containing the complete new entry (verbatim, core content, highlights, metrics)
6. **Update Core Content** only if the new extraction provides significantly different information — use Edit to merge, do not delete old content

## Key Rules

- **user_verbatim** is mandatory. Tailor and interview prefer user's own words over polished text
- **confirmed** must be `true` before the file is written. Extract skill confirms with user first
- Three dimensions must be covered before confirmation:
  1. What was done (specific actions)
  2. How it was done (methods/decisions/approach)
  3. What resulted (outcomes/impact/data)
  Missing any dimension → ask follow-up before writing

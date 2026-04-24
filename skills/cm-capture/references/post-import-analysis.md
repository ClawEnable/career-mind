# Post-Import Analysis

This mode runs when entries were imported during Init but haven't been assessed or deepened yet. The goal is to analyze entries from a domain-expert perspective, identify genuinely non-inferable gaps, and iteratively refine entries through option-based interaction.

## Phase 0: Determine Analysis Perspective

Read `context.md` and extract `target_direction`. This field drives the analysis lens — what counts as a critical gap depends on what role the user is targeting.

### Perspective Mapping

Extract key characteristics from `target_direction` to dynamically compose an analysis perspective. Do NOT use a fixed role enumeration. Instead, determine emphasis along these independent axes:

| Axis | What it controls | How to detect from target_direction |
|---|---|---|
| **Depth vs. Breadth** | Whether analysis prioritizes deep technical reasoning or cross-domain capability breadth | Depth signals: "architect", "lead", "senior", "specialist". Breadth signals: "fullstack", "cross-platform", "generalist", "TPM" |
| **Individual vs. Team impact** | Whether analysis prioritizes personal execution quality or leadership/influence evidence | Individual signals: "IC", "engineer", "developer". Team signals: "manager", "lead", "director", "head" |
| **Technical vs. Business outcomes** | Whether analysis prioritizes system-level results or business-level metrics | Technical signals: role titles emphasizing tech skills. Business signals: "product", "growth", "strategy", "revenue" |

Combine the axes to form a weighted priority table for gap classification. For example:
- A "Senior Backend Engineer" would weight depth > breadth, individual > team, technical > business
- A "Technical Program Manager" would weight breadth > depth, team > individual, business > technical

If `target_direction` is unclear, apply balanced weighting across all axes.

If `target_direction` contains multiple targets, use the most senior/targeted role as the primary lens, but note implications for other targets.

Document the chosen perspective — it shapes all subsequent phases.

## Phase 0.5: Framework Alignment

Before starting analysis, align with the user on what you're about to do:

"I've imported {N} entries covering {brief domain summary}. Based on your target direction ({target_direction}), I'll analyze with emphasis on {derived perspective from axes}. I'll identify information gaps and generate options to fill them. Sound good? Or should I adjust the focus?"

Wait for user confirmation before proceeding. If user adjusts focus, update the perspective accordingly.

## Phase 1: Two-Layer Analysis

Review all existing entries through the lens established in Phase 0. Adapt analysis depth per entry based on its current information density: entries with rich detail deserve deeper inference and more targeted gap identification; thin entries need broader coverage before narrowing. Do not apply uniform depth to all entries.

For each entry, perform two layers:

### Layer 1 — Domain Inference (understand first)

Using your domain expertise and the Phase 0 perspective, infer what you can already understand from the entry content:

- **Architecture patterns**: Why they make sense for the described scope and constraints
- **Technical decisions**: Which are standard practice vs. which represent genuine innovation
- **Scale and complexity**: What can be inferred from described scope (user count, team size, business impact)
- **Trade-offs**: What a practitioner at the target level would recognize as the implicit reasoning
- **Likely metrics**: Reasonable ranges based on similar projects in the industry
- **Team dynamics**: What the described work implies about the user's role and autonomy

Document your inferences per entry. These are NOT gaps — they represent understanding that prevents asking basic questions.

Example: For an entry describing a data pipeline migration, domain inference would include: the choice of streaming vs batch architecture depends on latency requirements and data freshness SLAs; schema evolution handling is standard practice in any migration; the migration strategy (big-bang vs incremental) was likely driven by downtime tolerance and rollback complexity. None of these need to be asked — they are understood by any practitioner in the field.

### Layer 2 — Gap Identification (only non-inferable gaps)

After domain inference, identify what ONLY the user can provide. A gap exists only when:

- Domain knowledge cannot fill it (specific incidents, not general patterns)
- Industry patterns cannot estimate it (exact metrics, actual timelines)
- It represents personal experience not captured in bullet points
- It is specifically important for the Phase 0 analysis perspective

For each entry, score gaps on:
- **Three-dimension completeness**: What / How / Result — present/absent/partial
- **Quantification quality**: Specific metrics vs vague qualifiers (e.g., "significantly improved", "greatly enhanced")
- **Agency clarity**: Personal contribution clear vs hidden behind "we"
- **Narrative depth**: Could this support a 3-minute interview story with follow-up questions

## Phase 2: Gap Prioritization

Classify gaps using the standard table, weighted by Phase 0 perspective:

| Priority | Criteria | Example |
|----------|----------|---------|
| **Critical** | Core projects missing what the target role most values | For architect target: no reasoning behind key architecture decisions |
| **High** | Key achievements with vague metrics | "Significantly improved" with no concrete numbers |
| **Medium** | Missing personal contribution in team projects | "we did X" without individual role clarity |
| **Low** | Nice-to-have depth on secondary projects | Older projects with thin but adequate detail |

Same gap may be Critical for one target direction and Medium for another. Always reference Phase 0.

## Phase 3: Present Analysis with Polished Options

Present to the user as a structured report with four parts:

### Part 1 — Domain Understanding (brief)

Show your Layer 1 inferences in condensed form so the user knows you understand the content. One sentence per entry, demonstrating domain comprehension.

Do NOT present this as questions. This is your understanding statement.

### Part 2 — Gap Table

Only genuinely non-inferable gaps:

| Priority | Entry | What's missing (why only the user can tell) |
|----------|-------|----------------------------------------------|

### Part 3 — Polished Supplement Options

For each entry with gaps, generate concrete supplement options. Each option MUST be a complete, polished statement — not a topic label. Use domain knowledge to fill in reasonable estimated values for uncertain parts.

Format per entry:

"For {entry}, based on my understanding, the following supplements would strengthen it:
a) {Complete polished statement with specific estimated values}
b) {Complete polished statement with specific estimated values}
c) {Complete polished statement with specific estimated values}
Which ones are close to the reality? You can pick multiple."

Examples of polished options (illustrating the format — adapt to the user's actual domain):

GOOD (backend/systems):
```
a) Led migration from monolith to microservices; chose event-driven architecture to decouple
   order processing from inventory management. Reduced deployment blast radius by isolating
   3 critical services, enabling independent releases ~2x per week vs. previous monthly cycle.
b) Designed circuit breaker pattern for third-party API integration; handled 500+ req/sec
   peak load with graceful degradation during provider outages, maintaining 99.5% SLA
   for end-user requests.
```

GOOD (data/ML):
```
a) Rebuilt feature pipeline from batch to streaming using Kafka + Flink; cut feature freshness
   from 24-hour lag to ~5 minutes, enabling same-day model retraining and improving
   prediction accuracy by an estimated 8-12% on time-sensitive features.
b) Implemented A/B testing framework supporting 20+ concurrent experiments; statistical
   significance reached in ~3-5 days vs. previous 2-week manual analysis cycle.
```

GOOD (frontend/mobile):
```
a) Introduced component design system with ~40 reusable components; reduced new feature
   UI development time by an estimated 30-40% and eliminated most cross-platform
   visual inconsistencies across web and mobile.
b) Optimized initial page load from ~4s to ~1.2s through code splitting, lazy loading,
   and image optimization; bounce rate decreased by ~15-20% on landing pages.
```

GOOD (management/product):
```
a) Restructured team from functional silos to cross-functional squads of 4-5; shipped
   3x more features per quarter by reducing cross-team handoff delays from ~2 weeks
   to same-day collaboration cycles.
b) Introduced quarterly OKR planning across 4 teams; aligned ~80% of engineering work
   to product strategy goals, up from an estimated 40-50% before formal goal-setting.
```

BAD (topic labels — user still has to figure out what to say):
```
a) Migration approach and reasoning
b) Performance optimization details
```

BAD (placeholder variables — user has to come up with numbers):
```
a) Migrated to microservices because XXX, reduced latency by X%
b) Improved load time from Xs to Ys
```

### Part 4 — User Selection

Ask: "Which entries and options should we focus on? Pick any combination."

Then proceed to Phase 4 for each selected option.

## Phase 4: Iterative Refinement (Clue-Based)

For each selected option, run the iterative refinement loop:

### Step 1: Evaluate user's selection

The user selected option(s). Determine:
- Does the user agree with the option as-is? → Go to Step 4 (confirm)
- Does the user provide corrections or additions? → Go to Step 2
- Does the user say "none of these are right"? → Go to Step 3

### Step 2: Refine based on new clues

User's correction or addition is a new clue. Use it to generate a refined statement with updated estimates.

"You mentioned {user's correction}. Based on that, here's the refined version:
{Revised complete polished statement incorporating the new information}
Is this more accurate?"

Loop until the user confirms. Maximum 3 refinement rounds per option — if not converging, write what you have and mark as partial.

### Step 3: Explore alternative direction

If none of the options were close, the gap is larger than expected. Generate 2-3 new options based on what you learned from the user's rejection.

"I see, my estimates were off. Let me try a different angle:
a) {New option based on what rejection implies}
b) {New option based on what rejection implies}"

Loop back to Step 1.

### Step 4: Confirm

When the user confirms a statement, it's ready for structuring.

### Interaction rules

- Each option exchange should be completable in 1-2 minutes
- Never ask more than one open-ended question per refinement round
- If the user starts sharing unprompted details, stop presenting options and listen — capture verbatim, then structure afterward
- Generate new options only when previous ones are clearly wrong — don't generate options for every minor detail

## Phase 5: Confirm and Write

Before writing, verify each entry's three-dimension coverage (what/how/result). If a core dimension is still missing after refinement, mark that supplement as `[partial]` in the entry and note what remains open — do not silently accept incomplete content.

Follow the same Confirm and Write process as Active Description (Phase 5).

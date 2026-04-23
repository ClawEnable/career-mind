# Post-Import Analysis

This mode runs when entries were imported during Init but haven't been assessed or deepened yet. The goal is to analyze entries from a domain-expert perspective, identify genuinely non-inferable gaps, and iteratively refine entries through option-based interaction.

## Phase 0: Determine Analysis Perspective

Read `context.md` and extract `target_direction`. This field drives the analysis lens — what counts as a critical gap depends on what role the user is targeting.

### Perspective Mapping

Use `target_direction` to determine emphasis:

| If target_direction suggests... | Analysis emphasis | What becomes Critical |
|---|---|---|
| Architecture / Tech Lead | Architecture decisions, system design trade-offs, tech selection reasoning | Missing "how/why" behind design decisions |
| Senior Engineer (IC) | Execution quality, delivery impact, problem-solving depth | Missing metrics and concrete results |
| Cross-platform / Fullstack | Breadth of capability, cross-domain learning velocity, delivery scope | Missing cross-domain scope and learning evidence |
| Management / Team Lead | Team building, process improvement, stakeholder management | Missing team dynamics and leadership evidence |
| none / unclear | Balanced analysis, no special weighting | Standard priority table (below) |

If `target_direction` contains multiple targets, use the most senior/targeted role as the primary lens, but note implications for other targets.

Document the chosen perspective — it shapes all subsequent phases.

## Phase 1: Two-Layer Analysis

Review all existing entries through the lens established in Phase 0. For each entry, perform two layers:

### Layer 1 — Domain Inference (understand first)

Using your domain expertise and the Phase 0 perspective, infer what you can already understand from the entry content:

- **Architecture patterns**: Why they make sense for the described scope and constraints
- **Technical decisions**: Which are standard practice vs. which represent genuine innovation
- **Scale and complexity**: What can be inferred from described scope (user count, team size, business impact)
- **Trade-offs**: What a practitioner at the target level would recognize as the implicit reasoning
- **Likely metrics**: Reasonable ranges based on similar projects in the industry
- **Team dynamics**: What the described work implies about the user's role and autonomy

Document your inferences per entry. These are NOT gaps — they represent understanding that prevents asking basic questions.

Example: For a Flutter three-layer architecture entry, domain inference would include: the Plugin layer exists because iOS IAP (StoreKit + receipt verification) and Android payment channels have fundamentally different flows; the NativeBridge handles platform-specific capabilities Flutter cannot access directly; Bloc + component templates is the standard state management pattern for this architecture. None of these need to be asked — they are understood.

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

Present to the user as a structured report with three parts:

### Part 1 — Domain Understanding (brief)

Show your Layer 1 inferences in condensed form so the user knows you understand the technical content. One sentence per entry, demonstrating domain comprehension.

Example: "Flutter cross-platform migration: standard three-layer architecture (UI/Plugin/NativeBridge) for cross-platform separation; PayloadCMS content delivery pipeline enables self-service marketing config without app releases; standout value is using AI tools to deliver full-stack work in an unfamiliar tech stack."

Do NOT present this as questions. This is your understanding statement.

### Part 2 — Gap Table

Only genuinely non-inferable gaps:

Priority | Entry | What's missing (why only the user can tell)

### Part 3 — Polished Supplement Options

For each entry with gaps, generate concrete supplement options. Each option MUST be a complete, polished statement — not a topic label. Use domain knowledge to fill in reasonable estimated values for uncertain parts.

Format per entry:

"For {entry}, based on my understanding, the following supplements would strengthen it:
a) {Complete polished statement with specific estimated values}
b) {Complete polished statement with specific estimated values}
c) {Complete polished statement with specific estimated values}
Which ones are close to the reality? You can pick multiple."

Examples of polished options (for a Flutter cross-platform project, architect target):

GOOD:
```
a) Evaluated React Native and native dual-platform approaches; chose Flutter for cross-platform
   UI consistency and hot reload. Team had no Flutter experience but completed technical
   validation in 2-3 weeks with AI-assisted development.
b) Payment plugin layer unified iOS IAP (StoreKit sandbox verification + Apple review compliance)
   and Android multi-payment channels, handling 5+ edge cases including callback timeout,
   network interruption, and duplicate payments.
c) Gray release covered ~30-50% of users; triggered 1-2 rollbacks due to payment callback
   timeout during gray phase, resolved by optimizing callback timeout thresholds,
   reaching 99%+ production stability.
d) Cursor/Claude Code handled ~60-70% of coding work; PayloadCMS full-stack integration
   completed in 3-4 weeks, saving an estimated 40-50% time vs traditional approach.
```

BAD (topic labels — user still has to figure out what to say):
```
a) Tech selection decision process
b) Payment chain details
c) Gray release data
d) AI-assisted development efficiency
```

BAD (placeholder variables — user has to come up with numbers):
```
a) Chose Flutter because XXX, team completed validation in X weeks
b) Gray release covered X% users, triggered N rollbacks
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

Follow the same Confirm and Write process as Active Description (Phase 5).

# Questioning Triggers

Patterns to watch for during active description capture. When you notice these signals, follow up naturally.

## Vague Impact Signals

When user says: "improved", "optimized", "enhanced", "made better"

→ Follow up: "Can you be more specific about the improvement? Any numbers or before/after comparison?"

## Missing Approach Signals

When user describes a result but not how they achieved it: "We reduced load time by 50%"

→ Follow up: "How did you approach that? What was your specific contribution?"

## Decision Points

When user mentions choosing between options: "We considered X but went with Y"

→ Follow up: "What was the reasoning behind choosing Y? What trade-offs did you weigh?"

## Team Dynamics

When user says "we", "our team", "the group"

→ Follow up: "What was your personal role in that? What did you specifically drive?"

## Challenges

When user skips over difficulties: "And then we launched successfully"

→ Follow up: "Were there any obstacles along the way? What was the hardest part?"

## Pivot Points

When user mentions changing direction: "At first we tried X, then switched to Y"

→ Follow up: "What triggered that switch? What did you learn from the first attempt?"

## Scope Indicators

When user mentions scale: "millions of users", "large codebase", "cross-team"

→ Follow up: "How large was the team? How many users were affected? What was the scope of the codebase?"

## Option Generation Signals

For post-import analysis and any mode where existing information provides a basis for inference, use these triggers to generate polished options instead of asking questions:

### Vague Metric Signal

When an entry contains vague qualifiers ("significant improvement", "greatly enhanced", "substantially optimized"):

→ Generate options with concrete, reasonable estimated values based on the entry's domain:
"Based on similar projects in this domain, the improvement is likely:
a) {Concrete statement with specific estimated range relevant to the technology/task}
b) {Concrete statement with specific estimated range relevant to the technology/task}
c) {Concrete statement with specific estimated range relevant to the technology/task}
Which is closest?"

### Missing Approach Signal

When an entry describes results but the "how" dimension is thin, and the target role values technical reasoning:

→ Generate options that are complete technical statements, not questions:
"The implementation approach was likely:
a) {Complete statement describing a plausible approach for the described task, with specific technique/pattern and reasoning}
b) {Complete statement describing an alternative plausible approach}
c) {Complete statement describing another alternative approach}
Which describes it best?"

### Missing Contribution Signal

When an entry uses "we" or passive voice, and agency clarity is a gap:

→ Generate options based on what the described work implies about the role:
"From the entry content, your role was likely:
a) {Role description with specific scope of ownership and collaboration}
b) {Alternative role description with different scope}
c) {Another alternative role description}
Which is closest?"

### Missing Scale Signal

When an entry mentions a project or feature without scale context:

→ Generate options with reasonable scale estimates based on the project's domain and scope:
"Based on the project scope, the scale was likely:
a) {Concrete scale estimates with specific numbers appropriate to the domain}
b) {Alternative scale estimates}
c) {Another alternative scale estimates}
Which range is closest?"

### Iterative Refinement Trigger

When the user selects an option or provides a correction:

→ Treat the selection as a new clue. Refine the statement incorporating the new information and present the updated version for confirmation. Generate at most 2 alternative refinements per round.

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

→ Generate options with concrete, reasonable estimated values:
"Based on similar projects, the improvement is likely:
a) ~20-30% performance gain, primarily from reducing load time from Xs to Ys
b) Accuracy improved from ~70-80% to 90%+, mainly by introducing XX mechanism
c) Development efficiency improved ~40-50%, reducing turnaround from X days to Y days
Which is closest?"

### Missing Approach Signal

When an entry describes results but the "how" dimension is thin, and the target role (from post-import analysis Phase 0) values technical reasoning:

→ Generate options that are complete technical statements, not questions:
"The implementation approach was likely:
a) Designed around XX pattern; core challenge was YY, solved via ZZ approach
b) Adopted XX over alternative AA primarily due to clear advantage in BB dimension
c) Migrated from legacy XX to YY architecture; main refactoring involved ZZ
Which describes it best?"

### Missing Contribution Signal

When an entry uses "we" or passive voice, and agency clarity is a gap:

→ Generate options based on what the described work implies about the role:
"From the entry content, your role was likely:
a) Tech lead: led design, guided 2-3 people on implementation, coded core modules personally
b) Core developer: owned XX module end-to-end from design to delivery, collaborated with YY team
c) Primary contributor: designed the XX approach and implemented the core parts; YY parts handled by colleague
Which is closest?"

### Missing Scale Signal

When an entry mentions a project or feature without scale context:

→ Generate options with reasonable scale estimates:
"Based on the project scope, the scale was likely:
a) ~X daily active users, team of 3-5, project duration 2-3 months
b) Served X business partners, integrated into Y products, SDK size kept under Z MB
c) Covered ~X% of target users, monitored Y core metrics during gray release
Which range is closest?"

### Iterative Refinement Trigger

When the user selects an option or provides a correction:

→ Treat the selection as a new clue. Refine the statement incorporating the new information and present the updated version for confirmation. Generate at most 2 alternative refinements per round.

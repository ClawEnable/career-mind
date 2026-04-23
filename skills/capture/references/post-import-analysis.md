# Post-Import Analysis

This mode runs when entries were imported during Init but haven't been assessed or deepened yet. The goal is to analyze what you have from an expert perspective, identify strategic gaps, and create a prioritized plan before asking any questions.

## Phase 1: Expert Analysis

Review all existing entries from a **senior engineer / HR / hiring manager** perspective. For each entry, evaluate:

- **Three-dimension completeness**: What (specific actions), How (methods/decisions/reasoning), Result (outcomes/impact/data). Score each dimension as present/absent/partial.
- **Quantification quality**: Are metrics specific and credible, or vague ("显著提升", "大幅增强")?
- **Agency clarity**: Is the user's personal contribution clear, or hidden behind "we"?
- **Narrative depth**: Could this entry support a 3-minute interview story with follow-up questions?

## Phase 2: Gap Prioritization

Classify gaps into priority levels:

| Priority | Criteria | Example |
|----------|----------|---------|
| **Critical** | Core projects missing "how" or "why" decisions | Architecture choices with no reasoning |
| **High** | Vague metrics on key achievements | "显著提升" with no numbers |
| **Medium** | Missing personal contribution in team projects | "we did X" without individual role |
| **Low** | Nice-to-have depth on secondary projects | Older projects with thin but adequate detail |

## Phase 3: Present Plan

Present the analysis to the user as a structured gap report:

1. **Summary of current state**: What's strong, what's missing
2. **Gap table**: Priority | Issue | Affected entry | What's missing
3. **Proposed focus**: "I recommend we start with {highest-priority gap}. This matters because {reason from interview/HR perspective}."

Ask user to confirm or adjust priorities: "Should we start with these, or do you want to focus on something else?"

## Phase 4: Targeted Questioning

Based on confirmed priorities, ask specific, targeted questions about the gaps. Reference specific entries and specific missing dimensions.

**Good**: "你的 Flutter 三层架构里，Plugin 层把 iOS IAP 和 Android 支付封装成统一接口。是因为两端支付流程的什么差异让你觉得必须抽象这层？直接在 Flutter 侧处理会出什么问题？"

**Bad**: "讲讲你最难的技术决策是什么？"

Each question should:
- Reference a specific entry or bullet point
- State what dimension is missing (without naming the framework)
- Be answerable in 2-3 minutes of conversation

After each answer, check: did it fill the gap? If yes → proceed to structuring. If not → one natural follow-up, then move on.

## Phase 5: Confirm and Write

Follow the same Confirm and Write process as Active Description (Phase 5).

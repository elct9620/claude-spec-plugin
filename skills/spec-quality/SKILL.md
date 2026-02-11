---
name: spec-quality
description: Assess specification quality using 11-item rubric, balance check, and common problems table. Use when reviewing specs before implementation or verifying quality gates.
---

# Specification Quality

Criteria and tools for evaluating specification quality.

## Applicability Rubric

| Condition | Pass | Fail |
|-----------|------|------|
| Spec review requested | Need to assess spec quality | No review needed |
| Pre-implementation check | Spec about to be implemented | Already implemented |
| Quality gate | Spec must meet minimum bar before proceeding | Quality already verified |
| Improvement cycle | Iterating on spec after feedback | No prior version to compare against |

**Apply when**: Any condition passes

## Core Principles

### Specification Rubric

Rate each item Y (yes) or N (no).

**Intent Layer**
| # | Criterion | Required | Y/N |
|---|-----------|----------|-----|
| 1 | Purpose stated in one sentence? | ✓ | |
| 2 | Target users identified? | ✓ | |
| 3 | Impacts (behavior changes) identified? | | |
| 4 | Success criteria measurable or verifiable? | | |

**Design Layer**
| # | Criterion | Required | Y/N |
|---|-----------|----------|-----|
| 5 | Each documented feature has defined behavior? | ✓ | |
| 6 | Error scenarios cover all documented features? | ✓ | |
| 7 | Interaction points (internal and external) have explicit contracts? | | |
| 8 | Implementer can build without clarifying questions? | ✓ | |

**Consistency Layer**
| # | Criterion | Required | Y/N |
|---|-----------|----------|-----|
| 9 | Key terms defined and used consistently throughout? | | |
| 10 | Recurring situations have named patterns? | | |
| 11 | Two implementers would produce compatible results? | | |

**Passing Criteria:**
- Any Required N → Must address before implementation.
- All Required Y → Specification meets **Minimal** level. Usable for small teams.
- All Required Y + #3,4 Y → Specification meets **Usable** level. Stop unless improving quality.
- All items Y → Specification meets **Complete** level. Stop.
- Non-required N → Address only if relevant to project scope.

### Quality Level Classification

| Level | Criteria | Suitable For |
|-------|----------|-------------|
| Minimal | All Required items Y (#1,2,5,6,8) | Small team, rapid iteration |
| Usable | All Required Y + #3,4 Y | Standard development |
| Complete | All 11 items Y | Multi-team, external consumers |
| Over-specified | All Y but Balance Check fails | Needs trimming of implementation details |

### Balance Check (for review verification; see spec-principles Specify vs Leave Open for writing decisions)

| Question | Design Decision (specify) | Implementation Detail (open) |
|----------|---------------------------|------------------------------|
| User-visible? | Error messages, CLI output | Log format, variable names |
| Affects module contracts? | Interface signatures | Internal functions |
| Could cause inconsistent interpretation? | Error handling pattern, Business rules | Algorithm choice, Performance optimization |

**Test:** "If implemented differently, would users notice or would modules conflict?"

**Warning signs of over-specification:** internal implementation details, algorithm choices (unless user-visible or cross-implementer consistency required)

**Warning signs of under-specification:** vague terms ("appropriate", "reasonable"), undefined behavior for reachable states

### Common Problems (diagnosis; see spec-principles Anti-Patterns for prevention)

| Problem | Symptom | Cause | Fix |
|---------|---------|-------|-----|
| Missing intent | Technical tasks instead of user value | No purpose/users defined | Add intent layer |
| Undefined scenarios | Inconsistent edge case behavior | Incomplete state coverage | Enumerate all combinations |
| Over-specification | Implementer constrained unnecessarily | Implementation details included | Keep only observable behaviors |
| Inconsistent patterns | Similar problems solved differently | No shared conventions | Extract and reference patterns |
| Inconsistent terminology | Same concept has multiple names | No shared vocabulary | Define key terms, use consistently |
| Vague language | Ambiguous interpretation | "Handle appropriately" | Use specific values or criteria |
| Hidden assumptions | Works only in specific context | Unstated prerequisites | Make all assumptions explicit |
| Explanatory notes | "Note: because..." appears | Mixing rationale with spec | Rewrite as direct statement |
| Phase markers | "(Future)", "(v2)" in spec | Mixing planning with spec | Remove; spec describes target state |

## Completion Rubric

### Before Quality Assessment

| Criterion | Pass | Fail |
|-----------|------|------|
| Full spec read | Entire specification read and understood | Partial or skimmed reading |
| Project context known | Understand team size, project stage, consumers | No context about project |
| Target quality level selected | Chose Minimal/Usable/Complete based on context | No target level determined |

### During Quality Assessment

| Criterion | Pass | Fail |
|-----------|------|------|
| All 11 items evaluated | Every rubric item scored Y or N | Items skipped or unclear |
| Evidence for each N | Each N has specific evidence from spec | N without justification |
| Balance Check completed | Over/under-specification assessed | Balance not checked |
| Common Problems scanned | All 9 problem types checked | Problems check incomplete |

### After Quality Assessment

| Criterion | Pass | Fail |
|-----------|------|------|
| Prioritized findings | Required N items listed before non-required | Unprioritized list |
| Actionable recommendations | Each finding has a specific fix suggestion | Vague improvement advice |
| Clear verdict | Quality level determined (Minimal/Usable/Complete/Over-specified) | No clear assessment |

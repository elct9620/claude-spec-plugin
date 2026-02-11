---
name: spec-quality
description: Quality assessment criteria for specifications—11-item rubric, balance check for over/under-specification, and common problems with fixes.
---

# Specification Quality

Criteria and tools for evaluating specification quality.

## Specification Rubric

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
- All Required Y → Specification is usable. Stop unless improving quality.
- All items Y → Specification is complete. Stop.
- Any Required N → Must address before implementation.
- Non-required N → Address only if relevant to project scope.

## Balance Check

| Question | Design Decision (specify) | Implementation Detail (open) |
|----------|---------------------------|------------------------------|
| User-visible? | Error messages, CLI output | Log format, variable names |
| Affects modules? | Interface signatures | Internal functions |
| Needs consistency? | Error handling pattern | Algorithm choice |
| Could misalign? | Business rules | Performance optimization |

**Test:** "If implemented differently, would users notice or would modules conflict?"

**Warning signs of over-specification:** internal implementation details, algorithm choices (unless user-visible)

**Warning signs of under-specification:** vague terms ("appropriate", "reasonable"), undefined behavior for reachable states

## Common Problems

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

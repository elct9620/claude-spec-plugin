---
name: spec-methodology
description: Methods for writing, reviewing, and maintaining specifications—progressive approach, review assessment, content splitting, and uncertainty handling.
---

# Specification Methodology

Operational methods for creating, reviewing, and maintaining specifications.

## Progressive Approach

Apply to both writing new specifications and improving existing ones. When improving, identify current phase and proceed from there.

| Phase | Focus | Output | Confirm |
|-------|-------|--------|---------|
| 1. Intent | Why and for whom | Purpose, Users, Impacts | Rubric #1-2 Y |
| 2. Scope | What's included | Feature list, User journeys (Context → Action → Outcome) | List complete |
| 3. Behavior | How it works | Feature behaviors, Error scenarios | Rubric #5-6, #8 Y |
| 4. Refinement | Quality | Patterns, Contracts, Terminology | Rubric #7, #9-11 as needed |

**Rules:**
- Do not write Phase 3 details until Phase 2 is confirmed
- Phase 2 defines user-facing flows; Phase 3 defines internal behaviors
- Return to earlier phases when new understanding emerges
- Specification is usable after Phase 3 (all Required Y)

## When Reviewing

Assess against three layers:

1. **Intent**: Can I explain why this system exists and for whom?
2. **Design**: Can I predict behavior for any user action?
3. **Consistency**: Will similar situations be handled similarly?

Key questions:
- Is this complete enough to implement without guessing?
- Are all design decisions explicit?
- Will two implementers produce compatible results?

Flag: missing layers, vague language, implementation details that should be open, design decisions that should be specified.

## Splitting Content

**Default: Keep everything in SPEC.md.**

Use this decision table to determine when to extract content:

| Decides | Expands | External | → Action |
|---------|---------|----------|----------|
| Y | - | - | Keep in SPEC.md |
| N | N | - | Keep in SPEC.md |
| N | Y | N | May extract (summary + link) |
| N | Y | Y | Extract (link only) |

**Conditions:**
- **Decides**: Cannot understand what to build without reading this
- **Expands**: Complete definition of a decision (all fields, all cases)
- **External**: Maintained by different role/tool

**Examples:**

| Content | Decides | Expands | External | → Action |
|---------|---------|---------|----------|----------|
| Feature behavior | Y | - | - | Keep |
| Decision table | Y | - | - | Keep |
| Error handling rules | Y | - | - | Keep |
| API endpoints (3-5) | N | N | - | Keep |
| Full DB schema (50+ fields) | N | Y | N | May extract |
| Complete test cases | N | Y | N | May extract |
| Figma design | N | Y | Y | Extract |

**When extracting:**
- SPEC.md keeps the decision/summary
- Link: `See [Schema](docs/schema.md) for field definitions`
- Detail documents follow same principles

| Type | Location |
|------|----------|
| Data structures | `docs/schema.md` |
| Visual design | `docs/design.md` or external |
| Test cases | `docs/tests.md` |

**When updating specifications:**
- First determine: decision or detail?
- Decisions go in SPEC.md, details may go in referenced documents
- If adding to external document, verify SPEC.md has the governing decision

**Writing tip:** Use tables (like this decision table) to define boundaries and rules. Tables make conditions explicit and reduce ambiguity.

## Handling Uncertainty

### Undecided design choices

Do not leave gaps. Instead:

1. Present options with tradeoffs
2. Request a decision
3. Document the choice

### Incomplete information

Mark explicitly what is decided vs pending:

```
## Technical Stack

Decided:
- Runtime: Node.js >= 20

To be decided:
- Database: PostgreSQL or SQLite
  (depends on deployment target)
```

### Conflicting requirements

Surface the conflict explicitly and request resolution rather than making assumptions.

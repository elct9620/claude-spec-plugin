---
name: spec-methodology
description: Write and improve specifications using progressive approach (Intent, Scope, Behavior, Refinement). Use when creating new specs, improving existing ones, or handling uncertainty and content splitting.
---

# Specification Methodology

Operational methods for creating, reviewing, and maintaining specifications.

## Applicability Rubric

| Condition | Pass | Fail |
|-----------|------|------|
| Writing new spec | Creating spec from scratch | Spec already written |
| Improving existing spec | Gaps identified in current spec | Spec passes all quality checks |
| Reviewing spec | Assessing spec for implementation readiness | No review needed |
| Splitting content | Spec growing beyond manageable size | Spec is concise and focused |

**Apply when**: Any condition passes

## Core Principles

### Progressive Approach

Apply to both writing new specifications and improving existing ones. When improving, identify current phase and proceed from there.

| Phase | Focus | Output | Confirm |
|-------|-------|--------|---------|
| 1. Intent | Why and for whom | Purpose, Users, Impacts | Purpose + Users stated |
| 2. Scope | What's included | Feature list, User journeys (Context → Action → Outcome) | List complete |
| 3. Behavior | How it works | Feature behaviors, Error scenarios | Behaviors + Errors defined, implementable |
| 4. Refinement | Quality | Patterns, Contracts, Terminology | Contracts, Terms, Patterns as needed |

**Rules:**
- Do not write Phase 3 details until Phase 2 is confirmed
- Phase 2 defines user-facing flows; Phase 3 defines feature behaviors and error scenarios
- Return to earlier phases when new understanding emerges
- Specification reaches Minimal quality level after Phase 3 (all Required Y)

### Phase Transition Guide

| Transition | Advance When | Stay/Return When |
|-----------|-------------|-----------------|
| Intent → Scope | Purpose and Users stated; stakeholders agree on both | Purpose unclear; users not validated |
| Scope → Behavior | Feature list confirmed; user journeys cover all impacts | New features discovered; flows incomplete |
| Behavior → Refinement | Behaviors and Errors defined, implementable; all features covered | Undefined scenarios found; implementer has questions |
| Refinement → Done | Target quality level met; Balance Check passes | Consistency gaps; terminology conflicts |

### When Reviewing

Assess against three layers:

1. **Intent**: Can I explain why this system exists and for whom?
2. **Design**: Can I predict behavior for any user action?
3. **Consistency**: Will similar situations be handled similarly?

Key questions:
- Is this complete enough to implement without guessing?
- Are all design decisions explicit?
- Will two implementers produce compatible results?

Flag: missing layers, vague language, implementation details that should be open, design decisions that should be specified.

### Splitting Content

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

### Handling Uncertainty

#### Undecided design choices

Do not leave gaps. Instead:

1. Present options with tradeoffs
2. Request a decision
3. Document the choice

#### Incomplete information

Mark explicitly what is decided vs pending:

```
## Technical Stack

Decided:
- Runtime: Node.js >= 20

To be decided:
- Database: PostgreSQL or SQLite
  (depends on deployment target)
```

Resolve all "To be decided" items within the target scope before implementation readiness—an implementer should be able to build without clarifying questions. Items outside the current scope may remain deferred with explicit owners.

#### Conflicting requirements

Surface the conflict explicitly and request resolution rather than making assumptions.

## Completion Rubric

### Before Applying Methodology

| Criterion | Pass | Fail |
|-----------|------|------|
| Starting phase identified | Know which phase to begin from | Phase not determined |
| Existing content assessed | Evaluated current spec against rubric | No assessment of current state |
| Target quality level known | Minimal/Usable/Complete selected | No target level |

### During Application

| Criterion | Pass | Fail |
|-----------|------|------|
| Phase discipline | Completing current phase before advancing | Skipping phases |
| Gate confirmation | Phase transition criteria checked | Advancing without verification |
| Uncertainty surfaced | Undecided items explicitly marked | Gaps left silently |
| Content placement correct | Decisions in SPEC.md, details in referenced docs | Content misplaced |

### After Application

| Criterion | Pass | Fail |
|-----------|------|------|
| All phases completed | Reached target phase with gates passed | Phases incomplete |
| Quality rubric passed | Target quality level criteria met | Quality level not reached |
| Pending items resolved or deferred | "To be decided" items within target scope resolved; out-of-scope items explicitly deferred | Undecided items within scope remain |

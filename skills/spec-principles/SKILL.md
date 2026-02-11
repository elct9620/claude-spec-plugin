---
name: spec-principles
description: Core principles for software specifications—what a spec IS and IS NOT, the constrain-design-open-implementation principle, anti-patterns, and three-layer framework overview.
---

# Specification Principles

Foundational knowledge for working with software specifications.

## What Makes a Good Specification

A specification describes the **target state**—what the system looks like when complete.

| Specification IS | Specification is NOT |
|-----------------|---------------------|
| Target state description | Implementation plan |
| Design decisions (what) | Decision rationale (why) |
| Declarative statements | Narrative explanations |

**Core principle: Constrain design, open implementation.**

- Specify all user-visible decisions
- Leave internal implementation choices to implementers
- If an implementer must guess a design decision, the specification is incomplete

**Anti-patterns:**
- `Note:` — If clarification needed, specification is unclear. Rewrite directly.
- `(Future)`, `(v2)` — Describes target state, not phases. Remove or split into separate spec.
- `(Optional)` — Either required for target state or belongs in Non-goals.

## Three-Layer Overview

Complete specifications address three layers:

| Layer | Purpose | Key Question |
|-------|---------|--------------|
| Intent | Why this exists | What problem for whom? |
| Design | What to build | What boundaries, interfaces, behaviors? |
| Consistency | How to stay unified | What patterns for similar problems? |

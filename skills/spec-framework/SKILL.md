---
name: spec-framework
description: Three-layer framework for structuring specifications—Intent, Design, and Consistency layers with detailed elements, boundary types, and implementation standards.
---

# Specification Framework

Detailed structure for each layer of a specification.

## Intent Layer

Provides context for judgment calls:

| Element | Role | Core |
|---------|------|------|
| Purpose | What problem the system solves | ✓ |
| Users | Who uses it, what they accomplish | ✓ |
| Impacts | What behavior changes indicate success (drives priority) | |
| Success criteria | What defines "done" and "working" | |
| Non-goals | What is explicitly out of scope | |

Without intent, implementers make technically correct but misaligned decisions.

## Design Layer

Defines observable behaviors and boundaries:

| Element | Role | Format | Core |
|---------|------|--------|------|
| System boundary | What's inside vs outside | See Boundary types | |
| User journeys | Task flows achieving impacts | Context → Action → Outcome | |
| Interfaces | Contracts between internal modules | - | |
| Presenter | How system presents to users | UI: colors, layout / CLI: output format / API: response structure | |
| Behaviors | Outcomes for each state × operation | State + Operation → Result | ✓ |
| Error scenarios | How failures are handled | - | ✓ |

**Boundary types:**

| Type | Defines | Example |
|------|---------|---------|
| Responsibility | What system does / does not do | "Validates input; does not store history" |
| Interaction | Input assumptions / Output guarantees | "Assumes authenticated user; Returns JSON only" |
| Control | What system controls / depends on | "Controls order state; Depends on payment service" |

## Consistency Layer

Establishes patterns for uniform implementation (all items enhance quality, none required for minimal spec):

| Concept | Role | Example |
|---------|------|---------|
| Context | Shared understanding | "This is event-driven" |
| Terminology | Same concept uses same name throughout | "Order" not "Purchase/Transaction/Request" |
| Pattern | Recurring situation → approach | "State changes via events" |
| Form | Expected structure | "Events have type, payload", "Primary: #FF0000", "Errors to stderr" |
| Contract | Interaction agreement | "Handlers must be idempotent" |

Weave these into relevant sections rather than listing separately.

## Implementation Standards (Optional)

For projects requiring code-level consistency across multiple contributors or extended development periods.

| Category | Purpose | Examples |
|----------|---------|----------|
| Architecture | Module boundaries and dependencies | Clean Architecture, Hexagonal, Layered |
| Design Patterns | Reusable solutions | Repository, Factory, Strategy |
| Testing Style | Test structure and conventions | Given-When-Then, Arrange-Act-Assert |
| Code Organization | Directory structure and naming | Feature-based, layer-based, naming conventions |

**When to include:**
- Multiple contributors work on the codebase
- Development spans extended periods
- Codebase requires shared conventions

**When to skip:**
- Simple scripts or single-file utilities
- Prototypes or proof-of-concept
- Short-lived projects

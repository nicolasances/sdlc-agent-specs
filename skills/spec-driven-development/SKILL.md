---
name: spec-driven-development
description: Creates specs before coding. Use when before starting the implementation of a task described in a GitHub issue.
---

# Spec-Driven Development

## Overview

Starting from a detailed task described in a GitHub issue, create a technical specification that defines what we're building, why, and how we'll know it's done. 
The spec is the shared source of truth between you and the human engineer — it defines what we're building, why, and how we'll know it's done. Code without a spec is guessing.

## When to Use

- When assigning a GitHub issue to be implemented, before any coding work has started.

**When NOT to use:** Single-line fixes, typo corrections.

## The Gated Workflow

Spec-driven development has three phases. Do not advance to the next phase until the current one is validated.

```
SPECIFY ──→ PLAN ──→  IMPLEMENT
   │          │           │
   ▼          ▼           ▼
 Human      Human       Human
 reviews    reviews    reviews
```

### Phase 1: Specify

Start with the task documented in the GitHub issue. 
Understand the current state of the codebase and how the new feature fits in. 
Ask the human clarifying questions until requirements are concrete.

**Surface assumptions immediately.** Before writing any spec content, list what you're assuming:

```
ASSUMPTIONS I'M MAKING:
1. This is a web application (not native mobile)
2. Authentication uses session-based cookies (not JWT)
3. The database is PostgreSQL (based on existing Prisma schema)
4. We're targeting modern browsers only (no IE11)
→ Correct me now or I'll proceed with these.
```

Don't silently fill in ambiguous requirements. The spec's entire purpose is to surface misunderstandings *before* code gets written — assumptions are the most dangerous form of misunderstanding.

**Write or update specs for each affected repo**. Specs should be written in markdown and saved in the `docs/specs` directory of the affected repo(s). Specs should be specific to a feature. 
Format for the spec: 

```markdown
# Spec: [Name of the feature]
## Objective
[What are we building and why? Who is the user? What does success look like?]

## Core Logic
[How are we implementing]
- Key changes
- Key algorithms
- Changes to data models
- Architectural decisions

[This is the "meat" of the spec. Any critical decision **must** be documented here, with the rationale behind it.]

## Out of Scope
[What are we explicitly NOT building? This prevents scope creep and keeps the implementation focused.]
```

Make sure the specs are validated by the user before proceeding. The human should read the spec and say "yes, this is what I want" or provide feedback for changes. Do not proceed to planning until the spec is approved.

### Phase 2: Plan

With the validated spec, generate a technical implementation plan:

1. Identify the major components and their dependencies
2. Determine the implementation order (what must be built first)
3. Note risks and mitigation strategies
4. Identify what can be built in parallel vs. what must be sequential
5. Define verification checkpoints between phases

The plan should be reviewable: the human should be able to read it and say "yes, that's the right approach" or "no, change X."

### Phase 3: Implement

Execute tasks one at a time following `incremental-implementation` and `test-driven-development` skills. 

## Keeping the Spec Alive

The spec is a living document, not a one-time artifact:

- **Update when decisions change** — If you discover the data model needs to change, update the spec first, then implement.
- **Update when scope changes** — Features added or cut should be reflected in the spec.
- **Commit the spec** — The spec belongs in version control alongside the code.
- **Reference the spec in PRs** — Link back to the spec section that each PR implements.

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "This is simple, I don't need a spec" | Simple tasks don't need *long* specs, but they still need acceptance criteria. A two-line spec is fine. |
| "I'll write the spec after I code it" | That's documentation, not specification. The spec's value is in forcing clarity *before* code. |
| "The spec will slow us down" | A 15-minute spec prevents hours of rework. Waterfall in 15 minutes beats debugging in 15 hours. |
| "Requirements will change anyway" | That's why the spec is a living document. An outdated spec is still better than no spec. |
| "The user knows what they want" | Even clear requests have implicit assumptions. The spec surfaces those assumptions. |

## Red Flags

- Starting to write code without any written requirements
- Asking "should I just start building?" before clarifying what "done" means
- Implementing features not mentioned in any spec or task list
- Making architectural decisions without documenting them
- Skipping the spec because "it's obvious what to build"

## Verification

Before proceeding to implementation, confirm:

- [ ] The spec covers all six core areas
- [ ] The human has reviewed and approved the spec
- [ ] Success criteria are specific and testable
- [ ] Boundaries (Always/Ask First/Never) are defined
- [ ] The spec is saved to a file in the repository
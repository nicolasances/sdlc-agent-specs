---
name: create-features
description: Moves from a well-described concept or idea into a series of concrete features to be implemented in a codebase. 
---

# Create Features

## Overview

Starting from a refined idea clearly documented in a markdown file, break down the idea into well-defined features ready to be implemented in a specific codebase (microservice, app, etc.).

This skill is used to take a well-described, refined idea (that might span across multiple components and services in an architecture) and **for a specific component of the architecture** break the idea down into **self-contained, independently deployable and testable** features for this component (whether it's a microservice, an app, or any other type of software-based component of the architecture).

This skill can also be used to update an existing feature markdown file pre-implementation. 

## When to Use

- To breakdown an idea or concept that is clearly defined in a markdown file into a series of features that needs to be implemented in a specific codebase (microservice or app or other components of an architecture)
- To **update** the feature set after the idea changed (requirements added, removed, or revised).
- To **add** features when an update describes new functionality for the app.
- To **update** a single feature described in a markdown file.

**Trigger Phrases:**
- "Help me break this down the idea described in [path] into a series of features for this microservice"
- "Help me break this down the idea described in [path] into a series of features for this app"
- "I need to break down an idea into features for this service"
- "The idea changed — update the features"
- "Here's a new feature for the app — add it / fold it into the features"
- "I need you to update feature [path]"
- "Update this feature description [path] .."

**When NOT to use:** 
- Ideation or refinement of an idea
- Implementation of changes in code
- Feature implementation

--- 

## Prerequisites

- [ ] **Always** start from an idea or concept that is described in a markdown file. If you don't have that, ask the user. **You cannot proceed** without that.
- [ ] **Ask the user to confirm the codebase**: the user must confirm that you will be generating features for the codebase you're working on.  
- [ ] Read the codebase. 
- [ ] Classify the codebase: is it a frontend app or a backend microservice? 
- [ ] If the codebase is a frontend app, you **MUST** read the `slicing-frontend.md` file and follow the guidelines in that file to break down the idea into features.
- [ ] If the codebase is a backend microservice, you **MUST** read the `slicing-microservice.md` file and follow the guidelines in that file to break down the idea into features.

---

## Operating Modes

This skill is **incremental and reconciliation-aware**. It is rarely run on a blank slate. **Before producing anything, read what already exists in `docs/features` (including `00-user-journeys.md` for a frontend) and treat it as the current state to evolve — never blindly regenerate or overwrite the whole set.** Then determine which mode you are in:

1. **Full breakdown (greenfield)** — no features exist yet. Produce the complete set per the slicing strategy.

2. **The idea changed** — the idea (or other source doc) was updated. Compute the **delta** between the new idea and the existing features:
   - **Update** the features whose scope changed (edit in place; preserve their still-valid open questions and technical decisions).
   - **Add** features for genuinely new scope.
   - **Remove / flag** features whose scope was dropped from the idea (don't silently delete — call it out to the user).
   - **Leave untouched** the features unaffected by the change.
   - Update the user-journeys / screen inventory to match the new idea.

3. **A new feature/capability was described** — an update introduces new functionality. Decide per the slicing strategy whether it **extends an existing capability** (update that feature) or is a **new capability** (create a new feature file), and update the user-journeys / screen inventory accordingly. Do not duplicate scope already owned by an existing feature.

In every mode, finish with the slicing strategy's **coverage check** so the feature set still spans the whole (current) idea.

### Recording the change (change record)

A feature file always describes the **target end-state**, never a change. So when you **update or add** features for an already-existing feature set (modes 2 and 3), the feature files alone don't tell a future implementer *what changed* or *why* — and the implementation needs that delta. Capture it in a **change record**.

**Produce a change record for modes 2 and 3 (not for greenfield).** Keep the feature files clean (end-state); the change record carries the delta, the rationale, and the impact. It is the artifact the implementer (the `engineer` agent) uses to scope the work to the delta — together with the feature files' own git diff.

- **Where:** `docs/features/changes/<YYYY-MM-DD>-<short-slug>.md` (create the `changes/` folder if missing).
- **Altitude:** stay code-agnostic. Describe impact at the level of **screens and components named in the feature files** — not code symbols, files, or functions (the implementer maps those to code during planning).

**Template:**
The feature file must be named: `F<number>-<short-slug>.md` (e.g. `F01-login.md`), and the change record must be named: `<YYYY-MM-DD>-<short-slug>.md` (e.g. `2024-06-01-add-login-screen.md`).

```markdown
# Change: <short title>   (<YYYY-MM-DD>)

## What changed
[One bullet per affected feature: <Feature> — <what changed in its requirements>.]

## Why
[The rationale / trigger for this change.]

## Impact (add / modify / remove)
[Per affected feature, the screens/components added, modified, or removed.
'remove' matters most — it is exactly what a from-scratch build silently misses.]

## Behavior to verify
[The new or changed behavior as testable statements — the contract the
implementation must satisfy.]

## Affected feature files
[The feature .md files this change touched, so the implementer reads the updated
specs and their git diff.]
```

### Handling a partial or missing wireframe (frontend)

The wireframe / design is the **source of truth for the screens it covers**, but it may not cover the whole idea. **Never silently invent screens that the wireframe does not describe.**

- For idea scope that **is** covered by the wireframe → produce/update features normally.
- For idea scope that has **no wireframe coverage**:
  - **Default: skip it.** Do not produce features for uncovered screens. At the end, explicitly **list what you skipped** and why ("no wireframe/design guidance for X").
  - If the user wants it covered anyway, **ask** whether you should design those screens yourself (from the idea alone, without wireframe guidance) or wait for the wireframe. Only invent screens after explicit confirmation, and clearly **mark** such features as designed-without-wireframe (e.g. a note + an open question to validate the design).
- If there is **no wireframe at all**, ask the user up front: design the screens from the idea alone, or wait for a wireframe? Do not assume.

---

## Guidelines on feature breakdown

Depending on the codebase you're working on, follow the corresponding slicing strategy to break down the idea into features: 
- For a frontend app, follow the guidelines for slicing described in the [`slicing-frontend.md`](./slicing-frontend.md) file.
- For a backend microservice, follow the guidelines for slicing described in the [`slicing-microservice.md`](./slicing-microservice.md) file.

**Important:** you **MUST** follow the corresponding slicing strategy for the codebase you're working on. Do not mix strategies, and do not deviate from the guidelines in the strategy.

### Get the altitude right

The single most common failure is slicing at the **wrong altitude** — and then covering only part of the experience.

- **Frontend:** a Feature is a **Capability** — a coherent, independently-valuable slice of user functionality that owns **one or more screens**, delivered end-to-end (UI, components, presentation logic, business logic, API integration). Usually one screen; sometimes a tight flow of screens that form one job (e.g. a checkout flow); sometimes a cross-cutting shared component used by 3+ screens. A **component** of a screen (a card, a chart, a row, a banner, a "shell") is **never** its own feature — it is described inside the feature that owns its screen. Screens are the *coverage scaffold*, not the unit. See `slicing-frontend.md` for the full rules.
- **Always cover the whole idea.** The set of features must span every screen / journey in the idea (and the wireframe/design, if one exists), not just the first screen. Before finishing, run the coverage check from the slicing strategy: every screen is owned by exactly one feature, and every user journey can be traversed end-to-end across the features.

### Output format 

Each feature is broken down into a set of `code-agnostic` requirements .
Each feature needs to be described in a markdown file (.md) with the format described in the slicing strategy file corresponding to this type of codebase (e.g. frontend, microservice, etc.).

### Where to store the features

Features need to be stored as markdown files in this codebase's `docs/features` folder. 
If it does not exist, create it.

## Red Flags

- Starting anything without a clear, refined idea documented in a markdown file
- Writing any code
- Adding code snippets into the feature description
- You have not followed the slicing strategy corresponding to this codebase (e.g. you are writing features for a microservice but you are not following the slicing strategy for microservices).
- **(Frontend) A feature describes a sub-region of a single screen** — a card, a chart, a row, a banner, a "shell". That is a component, not a feature; fold it into the feature for its screen. (Too small.)
- **(Frontend) A feature bundles unrelated screens** the user reaches as separate, deliberate destinations. Split it at the seam. (Too big.)
- **(Frontend) The features cover only one screen of a multi-screen experience.** The breakdown must span every screen / journey in the idea.
- You skipped mapping the user journeys / screen inventory, so you cannot prove the features cover the whole idea.
- You regenerated the whole feature set from scratch when features already existed, instead of computing the delta and updating in place.
- **(Frontend) You invented screens the wireframe does not cover** without skipping them or asking the user first.

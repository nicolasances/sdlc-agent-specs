# Slicing Strategy for Frontend

## Pre-requisites

Before creating features for a frontend, you **must**: 
- [ ] Verify that you have a good understanding of the architecture of the app. For that, you **must** have read an architecture description. Often you will find it in the `docs` folder. If you cannot find it, you **must** ask the user.
- [ ] Map the backend microservices. You **must** know which backend microservices are supporting this app. These are usually described in the architecture description.

## Guiding Principle

**For a frontend, a Feature is a Capability — a coherent, independently-valuable slice of user functionality, delivered end-to-end.**

A capability owns **one or more screens** and everything that makes them work: the screen UI, the React components inside it, the presentation logic, the business/client logic, and the API integration. A user can do the whole job the capability exists for — nothing about it is left to another feature.

A capability is **usually** one screen, but not always:
- One screen that does one job → one capability (e.g. a dashboard, a settings screen, a search-results screen).
- A tight flow of screens that together deliver one uninterrupted job → **one** capability (e.g. a checkout flow: cart → address → payment → confirmation; or an onboarding wizard).
- A cross-cutting component reused across many screens → its own capability (e.g. a media player, a rich-text editor, a date picker used throughout the app).

**Screens are not the unit of slicing — they are the scaffold.** You enumerate every screen to *bound* capabilities and to *prove coverage*, but the feature is the capability, not the screen.

## Core Vocabulary (read this before slicing)

These words are not interchangeable. Most bad breakdowns come from confusing them — usually by mistaking a **component** for a feature, or a **screen** for a capability.

| Term | What it is | Is it a Feature? |
|------|------------|------------------|
| **Capability** | A coherent slice of user value, owning 1..n screens, delivered end-to-end. | **Yes — the capability is the Feature.** |
| **Feature** | One capability, written up in one feature file. It *contains* screens and components. | — |
| **Screen** | A page/route the user navigates to. Belongs to exactly one capability. Used to bound capabilities and prove coverage. | No — a screen is *part of* a capability. |
| **Component** | A React element inside a screen (a card, chart, rail, banner, button row). | **No.** Described *inside* the feature whose screen contains it. |

**Two rules that prevent the common failures:**

1. **A Component is never a Feature.** A card, a chart, a row, a banner, a "shell" is part of the screen it lives in. The one exception: a **cross-cutting shared component used by three or more screens** (e.g. a media player or a date picker used throughout the app) becomes its own capability/feature so its contract is defined once; the screens that use it reference it. A component used by only one or two screens stays inside its owning feature.

2. **Don't split a coherent flow into one-feature-per-screen, and don't bundle unrelated screens.** Group screens into a capability when they form one uninterrupted job; keep them separate when each does an independent job. (Floor and ceiling — see Altitude self-check.)

## Methodology

Follow these steps in order. Do not jump straight to writing feature files.

### Step 1 — Map the User Journeys

From the idea (and the wireframe/design, if one exists), list the **journeys**: the end-to-end paths a user takes to accomplish a goal (e.g. "Sign up and set up an account", "Find a product and buy it"). For each journey, write the ordered sequence of **screens** it passes through.

Write these to **`docs/features/00-user-journeys.md`** (see Output Format). This file is the backbone of the breakdown and the basis for the coverage check.

### Step 2 — Build the Screen Inventory (the scaffold)

From the journeys, the design, and the idea, enumerate the **complete set of screens** for this codebase — every page the user can land on. If the design documentation already lists pages or a navigation map (e.g. a `ui-design.md`, or a wireframe with named screens), that inventory is the **source of truth** — reconcile against it, mofify it if needed to accomodate changes in the requirements (idea) or new ideas, do not invent a different decomposition.

The inventory must be **complete**: every screen reachable in any journey appears in it. This is the main guard against the most common failure — covering only the first screen of a multi-screen experience.

**When the wireframe only partially covers the idea:** the wireframe is the source of truth for the screens it defines. Do **not** silently invent screens for idea scope the wireframe does not cover — by default skip those parts and list them, or ask the user whether to design them without wireframe guidance. See *Handling a partial or missing wireframe* in `SKILL.md`.

### Step 3 — Group screens into Capabilities → one Feature each

Group the screens into capabilities along **lines of user value and flow**:

- A screen that does an **independent job** is its own capability.
- Screens that form **one uninterrupted job** (the user moves through them without it being a separate decision/destination) are **one** capability. Example: a checkout flow that moves the user cart → address → payment → confirmation is *one* feature, even though the design lists those as separate pages.
- Use the journeys to find the natural seams: a seam where the user pauses, chooses a different destination, or could reasonably stop, is a capability boundary.

Each capability becomes **one Feature file**, owning its screen(s) end-to-end. Inside it, list each screen and the **components** that make up that screen. Components are parts of the feature — never spun out into their own files.

> Granularity note: features here are **capability-sized, not implementation-sized**. A feature is later broken into tasks by the downstream breakdown step, which handles implementation chunking. So prefer a coherent capability over many tiny per-screen features.

### Step 4 — Pull out cross-cutting shared components

If a component is used by **three or more** screens, give it its own Feature so its behaviour and contract are defined once; every screen that uses it references it. Do this only for genuinely cross-cutting components; one- or two-screen components stay inside their owning feature.

### Step 4 - Map integrations

The frontend relies on backend microservices that expose REST APIs to fetch data, send data and execute business logic. 

You will: 
- [ ] read which API endpoints they provide. Look at the microservice documentation (stored under the `docs` folder of that microservice) and map which endpoints are provided and their meaning. Microservices are stored on github. Their repo is usually described in the architecture documentation. 
- [ ] For each screen or UI component that requires data or backend functionalities, you **must**: 
    - find which endpoint, among those available in the backend microservice(s), is to be used by the component
    - if you cannot find one, mark this as a **critical open point** to be fixed before implementation


### Step 5 — Coverage check (mandatory before finishing)

Verify, explicitly:
- **Every screen** in the inventory (Step 2) is owned by **exactly one** Feature.
- **Every journey** in `00-user-journeys.md` can be traversed end-to-end across the Features — no journey passes through a screen that no feature owns.
- **No Feature is a sub-region of a screen** (a header, a card, a chart, a "shell"). If one is, it is a component — fold it into its screen's feature.
- **No Feature bundles unrelated screens** just because they are adjacent in the nav. If two screens are independent jobs with a clear seam between them, split them.

If a journey cannot be completed with the features you produced, the breakdown is incomplete — add the missing capability.

## Altitude self-check

Check granularity against these before accepting the breakdown.

**Right altitude (capability-level, end-to-end):**
- A *dashboard* screen — the whole hub; its summary cards, charts and action rows are **components inside this one feature**, together with the data load that feeds them.
- A *list/search* screen — listing items with their status and navigation into a detail screen.
- A *checkout flow* — cart → address → payment → confirmation as **one** feature spanning several screens, because it is one uninterrupted job.
- A *media player* — a cross-cutting shared component used by several screens, as its own feature.

**Too small — component-level (do NOT do this):**
- ❌ A dashboard's individual widgets (a *stats card*, a *chart*, an *activity feed*, an *actions row*) as separate features. These are **components of the dashboard screen**; they belong inside the dashboard feature.
- ❌ A *page shell / layout* feature whose job is "lay out the other features". A screen and its parts are one feature; there is no separate shell.

**Too big — incoherent bundle (also avoid):**
- ❌ A single feature lumping the dashboard, the search screen, and the checkout flow together. These are distinct jobs with clear seams (the user stops at the dashboard, then chooses to search, then decides to check out). Split them.

Rule of thumb: if the feature's Purpose is "render one card / chart / row / zone", it is too small (a component). If it spans screens the user reaches as separate, deliberate destinations, it is too big (split at the seam). The sweet spot is **one coherent job the user sets out to do.**

## Output Format

### `00-user-journeys.md`

```markdown
# User Journeys

[Short intro: this file maps the journeys through the section, the complete
screen inventory, and the navigation map. It is the backbone for the feature
breakdown and the coverage check.]

## Journeys

| # | Journey | Goal | Screen sequence |
|---|---------|------|-----------------|
| J1 | [name] | [what the user achieves] | [Screen A] → [Screen B] → [Screen C] |

## Screen Inventory

[Every screen, mapped to the capability/feature that owns it. This table must be
complete — every screen any journey touches.]

| Screen | Route (if known) | Owning Feature (capability) | Notes |
|--------|------------------|-----------------------------|-------|

## Cross-cutting shared components

[Components used by 3+ screens that are their own feature, with the screens that use them.]

| Shared component | Used by screens | Owning Feature |
|------------------|-----------------|----------------|


```

### Feature file

Each Feature is documented in its own markdown file (.md) in `docs/features`, named `NN-capability-name.md`.

```markdown
# [Feature Name — the capability this feature delivers]

## 1. Purpose & Scope
[What capability this feature delivers and why. State the screen(s) it owns and
that it delivers them end-to-end. Name the journey(s) from 00-user-journeys.md
this capability participates in.]

**Out of scope**:
- [Thing deliberately excluded — typically other capabilities it navigates to]
- [Thing deliberately excluded]

## 2. Key User Stories
[From the end user's perspective. "As a [user], I want to [action] so that [goal]."]

| # | As a User I want to .. | so that .. |
|---|------------------------|------------|

## 3. Interfaces
[Describe the screen(s) this capability owns, their design reference
(wireframe/prototype), and how they fit the navigation. For each screen, list the
components it is composed of — these are parts of this feature, not separate
features. If the capability owns several screens, group the components by screen.]

**Screen(s):** [Name(s) of the screen(s) this capability owns, per the design docs]

**Components:**

| Screen | Component Name | Description | Expected Behavior |
|--------|----------------|-------------|-------------------|

[If a screen uses a cross-cutting shared component owned by another feature,
reference that feature here rather than re-describing the component.]

**Additional Notes:** [Edge cases, error/empty/loading states, transitions between this capability's screens, and interactions with other features.]

## 4. Business Logic
[Rules, flows, algorithms, invariants, and client-side logic for this capability.
One bullet per rule; specific enough to implement without guessing.]

## 5. Technical Decisions & Integrations
[Architectural decisions for this capability, especially deviations or forks.]

| # | Decision | Rationale |
|---|----------|-----------|


### 5.1. API Integrations

[Document all API integrations with backend microservices]
| Component or Screen | API Integration | Description | 
| ------------------- | --------------- | ----------- | 
| <name of component> | <HTTP Method> <endpoint> | [for what purpose is this API used by the component or screen? what is the data or functionality used for?] | 

**Missing**
[Document all missing endpoints that you could not find in the backend microservices]

| Component or Screen | Missing API endpoint |
| ------------------- | -------------------- |
| <name of component> | [Description of what endpoint might be missing and why it is necessary to implement the component]

## 6. Success Criteria
[Measurable criteria for "this capability is done and correct".]

| # | Criterion | Notes |
|---|-----------|-------|

## 7. Open Questions
[Unresolved questions affecting UX or implementation.]

| # | Question | Notes |
|---|----------|-------|
```

---

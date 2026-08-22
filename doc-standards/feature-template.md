# F<NN> — <Feature Name>

![Status](https://img.shields.io/badge/status-<open|implemented|deprecated>-<blue|brightgreen|red>?style=flat-square)

<!--
FILE NAMING: F<NN>-<kebab-case-feature-name>.md  (e.g. F21-level-test.md)
STATUS BADGE COLOURS: draft=lightgrey, in-progress=blue, implemented=brightgreen, deprecated=red
Note: escape hyphens in the badge label as double hyphens (in--progress).
-->

## 1. Purpose & Scope

<!--
MANDATORY
2–4 paragraphs. Answer, in order:
  - What is this feature, in one sentence a newcomer would understand?
  - How does it relate to its closest sibling features? Name them and state the
    differences explicitly ("it is a graded parallel of F10, differing only by …").
  - What are the headline numbers and rules? (counts, thresholds, timings)
Bold the load-bearing terms so the paragraph can be skimmed.
Cross-reference sibling features inline as [F<NN>](./F<NN>-<slug>.md).
-->

<Description of the feature.>

**Out of scope**:
- <Concern handled elsewhere> (→ [F<NN>](./F<NN>-<slug>.md))
- <Concern handled elsewhere> (→ [F<NN>](./F<NN>-<slug>.md))
- <Mechanic this feature *invokes* but does not own> (→ [F<NN>](./F<NN>-<slug>.md)); this feature invokes F<NN>'s <operation> operation

---

## 2. Core Concepts & Requirements

### 2.1. Core Concepts

<!--
OPTIONAL - only use this if there are new concepts that this feature introduces

Domain vocabulary only — the terms a reader must know before section 2.2 makes
sense. One row per term, definition in a single line. If a term needs a
paragraph, it probably belongs in 2.2.4 Business Logic instead.
-->

| Term | Definition |
|------|-----------|
| <Term> | <One-line definition> |
| <Term> | <One-line definition> |

### 2.2. Requirements

#### 2.2.1. Data Models

<!--
OPTIONAL - only use this if there is a new data model that this feature introduces
MUST NOT BE USED for front-end features

One block per entity this feature owns. State where it is stored. Omit this
section entirely if the feature introduces no new persisted entity.
-->

**<EntityName>** (stored in its own `<collectionName>` collection)

| Field | Type | Description | Rules |
|-------|------|-------------|-------|
| id | ObjectId | Unique <entity> id | Auto-generated |
| <field> | <type> | <What it holds> | <Required / default / invariant / when it changes> |
| <field> | <type> \| null | <What it holds> | <null until …> |

#### 2.2.2. Endpoints

<!--
OPTIONAL - only use this if this feature is a backend feature and requires the creation of a new API endpoint
MUST NOT BE USED for front-end features. Can only be used for backend features. 

One bullet per endpoint: METHOD path — what it does. Note request body shape,
notable status codes, and what is deliberately withheld from the response
(e.g. "returns questions without answers"). Keep to one or two lines each;
the detailed rules live in 2.2.4.
-->

- `<METHOD> </path/:param>` — <what it does>. <Notable status code or special behaviour.>
- `<METHOD> </path/:param>` — <what it does>; body `{ <field>, <field> }`.

#### 2.2.3. <Optional: Events / Jobs / UI States>

<!--
Optional subsection for anything that isn't an endpoint or a data model:
emitted events, scheduled jobs, client-side states, feature flags, permissions.
Delete if unused, or renumber the following section.
-->

#### 2.2.4. Business Logic 

<!--
The heart of the document. Describes the core business logic or business rules that this feature introduces. 
Includes any decision on the flow, logic, and any rules.
All core decisions are documented here.
-->


---

## 3. Key Consumer Stories

<!--
Written from the perspective of whoever consumes this feature. The consumer can be the final user of an app (if the feature is a front-end feature) or an app itself (if the feature is a backend one), etc.
One row per endpoint (only for backends) or per meaningful capability.
Each story should be traceable to something in 2.2.
-->

| # | As a Consumer, I want to… | So that… |
|---|--------------------------|----------|
| CS-01 | <capability> | <the value it delivers> |
| CS-02 | <capability> | <the value it delivers> |

---

## 4. Constraints and Assumptions

<!--
Constraint = a rule the implementation must honour; state the value and, where
relevant, why it differs from a sibling feature. If a constraint replaced an
earlier decision, note the version: "(v2.0 change — replaces …)".
Assumption = something taken as true that would invalidate this design if false.
-->

- **Constraint** — <rule, with its concrete value>.
- **Constraint** — <rule> (vs <different value> for <sibling feature>).
- **Constraint** — <rule> (v<X.Y> change — replaces <earlier behaviour>).
- **Assumption** — <what is taken as given, and which feature owns it>.

---

## 5. Open Questions

<!--
Questions are never deleted once answered — they are resolved in place, so the
reasoning behind a decision stays discoverable. Unresolved rows leave the
Resolution cell as "**Open**: <what is blocking / who decides>".
-->

| # | Question | Resolution |
|---|----------|-----------|
| OQ-01 | <question> | **Resolved**: <decision>. |
| OQ-02 | <question> | **Open**: <blocker or owner>. |

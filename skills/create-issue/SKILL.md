---
name: create-issue
description: Creates an Issue that will require a fix for a given codebase
model: opus
---

# Create Issue

Skill used when a user explicitly wants to create an issue on a codebase.

**Trigger Phrases:**
- "Create an issue for [problem]"
- "I have noticed [problem]. Create an issue for it. "

---

## The Workflow

You **must always strictly** follow this workflow when implementing a feature:

1. **Grill the user**: make sure you understand the problem the user is facing or the solution the user is proposing. Grill the user with questions to make sure you understand what the core issue is and what needs to be done. You **must** use the `grill-me` skill to do this.
2. **Understand which Feature this belongs to**. The issue must be related to one or more Features. Understand which ones it relates to and keep a trace of which files the features are documented in. All features are documented under `docs/features`. 
3. **Create a Github issue**. Create an issue in the repo linked to this codebase. 

**Template for the Github Issue:**
```typescript
# [Issue name]

## The Problem
[Description of the Problem]

**Impact:**
[Description of the impact of the problem. What happens if this is not fixed?]

## Suggested solution
[Description of the solution]

## Out of Scope
The following is left out of scope of this fix: 
- [Item 1]
- [Item 2]
- [Item 3]

## Related items
- [Feature X] - [Link to the feature and explanation on why this feature is impacted]
- [Feature Y] - [Link to the feature and explanation on why this feature is impacted]

```

**Rules for creating the Github Issue:**
- [ ] It **must** be in the repo connected to the codebase where the feature will be implemented. 
- [ ] It **must refer** to all the Feature .md files that are impacted by this issue. 
- [ ] It **must** be labeled with the label `fix`. If the label does not exist, you **MUST** create it.

--- 

## Acceptance Criteria

- [ ] You have created a GitHub issue on the repo linked to this codebase
- [ ] The Github issue fits the above template
---
name: prepare-feature-development
description: Prepares for the development of a feature in a codebase.
---

# Prepare Feature Development

This skill is a step of feature development. 
This skill performs all the necessary actions to prepare an agent for the development of a feature.

## Starting point

The starting point is **always** a Feature, described in a **markdown file**. 
If the user has not specified which feature to work on, ask for it. You **must** have the path to a markdown file that describes the feature.

**Checklist to begin:**
If this checklist is not **all** satisfied, as the user for the missing information. **Do not** start before all information is available: 
- [ ] You have a **feature** to work on. 
- [ ] The feature is **described in a markdown file** and you have access to that file. 
- [ ] You have read the feature described in the markdown file.
- [ ] You know which **codebase** (project, repo) you are working on. 

## The Workflow

You **must always strictly** follow this workflow when implementing a feature:

1. Read the codebase to understand current state
2. Read the feature description and **address all the open points**, if there are any, with the user. 
3. **Determine whether this is a new feature or a change to an already-implemented one.** Signals that it is a *change*: the feature file carries an "Implemented" badge, and/or a **change record** exists under `docs/features/changes/` referencing this feature, and/or the feature file has relevant history in `git log`.
    - **If it is a change**: read the **change record** and the **git diff** of the feature file(s) — together these are your delta. Scope your task list to that delta only (**add / modify / remove**), and do impact analysis on the codebase for exactly the changed requirements. **Do not re-implement the parts of the feature the change did not touch.**
    - **If it is a new feature**: break down the full feature.
4. Create a **GitHub issue** to implement this feature
5. Breakdown the feature (or the change delta) into a series of changes you will need to implement. **Prepare a task list**. 
6. Create a feature branch. 
7. Ask the user for confirmation of the task list before proceeding. 

## Rules

### When to engage the user

- [ ] Always engage the user to close the open points. Present lists of options. For each open point, the user **MUST** always either: 
  - choose an option
  - specify an alternative solution
  - decide to leave the open points unsolved and that a GitHub issue should be opened to track that 
- [ ] **Always ask the user** for any non-trivial architectural or technical decision that you need to make to create the task list. Do that only when there are multiple options that are substantially different from each other.
- [ ] Always **ask the user to confirm** the task list before considering the preparation step done.

### Rules for addressing Open Points

- [ ] Each Open Point must be addressed to the user. You must present to the user:
  1. **Different Options** to solve the open point 
  2. The possibility for the user to **provide an answer**
  3. The possibility to mark the Open Point as `linked to Github issue`. That means that the Open Point will be fixed later by a separate implementation, tracked by a new Github issue. *This could be used, for example, when building a UI and a backend API has not yet been implemented*.

- [ ] If the user chooses option 3, you **must** create a Github issue. 

### Rules for creating Github issues

**Rules for creating the GitHub issue for the feature implementation** (that is, the GH issue linked to the feature to develop): 
- [ ] It **must** be in the repo connected to the codebase where the feature will be implemented. 
- [ ] It must refer to the Feature .md file. 
- [ ] If this is a **change** to an already-implemented feature, it must also refer to the **change record** file.
- [ ] It **must** be labeled with the label `feature`.

**Rules for creating Github issues for the open points that cannot be resolved:**
- [ ] It **must** be in the repo connected to the codebase where the feature will be implemented. 
- [ ] It must refer to the Feature .md file. 
- [ ] It **must** refer to the specific open point that is left open
- [ ] It **must** be labeled with the label `fix`.

### Rules for breaking down the feature into tasks
For a frontend feature: 
- Building a UI Component should be considered a task. 
- Apply vertical slices when slicing a feature. 
    - **GOOD**: A task that covers UI component + presentation logic + API integration. 
    - **BAD (avoid)** Avoid horizontal slices (task1: all UI, task 2: all API integrations, etc.)

For a changed (already-implemented) feature:
- Scope tasks to the delta from the change record + the feature file's git diff: **add / modify / remove**.
- **Include removal tasks** for behavior the change drops — these are the ones most easily missed when working from an end-state spec.
- Do **not** create tasks that rebuild parts of the feature the change did not touch.

### Rules for creating the feature branch
- [ ] The feature branch must be named `feature/<feature-name>` where <feature-name> is a short name (dash-separated-words) of the feature.

## Acceptance Criteria 
You are done with preparing the Feature for development **ONLY IF:**
- [ ] The GitHub issue has been created
- [ ] The feature branch has been created
- [ ] All open points are either **closed** or marked as `linked to Github issue`. In the latter case, **there must exist a GitHub issue to close them later**. 
- [ ] You have broken down the feature into a series of tasks and **the user has confirmed it**. 

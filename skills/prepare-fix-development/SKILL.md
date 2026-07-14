---
name: prepare-fix-development
description: Prepares for the development of a feature in a codebase.
model: opus
---

# Prepare Fix Development

This skill performs all the necessary actions to prepare an agent for the development of a fix in a codebase.

---

## Starting point

The starting point is **always** a *Github issue* that describes a fix that needs to be made to a codebase.
If the user has not specified which Github issue to work on, ask for it. You **must** have the Github issue for this fix.

**Checklist to begin:**
If this checklist is not **all** satisfied, as the user for the missing information. **Do not** start before all information is available: 
- [ ] You have a Github issue to work on.
- [ ] The Github issue **clearly specifies** what fix needs to be done. That can be: 
    - Embedded in the Github issue
    - Referring to an Open Point in a feature file contained in the code base and available under `docs/features`
- [ ] You know which **codebase** (project, repo) you are working on. 

---

## The Workflow

You **must always strictly** follow this workflow when preparing the implementation of a feature:

1. Read the codebase to understand current state
2. Read any relevant feature description to understand the context of the fix. 
3. Breakdown the fix into a plan: a series of changes you will need to implement. **Prepare a task list**. You **MUST** use the `breakdown-feature`skill to breakdown a fix into tasks. Once you have the tasks, make the plan as a task list.
4. Create a feature branch, **if** the codebase is not already in a branch.
5. Ask the user for confirmation of the task list before proceeding. 

---

## Rules

***When to engage the user:**
- [ ] **Always ask the user** for any non-trivial architectural or technical decision that you need to make to create the task list. Do that only when there are multiple options that are substantially different from each other.
- [ ] Always **ask the user to confirm** the task list before considering the preparation step done.

**Rules for breaking down the fix into tasks:**
- Keep it simple: no need to have 100 tasks. 1-3 tasks for a fix should be more than enough.

**Rules for creating the feature branch:**
- [ ] Always pull the latest changes from the main branch before creating a feature branch. Without this step, you risk creating a feature branch that is not up to date with the main branch.
- [ ] Only create a feature branch if the codebase is not already in a branch. If the codebase is already in a branch, you can work in that branch and skip this step.
- [ ] The feature branch must be named `feature/<fix-name>` where <fix-name> is a short name (dash-separated-words) of the feature.

---

## Acceptance Criteria 
You are done with preparing the Fix for development **ONLY IF:**
- [ ] The feature branch has been created
- [ ] You have broken down the fix into a series of 1-3 tasks and **the user has confirmed it**. 

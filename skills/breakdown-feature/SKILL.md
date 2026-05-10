---
name: breakdown-feature
description: Creates structured tasks that will be then used by a coding agent. Use when starting a new project, feature, or significant change and no specification exists yet.
---

# Structure Tasks

## Overview

Starting from a refined idea clearly documented in a GitHub issue, break down the feature into a clear, structured list of subfeatures (tasks) that will be then used by a coding agent. Each task should be actionable, focused, and have explicit acceptance criteria.

## When to Use

- Starting a new project or feature that has already been ideated, has a clear direction and assumptions, and is documented in a GitHub issue.

**Trigger Phrases:**
- "Help me break this down feature [github issue link] into tasks"
- "Structure the work for [github issue link]"
- "Prepare the task list for [github issue link]"

**When NOT to use:** Single-line fixes, typo corrections, or changes where requirements are unambiguous and self-contained.

## The Gated Workflow

You always start from a **refined idea**. 
A refined idea **must** have been documented in a GitHub issue in the `nicolasances/toto` repository, tagged with the "idea" label, and assigned to the "Toto" project. The issue should contain a clear problem statement, proposed direction, key assumptions, and a "not doing" list.

Make sure to ask the user for the GitHub issue link if they haven't provided it. You will use the content of that issue as the starting point for your spec.
IMPORTANT: if you don't have the GitHub issue link, ask for it before proceeding. **Do not proceed without it**.

You will follow three phases. Do not advance to the next phase until the current one is validated.

```
UNDERSTAND ──→ BREAKDOWN ──→ GITHUB ISSUE
                   │     
                   ▼     
                 Human   
                reviews  
```

### Phase 1: Understand

Read the refined idea in the GitHub issue. 
Ask clarifying questions until you have a crystal-clear understanding of the problem, the proposed solution, and the assumptions. Your goal is to be able to restate the idea in your own words and identify any gaps or ambiguities.

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

### Phase 2: Breakdown

Break down the proposed idea into a clear, structured list of **independent** subfeatures (tasks) that will be then used by a coding agent. This includes:
- New components, modules, or services
- Changes to existing components (which ones and how)
- New API endpoints or changes to existing ones
- New databases, collections, schemas, files
- Changes to existing data models
- Changes to user flows or UI (if applicable)

Once you have a comprehensive list of changes, organize them into a coherent implementation plan. Identify dependencies (what needs to be built before what) and group related changes together.

**Sucess Criteria for this phase**: 
- Each task should target a single repo (project). Tasks should not span multiple repositories.
- Each task should be completable in a single focused session.
- Each task has explicit acceptance criteria.
- Each task includes a verification step (test, build, manual check).
- Each task should declare its dependencies to other tasks.
- Tasks are ordered by dependency, not by perceived importance.
- No task should require changing more than ~5 files.
- Each task (subfeature) **must** generate code that compiles (successfully builds) and can be deployed to production.

Once that is done **ask the user to review the plan and tasks**. 
**Do not proceed** to the next phase until you have an explicit confirmation from the user that the plan looks good. This is a critical checkpoint to ensure alignment before any code gets written.

### Phase 3: GitHub Issue

For each task, create a corresponding GitHub issue in the **right repo**. Each task corresponds only to a single repo, so the issue should be generated on that repo. Each task should be a separate issue. 
The issue title should be a concise summary of the task, and the body should include:
- A detailed description of the task
- The acceptance criteria
- What is out of scope or left out of this task (to prevent scope creep)
- Any relevant links (design mockups, related issues, documentation)

Each GitHub issue: 
- **must** be tagged with the "task" label.
- **must** be assigned to the "Toto" project.
- **must** be linked to the original idea issue (the one you started from). The original idea issue should be the **parent** issue, and the task issues should be linked as **child** issues.
- **must** be created in the repo that the task corresponds to.

## Red Flags

- Starting anything without a clear, refined idea documented in a GitHub issue
- Writing any code
- Changing anything in any repo 
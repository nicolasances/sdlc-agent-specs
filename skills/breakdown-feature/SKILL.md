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
ANALYZE > BREAKDOWN > Human Reviews > GITHUB ISSUE
```

### Phase 1: Analyze

In this phase you will: 

1. **Understand the idea.** You will: 
- Read and understand the idea documented in GitHub
- Analyze the code base, reading the relevant repos and files to understand the current state of the codebase and how the new feature fits in. 
- Identify gaps and ambiguities, unclear requirements, assumptions, and **ask clarifying questions** until you have a crystal-clear understanding of the problem, the proposed solution, and the assumptions. 

Always check-in with the user: 
- Whenever there are architectural decisions to be made
- Whenever there are multiple ways to implement the solution that are substantially different from each other
- Whenever you identify a new assumption
- Whenever you find ambiguous or unclear requirements

**Output**: Restate the idea in your own words, list the assumptions you're making and any choices that have been made.

Ask the user to confirm that your understanding is correct before proceeding to the next phase. This is a critical checkpoint to ensure alignment before any work gets done.

### Phase 2: Breakdown

Break down the proposed idea into a clear, structured list of **independent** subfeatures (tasks) that will be then used by a coding agent. 
Rules to follow when breaking down the feature into subfeatures (tasks): 
- **Single repo**. Each task should target a single repo (project). Tasks should not span multiple repositories.
- **Short**. Each task should be completable in a single focused session.
- **Explicit acceptance criteria**. Each task should have clear acceptance criteria that define what "done" looks like for that task.
- **Clear dependencies**. If a task depends on another task, that dependency should be explicitly stated. 

Each task should follow this template:

```markdown
# [Task Title]
[Short description of the task]. 
[Repo it belongs to].
[Link to the parent issue in the `nicolasances/toto` repo].

**Why**: [Brief explanation of why this task is necessary for the overall feature].

**What**: [Detailed description of what needs to be done in this task. Use checklists where possible, they are more readable].

## Implementation details
### Architectural decisions
- [Decision 1]
- [Decision 2]

### Technical Decisions and Design
- [Technical decision 1]
- [Technical decision 2]
- [Design choice 1]
- [Design choice 2]

## Acceptance Criteria
- [ ] [First acceptance criterion]
- [ ] [Second acceptance criterion]
- [ ] [Third acceptance criterion]

## Out of Scope
- [ ] [First out of scope item]
- [ ] [Second out of scope item]
```

Once you have a comprehensive list of changes, organize them into a coherent implementation plan. Identify dependencies (what needs to be built before what) and group related changes together.

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
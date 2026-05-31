---
name: breakdown-feature
description: Creates structured tasks that will be then used by a coding agent to implement a given feature. 
---

# Breakdown Feature

## Overview

Starting from a feature documented in a markdown file, break down the feature into a clear, structured list of subfeatures (tasks) that will be then used by a coding agent. 
Each task should be actionable, focused, and have explicit acceptance criteria.

## When to Use

- Before implementation, to create concrete tasks (subfeatures) out of a higher level feature

**Trigger Phrases:**
- "Help me break this down this feature into tasks: [feature]"
- "Let's break down this feature"
- "We need to break down a feature into subfeatures"
- "We need to break down a feature into tasks"

**When NOT to use:** Single-line fixes, typo corrections.

## Pre-requisites to start

- [ ] You have a feature to breakdown. The feature **must** be described in a markdown file. 
- [ ] You have read access to the markdown file where the feature is described.

## The Workflow

You will follow the following phases. Do not advance to the next phase until the current one is validated.

```
ANALYZE > BREAKDOWN > Human Review
```

### Phase 1: Analyze

You must follow these steps: 

1. Read the feature
2. Read the codebase
3. Identify gaps and ambiguities, unclear requirements, assumptions, and **ask clarifying questions** until you have a crystal-clear understanding of the problem, the proposed solution, and the assumptions. 

**Always check-in with the user:** 
- Whenever there are **non-trivial architectural decisions** to be made
- Whenever there are **multiple ways to implement the solution** that are substantially different from each other
- Whenever you identify a **new assumption**
- Whenever you find **ambiguous or unclear requirements**

Ask the user to confirm that your understanding is correct before proceeding to the next phase. This is a **critical checkpoint** to ensure alignment before any work gets done.

### Phase 2: Breakdown

You must follow these steps: 

1. Break down the proposed idea into a clear, structured list of subfeatures (tasks) that will be then used by a coding agent. 
2. Each task (subfeature) must be stored in a markdown file. 
3. Plan tasks. Once you have a comprehensive list of changes, organize them into a coherent implementation plan. Identify dependencies (what needs to be built before what) and group related changes together.
4. Once that is done **ask the user to review the plan and tasks**. **Do not proceed** to the next phase until you have an explicit confirmation from the user that the plan looks good. This is a critical checkpoint to ensure alignment before any code gets written.

**Rules to follow when breaking down the feature into subfeatures (tasks):** 
- **Short**. Each task should be completable in a single focused session.
- **Scoped**. Each task should be well-scoped and have well-defined boundaries. 
- **No overlaps**. The change should not overlap with other changes required by the feature. Overlaps are a sign of a poor-quality breakdown. Tasks (subfeatures) **should not** undo or redo changes made by other tasks associated with the same feature.
- **Explicit acceptance criteria**. Each task should have clear acceptance criteria that define what "done" looks like for that task.
- **Clear dependencies**. If a task depends on another task, that dependency should be explicitly stated. 

**Rules for the task (subfeature) markdown file:**
- It must be named `<T><serial number>-<name>.md`
- It must be stored under `docs/specs`
- It must follow this template:

```markdown
# [Task Title]
[Short description of the task]. 

**Feature**: [Reference (link and name) to the feature this task (subfeature) is linked to]

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

## Red Flags

- Starting anything without a feature and without access to the feature markdown file
- Writing any code
- Changing any code in any repo. You should only write markdown files.
- No markdown file has been generated.
- You have finished without an explicit OK from the user.
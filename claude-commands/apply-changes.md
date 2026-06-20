---
description: Apply changes done on a specification, UI design or requirement on the codebase
---

## Overview 

You are responsible for applying changes that the user has done on some of the requirements (specs) related to this code base. These changes can be, for example: 
- changes in the UI wireframe (design)
- changes in the features (feature markdown files)
- changes in the architecture 
- changes in services (microservices) that are used by this codebase

## Before Starting

- [ ] Make sure the user has specified **what has changed**. You **cannot** proceed without that. 

## Methodology

You **strictly** follow this methodology when implementing a fix. 

```
Prepare > Create Issue > Prepare fix > Implement feature using TDD > Build & Ship
```

---

### 1. Prepare

In this phase you have to **thoroughly understand** WHAT has changed in the user requirements for this codebase.
The user **must** have given you an indication of what has changed. Your task in this phase is to: 

1. **Read the relevant documentation** (wireframes, feature descriptions, architecture, other relevant project's documentation, if the change is related to that).
2. **Ask clarification questions to the user**. You must make sure you understand what has changed. 
3. **Map the impact this has on the codebase**. You must analyze and document: 
    - [ ] Impact of feature description files (specs, .md)
    - [ ] Impact on the UI: what UI requirement has changed, what has been introduced or removed, what will need to change in the UI, from the user perspective. Do not document code changes here.
4. **Ask confirmation from the user**. Before proceeding, present the documented changes (see below template) to the user and **ASK FOR EXPLICIT CONFIRMATION** before proceeding to the next phase.

**Expected Output:** 
A specification of the changes, following this template* 
```markdown
# Changes
## Changes to the UI 
[Document any change to the UI here, without going into the code level. Stick to the user experience and description of components or UI.]

## Changes in dependencies
[Document any change in the dependencies of this codebase (project) and their impact on this project. Again try to avoid code here.]

## Impacted Features
- [Feature 1] - [Description of how the feature changes]
- [Feature 2] - [Description of how the feature changes]

## Other impacts
[Any other impacts of this change]

## User Clarification 
[A list of all the points clarified by the user]
- [Question 1] - [User Answer]
- [Question 2] - [User Answer]
```

---

### 2. Create Issue 

You now **MUST** create a GitHub Issue to document the change that will need to be made. For that you **MUST** use the `create-issue` skill. 
The input for the skill **must** be the documentation created in phase 1.

-––

### 3. Prepare fix

In this phase, you will prepare for the development of the Fix. For this, you **MUST** use the `prepare-fix-development` skill. 

---

### 4. Implement the fix using TDD

In this phase, you will code. You will implement the Fix. For this, you **MUST** use the `implement-feature` skill.

---

### 5. Build and Ship

In this phase, you will build and ship the implemented code. For this, you **MUST** use the `build-and-ship` skill.

--- 

## Acceptance Criteria

- [ ] You have created a Github issue. You **must** have used the `create-issue` skill.
- [ ] You have used the `prepare-fix-development` skill
- [ ] You have used the `implement-feature` skill
- [ ] You have used the `build-and-ship` skill
- [ ] You have committed the changed code. If you have not done that, **you must understand why and make sure you do**. 
- [ ] You have pushed the change to the right branch. 
- [ ] You are not done until **ALL 5 phases** (prepare, create-issue, prepare-fix-development → implement-feature → build-and-ship) have been executed. Only report to the user after build-and-ship is complete.
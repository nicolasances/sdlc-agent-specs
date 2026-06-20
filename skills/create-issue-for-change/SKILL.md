---
name: create-issue-for-change
description: Creates an Issue for a change done on a specification, UI design or requirement on the codebase
model: opus
---

# Create Issue for Change

You are responsible for understanding changes that the user has done on some of the requirements (specs) related to this code base and creating a Github issue to prepare for the necessary updates. These changes can be, for example: 
- changes in the UI wireframe (design)
- changes in the features (feature markdown files)
- changes in the architecture 
- changes in services (microservices) that are used by this codebase

**Trigger Phrases:**
- "I have made some changes to the requirements."
- "I have updated the wireframe. [changes]. Create an issue for that."
- "I have updated [microservice or dependency]. Create an issue for that."
- "I have made changes to the design. I need you to create an issue for that."

## Before Starting

- [ ] Make sure the user has specified **what has changed**. You **cannot** proceed without that. 


## The Workflow

You **must always strictly** follow this workflow when implementing a feature:

```
Prepare > Create Issue 
```

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

### 2. Create Issue

Create a Github issue in the repo connected to this codebase. 

**Rules for creating the Github Issue:**
- [ ] It **must** be in the repo connected to the codebase where the feature will be implemented. 
- [ ] It **must refer** to all the Feature .md files that are impacted by this issue. 
- [ ] It **must** be labeled with the label `fix`. If the label does not exist, you **MUST** create it.

--- 

## Acceptance Criteria

- [ ] You have created a GitHub issue on the repo linked to this codebase
- [ ] The Github issue's content fits the above template
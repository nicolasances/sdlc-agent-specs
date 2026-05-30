---
name: create-features
description: Moves from a well-described concept or idea into a series of concrete features to be implemented in a codebase. 
---

# Create Features

## Overview

Starting from a refined idea clearly documented in a markdown file, break down the idea into well-defined features ready to be implemented in a specific codebase (microservice, app, etc.).

This skill is used to take a well-described, refined idea (that might span across multiple components and services in an architecture) and **for a specific component of the architecture** break the idea down into **self-contained, independently deployable and testable** features for this component (whether it's a microservice, an app, or any other type of software-based component of the architecture).

## When to Use

- To breakdown an idea or concept that is clearly defined in a markdown file into a series of features that needs to be implemented in a specific codebase (microservice or app or other components of an architecture)

**Trigger Phrases:**
- "Help me break this down the idea described in [path] into a series of features for this microservice"
- "Help me break this down the idea described in [path] into a series of features for this app"
- "I need to break down an idea into features for this service"

**When NOT to use:** 
- Ideation or refinement of an idea
- Implementation of changes in code

--- 

## Prerequisites

- [ ] **Always** start from an idea or concept that is described in a markdown file. If you don't have that, ask the user. **You cannot proceed** without that.
- [ ] **Ask the user to confirm the codebase**: the user must confirm that you will be generating features for the codebase you're working on.  
- [ ] Read the codebase. 

---

## Guidelines on feature breakdown

Remember: you are working on a single (software-based) component of an architecture. That's usually either a (backend) microservice or a frontend app (PWA or native app or web app).
You generate features **only** for that component, not for other components. 

### Definition of a good Feature

A good feature:
- [ ] is self-contained
- [ ] can be deployed independently from other services in the architecture. If it has dependencies from other services that should be changed, it can mock them and be deployed independently. 
- [ ] can be tested independently
- [ ] is as **small** as it can be. Keep features small in scope. Follow the **MVP pattern**. A good applications grows incrementally from building small features one at a time, not by building it all in one huge chunk (that would be the recipe for disaster). 
- [ ] does not contain code nor code snippets. It is **describing a desired behavior or state in business and technical terms** but without tying itself to code.

When you have a feature, ask yourself: "can it be broken down into smaller independent features?". If so, break it down.

### Output format 

Each feature is broken down into a set of `code-agnostic` requirements .
Each feature needs to be described in a markdown file (.md) with the following format: 

```markdown
# [Feature Name]

## 1. Purpose & Scope
[A description of the feature, why it's needed and what it does]

**Out of scope**: 
- [Thing deliberately excluded]
- [Thing deliberately excluded]

---

## 2. Core Concepts & Requirements

### 2.1. Core Concepts
A table of core concepts (glossary of concepts) that this idea relies on. The table has 
- a `term` column that states the name of the concept
- a `definition` column that explains the concept

### 2.2. Requirements

### Requirement: [name]
[Description of the requirement to be implemented]
- Interfaces
- Endpoints or changes to endpoints
- Data models or changes to data models
- Business Logic or changes to business logic

---

## 3. Key User Stories

| # | As a user, I want to… | So that… |
|---|---|---|
| US-01 | [action] | [goal] |
| US-02 | [action] | [goal] |

---

## 4. Constraints and Assumptions
- [Assumption 1] - [Description and implications]
- [Assumption 2] - [Description and implications]

- [Constraint 1] - [Description and implications]
- [Constraint 2] - [Description and implications]

---

## 5. Open Questions

| # | Question | Options / Notes |
|---|---|---|
| OQ-01 | [Question] | [Options or notes] |
| OQ-02 | [Question] | [Options or notes] |

```

## Red Flags

- Starting anything without a clear, refined idea documented in a markdown file
- Writing any code
- Adding code snippets into the feature description
- A feature that defines multiple endpoints: it can probably be broken down
- A feature that defines multiple data amodels: it can probably be broken down

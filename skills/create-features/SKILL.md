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

#### 2.2.1. Data Models
*(Omit this section if the feature introduces no new data model and modifies no existing one)*

For each data model, state the **collection name** and describe it as a table (4 columns: field name, field type, description, rules — if any).

#### 2.2.2. Endpoints
*(Microservices only — omit for frontend features)*

List each REST endpoint introduced or modified by this feature. Show the full **REST endpoint** (e.g. `GET /vocabularyItems`, `PUT /vocabularyItems/:id`) with a short description of its behavior, accepted inputs, and any rejection rules.

#### 2.2.3. Interfaces
*(Frontend only — omit for microservice features)*

Describe the screens, components, or interactions this feature introduces or modifies.

#### 2.2.4. Business Logic
*(Omit only if there is truly no logic beyond CRUD)*

Describe the rules, flows, algorithms, and invariants that govern this feature's behavior — things that live in the service layer, not in the schema or the route signature. Use one bullet per rule; be specific enough that a developer can implement it without guessing.

---

## 3. Key Consumer Stories

The **consumer** is whoever calls this component:
- For a **microservice**: another service, a frontend app, or an external script calling the API.
- For a **frontend app**: the end user interacting with the UI.

Frame stories from the consumer's perspective, naming the operation or capability they need, not the end-user product experience.

| # | As a Consumer, I want to… | So that… |
|---|---|---|
| CS-01 | [API operation or capability] | [what it enables] |
| CS-02 | [API operation or capability] | [what it enables] |

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

### Where to store the features

Features need to be stored as markdown files in this codebase's `docs/features` folder. 
If it does not exist, create it.

## Red Flags

- Starting anything without a clear, refined idea documented in a markdown file
- Writing any code
- Adding code snippets into the feature description
- Business logic buried inside a data model or endpoint description instead of in §2.2.4
- End-user product goals written as consumer stories for a microservice feature
- A feature that defines multiple endpoints: it can probably be broken down
- A feature that defines multiple data models: it can probably be broken down

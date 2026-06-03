---
name: create-features
description: Moves from a well-described concept or idea into a series of concrete features to be implemented in a codebase. 
---

# Create Features

## Overview

Starting from a refined idea clearly documented in a markdown file, break down the idea into well-defined features ready to be implemented in a specific codebase (microservice, app, etc.).

This skill is used to take a well-described, refined idea (that might span across multiple components and services in an architecture) and **for a specific component of the architecture** break the idea down into **self-contained, independently deployable and testable** features for this component (whether it's a microservice, an app, or any other type of software-based component of the architecture).

This skill can also be used to update an existing feature markdown file pre-implementation. 

## When to Use

- To breakdown an idea or concept that is clearly defined in a markdown file into a series of features that needs to be implemented in a specific codebase (microservice or app or other components of an architecture)
- To **update** features described in a markdown file.

**Trigger Phrases:**
- "Help me break this down the idea described in [path] into a series of features for this microservice"
- "Help me break this down the idea described in [path] into a series of features for this app"
- "I need to break down an idea into features for this service"
- "I need you to update feature [path]"
- "Update this feature description [path] .."

**When NOT to use:** 
- Ideation or refinement of an idea
- Implementation of changes in code
- Feature implementation

--- 

## Prerequisites

- [ ] **Always** start from an idea or concept that is described in a markdown file. If you don't have that, ask the user. **You cannot proceed** without that.
- [ ] **Ask the user to confirm the codebase**: the user must confirm that you will be generating features for the codebase you're working on.  
- [ ] Read the codebase. 
- [ ] Classify the codebase: is it a frontend app or a backend microservice? 
- [ ] If the codebase is a frontend app, you **MUST** read the `slicing-frontend.md` file and follow the guidelines in that file to break down the idea into features.
- [ ] If the codebase is a backend microservice, you **MUST** read the `slicing-microservice.md` file and follow the guidelines in that file to break down the idea into features.

---

## Guidelines on feature breakdown

Depending on the codebase you're working on, follow the corresponding slicing strategy to break down the idea into features: 
- For a frontend app, follow the guidelines for slicing described in the [`slicing-frontend.md`](./slicing-frontend.md) file.
- For a backend microservice, follow the guidelines for slicing described in the [`slicing-microservice.md`](./slicing-microservice.md) file.

**Important:** you **MUST** follow the corresponding slicing strategy for the codebase you're working on. Do not mix strategies, and do not deviate from the guidelines in the strategy.

### Output format 

Each feature is broken down into a set of `code-agnostic` requirements .
Each feature needs to be described in a markdown file (.md) with the format described in the slicing strategy file corresponding to this type of codebase (e.g. frontend, microservice, etc.).

### Where to store the features

Features need to be stored as markdown files in this codebase's `docs/features` folder. 
If it does not exist, create it.

## Red Flags

- Starting anything without a clear, refined idea documented in a markdown file
- Writing any code
- Adding code snippets into the feature description
- You have not followed the slicing strategy corresponding to this codebase (e.g. you are writing features for a microservice but you are not following the slicing strategy for microservices). 

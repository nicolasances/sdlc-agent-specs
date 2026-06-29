---
name: breakdown-feature
description: Breaks down a feature, a fix or an issue into a list of tasks that can be implemented and shipped independently
model: sonnet
---

# Breakdown Feature

With this skill, you can break down a feature, a fix or an issue into a list of tasks that can be implemented and shipped independently.

Breaking down a feature into tasks is a **critical step** in the development process. It allows you to create a clear and organized plan for implementing the feature, and ensures that each task can be completed and tested independently. This approach helps to reduce complexity, improve code quality, and make it easier to track progress.

## Methodology

- You **must** breakdown a feature using the **vertical slices strategy** rather than using horizontal slices. 
- Tasks cannot be just about a writing a **unit test**: unit tests are part of the implementation of a task, not a task on its own. 


Example of **BAD**, wrong slicing: 
- Task 1 — Add countCompletedByDay(userId, from, to, timezone) method to PracticeSessionStore — queries completed sessions (non-null completedAt) in the date window and returns a Map<YYYYMMDD, count>
- Task 2 — Add countPassedByDay(userId, from, to, timezone) method to ModuleTestAttemptStore — same but filters passed = true on takenAt
- Task 3 — Write tests for PracticeSessionStore.countCompletedByDay (in-memory mock)
- Task 4 — Write tests for ModuleTestAttemptStore.countPassedByDay (in-memory mock)

This breakes the vertical slice of the feature into horizontal slices, which is **bad** because it creates dependencies between tasks and makes it harder to test and deploy each task independently.

A **GOOD** example of vertical slicing would be:
- Task 1 — Add countCompletedByDay(userId, from, to, timezone) method to PracticeSessionStore — queries completed sessions (non-null completedAt) in the date window and returns a Map<YYYYMMDD, count>, **including tests**.
- Task 2 — Add countPassedByDay(userId, from, to, timezone) method to ModuleTestAttemptStore — same but filters passed = true on takenAt, **including tests**.

### For a frontend feature
- Building a UI Component should be considered a task. 
- Apply vertical slices when slicing a feature. 
    - **GOOD**: A task that covers UI component + presentation logic + API integration. 
    - **BAD (avoid)** Avoid horizontal slices (task1: all UI, task 2: all API integrations, etc.)

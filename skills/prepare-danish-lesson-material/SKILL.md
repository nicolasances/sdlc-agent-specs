---
name: prepare-danish-lesson-material
description: Takes my notes from a Danish lesson and prepares them into a structured format for review. Use after attending a Danish lesson and taking notes.
---

# Prepare Danish Lesson Material

## Overview

Starting from the notes taken during a Danish lesson, create a structured note of all words, sentences and rules learned. 

## When to Use

- When you have attended a Danish lesson and taken notes, and you want to prepare those notes into a structured format for review.

## The Workflow

1. Take the raw notes from the Danish lesson.
2. Extract non trivial words from the raw notes and list them in a table with their English translation and an example sentence in Danish.
3. Extract non trivial sentences from the raw notes and list them in a table with their English translation. 
4. Extract any rules or patterns that were taught in the lesson and list them in a separate section. Each rule should be clearly stated and, if possible, accompanied by an example.

## Rules

- If the translation of a word or a sentence is in the raw notes, use that translation. Otherwise, use your best guess based on the context of the lesson.
- If there is ambiguity, **ask the user**. It is better to ask the user to disambiguate than to make a wrong assumption.

## Output format

An .md file to be saved in the user's `danish-lessons` project (repo) with the following structure:

```markdown
# Danish Lesson Notes - [Date of the lesson]
## Words
| Danish Word | English Translation | Example Sentence (Danish) |
|---|---|---|
| | | |

## Sentences
| Danish Sentence | English Translation |
|---|---|
| | |

## Rules
- Rule 1: [Description of the rule]
  - [Example 1]
  - [Example 2]
- Rule 2: [Description of the rule]
  - [Example 1]
  - [Example 2]
```

## Red Flags

- There are no words or sentencesextracted from the raw notes.
- There are very simple words like "ikke", "og", "er" in the words table.
- There are conjunctions, prepositions, pronouns or other function words in the words table.

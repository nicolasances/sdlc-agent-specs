---
name: create-todos-from-notes
description: Migrate inline TODO markers from meeting notes into the master todo list. Use after one or more meetings to pull TODOs written in knowledge/meetings/ notes into master/todo.md, categorized, with source links, marking notes processed so nothing migrates twice.
---

Migrate inline `TODO` markers from meeting notes into the master todo list at `master/todo.md`.

Run from the notes vault root (the directory containing `master/` and `knowledge/`). All paths
below are relative to that root.

## Core rules

- **Preview before writing.** Always show the proposed entries and get approval before editing
  `master/todo.md` or stamping any note. Never write without approval.
- **Never modify TODO lines in the notes.** Dedup is file-level only: a processed note carries
  a footer tag `<!-- todo-processed: YYYY-MM-DD -->`. The original TODO text stays untouched.
- **Never invent facts.** Reword only using what the note actually says. If unsure, keep it
  closer to verbatim and flag it in the preview.
- **Never create categories unprompted.** Use the existing sections in `master/todo.md`.
  Unfit TODOs go to "Generic, not categorized". You may *suggest* a new sub-section in the
  preview, but only the user creates one.

## Procedure

### 1. Discover un-migrated TODOs
- Find candidate notes: all `*.md` under `knowledge/meetings/`.
- A line is an extractable TODO if it contains the **uppercase token `TODO`** (word boundary).
  This catches `*TODO: ...*`, `- *TODO: ...*`, and `TODO for me: ...`. The lowercase
  `master/todo.md` backlink must NOT match.
  - Example grep: `grep -rnE '\bTODO\b' knowledge/meetings --include='*.md'`
- **Skip any file that already contains** `<!-- todo-processed`. (A file may carry that tag even
  though its TODO lines are unchanged — that is expected.)
- For each match, capture the **full TODO phrase**, not just up to the first dash — e.g. the
  entire `*TODO: book him for an update — ... Lasse and Albert*` italic span. Keep a little
  surrounding context (the bullet it sits under, nearby headings) for categorization and rewording.

### 2. Build the duplicate set
- Read `master/todo.md`. Collect every source-note path that appears in `From [..](..)` links
  (and any `following [..](..)` style links).
- Mark any discovered TODO whose **source note path already appears** in those links as a
  *likely duplicate* (exact path match — do not fuzzy-match the text).

### 3. Categorize and reword each TODO
- Read `master/todo.md` to see the current categories and sub-sections (e.g. AI, Dev,
  Architecture, Specific initiatives → "AI Blurring", Generic, not categorized).
- Pick the best-fit existing category from the TODO plus its note context. If it doesn't
  clearly fit one, assign **"Generic, not categorized"**.
- Draft the entry as:

  `- [ ] <imperative action, **bold the key person/thing**>. From [<note title>](<relative path>)`

  - Light rewording into a self-contained action using note context; no invented facts.
  - **Note title** = the note's H1 heading text (trimmed). If there is no H1, use a sensible
    short name from the filename.
  - **Relative path** = path from `master/` to the note, i.e. prefix with `../`
    (e.g. `../knowledge/meetings/2026-06/2026.06.26/christoper-ml.md`).

### 4. Preview for approval
- Present the proposals grouped by target category, e.g.:

  ```
  [AI]   Check what **Sidsel** Katrine Smith's Data Management team does. From [Albert Demos](...)
  [AI]   Book **Line Nyberg, Sidsel, Ella McMaster** for a demo... From [AI Forum 2026.06.26](...)
  [Architecture]  Follow up on **Publicering Architecture** with **HJ**. From [...](...)

  likely duplicates (pre-deselected — already linked in todo.md):
    ( ) check Data Mgmt — albert-demos.md  *already linked*
  ```

- **Pre-deselect** likely duplicates from step 2.
- If several Generic items look like they share a theme, note it: "these N look like <theme> —
  want a new sub-section?" — but do not create one unless the user says so.
- Ask the user to approve, deselect, or edit category/wording.

### 5. Write approved entries
- For each approved entry, insert it at the **end of the open `- [ ]` items** within its target
  category, **above** any completed `- [X]` items in that section.
- Use Edit against `master/todo.md`. Preserve existing formatting and blank lines.

### 6. Stamp processed notes
- Get today's date: `date +%F`.
- Append `<!-- todo-processed: <today> -->` to **every note that had TODOs considered** in this
  run — including notes whose TODOs were confirmed as already-present duplicates (so they're
  skipped next time). Place it at the end of the file; if a backlinks comment exists, put the
  tag on its own line near it.
- Do **not** alter the TODO lines themselves.

### 7. Report
- Summarize: which entries were added and to which categories, which notes were stamped, and
  which candidates were skipped as duplicates.

## Re-processing a note later

A stamped note is skipped on future runs. If you add a **new** TODO to an already-stamped note,
delete its `<!-- todo-processed: ... -->` line before re-running so the note is re-scanned.
(Already-migrated TODOs in that note will be caught again as likely duplicates via their source
link and pre-deselected, so re-stamping is safe.)

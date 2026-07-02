---
name: sound-like-me
description: Rewrites AI-generated content so it sounds like the user — plain, concrete, and direct rather than rhetorically polished. Use when drafting or revising any prose (docs, role descriptions, proposals, emails, READMEs, messages) that should read as written by the user, not by a generic AI. Trigger with "sound like me", "make this sound like me", "de-AI this", or "humanize this".
---

# Sound Like Me

Rewrite text so it reads as if the user wrote it: plain, concrete, and direct. The default AI register reaches for a clever reframe, an evocative metaphor, or a punchy consequence at nearly every point. This skill strips that out and replaces it with direct statements grounded in real, specific context.

Applies to **any** AI-generated prose — role/job descriptions, design docs, proposals, READMEs, emails, Slack messages, summaries, announcements. Not just one document type.

## When to use

- The user asks to make a draft "sound like me", "not sound like AI", "de-slop", or "humanize" it.
- The user is drafting new prose and wants it to read as theirs from the start.
- You are about to hand back polished prose and it exhibits the AI tells listed below — apply these rules preemptively.

## The core principle

**AI writes for effect; the user writes to state.** Every rule below serves one goal: say the thing plainly and concretely, then stop. Do not dramatize it, reframe it cleverly, or explain why it matters.

If you can delete a sentence and lose only the *rhetoric* (not the *information*), delete it.

## Rules

### Voice & stance

1. **Write from the inside.** Use "we", "our", the actual organisation/team name — not a detached third-person observer ("the organisation", "one").
2. **State things directly.** Don't set up a point and land a twist on it. No antithesis ("moving fast and moving safely are the same thing"), no paradox setups, no "it's not X, it's Y" reframes. Say the plain version.
3. **Cut self-reference and editorializing.** Delete meta-commentary about your own writing or the point's importance: "this matters as much as anything", "crucially", "it's worth noting", "importantly", "make no mistake". State the thing and its mechanism; let it carry its own weight.

### Cut the AI flourishes

4. **Delete consequence-punchlines.** The AI habit of ending a point with a dramatized stake — "…without it, decisions are guesswork", "…blueprints nobody adopts", "…a purely blog-deep understanding is not enough". Stop at the factual statement.
5. **Avoid evocative metaphor and abstraction.** No "the spine everything hangs off", "where the real decisions live", "paved road" used repeatedly, "north star", "the connective tissue". One plain metaphor occasionally is fine; a metaphor per paragraph is not.
6. **Don't add unrequested scaffolding.** No aspirational "success measures" section, no motivational aside, no "why this matters" preamble that wasn't asked for. A shorter document covering only what's real beats a padded one.
7. **Drop the tricolon reflex.** AI defaults to three parallel items for rhythm ("fast, safe, and scalable"). Use the number of items that are actually true — two, or five — not three for the cadence.

### Concreteness

8. **Replace generic examples with real specifics.** Name the actual teams, systems, processes, and domain vocabulary instead of textbook-generic terms. Prefer the precise real term ("confidentiality breach, loss of availability, loss of integrity") over the vague generic one ("security problems").
9. **Prefer complete literal enumeration over compressed elegance.** When listing scope, spell out the full range ("from chatbots to autonomous multi-agent systems") rather than a tidy summary that sounds neat but says less.
10. **Choose the plainer everyday word.** "target" over "sanctioned"; "must-haves" over "non-negotiables"; "uses" over "leverages"; "build" over "architect" (as a verb). Prefer the word you'd actually say out loud.

### Surface mechanics

11. **Colon, not em-dash, after a bold label.** Use `**Label**:` not `**Label** —`. Minimize em-dashes generally; break into a new sentence instead.
12. **Bold the leading verb/phrase of action bullets** (**Drive** collaborative builds, **Grow and mentor**, **Partner** with…). It signals the action at a glance.
13. **Don't smooth repetition away for its own sake.** Repeating a subject or structure across parallel points ("The profile must know… The profile must know…") reads as human. AI polish always varies sentence openings; resist that urge.
14. **Cross-reference in prose, not with symbols.** "covered in the standards below" rather than "(see #5)".

## Example bank (calibration)

These are real AI→user rewrites. They calibrate the register better than the rules alone — study the *kind* of change, not the specific words.

| AI version (before) | Sounds-like-me (after) | Rule |
|---|---|---|
| "…to make moving *fast* and moving *safely* the same thing — enabling AI at scale while heading off the risks." | "…to enable scaling AI, increasing our speed of adoption and maturity, while making sure we do it securely and stay compliant." | 2, 3 |
| "**Build AI that lasts** — proper engineering discipline…" | "**Build sustainable AI systems**: proper engineering discipline…" | 10, 11 |
| "ungoverned AI opening the door to data leakage, prompt injection, and unvetted models." | "ungoverned AI opening the door to data leakage, confidentiality breach, loss of availability or loss of integrity." | 8 |
| "…where DR's real, un-solved decisions live:" | "…where we will add our specific guardrails, evals, rules, guidelines, QA, checks, human gates:" | 5, 8 |
| "This underpins the technology-selection mandate; without it, stack decisions are guesswork." | "This is an important base for target architectures and tech selections." | 4 |
| "This matters as much as the technical requirements. … A strong architect who cannot do this will produce blueprints nobody adopts." | "The Principal AI Architect has a strong ability to influence others through sound, well-thought arguments, leading by example." | 3, 4 |
| "Mandatory review is reserved for genuinely high-risk cases — anything touching personal data. Everything else flows through the paved road without sign-off, to avoid becoming a bottleneck." | "Mandatory review is reserved for high risk, high value, high cost or high impact use cases. Everything else goes through the agreed architecture and templates without explicit sign-off and subject to auditing." | 4, 8, 9 |
| (whole "## Success measures" section added by AI) | (section deleted) | 6 |

## Process

1. Read the draft and identify the tells: em-dash labels, consequence-punchlines, metaphors, tricolons, self-reference, generic examples, added scaffolding.
2. Rewrite each affected passage per the rules. Preserve all *information* — only remove *rhetoric*, or make abstractions concrete.
3. If a passage is abstract, ask the user for the real specifics rather than inventing them (rule 8 fails badly if you fabricate the concrete detail).
4. Show the result. Do not add a summary of "what I changed and why" unless asked — that is itself the meta-commentary rule 3 warns against.

## What NOT to do

- **Don't invent concrete details** to satisfy rule 8. If you don't know the real team/system/number, ask or leave a clear placeholder.
- **Don't strip information along with the rhetoric.** The goal is plainer, not thinner. A cut sentence should lose only flourish.
- **Don't over-correct into terse.** The user's register is plain and complete, not clipped. Full sentences, normal depth — just without the polish.
- **Don't replicate genuine typos or errors.** Human drafts contain them; that is evidence of hand-editing, not a style to imitate. Write clean plain prose.
- **Don't make every sentence identical in shape.** Plain ≠ monotonous. Natural repetition is fine (rule 13); mechanical repetition is not the target.

## Verification

- [ ] No em-dash after a bold label (colons instead)
- [ ] No consequence-punchlines at the ends of points
- [ ] No metaphor-per-paragraph; abstractions replaced with concrete specifics
- [ ] No unrequested scaffolding sections
- [ ] No self-referential meta-commentary ("this matters", "crucially", "it's worth noting")
- [ ] Written from the inside ("we"/"our") where appropriate
- [ ] All original information preserved — only rhetoric removed
- [ ] No fabricated specifics

---
name: compress-prose
description: Rewrite existing prose to its shortest form that preserves meaning. Use when asked to compress, tighten, condense, shorten, or make text terse; or when reviewing docs, READMEs, comments, commit messages, or specs for verbosity.
---

# Compress Prose

Rewrite the target text so every sentence carries information no other sentence carries, in the fewest words that keep the meaning.

## Procedure

1. Read the whole text. Note its purpose and audience.
2. For each section, paragraph, and sentence, ask: what does this add that the rest lacks? Delete it if the answer is nothing.
3. Rewrite what remains using the rules below.
4. Re-read the result. Verify every claim, constraint, and instruction of the original survives. Restore anything lost.
5. Return only the rewritten text unless asked for a diff or explanation.

## Rules

### Delete

- **Redundant assertions**: a point stated twice, a summary that repeats the body, a conclusion that restates the intro, an example that shows what the sentence already says.
- **Antithesis**: any "X, not Y" / "X rather than Y" / "X instead of Y" / "X — not Y" construction where Y merely negates X. Keep X. Keep Y only when Y is a plausible reading the reader would otherwise adopt.
- **Hedges and intensifiers**: "very", "really", "quite", "basically", "essentially", "it is important to note", "in order to", "the fact that".
- **Meta-commentary**: "this section describes", "as mentioned above", "it should be noted", "let's take a look at".
- **Throat-clearing openers and closers**: "In this document", "In summary", "Hopefully this helps".
- **Filler transitions** that carry no logical relation: "Additionally", "Furthermore", "Moreover", "That said".
- **Empty qualifiers**: "various", "certain", "a number of", "some kind of".

### Rewrite

- Replace a phrase with a word when one exists: "at this point in time" → "now"; "in the event that" → "if"; "has the ability to" → "can"; "make use of" → "use"; "is able to" → "can".
- Replace a clause with a phrase: "which is located in" → "in"; "that are responsible for" → "for".
- Prefer active voice and concrete subjects.
- Prefer a verb over its nominalization: "perform validation of" → "validate"; "make a decision" → "decide".
- Merge sentences that share a subject. Split sentences that carry two unrelated ideas.
- Collapse a list whose items differ only in a word into one sentence with that word varied.
- Replace a paragraph with a list when the paragraph enumerates. Replace a list with a sentence when the list has fewer than three short items.
- Cut a heading whose section is one sentence; fold the sentence into the parent.
- Drop an example when the rule is unambiguous without it. Keep one example when the rule is abstract.

### Keep

- Every fact, number, constraint, exception, and instruction.
- Structure: bullets, numbering, tables, etc, are good to keep unless clearly superfluous.
- Defined terms and the names of things (APIs, flags, files, people).
- Distinctions the reader would otherwise miss. When an antithesis marks such a distinction, keep it.
- Warnings about consequences.
- The tone the audience expects.

## Calibration

Terse whenever adequate. A rewrite is adequate when a reader with the intended background reaches the same understanding and takes the same action. Target: half the original word count for typical prose; a third for corporate or academic prose. Stop compressing when the next cut removes meaning.

## Example

Before:

> In this section, we will take a look at how the caching layer works. The caching layer is essentially responsible for storing the results of expensive computations so that they don't have to be recomputed every single time. It is important to note that the cache is an in-memory cache, not a disk-based one, which means that it will be cleared when the process restarts. In summary, the cache stores expensive results in memory and is lost on restart.

After:

> The cache stores results of expensive computations in memory; it is cleared when the process restarts.

---
name: frame
description: Frame a product idea into a concise anchor doc, branching sub-topics into focused folders for separate sessions. Use when the user invokes /frame or wants to sediment scope without losing focus to non-load-bearing noise.
disable-model-invocation: true
metadata:
  - based-on: grill-with-docs (Matt Pocock)
---

Interview me relentlessly about every aspect of this idea until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies one-by-one. For each question, provide your recommended answer.

Ask the questions one at a time, waiting for feedback before continuing.

If a question can be answered by exploring existing material, explore instead.

## Invocation

`/frame [arg]`:

- `@<path>` — focused re-entry on that file (resume).
- Free-form text — seed for a new root grill.
- No argument — ask the user to describe the idea.
- Ambiguous — ask.

## Artifact

The framing doc uses the scaffold defined in [FRAMING-FORMAT.md](./FRAMING-FORMAT.md). Five sections, recursively applied at every level:

1. One-liner
2. Problem
3. Mechanism
4. Insight
5. Out-of-scope

Opinionated default. Sections may be dropped when they don't earn their keep — but resist drops made out of laziness, not honest scope.

## File system

Default root: `~/docs/framing/<slug>/`. User can override with a path argument.

Self-named anchor at each level. Leaf-as-file, branched-as-folder:

```
~/docs/framing/some-product/
  some-product.md           ← root anchor
  pricing.md                ← leaf branch
  onboarding/               ← branched sub-topic
    onboarding.md           ← anchor at this level
    welcome-flow.md
    verification/           ← branched further
      verification.md
      mfa.md
```

When a leaf gains its own branches, convert it: `pricing.md` → `pricing/pricing.md`, then drop new siblings inside that folder.

Slug is kebab-case, derived from the crystallized One-liner. Skill proposes; user confirms or overrides.

## Process

Section ordering during the grill is fully opportunistic, including the One-liner. Probe wherever the user has heat.

**No file is written before the One-liner is good enough to slug on.** Until then, all material is held in conversation. Once the One-liner crystallizes:

1. Propose a slug, confirm.
2. Create `~/docs/framing/<slug>/<slug>.md`.
3. Dump in-memory material into the appropriate sections.
4. Continue iteratively — sections crystallize, write immediately. No batching.

On re-invocation against an existing file: always resume. Read existing content, treat as in-progress, bias questions toward gaps and tensions.

## Branching

Trigger a branch when:

- The trunk starts to bloat around a topic that deserves its own focus.
- The user explicitly asks to branch.
- The end-of-session pass catches something missed.

Mechanic — **queue, never stack**:

1. Create the new file at the right level (leaf, or convert a leaf to a folder per the FS rules).
2. Write a single line at the top: `Spawned from: <one-sentence reason>`.
3. Continue grilling the parent.

The branch is grilled later in a fresh `/frame @<path>` session.

## Focused sub-session re-entry

When `/frame @<path>` is invoked on a non-root file:

- Read the file (including the trigger note if still present).
- Walk up the directory tree and read each ancestor's self-named anchor.
- **Do not** enumerate siblings. **Do not** descend into children. The folder topology is the source of truth, but loading it back in defeats the zoned mindset.

First action of a focused session: internalize the trigger note, then **replace it** with the One-liner once that crystallizes for this sub-topic.

## Cross-level edits

A focused session may propose edits to ancestor files when an insight genuinely changes them. Always surface the proposed edit and require confirmation. Never silently mutate ancestors. No auto-revisit of the parent at end of session.

## End condition

Stop when the user says done. Then do one explicit pass over empty sections — for each, ask once: drop it or fill it. Respect the answer.

No polish pass.

The framing doc is a valid downstream input to `/to-prd` and `/spec-driven-development`, but invoking those is the user's call. Closing message: name the file path. That's it.

## Failure modes

- Writing to disk before the One-liner has crystallized.
- Loading siblings or descendants during focused re-entry.
- Automatic handoff to downstream skills.
- Polish pass after iterative writing.
- Silent ancestor mutation from a focused session.
- Premature scaffold filling in queued branch files (anything beyond the trigger note).
- Marching through sections in a fixed order instead of grilling where the user has heat.
- Creating empty placeholder folders before there is anything to put in them.

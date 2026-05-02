---
name: frame
description: Crystallize an idea into a handoff-ready artifact through a relentless one-question-at-a-time discovery process. Each scope becomes its own artifact under docs/frame/, with a shared glossary in DOMAIN.md. Use when the user has a thought, idea, or proposal that needs sharpening before it can be specced, prototyped, or iterated on.
metadata:
  - inspired-by: grill-with-docs (Matt Pocock)
---

# Frame

Crystallize an idea by resolving the dependencies between decisions, one at a time, until the framing is sharp enough to hand off. The output is a reference artifact that downstream work — spec, prototype, design, research — consumes.

Each domain scope produces its own artifact under `docs/frame/` — one scope per session. A shared glossary, `DOMAIN.md`, captures the language as it stabilizes.

This is not specification, design, or planning. It's not project management. No timelines, no milestones, no assignments. Just the idea itself, sharpened until it's ready for whatever comes next.

## What Frame guarantees (and what it doesn't)

A completed frame guarantees:

- A clear problem statement and scope boundary
- Resolved canonical language for the terms it uses
- Explicit out-of-scope items and stubbed sub-topics
- A list of assumptions that must hold for the framing to be valid
- Zero open questions that would block downstream spec work

A completed frame does NOT guarantee:

- A solution, design, or implementation plan
- Validation that the idea is worth pursuing
- Estimates, timelines, or resourcing

If a downstream reader has to come back and ask "what did you mean by X" or "did you consider Y" — the frame wasn't done.

## Tone

Dialectical skeptical. Firm, not contemptuous. Do not validate or soften — but do not manufacture friction either.

The user is a partner in discovery, not an opponent.

- No "great starting point", no "interesting direction", no "good question".
- If something is unclear, say it's unclear.
- If two things the user said contradict, point it out.
- If the user is internally consistent on a point, acknowledge it and move on. Don't invent contradictions for sport.
- Push back on fuzzy or overloaded terms. Propose a precise canonical term and force the user to pick.
- When the user uses a term that conflicts with `DOMAIN.md`, call it out before letting the conversation move on.

## Setup

Don't raise tensions yet. Gather information and get a sense of the landscape.

1. Frame the topic. Write back what the user said in your own words, and ask for confirmation.
2. Ask the user if they have existing features or requirements in mind. If so, ask them to list them. If not, ask them to describe the problem or opportunity in more detail.
3. Confirm the scope of _this_ frame. If the user is describing something that sounds like multiple frames, name that and pick one to start with — the others get stubbed.

## Process

1. **One question per turn.** Ask the question, state your recommended answer, wait. Never stack two questions. Never accept a batched answer to questions you didn't ask.
2. **Resolve dependencies first.** Identify the decision the rest of the discussion hangs on. Resolve it before its dependents. If two questions are mutually dependent, name the loop and pick the one to break it on.
3. **One scope per artifact.** When a tangent has its own decisions to make, it earns its own frame. Note it as a stub on the parent — don't derail the parent to chase it. Once a stub is grilled into its own child frame, remove it from the parent's stub list: the child frame is now where it lives.
4. **Concrete scenarios over abstractions.** When relationships are being asserted, invent a scenario that probes the boundary. _"A Customer cancels mid-checkout — does that produce an Invoice or not?"_ Force precision.
5. **Surface assumptions explicitly.** When a claim depends on something being true about the world, users, or systems, name it as an assumption. Assumptions accumulate in the frame's Assumptions section — they're what downstream validation work targets.
6. **Watch the depth.** If a frame is three levels deep in the tree, stop and ask whether the root is actually two or more ideas in a trenchcoat. Deep trees are usually a smell.
7. **Capture as you go.** When a term is resolved, update `DOMAIN.md` immediately. When a section of the current frame crystallizes, write it. No batching.
8. **Lazy writes.** Hold material in conversation until there is something concrete to write. Only then create the file.

## Done condition

A frame is done when:

- The Open Questions section contains nothing that would block spec
- All canonical terms used are in `DOMAIN.md`
- Assumptions are listed
- Stubs for deferred sub-topics are recorded
- The user explicitly confirms readiness to hand off

Anything else is parked under "Deferred questions" with a one-line reason for the deferral.

## Stub lifecycle

Stubs are queued sub-topics noted on a parent frame. They are not files. They have a shelf life.

- Each stub gets a one-line description and the date it was created.
- When a parent frame is reopened (revisited, revised, or referenced by new work), audit its stubs: still relevant, now obsolete, or ready to be promoted to a child frame?
- Stubs older than the user's chosen review interval (default: 90 days) get flagged on the parent for review next time it's opened. The user decides: keep, kill, or promote.
- A stub that's been deferred twice is a signal — either it's not actually important, or it's been wrongly scoped as a sub-topic when it's really independent.

## File structure

## File structure

```
docs/frame/
├── DOMAIN.md
├── 00-<root-slug>.md
├── 01-<child-slug>.md
├── 01-<child-slug>/          ← only created when 01 itself spawns children
│   ├── 01-<grandchild>.md
│   └── 02-<grandchild>.md
└── 02-<other-child>.md
```

- Numbering is zero-padded and scoped to each level. Root is `00-`. Direct children of the root start at `01-`. Each subfolder restarts at `01-`.
- A frame doc gains children by creating a sibling folder with the same slug. The original `.md` stays put; children live in the folder next to it.
- Slug is kebab-case, derived from the resolved one-liner. Propose, confirm, then create.
- See [FRAMING-FORMAT.md](./FRAMING-FORMAT.md) for the per-document format.

### Lazy creation

- Don't create `docs/frame/` until the first frame doc is ready to be written.
- Don't create `DOMAIN.md` until the first domain term is resolved.
- Don't create empty folders or stub files for queued sub-topics. A queued sub-topic is a one-line note on the parent frame, not a placeholder file.

## Glossary management (DOMAIN.md)

`DOMAIN.md` is the shared language. Format defined in [DOMAIN-FORMAT.md](./DOMAIN-FORMAT.md).

- **Challenge against the glossary.** When the user uses a term that conflicts with an existing entry, stop and resolve it. _"Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"_
- **Sharpen fuzzy language.** When the user uses a vague or overloaded term, propose a precise canonical term and ask which one is meant. _"You're saying 'account' — do you mean the **Customer** or the **User**? Those are different things."_
- **Update inline.** As soon as a term is settled, write it to `DOMAIN.md`. Don't queue it for later.
- **Flag conflicts in the doc itself.** When a term was used ambiguously and got resolved, record both the conflict and the resolution under "Flagged ambiguities".

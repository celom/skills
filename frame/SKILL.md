---
name: frame
description: Distill an idea through a relentless one-question-at-a-time discovery process. Each scope becomes its own artifact under docs/frame/, with a shared glossary in DOMAIN.md. Use when the user has a thought, idea, or proposal that needs sharpening before it can be acted on.
disable-model-invocation: true
metadata:
  - based-on: grill-with-docs (Matt Pocock)
---

# Frame

Distill an idea by resolving the dependencies between decisions, one at a time, until shared understanding is reached. Each domain scope produces its own artifact under `docs/frame/` - one scope/artifact per session. A shared glossary, `DOMAIN.md`, captures the language as it stabilizes.

This is not about specifying, designing or planning a solution. It's about getting to a clear, actionable artifact that can be used as a reference for whatever the next step is — whether that's implementation, design, or further research.

## Tone

Skeptical editor. Do not validate or soften.

The goal is to get to a clear, actionable artifact. Nonetheless, the process is conversational. The user is a partner in discovery, not a subject to be interrogated. The tone should be firm but collaborative.

- No "great starting point", no "interesting direction", no "good question".
- If something is unclear, say it's unclear.
- If two things the user said contradict, call it out.
- Push back on fuzzy or overloaded terms. Propose a precise canonical term and force the user to pick.
- When the user uses a term that conflicts with `DOMAIN.md`, call it out before letting the conversation move on.

## Process

1. **One question per turn.** Ask the question, state your recommended answer, wait. Never stack two questions. Never accept a batched answer to questions you didn't ask.
2. **Resolve dependencies first.** Identify the decision the rest of the discussion hangs on. Resolve it before its dependents. If two questions are mutually dependent, name the loop and pick the one to break it on.
3. **One scope per artifact.** When a tangent has its own decisions to make, it earns its own frame. Note it as an unresolved question on the parent — don't derail the parent scope to chase it. Once that question is grilled into its own child frame, remove it from the parent: the child frame is now where it lives, and the parent shouldn't carry a stale pointer.
4. **Concrete scenarios over abstractions.** When relationships are being asserted, invent a scenario that probes the boundary. _"A Customer cancels mid-checkout — does that produce an Invoice or not?"_ Force the user to be precise.
5. **Capture as you go.** When a term is resolved, update `DOMAIN.md` immediately. When a section of the current frame crystallizes, write it. No batching.
6. **Lazy writes.** Hold material in conversation until there is something concrete to write. Only then create the file.

## File structure

```
docs/frame/
├── DOMAIN.md
├── 000-<root-slug>.md
├── 001-<child-slug>.md
├── 001-<child-slug>/          ← only created when 001 itself spawns children
│   ├── 001-<grandchild>.md
│   └── 002-<grandchild>.md
└── 002-<other-child>.md
```

- Numbering is zero-padded and scoped to each level. Root is `000-`. Direct children of the root start at `001-`. Each subfolder restarts at `001-`.
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

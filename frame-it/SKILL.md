---
name: frame-it
description: Produce a hard-to-vary essence for one node of a foundation tree — the bird's-eye distillation of an idea, project, or topic. Use when the user wants to frame a topic, write a vision, distill an essence, or sharpen the load-bearing core of a document into something hard-to-vary. Operates on chat input, an external source doc, or an existing node.
---

# Frame It

Produce a **hard-to-vary essence** for one node of a foundation tree.

## What this is NOT

This is **not** a spec, PRD, plan, design doc, or feature list.

The artifact `frame-it` produces is a **baseline source-of-truth document** from which specs, PRDs, plans, and designs derive. It is upstream of all of those.

A frame does not list features. It does not enumerate user stories. It does not describe implementation. It captures the load-bearing essence — the part of an idea you cannot tweak without breaking the whole thing.

## What "hard-to-vary" means

(After Deutsch — _The Beginning of Infinity_.) An explanation is **hard-to-vary** when every detail plays a functional role: you cannot swap or drop any part without ruining the whole. The opposite — easy-to-vary — is the language of corporate mission statements: _"We help teams ship faster"_ survives any near-synonym substitution and means nothing.

This skill enforces hard-to-vary via five tests:

| Test             | Question                                                    | When applied                    |
| ---------------- | ----------------------------------------------------------- | ------------------------------- |
| **Negation**     | Could a reasonable competitor hold the opposite?            | Inline during grilling          |
| **Specificity**  | How many other ideas does this also describe? Aim for 1.    | Inline during grilling          |
| **Substitution** | Swap key words for near-synonyms — does it still read fine? | Final tightening pass           |
| **Subtraction**  | Remove a clause — does the essence still work?              | Final tightening pass           |
| **Falsifier**    | What observable evidence would prove this wrong?            | Required, written into artifact |

## Input modes

The skill detects the mode by inspecting the input:

- **Mode A — new node from chat.** No path given. User describes the topic conversationally.
  - Default: a new root node at `./foundation/FRAME.md`.
  - If the user wants this to be a child of an existing frame-shaped node, ask for (or accept) the parent path. Output goes into the parent's children directory per the path scheme in `../layer-it/SKILL.md` (step 1). The new file is created with `status: grilled` and its `Parent:` link points back to the parent file. The parent itself is **not modified** — children are discovered via the directory layout.
- **Mode B — non-frame-shaped source.** Path to a PRD, essay, notes, or any unstructured doc. Treat as **read-only source material**. Grill around it, distill an essence, ask where to write the output (default `./foundation/FRAME.md`).
- **Mode C — re-grill in place.** Path to an existing frame-shaped node (frontmatter + Carves/Falsifier per `NODE-FORMAT.md`). Load the existing essence as the starting point. Show a diff before writing.
  - If the node carries `status: stub`, this is a **graduation**: flip to `status: grilled` on write. Stubs are typically created by `layer-it`; graduating one is just Mode C with a status flip — no separate flow.

## Workflow

### 1. Setup

- Detect the input mode.
- If `./foundation/DOMAIN.md` exists, load it. Otherwise create it lazily — only when the first canonical term is resolved (see `DOMAIN-FORMAT.md`).
- For Mode B/C, load the source/existing artifact into context.
- Resolve the output path. For Mode A/B, ask the user if you can't infer cleanly.

### 2. Essence grill (interactive)

Open with: _"What's the essence here? What's the part you can't tweak without ruining the whole?"_

Iterate on drafts. As candidates emerge, **apply two tests inline**:

- **Negation.** _"Could a reasonable competitor hold the opposite of what you just said? If not, that's a sign it's vacuous."_
- **Specificity.** _"Could this same sentence also describe [other plausible project]? If yes, what's specific to this one?"_

If the user uses a domain term that conflicts with an existing entry in `DOMAIN.md`, **stop immediately** and surface the conflict. Don't paper over it.

If a new canonical term is needed, append it to `DOMAIN.md` **now** — not at end of session — so it's available for the rest of the conversation. Follow the schema in `DOMAIN-FORMAT.md`.

### 3. Falsifier grill

Once an essence holds, ask: _"What observable evidence would prove this is wrong?"_

Push until the answer is concrete and observable.

- ❌ "Users wouldn't like it."
- ✅ "Fewer than 10% of trial users return for a second session within a week."

If the user can't produce a falsifier, the essence likely isn't taking a position — loop back to step 2.

**Escape hatch — distinguishers.** Some framings (design philosophies, research directions, personal essays) genuinely don't take an empirically falsifiable position. In that case, accept a **distinguisher** instead: a concrete situation where this essence would lead to a different decision than its plausible alternatives. Write it on the `Falsifier:` line prefixed with `(distinguisher)` so future readers can tell it apart from a true falsifier. Don't reach for this escape hatch by default — only when an honest attempt at falsification fails.

### 4. Carves grill (only if not root)

If this node has a parent (Mode A with a parent specified, or Mode B/C where the file lives below `./foundation/FRAME.md`), ask:

> _"What slice of the parent does this node own that no sibling does? Why is this one of the parent's pillars and not redundant with another?"_

The answer becomes the **Carves:** line. For the root, this line reads `(root)`.

### 5. Final tightening pass

Apply the line-edit tests to the working essence:

- **Substitution.** For each key noun/verb, propose two near-synonyms and read the sentence with each. If any version reads fine, the original word wasn't load-bearing. Either drop the word, or replace it with the specific concept the slot actually demands (and promote that concept to `DOMAIN.md` if it's a domain term).
- **Subtraction.** Strike each clause in turn. If the essence still holds without it, drop it.

Then run the **DOMAIN.md conformance check**. Every domain noun in the artifact must be:

- (a) an existing canonical term in `DOMAIN.md`,
- (b) common English not specific to this project, or
- (c) a term promoted to canonical in this session.

No floating non-canonical terms.

### 6. Write

- Show the artifact draft (full content, including frontmatter).
- For **Mode C**, show a diff against the existing artifact.
- Ask for explicit confirmation before writing.
- Write the file following the template in `NODE-FORMAT.md`.
- If this is a fresh non-root node, set the new file's `Parent:` link to the parent's relative path. **Do not mutate the parent file** — children are discovered via the directory layout, not a `Children:` index.
- Verify any new canonical terms made it into `DOMAIN.md` (they should already be appended from step 2).

## Boundaries

- **Never delete files.** If a re-grill fundamentally changes the essence, the prior version lives in git history.
- **Don't scan the repository unless the user asks.** This skill operates inside `foundation/` only. If the user explicitly says "check this against the codebase" or names files outside `foundation/`, follow that instruction; otherwise, don't.
- **Don't write outside `foundation/`.** Source material in Mode B is **read-only**.

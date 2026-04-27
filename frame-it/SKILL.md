---
name: frame-it
description: Produce a hard-to-vary essence for one node of a foundation tree — the bird's-eye distillation of an idea, project, or topic. Use when the user wants to frame a topic, write a vision, distill an essence, or sharpen the load-bearing core of a document into something hard-to-vary. Operates on chat input, an external source doc, an existing stub, or an already-grilled node.
---

# Frame It

Produce a **hard-to-vary essence** for one node of a foundation tree.

This is a **depth move** — compress one node until only the load-bearing remains. It is the counterpart to `layer-it`, which decomposes a node into its pillars (a breadth move). Both skills share the same artifact contract (`NODE-FORMAT.md`) and glossary contract (`DOMAIN-FORMAT.md`).

## What this is NOT

Not a spec, PRD, plan, design doc, or feature list. The artifact `frame-it` produces is a **baseline source-of-truth document** from which specs, PRDs, plans, and designs derive. It is upstream of all of those.

A frame does not list features. It does not enumerate user stories. It does not describe implementation. It captures the load-bearing essence — the part of an idea you cannot tweak without breaking the whole thing.

## What "hard-to-vary" means

After Deutsch (_The Beginning of Infinity_): an explanation is **hard-to-vary** when every detail plays a functional role — you cannot swap or drop any part without ruining the whole. The opposite is the language of corporate mission statements: _"We help teams ship faster"_ survives any near-synonym substitution and means nothing.

Five tests enforce hard-to-vary:

| Test             | Question                                                    | When applied                |
| ---------------- | ----------------------------------------------------------- | --------------------------- |
| **Negation**     | Could a reasonable competitor hold the opposite?            | Inline during grilling      |
| **Specificity**  | How many other ideas does this also describe? Aim for 1.    | Inline during grilling      |
| **Substitution** | Swap key words for near-synonyms — does it still read fine? | Final tightening pass       |
| **Subtraction**  | Remove a clause — does the essence still work?              | Final tightening pass       |
| **Falsifier**    | What observable evidence would prove this wrong?            | Required, written into node |

## Discipline

- **One question at a time.** Wait for the answer before moving on.
- **Recommended answer.** Each question carries a recommendation grounded in the principles above (hard-to-vary tests, DOMAIN conformance) — not free-form opinion.
- **Stay inside `foundation/`.** Don't scan the rest of the repository unless the user explicitly invites it.

## Input dispatch

Behavior is selected from the input — no named modes.

| Input                                    | Behavior                                                                                                            |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Chat description (no path)               | Fresh node. Default a new root at `./foundation/FRAME.md`; if a parent path is supplied, place under the parent's children directory. |
| Source doc (path outside `foundation/`)  | Read-only source material. Grill around it; ask where to write the output (default `./foundation/FRAME.md`).        |
| Stub node (`status: stub`)               | **Graduation.** Produce the essence from scratch with parent and Carves slot prefilled by the stub. Flip `status: stub` → `grilled` on write. |
| Grilled node (`status: grilled`)         | **Evolution.** Load the existing essence as starting point. Show a diff before writing.                             |

## Workflow

### 1. Setup

- Identify the input and the corresponding behavior from the dispatch table above.
- If `./foundation/DOMAIN.md` exists, load it. Otherwise create it lazily — only when the first canonical term is resolved (see `DOMAIN-FORMAT.md`).
- Resolve the output path. For fresh nodes, ask the user if you can't infer cleanly.

### 2. Essence grill

Open with: _"What's the essence here? What's the part you can't tweak without ruining the whole?"_

Iterate on drafts. Apply two tests inline:

- **Negation.** _"Could a reasonable competitor hold the opposite of what you just said? If not, that's a sign it's vacuous."_
- **Specificity.** _"Could this same sentence also describe [other plausible project]? If yes, what's specific to this one?"_

If the user uses a domain term that conflicts with `DOMAIN.md`, **stop immediately** and surface the conflict. Don't paper over it. If a new canonical term is needed, append it to `DOMAIN.md` **now** — not at end of session — so it's available for the rest of the conversation. Follow `DOMAIN-FORMAT.md`.

### 3. Falsifier grill

Once an essence holds, ask: _"What observable evidence would prove this is wrong?"_ Push until the answer is concrete and observable.

- ❌ "Users wouldn't like it."
- ✅ "Fewer than 10% of trial users return for a second session within a week."

If no empirical falsifier honestly exists (design philosophies, research directions, personal essays), accept a **distinguisher** instead — a concrete situation where this essence would lead to a different decision than its plausible alternatives. Write it on the `Falsifier:` line prefixed with `(distinguisher)`. Don't reach for this by default; only when an honest attempt at falsification fails.

### 4. Carves grill (only if not root)

Ask: _"What slice of the parent does this node own that no sibling does? Why is this one of the parent's pillars and not redundant with another?"_

The answer becomes the **Carves:** line. For the root, this line reads `(root)`.

### 5. Final tightening pass

- **Substitution.** For each key noun/verb, propose two near-synonyms and read the sentence with each. If any version reads fine, the original word wasn't load-bearing. Either drop the word or replace it with the specific concept the slot demands (and promote that concept to `DOMAIN.md` if it's a domain term).
- **Subtraction.** Strike each clause in turn. If the essence still holds without it, drop it.
- **DOMAIN conformance.** Every domain noun in the artifact must be (a) an existing canonical term in `DOMAIN.md`, (b) common English not specific to this project, or (c) a term promoted to canonical in this session. No floating non-canonical terms.

### 6. Write

- Show the artifact draft (full content, including frontmatter).
- For evolution of an existing grilled node, show a diff against the prior version.
- Ask for explicit confirmation before writing.
- Write the file per `NODE-FORMAT.md`. If this is a fresh non-root node, set `Parent:` to the parent's relative path. **Never mutate the parent file** — children are discovered via the directory layout.
- For graduation, flip `status: stub` → `status: grilled` on write.

## Boundaries

- **Never delete files.** If a re-grill fundamentally changes the essence, the prior version lives in git history.
- **Don't write outside `foundation/`.** Source material is read-only.
- **Don't scan outside `foundation/`** unless the user explicitly invites it.

---
name: layer-it
description: Decompose a frame-shaped foundation node into its load-bearing pillars — the main vertical concepts that hold the parent's essence up. Use when the user wants to break down a frame, identify the main pillars of an idea, or extract the structural axes of a topic. Operates only on frame-shaped nodes.
---

# Layer It

Decompose a **frame-shaped node** into N **pillars** — the load-bearing axes that, together, hold the parent's essence up.

This is a **breadth move** — find the pillars beneath one node, no deeper. It is the counterpart to `frame-it` (a depth move). Both skills share the artifact contract (`../frame-it/NODE-FORMAT.md`) and glossary contract (`../frame-it/DOMAIN-FORMAT.md`).

The output is **stubs**, not grilled children. Pillars are conceptual axes — not modules, components, or work items. Detailing an individual pillar is `frame-it`'s job, run separately.

## Strict input contract

Operates **only on frame-shaped nodes** (per `../frame-it/NODE-FORMAT.md`). Pointed at a non-frame doc → **refuse** and tell the user to run `frame-it` on it first. Pillars only carry meaning when decomposing a parent that has a hard-to-vary essence.

## Rigor degrades with depth

Stub essences may be a single line. The 2–5 sentence guidance in `NODE-FORMAT.md` is for `grilled` nodes. Sub-pillars deeper in the tree carry less weight than direct children of the root. Push for rigor where the user wants the tree to load-bear deeply; accept lighter scaffolding at depth.

## Discipline

- **One question at a time.** Wait for the answer before moving on.
- **Recommended answer.** Each question carries a recommendation grounded in the set-level tests and DOMAIN conformance — not free-form opinion.
- **Stay inside `foundation/`.** Don't scan the rest of the repository unless the user explicitly invites it.

## Workflow

### 1. Setup

- Validate input is frame-shaped. If not → refuse, suggest `frame-it`.
- Load `./foundation/DOMAIN.md` if it exists.
- Children directory:
  - **Root (`./foundation/FRAME.md`)** → `./foundation/pillars/`
  - **Other node** at `<path>/<slug>.md` → `<path>/<slug>/`
- If children already exist → **revise mode** (step 4). Otherwise → fresh decomposition.

### 2. Draft and grill the set

Read the parent's essence and Carves. Propose 3–7 candidate pillars, each with a working title, one-line essence, and one-line Carves. Present them as a numbered list.

Apply the **set-level tests** — the hard-to-vary tests from `frame-it`, applied to the *set*:

| Test             | Question                                                                                                           |
| ---------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Substitution** | Replace a pillar with a near-synonym. Does the carving still feel load-bearing? If yes → it wasn't pulling weight. |
| **Subtraction**  | Drop a pillar. Does the parent feel underdescribed? If no → decoration.                                            |
| **Negation**     | State an alternative carving along a different axis. If both work equally → the chosen axis isn't justified.       |
| **Specificity**  | Could this set decompose a *different* parent? If yes → too generic.                                               |

**DOMAIN conformance** on every pillar name and Carves line. `layer-it` follows the existing canonical language but does not promote new terms — that's `frame-it`'s job. If a pillar genuinely needs a new term, queue it for graduation (step 5).

**Cardinality**, soft 3–7 band — challenge but don't refuse:
- N < 3 → _"Binary worldview — is there really no third axis?"_
- N > 7 → _"This looks like a list, not a carving. Can any be merged, or are some descendants of others?"_

Iterate until the set holds.

### 3. Write

For each pillar:

- Create the children directory if missing.
- Write per `../frame-it/NODE-FORMAT.md`. Frontmatter `status: stub`. Title, one-line essence, Carves, placeholder Falsifier `(to be defined when graduated)`.
- `Parent:` → relative path to the parent file.
- File name: `NN-<slug>.md` — zero-padded order from step 2's list, kebab-case slug.

The parent file is **never mutated** — children are discovered via the directory listing, which *is* the index.

### 4. Revise mode (only if children already exist)

For each existing child, ask: **keep / revise / drop**. Then ask whether to add new pillars (run step 2 for additions only).

Drops move the file (and its sub-tree) to `./foundation/_deprecated/`, preserving the relative path. **Never `rm`.**

### 5. Graduate (default-offered)

Ask: _"Want to graduate any of these stubs to `grilled` now? I'll run `frame-it` on each."_

If yes → run `frame-it` on each selected stub. (`frame-it` recognizes `status: stub` via frontmatter and dispatches into graduation behavior.) If no → exit cleanly; the user can run `frame-it` on any stub later.

## Boundaries

- **Never delete files.** Drops move to `./foundation/_deprecated/`, preserving the path.
- **Don't write outside `foundation/`.**
- **Don't accept non-frame-shaped input.**
- **Don't create or modify `DOMAIN.md`** — that's `frame-it`'s job.
- **One level per invocation.** Layering deeper is a separate invocation on the new child.
